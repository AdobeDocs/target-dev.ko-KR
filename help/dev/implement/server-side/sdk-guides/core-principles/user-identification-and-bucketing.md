---
title: 사용자 식별 및 버킷팅
description: 사용자 식별 및 버킷팅
exl-id: 4fcf235b-6a58-442c-ae13-9d05ec1033fc
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 3%

---

# 사용자 식별 및 버킷팅

## 사용자 식별

[!DNL Adobe Target] 내에서 사용자를 식별하는 방법에는 여러 가지가 있습니다. [!UICONTROL Target]은(는) 다음 식별자를 사용합니다.

| 필드 이름 | 설명 |
| --- | --- |
| `tntID` | `tntId`은(는) 사용자의 [!DNL Target]에 있는 기본 식별자입니다. 이 ID를 제공할 수 있습니다. 그렇지 않으면 요청에 ID가 포함되지 않은 경우 [!DNL Target]에서 자동으로 생성합니다. |
| `thirdPartyId` | `thirdPartyId`은(는) 모든 호출과 함께 보낼 수 있는 사용자의 회사 식별자입니다. 사용자가 회사 사이트에 로그인하면 일반적으로 회사는 방문자 계정, 로열티 카드, 멤버십 번호 또는 해당 회사에 대한 기타 적용 가능한 식별자에 연결되는 ID를 만듭니다. |
| `marketingCloudVisitorId` | `marketingCloudVisitorId`은(는) 다른 Adobe 솔루션 간에 데이터를 병합하고 공유하는 데 사용됩니다. marketingCloudVisitorId는 Adobe Analytics 및 Adobe Audience Manager과의 통합에 필요합니다. |
| `customerIds` | Experience Cloud 방문자 ID와 함께 각 방문자에 대한 추가 [고객 ID](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) 및 인증된 상태도 활용할 수 있습니다. |

## [!DNL Target] ID(tntID)

[!DNL Target] ID 또는 `tntId`은(는) 장치 ID로 간주할 수 있습니다. 이 `tntId`은(는) 요청에 제공되지 않을 경우 [!DNL Adobe Target]에 의해 자동으로 생성됩니다. 동일한 사용자가 사용하는 장치에 올바른 콘텐츠를 전달하려면 후속 요청에 이 `tntId`을(를) 포함해야 합니다.

다음 샘플 호출은 `tntId`이(가) [!DNL Target]에 전달되지 않는 상황을 보여 줍니다.

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

`tntId`이(가) 없는 경우 [!DNL Adobe Target]은(는) `tntId`을(를) 생성하여 다음과 같이 응답에 제공합니다.

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

이 예제에서 생성된 `tntId`은(는) `10abf6304b2714215b1fd39a870f01afc.35_0`입니다. 이 `tntId`은(는) 세션 간 동일한 사용자에 대해 사용해야 합니다.

## 타사 ID(thirdPartyId)

조직에서 ID를 사용하여 방문자를 식별하는 경우 `thirdPartyID`을(를) 사용하여 콘텐츠를 전달할 수 있습니다. `thirdPartyID`은(는) 최종 사용자가 웹, 모바일 또는 IoT 채널에서 비즈니스와 상호 작용하는지 여부에 관계없이 비즈니스에서 최종 사용자를 식별하는 데 사용하는 영구 ID입니다. 즉, `thirdPartyId`은(는) 여러 채널에서 사용할 수 있는 사용자 프로필 데이터를 참조합니다. 그러나 [!DNL Adobe Target] 배달 API 호출을 수행할 때마다 `thirdPartyID`을(를) 제공해야 합니다.

다음 샘플 호출에서는 `thirdPartyId`의 사용을 보여 줍니다.

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

이 시나리오에서 [!DNL Adobe Target]은(는) 원래 호출로 전달되지 않았으므로 `tntId`을(를) 생성하며, 이 호출은 제공된 `thirdPartyId`에 매핑됩니다.

## Marketing Cloud 방문자 ID(marketingCloudVisitorId)

`marketingCloudVisitorId`은(는) Adobe Experience Cloud의 모든 솔루션에서 방문자를 식별하는 범용 및 영구 ID입니다. 조직에서 ID 서비스를 구현하면 이 ID를 사용하여 [!DNL Adobe Target], Adobe Analytics 및 Adobe Audience Manager을 비롯한 다양한 Experience Cloud 솔루션에서 동일한 사이트 방문자와 해당 데이터를 식별할 수 있습니다. [!DNL Target]을(를) [!DNL Adobe Analytics] 및 [!DNL Adobe Audience Manager]과(와) 통합할 때 `marketingCloudVisitorId`이(가) 필요합니다.

다음 샘플 호출은 Experience Cloud ID 서비스에서 검색된 `marketingCloudVisitorId`이(가) [!DNL Target]에 전달되는 방법을 보여 줍니다.

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

이 시나리오에서 [!DNL Target]은(는) 원래 호출로 전달되지 않았으므로 `tntId`을(를) 생성하며, 이 호출은 제공된 `marketingCloudVisitorId`에 매핑됩니다.

## 고객 ID (customerIds)

[고객 ID](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html)를 Experience Cloud 방문자 ID에 추가하거나 연결할 수 있습니다. `customerIds`을(를) 보낼 때마다 `marketingCloudVisitorId`도 제공해야 합니다. 또한 각 방문자에 대해 각 `customerId`과(와) 함께 인증 상태를 제공할 수 있습니다. 다음과 같은 인증 상태가 사용될 수 있습니다.

| 인증 상태 | 사용자 상태 |
| --- | --- |
| `unknown` | 알 수 없음 또는 인증되지 않음. 이 상태는 방문자가 디스플레이 광고를 클릭하여 사이트에 도착하는 시나리오와 같은 시나리오에 사용할 수 있습니다. |
| `authenticated` | 사용자는 현재 웹 사이트 또는 앱에서 활성 세션으로 인증됩니다. |
| `logged_out` | 사용자가 인증되었지만 로그아웃되었습니다. 사용자가 인증된 상태에서 연결을 끊으려고 했습니다. 사용자가 더 이상 인증됨으로 처리되는 것을 원치 않습니다. |

`customerId`이(가) 인증된 상태인 경우에만 [!DNL Target]이(가) 저장되고 customerId에 연결된 사용자 프로필 데이터를 참조합니다. `customerId`이(가) 알 수 없거나 `logged_out` 상태인 경우 무시되며, 해당 `customerId`과(와) 연결할 수 있는 모든 사용자 프로필 데이터는 대상 타기팅에 사용되지 않습니다.

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

위의 예에서는 `authenticatedState`을(를) 사용하여 `customerId`을(를) 보내는 방법을 보여 줍니다. `customerId`을(를) 보낼 때 `integrationCode`, `id`, `authenticatedState` 및 `marketingCloudVisitorId`이(가) 필요합니다. `integrationCode`은(는) CRS를 통해 제공한 [고객 특성 파일](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=ko-KR)의 별칭입니다.

## 병합된 프로필

동일한 요청에서 `tntId`, `thirdPartyID` 및 `marketingCloudVisitorId`을(를) 결합할 수 있습니다. 이 시나리오에서는 [!DNL Adobe Target]이(가) 이러한 모든 ID의 매핑을 유지하고 방문자에게 고정합니다. 다른 식별자를 사용하여 프로필이 [실시간으로 병합 및 동기화](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html)되는 방법을 알아봅니다.

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

위의 예에서는 동일한 요청에서 `tntId`, `thirdPartyID` 및 `marketingCloudVisitorId`을(를) 결합하는 방법을 보여 줍니다.

## 버킷팅

[!DNL Adobe Target] 활동을 설정하는 방법에 따라 사용자가 경험을 볼 수 있도록 그룹화됩니다. [!DNL Adobe Target]에서 버킷팅은 다음과 같습니다.

* **결정론적**: MurmurHash3은 사용자가 그룹화되고 사용자 ID가 일관적인 한 항상 올바른 변형을 확인하는 데 사용됩니다.
* **고정**: [!DNL Adobe Target]은(는) 사용자 프로필에 표시되는 변형을 저장하여 세션 및 채널에서 해당 사용자에게 변형이 일관되게 표시되도록 합니다. 서버측 의사 결정을 사용할 때 변형과 고착성이 보장됩니다. 온디바이스 의사 결정을 사용하면 고착성이 보장되지 않습니다.

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

* 클라이언트 코드가 `acmeclient`인 클라이언트 C
* 활동 A의 ID는 `1111`이고 경험은 `E1`, `E2`, `E3`입니다.
* 경험에 다음과 같은 분포가 있습니다. `E1` - 33%, `E2` - 33%, `E3` - 34%

선택 흐름은 다음과 같습니다.

1. 장치 ID `702ff4d0-83b1-4e2e-a0a6-22cbe460eb15`
1. 클라이언트 코드 `acmeclient`
1. 활동 ID `1111`
1. 솔트 `experience`
1. 해시 값 `acmeclient.1111.702ff4d0-83b1-4e2e-a0a6-22cbe460eb15.experience`, 해시 값 `-919077116`
1. 해시 `919077116`의 절대값
1. `7116`(으)로 10000 후 남은 시간
1. 나머지 이후의 값은 `0.7116`10000(으)로 나뉩니다.
1. 총 경험 수 `3 * 0.7116 = 2.1348`에 값을 곱한 후 결과
1. 경험 인덱스는 `2`입니다. `0` 기반 인덱싱을 사용하고 있으므로 세 번째 경험을 의미합니다.
