---
title: Node.js SDK를 사용할 때  [!DNL Adobe Target] 에서 [!UICONTROL getOffers()] 사용
description: '[!UICONTROL getOffers()]을(를) 사용하여 결정을 실행하고  [!DNL Adobe Target]에서 경험을 검색하는 방법에 대해 알아봅니다.'
feature: APIs/SDKs
exl-id: 3c4125ea-68d4-405e-9b9a-5fa832743153
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 21%

---

# [!UICONTROL Get Offers] (Node.js)

## 설명

`[!UICONTROL getOffers()]`은(는) 결정을 실행하고 [!DNL Adobe Target]에서 경험을 검색하는 데 사용됩니다.


## 방법

### getOffers

```js {line-numbers="true"}
TargetClient.getOffers(options: Object): Promise
```

## 매개 변수

`options` 개체의 구조는 다음과 같습니다.

| 이름 | 유형 | 필수 | 기본값 | 설명 |
| --- |--- | --- | --- | --- |
| 요청 | 개체 | 예 | 없음 | [[!DNL Target] 배달 API](/help/dev/implement/delivery-api/overview.md) 요청 준수 |
| visitorCookey | 문자열 | 아니오 | 없음 | ECID(VisitorId) 쿠키 |
| target쿠키 | 문자열 | 아니오 | 없음 | [!DNL Target] 쿠키 |
| targetLocationHint | 문자열 | 아니오 | 없음 | [!DNL Target] 위치 힌트 |
| consumerId | 문자열 | 아니요 | 없음 | [!UICONTROL Analytics for Target] (A4T) 결합에 대한 consumerIds |
| 고객 ID | 배열 | 아니요 | 없음 | VisitorId 호환 형식의 고객 ID |
| sessionId | 문자열 | 아니오 | 없음 | 여러 [!DNL Target]개의 요청을 연결하는 데 사용됨 |
| (방문자 | 개체 | 아니오 | 새 VisitorId | 외부 VisitorId 인스턴스 제공 |

## 약속

반환된 `Promise`의 구조는 다음과 같습니다.

| 이름 | 유형 | 설명 |
| --- | --- | --- |
| 요청 | 개체 | [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) 요청 |
| 응답 | 개체 | [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) 응답 |
| visitorState | 개체 | 방문자 API `getInstance()`에 전달해야 하는 개체 |
| target쿠키 | 개체 | [!DNL Target] 쿠키 |
| targetLocationHintCookie | 개체 | [!DNL Target] 위치 힌트 쿠키 |
| analyticsDetails | 배열 | 클라이언트측 Analytics 사용의 경우 Analytics 페이로드 |
| responseTokens | 배열 | [응답 토큰](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=ko&) 목록입니다. |
| 추적 | 배열 | 모든 요청 mbox/보기에 대해 집계된 추적 데이터 |
| status | 개체 | 응답의 상태를 포함하는 개체. |
| decisioningMethod | 문자열 | 사용할 의사 결정 방법([on-device](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), 서버측, 하이브리드)을 결정합니다 |

데이터를 다시 브라우저로 전달하는 데 사용되는 `targetCookie` 및 `targetLocationHintCookie` 개체의 구조는 다음과 같습니다.

| 이름 | 유형 | 설명 |
| --- | --- | --- |
| 이름 | 문자열 | 쿠키 이름 |
| value | Any | 쿠키 값, 은(는) 문자열로 변환됩니다. |
| maxAge | 숫자 | `maxAge` 옵션은 현재 시간(초)을 기준으로 하여 편리하게 만료되도록 설정할 수 있습니다. |

대상 응답의 상태를 나타내는 데 사용되는 `status` 개체의 구조는 다음과 같습니다.

| 이름 | 유형 | 설명 |
| --- | --- | --- |
| status | 숫자 | HTTP 상태 코드 |
| message | 문자열 | 응답에 대한 메시지. 예를 들어 응답이 [장치 &#x200B;](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md) 또는 서버측에서 결정되었는지 여부를 나타낼 수 있습니다 |
| remoteMbox | 배열 | Decisioning 메서드가 `on-device`인 경우 온디바이스에서 완전히 결정할 수 없는 mbox 이름 배열이 제공됩니다. 즉, [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) 요청이 필요합니다. |

## 예

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

const request = {
    context: {channel: "web"},
    execute: {
        mboxes: [{
            name: "a1-serverside-ab",
            index: 1
        }]
}};

const response = await targetClient.getOffers({ request });
```
