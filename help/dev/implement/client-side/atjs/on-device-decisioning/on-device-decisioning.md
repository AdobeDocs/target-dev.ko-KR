---
keywords: 구현, javascript 라이브러리, js, atjs, 온디바이스 의사 결정, 온디바이스 의사 결정, at.js, 온디바이스, 온디바이스, 구현0
description: 수행 방법 알아보기 [!UICONTROL 온디바이스 의사 결정] at.js 라이브러리 사용
title: 온디바이스 의사 결정은 at.js JavaScript 라이브러리에서 어떻게 작동합니까?
feature: at.js
exl-id: bd0e062f-c259-46f3-adba-e380af058ac8
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '3689'
ht-degree: 9%

---

# [!UICONTROL 온디바이스 의사 결정] at.js용

버전 2.5.0부터 at.js는 [!UICONTROL 온디바이스 의사 결정]. [!UICONTROL 온디바이스 의사 결정] 을(를) 캐시할 수 있습니다 [A/B 테스트](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) 및 [경험 타기팅](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) 브라우저에 대한 네트워크 요청을 차단하지 않고 메모리 내 의사 결정을 수행하는 작업 [!DNL Adobe Target] 에지 네트워크.

>[!NOTE]
>
>[!UICONTROL 온디바이스 의사 결정] 는 클라이언트측과 서버측 구현 모두에서 사용할 수 있습니다. 이 문서에서는 [!UICONTROL 온디바이스 의사 결정] 클라이언트 측. 에 관한 정보를 위하여 [!UICONTROL 온디바이스 의사 결정] 서버측은 서버측 구현 설명서를 참조하십시오 [여기](../../../server-side/sdk-guides/on-device-decisioning/overview.md).

[!DNL Target] 또한 라이브 서버 호출을 통해 실험 및 ML 기반(Machine Learning-driven) 개인화 활동에서 가장 관련성이 높고 최신 경험을 제공할 수 있는 유연성을 제공합니다. 즉, 성과가 가장 중요할 때 다음을 사용하도록 선택할 수 있습니다. [!UICONTROL 온디바이스 의사 결정]. 그러나 가장 관련성이 높고 최신 ML 기반 경험이 필요한 경우 대신 서버 호출을 수행할 수 있습니다.

## 의 이점은 무엇입니까 [!UICONTROL 온디바이스 의사 결정]?

의 이점 [!UICONTROL 온디바이스 의사 결정] 포함:

* **매우 빠른 의사 결정 및 경험을 제공합니다.** 버킷팅 및 의사 결정은 네트워크 요청이 차단되지 않도록 인메모리 및 브라우저에서 수행됩니다.
* **애플리케이션 성능 향상** 최종 사용자 경험을 그대로 유지하면서 실험을 실행하고 고객 및 사용자에게 개인화를 제공할 수 있습니다.
* **Google 사이트 품질 점수를 개선합니다.** 메모리에서 발생하는 의사 결정을 통해 온라인 비즈니스의 Google 사이트 품질 점수를 개선하여 소비자가 더 많이 검색할 수 있도록 합니다.
* **실시간 분석에서 알아봅니다.** 을 통해 활동 성과를 실시간으로 통찰력 확보 [Target 분석](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) (A4T) 보고. A4T를 사용하면 중요한 순간에 전략을 피벗할 수 있습니다.

## 지원되는 기능

다음 [!DNL Adobe Target] JS SDK는 고객이 의사 결정을 위해 데이터의 성능과 신선도 중에서 선택할 수 있는 유연성을 제공합니다. 즉, 머신 러닝을 통해 가장 관련성이 높고 매력적인 개인화된 콘텐츠를 전달하는 것이 가장 중요한 경우 라이브 서버 호출을 수행해야 합니다. 그러나 성능이 더 중요한 경우에는 온디바이스 및 인메모리 결정을 내려야 합니다. 대상 [!UICONTROL 온디바이스 의사 결정] 작동하려면 지원되는 기능 목록을 참조하십시오.

* 활동 유형
* 대상 타기팅
* 할당 방법

자세한 내용은 [에 대해 지원되는 기능 [!UICONTROL 온디바이스 의사 결정]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md).

## 은 어떻게 합니까? [!UICONTROL 온디바이스 의사 결정] 일?

를 사용하여 at.js를 배포하고 초기화할 때 [!UICONTROL 온디바이스 의사 결정] 활성화됨, a [규칙 아티팩트](/help/dev/implement/client-side/atjs/on-device-decisioning/rule-artifact.md) 다음을 포함: [!UICONTROL 온디바이스 의사 결정] A/B 및 XT 활동, 대상 및 에셋의 경우 방문자와 가장 가까운 Akamai CDN에서 다운로드되어 방문자의 브라우저에 로컬로 캐시됩니다. at.js에서 경험을 검색하도록 요청하는 경우 캐시된 규칙 아티팩트에 인코딩된 메타데이터를 기반으로 반환할 경험에 대한 결정이 인메모리에 수행됩니다.

## 의사 결정 방법

포함 [!UICONTROL 온디바이스 의사 결정], [!DNL Target] decisioning 메서드라는 새로운 설정을 소개합니다. 의사 결정 방법 설정은 at.js가 경험을 전달하는 방법을 지시합니다. Decisioning 메서드에는 세 가지 값이 있습니다.

* 서버측 전용
* 온디바이스 전용
* 하이브리드

### 서버측 전용

Server-side만 at.js 2.5.0+가 구현되고 웹 속성에 배포되는 경우 기본적으로 설정되는 기본 의사 결정 방법입니다.

서버측을 기본 구성으로만 사용한다는 것은 모든 결정이 [!DNL Target] 에지 네트워크: 차단 서버 호출을 포함합니다. 이 방법을 사용하면 지연 시간이 늘어날 수 있지만 적용 기능을 제공하는 등 상당한 이점이 있습니다 [!DNL Target]다음을 포함하는 의 머신 러닝 기능 [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html), [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) (AP) 및 [자동 Target](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) 활동.

또한 을 사용하여 개인화된 경험을 향상시킵니다. [!DNL Target]세션 및 채널에서 지속되는 의 사용자 프로필은 비즈니스에 강력한 결과를 제공할 수 있습니다.

마지막으로, 서버측에서는 Adobe Experience Cloud만 사용할 수 있고 Audience Manager 및 Adobe Analytics 세그먼트를 통해 타깃팅할 수 있는 대상을 미세 조정할 수 있습니다.

다음 다이어그램은 방문자, 브라우저, at.js 2.5.0+ 및 [!DNL Adobe Target] 에지 네트워크. 이 흐름 다이어그램은 새 방문자와 재방문자를 캡처합니다.

이미지 를 클릭하여 전체 너비로 확장합니다.

![서버측 전용 흐름 다이어그램](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/server-side-only.png "서버측 전용 흐름 다이어그램"){zoomable=&quot;yes&quot;}

다음 목록은 다이어그램의 숫자와 일치합니다.

| 단계 | 설명 |
| --- | --- |
| 1 | Experience Cloud 방문자 ID는 [Adobe Experience Cloud ID 서비스](https://experienceleague.adobe.com/docs/id-service/using/home.html?). |
| 2 | at.js 라이브러리는 동기식으로 로드되며 문서 본문을 숨깁니다.<br />   at.js 라이브러리는 페이지에 구현된 코드 조각 사전 숨김(선택 사항)을 사용하여 비동기식으로 로드할 수도 있습니다. |
| 3 | at.js 라이브러리는 깜박임을 방지하기 위해 본문을 숨깁니다. |
| 4 | (ECID, 고객 ID, 사용자 지정 매개 변수, 사용자 프로필 등과 같은) 구성된 모든 매개 변수를 포함하는 페이지 로드 요청이 이루어집니다. |
| 5 | 프로필 스크립트가 실행된 다음 프로필 저장소에 반영됩니다.<br />프로필 저장소는 대상 라이브러리의 적절한 대상(예: Adobe Analytics, Adobe Audience Manager 등에서 공유되는 대상)을 요청합니다.<br />고객 속성은 묶음 프로세스를 통해 프로필 저장소로 전송됩니다. |
| 6 | 프로필 저장소는 활동을 필터링하기 위한 대상 자격 및 버킷팅에 사용됩니다. |
| 7 | 라이브에서 경험이 결정된 후 결과 콘텐츠가 선택됩니다 [!DNL Target] 활동. |
| 8 | at.js 라이브러리는 렌더링해야 하는 경험과 연결된 페이지에서 해당 요소를 숨깁니다. |
| 9 | at.js 라이브러리에는 방문자가 볼 수 있도록 페이지의 나머지 부분을 로드할 수 있도록 본문이 표시됩니다. |
| 10 | at.js 라이브러리는 DOM을 조작하여 의 경험을 렌더링합니다. [!DNL Target] 에지 네트워크. |
| 11 | 방문자에 대해 경험이 렌더링됩니다. |
| 12 | 전체 웹 페이지가 로드됩니다. |
| 13 | Analytics 데이터가 데이터 수집 서버로 전송됩니다. |
| 14 | 타기팅된 데이터는 SDID를 통해 Analytics 데이터에 대응되며 Analytics 보고 저장소로 처리됩니다. 그런 다음 Analytics 데이터는 [!DNL Target]Analytics for [!UICONTROL  (A4T) 보고서를 통해 Analytics 및 ]Target 모두에서 볼 수 있게 됩니다. |

### 온디바이스 전용

온디바이스 전용 은 다음과 같은 경우 at.js 2.5.0+에서 설정해야 하는 의사 결정 방법입니다 [!UICONTROL 온디바이스 의사 결정] 는 웹 페이지 전체에서 만 사용해야 합니다.

[!UICONTROL 온디바이스 의사 결정] 은 자격 조건을 갖춘 모든 활동이 포함된 캐시된 규칙 아티팩트에서 결정이 수행되므로 매우 빠른 속도로 경험 및 개인화 활동을 제공할 수 있습니다 [!UICONTROL 온디바이스 의사 결정].

적합한 활동에 대해 자세히 알아보려면 [!UICONTROL 온디바이스 의사 결정], 참조 [에서 지원되는 기능 [!UICONTROL 온디바이스 의사 결정]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md).

이 의사 결정 방법은 Target의 의사 결정이 필요한 모든 페이지에서 성능이 매우 중요한 경우에만 사용해야 합니다. 또한 이 결정 방법을 선택하면 [!DNL Target] 자격이 없는 활동 [!UICONTROL 온디바이스 의사 결정] 은(는) 전달되거나 실행되지 않습니다. at.js 라이브러리 2.5.0+는 의사 결정을 위해 캐시된 규칙 아티팩트만 찾도록 구성됩니다.

다음 다이어그램은 방문자, 브라우저, at.js 2.5.0+ 및 Akamai CDN 간의 상호 작용을 보여 줍니다. Akamai CDN은 방문자의 첫 번째 방문에 대해 규칙 아티팩트를 캐시합니다. 새 방문자의 첫 번째 페이지 방문의 경우 방문자의 브라우저에서 로컬로 캐시되려면 Akamai CDN에서 JSON 규칙 아티팩트를 다운로드해야 합니다. JSON 규칙 아티팩트가 다운로드되면 차단 네트워크 호출 없이 즉시 결정됩니다. 다음 흐름 다이어그램은 새 방문자를 캡처합니다.

이미지 를 클릭하여 전체 너비로 확장합니다.

![온디바이스 전용 흐름 다이어그램](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/on-device-only.png "온디바이스 전용 흐름 다이어그램"){zoomable=&quot;yes&quot;}

다음 목록은 다이어그램의 숫자와 일치합니다.

>[!NOTE]
>
>[!DNL Adobe Target] 관리 서버는 자격이 되는 모든 활동을 대상으로 합니다. [!UICONTROL 온디바이스 의사 결정]를 통해 JSON 규칙 아티팩트를 생성하고 Akamai CDN에 전파합니다. Akamai CDN에 전파할 새 JSON 규칙 아티팩트를 출력하는 업데이트가 있는지 활동이 계속 모니터링됩니다.

| 단계 | 설명 |
| --- | --- |
| 1 | Experience Cloud 방문자 ID는 [Adobe Experience Cloud ID 서비스](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | at.js 라이브러리는 동기식으로 로드되며 문서 본문을 숨깁니다.<br />at.js 라이브러리는 페이지에 구현된 코드 조각 사전 숨김(선택 사항)을 사용하여 비동기식으로 로드할 수도 있습니다. |
| 3 | at.js 라이브러리는 깜박임을 방지하기 위해 본문을 숨깁니다. |
| 4 | at.js 라이브러리는 방문자에게 가장 가까운 Akamai CDN에서 JSON 규칙 아티팩트를 검색하도록 요청합니다. |
| 5 | Akamai CDN이 JSON 규칙 아티팩트에 응답합니다. |
| 6 | JSON 규칙 아티팩트는 방문자의 브라우저에 로컬로 캐시됩니다. |
| 7 | at.js 라이브러리는 JSON 규칙 아티팩트를 해석하고 경험 검색 결정을 실행하고 테스트된 요소를 숨깁니다. |
| 8 | at.js 라이브러리에는 방문자가 볼 수 있도록 페이지의 나머지 부분을 로드할 수 있도록 본문이 표시됩니다. |
| 9 | at.js 라이브러리는 캐시된 JSON 규칙 아티팩트에서 경험을 렌더링하도록 DOM을 조작합니다. |
| 10 | 방문자에 대해 경험이 렌더링됩니다. |
| 11 | 전체 웹 페이지가 로드됩니다. |
| 12 | Analytics 데이터가 데이터 수집 서버로 전송됩니다. 타기팅된 데이터는 SDID를 통해 Analytics 데이터에 대응되며 Analytics 보고 저장소로 처리됩니다. 그런 다음 Analytics 데이터는 [!DNL Target]Analytics for [!UICONTROL  (A4T) 보고서를 통해 Analytics 및 ]Target 모두에서 볼 수 있게 됩니다. |

다음 다이어그램은 방문자의 후속 페이지 히트 또는 재방문에 대한 방문자, 브라우저, at.js 2.5.0+ 및 캐시된 JSON 규칙 아티팩트 간의 상호 작용을 보여 줍니다. JSON 규칙 아티팩트는 이미 캐시되어 있으며 브라우저에서 사용할 수 있으므로, 차단 네트워크 호출 없이 즉시 결정됩니다. 이 흐름 다이어그램은 후속 페이지 탐색 또는 재방문자를 캡처합니다.

이미지 를 클릭하여 전체 너비로 확장합니다.

![후속 페이지 탐색 및 반복 방문에 대한 온디바이스 전용 흐름 다이어그램](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/on-device-only-subsequent.png "후속 페이지 탐색 및 반복 방문에 대한 온디바이스 전용 흐름 다이어그램"){zoomable=&quot;yes&quot;}

다음 목록은 다이어그램의 숫자와 일치합니다.

>[!NOTE]
>
>[!DNL Adobe Target] 관리 서버는 자격이 되는 모든 활동을 대상으로 합니다. [!UICONTROL 온디바이스 의사 결정]를 통해 JSON 규칙 아티팩트를 생성하고 Akamai CDN에 전파합니다. Akamai CDN에 전파할 새 JSON 규칙 아티팩트를 출력하는 업데이트가 있는지 활동이 계속 모니터링됩니다.

| 단계 | 설명 |
| --- | --- |
| 1 | Experience Cloud 방문자 ID는 [Adobe Experience Cloud ID 서비스](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | at.js 라이브러리는 동기식으로 로드되며 문서 본문을 숨깁니다.<br />at.js 라이브러리는 페이지에 구현된 코드 조각 사전 숨김(선택 사항)을 사용하여 비동기식으로 로드할 수도 있습니다. |
| 3 | at.js 라이브러리는 깜박임을 방지하기 위해 본문을 숨깁니다. |
| 4 | at.js 라이브러리는 JSON 규칙 아티팩트를 해석하고 메모리에서 결정을 실행하여 경험을 검색합니다. |
| 5 | 테스트된 요소는 숨겨집니다. |
| 6 | at.js 라이브러리에는 방문자가 볼 수 있도록 페이지의 나머지 부분을 로드할 수 있도록 본문이 표시됩니다. |
| 7 | at.js 라이브러리는 캐시된 JSON 규칙 아티팩트에서 경험을 렌더링하도록 DOM을 조작합니다. |
| 8 | 방문자에 대해 경험이 렌더링됩니다. |
| 9 | 전체 웹 페이지가 로드됩니다. |
| 10 | Analytics 데이터가 데이터 수집 서버로 전송됩니다. 타기팅된 데이터는 SDID를 통해 Analytics 데이터에 대응되며 Analytics 보고 저장소로 처리됩니다. 그런 다음 Analytics 데이터는 [!DNL Target]Analytics for [!UICONTROL  (A4T) 보고서를 통해 Analytics 및 ]Target 모두에서 볼 수 있게 됩니다. |

### 하이브리드

Hybrid는 at.js 2.5.0+에서 설정해야 하는 의사 결정 방법입니다. [!UICONTROL 온디바이스 의사 결정] 및에 대한 네트워크 호출이 필요한 활동 [!DNL Adobe Target] 에지 네트워크를 실행해야 합니다.

두 항목을 모두 관리하는 경우 [!UICONTROL 온디바이스 의사 결정] 활동 및 서버측 활동, 배포 및 프로비저닝 방법을 생각하면 다소 복잡하고 지루할 수 있습니다 [!DNL Target] 페이지에서 확인할 수 있습니다. 결정 방법으로 하이브리드를 사용하면 [!DNL Target] 는에 대해 서버 호출을 수행해야 하는 시점을 알고 있습니다. [!DNL Adobe Target] 서버측 실행이 필요한 활동 및 디바이스에서 의사 결정만 실행할 경우 에지 네트워크.

JSON 규칙 아티팩트에는 mbox에 실행 중인 서버측 활동이 있는지 또는 가 있는지 여부를 at.js에 알려주는 메타데이터가 포함됩니다. [!UICONTROL 온디바이스 의사 결정] 활동. 이 의사 결정 방법을 사용하면 신속하게 전달하려는 활동을 [!UICONTROL 온디바이스 의사 결정] 및 보다 강력한 ML 기반 개인화가 필요한 활동의 경우 이러한 활동은 다음을 통해 수행됩니다. [!DNL Adobe Target] 에지 네트워크.

다음 다이어그램은 방문자, 브라우저, at.js 2.5.0+, Akamai CDN 및 [!DNL Adobe Target] 페이지를 처음 방문하는 새 방문자를 위한 Edge Network. 이 다이어그램의 장점은 JSON 규칙 아티팩트가 를 통해 결정되는 동안 비동기적으로 다운로드된다는 것입니다. [!DNL Adobe Target] 에지 네트워크.

이 접근 방식을 사용하면 많은 활동을 포함할 수 있는 아티팩트의 크기가 의사 결정 지연에 부정적인 영향을 주지 않습니다. JSON 규칙 아티팩트를 동기적으로 다운로드하고 그 후에 결정을 내리는 것은 지연에 부정적인 영향을 줄 수 있으며 일관되지 않을 수 있습니다. 따라서 하이브리드 의사 결정 방법은 새 방문자에 대한 의사 결정에 대해 항상 서버측 호출을 하는 것이 모범 사례 권장 사항이며 JSON 규칙 아티팩트가 동시에 캐시됩니다. 이후 페이지 방문 횟수 및 재방문 횟수의 경우 JSON 규칙 아티팩트를 통해 캐시 및 인메모리에서 결정됩니다.

이미지 를 클릭하여 전체 너비로 확장합니다.

![처음 방문자에 대한 하이브리드 흐름 다이어그램](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/hybrid-first-time-visitor.png "처음 방문자에 대한 하이브리드 흐름 다이어그램"){zoomable=&quot;yes&quot;}

다음 목록은 다이어그램의 숫자와 일치합니다.

>[!NOTE]
>
>[!DNL Adobe Target] 관리 서버는 자격이 되는 모든 활동을 대상으로 합니다. [!UICONTROL 온디바이스 의사 결정]를 통해 JSON 규칙 아티팩트를 생성하고 Akamai CDN에 전파합니다. Akamai CDN에 전파할 새 JSON 규칙 아티팩트를 출력하는 업데이트가 있는지 활동이 계속 모니터링됩니다.

| 단계 | 설명 |
| --- | --- |
| 1 | Experience Cloud 방문자 ID는 [Adobe Experience Cloud ID 서비스](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | at.js 라이브러리는 동기식으로 로드되며 문서 본문을 숨깁니다.<br />at.js 라이브러리는 페이지에 구현된 코드 조각 사전 숨김(선택 사항)을 사용하여 비동기식으로 로드할 수도 있습니다. |
| 3 | at.js 라이브러리는 깜박임을 방지하기 위해 본문을 숨깁니다. |
| 4 | 에 대한 페이지 로드 요청이 이루어집니다. [!DNL Adobe Target] (ECID, 고객 ID, 사용자 지정 매개 변수, 사용자 프로필 등과 같은 구성된 모든 매개 변수가 포함된 Edge Network.) |
| 5 | 동시에 at.js는 방문자에게 가장 가까운 Akamai CDN에서 JSON 규칙 아티팩트를 검색하도록 요청합니다. |
| 6 | ([!DNL Adobe Target] Edge Network) 프로필 스크립트가 실행된 다음 프로필 저장소에 반영됩니다. 프로필 저장소는 대상 라이브러리의 적절한 대상(예: Adobe Analytics, Adobe Audience Manager 등에서 공유되는 대상)을 요청합니다. |
| 7 | Akamai CDN이 JSON 규칙 아티팩트에 응답합니다. |
| 8 | 프로필 저장소는 활동을 필터링하기 위한 대상 자격 및 버킷팅에 사용됩니다. |
| 9 | 라이브에서 경험이 결정된 후 결과 콘텐츠가 선택됩니다 [!DNL Target] 활동. |
| 10 | at.js 라이브러리는 렌더링해야 하는 경험과 연결된 페이지에서 해당 요소를 숨깁니다. |
| 11 | at.js 라이브러리에는 방문자가 볼 수 있도록 페이지의 나머지 부분을 로드할 수 있도록 본문이 표시됩니다. |
| 12 | at.js 라이브러리는 DOM을 조작하여 의 경험을 렌더링합니다. [!DNL Target] 에지 네트워크. |
| 13 | 방문자에 대해 경험이 렌더링됩니다. |
| 14 | 전체 웹 페이지가 로드됩니다. |
| 15 | Analytics 데이터가 데이터 수집 서버로 전송됩니다. 타기팅된 데이터는 SDID를 통해 Analytics 데이터에 대응되며 Analytics 보고 저장소로 처리됩니다. 그런 다음 Analytics 데이터는 [!DNL Target]Analytics for [!UICONTROL  (A4T) 보고서를 통해 Analytics 및 ]Target 모두에서 볼 수 있게 됩니다. |

다음 다이어그램은 후속 페이지 탐색 또는 재방문을 위해 방문자, 브라우저, at.js 2.5.0+ 및 캐시된 JSON 규칙 아티팩트 간의 상호 작용을 보여 줍니다. 이 다이어그램에서는 후속 페이지 탐색 또는 재방문에 대해 디바이스에서 의사 결정이 이루어지는 사용 사례에만 중점을 둡니다. 특정 페이지에 대해 라이브 상태인 활동에 따라 서버측 결정을 실행하기 위해 서버측 호출을 수행할 수 있습니다.

이미지 를 클릭하여 전체 너비로 확장합니다.

![후속 페이지 탐색 및 반복 방문을 위한 하이브리드 흐름 다이어그램](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/hybrid-subsequent.png "후속 페이지 탐색 및 반복 방문을 위한 하이브리드 흐름 다이어그램"){zoomable=&quot;yes&quot;}

다음 목록은 다이어그램의 숫자와 일치합니다.

>[!NOTE]
>
>[!DNL Adobe Target] 관리 서버는 자격이 되는 모든 활동을 대상으로 합니다. [!UICONTROL 온디바이스 의사 결정]를 통해 JSON 규칙 아티팩트를 생성하고 Akamai CDN에 전파합니다. Akamai CDN에 전파할 새 JSON 규칙 아티팩트를 출력하는 업데이트가 있는지 활동이 계속 모니터링됩니다.

| 단계 | 설명 |
| --- | --- |
| 1 | Experience Cloud 방문자 ID는 [Adobe Experience Cloud ID 서비스](https://experienceleague.adobe.com/docs/id-service/using/home.html). |
| 2 | at.js 라이브러리는 동기식으로 로드되며 문서 본문을 숨깁니다.<br />at.js 라이브러리는 페이지에 구현된 코드 조각 사전 숨김(선택 사항)을 사용하여 비동기식으로 로드할 수도 있습니다. |
| 3 | at.js 라이브러리는 깜박임을 방지하기 위해 본문을 숨깁니다. |
| 4 | 경험 검색을 요청합니다. |
| 5 | at.js 라이브러리는 JSON 규칙 아티팩트가 이미 캐시되었음을 확인하고 메모리에서 결정을 실행하여 경험을 검색합니다. |
| 6 | 테스트된 요소는 숨겨집니다. |
| 7 | at.js 라이브러리에는 방문자가 볼 수 있도록 페이지의 나머지 부분을 로드할 수 있도록 본문이 표시됩니다. |
| 8 | at.js 라이브러리는 캐시된 JSON 규칙 아티팩트에서 경험을 렌더링하도록 DOM을 조작합니다. |
| 9 | 방문자에 대해 경험이 렌더링됩니다. |
| 10 | 전체 웹 페이지가 로드됩니다. |
| 11 | Analytics 데이터가 데이터 수집 서버로 전송됩니다. 타기팅된 데이터는 SDID를 통해 Analytics 데이터에 대응되며 Analytics 보고 저장소로 처리됩니다. 그런 다음 Analytics 데이터는 [!DNL Target]Analytics for [!UICONTROL  (A4T) 보고서를 통해 Analytics 및 ]Target 모두에서 볼 수 있게 됩니다. |

## 활성화 방법 [!UICONTROL 온디바이스 의사 결정]?

[!UICONTROL 온디바이스 의사 결정] 모든 사용자가 사용할 수 있음 [!DNL Target] at.js 2.5.0+를 사용하는 고객

활성화하려면 [!UICONTROL 온디바이스 의사 결정]:

>[!NOTE]
>
>관리자 또는 승인자가 있어야 합니다. [사용자 역할](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) 온디바이스 의사 결정 토글을 활성화하거나 비활성화합니다.

1. 클릭 **[!UICONTROL 관리]** > **[!UICONTROL 구현]** > **[!UICONTROL 계정 세부 정보]**.
1. 아래 **[!UICONTROL 계정 세부 정보]**, 슬라이드 **[!UICONTROL 온디바이스 의사 결정]** &quot;켜짐&quot; 위치로 전환합니다.

   ![[!UICONTROL 온디바이스 의사 결정] 전환](assets/on-device-decisioning-toggle.png)

   &quot;기존 항목 모두 포함 [!UICONTROL 온디바이스 의사 결정] artifact의 qualified activities&quot; 옵션은 [!UICONTROL 온디바이스 의사 결정].
1. (조건부) 모든 라이브를 원하는 경우 토글을 &quot;켜짐&quot; 위치로 밉니다 [!DNL Target] 대상 활동 [!UICONTROL 온디바이스 의사 결정] 아티팩트에 자동으로 포함될 수 있습니다.

   이 토글을 해제하면 항목을 다시 만들고 활성화해야 합니다. [!UICONTROL 온디바이스 의사 결정] 생성된 규칙 아티팩트에 포함할 활동. 즉, 온디바이스 의사 결정 토글을 켜기 전에 라이브 상태에 있는 모든 활동은 규칙 아티팩트에 포함되지 않습니다.

온디바이스 의사 결정 토글을 활성화한 후 [!DNL Target] 생성 및 전파 시작 [규칙 아티팩트](/help/dev/implement/client-side/atjs/on-device-decisioning/rule-artifact.md) 클라이언트.

>[!WARNING]
>
>초기화하기 전에 토글을 활성화해야 합니다. [!DNL Adobe Target] 사용할 SDK [!UICONTROL 온디바이스 의사 결정]. 규칙 아티팩트는 먼저 다음을 위해 Akamai CDN을 생성하고 전파해야 합니다. [!UICONTROL 온디바이스 의사 결정] 일 때문에. 전파는 첫 번째 규칙 아티팩트가 생성되어 Akamai CDN으로 전파하는 데 5~10분 정도 걸릴 수 있습니다.

## at.js 2.5.0+에서 를 사용하도록 구성하는 방법 [!UICONTROL 온디바이스 의사 결정]?

1. 클릭 **[!UICONTROL 관리]** > **[!UICONTROL 구현]** > **[!UICONTROL 계정 세부 정보]**.
1. 아래 **[!UICONTROL 구현 방법]** > **[!UICONTROL 주요 구현 방법]**, 클릭 **[!UICONTROL 편집]** at.js 버전 옆에 있어야 합니다(at.js 2.5.0 이상이어야 함).

   ![기본 구현 방법 설정 편집](assets/main-implementation-method.png)

   >[!WARNING]
   >
   >이러한 기본 설정을 변경하기 전에 Client Care에 문의하여 현재 구현에 영향을 주지 않도록 하십시오.

1. 원하는 의사 결정 방법을 선택합니다.

   * 서버측 전용
   * 온디바이스 전용
   * 하이브리드

   ![at.js 설정 편집 패널](assets/global-settings.png)

### 전역 설정

모든 항목에 대해 기본 의사 결정 방법을 구성할 수 있습니다. [!DNL Target] 결정. 다양한 의사 결정 방법은 서버측 전용, 온디바이스 전용 및 하이브리드입니다. 에서 선택된 의사 결정 방법 [!DNL Target] UI가에 구성되어 있습니다. `window.targetGlobalSettings` 다음 아래에 `decisioningMethod` 필드. 에 대해 자세히 알아보기 `decisioningMethod` 위치: [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#decisioningmethod).

```javascript {line-numbers="true"}
<head> 
    <script type="text/javascript">

        window.targetGlobalSettings = { 
            clientCode: "yourClientCodeHere", 
            imsOrgId: "imsOrgId@AdobeOrg", 
            decisioningMethod: "on-device"

        }; 
    </script>

    <script type="text/javascript" src="at.js"></script> 
</head>
```

### 사용자 지정된 설정

다음을 설정하는 경우 `decisioningMethod` 위치: `window.targetGlobalSettings`, 하지만 을(를) 재정의하려는 경우 `decisioningMethod` 각 [!DNL Adobe Target] 사용 사례에 따라 다음 절차를 지정할 수 있습니다. `decisioningMethod` at.js2.5.0+의 [getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) 호출합니다.

```javascript {line-numbers="true"}
adobe.target.getOffers({ 

  decisioningMethod:"on-device", 
  request: { 
    execute: { 
      mboxes: [ 
        { 
          index: 0, 
          name: "homepage" 
        } 
      ] 
    } 
 } 
});
```

>[!NOTE]
>
>getOffers() 호출에서 의사 결정 메서드로 &quot;on-device&quot; 또는 &quot;hybrid&quot;를 사용하려면 전역 설정에 이 있는지 확인하십시오. `decisioningMethod` &quot;on-device&quot; 또는 &quot;hybrid&quot;로 표시됩니다. at.js 라이브러리 2.5.0+는 페이지에서 로드한 직후 JSON 규칙 아티팩트를 다운로드하고 캐시할지 여부를 알아야 합니다. 전역 설정에 대한 의사 결정 메서드가 &quot;서버측&quot;으로 설정되고 &quot;온디바이스&quot; 또는 &quot;하이브리드&quot; 의사 결정 메서드가 getOffers() 호출로 전달되는 경우 at.js 2.5.0+에는 온디바이스 의사 결정을 실행하기 위해 캐시된 JSON 규칙 아티팩트가 없습니다.

### 아티팩트 캐시 TTL

Target은 다음에 적합한 활동을 나타냅니다. [!UICONTROL 온디바이스 의사 결정] 메타데이터, 규칙 및 조건으로 구성된 아티팩트. 이 아티팩트는 Akamai CDN에 캐시됩니다. 사용자의 첫 번째 방문 동안 사용자의 브라우저는 를 나타내는 아티팩트를 다운로드하고 캐시합니다. [!UICONTROL 온디바이스 의사 결정] 활동.

이후 사이트를 방문하면 브라우저는 아티팩트의 최신 버전을 다운로드해야 하는지 여부를 자동으로 확인합니다. 이 검사는 지연을 추가합니다. 아티팩트 캐시 TTL은 마지막으로 성공한 다운로드 이후 업데이트된 아티팩트를 브라우저에서 확인하지 않으려는 시간(분)을 정의합니다. 기간이 길수록 성능이 향상됩니다. 기간이 짧을수록 데이터 신선도가 향상되지만 추가적인 지연 시간이 발생합니다.

## 활동이 이라는 것을 어떻게 알 수 있습니까 [!UICONTROL 온디바이스 의사 결정] 적격?

다음과 같은 활동을 만든 후 [!UICONTROL 온디바이스 의사 결정] 적격: 온디바이스 의사 결정 적격 이라고 표시된 레이블은 활동의 개요 페이지에 표시됩니다.

![활동의 개요 페이지에 있는 온디바이스 의사 결정 적격 레이블.](assets/on-device-decisioning-eligible-label.png)

이 레이블은 활동이 항상 을 통해 전달됨을 의미하지 않습니다. [!UICONTROL 온디바이스 의사 결정]. at.js 2.5.0+가 [!UICONTROL 온디바이스 의사 결정] 이 활동이 디바이스에서 실행됩니까? at.js 2.5.0+가 온디바이스를 사용하도록 구성되지 않은 경우 이 활동은 at.js에서 수행하는 서버 호출을 통해 계속 전달됩니다.

다음과 같은 모든 활동을 필터링할 수 있습니다. [!UICONTROL 온디바이스 의사 결정] 온디바이스 의사 결정 적격 필터를 통해 활동 페이지에서 적격 결정을 내릴 수 있습니다.

![활동 페이지의 온디바이스 의사 결정 적격 필터.](assets/on-device-decisioning-filter.png)

>[!NOTE]
>
>다음과 같은 활동을 만들고 활성화한 후 [!UICONTROL 온디바이스 의사 결정] 적용 가능, Akamai CDN 시점(presence point of presence)에 생성 및 전파되는 규칙 아티팩트에 포함되기까지 5~10분 정도 걸릴 수 있습니다.

## 다음을 확인하는 단계 요약 [!UICONTROL 온디바이스 의사 결정] 활동은 At.js 2.5.0을 통해 전달됩니다+?

1. 액세스 [!DNL Adobe Target] UI 및 탐색 **[!UICONTROL 관리]** > **[!UICONTROL 구현]** > **[!UICONTROL 계정 세부 정보]** 을(를) 활성화하려면 **[!UICONTROL 온디바이스 의사 결정]** 토글.
1. 활성화 **[!UICONTROL &quot;기존 항목 모두 포함 [!UICONTROL 온디바이스 의사 결정] 아티팩트의 적격 활동&quot;]** 토글.

   첫 번째 JSON 규칙 아티팩트 생성은 최대 10분 정도 소요될 수 있습니다.

1. 만들기 및 활성화 [에서 지원하는 활동 유형 [!UICONTROL 온디바이스 의사 결정]](/help/dev/implement/client-side/atjs/on-device-decisioning/supported-features.md), 및 다음을 확인합니다. [!UICONTROL 온디바이스 의사 결정] 적격.
1. 설정 **[!UICONTROL 의사 결정 방법]** 다음 중 하나로 **[!UICONTROL &quot;하이브리드&quot;]** 또는 **[!UICONTROL &quot;온디바이스 전용&quot;]** at.js 설정 UI를 통해
1. At.js 2.5.0+를 다운로드하여 페이지에 배포합니다.
