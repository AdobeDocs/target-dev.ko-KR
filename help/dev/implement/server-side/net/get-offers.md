---
title: .NET SDK를 사용할 때  [!DNL Adobe Target] 에서 getOffers()를 사용합니다.
description: getOffers()를 사용하여 결정을 실행하고  [!DNL Adobe Target]에서 경험을 검색하는 방법을 알아봅니다.
feature: APIs/SDKs
exl-id: 4d1d1cbd-c7e5-4146-9fea-08e01923874d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 13%

---

# 오퍼 가져오기(.NET)

## 설명

`GetOffers()`은(는) 결정을 실행하고 [!DNL Adobe Target]에서 경험을 검색하는 데 사용됩니다.

## 방법

`TargetClient.GetOffers` 메서드 시그니처입니다.

## \.NET

```dotnet {line-numbers="true"}
TargetDeliveryResponse TargetClient.GetOffers(TargetDeliveryRequest request)
```

`TargetDeliveryRequest.Builder`을(를) 사용하여 `TargetDeliveryRequest`을(를) 만듭니다.

## \.NET

```dotnet {line-numbers="true"}
TargetDeliveryRequest.Builder TargetDeliveryRequest.Builder()
```

## 매개 변수

`TargetDeliveryRequest.Builder` 개체의 구조는 다음과 같습니다.

| 이름 | 유형 | 필수 | 설명 |
| --- | --- | --- | --- |
| 컨텍스트 | 컨텍스트 | 예 | 요청에 대한 컨텍스트를 지정합니다. |
| sessionId | 문자열 | 아니오 | 여러 [!DNL Target]개의 요청을 연결하는 데 사용됨 |
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
| mcId | 문자열 | 아니오 | 서로 다른 Adobe 솔루션(ECID) 간에 데이터를 병합하고 공유하는 데 사용됩니다. targetCookies에서 가져왔습니다. 제공되지 않을 경우 자동으로 생성됩니다. |
| trackingServer | 문자열 | 아니오 | [!DNL Adobe Target]과(와) [!DNL Adobe Analytics]이(가) 데이터를 올바르게 결합하기 위한 Adobe Analytics 서버. |
| trackingServerSecure | 문자열 | 아니오 | [!DNL Adobe Target]과(와) [!DNL Adobe Analytics]이(가) 데이터를 올바르게 결합하기 위한 [!UICONTROL Adobe Analytics Secure Server]입니다. |
| decisioningMethod | DecisioningMethod | 아니요 | 온디바이스 의사 결정에 대해 ON_DEVICE 또는 HYBRID 의사 결정 방법을 명시적으로 설정하는 데 사용할 수 있습니다. |

각 필드의 값은 [Target 배달 API](/help/dev/implement/delivery-api/overview.md) 요청 사양을 준수해야 합니다.

## 응답

`TargetClient.GetOffers()`이(가) 반환한 `TargetDeliveryResponse`의 구조는 다음과 같습니다.

| 이름 | 유형 | 설명 |
| --- | --- | --- |
| 요청 | TargetDeliveryRequest &#x200B; | [Target 배달 API](/help/dev/implement/delivery-api/overview.md) 요청 |
| 응답 | DeliveryResponse &#x200B; | [Target 배달 API](/help/dev/implement/delivery-api/overview.md)* 응답 |
| 상태 | HttpStatusCode | 응답 HTTP 상태 코드 |
| 메시지 | string | 응답 상태 메시지 또는 오류 메시지 |
| 위치 | 위치 | [!DNL Target] 위치 이름(글로벌 mbox 이름 및 원격 의사 결정만 사용할 수 있는 mbox/보기 포함) |
| GetCookies | 사전 | 이 사용자의 세션 메타데이터 사전을 반환합니다. 이 사용자를 위해 다음 [!DNL Target] 요청에서 전달해야 합니다. |
| VisitorState | IDictionary | 방문자 API Javascript 라이브러리 초기화를 위해 클라이언트측에서 설정할 방문자 상태 |

사용자 세션에 대한 데이터를 저장하는 데 사용되는 `TargetCookie` 개체의 구조는 다음과 같습니다.

| 이름 | 유형 | 설명 |
| --- | --- | --- |
| 이름 | string | 쿠키 이름 |
| 값 | string | 쿠키 값 |
| MaxAge | int | `MaxAge` 옵션은 현재 시간(초)을 기준으로 하여 Expires를 편리하게 설정할 수 있습니다 |

쿠키가 만료되는 것에 대해 걱정할 필요는 없습니다. [!DNL Target]이(가) SDK 내에서 `MaxAge`을(를) 처리합니다.

## 예

## \.NET

```dotnet {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

var targetClient = TargetClient.Create(targetClientConfig);

var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .SetExecute(new ExecuteRequest(mboxes: mboxRequests))
    .Build();

var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
```
