---
keywords: 서버측, 서버측, sdk, sdk, sdk, 온디바이스, 의사 결정, 온디바이스, 온디바이스, 제로 지연, 지연, 거의 제로, node.js, server side3
description: '[!UICONTROL [!UICONTROL on-device decisioning]을(를) 사용하여  [!DNL Target] A/B 및 MVT 활동을 서버에 캐시하여 거의 0에 가까운 대기 시간에 메모리 내 결정을 수행하는 방법에 대해 알아봅니다.'
title: 온디바이스 의사 결정이란 무엇입니까?
feature: Implement Server-side
exl-id: 22ed3072-56f0-4075-9d1a-d642afe3b649
source-git-commit: ff0becf3fe3a6fd6694e13243b6a93b910316434
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 9%

---

# 온디바이스 의사 결정 개요

차세대 [!DNL Adobe Target] SDK는 이제 [!DNL Adobe Target]의 Edge Network에 대한 네트워크 요청을 차단하지 않고 서버에서 A/B 및 Experience Targeting(XT) 캠페인을 캐시하고 거의 0에 가까운 대기 시간에 메모리 내 결정을 수행하는 기능을 제공하는 [!UICONTROL on-device decisioning]을(를) 제공합니다.

[!DNL Adobe Target]은(는) 또한 라이브 서버 호출을 통해 실험 및 ML 기반 개인화 캠페인에서 가장 관련성이 높고 최신 경험을 제공할 수 있는 유연성을 제공합니다. 즉, 성능이 가장 중요한 경우 [!UICONTROL on-device decisioning]을(를) 활용하도록 선택할 수 있지만 가장 관련성이 높고 최신 경험이 필요한 경우 대신 서버 호출을 수행할 수 있습니다. 상호 사용을 보증하는 사용 사례에 대해 알아보려면 [장치 대 Edge Decisioning을 사용할 시기](../../sdk-guides/on-device-decisioning/supported-features.md)를 참조하십시오.

>[!NOTE]
>
>온디바이스 의사 결정은 클라이언트측과 서버측 구현 모두에서 사용할 수 있습니다. 이 문서에서는 서버측 [!UICONTROL on-device decisioning]에 대해 설명합니다. 클라이언트측 [!UICONTROL on-device decisioning]에 대한 자세한 내용은 클라이언트측 구현 설명서 [여기](../../../client-side/atjs/on-device-decisioning/on-device-decisioning.md)를 참조하십시오.

## 어떻게 작동합니까?

[!UICONTROL on-device decisioning]이(가) 활성화된 [!DNL Adobe Target] SDK를 설치하고 초기화하면 서버와 가장 가까운 Akamai CDN에서 *규칙 아티팩트*&#x200B;가 서버에 로컬로 다운로드되고 캐시됩니다. 서버측 응용 프로그램 내에서 [!DNL Adobe Target] 경험 검색을 요청하면 캐시된 규칙 아티팩트에 인코딩된 메타데이터를 기반으로 반환할 콘텐츠에 대한 결정이 메모리 내에서 결정되며, 이는 모든 [!UICONTROL on-device decisioning] A/B 및 XT 활동을 정의합니다.

다음 다이어그램은 [!UICONTROL on-device decisioning] 아키텍처를 보여 줍니다. 이미지를 확장하려면 를 클릭합니다.

이미지 를 클릭하여 전체 너비로 확장합니다.

![온디바이스 의사 결정 아키텍처 다이어그램](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/assets/asset-sdk-local-decisioning-architecture-diagram.png "온디바이스 의사 결정 아키텍처 다이어그램"){zoomable="yes"}

## 어떤 혜택이 있나요?

* **지연 시간이 거의 0에 가까운 결정을 제공합니다.** 버킷팅 및 의사 결정은 네트워크 요청을 차단하지 않도록 인메모리 및 디바이스에서 수행됩니다.
* **응용 프로그램 성능을 향상시킵니다.** 실험을 실행하고 최종 사용자 환경을 손상시키지 않고 고객 및 사용자에게 개인화를 제공합니다.
* **Google 사이트 품질 점수를 개선합니다.** 메모리 내 및 서버측에서 발생하는 의사 결정을 통해 온라인 비즈니스의 Google 사이트 품질 점수를 향상시켜 소비자가 더 많이 검색할 수 있도록 하십시오.
* **실시간 분석에서 알아봅니다.** [!DNL Adobe Target] 또는 A4T 보고를 통해 실시간으로 활동 성과를 통찰력을 얻음으로써 중요한 순간에 전략을 피벗할 수 있습니다.

## 지원되는 기능

### 활동

디바이스에서 의사 결정은 [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)에서 만든 다음 활동 유형을 지원합니다.

* [!UICONTROL A/B Test]
* [!UICONTROL Experience Targeting](XT)

### 할당 방법

온디바이스 의사 결정은 다음과 같은 할당 방법을 지원합니다.

* 수동

### 대상 타기팅

온디바이스 의사 결정은 다음 대상 규칙을 지원합니다.

| 대상 규칙 | 온디바이스 의사 결정 |
| --- | --- |
| [지역](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | 예<P>온디바이스 의사 결정을 사용할 때 지원되는 지역 속성은 다음과 같습니다.<ul><li>국가/지역</li><li>구/군/시</li><li>위도</li><li>경도</li></ul> |
| [네트워크](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | 아니요 |
| [모바일](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | 아니요 |
| [사용자 지정 매개 변수](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | 예 |
| [운영 체제](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | 예 |
| [사이트 페이지](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | 예 |
| [브라우저](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | 예 |
| [방문자 프로필](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | 아니요 |
| [트래픽 소스](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | 아니요 |
| [시간대](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | 예 |
| [Experience Cloud 대상](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html)(Adobe Audience Manager, Adobe Analytics 및 Adobe Experience Manager의 대상) | 아니요 |

## [!UICONTROL on-device decisioning]을(를) 사용하도록 클라이언트를 프로비저닝하려면 어떻게 해야 합니까?

[!DNL Adobe Target] 서버측 SDK를 사용하는 모든 [!DNL Adobe Target] 고객에게 온디바이스 의사 결정을 사용할 수 있습니다. 이 기능을 사용하려면 [!DNL Adobe Target] UI에서 **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]**(으)로 이동하여 **[!UICONTROL On-Device Decisioning]** 전환을 활성화하십시오.

>[!NOTE]
>
>[!UICONTROL On-Device Decisioning] 전환을 활성화하거나 비활성화하려면 관리자 또는 승인자 *사용자 역할*&#x200B;이(가) 있어야 합니다.

![대체 이미지](assets/asset-odd-toggle.png)

On-Device Decisioning 토글을 활성화한 후 [!DNL Adobe Target]에서 클라이언트에 대한 *규칙 아티팩트*&#x200B;를 생성하고 전파합니다.

>[!NOTE]
>
>[!UICONTROL on-device decisioning]을(를) 사용하도록 [!DNL Adobe Target] SDK를 초기화하기 전에 토글을 활성화하십시오. [!UICONTROL on-device decisioning]이(가) 작동하려면 먼저 규칙 아티팩트가 생성되어 Akamai CDN으로 전파되어야 합니다.

### 아티팩트 토글 영역에 기존의 모든 [!UICONTROL on-device decisioning]개 적격 활동 포함

[!UICONTROL on-device decisioning]의 자격이 되는 모든 라이브 [!DNL Target] 활동을 아티팩트에 자동으로 포함시키려면 이 **on**&#x200B;을(를) 전환하십시오.

이 토글을 **끄기**&#x200B;로 두면 생성된 규칙 아티팩트에 포함할 [!UICONTROL on-device decisioning] 활동을 다시 만들고 활성화해야 합니다.

## 활동이 [!UICONTROL on-device decisioning] 가능한지를 어떻게 알 수 있습니까?

활동을 만든 후 활동 세부 정보 페이지에 표시되는 레이블 **[!UICONTROL Decisioning Method]**&#x200B;은(는) 활동이 [!UICONTROL on-device decisioning] 가능한지 여부를 나타냅니다.

![대체 이미지](assets/asset-odd9.png)

**[!UICONTROL Decisioning Method]** 열을 활동 목록에 추가하여 **[!UICONTROL Activities]** 페이지에서 [!UICONTROL on-device decisioning]할 수 있는 모든 활동을 볼 수도 있습니다.

![대체 이미지](assets/asset-odd7.png)

>[!NOTE]
>
>[!UICONTROL on-device decisioning] 가능한 활동을 만들고 활성화한 후 Akamai CDN PoPs에 생성 및 전파되는 규칙 아티팩트에 포함되기까지 최대 20분이 걸릴 수 있습니다.

## [!UICONTROL on-device decisioning] 활동이 [!DNL Adobe Target]의 서버측 SDK를 통해 성공적으로 전달되도록 하려면 따라야 할 단계에 대한 요약은 무엇입니까?

1. [!DNL Adobe Target] UI에 액세스하여 **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]**(으)로 이동하여 **[!UICONTROL On-Device Decisioning]** 전환을 활성화합니다.
1. **[!UICONTROL Include all existing [!UICONTROL on-device decisioning] qualified activities in the artifact]** 토글을 사용하도록 설정합니다.
1. [!UICONTROL on-device decisioning]에서 지원하는 활동 유형을 만들고 활성화한 다음 해당 활동에 대해 **[!UICONTROL Decisioning Method]**&#x200B;이(가) **[!UICONTROL On-Device Decisioning]**&#x200B;인지 확인하십시오.
1. `decisioningMethod = on-device`을(를) 사용하여 [Node.js](../../node-js/overview.md) 또는 [Java](../../java/overview.md) SDK를 설치하고 초기화합니다.
1. 코드에서 `getOffers()` 또는 `getAttributes()`을(를) 구현하여 디바이스에서 경험을 검색합니다.
1. 코드 배포.

위의 1~3단계를 시작하는 방법을 보여 주는 예제는 [시작하기](../getting-started/getting-started.md) 섹션을 참조하십시오.


## 추가 리소스

### 웨비나: [!DNL Adobe Target]의 디바이스에서 의사 결정을 통해 대기 시간 없이 개인화 및 테스트

그 어느 때보다 마케터, 제품 소유자 및 개발자들은 사이트, 앱, 그리고 고객과 연결되는 모든 곳에서 전체적인 고객 경험을 최적화해야 하는 과제를 안고 있습니다. 데이터 사일로와 복잡한 구현이 포함된 여러 도구는 적절하지 않습니다.

이 녹화된 웨비나에서 [!DNL Adobe Target] 제품 전문가들이 중요한 경험 최적화 결정을 디바이스에서 대기 시간이 거의 없는 상태로 로컬로 실행하기 위해 이동함으로써 고객의 사이트 성능을 향상시키는 동시에 흥미로운 새로운 사용 사례를 어떻게 활용할 수 있는지에 대해 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/328148/?quality=12)


### 자습서: 온디바이스 의사 결정

[!DNL Adobe Target] [!UICONTROL on-device decisioning]은(는) 0에 가까운 지연 콘텐츠 전달을 사용합니다.

이 7분 길이의 비디오:

* [!DNL Target] 구현의 다른 메서드와 비교하는 방법을 포함하여 [!UICONTROL on-device decisioning]에 대해 설명합니다.
* Target에서 [!UICONTROL on-device decisioning]을(를) 활성화하는 방법을 보여 줍니다.
* JSON 콘텐츠로 구성된 샘플 양식 기반 작성기 활동을 검사합니다
* [!UICONTROL on-device decisioning]에 필요한 키 구성이 포함된 샘플 Node.JS SDK 코드를 표시합니다.
* 브라우저에서 결과를 보여 줍니다

>[!VIDEO](https://video.tv.adobe.com/v/329032/?quality=12)

자세한 비디오 및 튜토리얼은 [[!DNL Adobe Target] Tutorials](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=ko-KR)을 참조하세요.

### Adobe 기술 블로그 - 파트1: Edge 플랫폼(Akamai Edge Workers)에서 실험과 개인화에 대해 [!DNL Adobe Target] NodeJS SDK 실행

[블로그 게시물에 액세스하려면 여기를 클릭하세요](https://medium.com/adobetech/part-1-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-4d8660964ed9).

### Adobe 기술 블로그 - 파트2: Edge 플랫폼(AWS Lambda@Edge)에서 실험과 개인화에 대해 [!DNL Adobe Target] NodeJS SDK 실행하기

[블로그 게시물에 액세스하려면 여기를 클릭하세요](https://medium.com/adobetech/part-2-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-aws-4d6bdac24563).
