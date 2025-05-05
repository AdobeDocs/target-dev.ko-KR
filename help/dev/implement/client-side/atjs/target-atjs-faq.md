---
keywords: at.js faq, at.js 자주 묻는 질문, faq, 깜박임, 로더, 페이지 로더, 교차 도메인, 파일 크기, 파일크기, x-domain, at.js 및 mbox.js, x 전용, 교차 도메인, safari, 단일 페이지 앱, 누락된 선택기, 선택기, 단일 페이지 애플리케이션, tt.omtrdc.net, spa, Adobe Experience Manager, AEM, ip 주소, httponly, HttpOnly, 보안, ip, 쿠키 도메인
description: ' [!DNL Adobe Target] at.js JavaScript 라이브러리에 대해 자주 묻는 질문과 대답(FAQ)을 읽어 보십시오.'
title: at.js에 대한 일반적인 질문과 대답은 무엇입니까?
feature: at.js
exl-id: 362ccc5b-8731-46c0-bc52-3e55c273e216
source-git-commit: 448c43c0c10e22ad054f4ee98bfc282f8c96cdcb
workflow-type: tm+mt
source-wordcount: '2923'
ht-degree: 39%

---

# at.js FAQ

[!DNL Adobe Target] at.js JavaScript 라이브러리에 대해 자주 묻는 질문과 대답(FAQ)입니다.

## mbox.js와 비교하여 at.js를 사용할 때의 장점은 무엇입니까?

at.js 라이브러리는 mbox.js를 대체합니다. mbox.js 라이브러리는 더 이상 지원되지 않습니다. 그러나 대부분의 사용자에게 at.js는 mbox.js보다 나은 이점을 제공합니다.

여러 가지 이점 중에서 at.js는 웹 구현에 대한 페이지 로드 시간을 향상시키고, 보안을 강화하고, 단일 페이지 애플리케이션에 대해 더 나은 구현 옵션을 제공합니다.

다음 다이어그램은 mbox.js를 사용할 때의 페이지 로드 성능과 at.js를 사용할 때의 페이지 로드 성능을 보여줍니다.

이미지 를 클릭하여 전체 너비로 확장합니다.

![mbox.js와 at.js를 비교하는 페이지 성능 다이어그램](/help/dev/implement/client-side/atjs/assets/atjs_versus_mboxjs.png "mbox.js와 at.js를 비교하는 페이지 성능 다이어그램"){zoomable="yes"}

위에서 보듯이 mbox.js를 사용하는 페이지 컨텐츠는 [!DNL Target] 호출이 완료될 때까지 로드되지 않았습니다. 반면에 at.js를 사용하는 페이지 콘텐츠는 [!DNL Target] 호출이 시작되면 로드가 시작되며 호출이 완료될 때까지 기다리지 않습니다.

## at.js 및 mbox.js가 페이지 로드 시간에 미치는 영향은 무엇입니까?

많은 고객과 컨설턴트는 특히 새 사용자와 재방문 사용자의 컨텍스트에서 페이지 로드 시간에 대한 at.js 및 mbox.js의 영향을 알고 싶어 합니다. 안타깝게도 at.js 또는 mbox.js가 각 고객의 구현으로 인해 페이지 로드 시간에 어떻게 영향을 주는지에 대한 구체적 수치를 측정하고 제공하기는 어렵습니다.

하지만 방문자 API가 페이지에 있으면 [!DNL Target]에서 at.js와 mbox.js가 페이지 로드 시간에 어떻게 영향을 주는지를 더 잘 이해할 수 있습니다.

>[!NOTE]
>
>방문자 API와 at.js 또는 mbox.js는 글로벌 mbox를 사용하는 경우에만 페이지 로드 시간에 영향을 미칩니다(본문 숨기기 기법으로 인해). 지역 mbox는 방문자 API 통합의 영향을 받지 않습니다.

다음 섹션에서는 새 방문자와 재방문자에 대한 작업 시퀀스를 설명합니다.

### 새 방문자 수

1. 방문자 API가 로드, 구문 분석 및 실행됩니다.
1. at.js/mbox.js가 로드, 구문 분석 및 실행됩니다.
1. 글로벌 mbox 자동 만들기를 사용하도록 설정한 경우 [!DNL Target] JavaScript 라이브러리는 다음과 같습니다.

   * 방문자 개체를 인스턴스화합니다.
   * [!DNL Target] 라이브러리에서 Experience Cloud 방문자 ID 데이터를 검색하려고 합니다.
   * 이 방문자는 새로운 방문자이므로 방문자 API는 demdex.net에 대한 도메인 간 요청을 실행합니다.
   * Experience Cloud 방문자 ID 데이터를 검색한 후 [!DNL Target]에 대한 요청이 실행됩니다.

### 재방문자

1. 방문자 API가 로드, 구문 분석 및 실행됩니다.
1. at.js/mbox.js가 로드, 구문 분석 및 실행됩니다.
1. 글로벌 mbox 자동 만들기를 사용하도록 설정한 경우 [!DNL Target] JavaScript 라이브러리는 다음과 같습니다.

   * 방문자 개체를 인스턴스화합니다.
   * [!DNL Target] 라이브러리에서 Experience Cloud 방문자 ID 데이터를 검색하려고 합니다.
   * 방문자 API는 쿠키의 데이터를 검색합니다.
   * Experience Cloud 방문자 ID 데이터를 검색한 후 [!DNL Target]에 대한 요청이 실행됩니다.

>[!NOTE]
>
>새 방문자의 경우 방문자 API가 있으면 [!DNL Target]이(가) 여러 번 연결하여 [!DNL Target] 요청에 Experience Cloud 방문자 ID 데이터가 포함되어 있는지 확인해야 합니다. 재방문자의 경우 [!DNL Target]이(가) [!DNL Target]에만 연결하여 개인화된 콘텐츠를 검색합니다.

## 이전 버전의 at.js를 버전 1.0.0으로 업그레이드한 후 응답 속도가 느려진 것 같은 이유는 무엇입니까?

at.js 버전 1.0.0 이상은 모든 요청을 동시에 실행합니다. 이전 버전은 요청을 순차적으로 실행합니다. 즉, 요청이 큐에 들어가고 [!DNL Target]은(는) 다음 요청으로 이동하기 전에 첫 번째 요청이 완료될 때까지 대기합니다.

이전 버전의 at.js가 요청을 실행하는 방식은 &quot;head of line blocking&quot;(HOL 블로킹)이라는 현상이 발생하기 쉽습니다. at.js 1.0.0 이상에서는 [!DNL Target]이(가) 병렬 요청 실행으로 전환되었습니다.

예를 들어 at.js 0.9.1에 대한 네트워크 탭 폭포를 선택하면 이전 요청이 완료될 때까지 다음 [!DNL Target] 요청이 시작되지 않습니다. 이 시퀀스는 기본적으로 모든 요청이 동시에 시작되는 at.js 1.0.0 이상에서는 해당되지 않습니다.

응답-시간 관점에서 수학적으로 이 수열은 다음과 같이 합산될 수 있다

<ul class="simplelist"> 
 <li> at.js 0.9.1: 모든 [!DNL Target]개의 요청에 대한 응답 시간 = 요청 응답 시간의 합계 </li> 
 <li> at.js 1.0.0 이상: 모든 [!DNL Target]개의 요청에 대한 응답 시간 = 최대 요청 응답 시간 </li> 
</ul>

at.js 라이브러리 버전 1.0.0은 요청을 더 빨리 완료합니다. 또한 at.js 요청은 비동기적이므로 [!DNL Target]이(가) 페이지 렌더링을 차단하지 않습니다. 요청이 완료되는 데 몇 초가 걸리더라도 렌더링된 페이지가 표시되며, [!DNL Target]이(가) [!DNL Target] 가장자리에서 응답을 받을 때까지 페이지의 일부 부분만 공백으로 표시됩니다.

## [!DNL Target] 라이브러리를 비동기식으로 로드할 수 있습니까?

at.js 1.0.0 릴리스를 사용하면 [!DNL Target] 라이브러리를 비동기적으로 로드할 수 있습니다.

at.js를 비동기적으로 로드하려면 다음을 수행하십시오.

* 권장되는 방법은 Adobe Experience Platform의 태그를 사용하는 것입니다.
* at.js를 로드하는 스크립트 태그에 비동기 속성을 추가하여 at.js를 비동기로 로드할 수도 있습니다. 다음과 같은 방법 사용:

  ```
  <script src="<URL to at.js>" async></script>
  ```

* 다음 코드를 사용하여 at.js를 비동기식으로 로드할 수도 있습니다.

  ```
  var script = document.createElement('script'); 
  script.async = true; 
  script.src = "<URL to at.js>"; 
  document.head.appendChild(script);
  ```

at.js를 비동기식으로 로드하는 것은 브라우저 렌더링이 차단되지 않도록 하는 좋은 방법입니다. 그러나 이 기법은 웹 페이지에서 플리커를 유발할 수 있습니다.

페이지(또는 지정된 부분)를 숨긴 다음 at.js 및 글로벌 요청이 로드된 후에 표시하는 사전에 숨기는 코드 조각을 사용하여 플리커를 방지할 수 있습니다. at.js를 로드하기 전에 코드 조각을 추가해야 합니다.

비동기 [!UICONTROL Adobe Experience Platform] 구현을 통해 at.js를 배포하는 경우 [!UICONTROL Adobe Experience Platform] 포함 코드를 사용하여 [!DNL Target]을(를) 구현하기 전에 페이지에 사전에 숨기는 코드 조각을 직접 포함해야 합니다.

동기 DTM 구현을 통해 at.js를 배포하는 경우 페이지 상단에서 트리거된 페이지 로드 규칙을 통해 사전에 숨기는 코드 조각을 추가할 수 있습니다.

자세한 내용은 [at.js에서 플리커를 관리하는 방법](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)을 참조하십시오.

## at.js가 [!DNL Adobe Experience Manager] 통합(Experience Manager)과 호환됩니까?

FP-11577을 사용하는 [!DNL Adobe Experience Manager] 6.2(또는 이상)에서는 이제 [!UICONTROL Adobe Target Cloud Services] 통합으로 at.js 구현을 지원합니다.

## at.js를 사용하여 페이지 로드 플리커를 방지하려면 어떻게 합니까?

[!DNL Target]은(는) 페이지 로드 깜박임을 방지하는 여러 가지 방법을 제공합니다. 자세한 내용은 [at.js를 사용하여 플리커 방지](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)를 참조하십시오.

## at.js의 파일 크기는 얼마입니까?

at.js 파일은 다운로드 시 약 109KB입니다. 그러나 대부분의 서버는 파일 크기를 줄이기 위해 파일을 자동으로 압축하므로, at.js는 서버에서 압축되고(GZIP 또는 다른 방법 사용) 사용자가 웹 사이트를 방문하여 로드될 때 약 34KB입니다. at.js를 설치한 서버의 압축 설정이 실제 압축 크기를 결정합니다.

## at.js가 mbox.js보다 큰 이유는 무엇입니까?

at.js 구현은 단일 라이브러리(at.js)를 사용하는 반면, mbox.js 구현은 실제로 두 개의 라이브러리(mbox.js 및 target.js)를 사용합니다. 따라서 공정한 비교는 at.js 대 mbox.js *와* `target.js`입니다. gzip으로 압축된 두 버전의 크기를 비교하면 at.js 버전 1.2는 34KB이고 mbox.js 버전 63은 26.2KB입니다. &grave;&grave;

at.js는 mbox.js와 비교하여 훨씬 더 많은 DOM 구문 분석을 수행하므로 더 adfd큽니다. 이것은 at.js가 JSON 응답에 있는 &quot;원시&quot; 데이터를 가져오고 이를 이해해야 하기 때문에 필요합니다. mbox.js가 `document.write()`을(를) 사용했으며 브라우저에서 모든 구문 분석을 수행했습니다.

파일이 큼에도 불구하고 테스트를 해보면 mbox.js에 비해 at.js를 사용할 때 페이지가 더 빨리 로드됩니다. 또한 at.js는 추가적인 파일을 동적으로 로드하거나 `document.write`을(를) 사용하지 않으므로 보안 관점에서 더 우수합니다.

## at.js 안에 jQuery가 있습니까? 이미 웹 사이트에 jQuery가 있으므로 at.js에서 이 부분을 제거할 수 있습니까?

at.js는 현재 jQuery의 일부를 사용하므로 at.js의 맨 위에 MIT 라이센스 알림이 표시됩니다. jQuery가 노출되지 않았으며 이미 페이지에 있는 jQuery 라이브러리도 방해하지 않으므로 다른 버전일 수 있습니다. at.js 내의 jQuery 코드 제거는 지원되지 않습니다.

## at.js는 x 전용으로 설정된 교차 도메인과 Safari를 지원합니까?

아니요. 교차 도메인이 x 전용으로 설정되어 있고 Safari에 타사 쿠키가 비활성화되어 있다면, mbox.js와 at.js는 모두 비활성화된 쿠키를 설정하며 mbox 요청은 해당 특정 클라이언트의 도메인에 대해 실행되지 않습니다.

Safari 방문자를 지원하기 위해 더 나은 X-Domain이 &quot;비활성화&quot;(퍼스트 파티 쿠키만 설정)되거나 &quot;활성화&quot;(Safari에서 퍼스트 파티 쿠키만 설정하고 기타 브라우저에서는 퍼스트 파티 쿠키와 타사 쿠키 설정)됩니다.

## 단일 페이지 애플리케이션에서 Target [!UICONTROL Visual Experience Composer] (VEC)을 사용할 수 있습니까?

예. at.js 2.x를 사용하는 경우 SPA용 VEC를 사용할 수 있습니다. 자세한 내용은 [단일 페이지(SPA) 시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/spa-visual-experience-composer.html?lang=ko)를 참조하십시오.

## at.js 구현에 Adobe Experience Cloud Debugger를 사용할 수 있습니까?

예. 디버깅 목적으로 mboxTrace를 사용하거나 브라우저의 개발자 도구를 사용하여 네트워크 요청을 검사하고, &quot;mbox&quot;로 필터링하여 mbox 통화를 가려낼 수도 있습니다.

## at.js를 사용하는 mbox 이름에 특수 문자를 사용할 수 있습니까?

예, mbox.js에서와 같습니다.

## 웹 페이지에서 mbox가 실행되지 않는 이유는 무엇입니까?

[!DNL Target] 고객은 테스트나 간단한 개념 입증 용도로 [!DNL Target]에 클라우드 기반 인스턴스를 사용하는 경우가 있습니다. 이러한 도메인 및 기타 많은 다른 도메인이 [공용 접미사 목록](https://publicsuffix.org/list/public_suffix_list.dat)에 나와 있습니다.

최신 브라우저에서는 targetGlobalSettings()를 사용하여 `cookieDomain` 설정을 사용자 지정하지 않는 한, 이러한 도메인을 사용하는 경우 쿠키를 저장하지 않습니다. 자세한 내용은 [클라우드 기반 인스턴스를 함께 사용 [!DNL Target]](/help/dev/implement/client-side/target-debugging-atjs/targeting-using-cloud-based-instances.md)을 참조하십시오.

## at.js를 사용할 때 IP 주소를 쿠키 도메인으로 사용할 수 있습니까?

예. [at.js 버전 1.2 이상](/help/dev/implement/client-side/atjs/target-atjs-versions.md)을 사용 중이라면 사용할 수 있습니다. 그러나 Adobe은 최신 버전을 사용하여 최신 상태로 유지하는 것이 좋습니다.

>[!NOTE]
>
>at.js 버전 1.2 이상을 사용하는 경우에는 다음 예가 필요하지 않습니다.

[targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)를 사용하는 방법에 따라 at.js를 다운로드한 후 코드를 추가로 수정해야 할 수 있습니다. 예를 들어, 다양한 웹 사이트에서 [!DNL Target] 구현들에 대해 약간씩 다르게 설정해야 하지만 이러한 설정을 사용자 지정 JavaScript를 사용하여 동적으로 정의할 수 없다면, 파일을 다운로드한 후 각 웹 사이트에 업로드하기 전에 이러한 사용자 지정을 수동으로 수행하십시오.

다음 예에서는 `targetGlobalSettings()` at.js 함수를 사용하여 IP 주소를 지원하는 코드 조각을 삽입할 수 있습니다.

이 예는 단일 IP 주소용입니다.

```
if (window.location.hostname === '123.456.78.9') { 
    window.targetGlobalSettings = window.targetGlobalSettings || {}; 
    window.targetGlobalSettings.cookieDomain = window.location.hostname; 
}
```

이 예는 IP 주소 범위용입니다.

```
if (/^123\.456\.78\..*/g.test(window.location.hostname)) { 
    window.targetGlobalSettings = window.targetGlobalSettings || {}; 
    window.targetGlobalSettings.cookieDomain = window.location.hostname; 
}
```

## &quot;누락된 선택기 관련 작업&quot;과 같은 경고 메시지가 표시되는 이유는 무엇입니까?

이러한 메시지는 at.js 기능과 관련이 없습니다. at.js 라이브러리는 DOM에서 찾을 수 없는 모든 것을 보고합니다.

이 경고 메시지가 표시되는 경우 가능한 근본 원인은 다음과 같습니다.

* 페이지가 동적으로 작성 중이므로 at.js에서 요소를 찾을 수 없습니다.
* 느린 네트워크로 인해 페이지가 느리게 작성되고 있으며 at.js가 DOM에서 선택기를 찾을 수 없습니다.
* 활동이 실행 중인 페이지 구조가 변경되었습니다. 시각적 경험 작성기(VEC)에서 활동을 다시 열 경우 경고 메시지가 표시됩니다. 필요한 모든 요소를 찾을 수 있도록 활동을 업데이트합니다.
* 기본 페이지가 단일 페이지 애플리케이션(SPA)의 일부이거나 이 페이지에 페이지 아래쪽에 나타나는 요소가 있는데, at.js &quot;선택기 폴링 메커니즘&quot;이 해당 요소를 찾을 수 없습니다. `selectorsPollingTimeout`을 늘리는 것이 도움이 될 수 있습니다. 자세한 내용은 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)를 참조하십시오.
* 지표가 설정된 URL과 관계없이 모든 클릭 추적 지표가 모든 페이지에 추가되려고 시도합니다. 이러한 상황에서는 문제가 없지만 이러한 메시지가 많이 표시됩니다.

  최상의 결과를 얻으려면 [최신 버전의 at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md)를 다운로드하여 사용하십시오. at.js 다운로드 방법에 대한 자세한 내용은 [*at.js를 배포하는 방법* > *태그 관리자 없이 [!DNL Target] 구현*](how-to-deployatjs/implement-target-without-a-tag-manager.md) 문서의 [인터페이스를 사용하여  [!DNL Target] at.js 다운로드](how-to-deployatjs/implement-target-without-a-tag-manager.md#download-atjs-using-the-target-interface) 섹션을 참조하십시오.

## [!DNL Target] 서버 호출이 이동하는 도메인 tt.omtrdc.net은 무엇입니까?

tt.omtrdc.net 은 Adobe의 EDGE 네트워크에 대한 도메인 이름으로, [!DNL Target]에 대한 모든 서버 호출을 받는 데 사용됩니다.

## at.js가 항상 HttpOnly 및 Secure 쿠키 플래그를 사용하지 않는 이유는 무엇입니까?

HttpOnly는 서버 측 코드를 통해서만 설정할 수 있습니다. mbox와 같은 [!DNL Target] 쿠키는 JavaScript 코드를 통해 생성 및 저장되므로 [!DNL Target]에서 HttpOnly 쿠키 플래그를 사용할 수 없습니다. [!DNL Target]은(는) 도메인 간 사용이 활성화된 경우 서버측에서 설정된 서드파티 쿠키에 대해 set HttpOnly를 사용합니다.

HTTPS를 통해 페이지를 로드한 경우에만 JavaScript를 통해 보안을 설정할 수 있습니다. 페이지가 처음에 HTTP를 통해 로드된 경우에는 JavaScript에서 이 플래그를 설정할 수 없습니다. 또한 보안 플래그를 사용하면 쿠키는 HTTPS 페이지에서만 사용할 수 있습니다. HTTPS를 통해 로드된 페이지의 경우 [!DNL Target]은(는) Secure 및 SameSite=None 특성을 설정합니다.

[!DNL Target]이(가) 사용자를 제대로 추적할 수 있도록 하기 위해, 그리고 쿠키가 클라이언트측에서 생성되기 때문에 [!DNL Target]은(는) 위에서 언급한 상황을 제외하고 이러한 플래그 중 하나를 사용하지 않습니다.

## at.js는 XSS 및 MITM 공격과 같은 보안 문제를 어떻게 처리합니까?

targetGlobalSettings() 함수([targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md))에서 `secureOnly` 옵션이 true로 설정되어 있는 한, at.js에서 활성화한 Adobe Edge 네트워크와의 통신은 HTTPS를 통해서만 가능합니다. 그렇지 않으면 at.js가 페이지 프로토콜을 기준으로 HTTP와 HTTPS 간을 전환할 수 있습니다.

기본적으로 다음 헤더가 적용됩니다.
* HTTP Strict Transport Security (HSTS)
* X-XSS 보호
* X 컨텐츠 유형 옵션
* 레퍼러 정책

클라이언트 페이지에서 이미 사용된 모든 헤더를 적용할 수 있습니다. 이를 수행하는 일반적인 방법 중 하나는 &quot;HTTP 요청 헤더 인증&quot;을 통한 것입니다. Adobe 고객 지원 센터에서 모범 방법 및 사례에 대해 추가로 조언할 수 있습니다.

또한 Adobe Edge 네트워크에 대한 요청은 (방문자의 브라우저에서 수행되도록 설계된) 공개적이며, 가시적인 방문자 세부 정보를 포함하지 않습니다 (방문자 ID만 포함). 이러한 요청은 방문자에게 경험을 전달하며, 방문자가 페이지에서 봐야 하는 사항에 대한 세부 정보를 포함합니다.

이러한 요청에서 전송되는 응답 토큰 및 세션 ID의 경우:

* 커뮤니케이션 세션을 추적합니다
* 무작위 문자로 구성되어 있습니다
* 세션 ID는 30분 동안 유효합니다.
* 응답 토큰을 비활성화할 수 있습니다([응답 토큰](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=ko)).
* 이 변수는 Adobe 솔루션 환경에서만 유용합니다.

값이 &quot;*&quot;인 `Access-Control-Allow-Origin` 헤더가 at.js 요청에 표시될 것으로 예상됩니다. 공용 항목이므로 인증이 필요하지 않으며 JavaScript 호출을 통해 모든 도메인에서 Adobe Edge 네트워크에 액세스해야 합니다.

하지만 페이지에 CSP(콘텐츠 보안 정책)를 적용해야 합니다. at.js에 대한 CSP 요구 사항에 대한 자세한 내용은 [콘텐츠 보안 정책](/help/dev/before-implement/privacy/content-security-policy.md) 및 [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)를 참조하십시오.

## at.js가 네트워크 요청을 얼마나 자주 실행합니까?

[!DNL Target]은(는) 서버측에서 모든 의사 결정을 실행합니다. 즉, at.js는 페이지가 다시 로드되거나 at.js 공용 API가 호출될 때마다 네트워크 요청을 실행합니다.

## 최상의 사례 시나리오에서 사용자가 컨텐츠를 숨기고, 대체하고, 표시하는 것과 관련된 페이지 로드에 가시적인 영향을 미치지 않을 것으로 기대할 수 있습니까?

at.js는 연장된 기간 동안 HTML BODY 또는 기타 DOM 요소를 사전에 숨기지 않으려고 시도하지만 이는 네트워크 조건 및 활동 설정에 따라 다릅니다. at.js에서는 본문 숨기기 CSS 스타일을 사용자 지정하는 데 사용할 수 있는 [설정](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)을 제공하므로 전체 HTML BODY를 공백으로 남기지 않고 페이지의 일부만 미리 숨길 수 있습니다. 이러한 부분에는 &quot;개인화&quot;해야 하는 DOM 요소가 포함될 것으로 예상됩니다.

## 사용자가 활동 자격이 있는 평균 시나리오의 이벤트 순서는 무엇입니까?

at.js 요청은 비동기 `XMLHttpRequest`이므로 다음 단계를 실행합니다.

1. 페이지가 로드됩니다.
1. at.js는 HTML BODY를 미리 숨깁니다. HTML BODY 대신 특정 컨테이너를 미리 숨길 수 있는 설정이 있습니다.
1. at.js 요청이 실행됩니다.
1. [!DNL Target] 응답을 받은 후 [!DNL Target]에서 CSS 선택기를 추출합니다.
1. [!DNL Target]은(는) CSS 선택기를 사용하여 사용자 지정할 DOM 요소를 미리 숨기는 STYLE 태그를 만듭니다.
1. HTML BODY 미리 숨김 STYLE이 제거되었습니다.
1. [!DNL Target]에서 DOM 요소에 대한 폴링을 시작합니다.
1. DOM 요소가 발견되면 [!DNL Target]에서 DOM 변경 내용을 적용하고 요소 사전 숨김 STYLE을 제거합니다.
1. DOM 요소를 찾을 수 없는 경우 전역 시간 초과로 인해 페이지가 손상되지 않도록 요소가 숨김 해제됩니다.

## at.js가 활동이 변경하는 요소를 최종적으로 숨기지 않을 때 페이지의 콘텐츠는 얼마나 자주 로드 및 표시됩니까?

위의 시나리오를 고려할 때, at.js가 활동이 변경하는 요소를 최종적으로 숨기지 않으면 페이지의 컨텐츠는 얼마나 자주 로드 및 표시됩니까? 다시 말해, 페이지는 활동 콘텐츠를 제외하고 완전히 표시되며, 나머지 콘텐츠는 잠시 후에 표시됩니다.

at.js는 페이지의 렌더링을 차단하지 않습니다. [!DNL Target]에서 사용자 지정한 요소를 나타내는 빈 영역이 페이지에 표시될 수 있습니다. 적용할 콘텐츠에 SCRIPT 또는 IMG와 같은 원격 자산이 포함되지 않은 경우 모든 것을 빠르게 렌더링해야 합니다.

## 완전히 캐시된 페이지는 위의 시나리오에 어떻게 영향을 줍니까? 페이지의 나머지 콘텐츠를 로드한 후에 활동 콘텐츠가 눈에 더욱 잘 띄게 표시될 수 있습니까?

페이지가 사용자 위치와 가깝지만 [!DNL Target] 에지 근처가 아닌 CDN에 캐시된 경우 해당 사용자에게 약간의 지연이 표시될 수 있습니다. [!DNL Target] 가장자리는 전 세계에 잘 분포되어 있으므로 대부분의 경우 문제가 되지 않습니다.

## 대표 이미지가 표시되고 잠시 지연된 뒤 교체될 수 있습니까?

다음 시나리오를 고려하십시오.

[!DNL Target] 시간 제한은 5초입니다. 사용자가 대표 이미지를 사용자 지정할 수 있는 활동이 포함된 페이지를 로드합니다. at.js는 적용할 활동이 있는지 확인하기 위한 요청을 보내지만 초기 응답이 없습니다. 연결된 활동이 있는지 여부에 대해 [!DNL Target]에서 수신된 응답이 없기 때문에 사용자는 대표 이미지의 일반 콘텐츠를 볼 수 있다고 가정합니다. 4초 후 [!DNL Target]은(는) 활동 내용이 포함된 응답을 반환합니다.

이 단계에서 대체 버전을 표시할 수 있습니까? 따라서 4초 후에 대표 이미지를 교체할 수 있으며 사용자가 이 이미지 교체를 알 수 있습니까?

처음에는 이미지 대표 DOM 요소가 숨겨져 있습니다. [!DNL Target]의 응답을 받은 후 at.js는 DOM 변경 사항을 적용합니다(예: IMG를 대체하고 사용자 지정된 대표 이미지 표시).

## at.js에 필요한 HTML doctype은 무엇입니까?

at. s에는 HTML5 doctype이 필요합니다.

이 구문은 다음과 같습니다.

`<!DOCTYPE html>`

HTML5 doctype은 페이지가 표준 모드로 로드되도록 합니다. quirks 모드로 로드할 때 at.js가 사용하는 일부 JS API가 비활성화됩니다. [!DNL Target]이(가) quirks 모드에서 at.js를 사용하지 않도록 설정합니다.

## at.js는 Ionic 앱 환경에서 작동합니까?

at.js는 웹이 아닌 환경에서 작동하도록 의도되지 않았으므로 이 구현은 테스트되지 않았습니다. [!DNL Adobe]은(는) 모바일 구현용 [SDK를 권장합니다](/help/dev/implement/mobile/overview.md).
