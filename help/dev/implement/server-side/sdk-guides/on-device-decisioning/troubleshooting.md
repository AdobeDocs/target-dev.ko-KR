---
title: 온디바이스 의사 결정 문제 해결
description: '[!UICONTROL on-device decisioning] 문제 해결 방법 알아보기'
exl-id: e76f95ce-afae-48e0-9dbb-2097133574dc
feature: APIs/SDKs
source-git-commit: 1d892d4d4d6f370f7772d0308ee0dd0d5c12e700
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 0%

---

# 문제 해결 [!UICONTROL on-device decisioning]

## 구성 확인

### 단계 요약

1. `logger`이(가) 구성되어 있는지 확인합니다.
1. [!DNL Target] 추적이 활성화되었는지 확인
1. 정의된 폴링 간격에 따라 [!UICONTROL on-device decisioning] *규칙 아티팩트*&#x200B;가 검색되고 캐시되었는지 확인하십시오.
1. 양식 기반 경험 작성기를 통해 테스트 [!UICONTROL on-device decisioning] 활동을 만들어 캐시된 규칙 아티팩트를 통해 콘텐츠 전달의 유효성을 검사합니다.
1. Inspect 알림 전송 오류

## 1. 로거가 구성되어 있는지 확인합니다

SDK를 초기화할 때 로깅을 활성화했는지 확인하십시오.

**Node.js**

Node.js SDK의 경우 `logger` 개체를 제공해야 합니다.

```js {line-numbers="true"}
const CONFIG = {
  client: "<your client code>",
  organizationId: "<your organization ID>",
  logger: console
};
```

**Java SDK**

`ClientConfig`에서 Java SDK `logRequests`을(를) 사용하도록 설정해야 합니다.

```js {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("<your client code>")
  .organizationId("<your organization ID>")
  .logRequests(true)
  .build();
```

또한 JVM은 다음 명령줄 매개 변수로 시작해야 합니다.

```bash {line-numbers="true"}
java -Dorg.slf4j.simpleLogger.defaultLogLevel=DEBUG ...
```

## 2.[!DNL Target]추적이 활성화되었는지 확인

추적을 사용하도록 설정하면 [!DNL Adobe Target]에서 규칙 아티팩트와 관련된 추가 정보를 출력합니다.

1. [!DNL Experience Cloud]의 [!DNL Target]UI로 이동합니다.

   ![대체 이미지](assets/asset-target-ui-1.png)

1. **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**(으)로 이동한 다음 **[!UICONTROL Generate New Authorization Token]**&#x200B;을(를) 클릭합니다.

   ![대체 이미지](assets/asset-target-ui-2.png)

1. 새로 생성된 인증 토큰을 클립보드에 복사하고 [!DNL Target]요청에 추가합니다.

   **Node.js**

   ```js {line-numbers="true"}
   const request = {
     trace: {
       authorizationToken: "88f1a924-6bc5-4836-8560-2f9c86aeb36b"
     },
     execute: {
       mboxes: [{
         name: "sdk-mbox"
       }]
   }};
   ```

   **Java**

   ```js {line-numbers="true"}
   Trace trace = new Trace()
     .authorizationToken("88f1a924-6bc5-4836-8560-2f9c86aeb36b");
   Context context = new Context()
     .channel(ChannelType.WEB);
   MboxRequest mbox = new MboxRequest()
     .name("sdk-mbox")
     .index(0);
   ExecuteRequest executeRequest = new ExecuteRequest()
     .mboxes(Arrays.asList(mbox));
   
   TargetDeliveryRequest request = TargetDeliveryRequest.builder()
     .trace(trace)
     .context(context)
     .execute(executeRequest)
     .build();
   ```

1. 로거 및 추적을 적절히 사용하여 앱을 시작하고 서버 터미널을 모니터링합니다. 로거의 다음 출력에서 규칙 아티팩트가 검색되었음을 확인합니다.

   **Node.js SDK**

   ```text {line-numbers="true"}
     AT: LD.ArtifactProvider fetching artifact - https://assets.adobetarget.com/your-client-code/production/v1/rules.json
     AT: LD.ArtifactProvider artifact received - status=200
   ```

## 3. 정의된 폴링 간격에 따라 [!UICONTROL on-device decisioning] *규칙 아티팩트*&#x200B;가 검색 및 캐시되었는지 확인합니다.

1. 폴링 간격(기본값: 20분) 기간을 기다린 후 SDK에서 아티팩트를 가져오는지 확인하십시오. 동일한 터미널 로그가 출력됩니다.

   또한 [!DNL Target]Trace의 정보를 규칙 아티팩트에 대한 세부 정보와 함께 터미널에 출력해야 합니다.

   ```text {line-numbers="true"}
   "trace": {
     "clientCode": "your-client-code",
     "artifact": {
       "artifactLocation": "https://assets.adobetarget.com/your-client-code/production/v1/rules.json",
       "pollingInterval": 300000,
       "pollingHalted": false,
       "artifactVersion": "1.0.0",
       "artifactRetrievalCount": 10,
       "artifactLastRetrieved": "2020-09-20T00:09:42.707Z",
       "clientCode": "your-client-code",
       "environment": "production",
       "generatedAt": "2020-09-22T17:17:59.783Z"
     },
   ```

## 4. 양식 기반 경험 작성기를 통해 테스트 [!UICONTROL on-device decisioning] 활동을 만들어 캐시된 규칙 아티팩트를 통해 콘텐츠 배달을 확인합니다

1. Experience Cloud의 [!DNL Target]UI로 이동

   ![대체 이미지](assets/asset-target-ui-1.png)

1. 양식 기반 경험 작성기를 사용하여 새 XT 활동을 만듭니다.

   ![대체 이미지](assets/asset-form-base-composer-ui.png)

1. [!DNL Target]요청에 사용된 mbox 이름을 XT 활동의 위치로 입력합니다(이 이름은 개발용으로만 고유한 mbox 이름이어야 함).

   ![대체 이미지](assets/asset-mbox-location-ui.png)

1. 콘텐츠를 HTML 오퍼 또는 JSON 오퍼로 변경합니다. 이 요청은 응용 프로그램에 대한 [!DNL Target]요청에서 반환됩니다. 활동에 대한 타깃팅을 &#39;모든 방문자&#39;로 두고 원하는 지표를 선택합니다. 활동의 이름을 지정하고, 저장한 다음 활성화하여 사용 중인 mbox/위치가 개발용으로만 사용되도록 합니다.

   ![대체 이미지](assets/asset-target-content-ui.png)

1. 응용 프로그램에서 [!DNL Target]요청의 응답에서 받은 콘텐츠에 대한 로그 문을 추가합니다.

   **Node.js SDK**

   ```js {line-numbers="true"}
   try {
     const response = await targetClient.getOffers({ request });
     console.log('Response: ', response.response.execute.mboxes[0].options[0].content);
   } catch (error) {
     console.error('Something went wrong', error);
   }
   ```

   **Java SDK**

   ```js {line-numbers="true"}
   try {
     Context context = new Context()
       .channel(ChannelType.WEB);
     MboxRequest mbox = new MboxRequest()
       .name("sdk-mbox")
       .index(0);
     ExecuteRequest executeRequest = new ExecuteRequest()
       .mboxes(Arrays.asList(mbox));
   
     TargetDeliveryRequest request = TargetDeliveryRequest.builder()
       .context(context)
       .decisioningMethod(DecisioningMethod.ON_DEVICE)
       .execute(executeRequest)
       .build();
   
       TargetDeliveryResponse response = targetClient.getOffers(request);
     logger.debug("Response: ", response.getResponse().getExecute().getMboxes().get(0).getOptions().get(0).getContent());
   } catch (Exception exception) {
     logger.error("Something went wrong", exception);
   }
   ```

1. 터미널의 로그를 검토하여 콘텐츠가 게재되고 있는지, 그리고 콘텐츠가 서버의 규칙 아티팩트를 통해 게재되었는지 확인합니다. `LD.DeciscionProvider` 개체는 활동 자격 및 의사 결정이 규칙 아티팩트를 기반으로 디바이스에서 결정되면 출력됩니다. 또한 `content`의 로그로 인해 `<div>test</div>`이(가) 표시되거나 테스트 활동을 만들 때 응답이 (이)라고 결정되었습니다.

   **로거 출력**

   ```text {line-numbers="true"}
   AT: LD.DecisionProvider {...}
   AT: Response received {...}
   Response:  <div>test</div>
   ```

## Inspect 알림 전송 오류

온디바이스 의사 결정을 사용할 때 getOffers 실행 요청에 대해 알림이 자동으로 전송됩니다. 이러한 요청은 백그라운드에서 자동으로 전송됩니다. `sendNotificationError` 이벤트를 구독하면 모든 오류를 검사할 수 있습니다. 다음은 Node.js SDK를 사용하여 알림 오류에 가입하는 방법을 보여 주는 코드 샘플입니다.

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
let client;

function onSendNotificationError({ notification, error }) {
  console.log(
    `There was an error when sending a notification: ${error.message}`
  );
  console.log(`Notification Payload: ${JSON.stringify(notification, null, 2)}`);
}

async function targetClientReady() {
  const request = {
    context: { channel: "web" },
    execute: {
      mboxes: [{
        name: "a1-serverside-ab",
        index: 1
      }]
    }
  };
  const targetResponse = await client.getOffers({ request });
}

client = TargetClient.create({
  events: {
    clientReady: targetClientReady,
    sendNotificationError: onSendNotificationError
  }
});
```

## 일반적인 문제 해결 시나리오

문제가 발생하면 [!UICONTROL on-device decisioning]에 대해 [지원되는 기능](supported-features.md)을(를) 검토하십시오.

### 지원되지 않는 대상 또는 활동으로 인해 온디바이스 의사 결정 활동이 실행되지 않음

대상이 사용 중이거나 활동 유형이 지원되지 않아 [!UICONTROL on-device decisioning] 활동이 실행되지 않는 문제가 발생할 수 있습니다.

(1) 로거 출력을 사용하여 응답 개체에 있는 추적 속성의 항목을 검토합니다. 특히 캠페인 속성을 식별합니다.

**추적 출력**

```text {line-numbers="true"}
  "execute": {
  "mboxes": [
    {
      "name": "your-mbox-name",
      "index": 0,
      "trace": {
        "clientCode": "your-client-code",
        ...
        "campaigns": [],
        ...
      }
    }
```

대상 또는 활동 유형이 지원되지 않으므로 자격을 부여하려는 활동이 `campaigns` 속성에 없습니다. 활동이 `campaigns` 속성 아래에 나열되는 경우 지원되지 않는 대상 또는 활동 유형으로 인해 문제가 발생하지 않습니다.

(2) 또한 로거 출력에서 `trace` > `artifact` > `artifactLocation`을(를) 확인하여 `rules.json` 파일을 찾은 다음 `rules` > `mboxes` 속성에서 활동이 누락되었음을 확인합니다.

**로거 출력**

```text {line-numbers="true"}
 ...
 rules: {
   mboxes: { },
   views: { }
 }
```

마지막으로 [!DNL Target]UI로 이동하여 해당 활동을 찾습니다. [experience.adobe.com/target](https://experience.adobe.com/target)

대상자에서 사용된 규칙을 검토하고 지원되는 앞서 언급한 규칙만 사용하는지 확인하십시오. 또한 활동 유형이 A/B 또는 XT인지 확인합니다.

![대체 이미지](assets/asset-target-audience-ui.png)

### 부적격 대상자로 인해 온디바이스 의사 결정 활동이 실행되지 않음

온디바이스 의사 결정 활동이 실행되고 있지 않지만 rules.json 파일에 활동이 포함되어 있는지 확인한 경우 다음 단계를 수행하십시오.

(1) 애플리케이션에서 실행 중인 mbox가 활동이 사용 중인 mbox와 동일한지 확인합니다.

>[!BEGINTABS]

>[!TAB rule.json]

```text {line-numbers="true"}
 ...
 rules: {
   mboxes: {
    target-only-node-sdk-mbox: [{ // this mbox name must match the mbox in your request
      ...
    }]
   }
 ...
```

>[!TAB Node.js SDK]

```js {line-numbers="true"}
 const request = {
   trace: {
     authorizationToken: '2dfc1dce-1e58-4e05-bbd6-a6725893d4d6'
   },
   execute: {
     mboxes: [{
       address: getAddress(req),
       name: "target-only-node-sdk-mbox-two" // this mbox name must match the mbox the activity is using
     }]
   }};
```

>[!TAB Java SDK]

```js {line-numbers="true"}
Context context = new Context()
  .channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("target-only-node-sdk-mbox-two")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .decisioningMethod(DecisioningMethod.ON_DEVICE)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse response = targetClient.getOffers(request);
```

>[!ENDTABS]

(2) 추적 출력의 `matchedRuleConditions` 또는 `unmatchedRuleConditions` 속성을 검토하여 사용자의 활동 대상에 대해 자격이 있는지 확인합니다.

**추적 출력**

```text {line-numbers="true"}
...
},
"campaignId": 368564,
"campaignType": "landing",
"matchedSegmentIds": [],
"unmatchedSegmentIds": [
  6188838
      ],
      "matchedRuleConditions": [],
          "unmatchedRuleConditions": [
            {
              "in": [
                "true",
                {
                  "var": "mbox.auth_lc"
                }
              ]
            }
          ]
    ...
```

일치하지 않는 규칙 조건이 있는 경우 활동에 대한 자격이 없으므로 활동이 실행되지 않습니다. 대상의 규칙을 검토하여 자격이 없는 이유를 확인하십시오.

### 온디바이스 의사 결정 활동이 실행되지 않지만 원인이 명확하지 않음

온디바이스 의사 결정 활동이 실행되지 않는 이유는 명확하지 않을 수 있습니다. 이 경우 다음 문제 해결 단계를 따라 문제를 식별하십시오.

(1) 콘솔에서 로거 추적 출력을 읽고 다음과 유사한 아티팩트 속성을 식별합니다.

**추적 출력**

```text {line-numbers="true"}
...
      "artifact": {
          "artifactLocation": "https://assets.adobetarget.com/your-client-code/production/v1/rules.json",
          "pollingInterval": 300000,
          "pollingHalted": false,
          "artifactVersion": "1.0.0",
          "artifactRetrievalCount": 3,
          "artifactLastRetrieved": "2020-10-16T00:56:27.596Z",
          "clientCode": "adobeinterikleisch",
          "environment": "production"
        },
...
```

아티팩트의 `artifactLastRetrieved` 날짜를 확인하고 앱에 최신 `rules.json` 파일을 다운로드했는지 확인하십시오.

(2) 로거 출력에서 `evaluatedCampaignTargets` 속성을 찾습니다.

**로거 출력**

```text {line-numbers="true"}
...
  "evaluatedCampaignTargets": [
      {
        "context": {
          "current_timestamp": 1602812599608,
          "current_time": "0143",
          "current_day": 5,
          "user": {
            "browserType": "unknown",
            "platform": "Unknown",
            "locale": "en",
            "browserVersion": -1
          },
          "page": {
            "url": "localhost:3000/",
            "path": "/",
            "query": "",
            "fragment": "",
            "subdomain": "",
            "domain": "3000",
            "topLevelDomain": "",
            "url_lc": "localhost:3000/",
            "path_lc": "/",
            "query_lc": "",
            "fragment_lc": "",
            "subdomain_lc": "",
            "domain_lc": "3000",
            "topLevelDomain_lc": ""
          },
          "referring": {
            "url": "localhost:3000/",
            "path": "/",
            "query": "",
            "fragment": "",
            "subdomain": "",
            "domain": "3000",
            "topLevelDomain": "",
            "url_lc": "localhost:3000/",
            "path_lc": "/",
            "query_lc": "",
            "fragment_lc": "",
            "subdomain_lc": "",
            "domain_lc": "3000",
            "topLevelDomain_lc": ""
          },
          "geo": {},
          "mbox": {},
          "allocation": 23.79
        },
        "campaignId": 368564,
        "campaignType": "landing",
        "matchedSegmentIds": [],
        "unmatchedSegmentIds": [
          6188838
        ],
        "matchedRuleConditions": [],
        "unmatchedRuleConditions": [
          {
            "in": [
              "true",
              {
                "var": "mbox.auth_lc"
              }
            ]
          }
        ]
...
```

(3) `context`, `page` 및 `referring` 데이터를 검토하여 활동의 타기팅 자격에 영향을 줄 수 있으므로 예상대로 적용되는지 확인하십시오.

(4) `campaignId`을(를) 검토하여 실행해야 하는 활동을 평가합니다. `campaignId`은(는) [!DNL Target]UI의 활동 개요 탭에 있는 활동 ID와 일치합니다.

![대체 이미지](assets/asset-activity-id-target-ui.png)

(5) `matchedRuleConditions` 및 `unmatchedRuleConditions`을(를) 검토하여 특정 활동에 대한 대상 규칙에 적합한 문제를 식별하십시오.

(6) 최신 `rules.json` 파일을 검토하여 로컬에서 실행할 활동이 포함되어 있는지 확인하십시오. 위치는 1단계에서 위에 참조됩니다.

(7) 요청 및 활동에서 동일한 mbox 이름을 사용하고 있는지 확인합니다.

(8) 지원되는 대상 규칙 및 지원되는 활동 유형을 사용하고 있는지 확인합니다.

### [!DNL Target]사용자 인터페이스의 mbox 아래에 있는 활동 설정에 &quot;On Device Decisioning Propriable&quot;이 표시되어 있어도 서버 호출이 수행됩니다

장치가 온디바이스 의사 결정에 적합함에도 불구하고 서버 호출이 수행되는 몇 가지 이유는 다음과 같습니다.

* &quot;온디바이스 의사 결정 적격&quot; 활동에 사용된 mbox가 &quot;온디바이스 의사 결정 적격&quot;이 아닌 다른 활동에도 사용되면 mbox는 `rules.json` 아티팩트의 `remoteMboxes` 섹션 아래에 나열됩니다. mbox가 `remoteMboxes` 아래에 나열되면 해당 mbox에 대한 `getOffer(s)` 호출로 인해 서버가 호출됩니다.

* 작업 영역/속성에서 활동을 설정하고 SDK를 구성할 때 이를 포함하지 않으면 기본 작업 영역의 `rules.josn`이(가) 다운로드될 수 있으며 `remoteMboxes` 섹션 아래에서 mbox를 사용할 수 있습니다.
