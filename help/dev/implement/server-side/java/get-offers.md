---
title: Java SDK를 사용할 때  [!DNL Adobe Target] 에서 getOffers()를 사용합니다.
description: getOffers()를 사용하여 결정을 실행하고  [!DNL Adobe Target]에서 경험을 검색하는 방법을 알아봅니다.
feature: APIs/SDKs
exl-id: 9d7bf956-9d6a-4b4f-a401-2e6814f17f3d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 13%

---

# 오퍼 가져오기(Java)

## 설명

`getOffers()`은(는) 결정을 실행하고 [!DNL Adobe Target]에서 경험을 검색하는 데 사용됩니다.

## 방법

### getOffers

`TargetClient.getOffers` 메서드 시그니처는 다음과 같이 표시됩니다.

**요청**

```javascript {line-numbers="true"}
TargetDeliveryResponse TargetClient.getOffers(TargetDeliveryRequest request)
```

`TargetDeliveryRequest.builder`을(를) 사용하여 TargetDeliveryRequest를 만듭니다.

**응답**

```javascript {line-numbers="true"}
TargetDeliveryRequestBuilder TargetDeliveryRequest.builder()
```

## 매개 변수

`[!UICONTROL TargetDeliveryRequestBuilder]` 개체의 구조는 다음과 같습니다.

| 이름 | 유형 | 필수 | 설명 |
| --- | --- | --- | --- |
| 컨텍스트 | 컨텍스트 | 예 | 요청에 대한 컨텍스트를 지정합니다. |
| sessionId |  | 문자열 | 아니오 | 여러 [!DNL Target]개의 요청을 연결하는 데 사용됨 |
| thirdPartyId | 문자열 | 아니오 | 모든 호출에서 보낼 수 있는 사용자의 회사 식별자 |
| cookies | 목록 | 아니요 | 동일한 사용자의 이전 [!DNL Target] 요청에서 반환된 쿠키 목록입니다. |
| customerIds | 맵 | 아니요 | VisitorId 호환 형식의 고객 ID |
| 실행 | ExecuteRequest | 아니요 | 실행할 PageLoad 또는 mbox 요청입니다. 서버측에서 즉시 평가됩니다. |
| 프리페치 | PrefetchRequest | 아니요 | 미리 가져오기에 대한 보기, PageLoad 또는 mbox 요청입니다. 전환 시 반환될 알림 토큰과 함께 반환됩니다. |
| 알림 | 목록 | 아니요 | 표시된 프리페치된 콘텐츠와 관련된 알림을 전송하는 데 사용됨 |
| requestId | 문자열 | 아니오 | 응답에서 반환될 요청 ID입니다. 없는 경우 자동으로 생성됩니다. |
| impressionId | 문자열 | 아니오 | 동일한 ID를 가진 두 번째 및 후속 요청이 존재하는 경우 활동/지표에 대한 노출 수가 증가하지 않습니다. 없는 경우 자동으로 생성됩니다. |
| environmentId | Long | 아니요 | 유효한 클라이언트 환경 ID입니다. 지정하지 않으면 제공된 호스트를 기반으로 호스트가 결정됩니다. |
| 속성 | 속성 | 아니요 | 토큰 필드를 통해 at_property를 지정합니다. 게재 범위를 제어하는 데 사용할 수 있습니다. |
| 추적 | 추적 | 아니요 | 게재 API에 대한 추적을 활성화합니다. |
| qaMode | QAM 코드 | 아니요 | 이 개체를 사용하여 요청에서 QA 모드를 활성화합니다. |
| locationHint | 문자열 | 아니오 | [!DNL Target] 에지 클러스터 위치 힌트입니다. 이 요청에 대해 주어진 에지 클러스터를 타겟팅하는 데 사용됩니다. |
| (방문자 | 방문자 | 아니요 | 사용자 지정 방문자 API 개체를 제공하는 데 사용됩니다. |
| ID | VisitorId | 아니요 | 방문자에 대한 식별자를 포함하는 객체입니다. 예: tntId, thirdParyId, mcId, customerIds. |
| experienceCloud | Experience Cloud | 아니요 | Audience Manager 및 Analytics와의 통합을 지정합니다. 제공되지 않을 경우 쿠키를 사용하여 자동으로 채워집니다. |
| tntId | 문자열 | 아니오 | 사용자의 [!DNL Target]에 있는 기본 식별자입니다. targetCookies에서 가져왔습니다. 제공되지 않을 경우 자동으로 생성됩니다. |
| mcId | 문자열 | 아니오 | 다른 [!DNL Adobe] 솔루션(ECID) 간에 데이터를 병합하고 공유하는 데 사용됩니다. targetCookies에서 가져왔습니다. 제공되지 않을 경우 자동으로 생성됩니다. |
| trackingServer | 문자열 | 아니오 | [!DNL Adobe Target]과(와) [!DNL Adobe Analytics]이(가) 데이터를 올바르게 결합하기 위한 Adobe Analytics 서버. |
| trackingServerSecure | 문자열 | 아니오 | [!DNL Adobe Target]과(와) [!DNL Adobe Analytics]이(가) 데이터를 올바르게 결합하기 위한 [!UICONTROL Adobe Analytics Secure Server]입니다. |
| decisioningMethod | DecisioningMethod | 아니요 | 온디바이스 의사 결정에 대해 ON_DEVICE 또는 HYBRID 의사 결정 방법을 명시적으로 설정하는 데 사용할 수 있습니다. |

각 필드의 값은 *[!UICONTROL Target View Delivery API]* 요청 사양을 준수해야 합니다. *[!UICONTROL Target View Delivery API]*&#x200B;에 대한 자세한 내용은 [http://developers.adobetarget.com/api/#view-delivery-overview](http://developers.adobetarget.com/api/#view-delivery-overview)을(를) 참조하세요.


## 응답

`TargetClient.getOffers(`이(가) 반환한 `TargetDeliveryResponse`의 구조는 다음과 같습니다.

| 이름 | 유형 | 설명 |
| --- | --- | --- |
| 요청 | TargetDeliveryRequest &#x200B; | *[!DNL Target]* 요청 |
| 응답 | DeliveryResponse | *[!DNL Target]* 응답 |
| cookies | 목록 | 이 사용자의 세션 메타데이터 목록입니다. 이 사용자에 대한 다음 대상 요청에서 전달해야 합니다. |
| visitorState | 맵 | 방문자 API에서 사용할 클라이언트측에 설정할 방문자 상태 |
| responseStatus | ResponseStatus | 응답의 상태를 나타내는 개체 |

응답의 `ResponseStatus`에 다음 필드가 포함되어 있습니다.

| 이름 | 유형 | 설명 |
| --- | --- | --- |
| status | int | [!DNL Target]에서 반환된 HTTP 상태 |
| message | 문자열 | HTTP 상태가 200이 아닌 경우의 상태 메시지 |
| remoteMbox | 문자열 목록 | 온디바이스 의사 결정에 사용됩니다. 전적으로 디바이스에서 결정할 수 없는 원격 활동이 있는 mbox 목록을 포함합니다. |
| 원격 보기 | 문자열 목록 | 온디바이스 의사 결정에 사용됩니다. 전적으로 디바이스에서 결정할 수 없는 원격 활동이 있는 보기 목록을 포함합니다. |

사용자 세션에 대한 데이터를 저장하는 데 사용되는 `TargetCookie` 개체의 구조는 다음과 같습니다.

| 이름 | 유형 | 설명 |
| --- | --- | --- |
| 이름 | 문자열 | 쿠키 이름 |
| value | 문자열 | 쿠키 값, 값이 문자열로 변환됩니다. |
| maxAge | 숫자 | maxAge 옵션은 현재 시간(초)을 기준으로 하여 편리하게 만료되도록 설정할 수 있습니다 |

쿠키가 만료되는 것에 대해 걱정할 필요는 없습니다. Target은 SDK 내에서 maxAge를 처리합니다.

## 예

**요청**

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);

List<MboxRequest> mboxRequests = new ArrayList<>();
mboxRequests.add((MboxRequest) new MboxRequest().name("a1-serverside-ab").index(1));

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .execute(new ExecuteRequest().setMboxes(mboxRequests))
        .build();
```

**응답**

```javascript {line-numbers="true"}
TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
```
