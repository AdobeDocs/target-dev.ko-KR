---
title: create 메서드를 사용하여 Node.js SDK 초기화
description: create 메서드를 사용하여 Node.js SDK를 초기화하고 [!DNL Target] 에 대해 호출할 클라이언트 [!DNL Adobe Target] (실험 및 개인화된 경험)
feature: APIs/SDKs
exl-id: 71516e44-508a-4d8d-9f2b-7c54243e9c60
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 19%

---

# Node.js SDK 초기화

## 설명

사용 `create` Node.js SDK를 초기화하고 [!UICONTROL Target] 에 대해 호출할 클라이언트 [!DNL Adobe Target] (실험 및 개인화된 경험)

## 방법

**만들기**

```js {line-numbers="true"}
TargetClient.create(options: Object): TargetClient
```

## 매개 변수

`options` 에는 다음 구조가 있습니다.

| 이름 | 유형 | 필수 | 기본값 | 설명 |
| --- | --- | --- | --- | --- |
| 클라이언트 | 문자열 | 예 | 없음 | [!UICONTROL Adobe Target 클라이언트 ID] |
| organizationId | 문자열 | 예 | 없음 | [!UICONTROL Experience Cloud 조직 ID] |
| 환경에만 해당되는 결과를 반환합니다 | 문자열 | 아니오 | production | Target 환경 이름입니다. 다음에서 [!DNL Target] UI, [!UICONTROL 관리] > [!UICONTROL 환경]. |
| timeout | 숫자 | 아니오 | 3000 | 시간 초과(밀리 초)입니다 |
| serverDomain | 문자열 | 아니오 | `*client*.tt.omtrdc.net` | 기본 호스트 이름 무시 |
| secure | 부울 | 아니오 | true | HTTP 체계를 적용하도록 설정 해제 |
| 로거 | 개체 | 아니오 | NOOP 로거 | 기본 NOOP 로거를 바꿉니다. |
| targetLocationHint | 문자열 | 아니오 | 없음 | Target 위치 힌트 |
| fetchApi | 함수 | 아니오 | global.fetch 또는 window.fetch | [가져오기](https://fetch.spec.whatwg.org/) SDK에서 http 요청에 사용합니다. 기본적으로 노드 가져오기 또는 브라우저 가져오기 구현이 사용됩니다. 그러나 을 사용하여 대체 구현을 제공할 수 있습니다. `fetchApi` |
| propertyToken | 문자열 | 아니오 | 없음 | **Target 속성 토큰**. 여기에 지정된 경우 모두 `getOffers` 호출은 이 값을 사용합니다. **온디바이스 의사 결정**, SDK는에 설정된 속성 토큰에 대한 적격 활동이 포함된 아티팩트만 다운로드합니다. `propertyToken` |
| decisioningMethod | 문자열 | 아니오 | 서버측 | 사용할 의사 결정 방법 결정([온디바이스](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), 서버측, 하이브리드) |
| pollingInterval | 숫자 | 아니오 | 300000(5분) | 에 대한 폴링 간격 [온디바이스 의사 결정 규칙 아티팩트](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md) (밀리초) |
| artifactLocation | 문자열 | 아니오 | 없음 | 에 대한 정규화된 URL [온디바이스 의사 결정 규칙 아티팩트](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). 내부적으로 결정된 위치를 재정의합니다. |
| artifactPayload | 개체 | 아니오 | 없음 | 의 JSON 페이로드 [온디바이스 의사 결정 규칙 아티팩트](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). 지정하면 URL에서 요청하는 대신 사용됩니다. |
| [events](sdk-events.md) | 오브젝트&lt;string function=&quot;&quot;> | 아니요 | 없음 | 이벤트 이름 키와 콜백 함수 값이 있는 선택적 개체입니다 |
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
