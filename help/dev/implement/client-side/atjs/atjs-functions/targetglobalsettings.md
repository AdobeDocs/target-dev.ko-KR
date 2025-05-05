---
keywords: serverstate, targetGlobalSettings, targetglobalsettings, globalSettings, global 설정, at.js, function, function, clientCode, clientcode, serverDomain, serverdomain, cookieDomain, serverstate5, serverstate6, serverstate7, serverstate8, serverstate9, targetGlobalSettings0, targetGlobalSettings1, targetGlobalSettings2, targetGlobalSettings3, targetGlobalSettings4, targetGlobalSettings5, cookiedomain, crossDomain, crossdomain, timeout, globalMboxAutoCreate, visitorApiTimeout, defaultContentHiddenStyle, defaultContentVisibleStyle body, bodyBodyBodyBodySettings hidingEnabled, imsOrgId, secureOnly, overrideMboxEdgeServer, overrideMboxEdgeServerTimeout, cookiedomain5, cookiedomain6, cookiedomain7, cookiedomain8, cookiedomain9, crossDomain0, crossDomain1, crossDomain2, crossDomain3, crossDomain4, crossDomain5, optoutEnabled, optout, 옵트아웃, selectorsPollingTimeout, dataProviders, Hybrid Personalization, deviceIdLifetime
description: ' [!DNL Target] UI 또는 REST API를 사용하는 대신 설정을 재정의하려면  [!DNL Adobe Target] at.js JavaScript 라이브러리에 대해 [!UICONTROL targetGlobalSettings()] 함수를 사용하십시오.'
title: '[!UICONTROL targetGlobalSettings()] 함수를 사용하는 방법'
feature: at.js
exl-id: f6218313-6a70-448e-8555-b7b039e64b2c
source-git-commit: 12cf430b65695d38d1651f2a97df418d82d231f3
workflow-type: tm+mt
source-wordcount: '2565'
ht-degree: 18%

---

# [!UICONTROL targetGlobalSettings()]

[!DNL Target] UI에서 또는 REST API를 사용하여 설정하는 대신 `[!UICONTROL targetGlobalSettings()]`을(를) 사용하여 at.js 라이브러리의 설정을 재정의할 수 있습니다.

## 설정의 지침을 완료하여 이 설정을 변경할 수 있습니다

다음 설정을 재정의할 수 있습니다.

### aepSandboxId

* **유형**: 문자열
* **기본값**: null
* **설명**: [!DNL Target]과(와) 기본이 아닌 샌드박스에서 만든 [!DNL Adobe Experience Platform] 대상을 공유하기 위해 [!DNL Adobe Experience Platform] 샌드박스 ID를 보내는 데 사용되는 선택적 매개 변수입니다. `aepSandboxId`이(가) null이 아닌 경우 `aepSandboxName`도 제공해야 합니다.

### aepSandboxName

* **유형**: 문자열
* **기본값**: null
* **설명**: [!DNL Target]과(와) 기본이 아닌 샌드박스에서 만든 [!DNL Adobe Experience Platform] 대상을 공유하기 위해 [!DNL Adobe Experience Platform] 샌드박스 이름을 보내는 데 사용되는 선택적 매개 변수입니다. `aepSandboxName`이(가) null이 아닌 경우 `aepSandboxId`도 제공해야 합니다.

### artifactLocation

* **유형**: 문자열
* **기본값**: 없음
* **설명**: [온디바이스 의사 결정 규칙 아티팩트에 대한 정규화된 URL](../../../server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)

### bodyHiddenStyle

* **유형**: 문자열
* **기본값**: 본문 { 불투명도: 0 }
* **설명**: 깜박임 가능성을 최소화하기 위해 `globalMboxAutocreate === true`일 때만 사용됩니다.

  자세한 내용은 [at.js에서 플리커를 관리하는 방법](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)을 참조하십시오.

### bodyHidingEnabled

* **유형**: 부울
* **기본값**: true
* **설명**: `target-global-mbox`이(가) 시각적 오퍼로도 알려진 시각적 경험 작성기에서 만든 오퍼를 전달하는 데 사용될 때 깜박임을 제어하는 데 사용됩니다.

### clientCode

* **유형**: 문자열
* **기본값**: UI를 통해 설정된 값입니다.
* **설명**: 클라이언트 코드를 나타냅니다.

### cookieDomain

* **유형**: 문자열
* **기본값**: 가능한 경우 최상위 도메인으로 설정하십시오.
* **설명**: 쿠키를 저장할 때 사용되는 도메인을 나타냅니다.

### crossDomain

* **유형**: 문자열
* **기본값**: UI를 통해 설정된 값입니다.
* **설명**: 도메인 간 추적이 사용되는지 여부를 나타냅니다. 허용되는 값은 at.js 버전에 따라 다릅니다. at.js v1의 경우&#x200B;*x*&#x200B;에서 `enabled`(브라우저는 자사 쿠키와 타사 쿠키 모두 설정)을 선택하여 도메인 간 기능이 `disabled`(브라우저에서 사용자 도메인의 쿠키 설정(자사 쿠키만)), `x only`(브라우저에서 [!DNL Target]의 도메인에서만 쿠키 설정) 또는 둘 다인지 여부를 지정합니다. at.js v2.10 이상 버전의 경우 도메인 간 기능이 `enabled`(브라우저는 퍼스트 파티 쿠키와 타사 쿠키를 모두 설정함)인지 `disabled`(브라우저는 타사 쿠키를 설정하지 않음)인지를 지정합니다.

### cspScriptNonce

* **유형**: 아래의 [콘텐츠 보안 정책](#content-security-policy)을 참조하세요.
* **기본값**: 아래의 [콘텐츠 보안 정책](#content-security-policy)을 참조하십시오.
* **설명**: 아래의 [콘텐츠 보안 정책](#content-security-policy)을 참조하세요.

### cspStyleNonce

* **유형**: 아래의 [콘텐츠 보안 정책](#content-security-policy)을 참조하세요.
* **기본값**: 아래의 [콘텐츠 보안 정책](#content-security-policy)을 참조하십시오.
* **설명**: 아래의 [콘텐츠 보안 정책](#content-security-policy)을 참조하세요.

### dataProviders

* **유형**: 아래의 [데이터 공급자](#data-providers)를 참조하십시오.
* **기본값**: 아래의 [데이터 공급자](#data-providers)를 참조하십시오.
* **설명**: 아래의 [데이터 공급자](#data-providers)를 참조하십시오.

### decisioningMethod

* **유형**: 문자열
* **기본값**: 서버측
* **기타 값**: 온디바이스, 하이브리드
* **설명**: 아래 Decisioning 메서드를 참조하십시오.

  **의사 결정 메서드**

  [!DNL Target]은(는) 온디바이스 의사 결정을 통해 at.js가 사용자 경험을 전달하는 방법을 지정하는 의사 결정 메서드라는 새로운 설정을 도입합니다. `decisioningMethod`에는 서버 측 전용, 온디바이스 전용 및 하이브리드의 세 가지 값이 있습니다. `decisioningMethod`이(가) `targetGlobalSettings()`에 설정되어 있으면 모든 [!DNL Target] 결정에 대한 기본 결정 메서드로 작동합니다.

  **서버측 전용**:

  Server-side만 at.js 2.5+가 구현되고 웹 속성에 배포되는 경우 기본적으로 설정되는 기본 의사 결정 방법입니다.

  서버측만 기본 구성으로 사용하면 모든 결정이 [!DNL Target] 에지 네트워크에서 수행되며, 여기에는 차단 서버 호출이 포함됩니다. 이 접근 방식은 점진적 지연을 발생시킬 수 있지만, [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html), [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)(AP) 및 [자동 타기팅](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) 활동을 포함하는 [!DNL Target]의 기계 학습 기능을 적용할 수 있는 기능을 제공하는 등의 상당한 이점도 제공합니다.

  또한 세션 및 채널에서 지속되는 [!DNL Target]의 사용자 프로필을 사용하여 개인화된 경험을 향상하면 비즈니스에 강력한 결과를 제공할 수 있습니다.

  마지막으로, 서버측에서는 Adobe Experience Cloud만 사용할 수 있고 Audience Manager 및 Adobe Analytics 세그먼트를 통해 타깃팅할 수 있는 대상을 미세 조정할 수 있습니다.

  **온디바이스 전용**:

  온디바이스 의사 결정은 웹 페이지 전체에서 사용해야 하는 경우 온디바이스 전용 은 at.js 2.5+에서 설정해야 하는 의사 결정 방법입니다.

  온디바이스 의사 결정은 온디바이스 의사 결정의 자격이 되는 모든 활동을 포함하는 캐시된 규칙 아티팩트에서 결정되므로 매우 빠른 속도로 경험 및 개인화 활동을 제공할 수 있습니다.

  온디바이스 의사 결정의 대상이 되는 활동에 대한 자세한 내용은 지원되는 기능 섹션을 참조하십시오.

  이 결정 방법은 [!DNL Target]의 결정이 필요한 모든 페이지에서 성능이 매우 중요한 경우에만 사용해야 합니다. 또한 이 결정 방법을 선택하면 온디바이스 결정에 적합하지 않은 [!DNL Target] 활동이 전달되거나 실행되지 않습니다. at.js 라이브러리 2.5+는 의사 결정을 위해 캐시된 규칙 아티팩트만 찾도록 구성됩니다.

  **하이브리드**:

  Hybrid는 [!DNL Adobe Target] Edge 네트워크에 대한 네트워크 호출이 필요한 활동 및 온디바이스 의사 결정을 모두 실행해야 하는 경우 at.js 2.5+에서 설정해야 하는 의사 결정 메서드입니다.

  온디바이스 의사 결정 활동과 서버측 활동을 모두 관리하는 경우 페이지에 [!DNL Target]을(를) 배포하고 프로비전하는 방법을 생각하면 약간 복잡하고 지루할 수 있습니다. Decisioning 메서드로 하이브리드를 사용하면 [!DNL Target]은(는) 서버측 실행이 필요한 활동에 대해 [!DNL Adobe Target] Edge 네트워크에 대한 서버 호출을 수행해야 하는 시기와 디바이스에서 의사 결정만 실행해야 하는 시기를 알 수 있습니다.

  JSON 규칙 아티팩트에는 mbox에 실행 중인 서버측 활동 또는 온디바이스 의사 결정 활동이 있는지 여부를 at.js에 알려주는 메타데이터가 포함됩니다. 이 의사 결정 방법을 사용하면 빠르게 전달하려는 활동을 디바이스에서 의사 결정을 통해 수행할 수 있으며, 보다 강력한 ML 기반 개인화가 필요한 활동의 경우 이러한 활동이 [!DNL Adobe Target] Edge 네트워크를 통해 수행됩니다.

### defaultContentHiddenStyle

* **유형**: 문자열
* **기본값**: 표시 유형: 숨겨짐
* **설명**: 기본 콘텐츠를 숨기기 위해 DIV를 클래스 이름 &quot;mboxDefault&quot;와 함께 사용하고 `mboxCreate()`, `mboxUpdate()` 또는 `mboxDefine()`을(를) 통해 실행되는 mbox를 래핑하는 데만 사용됩니다.

### defaultContentVisibleStyle

* **유형**: 문자열
* **기본값**: 표시 여부: 표시
* **설명**: 적용된 오퍼(있는 경우) 또는 기본 콘텐츠를 표시하기 위해 DIV를 클래스 이름 &quot;mboxDefault&quot;와 함께 사용하고 `mboxCreate()`, `mboxUpdate()` 또는 `mboxDefine()`을(를) 통해 실행되는 mbox를 래핑하는 데만 사용됩니다.

### deviceIdLifetime

* **유형**: 숫자
* **기본값**: 63244800000ms = 2년
* **설명**: `deviceId`이(가) 쿠키에서 유지됩니다.

>[!NOTE]
>
>at.js 버전 2.3.1 이상에서는 deviceIdLifetime 설정을 재정의할 수 있습니다.

### 활성화됨

* **유형**: 부울
* **기본값**: true
* **설명**: 활성화되면 경험을 검색하기 위한 [!DNL Target] 요청과 경험을 렌더링하기 위한 DOM 조작이 자동으로 실행됩니다. 또한 [!DNL Target] 호출은 `getOffer(s)` / `applyOffer(s)`을(를) 통해 수동으로 실행할 수 있습니다.

  비활성화되면 [!DNL Target] 요청이 자동 또는 수동으로 실행되지 않습니다.

### globalMboxAutoCreate

* **유형**: 숫자
* **기본값**: UI를 통해 설정된 값입니다.
* **설명**: 글로벌 mbox 요청을 실행할지 여부를 나타냅니다.

### imsOrgId

* **유형**: 문자열
* **기본값**: true
* **설명**: IMS 조직 ID를 나타냅니다.

### optinEnable

* **유형**: 부울
* **기본값**: false
* **설명**: [!DNL Target]은(는) 동의 관리 전략을 지원하는 데 도움이 되도록 Adobe Experience Platform을 통해 옵트인 기능을 지원합니다. 선택 기능을 통해 고객이 [!DNL Target] 태그를 실행하는 방법과 시기를 제어할 수 있습니다. [!DNL Target] 태그를 사전 승인할 수 있는 옵션이 Adobe Experience Platform을 통해 제공됩니다. [!DNL Target] at.js 라이브러리에서 옵트인을 사용하는 기능을 활성화하려면 `optinEnabled=true` 설정을 추가하십시오. Adobe Experience Platform의 확장 프로그램 설치 보기에 있는 GDPR 옵트인 드롭다운 목록에서 &quot;활성화&quot;를 선택해야 합니다. 자세한 내용은 [Adobe Experience Platform 설명서](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)를 참조하세요. 유럽 연합의 일반 데이터 정보 보호 규정(GDPR) 및 캘리포니아 소비자 개인정보 보호법(CCPA)을 포함하여 개인정보 보호 및 데이터 보호 규정과 관련된 이 설정에 대한 자세한 내용은 [개인정보 보호 및 데이터 보호 규정](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md)을 참조하십시오.

### optoutEnabled

* **유형**: 부울
* **기본값**: false
* **설명**: [!DNL Target]에서 방문자 API `isOptedOut()` 함수를 호출해야 하는지 여부를 나타냅니다. Device Graph 지원의 일부입니다.

### overrideMboxEdgeServer

* **유형**: 부울
* **기본값**: true(at.js 버전 1.6.2부터 true)
* **설명**: `<clientCode>.tt.omtrdc.net` 도메인을 사용할지 `mboxedge<clusterNumber>.tt.omtrdc.net` 도메인을 사용할지 여부를 나타냅니다.

  이 값이 true이면 `mboxedge<clusterNumber>.tt.omtrdc.net` 도메인이 쿠키에 저장됩니다. at.js 1.8.2 및 at.js 2.3.1 이전 버전의 at.js를 사용할 때 현재 [CNAME](/help/dev/before-implement/implement-cname-support-in-target.md)에서 작동하지 않습니다. 문제가 발생하면 [at.js를 ](/help/dev/implement/client-side/atjs/target-atjs-versions.md)최신 지원되는 버전으로 업데이트하는 것이 좋습니다.

### overrideMboxEdgeServerTimeout

* **유형**: 숫자
* **기본값**: 1860000 => 31분
* **설명**: `mboxedge<clusterNumber>.tt.omtrdc.net` 값을 포함하는 쿠키 수명을 나타냅니다.

### pageLoadEnabled

* **유형**: 부울
* **기본값**: true
* **설명**: 활성화되면 페이지 로드 시 반환해야 하는 경험을 자동으로 검색합니다.

### pollingInterval

* **유형**: 숫자
* **기본값**: 300000(5분(밀리초))
* **설명**: at.js가 새 버전의 온디바이스 의사 결정 아티팩트를 가져오고 캐시를 업데이트하는 간격입니다. 3000000&rbrace;에 허용되는 최소값입니다.`pollingInterval`

### secureOnly

* **유형**: 부울
* **기본값**: false
* **설명**: at.js에서 HTTPS만 사용되는지 또는 페이지 프로토콜을 기준으로 HTTP와 HTTPS 간을 전환할 수 있는지를 나타냅니다. true로 설정하면 secureOnly는 Secure 및 SameSite 속성도 mbox 쿠키로 설정합니다.

### selectorsPollingTimeout

* **유형**: 숫자
* **기본값**: 5000ms = 5초
* **설명**: at.js 0.9.6에서 [!DNL Target]이(가) `targetGlobalSettings`을(를) 통해 재정의할 수 있는 이 새 설정을 도입했습니다.

  `selectorsPollingTimeout` 설정은 선택기로 식별된 모든 요소가 페이지에 표시되도록 하기 위해 클라이언트가 대기하는 시간을 나타냅니다.

  VEC(시각적 경험 작성기)를 통해 작성된 활동에는 선택기를 포함하는 오퍼가 있습니다.

### serverDomain

* **유형**: 문자열
* **기본값**: UI를 통해 설정된 값입니다.
* **설명**: [!DNL Target] 에지 서버를 나타냅니다.

### serverState

* **유형**: 아래의 [하이브리드 개인화](#hybrid-personalization)를 참조하십시오.
* **기본값**: 아래의 [하이브리드 개인화](#hybrid-personalization)를 참조하십시오.
* **설명**: 아래의 [하이브리드 개인화](#hybrid-personalization)를 참조하십시오.

### 원격 분석 사용

* **유형**: 부울
* **기본값**: true
* **설명**: 사용하도록 설정하면 Adobe에서 SDK 기능 사용 및 성능 원격 분석 데이터를 수집합니다. 개인 데이터는 수집되지 않습니다.

### timeout

* **유형**: 숫자
* **기본값**: UI를 통해 설정된 값입니다.
* **설명**: [!DNL Target] Edge 요청 시간 제한을 나타냅니다.

### viewsEnabled {#viewsenabled}

* **유형**: 부울
* **기본값**: true
* **설명**: 활성화되면 페이지가 로드될 때 보기가 자동으로 검색됩니다. `triggerView`이(가) 호출되면 해당 보기가 브라우저에 표시됩니다. 이 옵션을 사용하지 않으면 페이지 로드 시 보기가 검색되지 않고 `triggerView`이(가) 아무 작업도 하지 않습니다. 보기는 at.js 2에서 지원됩니다.*x* 에만 사용할 수 있습니다.

### visitorApiTimeout

* **유형**: 숫자
* **기본값**: 2000ms = 2초
* **설명**: 방문자 API 요청 시간 제한을 나타냅니다.

## 사용

이 함수는 at.js가 로드되기 전에 또는 **관리** > **구현** > **at.js 설정 편집** > **코드 설정** > **라이브러리 헤더**&#x200B;에서 정의할 수 있습니다.

라이브러리 헤더 필드에는 자유 형식 JavaScript를 입력할 수 있습니다. 사용자 지정 코드는 다음 예제와 유사해야 합니다.

```javascript {line-numbers="true"}
window.targetGlobalSettings = {
   timeout: 200, // using custom timeout
   visitorApiTimeout: 500, // using custom API timeout
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com
};
```

## 데이터 공급자 {#data-providers}

이 설정을 사용하면 고객이 Demandbase, BlueKai 및 사용자 지정 서비스와 같은 타사 데이터 공급자로부터 데이터를 수집하고, 글로벌 mbox 요청의 mbox 매개 변수로 데이터를 [!DNL Target]에 전달할 수 있습니다. 비동기 및 동기 요청을 통해 여러 공급자로부터 데이터를 수집하도록 지원합니다. 이 접근 방식을 사용하면 각 공급자에 대해 독립적인 시간 제한을 포함하여 페이지 성능에 미치는 영향을 제한하면서, 기본 페이지 콘텐츠의 깜박임을 쉽게 관리할 수 있습니다

>[!NOTE]
>
>데이터 공급자는 at.js 1.3 이상이 필요합니다.

다음 비디오에는 추가 정보가 포함되어 있습니다.

| 비디오 | 설명 |
|--- |--- |
| [Adobe Target에서 데이터 공급자 사용](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/use-data-providers-to-integrate-third-party-data.html) | 데이터 공급자는 타사의 데이터를 Target에 쉽게 전달할 수 있는 기능입니다. 타사는 기상 서비스, DMP 또는 자체 웹 서비스일 수 있습니다. 그런 다음, 이 데이터를 사용하여 대상자, Target 콘텐츠를 작성하고 방문자 프로필을 보강할 수 있습니다. |
| [Adobe Target에서 데이터 공급자 구현](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/implement-data-providers-to-integrate-third-party-data.html) | Adobe [!DNL Target]의 dataProviders 기능을 사용하여 타사 데이터 공급자로부터 데이터를 검색하고 [!DNL Target] 요청에 전달하는 방법에 대한 자세한 내용과 예제에 대한 구현입니다. |

`window.targetGlobalSettings.dataProviders` 설정은 데이터 공급자의 배열입니다.

각 데이터 공급자의 구조는 다음과 같습니다.

| 키 | 유형 | 설명 |
|--- |--- |--- |
| 이름 | 문자열 | 공급자의 이름입니다. |
| version | 문자열 | 공급자 버전입니다. 이 키는 공급자 발전에 사용됩니다. |
| timeout | 숫자 | 네트워크 요청인 경우 공급자 시간 제한을 나타냅니다.  이 키는 선택 사항입니다. |
| provider | 함수 | 공급자 데이터 가져오기 로직을 포함하는 함수입니다.<p>함수에는 단일 필수 매개 변수 `callback`이(가) 있습니다. callback 매개 변수는 데이터를 성공적으로 가져왔거나 오류가 있는 경우에만 호출되어야 하는 함수입니다.<p>콜백에는 다음 두 매개 변수가 필요합니다.<ul><li>error: 오류가 발생했는지를 나타냅니다. 모든 것이 정상이면 이 매개 변수를 null로 설정해야 합니다.</li><li>params: [!DNL Target] 요청에서 전송될 매개 변수를 나타내는 JSON 개체입니다.</li></ul> |

다음 예제에서는 데이터 공급자가 동기화 실행을 사용하는 위치를 보여 줍니다.

```javascript {line-numbers="true"}
var syncDataProvider = {
  name: "simpleDataProvider",
  version: "1.0.0",
  provider: function(callback) {
    callback(null, {t1: 1});
  }
};

window.targetGlobalSettings = {
  dataProviders: [
    syncDataProvider
  ]
};
```

at.js가 `window.targetGlobalSettings.dataProviders`을(를) 처리하면 [!DNL Target] 요청에 새 매개 변수 `t1=1`이(가) 포함됩니다.

다음은 [!DNL Target] 요청에 추가하려는 매개 변수를 Bluekai, Demandbase 등과 같은 서드파티 서비스에서 가져오는 경우의 예입니다.

```javascript {line-numbers="true"}
var blueKaiDataProvider = {
   name: "blueKai",
   version: "1.0.0",
   provider: function(callback) {
      // simulating network request
     setTimeout(function() {
       callback(null, {t1: 1, t2: 2, t3: 3});
     }, 1000);
   }
}

window.targetGlobalSettings = {
   dataProviders: [
      blueKaiDataProvider
   ]
};
```

at.js가 `window.targetGlobalSettings.dataProviders`을(를) 처리한 후 [!DNL Target] 요청에 추가 매개 변수 `t1=1`, `t2=2` 및 `t3=3`이(가) 포함됩니다.

다음 예제에서는 데이터 공급자를 사용하여 날씨 API 데이터를 수집하고 [!DNL Target] 요청에 매개 변수로 전송합니다. [!DNL Target] 요청에는 `country` 및 `weatherCondition`과(와) 같은 추가 매개 변수가 있습니다.

```javascript {line-numbers="true"}
var weatherProvider = {
      name: "weather-api",
      version: "1.0.0",
      timeout: 2000,
      provider: function(callback) {
        var API_KEY = "caa84fc6f5dc77b6372d2570458b8699";
        var lat = 44.426767399999996;
        var lon = 26.1025384;
        var url = "//api.openweathermap.org/data/2.5/weather?";
        var data = {
          lat: lat,
          lon: lon,
          appId: API_KEY
        }

        $.ajax({
          type: "GET",
                url: url,
          dataType: "json",
          data: data,
          success: function(data) {
            console.log("Weather data", data);
            callback(null, {
              country: data.sys.country,
              weatherCondition: data.weather[0].main
            });
          },
          error: function(err) {
            console.log("Error", err);
            callback(err);
          }
        });
      }
    };

    window.targetGlobalSettings = {
      dataProviders: [weatherProvider]
    };
```

`dataProviders` 설정을 사용할 때는 다음 사항을 고려하십시오.

* `window.targetGlobalSettings.dataProviders`에 추가된 데이터 공급자가 비동기 상태인 경우 병렬로 실행됩니다. 방문자 API 요청은 최소 대기 시간을 허용하기 위해 `window.targetGlobalSettings.dataProviders`에 추가된 함수와 함께 실행됩니다.
* at.js는 데이터를 캐시하려고 하지 않습니다. 데이터 공급자는 데이터를 한 번만 가져오는 경우 데이터가 캐시되는지 확인해야 하고, 공급자 함수가 호출될 때 두 번째 호출을 위해 캐시 데이터를 제공해야 합니다.

## 콘텐츠 보안 정책

at.js 2.3.0+에서는 전달된 [!DNL Target] 오퍼를 적용할 때 페이지 DOM에 추가된 SCRIPT 및 STYLE 태그에 대한 콘텐츠 보안 정책 임시 설정을 지원합니다.

at.js 2.3.0+를 로드하기 전에 SCRIPT 및 STYLE nonces를 `targetGlobalSettings.cspScriptNonce` 및 `targetGlobalSettings.cspStyleNonce`에 각각 설정해야 합니다. 아래 예를 참조하십시오.

```javascript {line-numbers="true"}
...
<head>
 <script nonce="<script_nonce_value>">
window.targetGlobalSettings = {
  cspScriptNonce: "<csp_script_nonce_value>",
  cspStyleNonce: "<csp_style_nonce_value>"
};
 </script>
 <script nonce="<script_nonce_value>" src="at.js"></script>
...
</head>
...
```

`cspScriptNonce` 및 `cspStyleNonce` 설정이 지정된 후 at.js 2.3.0+는 [!DNL Target] 오퍼를 적용할 때 DOM에 추가하는 모든 SCRIPT 및 STYLE 태그에서 임시 특성으로 설정합니다.

## 하이브리드 개인화

`serverState`은(는) at.js v2.2+에서 사용할 수 있는 설정이며, [!DNL Target]의 하이브리드 통합이 구현될 때 페이지 성능을 최적화하는 데 사용할 수 있습니다. 하이브리드 통합은 클라이언트측에서 at.js v2.2+를 사용하고 있으며, 서버측에서 배달 API 또는 [!DNL Target] SDK를 모두 사용하고 있음을 의미합니다. `serverState` 는 at.js v2.2+에서 서버측에서 가져온 콘텐츠에서 직접 경험을 적용하고 서비스되는 페이지의 일부로 클라이언트에 반환할 수 있는 기능을 제공합니다.

### 전제 조건

[!DNL Target]의 하이브리드 통합이 있어야 합니다.

* **서버측**: [배달 API](/help/dev/implement/delivery-api/overview.md) 또는 [Target SDK](/help/dev/implement/server-side/sdk-guides/getting-started/getting-started.md)를 사용해야 합니다.
* **클라이언트측**: [at.js 버전 2.2 이상](/help/dev/implement/client-side/atjs/target-atjs-versions.md)을 사용해야 합니다.

### 코드 샘플

작동 방식을 더 잘 이해하려면 서버에 있는 아래 코드 예를 참조하십시오. 이 코드는 사용자가 [Target Node.js SDK](https://github.com/adobe/target-nodejs-sdk)를 사용하고 있다고 가정합니다.

```javascript {line-numbers="true"}
// First, we fetch the offers via Target Node.js SDK API, as usual
const targetResponse = await targetClient.getOffers(options);
// A successfull response will contain Target Delivery API request and response objects, which we need to set as serverState
const serverState = {
  request: targetResponse.request,
  response: targetResponse.response
};
// Finally, we should set window.targetGlobalSettings.serverState in the returned page, by replacing it in a page template, for example
const PAGE_TEMPLATE = `
<!doctype html>
<html>
<head>
  ...
  <script>
    window.targetGlobalSettings = {
      overrideMboxEdgeServer: true,
      serverState: ${JSON.stringify(serverState, null, " ")}
    };
  </script>
  <script src="at.js"></script>
</head>
...
</html>
`;
// Return PAGE_TEMPLATE to the client ...
```

보기 미리 가져오기에 대한 샘플 `serverState` 개체 JSON은 다음과 같습니다.

```javascript {line-numbers="true"}
{
 "request": {
  "requestId": "076ace1cd3624048bae1ced1f9e0c536",
  "id": {
   "tntId": "08210e2d751a44779b8313e2d2692b96.21_27"
  },
  "context": {
   "channel": "web",
   "timeOffsetInMinutes": 0
  },
  "experienceCloud": {
   "analytics": {
    "logging": "server_side",
    "supplementalDataId": "7D3AA246CC99FD7F-1B3DD2E75595498E"
   }
  },
  "prefetch": {
   "views": [
    {
     "address": {
      "url": "my.testsite.com/"
     }
    }
   ]
  }
 },
 "response": {
  "status": 200,
  "requestId": "076ace1cd3624048bae1ced1f9e0c536",
  "id": {
   "tntId": "08210e2d751a44779b8313e2d2692b96.21_27"
  },
  "client": "testclient",
  "edgeHost": "mboxedge21.tt.omtrdc.net",
  "prefetch": {
   "views": [
    {
     "name": "home",
     "key": "home",
     "options": [
      {
       "type": "actions",
       "content": [
        {
         "type": "setHtml",
         "selector": "#app > DIV.app-container:eq(0) > DIV.page-container:eq(0) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(1) > DIV.heading:eq(0) > H1.title:eq(0)",
         "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > H1:nth-of-type(1)",
         "content": "<span style=\"color:#FF0000;\">Latest</span> Products for 2020"
        }
       ],
       "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
       "responseTokens": {
        "profile.memberlevel": "0",
        "geo.city": "dublin",
        "activity.id": "302740",
        "experience.name": "Experience B",
        "geo.country": "ireland"
       }
      }
     ],
     "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
    }
   ]
  }
 }
}
```

페이지가 브라우저에 로드되면 at.js가 [!DNL Target] 에지에 대해 네트워크 호출을 실행하지 않고 `serverState`의 모든 [!DNL Target] 오퍼를 즉시 적용합니다. 또한 at.js는 가져온 콘텐츠 서버측에서 [!DNL Target] 오퍼를 사용할 수 있는 DOM 요소만 미리 숨김으로써 페이지 로드 성능 및 최종 사용자 경험에 긍정적인 영향을 줍니다.

### 중요 정보

`serverState`을(를) 사용할 때는 다음 사항을 고려하십시오.

* 현재 at.js v2.2에서는 다음에 대해 serverState를 통한 경험 전달만 지원합니다.

   * 페이지 로드 시 실행되는 VEC 생성 활동.
   * 미리 가져온 보기.

     at.js API에서 [!DNL Target] 보기 및 `triggerView()`을(를) 사용하는 SPA의 경우, at.js v2.2는 서버측에서 미리 가져온 모든 보기에 대한 콘텐츠를 캐시하고 각 보기가 `triggerView()`을(를) 통해 트리거되는 즉시 적용하며, [!DNL Target]에 대한 추가적인 콘텐츠 가져오기 호출을 실행하지 않습니다.

   * **참고**: 현재 서버측에서 검색된 mbox는 `serverState`에서 지원되지 않습니다.

* `serverState` 오퍼를 적용할 때 at.js는 `pageLoadEnabled` 및 `viewsEnabled` 설정을 고려합니다. 예를 들어 `pageLoadEnabled` 설정이 false인 경우 페이지 로드 오퍼가 적용되지 않습니다.

  이 설정을 켜려면 **관리 > 구현 > 편집 > 페이지 로드 활성화됨**&#x200B;에서 토글을 활성화하십시오.

  ![페이지 로드 사용 설정](../../assets/page-load-enabled-setting.png)

* `serverState`을(를) 사용하고 반환된 콘텐츠에서 `<script>` 태그를 사용하는 경우 HTML 콘텐츠에서 `</script>` 대신 `<\/script>`을(를) 사용하는지 확인하십시오. `</script>`을(를) 사용하는 경우 브라우저에서 `</script>`을(를) 인라인 스크립트의 끝으로 해석하므로 HTML 페이지가 손상될 수 있습니다.

### 추가 리소스

`serverState`의 작동 방식에 대해 자세히 알아보려면 다음 리소스를 확인하십시오.

* [샘플 코드](https://github.com/Adobe-Marketing-Cloud/target-node-client-samples/tree/master/advanced-atjs-integration-serverstate).
* `serverState`[&#128279;](https://github.com/Adobe-Marketing-Cloud/target-node-client-samples/tree/master/react-shopping-cart-demo)이(가) 있는 단일 페이지 응용 프로그램(SPA) 샘플 앱입니다.
