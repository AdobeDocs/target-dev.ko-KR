---
keywords: 서버측, 서버측, sdk, sdk, sdk, 온디바이스, 의사 결정, 온디바이스, 온디바이스, 제로 지연, 지연, 거의 제로, node.js, server side3
description: 사용 방법 알아보기 [!UICONTROL [!UICONTROL 온디바이스 의사 결정]를 캐시하려면 ] [!DNL Target] 거의 0에 가까운 지연 시간에 메모리 내 의사 결정을 수행하기 위한 서버의 A/B 및 MVT 활동.
title: 온디바이스 의사 결정이란 무엇입니까?
feature: Implement Server-side
exl-id: 22ed3072-56f0-4075-9d1a-d642afe3b649
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 8%

---

# 온디바이스 의사 결정 개요

차세대 [!DNL Adobe Target] 이제 SDK에서 오퍼 사용 [!UICONTROL 온디바이스 의사 결정]: 서버에서 A/B 및 Experience Targeting (XT) 캠페인을 캐시하고, 네트워크 요청을 차단하지 않고 거의 0에 가까운 지연 시간에 메모리 내 의사 결정을 수행하는 기능을 제공합니다. [!DNL Adobe Target]의 에지 네트워크.

[!DNL Adobe Target] 또한 라이브 서버 호출을 통해 실험 및 ML 기반 개인화 캠페인에서 가장 관련성이 높고 최신 경험을 제공할 수 있는 유연성을 제공합니다. 즉, 성과가 가장 중요할 때 다음을 활용하도록 선택할 수 있다 [!UICONTROL 온디바이스 의사 결정]가장 관련성이 높고 최신 경험이 필요한 경우 대신 서버 호출을 수행할 수 있습니다. 다음을 참조하십시오 [온디바이스 의사 결정과 edge decisioning 비교 사용 시기](../../sdk-guides/on-device-decisioning/supported-features.md) 을 사용할 수 있는 사용 사례에 대해 알아봅니다.

>[!NOTE]
>
>온디바이스 의사 결정은 클라이언트측과 서버측 구현 모두에서 사용할 수 있습니다. 이 문서에서는 [!UICONTROL 온디바이스 의사 결정] 서버측. 에 관한 정보를 위하여 [!UICONTROL 온디바이스 의사 결정] 클라이언트측의 경우 클라이언트측 구현 설명서 를 참조하십시오 [여기](../../../client-side/atjs/on-device-decisioning/on-device-decisioning.md).

## 어떻게 작동합니까?

을(를) 설치하고 초기화할 때 [!DNL Adobe Target] 을 사용한 SDK [!UICONTROL 온디바이스 의사 결정] 활성화됨, a *규칙 아티팩트* 서버에 가장 가까운 Akamai CDN에서 로컬로 다운로드 및 캐시됩니다. 검색 요청 시 [!DNL Adobe Target] 경험은 서버측 애플리케이션 내에서 이루어지며, 반환할 콘텐츠는 캐시된 규칙 아티팩트에 인코딩된 메타데이터를 기반으로 메모리 내에서 결정되며, 이 메타데이터는 다음을 모두 정의합니다. [!UICONTROL 온디바이스 의사 결정] A/B 및 XT 활동.

다음 다이어그램은 [!UICONTROL 온디바이스 의사 결정] 아키텍처. 이미지를 확장하려면 를 클릭합니다.

이미지 를 클릭하여 전체 너비로 확장합니다.

![온디바이스 의사 결정 아키텍처 다이어그램](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/assets/asset-sdk-local-decisioning-architecture-diagram.png "온디바이스 의사 결정 아키텍처 다이어그램"){zoomable=&quot;yes&quot;}

## 어떤 혜택이 있나요?

* **거의 0에 가까운 지연 결정을 제공합니다.** 네트워크 요청이 차단되지 않도록 메모리 내 및 디바이스에서 버킷팅 및 의사 결정이 수행됩니다.
* **애플리케이션 성능 향상** 최종 사용자 경험을 그대로 유지하면서 실험을 실행하고 고객 및 사용자에게 개인화를 제공할 수 있습니다.
* **Google 사이트 품질 점수를 개선합니다.** 메모리 내 및 서버측에서 발생하는 의사 결정을 통해 온라인 비즈니스의 Google 사이트 품질 점수를 개선하여 소비자가 더 많이 검색할 수 있도록 합니다.
* **실시간 분석에서 알아봅니다.** 을 통해 실시간으로 활동 성과를 통찰력 확보 [!DNL Adobe Target] 또는 A4T 보고를 통해 중요한 시점에 전략을 피벗할 수 있습니다.

## 지원되는 기능

### 활동

온디바이스 의사 결정은 [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html):

* [!UICONTROL A/B 테스트]
* [!UICONTROL 경험 타겟팅] (XT)

### 할당 방법

온디바이스 의사 결정은 다음과 같은 할당 방법을 지원합니다.

* 수동

### 대상 타기팅

온디바이스 의사 결정은 다음 대상 규칙을 지원합니다.

| 대상 규칙 | 온디바이스 의사 결정 |
| --- | --- |
| [지역](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | 예 |
| [네트워크](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | 아니요 |
| [모바일](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | 아니요 |
| [사용자 지정 매개 변수](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | 예 |
| [운영 체제](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | 예 |
| [사이트 페이지](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | 예 |
| [브라우저](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | 예 |
| [방문자 프로필](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | 아니요 |
| [트래픽 소스](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | 아니요 |
| [시간대](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | 예 |
| [Experience Cloud 대상](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Adobe Audience Manager, Adobe Analytics 및 Adobe Experience Manager의 대상 | 아니요 |

## 사용할 클라이언트를 프로비저닝하려면 어떻게 해야 합니까 [!UICONTROL 온디바이스 의사 결정]?

모든 사용자가 온디바이스 의사 결정을 사용할 수 있습니다. [!DNL Adobe Target] 를 사용하는 고객 [!DNL Adobe Target] 서버측 SDK입니다. 이 기능을 사용하려면 다음 위치로 이동하십시오. **[!UICONTROL 관리]** > **[!UICONTROL 구현]** > **[!UICONTROL 계정 세부 정보]** 다음에서 [!DNL Adobe Target] UI 및 활성화 **[!UICONTROL 온디바이스 의사 결정]** 토글.

>[!NOTE]
>
>관리자 또는 승인자가 있어야 합니다. *사용자 역할* 을(를) 활성화 또는 비활성화하려면 [!UICONTROL 온디바이스 의사 결정] 토글.

![대체 이미지](assets/asset-odd-toggle.png)

온디바이스 의사 결정 토글을 활성화한 후 [!DNL Adobe Target] 생성 및 전파가 시작됩니다. *규칙 아티팩트* 클라이언트.

>[!NOTE]
>
>초기화하기 전에 토글을 활성화하십시오. [!DNL Adobe Target] 사용할 SDK [!UICONTROL 온디바이스 의사 결정]. 규칙 아티팩트는 먼저 다음을 위해 Akamai CDN을 생성하고 전파해야 합니다. [!UICONTROL 온디바이스 의사 결정] 일 때문에.

### 기존 항목 모두 포함 [!UICONTROL 온디바이스 의사 결정] 아티팩트 토글 의 적격 활동

전환 **날짜** 라이브를 원하는 경우 [!DNL Target] 대상 활동 [!UICONTROL 온디바이스 의사 결정] 아티팩트에 자동으로 포함될 수 있습니다.

이 토글 나가기 **끔** 은(는) 다음을 다시 만들고 활성화해야 함을 의미합니다. [!UICONTROL 온디바이스 의사 결정] 생성된 규칙 아티팩트에 포함될 활동을 지정합니다.

## 활동은 어떻게 알 수 있습니까? [!UICONTROL 온디바이스 의사 결정] 가능합니까?

활동을 만든 후 레이블 을 호출합니다. **[!UICONTROL 의사 결정 방법]**&#x200B;활동 세부 사항 페이지에 표시되면 활동이 [!UICONTROL 온디바이스 의사 결정] 할 수 있습니다.

![대체 이미지](assets/asset-odd9.png)

다음과 같은 모든 활동을 볼 수도 있습니다. [!UICONTROL 온디바이스 의사 결정] 다음에 사용 가능 **[!UICONTROL 활동]** 열을 추가하여 페이지 **[!UICONTROL 의사 결정 방법]** 활동 목록으로 이동합니다.

![대체 이미지](assets/asset-odd7.png)

>[!NOTE]
>
>다음과 같은 활동을 만들고 활성화한 후 [!UICONTROL 온디바이스 의사 결정] Akamai CDN PoPs에 생성 및 전파되는 규칙 아티팩트에 포함되기까지 최대 5~10분이 소요될 수 있습니다.

## 다음을 확인하기 위해 따라야 하는 단계에 대한 요약은 무엇입니까? [!UICONTROL 온디바이스 의사 결정] 활동은 다음을 통해 성공적으로 전달되었습니다. [!DNL Adobe Target]의 서버측 SDK?

1. 액세스 [!DNL Adobe Target] UI 및 탐색 **[!UICONTROL 관리]** > **[!UICONTROL 구현]** > **[!UICONTROL 계정 세부 정보]** 을(를) 활성화하려면 **[!UICONTROL 온디바이스 의사 결정]** 토글.
1. 활성화 **[!UICONTROL 기존 항목 모두 포함 [!UICONTROL 온디바이스 의사 결정] 아티팩트의 적격 활동]** 토글.
1. 에서 지원하는 활동 유형 만들기 및 활성화 [!UICONTROL 온디바이스 의사 결정]을 클릭하고 **[!UICONTROL 의사 결정 방법]** 은(는) **[!UICONTROL 온디바이스 의사 결정]** 을 참조하십시오.
1. 설치 및 초기화 [Node.js](../../node-js/overview.md) 또는 [Java](../../java/overview.md) 을 사용한 SDK `decisioningMethod = on-device`.
1. 구현 `getOffers()` 또는 `getAttributes()` 를 사용하여 디바이스에서 경험을 검색할 수 있습니다.
1. 코드 배포.

위의 1~3단계를 시작하는 방법을 보여 주는 예는 다음을 참조하십시오. [시작](../getting-started/getting-started.md) 섹션.


## 추가 리소스

### 웨비나: [!DNL Adobe Target]의 디바이스에서 의사 결정을 통해 대기 시간 없이 개인화 및 테스트

그 어느 때보다 마케터, 제품 소유자 및 개발자들은 사이트, 앱, 그리고 고객과 연결되는 모든 곳에서 전체적인 고객 경험을 최적화해야 하는 과제를 안고 있습니다. 데이터 사일로와 복잡한 구현이 포함된 여러 도구는 적절하지 않습니다.

이 녹화된 웨비나에서, [!DNL Adobe Target] 제품 전문가들은 중요한 경험 최적화 결정을 디바이스에서 대기 시간이 거의 없이 로컬로 실행하기 위해 이동함으로써 고객의 사이트 성능을 향상시키는 동시에 흥미로운 새로운 사용 사례를 어떻게 활용할 수 있는지에 대해 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/328148/?quality=12)


### 자습서: 온디바이스 의사 결정

[!DNL Adobe Target] [!UICONTROL 온디바이스 의사 결정] 거의 0에 가까운 지연 시간 콘텐츠 전달을 활성화합니다.

이 7분 길이의 비디오:

* 설명 [!UICONTROL 온디바이스 의사 결정], 의 다른 메서드와 비교하는 방법 포함 [!DNL Target] 구현
* 을 활성화하는 방법을 보여 줍니다. [!UICONTROL 온디바이스 의사 결정] Target
* JSON 콘텐츠로 구성된 샘플 양식 기반 작성기 활동을 검사합니다
* 에 필요한 키 구성이 포함된 샘플 Node.JS SDK 코드를 표시합니다. [!UICONTROL 온디바이스 의사 결정]
* 브라우저에서 결과를 보여 줍니다

>[!VIDEO](https://video.tv.adobe.com/v/329032/?quality=12)

자세한 비디오 및 튜토리얼은 [[!DNL Adobe Target] Tutorials](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=ko-KR).

### Adobe 기술 블로그 - 파트 1: 실행 [!DNL Adobe Target] Edge 플랫폼(Akamai Edge Workers)에서 실험과 개인화를 위한 NodeJS SDK

[블로그 게시물에 액세스하려면 여기를 클릭하십시오.](https://medium.com/adobetech/part-1-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-4d8660964ed9).

### Adobe 기술 블로그 - 파트2: Edge 플랫폼(AWS Lambda@Edge)에서 실험과 개인화에 대해 [!DNL Adobe Target] NodeJS SDK 실행하기

[블로그 게시물에 액세스하려면 여기를 클릭하십시오.](https://medium.com/adobetech/part-2-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-aws-4d6bdac24563).
