---
keywords: 시스템 다이어그램, 플리커, at.js, 구현, javascript 라이브러리, js, atjs, $8
description: 페이지가 로드될 때의 워크플로를 이해하는 데 도움이 되는 시스템 다이어그램을 포함하여 [!DNL Target] at.js JavaScript 라이브러리가 작동하는 방법에 대해 알아봅니다.
title: at.js JavaScript 라이브러리는 어떻게 작동합니까?
feature: at.js
exl-id: 9183797c-857b-4b7f-a573-6bb1d583f7b1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 66%

---

# at.js 작동 방식

[!DNL Adobe Target] 클라이언트측을 구현하려면 at.js JavaScript 라이브러리를 사용해야 합니다.

클라이언트측 [!DNL Adobe Target]의 구현에서 [!DNL Target]은 활동과 연관된 경험을 클라이언트 브라우저에 직접 전달합니다. 브라우저는 표시할 경험을 결정하고 표시합니다. 클라이언트측 구현에서는 WYSIWYG 편집기, VEC([시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)) 또는 [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)인 비-시각적 인터페이스를 사용하여 테스트 및 개인화 경험을 만들 수 있습니다.

## at.js란 무엇입니까?

at.js 라이브러리는 [!DNL Adobe Target]의 클라이언트측 구현을 위한 구현 라이브러리입니다. at.js 라이브러리는 웹 구현에 대한 페이지 로드 시간을 향상시키고, 단일 페이지 애플리케이션에 대해 더 나은 구현 옵션을 제공합니다. at.js는 권장되는 구현 라이브러리이며 새 기능으로 자주 업데이트됩니다. 모든 고객은 [최신 버전의 at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md)를 구현하거나 이 버전으로 마이그레이션하는 것이 좋습니다.

자세한 내용은 [Target JavaScript 라이브러리](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#libraries)를 참조하십시오.

아래에 표시된 [!DNL Target]구현에서 구현되는 Adobe Experience Cloud 솔루션은 [!DNL Analytics], Target 및 [!DNL Audience Manager]입니다. 또한 다음 [!DNL Experience Cloud]개의 핵심 서비스가 구현됩니다. [!DNL Adobe Experience Platform], [!UICONTROL Audiences] 및 [!UICONTROL Visitor ID Service].

## at.js 1과의 차이점&#x200B;*x* 및 at.js 2.x 워크플로 다이어그램의 차이점은 무엇입니까?

[at.js 1.x에서 at.js 2.x로 업그레이드](/help/dev/implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md)에서 1.*x*&#x200B;와 다른 2.O에 도입된 차이점을 자세히 알 수 있습니다.

상위 수준의 보기에서 보면 두 버전 간에 두 가지 차이점이 있습니다.

* at.js 2.x에는 글로벌 mbox 요청 개념이 없지만 페이지 로드 요청은 있습니다. 페이지 로드 요청은 웹 사이트의 초기 페이지 로드 시 적용해야 하는 콘텐츠를 검색하는 요청으로 볼 수 있습니다.
* at.js 2.x에서는 SPA(단일 페이지 애플리케이션)에 사용되는 [!UICONTROL Views]이라는 개념을 관리합니다. at.js 1.*x*&#x200B;는 이 개념을 알지 못합니다.

## at.js 2.x 다이어그램

다음 다이어그램은 [!UICONTROL Views]을(를) 사용하는 at.js 2.x의 워크플로를 이해하고 이를 통해 SPA 통합이 어떻게 향상되는지를 이해하는 데 도움이 됩니다. at.js 2.x에서 사용되는 개념의 도입을 보다 잘 이해하려면 [단일 페이지 애플리케이션 구현](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)을 참조하십시오.

이미지 를 클릭하여 전체 너비로 확장합니다.

![at.js 2.x가 있는 Target 흐름](/help/dev/implement/client-side/assets/system-diagram-atjs-20.png "at.js 2.x가 있는 Target 흐름"){zoomable="yes"}

| 단계 | 세부 사항 |
| --- | --- |
| 1 | 사용자가 인증되면 호출에서 [!UICONTROL Experience Cloud ID]를 반환합니다. 다른 호출은 고객 ID를 동기화합니다. |
| 2 | at.js 라이브러리는 동기식으로 로드되며 문서 본문을 숨깁니다.<br />at.js는 페이지에 구현된 스니펫을 미리 숨기는 선택 사항을 사용하여 비동기식으로 로드할 수도 있습니다. |
| 3 | 모든 구성된 매개변수(MCID, SDID 및 고객 ID)를 포함하는 페이지 로드 요청이 이루어집니다. |
| 4 | 프로필 스크립트가 실행된 다음 [!UICONTROL Profile Store]에 전달됩니다. Store는 [!UICONTROL Audience Library]의 적격 대상(예: [!DNL Adobe Analytics], [!DNL Audience Manager]에서 공유되는 대상 등)을 요청합니다.<br />고객 속성은 배치 프로세스를 통해 [!UICONTROL Profile Store]로 전송됩니다. |
| 5 | [!DNL Target]에서는 URL 요청 매개변수 및 프로필 데이터를 기반으로 현재 페이지 및 미래 보기를 위해 방문자에게 반환할 활동 및 경험을 결정합니다. |
| 6 | 타기팅된 콘텐츠는 다시 페이지로 전송되며, 원할 경우 추가적인 개인화를 위한 프로필 값을 포함할 수 있습니다.<br />현재 페이지의 타기팅된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다.<br />SPA에서 사용자 작업의 결과로 표시되는 보기의 대상 콘텐츠는 브라우저에 캐시되므로 보기가 `triggerView()`를 통해 트리거될 때 추가적인 서버 호출 없이 즉시 적용될 수 있습니다. |
| 7 | Analytics 데이터가 [!UICONTROL Data Collection] 서버로 전송됩니다. |
| 8 | 타깃팅된 데이터는 SDID를 통해 Analytics 데이터에 대응되며 [!DNL Analytics] 보고 저장소로 처리됩니다.그런 다음 <br />[!DNL Analytics] 데이터는 (A4T) 보고서를 통해 [!DNL Analytics] 및 [!DNL Target] 모두에서 볼 수 있습니다. |

이제 SPA에서 `triggerView()`이(가) 구현되면 캐시에서 [!UICONTROL Views] 및 작업을 검색하고 서버 호출 없이 사용자에게 표시합니다. `triggerView()`는 또한 노출 수를 증가시키고 기록하기 위해 [!DNL Target] 백엔드에 알림을 요청합니다. 보기가 있는 SPA용 at.js에 대한 자세한 내용은 [단일 페이지 애플리케이션 구현](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)을 참조하십시오.

이미지 를 클릭하여 전체 너비로 확장합니다.

![Target 흐름 at.js 2.x triggerView](/help/dev/implement/client-side/assets/atjs-20-triggerview.png "Target 흐름 at.js 2.x triggerView"){zoomable="yes"}

| 단계 | 세부 사항 |
| --- | --- |
| 1 | [!UICONTROL View]을(를) 렌더링하고 작업을 적용하여 시각적 요소를 수정하기 위해 SPA에서 `triggerView()`을(를) 호출합니다. |
| 2 | 보기용으로 타기팅된 콘텐츠를 캐시에서 읽습니다. |
| 3 | 타기팅된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다. |
| 4 | 활동 및 증분 지표에서 방문자를 계산하기 위해 알림 요청이 [!DNL Target] [!UICONTROL Profile Store] (으)로 전송됩니다. |
| 5 | [!DNL Analytics] 데이터가 [!UICONTROL Data Collection Servers] (으)로 전송되었습니다. |
| 6 | [!DNL Target] 데이터가 SDID를 통해 [!DNL Analytics] 데이터와 일치하고 [!DNL Analytics] 보고 저장소로 처리됩니다. 그런 다음 [!DNL Analytics] 데이터는 A4T 보고서를 통해 [!DNL Analytics] 및 [!DNL Target] 모두에서 볼 수 있습니다. |

### 비디오 - at.js 2.x 아키텍처 다이어그램

at.js 2.x는 SPA에 대한 Adobe Target의 지원을 개선하고 다른 Experience Cloud 솔루션과 통합됩니다. 다음 비디오에서는 모든 것이 어떻게 합쳐지는지 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/26250/?quality=12)

자세한 내용은 [at.js 2.x 작동 방식 이해](https://experienceleague.adobe.com/docs/target-learn/tutorials/implementation/understanding-how-atjs-20-works.html)를 참조하십시오.

## at.js 1.x 다이어그램

다음 다이어그램은 at.js 1.x의 워크플로를 이해하는 데 도움이 됩니다.

이미지 를 클릭하여 전체 너비로 확장합니다.

![Target 흐름 at.js 1.x](/help/dev/implement/client-side/assets/target-flow.png "Target 흐름 at.js 1.x"){zoomable="yes"}

| 단계 | 설명 | 호출 | 설명 |
|--- |--- |--- |--- |
| 1 | 사용자가 인증되면 호출에서 Experience Cloud ID(MCID)를 반환합니다. 다른 호출은 고객 ID를 동기화합니다. | 2 | at.js 라이브러리는 동기식으로 로드되며 문서 본문을 숨깁니다. |
| 3 | 모든 구성된 매개변수, MCID, SDID 및 고객 ID(선택 사항)를 포함하는 글로벌 mbox 요청이 이루어집니다. | 4 | 프로필 스크립트가 실행된 다음 프로필 저장소에 반영됩니다. 저장소는 대상 라이브러리의 적절한 대상(예: Adobe Analytics, Audience Manager 등에서 공유되는 대상)을 요청합니다.<br />고객 속성은 묶음 프로세스를 통해 프로필 저장소로 전송됩니다. |
| 5 | [!DNL Target]에서는 URL, mbox 매개변수 및 프로필 데이터를 기반으로 방문자에게 반환할 활동 및 경험을 결정합니다. | 6 | 타기팅된 콘텐츠는 다시 페이지로 전송되며, 원할 경우 추가적인 개인화를 위한 프로필 값을 포함할 수 있습니다.<br />경험은 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다. |
| 7 | Analytics 데이터가 데이터 수집 서버로 전송됩니다. | 8 | Target 데이터는 SDID를 통해 Analytics 데이터에 대응되며 Analytics 보고 저장소로 처리됩니다.그런 다음 <br />Analytics 데이터는 [!UICONTROL Analytics for Target] (A4T) 보고서를 통해 Analytics 및 [!DNL Target] 모두에서 볼 수 있습니다. |

### 비디오 - 운영 시간: at.js 팁 및 개요(2019년 6월 26일)

이 비디오는 [!UICONTROL Adobe Customer Care] 팀이 주도하는 이니셔티브인 &quot;운영 시간&quot; 기록입니다.

* at.js 사용의 이점
* at.js 설정
* 플리커 처리
* at.js 디버깅
* 알려진 문제
* FAQ

>[!VIDEO](https://video.tv.adobe.com/v/27959/?quality=12)

## at.js에서 HTML 콘텐츠로 오퍼를 렌더링하는 방법

오퍼를 HTML 콘텐츠로 렌더링할 때 at.js는 다음 알고리즘을 적용합니다.

1. 이미지가 미리 로드됩니다(HTML 콘텐츠에 `<img>` 태그가 있는 경우).

1. HTML 콘텐츠가 DOM 노드에 첨부됩니다.

1. 인라인 스크립트가 실행됩니다(`<script>` 태그로 둘러싸인 코드).

1. 원격 스크립트가 비동기식으로 로드 및 실행됩니다(`src` 속성이 있는 `<script>` 태그).

중요 참고 사항:

* at.js는 비동기식으로 로드되므로 원격 스크립트 실행 순서에 대해 보장하지 않습니다.
* 원격 스크립트는 나중에 로드 및 실행되므로 인라인 스크립트에 대한 종속성을 가지면 안 됩니다.
