---
title: Experience Cloud A4T 보고와 통합
description: Experience Cloud, A4T 보고, Analytics for Target 통합과 통합
keywords: 배달 api, 서버측, 서버측, 통합, a4t
exl-id: 0d09d7a1-528d-4e6a-bc6c-f7ccd61f5b75
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 7%

---

# A4T (Analytics for Target) 보고

[!DNL Adobe Target]은(는) 온디바이스 의사 결정 및 서버측 Target 활동 모두에 대한 A4T 보고를 지원합니다. A4T 보고를 활성화하는 두 가지 구성 옵션이 있습니다.

* [!DNL Adobe Target]이(가) 분석 페이로드를 [!DNL Adobe Analytics]에 자동으로 전달하거나
* 사용자가 [!DNL Adobe Target]에서 분석 페이로드를 요청합니다. ([!DNL Adobe Target]이(가) [!DNL Adobe Analytics] 페이로드를 호출자에게 다시 반환합니다.)

>[!NOTE]
>
>온디바이스 의사 결정은 [!DNL Adobe Target]이(가) Analytics 페이로드를 [!DNL Adobe Analytics]에 자동으로 전달하는 A4T 보고만 지원합니다. [!DNL Adobe Target]에서 분석 페이로드를 검색할 수 없습니다.

## 전제 조건

1. [!DNL Adobe Analytics]을(를) 보고 소스로 사용하여 [!DNL Adobe Target] UI에서 활동을 구성하고 계정이 A4T에 대해 활성화되었는지 확인하십시오.
1. API 사용자는 Adobe Marketing Cloud 방문자 ID를 생성하고, Target 요청이 실행될 때 이 ID를 사용할 수 있도록 합니다.

## [!DNL Adobe Target]에서 Analytics 페이로드를 자동으로 전달합니다.

다음 식별자가 제공되면 [!DNL Adobe Target]이(가) analytics 페이로드를 [!DNL Adobe Analytics]에 자동으로 전달할 수 있습니다.

1. `supplementalDataId`: [!DNL Adobe Analytics]에서 [!DNL Adobe Target] 사이를 연결하는 데 사용되는 ID입니다. [!DNL Adobe Target]과(와) [!DNL Adobe Analytics]이(가) 데이터를 올바르게 결합하려면 동일한 `supplementalDataId`을(를) [!DNL Adobe Target]과(와) [!DNL Adobe Analytics] 모두에 전달해야 합니다.
1. `trackingServer`: [!DNL Adobe Analytics] 서버입니다.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {     
    id: {
      marketingCloudVisitorId : "2304820394812039",
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId:"23423432"
    },
    experienceCloud: {
      analytics: {
        logging: "server_side",
        supplementalDataId: "7D3AA246CC99FD7F-1B3DD2E75595498E",
        trackingServer: "jimsbrims.sc.omtrds.net"
      }
    }, 
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }       
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .tntId("d359234570e044f14e1faeeba02d6ab23439914e.35_0")
  .thirdPartyId("B234A029348")
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

AnalyticsRequest analyticsRequest =
    new AnalyticsRequest()
        .trackingServer("jimsbrims.sc.omtrds.net")
        .logging(LoggingType.SERVER_SIDE)
        .supplementalDataId("7D3AA246CC99FD7F-1B3DD2E75595498E");
ExperienceCloud expCloud =
    new ExperienceCloud()
        .setAnalytics(analyticsRequest);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .experienceCloud(expCloud)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

## 사용자가 [!DNL Adobe Target]에서 분석 페이로드를 검색합니다.

사용자는 지정된 mbox에 대한 [!DNL Adobe Analytics] 페이로드를 검색한 다음 [데이터 삽입 API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)를 통해 [!DNL Adobe Analytics]에 보낼 수 있습니다. [!DNL Adobe Target] 요청이 실행되면 `client_side`을(를) 요청의 `logging` 필드에 전달합니다. 지정된 mbox가 Analytics를 보고 소스로 사용하는 활동에 있는 경우 페이로드를 반환합니다.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};
const targetClient = TargetClient.create(CONFIG);
targetClient.getOffers({
  request: {     
    id: {
      marketingCloudVisitorId : "2304820394812039",
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId:"23423432"
    },
    experienceCloud: {
      analytics: {
        logging: "client_side"
      }
    },  
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }       
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .tntId("d359234570e044f14e1faeeba02d6ab23439914e.35_0")
  .thirdPartyId("B234A029348")
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

AnalyticsRequest analyticsRequest =
    new AnalyticsRequest()
        .logging(LoggingType.CLIENT_SIDE);
ExperienceCloud expCloud =
    new ExperienceCloud()
        .setAnalytics(analyticsRequest);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .experienceCloud(expCloud)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

`logging = client_side`을(를) 지정하면 mbox 필드에 페이로드를 받게 됩니다.

Target의 응답에 `analytics -> payload` 속성의 항목이 포함되어 있으면 그대로 [!DNL Adobe Analytics]에 전달하십시오. [!DNL Adobe Analytics]은(는) 이 페이로드를 처리하는 방법을 알고 있습니다. 이 작업은 다음 형식을 사용하여 GET 요청에서 수행할 수 있습니다.

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/0/CODEVERSION?pe=tnt&tnta={payload}&mid={mid}&vid={vid}&aid={aid}
```

### 쿼리 문자열 매개 변수 및 변수

| 필드 이름 | 필수 | 설명 |
| --- | --- | --- |
| `rsid` | 예 | 보고서 세트 ID |
| `pe` | 예 | 페이지 이벤트. 항상 `tnt`(으)로 설정 |
| `tnta` | 예 | `analytics -> payload -> tnta`의 Target 서버에서 반환된 Analytics 페이로드 |
| `mid` | 예 | Marketing Cloud 방문자 ID |

### 필수 헤더 값

| 헤더 이름 | 헤더 값 |
| --- | --- |
| 호스트 | Analytics 데이터 수집 서버(예: `adobeags421.sc.omtrdc.net`) |

### 샘플 A4T 데이터 삽입 HTTP Get 호출

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0?pe=tnt&tnta=285408:0:0|2&mid=2304820394812039
```
