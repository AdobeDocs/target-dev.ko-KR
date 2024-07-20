---
title: create 메서드를 사용하여 Node.js SDK 초기화
description: create 메서드를 사용하여 Node.js SDK를 초기화하고  [!DNL Target] 클라이언트를 인스턴스화하여  [!DNL Adobe Target] 실험 및 개인화된 경험을 위해 호출하는 방법에 대해 알아봅니다.
feature: APIs/SDKs
exl-id: 71516e44-508a-4d8d-9f2b-7c54243e9c60
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 18%

---

# Node.js SDK 초기화

## 설명

`create` 메서드를 사용하여 Node.js SDK를 초기화하고 [!UICONTROL Target] 클라이언트를 인스턴스화하여 실험 및 개인화된 경험을 위해 [!DNL Adobe Target]을(를) 호출합니다.

## 방법

**만들기**

```js {line-numbers="true"}
TargetClient.create(options: Object): TargetClient
```

## 매개 변수

`options`의 구조는 다음과 같습니다.

| 이름 | 유형 | 필수 | 기본값 | 설명 |
| --- | --- | --- | --- | --- |
| 클라이언트 | 문자열 | 예 | 없음 | [!UICONTROL Adobe Target Client ID] |
| organizationId | 문자열 | 예 | 없음 | [!UICONTROL Experience Cloud Organization ID] |
| 환경 | 문자열 | 아니오 | production | 대상 환경 이름입니다. [!DNL Target] UI에서 [!UICONTROL Administration] > [!UICONTROL Environments]입니다. |
| timeout | 숫자 | 아니오 | 3000 | 시간 제한(밀리초) |
| serverDomain | 문자열 | 아니오 | `*client*.tt.omtrdc.net` | 기본 호스트 이름 무시 |
| secure | 부울 | 아니오 | true | HTTP 체계를 적용하도록 설정 해제 |
| 로거 | 개체 | 아니오 | NOOP 로거 | 기본 NOOP 로거를 바꿉니다. |
| targetLocationHint | 문자열 | 아니오 | 없음 | Target 위치 힌트 |
| fetchApi | 함수 | 아니오 | global.fetch 또는 window.fetch | SDK에서 http 요청에 [fetch](https://fetch.spec.whatwg.org/)을(를) 사용합니다. 기본적으로 노드 가져오기 또는 브라우저 가져오기 구현이 사용됩니다. 그러나 `fetchApi`을(를) 사용하여 대체 구현을 제공할 수 있습니다. |
| propertyToken | 문자열 | 아니오 | 없음 | **대상 속성 토큰**. 여기에 지정하면 모든 `getOffers` 호출에서 이 값을 사용합니다. **온디바이스 의사 결정**&#x200B;의 경우 SDK는 `propertyToken`에 설정된 속성 토큰에 대해 정규화된 활동이 포함된 아티팩트만 다운로드합니다. |
| decisioningMethod | 문자열 | 아니오 | 서버측 | 사용할 의사 결정 방법([on-device](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), 서버측, 하이브리드)을 결정합니다 |
| pollingInterval | 숫자 | 아니오 | 300000(5분) | [온디바이스 의사 결정 규칙 아티팩트](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)의 폴링 간격(밀리초) |
| artifactLocation | 문자열 | 아니오 | 없음 | [온디바이스 의사 결정 규칙 아티팩트](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)에 대한 정규화된 URL입니다. 내부적으로 결정된 위치를 재정의합니다. |
| artifactPayload | 개체 | 아니오 | 없음 | [온디바이스 의사 결정 규칙 아티팩트](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)의 JSON 페이로드. 지정하면 URL에서 요청하는 대신 사용됩니다. |
| [events](sdk-events.md) | Object&lt;String,Function> | 아니요 | 없음 | 이벤트 이름 키와 콜백 함수 값이 있는 선택적 개체입니다 |
| 원격 분석 사용 | 부울 | 아니오 | true | 사용하도록 설정하면 Adobe이 SDK 기능 사용 및 성능 원격 분석 데이터를 수집합니다. 개인 데이터는 수집되지 않습니다. |

## 예

### Node.js

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    events: {clientReady: targetClientReady }
};

const targetClient = TargetClient.create(CONFIG);

function targetClientReady() {
    // make calls to Adobe Target
}
```
