---
title: 사용자 식별 및 버킷팅
description: 사용자 식별 및 버킷팅
exl-id: 4fcf235b-6a58-442c-ae13-9d05ec1033fc
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 5%

---

# 사용자 식별 및 버킷팅

## 사용자 식별

내에서 사용자를 식별할 수 있는 방법에는 여러 가지가 있습니다 [!DNL Adobe Target]. [!UICONTROL Target] 는 다음 식별자를 사용합니다.

| 필드 이름 | 설명 |
| --- | --- |
| `tntID` | 다음 `tntId` 는 의 기본 식별자입니다. [!DNL Target] 사용자용입니다. 이 ID를 제공하거나 [!DNL Target] 요청에 포함되지 않은 경우 이 자동으로 생성됩니다. |
| `thirdPartyId` | 다음 `thirdPartyId` 는 모든 호출과 함께 보낼 수 있는 사용자의 회사 식별자입니다. 사용자가 회사 사이트에 로그인하면 일반적으로 회사는 방문자 계정, 로열티 카드, 멤버십 번호 또는 해당 회사에 대한 기타 적용 가능한 식별자에 연결되는 ID를 만듭니다. |
| `marketingCloudVisitorId` | 다음 `marketingCloudVisitorId` 는 서로 다른 Adobe 솔루션 간에 데이터를 병합하고 공유하는 데 사용됩니다. marketingCloudVisitorId는 Adobe Analytics 및 Adobe Audience Manager과의 통합에 필요합니다. |
| `customerIds` | Experience Cloud 방문자 ID와 함께, 추가 [고객 ID](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) 각 방문자에 대한 인증된 상태를 활용할 수도 있습니다. |

## [!DNL Target] ID (tntID)

다음 [!DNL Target] ID 또는 `tntId`는 장치 ID로 간주할 수 있습니다. 이 `tntId` 다음에 의해 자동으로 생성됨: [!DNL Adobe Target] 요청에 제공되지 않는 경우. 후속 요청에는 이 항목이 포함되어야 합니다. `tntId` 동일한 사용자가 사용하는 장치에 올바른 콘텐츠를 게재할 수 있습니다.

다음 샘플 호출에서는 `tntId` 이(가)에 전달되지 않습니다. [!DNL Target].

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
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

>[!TAB Java SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

가 없을 때 `tntId`, [!DNL Adobe Target] 다음을 생성합니다. `tntId` 와 는 다음과 같이 응답에 제공합니다.

```json {line-numbers="true"}
{
  "status": 200,
  "requestId": "5b586f83-890c-46ae-93a2-610b1caa43ef",
  "client": "acmeclient",
  "id": {
      "tntId": "10abf6304b2714215b1fd39a870f01afc.35_0"
  },
  "edgeHost": "mboxedge35.tt.omtrdc.net",
  ...
}
```

이 예에서 은 `tntId` 은(는) `10abf6304b2714215b1fd39a870f01afc.35_0`. 이 점을 참고하십시오. `tntId` 는 세션 간 동일한 사용자에 대해 사용해야 합니다.

## 타사 ID(thirdPartyId)

조직에서 ID를 사용하여 방문자를 식별하는 경우 다음을 사용할 수 있습니다 `thirdPartyID` 콘텐츠를 게재할 수 있습니다. A `thirdPartyID` 는 최종 사용자가 웹, 모바일 또는 IoT 채널에서 비즈니스와 상호 작용하는지 여부에 관계없이 귀사에서 최종 사용자를 식별하는 데 사용하는 영구 ID입니다. 즉, `thirdPartyId` 은 여러 채널에서 사용할 수 있는 사용자 프로필 데이터를 참조합니다. 그러나 다음을 제공해야 합니다. `thirdPartyID` 마다 [!DNL Adobe Target] 게재 API 호출.

다음 샘플 호출에서는 `thirdPartyId`.

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      thirdPartyId: "B234A029348"
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

>[!TAB Java SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .thirdPartyId("B234A029348");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

이 시나리오에서는 [!DNL Adobe Target] 다음을 생성합니다. `tntId` 제공된 에 매핑될 원래 호출로 전달되지 않았기 때문입니다 `thirdPartyId`.

## Marketing Cloud 방문자 ID(marketingCloudVisitorId)

다음 `marketingCloudVisitorId` 는 Adobe Experience Cloud의 모든 솔루션에서 방문자를 식별하는 범용 및 영구 ID입니다. 조직이 ID 서비스를 구현하면 이 ID를 사용하여 다음을 포함한 다른 Experience Cloud 솔루션에서 동일한 사이트 방문자와 해당 데이터를 식별할 수 있습니다. [!DNL Adobe Target], Adobe Analytics 및 Adobe Audience Manager. 다음을 참고하십시오. `marketingCloudVisitorId` 을(를) 통합할 때 필요합니다. [!DNL Target] 포함 [!DNL Adobe Analytics] 및 [!DNL Adobe Audience Manager].

다음 샘플 호출에서는 `marketingCloudVisitorId` Experience Cloud ID 서비스에서 검색한 데이터를에 전달합니다. [!DNL Target].

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      marketingCloudVisitorId: "10527837386392355901041112038610706884"
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

>[!TAB Java SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

이 시나리오에서는 [!DNL Target] 다음을 생성합니다. `tntId` 제공된 에 매핑될 원래 호출로 전달되지 않았기 때문입니다 `marketingCloudVisitorId`.

## 고객 ID (customerIds)

[고객 ID](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) Experience Cloud 방문자 ID에 추가하거나 연결할 수 있습니다. 전송할 때마다 `customerIds`, `marketingCloudVisitorId` 도 제공해야 합니다. 또한, 각각의 인증 상태와 함께 제공될 수 있다 `customerId` 각 방문자에 대해. 다음과 같은 인증 상태가 사용될 수 있습니다.

| 인증 상태 | 사용자 상태 |
| --- | --- |
| `unknown` | 알 수 없음 또는 인증되지 않음. 이 상태는 방문자가 디스플레이 광고를 클릭하여 사이트에 도착하는 시나리오와 같은 시나리오에 사용할 수 있습니다. |
| `authenticated` | 사용자는 현재 웹 사이트 또는 앱에서 활성 세션으로 인증됩니다. |
| `logged_out` | 사용자가 인증되었지만 로그아웃되었습니다. 사용자가 인증된 상태에서 연결을 끊으려고 했습니다. 사용자가 더 이상 인증됨으로 처리되는 것을 원치 않습니다. |

다음 경우에만 주의하십시오. `customerId` 이(가) 인증된 상태이면 [!DNL Target] 저장되고 customerId에 연결된 사용자 프로필 데이터를 참조합니다. 다음과 같은 경우 `customerId` 은(는) 알 수 없거나 `logged_out` 상태, 무시되며 와 연결될 수 있는 모든 사용자 프로필 데이터가 표시됩니다 `customerId` 은 대상 타기팅에 활용되지 않습니다.

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      marketingCloudVisitorId : "10527837386392355901041112038610706884",
      customerIds: [{
        id: "134325423",
        integrationCode : "crm_data",
        authenticatedState : "authenticated"
      }]
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

>[!TAB Java SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

CustomerId customerId = new CustomerId()
  .id("134325423")
  .integrationCode("crm_data")
  .authenticatedState(AuthenticatedState.AUTHENTICATED);
VisitorId id = new VisitorId()
  .marketingCloudVisitorId("10527837386392355901041112038610706884")
  .customerIds(Arrays.asList(customerId));
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

위의 예에서는 를 보내는 방법을 보여 줍니다. `customerId` 다음 포함 `authenticatedState`. 전송 시 `customerId`, `integrationCode`, `id`, 및 `authenticatedState` 및 `marketingCloudVisitorId` 필수 항목입니다. 다음 `integrationCode` 은(는) 의 별칭입니다 [고객 특성 파일](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=ko-KR) CRS를 통해서 제공했습니다.

## 병합된 프로필

다음을 결합할 수 있습니다 `tntId`, `thirdPartyID`, 및 `marketingCloudVisitorId` 동일한 요청에서. 이 시나리오에서는 [!DNL Adobe Target] 는 이러한 모든 ID의 매핑을 유지하고 방문자에게 고정합니다. 프로필의 기능 알아보기 [실시간으로 병합 및 동기화](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) 다른 식별자 사용.

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId: "B234A029348",
      marketingCloudVisitorId : "10527837386392355901041112038610706884"
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

>[!TAB Java SDK]

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

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

위의 예에서는 를 결합하는 방법을 보여 줍니다 `tntId`, `thirdPartyID`, 및 `marketingCloudVisitorId` 동일한 요청에서.

## 버킷팅

을 설정하는 방법에 따라 사용자가 경험을 보게 그룹화됩니다. [!DNL Adobe Target] 활동. 위치 [!DNL Adobe Target], 버킷팅:

* **결정론적**: MurmurHash3은 사용자 ID가 일관적인 한 사용자가 그룹화되고 매번 올바른 변형을 확인하는 데 사용됩니다.
* **고정**: [!DNL Adobe Target] 는 사용자가 사용자 프로필에 표시하는 변형을 저장하여 세션 및 채널에서 변형이 해당 사용자에게 일관되게 표시되도록 합니다. 서버측 의사 결정을 사용할 때 변형과 고착성이 보장됩니다. 온디바이스 의사 결정을 사용하면 고착성이 보장되지 않습니다.

## 전체 버킷팅 워크플로

실제 버킷팅 알고리즘으로 이동하기 전에 트래픽 할당 비율에 따라 활동을 선택하고 활동 내에서 경험을 선택하는 데 유사한 단계가 모두 사용됨을 강조 표시하는 것이 중요합니다.

### 활동 선택 단계

1. 디바이스 ID(일반적으로 UUID) 생성
1. 클라이언트 코드 가져오기
1. 활동 ID 가져오기
1. 일반적으로 &quot;활동&quot;과 같은 문자열인 소금을 가져옵니다.
1. MurmurHash3를 사용하여 해시 계산
1. 해시의 절대값 가져오기
1. 해시 절대값을 10000으로 나눕니다.
1. 나머지를 0과 10000 사이의 값을 생성하는 값으로 나눕니다
1. 결과에 100%를 곱합니다.
1. 활동 트래픽 할당 백분율과 획득한 백분율 비교 트래픽 할당 비율이 더 낮으면 활동이 선택됩니다. 그렇지 않으면 활동을 건너뜁니다.

### 경험 선택 단계

1. 디바이스 ID(일반적으로 UUID) 생성
1. 클라이언트 코드 가져오기
1. 활동 ID 가져오기
1. 일반적으로 &quot;경험&quot;과 같은 문자열인 소금을 가져옵니다.
1. MurmurHash3를 사용하여 해시 계산
1. 해시의 절대값 가져오기
1. 해시 절대값을 10000으로 나눕니다.
1. 나머지를 0과 10000 사이의 값을 생성하는 값으로 나눕니다
1. 결과에 활동 내의 총 경험 수를 곱합니다.
1. 결과를 반올림합니다. 그러면 경험 색인이 생성됩니다.

### 예

다음과 같이 가정해 보십시오.

* 클라이언트 코드가 있는 클라이언트 C `acmeclient`
* ID가 있는 활동 A `1111` 및 세 가지 경험 `E1`, `E2`, `E3`
* 경험에는 다음과 같은 배포가 있습니다. `E1` - 33%, `E2` - 33%, `E3` - 34%

선택 흐름은 다음과 같습니다.

1. 디바이스 ID `702ff4d0-83b1-4e2e-a0a6-22cbe460eb15`
1. 클라이언트 코드 `acmeclient`
1. 활동 ID `1111`
1. 소금 `experience`
1. 해시할 값 `acmeclient.1111.702ff4d0-83b1-4e2e-a0a6-22cbe460eb15.experience`, 해시 값 `-919077116`
1. 해시의 절대값 `919077116`
1. 10000 나누어서 나머지를 `7116`
1. 나머지 이후의 값은 10000으로 나뉩니다. `0.7116`
1. 총 경험 수에 값을 곱한 후 결과 `3 * 0.7116 = 2.1348`
1. 경험 색인은 입니다. `2`: 를 사용하고 있으므로 세 번째 경험을 의미합니다. `0` 기반 색인화.
