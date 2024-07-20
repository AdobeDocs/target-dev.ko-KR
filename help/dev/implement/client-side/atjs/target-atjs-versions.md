---
keywords: at.js 릴리스, at.js 버전, 릴리스 정보
description: ' [!DNL Adobe Target] at.js JavaScript 라이브러리의 각 버전 변경 내용에 대한 세부 사항을 봅니다.'
title: at.js의 각 버전에 포함된 것은 무엇입니까?
feature: at.js
exl-id: 609dacba-2ab8-45e9-b189-928d59938c98
source-git-commit: 9999c1b5f603e6607bd81f6ad6a06a7f74e76acb
workflow-type: tm+mt
source-wordcount: '4904'
ht-degree: 64%

---

# at.js 버전 세부 사항

[!DNL Adobe Target] at.js JavaScript 라이브러리의 각 버전 변경 내용에 대한 세부 사항입니다.

>[!IMPORTANT]
>
>[!DNL Adobe Target]은(는) at.js 1을 모두 지원합니다.*x*&#x200B;와 at.js 2 모두에 있는 Hide Body(본문 숨기기) 및 Show Body(본문 표시) 호출을 보여줍니다.*x*.
>
>at.js 1.*x*&#x200B;이(가) 유지 관리 모드로 들어갔습니다. [!DNL Target] 팀은 필요한 경우 버그 수정 및 보안 패치를 릴리스합니다.
>
>[!DNL Target] 팀은 at.js 2에 대한 모든 지원을 제공합니다.*x*&#x200B;을(를) 통해 버그 수정, 보안 패치, 기능 및 성능 최적화를 지속적으로 릴리스할 수 있습니다.
>
>둘 중 하나의 최신 버전으로 업그레이드해야 합니다.*x* 또는 2.*x*&#x200B;을(를) 통해 해당 주 버전의 이전 부 버전에서 발견된 문제에 대한 버그 수정 및 보안 패치를 얻을 수 있습니다.

[Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)의 태그는 at.js를 업그레이드하는 기본 방법입니다. 확장 개발자는 확장에 새로운 기능을 지속적으로 추가하고 버그를 자주 수정합니다. 이러한 업데이트는 새로운 버전의 확장에 패키지화되어 Adobe Experience Platform 카탈로그에서 업그레이드로 사용할 수 있습니다. 자세한 내용은 *태그 개요* 안내서의 [확장 업그레이드](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/extensions/extension-upgrade.html)를 참조하십시오.6+

## at.js 버전 2.11.4 (2024년 1월 24일 목요일)

* 잘못된 지역 데이터가 배달 API로 전송되지 않도록 at.js가 업데이트되었습니다.

## at.js 버전 2.11.3(2023년 11월 21일)

* `at-content-rendering-failed`개 이벤트에서 응답 토큰을 보낼 수 없는 문제를 해결했습니다.

## at.js 버전 2.11.2(2023년 10월 26일)

* 사용자 지정 이벤트에서 전송된 응답 토큰에 불일치가 발생하는 문제를 해결했습니다.

## at.js 버전 2.11.1(2023년 10월 13일)

* at.js를 실행하는 페이지가 quirks 모드에 있는 동안 확인할 수 없는 오류가 발생하는 문제를 해결했습니다.

## at.js 버전 2.11.0(2023년 10월 10일)

* `getOffer/getOffers` 호출 시 배달 API로 전달되는 `targetGlobalSettings`의 사용자 지정 [!DNL Adobe Experience Platform](AEP) `sandboxId` 및 `sandboxName` 설정에 대한 지원이 추가되었습니다.
* 선택기에서 `:eq()`을(를) 연결하는 섀도 DOM 수정.

## at.js 버전 2.10.3(2023년 9월 12일)

* 렌더링되는 오퍼가 없을 때 `at-content-rendering-succeeded` 사용자 지정 이벤트를 잘못 트리거하는 문제를 해결했습니다. 올바른 이벤트 `at-content-rendering-no-offers`이(가) 트리거되었습니다.
* `at-content-rendering-failed` 사용자 지정 이벤트에 대한 오류 개체에 `eventToken` 및 `responseTokens`을(를) 추가했습니다.

## at.js 버전 2.10.2 (2023년 3월 7일)

* `trackEvent` 함수가 항상 오류를 반환하는 문제가 해결되었습니다.

## at.js 버전 2.10.1 (2023년 2월 2일)

* 이름에 점이 있는 매개변수를 포함하는 대상자 규칙과 관련된 활동이 온디바이스 결정을 위해 예상되는 경험을 반환하지 않는 버그가 수정되었습니다.
* mboxDisable이 활성화된 경우에도 at.js가 게재 호출을 실행하는 at.js 2.6.0에서 도입된 버그를 수정했습니다.

## at.js 버전 2.10.0(2022년 9월 19일 화요일)

* 서드파티 쿠키 지원이 추가되었습니다.

## at.js 버전 2.9.0(2022년 5월 27일)

* [사용자 에이전트 클라이언트 힌트](user-agent-and-client-hints.md) 지원이 추가되었습니다.
* 동일한 페이지의 여러 mbox 요청에 서로 다른 노출 ID가 있는 버그가 수정되었습니다.

## at.js 버전 2.8.1 (2022년 1월 28일)

* `pageLoad`이(가) ODD(On Device Decisioning) 하이브리드 실행 모드에서 target-global-mbox에 매핑되지 않는 문제를 해결했습니다.
* mbox 요청에 대한 분석 세부 정보 관련 문제가 해결되었습니다.
* 보안 취약성을 해결하기 위해 개발 종속성이 업그레이드되었습니다.

## at.js 버전 2.8.0 (2022년 1월 7일)

이제 [!DNL Target] at.js JavaScript 라이브러리가 기능 사용 및 성능 원격 분석 데이터를 수집합니다. 개인 데이터는 수집되지 않습니다. 이 기능은 `targetGlobalSettings`에서 `telemetryEnabled`를 false로 설정하여 옵트아웃할 수 있습니다. 자세한 내용은 [telemetryEnabled in targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#telemetryenabled)를 참조하십시오.

## at.js 버전 2.7.0(2021년 10월 28일)

이번 릴리스에는 다음과 같은 개선 사항이 포함됩니다.

* [웹 구성 요소](https://developer.mozilla.org/en-US/docs/Web/Web_Components)에 대한 지원이 추가되었습니다. 이 버전의 at.js는 맞춤형 요소 및 맞춤형 요소 내부의 요소에 대한 개인화된 경험과 오퍼를 만들고 테스트하는 데 필요합니다. 이 기능은 [!DNL Target Standard/Premium] 21.10.5 릴리스에 포함되어 있습니다.

## at.js 1.8.3 (2021년 9월 21일)

이번 릴리스에는 다음과 같은 변경 사항이 포함됩니다.

* `window.default` 또는 `document-default`을(를) 설정한 고객에 대해 Platform launch 빌드가 올바르게 작동하도록 `reactor-window` 및 `reactor-document` Adobe Experience Platform Launch 모듈을 제거했습니다.
* 이제 at.js 1.8.3은 서드파티 도메인 쿠키가 제대로 설정되었는지 확인하기 위해 `Samesite=None` 및 `Secure`을(를) 명시적으로 설정합니다.

## at.js 2.6.1 (2021년 8월 16일)

* 온디바이스 의사 결정 사용 시 “하이브리드 모드에 대해 사용 가능한 아티팩트 없음” 버그가 수정되었습니다.

## at.js 2.6.0 (2021년 7월 16일)

* at.js settings `secureOnly`가 `true`로 설정될 때마다 쿠키에 보안 속성이 추가됩니다.
* 이제 `triggerView()`를 사용할 때 응답 토큰을 사용할 수 있습니다.
* `CONTENT_RENDERING_NO_OFFERS` 이벤트와 관련된 문제가 해결되었습니다. 이제 [!DNL Target]에서 반환되는 내용이 없을 때 이 이벤트가 정상적으로 트리거됩니다.
* `prefetch` 요청을 사용할 때 [!UICONTROL Analytics for Target] (A4T) 클릭 메트릭 세부 사항이 정상적으로 반환됩니다.
* UUID 생성이 더 이상 `Math.random()`을 사용하지 않고 `window.crypto`를 사용합니다.
* 모든 네트워크 호출에서 `sessionId` 쿠키 만료가 정상적으로 연장됩니다.
* 이제 SPA(단일 페이지 애플리케이션) 보기 캐시 초기화가 올바르게 처리되며 `viewsEnabled` 설정이 적용됩니다. `viewsEnabled`을(를) `false` 값으로 설정하면 이제 `triggerView()` 함수가 비활성화됩니다. [초기 페이지 로드 작업 순서](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md#order)를 참조하세요.

## at.js 2.5.0 (2021년 5월 13일)

이 at.js의 릴리스에는 다음과 같은 개선 사항 및 변경 사항이 포함되어 있습니다.

* at.js에 대한 [온디바이스 의사 결정](/help/dev/implement/client-side/atjs/on-device-decisioning/on-device-decisioning.md) 지원
* 자동화된 개인화 활동에 대한 [링크 미리보기](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) 지원

이 릴리스는 또한 Microsoft Internet Explorer 10 이상의 버전에 대한 지원을 제거합니다.

## at.js 2.4.1(2021년 3월 23일)

at.js 유지 관리 릴리스이며, 다음과 같은 개선 기능 및 수정 사항이 포함되어 있습니다.

* mbox 요청에 포함되는 `targetPageParams`에 관한 문제가 해결되었습니다. `targetPageParams`은 `pageLoad` 요청에만 포함되어야 합니다. (TNT-40247)
* Adobe Experience Platform 확장에서 를 참조하는 최적화된 창 및 문서 전역 (TNT-37124)

## at.js 2.4.0(2021년 1월 14일)

at.js 유지 관리 릴리스이며, 다음과 같은 수정 사항이 포함되어 있습니다.

* 통합 프로필/플랫폼 ID에 대한 지원을 배달 API customerIds에 추가합니다.
* 잘못된 스타일 태그 삽입을 해결합니다.

## at.js 2.3.3 (2020년 11월 13일)

at.js 유지 관리 릴리스이며, 다음과 같은 수정 사항이 포함되어 있습니다.

* mbox 클릭 추적 및 A4T와 관련된 문제가 해결되었습니다. 0n-클릭으로 [!DNL Target]에서 올바른 mbox 및 mbox 매개 변수를 사용하여 배달 API 호출을 실행했습니다. 그러나 SDID가 [!DNL Analytics] 호출의 SDID와 일치하지 않으므로 히트 결합과 전환이 없습니다. (TNT-38372)

## at.js 2.3.2(2020년 7월 24일)

at.js 유지 관리 릴리스이며, 다음과 같은 수정 사항이 포함되어 있습니다.

* 스크립트 또는 코드가 창 또는 문서에 기본 속성을 추가할 때의 버그를 해결했습니다.

## at.js 1.8.2 (2020년 6월 15일)

at.js 유지 관리 릴리스이며, 다음과 같은 수정 사항이 포함되어 있습니다.

* CNAME 및 에지 재정의 at.js 1을 사용할 때 문제를 해결했습니다.*x* 가 서버 도메인을 잘못 만들어 [!DNL Target] 요청에 실패할 수 있습니다. (TNT-35064)

## at.js 2.3.1 릴리스(2020년 6월 15일)

at.js 유지 관리 릴리스이며, 다음과 같은 개선 기능 및 수정 사항이 포함되어 있습니다.

* [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)를 통해 `deviceIdLifetime` 설정을 재정의할 수 있게 했습니다. (TNT-36349)
* CNAME 및 에지 재정의 at.js 2를 사용할 때 문제를 해결했습니다.*x* 가 서버 도메인을 잘못 만들어 [!DNL Target] 요청에 실패할 수 있습니다. (TNT-35065)
* [!DNL Target] 확장 v2 및 [!UICONTROL Adobe Analytics Launch] 확장을 사용할 때 [!DNL Target]이(가) [!DNL Analytics] `sendBeacon` 호출을 지연시키는 문제를 해결했습니다. (TNT-36407, TNT-35990, TNT-36000)

## at.js 버전 2.3.0 (2020년 3월 25일 목요일)

at.js 유지 관리 릴리스이며, 다음과 같은 개선 기능 및 수정 사항이 포함되어 있습니다.

* 전달된 [!DNL Target] 오퍼를 적용할 때 페이지 DOM에 추가되는 SCRIPT 및 STYLE 태그에 대한 콘텐츠 보안 정책 임시 설정을 지원합니다. at.js에서 적용된 오퍼에 해당 스크립트 및 스타일 태그 주석을 설정할 수 있도록 고객은 `targetGlobalSettings.cspScriptNonce` 및 `targetGlobalSettings.cspStyleNonce`을(를) 설정할 수 있습니다. 자세한 내용은 [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)를 참조하십시오.
* Google Tag Manager 배포용 Google Closure 컴파일러로 at.js를 컴파일할 때 발생하는 문제를 수정했습니다.
* 고객 구현과 충돌을 방지하기 위해 at.js 검사 쿠키의 이름을 `check`에서 `at_check`(으)로 변경했습니다.

## at.js 버전 1.8.1 (2020년 3월 25일 목요일)

at.js 유지 관리 릴리스이며, 다음과 같은 개선 기능 및 수정 사항이 포함되어 있습니다.

* 고객 구현과 충돌을 방지하기 위해 at.js 검사 쿠키의 이름을 `check`에서 `at_check`(으)로 변경했습니다.

## at.js 버전 2.2.0(2019년 10월 10일)

이번 at.js 릴리스에는 다음과 같은 개선 사항 및 수정 사항이 포함되어 있습니다.

* 페이지 요소에 [!DNL Adobe Analytics] 코드가 없을 때 클릭 추적이 [!DNL Analytics for Target](A4T)에서 전환을 보고하지 않는 문제를 해결했습니다.
* 웹 페이지에서 ECID(Experience Cloud ID 서비스) v4.4와 at.js 2.2를 모두 사용할 때 성능이 향상되었습니다.
* 이전에는 at.js가 경험을 가져오기 전에 ECID가 두 번의 차단 호출을 했습니다. 이것이 한 번의 호출로 줄어들어 성능이 크게 향상되었습니다.
* 기본 오퍼의 이벤트 토큰이 전송된 알림에 포함되지 않던 잘못된 프리페치된 보기 처리가 수정되었습니다.

>[!NOTE]
>
>ECID 확장을 v4.4로 업그레이드하여 향상된 성능을 이용해 보십시오.

* at.js 버전 2.2에서는 `serverState`이라는 새 설정도 제공합니다. 이 설정은 [!DNL Target]의 하이브리드 통합이 구현될 때 페이지 성능을 최적화하는 데 사용할 수 있습니다. 하이브리드 통합은 클라이언트측에서 at.js v2.2+를 사용하고 있으며, 서버측에서 배달 API 또는 [!DNL Target] SDK를 모두 사용하고 있음을 의미합니다. `serverState`은(는) at.js v2.2+에서 서버측에서 가져온 콘텐츠에서 직접 경험을 적용하고 서비스되는 페이지의 일부로 클라이언트에 반환할 수 있는 기능을 제공합니다. 자세한 내용은 [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#serverstate)의 &quot;serverState&quot;를 참조하십시오.

## at.js 버전 1.8.0(2019년 10월 10일)

이번 at.js 릴리스에는 다음과 같은 개선 사항 및 수정 사항이 포함되어 있습니다.

* 웹 페이지에서 ECID(Experience Cloud ID 서비스) v4.4와 at.js 1.8을 모두 사용할 때 성능이 향상되었습니다.
* 이전에는 at.js가 경험을 가져오기 전에 ECID가 두 번의 차단 호출을 했습니다. 이것이 한 번의 호출로 줄어들어 성능이 크게 향상되었습니다.

>[!NOTE]
>
>ECID 확장을 v4.4로 업그레이드하여 향상된 성능을 이용해 보십시오.

## at.js 버전 2.1.1(2019년 7월 24일)

at.js 유지 관리 릴리스이며, 다음과 같은 개선 기능 및 수정 사항이 포함되어 있습니다.

(괄호로 묶인 문제 번호는 내부 Adobe용입니다.)

* Visual Experience Composer(VEC)의 목표 및 설정 페이지에서 클릭 추적 지표를 사용할 때 여러 개의 비콘이 실행되는 문제를 해결했습니다. (TNT-32812)
* `triggerView()` 이 오퍼를 두 번 이상 렌더링하지 않는 문제를 해결했습니다. (TNT-32780)
* `triggerView()` 이 요청에서 MCID(Marketing Cloud ID) 정보가 포함되어 있는지 확인하는 문제를 해결했습니다. (TNT-32776)
* 저장된 보기가 없는 경우에도 `triggerView()` 알림이 실행되지 않는 문제를 해결했습니다. (TNT-32614)
* URL에 잘못된 형식의 쿼리 문자열 매개 변수가 포함되어 있을 때 decodeURIcomponent를 사용하여 오류가 발생하는 문제를 해결했습니다. (TNT-32710)
* 이제 `Navigator.sendBeacon()` API를 통해 전송된 배달 요청의 컨텍스트에서 비콘 플래그가 &#39;true&#39;로 설정됩니다. (TNT-32683)
* 일부 고객의 웹 사이트에서 추천 오퍼가 표시되지 않는 문제를 해결했습니다. 고객이 배달 API 호출에서 오퍼 콘텐츠를 볼 수 있지만 오퍼가 웹 사이트에 적용되지 않았습니다. (TNT-32680)
* 여러 경험에서 클릭 추적이 예상대로 작동되지 않는 문제를 해결했습니다. (TNT-32644)
* 첫 번째 지표 렌더링이 실패한 후 at.js에서 두 번째 지표를 적용하지 못했던 문제를 해결했습니다. (TNT-32628)
* 요청 페이로드가 쿼리 매개 변수 또는 요청 페이로드에 존재하지 않는 `mbox3rdPartyId` 함수를 사용하여 `targetPageParams`을 전달할 때 발생하는 문제를 해결했습니다. (TNT-32613)
* Chromium 기반 브라우저(Google Chrome 포함)에서 디스플레이 및 클릭 알림 응답이 차단되는 문제를 해결했습니다. (TNT-32290)

## at.js 버전 2.1.0(2019년 6월 3일)

이 릴리스에는 다음과 같은 기능 및 개선 사항이 포함되었습니다.

* **Adobe 옵트인(Opt-in) 지원**: Adobe 옵트인(Opt-in)은 동의 관리 플랫폼과 Adobe 솔루션과의 통합을 간소화하는 방법입니다. Adobe 옵트인에 대한 자세한 내용은 [개인 정보 및 GDPR(일반 데이터 보호 규정)](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md)을 참조하십시오.

* **업계 표준 CSP 준수**: at.js는 더 이상 eval()을 사용하여 JavaScript를 실행하지 않습니다.

* **클라이언트 측 분석 로깅**: 클라이언트 측이든 아니면 서버측이든 간에 분석 데이터를 [!DNL Adobe Analytics]에 보내는 방법을 고객이 완벽하게 제어할 수 있도록 합니다.

  자세한 내용은 [클라이언트측 [!DNL Analytics] 로깅](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html#client-side)을 참조하십시오.

* **알림 보내기**: 경험이 `applyOffer()` 또는 `applyOffers()` 대신 코드로 렌더링될 때 개발자가 알림을 전송할 수 있습니다.

  자세한 내용은 [adobe.target.sendNotifications(options)](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)를 참조하십시오.

* **at.js 크기가 24%까지 줄어듦**: at.js의 크기가 24%까지 줄어듭니다. 파일 크기가 작을수록 페이지 로드 성능이 향상되고 페이지의 at.js 다운로드 시간이 줄어듭니다.

## at.js 버전 2.0.1(2019년 3월 19일)

유지 관리 릴리스이며, 다음과 같은 개선 기능 및 수정 사항이 포함되어 있습니다.

(괄호로 묶인 문제 번호는 내부 Adobe용입니다.)

* 특정 고객에 대해 JavaScript 예외가 발생한 DOM 폴링 코드의 경합 조건을 수정했습니다. (TNT-31869)
* 보기가 렌더링되었다는 알림이 클릭 추적 이벤트 핸들러에서 분리되었습니다. 처음에는 렌더링된 보기에 속하는 클릭 이벤트 처리기를 연결할 수 없는 경우 [!DNL Target]에서 알림을 보내지 않았습니다. 이제 클릭 요소를 찾을 수 없는 경우에도 [!DNL Target]에서 보기 알림을 보냅니다. (TNT-31969)
* request-succeeded 이벤트 리디렉션 플래그가 항상 true로 설정되는 문제가 해결되었습니다. (TNT-31907)
* 요소가 누락된 경우에도 VEC 재정렬 작업이 성공으로 기록되는 문제가 해결되었습니다. (TNT-31924)
* 특정 고객에 대한 알림에 엔터프라이즈 권한 속성 토큰이 포함되지 않는 문제가 해결되었습니다. (TNT-31999)

## at.js 버전 1.7.1(2019년 3월 19일)

유지보수 릴리스이며, 다음과 같은 수정 사항이 포함되어 있습니다.

(괄호로 묶인 문제 번호는 내부 Adobe용입니다.)

* 특정 고객에 대해 JavaScript 예외가 발생한 DOM 폴링 코드의 경합 조건을 수정했습니다. (TNT-31869)

## at.js 버전 2.0.0

at.js 2에서는 차세대 클라이언트측 기술에 대한 개인화를 실행하도록 기업을 지원하는 다양한 기능 세트를 제공합니다. 이 새로운 버전은 단일 페이지 애플리케이션(SPA)과 조화로운 상호 작용을 하도록 at.js를 업그레이드하는 데 주력하고 있습니다.

at.js 2.x를 사용하면 이전 버전에서 사용할 수 없는 다음과 같은 몇 가지 이점이 있습니다.

* 페이지 로드 시 모든 오퍼를 캐시하여 여러 서버 호출을 하나의 서버 호출로 줄일 수 있습니다.
* 오퍼가 기존 서버 호출로 인해 초래되는 지연 없이 캐시를 통해 즉시 표시되므로 사이트에서 최종 사용자의 경험을 크게 향상시킬 수 있습니다.
* 간단한 1줄의 코드 및 일회용 개발자 설정으로 마케터가 단일 페이지 애플리케이션에서 시각적 경험 작성기(VEC)를 통해 A/B 및 경험 타기팅 (XT) 활동을 만들고 실행할 수 있도록 할 수 습니다.

at.js 2.x에서는 다음과 같은 새로운 기능을 도입했습니다.

* getOffers()
* applyOffers()
* triggerView()

다음 함수는 at.js 2.x의 도입으로 더 이상 사용되지 않습니다.

* mboxCreate()
* mboxDefine
* registerExtension()

자세한 내용은 [at.js 1.x에서 at.js 2.x로 업그레이드](/help/dev/implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md) 및 [at.js 함수](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md)를 참조하십시오.

>[!NOTE]
>
>[일반 데이터 보호 규정](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md)(GDPR)에 대한 Adobe 옵트인 지원이 필요한 경우, 현재 at.js 1.7.0 또는 at.js 2.1.0 이상을 사용해야 합니다.

## at.js 버전 1.7.0

at.js 1.7.0에서는 Adobe 옵트인을 지원합니다. Adobe 옵트인(Opt-in)은 동의 관리 플랫폼과 Adobe 솔루션과의 통합을 간소화하는 방법입니다.

Adobe 옵트인에 대한 자세한 내용은 [개인 정보 보호 및 일반 데이터 보호 규정](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md)(GDPR)을 참조하십시오.

또한 이 릴리스에서는 [!DNL Target]이(가) 리디렉션 URL에서 발생하는 매개 변수로 리디렉션 URL 매개 변수를 무시할 수 있는 문제를 수정합니다.

>[!NOTE]
>
>GDPR에 대한 Adobe 옵트인 지원이 필요한 경우 현재 at.js 1.7.0 또는 at.js 2.1.0 이상을 사용해야 합니다.

## at.js 버전 1.6.4

at.js 1.6.4는 유지보수 릴리스이며 다음 문제를 해결합니다.

* Microsoft Internet Explorer 11에서 중복된 오퍼가 적용되는 경합 조건 매니페스트를 수정했습니다.

## at.js 버전 1.6.3

at.js 버전 1.6.3에는 다음의 수정 사항과 개선 사항이 포함되어 있습니다.

* 이제 선택기는 십진수, 하이픈 두 개 또는 뒤에 십진수가 있는 하이픈(예: #-123)으로 시작하는 ID 또는 CSS 클래스를 포함하는 경우 CSS가 이스케이프 처리됩니다. (TNT-31061)
* 동일한 CSS 선택기에 적용되는 서로 다른 활동의 시각적 경험 작성기(VEC) 오퍼가 활동 우선순위를 준수하지 않는 at.js 1.6.2에서 발생하는 문제를 수정했습니다. (TNT-31052)
* 약속에 대한 기본 지원이 없는 환경에서 약속 시간 제한 관련 문제를 해결했습니다. (TNT-30974)
* 이제 콘텐츠 렌더링 실패 이벤트를 통해 문제가 올바로 캡처되고 보고됩니다. 이전에는 사실이 아님에도 불구하고 JavaScript가 성공적으로 실행된 것으로 보고되었습니다. (TNT-30599)

## at.js 버전 1.6.2

유지보수 릴리스이며 다음 문제를 해결합니다.

* 일부 고객 사이트에서 무한 &quot;비동기화&quot; 루프가 발생하는 문제를 해결했습니다.

>[!WARNING]
>
>또한 at.js 버전 1.6.2에는 at.js 버전 1.6.1 및 1.6.0에 포함된 모든 개선 사항 및 수정 사항이 포함되어 있으며 이러한 버전은 더 이상 다운로드할 수 없습니다. 1.6.1 또는 1.6.0을 사용하는 경우 버전 1.6.2로 업그레이드하는 것이 좋습니다

다음은 at.js 버전 1.6.1에 포함된 개선 사항 및 수정 사항입니다.

* 권장 사항이 Microsoft Internet Explorer 11에서 복제되도록 하는 at.js 1.6.0 문제가 해결되었습니다. (TNT-30593)
* 이제 at.js는 사용자가 세션 중에 엣지를 변경하는 경우 엣지 오버라이드 로직이 엣지 클러스터 쿠키의 존재 여부를 확인하여 다른 엣지 번호가 발생하지 않도록 합니다. (TNT-30563)
* HTML 콘텐츠에 잘못된 JS 코드가 포함된 경우 at.js가 후속 조치를 실행하지 못하도록 하는 문제가 수정되었습니다. 이제 at.js는 오류를 로그하고 문제 없이 나머지 조치를 렌더링합니다. (TNT-30546)
* .리디렉션 페이지가 리디렉션 활동에 대해 다시 자격을 확보할 때 예외가 발생하도록 변경했습니다. (TNT-30532)
* getOffer() API 요청에서 올바른 요청 제한 시간이 적용되지 않는 문제가 수정되었습니다. (TNT-30498)
* 파일 프로토콜을 사용할 때 at.js 1.6.0이 쿠키를 저장하지 못하도록 하는 문제가 수정되었습니다. (TNT-30454)
* [!DNL Analytics for Target](A4T)을(를) 사용할 때 리디렉션을 사용하여 일부 경험만 전달되는 것으로 보이지 않는 문제를 해결했습니다. (TNT-30444)
* [!DNL Target] 호출이 성공한 후 페이지를 숨기는 문제를 해결했습니다. (TNT-30358)

다음은 at.js 버전 1.6.0에 포함된 개선 사항 및 수정 사항입니다.

* 이제 리디렉션 오퍼가 [!UICONTROL Analytics for Target](A4T) 통합에서 자동으로 지원됩니다. 클라이언트 측 임시 해결책이 제거되었습니다. (TNT-30247)
* 이제 클라이언트 측 엣지 라우팅이 기본적으로 사용됩니다. (TNT-30261)
* 동작 간에 종속성이 있을 때 Visual Experience Composer(VEC) 동작 렌더링에 문제가 수정되었습니다. (TNT-30248)

## at.js 버전 1.5.0

이제 at.js 버전 1.5.0을 사용할 수 있습니다.

* `at-request-succeeded` 이벤트 세부 사항에 리디렉션 플래그가 들어 있습니다. 이 플래그는 페이지가 다른 URL로 리디렉션되는지 여부를 확인하는 데 사용할 수 있습니다. URL을 알아보려면 `at-content-rendering-redirect`에 가입합니다. (TNT-29834)
* false로 설정한 경우 런타임 예외로 인해 `window.targetGlobalSettings.enabled`에 오류가 발생하는 문제가 해결되었습니다. (TNT-29829)
* 글로벌 mbox 요청 실행에 사용자 지정 코드를 사용하고 본문 숨기기를 사용하는 경우 VEC(시각적 경험 작성기)에서 로드하는 동안 페이지에 오류가 발생하는 문제가 해결되었습니다. (TNT-29795)
* `screenOrientation`, `devicePixelRatio` 및 `webGLRenderer`에 대한 지원을 추가했습니다. 이러한 새로운 [!DNL Target] 요청 매개 변수는 iPhone X 및 기타 최신 장치 검색에 사용됩니다. 자세한 내용은 [모바일](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html)을 참조하십시오. (TNT-29781)
* AAM (Adobe Audience Manager) 위치 힌트가 가끔씩 전송되지 않은 문제가 해결되었습니다. (TNT-29695)
* 이를 지원하는 브라우에서 at.js 1.5.0이 선택기 폴링을 위해 MutationObserver로 전환됩니다. at.js 1.0.0 이전의 버전은 MutationObserver polyfill을 사용했으며, 이는 문제가 있는 것으로 입증되었습니다. polyfill 문제를 방지하기 위해 버전 1.5.0에서 다음 의사 코드를 사용하여 사용할 예약 메커니즘을 결정합니다.

  ```
  if MutationObserver is supported
    scheduler = MutationObserver
  else if document is visible
    scheduler = requestAnimationFrame
  else
    scheduler = setTimeout
  ```

## at.js 버전 1.3.0

현재 at.js 버전 1.3.0을 사용할 수 있습니다.

* at.js와의 상호 작용을 추적, 디버깅 및 사용자 지정하는 데 도움이 되도록 다음과 같은 새 이벤트를 사용할 수 있습니다.

   * LIBRARY_LOADED
   * REQUEST_START
   * CONTENT_RENDERING_START
   * CONTENT_RENDERING_NO_OFFERS
   * CONTENT_RENDERING_REDIRECT

  자세한 내용은 [at.js 사용자 지정 이벤트](/help/dev/implement/client-side/atjs/atjs-functions/atjs-custom-events.md)를 참조하십시오.

* 데이터 공급자에서 가져온 추가 매개 변수로 at.js 요청을 확장할 수 있습니다. 데이터 공급자는 `dataProviders key` 아래의 `window.targetGlobalSettings`에 추가되어야 합니다.

  자세한 내용은 [데이터 공급자](atjs-functions/targetglobalsettings.md#data-providers)를 참조하십시오.

* 이제 at.js 요청은 GET을 사용하지만 URL 크기가 2048자를 초과하면 POST로 전환됩니다. 필요한 경우 크기 제한을 늘릴 수 있는 `urlSizeLimit`라는 새 특성이 있습니다. 이 변경 사항으로 [!DNL Target]에서 동일한 기술을 사용하는 AppMeasurement에 at.js를 정렬할 수 있습니다.
* 이제 [!DNL Target]에서 `adobe.target.applyOffer(options)` 함수의 `mbox` 키를 사용하도록 강제 적용합니다. 이 키는 과거에는 필요했지만, 이제 [!DNL Target]은(는) [!DNL Target]이(가) 적절한 유효성 검사를 수행하고 고객이 함수를 올바르게 사용하고 있는지 확인하기 위해 이 키를 강제로 사용합니다.
* at.js의 이벤트 및 클릭 추적 기능이 개선되었습니다. at.js는 `navigator.sendBeacon()`을 사용하여 이벤트 추적 데이터를 전송하고, `navigator.sendBeacon()`이 지원되지 않을 때 동기 XHR로 대체됩니다. 이 대체 항목은 주로 Internet Explorer 10 및 11과 일부 Safari 버전에 영향을 줍니다. Safari는 향후 iOS 11.3 릴리스에서 `navigator.sendBeacon()`을 추가로 지원할 예정입니다.
* 이제 페이지가 백그라운드 탭에서 열릴 때도 at.js가 오퍼를 렌더링할 수 있습니다. 백그라운드 탭의 브라우저 조절 동작으로 인해 `requestAnimationFrame()`이(가) 비활성화될 때 일부 [!DNL Target] 고객에서 문제가 발생합니다.
* 이번 릴리스에서는 Chrome CPU 프로필 검사 시 호출 스택 단축을 비롯하여 여러 가지 성능이 개선되었습니다.
* at.js 1.3.0은 더 이상 Microsoft Internet Explorer 9에서 콘텐츠 전달을 지원하지 않습니다. 지원되는 브라우저 목록에 대해서는 [지원되는 브라우저](/help/dev/before-implement/supported-browsers.md)를 참조하십시오. 앞으로, 모든 요청은 JSONP 요청 없이 CORS가 지원되는 `XMLHttpRequest`를 통해 실행됩니다. 이 변경 사항은 보안을 크게 향상시킵니다.

## at.js 버전 1.2.3

이제 at.js 버전 1.2.3을 사용할 수 있습니다.

* JSON 오퍼에 대한 지원을 추가합니다. JSON은 양식 기반 경험 작성기를 사용하여 만든 활동에서만 지원됩니다. 현재 JSON을 사용하는 유일한 방법은 직접 API 호출을 통해서입니다. [JSON 오퍼 만들기](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html)를 참조하십시오.

## at.js 버전 1.2.2

이제 at.js 버전 1.2.2를 사용할 수 있습니다.

* [!DNL Target] 라이브러리가 QUIRKS 모드를 사용하여 페이지에 로드될 때 JavaScript 오류를 반환하는 문제를 해결했습니다. (TNT-28312)
* [!DNL Target] 클릭 추적이 [!DNL Analytics]개의 데이터 수집 호출을 중단하는 문제를 해결했습니다. (TNT-28261)
* `targetPageParams()`가 빈 문자열을 반환하는 경우 `getOffer() params`가 실패하도록 하는 문제가 수정되었습니다. (TNT-28359)
* x-only를 사용할 때 발생하는 세션 ID 생성 관련 문제가 수정되었습니다. (TNT-28361)

## at.js 버전 1.2.1

이제 at.js 버전 1.2.1을 사용할 수 있습니다.

* target=&quot;_blank&quot;인 링크에 대한 클릭 추적을 수행할 경우 [!DNL Target]이(가) 새 탭에서 링크를 열 수 없는 문제를 해결했습니다.

## at.js 버전 1.2.0

이제 at.js 버전 1.2는 대부분의 버그 수정 사항을 포함하는 유지 관리 릴리스로 사용할 수 있습니다.

* 클릭 추적 특수 사례에 대해 기본 동작이 수행되지 않도록 하는 문제가 수정되었습니다. (TNT-28089)
* `target="_blank"`이(가) 있는 링크에 대한 클릭 추적을 수행할 경우 [!DNL Target]이(가) 새 탭에서 링크를 열 수 없는 문제를 해결했습니다. (TNT-28072)
* IP 주소를 쿠키 도메인으로 사용할 수 있습니다. (TNT-28002)
* 글로벌 mbox 또는 기타 지역 mbox가 있는 리디렉션 오퍼에서 깜박임을 유발하던 문제가 수정되었습니다. (TNT-27978)
* 찾아보기와 작성 간을 전환할 때 VEC 내에서 [!UICONTROL Experience Targeting] 활동 설정이 실패하는 문제를 해결했습니다. (TNT-27942)
* 클릭 추적 요소에 대한 깜박임 스타일 클래스의 잘못된 처리가 수정되었습니다. (TNT-27896)
* 전역 mbox 매개 변수가 모든 mbox 매개 변수와 혼합되도록 하는 문제가 수정되었습니다. (TNT-27846)
* Handlebars, Mustache 및 기타 클라이언트 측 템플릿 라이브러리가 at.js에서 제대로 처리되도록 하는 데 필요한 변경이 수행되었습니다. (TNT-27831)
* `sdidParamExpiry`가 제대로 초기화되어 방문자 API로 전달되도록 하는 데 필요한 변경이 수행되었습니다. `at.js 1.1.0`에 추가된 회귀입니다. 이전 at.js 버전은 영향을 받지 않습니다. 리디렉션 오퍼 및 A4T를 사용하는 클라이언트에만 영향을 줍니다. (TNT-27791)
* 사용 중인 형식 속성과 관계없이 `SCRIPT`가 실행되도록 하는 데 필요한 변경이 수행되었습니다. (TNT-27865)

## at.js 버전 1.1.0.

**날짜:** 2017년 8월 2일

다음 개선 사항 및 수정 사항이 at.js 버전 1.1에 포함되어 있습니다.

* 응답 토큰 처리가 추가되었습니다. 자세한 내용은 [응답 토큰](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)을 참조하십시오.
* `document.currentScript polyfill`이 Angular 1.X를 방해하지 않도록 문제가 해결되었습니다.
* 클릭 추적이 가시성 속성을 방해하지 않도록 하는 데 필요한 변경이 수행되었습니다. 클릭 추적 요소가 `at-element-click-tracking` 대신 `at-element-marker` CSS 클래스로 표시됩니다.

## at.js 버전 1.0.0

**날짜:** 2017년 7월 7일

다음 개선 사항 및 수정 사항이 at.js 버전 1.0에 포함되어 있습니다.

* 더 빠른 페이지 로드를 위해 at.js의 비동기식 로드가 지원됩니다.
* at.js를 비동기식으로 로드할 때 사전 숨김 페이지 콘텐츠가 지원됩니다.
* 콘텐츠 전달을 사용하지 않도록 설정할 때 오류 메시지가 개선됩니다.
* 여러 활동을 전달할 때 성능이 향상됩니다.
* YUI Compressor가 지원됩니다.
* 활동 전달 중 사용자 지정 이벤트에 대한 버그/오류가 보고됩니다.
* Microsoft Internet Explorer 11의 성능 문제가 해결되었습니다.
* 일부 웹 사이트에 오류를 발생하는 `getOffer()` 함수가 수정되었습니다.
* [!DNL Target] 라이브러리를 비동기적으로 로드합니다. 자세한 내용은 [at.js FAQ](/help/dev/implement/client-side/atjs/target-atjs-faq.md)를 참조하십시오.

## at.js 버전 0.9.7

**날짜:** 2017년 5월 22일

다음 개선 사항 및 수정 사항이 at.js 버전 0.9.7에 포함되어 있습니다.

* VEC(시각적 경험 작성기)에서 `insertAfter` 및`insertBefore` 작업에서 누락된 자산 키와 관련된 문제가 수정되었습니다. 이러한 문제는 시각적 오퍼에서 오퍼 템플릿으로의 마이그레이션과 관련되어 있습니다.

## at.js 버전 0.9.6

**날짜:** 2017년 4월 13일

다음 개선 사항 및 수정 사항이 at.js 버전 0.9.6에 포함되어 있습니다.

* A4T에 대해 리디렉션 오퍼가 지원됩니다. at.js 버전 0.9.6을 다운로드하여 설치한 후에는 [!UICONTROL Adobe Analytics as the Reporting Source for Target](A4T)을 사용하는 활동에서 리디렉션 오퍼를 사용할 수 있습니다. at.js 버전 0.9.6 외에, 리디렉션 오퍼 및 A4T를 사용하기 위해 구현이 충족해야 하는 다른 최소 요구 사항도 있습니다. 자세한 내용 및 알고 있어야 하는 추가 중요한 정보는 [리디렉션 오퍼 - A4T FAQ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html)를 참조하십시오.
* 방문자 API가 페이지에 있고 `visitorApiTimeout` 설정이 너무 적극적이었던 at.js 0.9.6 이전에는 [!DNL Target]에서 [!DNL Target] 요청에 MCID 데이터를 전송하지 않는 상황이 발생할 수 있었습니다. 이로 인해 A4T를 사용할 때 [!DNL Analytics]에서 연결되지 않은 히트 발생과 같은 문제가 나타날 수 있습니다.

  이 동작은 `visitorApiTimeout`이(가) 1ms로 설정되어 있더라도 [!DNL Target]은(는) SDID, 추적 서버 및 고객 ID를 수집한 후 [!DNL Target] 요청에 전송하려고 하므로 at.js 0.9.6에서 변경되었습니다.

* `selectorsPollingTimeout` 설정이 추가되었습니다. 자세한 내용은 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)를 참조하십시오.
* `getOffer()`의 응답 형식이 변경되었습니다. 자세한 내용은 [adobe.target.getOffer(options)](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md)를 참조하십시오.
* 지원되지 않는 `<!DOCTYPE>` 선언에 대한 콘솔 로깅이 추가되었습니다.
* 여러 기본 오퍼가 단일 mbox에 전달된 경우 [!DNL Target Classic] 플러그인이 올바르게 적용되지 않던 문제가 수정되었습니다. (TGT-22664)
* mbox 쿠키가 이러한 도메인(예: test.no, autodrives.ca 등)에 대해 올바르게 설정되었는지 확인할 수 있도록 두 글자로 된 TLD(최상위 도메인)에 대한 쿠키 설정이 개선되었습니다.
* 쿠키를 저장할 때 사용해야 하는 최상위 도메인을 추출하는 알고리즘이 at.js 버전 0.9.6에서 변경되었습니다. 이러한 변경으로 인해 쿠키를 IP를 사용하는 주소에 저장할 수 없습니다. 대부분의 경우 IP 주소는 테스트 용도로 사용되지만, 해결 방법으로 DNS 항목을 사용하거나, 로컬 상자에서 호스트 파일을 조정할 수 있습니다.
* 속성이 정수 대신 문자열 값일 때 이동 및 재정렬 작업 처리 방식이 수정되었습니다.

## at.js 버전 0.9.4

**날짜:** 2017년 1월 19일

* 이제 mbox 이름에는 앰퍼샌드(&amp;)를 비롯한 특수 문자가 포함될 수 있습니다.

  허용 가능한 특수 문자 목록을 보려면 [at.js 구성](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)을 참조하십시오.

* at.js에서 HTTPS만 사용되는지 또는 페이지 프로토콜을 기준으로 HTTP와 HTTPS 간을 전환할 수 있는지를 나타내는 `secureOnly` 설정이 추가되었습니다. 이 설정은 기본값이 False이고 `targetGlobalSettings`를 통해 대체할 수 있는 고급 설정입니다.
* at.js 버전 0.9.3 및 이전 버전에서 레거시 브라우저 지원 옵션을 사용할 수 있습니다. 이 옵션은 at.js 버전 0.9.4에서 제거되었습니다.

## at.js 버전 0.9.3

**날짜:** 2016년 10월 10일

* at.js 설정에서 레거시 브라우저가 비활성화될 경우 Microsoft Internet Explorer 11에서 mbox가 실행되도록 합니다.
* 다이내믹 원격 오퍼가 실패하는 경우(예를 들어, URL이 올바르지 않고 404 오류를 반환하는 경우) 기본 콘텐츠가 렌더링되도록 합니다.
* DOM에서 VEC 클릭 추적 선택기를 찾을 수 없는 경우 요소가 빠르게 표시되도록 합니다.

## at.js 버전 0.9.2

**날짜:** 2016년 9월 21일

* Device Graph 옵트아웃을 활성화하거나 비활성화하는 `optoutEnabled` 설정이 추가되었습니다. 이 설정이 `true`로 설정되고 방문자가 추적을 옵트아웃한 경우 방문자의 브라우저는 mbox 호출을 수행하지 않습니다. Device Graph는 현재 베타 버전입니다. 이 설정은 기본적으로 `false`(으)로 설정되지만 Device Graph를 사용하는 경우에는 `true`(으)로 설정되어야 합니다.
* 알림 메커니즘에 대한 `CustomEvent` 지원이 추가되었습니다. 이전에는 at.js 이벤트 알림 메커니즘을 `document.addEventListener()`()와 같은 표준 DOM API를 통해 사용할 수 없었습니다. 이제는 `document.addEventListener()`를 사용하여 요청 이벤트 및 콘텐츠 렌더링 이벤트와 같은 at.js 이벤트에 가입할 수 있습니다.
* VEC(시각적 경험 작성기)에서 만든 오퍼와 관련된 문제가 수정되었습니다. 이 릴리스 이전에 [!DNL Target]은(는) 선택기를 숨기고, 모든 선택기가 선택될 때만 숨김을 해제했습니다. at.js 0.9.2 [!DNL Target]에서는 일치하는 선택기가 확인되면 바로 숨김을 해제합니다.

## at.js 버전 0.9.1

**날짜:** 2016년 7월 14일

* 서비스의 자체 시간 제한과 독립적인 방문자 ID 서비스에 대한 시간 제한을 at.js에 제공합니다.
* 일부 페이지에서는 at.js를 사용하고 다른 페이지에서는 mbox.js(사용 중단됨)를 사용하여 구현에 영향을 준 0.9.0의 문제를 수정합니다.
* [!DNL Adobe Analytics]을(를) 활동의 보고 소스로 사용하는 경우, mbox.js 버전 61 이상 또는 at.js 버전 0.9.1 이상을 사용하는 경우 활동을 만드는 동안 추적 서버를 지정할 필요가 없습니다. at.js 라이브러리는 [!DNL Target]에 추적 서버 값을 자동으로 전송합니다. 활동을 생성하는 동안에는 목표 및 설정 페이지의 추적 서버 필드를 비워둘 수 있습니다.

## at.js 버전 0.9.0

**[!DNL Target]릴리스:** 16.6.1

**날짜:** 2016년 6월 23일

* VEC 오퍼를 사용할 때 발생하는 흰색 화면 문제를 수정합니다. at.js를 사용하는 모든 사용자는 이 새 버전으로 업그레이드해야 합니다.
* 새 `registerExtension` API.

  이 새로운 API는 개발자가 at.js에서 사용되는 특정 jQuery 모듈에 액세스하여 라이브러리에 대한 확장 프로그램(즉, 플러그인)을 개발할 수 있도록 합니다. 이 변경으로 인해 몇 가지 결과가 나타납니다. 이러한 결과는 다음 기능을 사용하는 사용자에게만 적용됩니다.

   * `getSettings()` API가 제거되었지만 `registerExtension()`을 사용하여 동일한 기능을 사용할 수 있습니다.
   * `getTracking()` API가 제거되었지만 `registerExtension()`을 사용하여 동일한 기능을 사용할 수 있습니다.

   * 기존 확장(예: AngularJS 확장)은 `registerExtension()` 접근 방식을 사용하도록 업데이트해야 합니다.

* 새 at.js 알림 API.

  이 알림 시스템의 목표는 페이지에서 at.js가 수행하는 작업과 문제가 발생하는 경우를 보다 잘 이해할 수 있도록 하는 것입니다. VEC에서 나타나는 일반적인 문제는 IT 릴리스가 페이지를 변경하고, VEC 선택기가 중단되고, 테스트가 더 이상 콘텐츠를 올바르게 배달하지 못하는 것입니다. 이 알림 시스템의 목표는 이 배달 문제를 페이지에 알려서 개발자들이 이 정보에 액세스하고, [!DNL Adobe Analytics]와 같은 시스템에 전달하고, 테스트가 중단된 비즈니스 소유자에게 경고를 보낼 수 있도록 하는 것입니다.

* 새 `targetGlobalSettings()` API 메서드.

  [!DNL Target Standard/Premium] UI에서 또는 REST API를 사용하여 설정을 구성하는 대신, at.js 라이브러리에서 설정을 재정의할 수 있습니다.

## at.js 버전 0.8.0

**날짜:** 2016년 5월 5일

at.js 라이브러리의 첫 번째 공식 릴리스입니다.

at.js는 일반적인 웹 구현과 단일 페이지 애플리케이션 둘 다에 맞게 디자인된 새로운 [!DNL Target]용 구현 라이브러리입니다.

at.js는 [!DNL Adobe Target] 구현을 위한 mbox.js를 대신합니다.

여러 가지 이점 중에서 at.js는 웹 구현에 대한 페이지 로드 시간을 향상시키고, 보안을 강화하고, 단일 페이지 애플리케이션에 대해 더 나은 구현 옵션을 제공합니다.

at.js에는 target.js에 포함된 구성 요소도 포함되어 있으므로 더 이상 target.js를 호출할 필요가 없습니다.

at.js를 구현할 때는 다음에 유의하십시오.

* 버전 8 이전의 Internet Explorer 버전은 지원되지 않습니다.
* 비동기 구현은 [!UICONTROL Test&Target to SiteCatalyst] 플러그인과 같은 레거시 통합이 작동하지 않을 수 있음을 의미합니다.
* mbox.js 개체 및 메서드를 참조하는 [!DNL Target] 플러그인은 지원되지 않습니다.
* 모든 [!DNL Target] 호출은 XMLHTTPRequest를 통해 수행되고 콘텐츠는 JSON을 통해 반환됩니다.
