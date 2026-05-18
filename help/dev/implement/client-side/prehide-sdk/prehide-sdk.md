---
keywords: SDK 미리 숨기기, 깜박임, 깜박임 방지, 사전 숨김, 사전 숨김, alloy, at.js, 구현, 동의, CMP, 스크립트 배치, 인라인, 외부, SDK 선택
description: 페이지를 로드하는 동안 개인화되지 않은 콘텐츠(깜박임)를 방지하기 위해  [!DNL Adobe Target] SDK을 미리 숨기는 방법을 알아봅니다. SDK은 Adobe Alloy(웹 SDK) 및 at.js 모두에서 작동합니다.
title: SDK 통합 안내서 미리 숨기기
feature: Implementation
hide: true
source-git-commit: 81818370d32ee8c3f3538e5d8d942f66c13e6a13
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 0%

---


# SDK 통합 안내서 미리 숨기기

[!DNL Adobe Target] 개인화로 인해 페이지 중간 렌더링이 다시 작성되어 깜박임이 발생하는 것을 방지하는 아주 작은 동기 JavaScript 라이브러리입니다. `<head>`의 맨 위에 인라인 `<script>` 태그를 하나 추가하면 개인화된 콘텐츠가 준비되거나 안전 타이머가 실행된 후에만 페이지가 표시됩니다.

## 통합 단계 {#integration-steps}

1. 번들을 다운로드합니다.

   깜박임 관리자 UI를 사용하여 `prehide.min.js`을(를) 다운로드합니다. 파일이 클라이언트 코드와 보호 제한 시간으로 미리 구성되어 있으므로 `PrehideConfig` 블록이 필요하지 않습니다.

1. `<head>`의 맨 위에 인라인으로 포함하십시오.

   `prehide.min.js`의 내용을 인라인 `<script>` 태그 내에 `<head>`의 첫 번째 하위 항목으로 직접 붙여 넣습니다. 인라인이 선호되는 이유는 [인라인과 외부](#inline-vs-external)를 참조하십시오.

   ```html
   <!-- 1. Prehide SDK: must be FIRST in <head> and BEFORE any Adobe SDK -->
   <script>
     // paste the contents of prehide.min.js here
   </script>
   
   <!-- 2. Then load Alloy.js OR at.js -->
   <script src="https://your-cdn/alloy.min.js"></script>
   ```

1. (선택 사항) 런타임 구성 블록을 추가합니다.

   UI를 통해 다운로드하지 않고 번들을 자체 호스팅하거나 SDK 선택을 무시해야 하는 경우에만 필요합니다. 구성 블록을 사전 숨김 스크립트 앞에 배치합니다.

   ```html
   <script>
     window.PrehideConfig = {
       org: "your-client-code",
       sdk: "alloy"            // or "atjs" (defaults to "alloy")
     };
   </script>
   <script> /* prehide.min.js inline contents */ </script>
   <script src="https://your-cdn/alloy.min.js"></script>
   ```

1. (선택 사항) 동의를 연결합니다.

   구현에서 CMP(동의 관리 플랫폼)를 사용하는 경우 동의 상태가 알려지는 즉시 `window.Prehide.setConsent(...)`을(를) 호출합니다. [동의 관리](#consent-management)를 참조하세요.

1. 확인합니다.

   DevTools를 열고 `<style id="alloy-prehiding">`(또는 at.js의 경우 `at-body-style`)이(가) 첫 번째 페인트에서 `<head>`에 나타나며, SDK이 완료되면 제거되는지 확인합니다. 콘솔에서 `window.Prehide.getState()`을(를) 실행하여 런타임 상태를 검사합니다.

## 스크립트를 배치할 위치 {#script-placement}

>[!IMPORTANT]
>
>SDK 사전 숨김은 Alloy/at.js 전에 실행해야 합니다. Alloy가 먼저 로드되면 페이지는 개인화되지 않은 콘텐츠를 렌더링한 다음 다시 렌더링합니다. 이것이 이 SDK이 방지하려고 고안한 정확한 깜박임입니다.
></br>>SDK 스크립트 사전 숨김 태그에 `async` 또는 `defer`을(를) 추가하지 마십시오. 브라우저가 페이지 레이아웃을 시작하기 전에 숨김 규칙이 삽입되도록 하려면 동기 실행이 필요합니다.

SDK 미리 숨김은 이후에 정리되는 [!DNL Adobe Target] SDK보다 문서에 먼저 표시되어야 합니다. 로드 순서는 협상할 수 없습니다.

```html
<!doctype html>
<html>
<head>
  <!-- ① Prehide SDK FIRST. Inline. Synchronous. No async/defer. -->
  <script> /* prehide.min.js inline contents */ </script>

  <!-- ② Alloy or at.js loads next -->
  <script src="https://cdn.alloy.adobe.com/alloy.min.js"></script>

  <!-- ③ Then everything else: meta, css, third-party tags, ... -->
  <link rel="stylesheet" href="main.css">
</head>
<body> ... your page ... </body>
</html>
```

## 인라인과 외부 {#inline-vs-external}

`prehide.min.js`을(를) 포함하는 방법에는 두 가지가 있습니다.

| 방법 | 예 | 참고 |
| --- | --- | --- |
| 인라인(기본 설정) | `<script>/* full contents of prehide.min.js pasted directly into the page */</script>` | 네트워크 왕복 없음. SDK은 다른 것이 렌더링되기 전에 실행됩니다. |
| 외부(인라이닝이 불가능한 경우에만) | `<script src="/static/prehide.min.js"></script>` | 첫 번째 렌더링 전에 차단 네트워크 요청을 도입합니다. HTTP/2 및 에지 캐싱을 사용하더라도 일반적으로 30-80ms의 비용이 듭니다. |

### 인라인이 선호되는 이유

>[!TIP]
>
>HTML 템플릿의 `<script>...</script>` 내에서 직접 번들을 인라인합니다. 중요한 CSS 블록(작음, 인라인 및 항상 맨 위에 있음)으로 취급합니다.

* 렌더링 차단 가져오기가 없습니다. SDK 미리 숨김의 목적은 첫 번째 렌더링에 *before* 숨기기 규칙을 삽입하는 것입니다. 외부 `<script src>`은(는) 정확히 해당 중요 창에 네트워크 왕복이 추가됩니다.
* 새 실패 모드가 없습니다. 외부 파일은 404 시간 초과되거나 광고 차단기에 의해 차단될 수 있습니다. 인라인 사본은 수행할 수 없습니다.
* 번들이 작습니다(~6KB). 인라인 비용은 일반적인 favicon보다 저렴하고 캐싱 이점이 없으므로 첫 번째 렌더링에서 추가 왕복보다 훨씬 큽니다.
* 캐시에 친숙합니다. HTML 응답에서 인라인될 때 SDK은 기존 캐싱 계층(CDN 또는 브라우저 HTTP 캐시)에 의해 문서의 나머지 부분과 함께 캐시됩니다.
* 고객별 번들. 다운로드한 파일에는 다운로드 시 생성되는 클라이언트 코드가 있습니다. 인라이닝은 모든 방문자가 추가 요청 없이 올바른 맞춤형 번들을 받도록 보장합니다.

## 구성 {#configuration}

SDK은 두 소스의 구성을 우선순위 순서로 수락합니다. 어떤 것이든 먼저 구할 수 있는 것으로 나와 있다.

### A: 다운로드 시간 자리 표시자(런타임 구성 없음)

플리커 관리자 UI에서 `prehide.min.js`을(를) 다운로드하면 서버는 번들 내의 세 자리 표시자를 대체합니다.

| 자리 표시자 | (으)로 대체됨 | 교체되지 않은 경우 대체 |
| --- | --- | --- |
| `__FM_CLIENT_CODE__` | 클라이언트 코드(예: `"acmecorp"`) | `window.PrehideConfig.org` 읽기 |
| `__FM_TIMEOUT__` | 보호 타이머 기간(밀리초)(예: `"3000"`) | `5000`밀리초 |
| `__FM_VERSION__` | SDK 버전(예: `"1.0.0"`) | `"0.0.0-dev"` |

UI 다운로드 번들을 사용하는 경우 `PrehideConfig` 블록이 필요하지 않습니다. 스크립트를 인라인하기만 하면 됩니다.

### B: 런타임 `window.PrehideConfig`(수동 통합)

자체 호스팅되거나 수정되지 않은 번들의 경우 사전 숨김 스크립트가 실행되기 전에 구성 개체를 선언합니다.

```html
<script>
  window.PrehideConfig = {
    org: "acmecorp",        // required (or rely on baked-in __FM_CLIENT_CODE__)
    sdk: "alloy"             // optional: "alloy" (default) or "atjs"
  };
</script>
```

| 필드 | 유형 | 필수 | 설명 |
| --- | --- | --- | --- |
| `org` | string | 예(구워지지 않은 경우) | 고객 클라이언트 코드입니다. 사전 숨김 규칙을 가져오는 CDN URL의 조직 세그먼트로 사용됩니다. |
| `sdk` | `"alloy"` \| `"atjs"` | 아니오 | Adobe SDK이 페이지에 로드되었습니다. [SDK 선택](#sdk-selection)을 참조하세요. |

## SDK 선택 {#sdk-selection}

[!DNL Adobe Target]은(는) Alloy(최신 웹 SDK)와 at.js(클래식 라이브러리), 이렇게 두 개의 배달 SDK를 제공합니다. 각 요소는 개인화가 완료될 때 *서로 다른* `<style>` 요소 `id`을(를) 찾고 이를 제거하여 페이지를 표시합니다. SDK 미리 숨김은 일치하는 `id`을(를) 삽입해야 합니다. 그렇지 않으면 안전 타이머가 실행될 때까지 페이지가 숨겨집니다.

| `sdk` 값 | 스타일 태그 ID 삽입됨 | 제거된 사람 | 사용 시기 |
| --- | --- | --- | --- |
| `"alloy"` *(기본값)* | `<style id="alloy-prehiding">` | 개인화 완료 시 SDK 합금 | 이 페이지에서 Alloy/Adobe 웹 SDK을 로드 중입니다. |
| `"atjs"` | `<style id="at-body-style">` | personalize-complete의 at.js | 이 페이지에서 클래식 at.js 라이브러리를 로드하고 있습니다. |

### 설정 방법

```html
<!-- For at.js -->
<script>
  window.PrehideConfig = { org: "acmecorp", sdk: "atjs" };
</script>
<script> /* prehide.min.js inline */ </script>
<script src="https://cdn.adobe.com/.../at.js"></script>
```

>[!WARNING]
>
>불일치 경고. at.js를 로드하는 동안 `sdk: "alloy"`을(를) 설정하면(또는 그 반대의 경우) SDK에서 제거할 사전 숨김 요소를 찾을 수 없음을 의미합니다. 보호 타이머는 결국 페이지를 표시하지만 방문자는 더 긴 숨겨진 창을 경험하게 됩니다. 항상 `sdk`을(를) 로드 중인 라이브러리와 일치하도록 설정하십시오.

알 수 없거나 누락된 값이 `"alloy"`(으)로 대체되므로 기존 Alloy 통합은 구성 변경 없이 계속 작동합니다.

## 동의 관리 {#consent-management}

>[!NOTE]
>
>* 동의 값이 `window`에 저장되지 않았습니다. 함수만 노출됩니다. 내부 상태는 SDK에 비공개로 유지됩니다.
>* `"out"`에서 `"in"`(으)로의 전환은 완전히 렌더링된 콘텐츠를 다시 숨기면 시각적으로 문제가 되므로 페이지를 다시 숨기지 않습니다.
>* 단일 페이지 보기에서 `setConsent`을(를) 여러 번 호출할 수 있습니다. 각 호출은 이전 상태를 대체합니다.

사전 숨김 SDK에는 CMP와 조정하기 위한 동의 인식 API가 포함되어 있습니다. 이 옵션 사용은 선택 사항입니다. `setConsent`이(가) 호출되지 않으면 SDK은 표준 비동의 통합처럼 동작합니다.

### API 표면

```js
// Single function call. Pass a status string.
window.Prehide.setConsent("pending");  // banner shown, awaiting decision
window.Prehide.setConsent("in");       // user accepted personalization
window.Prehide.setConsent("out");      // user declined personalization

// Read-only debug snapshot.
window.Prehide.getState();
// → { sdk, version, consentStatus, consentApiUsed,
//      rulesResolved, hasSelectorsToGuard, guardTimeout }
```

### 각 상태의 기능

| 호출 | 보호 타이머에 미치는 영향 | 숨겨진 콘텐츠에 효과 |
| --- | --- | --- |
| `setConsent("pending")` | 활성 타이머가 지워졌습니다. 동의가 해결될 때까지 화재 안전을 위해 숨기지 않습니다. | 선택기는 무기한 숨겨집니다. |
| `setConsent("in")` | 선택을 취소한 후 구성된 시간 초과로 다시 시작합니다. 규칙이 아직 해결되지 않은 경우 규칙이 해결될 때까지 기다립니다. | 콘텐츠는 SDK이 개인화하거나 보호 타이머가 실행될 때까지 숨겨진 상태로 유지됩니다. |
| `setConsent("out")` | 지웠습니다. 페이지가 즉시 숨김 취소됩니다. | 페이지가 바로 표시됩니다. 나중에 확인되는 규칙은 콘텐츠를 다시 숨기지 *않습니다*. |
| *(호출되지 않음)* | 구성된 기간 동안 `init()`에서 기본 타이머가 실행됩니다. | 콘텐츠는 SDK이 개인화하거나 보호 타이머가 실행될 때까지 숨겨진 상태로 유지됩니다. (이전 버전과 호환되는 레거시 모드) |

### 권장 패턴: 명시적 보류 단계

1. CMP에서 동의 UI를 표시하는 즉시 `setConsent("pending")`을(를) 호출합니다. 이렇게 하면 안전 타이머가 지워지므로 방문자가 결정하는 동안 페이지가 숨겨져 배너 뒤에 개인화되지 않은 콘텐츠가 깜박이는 것을 방지할 수 있습니다.

   ```js
   window.Prehide.setConsent("pending");
   ```

1. 방문자가 개인화를 수락하면 `setConsent("in")`에 전화를 걸어 보세요. 보호 타이머가 다시 시작되고 Alloy/at.js 이 인수되어 개인화가 적용되면 페이지가 표시됩니다.

   ```js
   window.Prehide.setConsent("in");
   ```

1. 방문자가 개인화를 거부하면 `setConsent("out")`에 문의하십시오. 페이지가 즉시 표시되고 계속 표시됩니다. 나중에 해결되는 CDN 규칙은 다시 숨기지 않습니다.

   ```js
   window.Prehide.setConsent("out");
   ```

### 예: OneTrust 스타일 통합

```js
// Called once OneTrust has rendered its banner.
function onOneTrustReady() {
  // Pause the guard timer while the banner is visible.
  window.Prehide.setConsent("pending");

  OneTrust.OnConsentChanged(function (event) {
    if (event.consentedToTargeting) {
      window.Prehide.setConsent("in");
    } else {
      window.Prehide.setConsent("out");
    }
  });
}
```

### 예: TCF / IAB-style

```js
// Optional: pause the guard while UI is up.
window.Prehide.setConsent("pending");

// Your CMP eventually emits the final TC string.
function onTcData(tcData) {
  const hasTargetConsent = /* derive from tcData */;
  window.Prehide.setConsent(hasTargetConsent ? "in" : "out");
}
```

