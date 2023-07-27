---
keywords: Adobe Experience Platform Web SDK, aep web sdk, web sdk, sdk, adobe experience cloud, platform edge network, adobe experience platform edge network, edge network, aep edge network, Adobe Experience Platform Web SDK0
description: 사용 방법 알아보기 [!UICONTROL Adobe Experience Platform 웹 SDK] 에서 다양한 서비스와 상호 작용하기 [!UICONTROL Adobe Experience Cloud] 다음을 통해 [!UICONTROL AEP Edge 네트워크].
title: 를 사용하여 를 구현하는 방법 [!UICONTROL Experience Platform Web SDK]?
feature: AEP Web SDK
exl-id: 35ee60d2-3d6d-4169-9f22-b2aef4c6548b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 12%

---

# [!UICONTROL Adobe Experience Platform Web SDK]

[!UICONTROL Adobe Experience Platform 웹 SDK] (AEP Web SDK)는 고객이 다음을 사용할 수 있는 클라이언트측 JavaScript 라이브러리입니다. [!UICONTROL Adobe Experience Cloud] 에서 다양한 서비스와 상호 작용하기 [!DNL Adobe Experience Cloud] (포함) [!DNL Target])을 통해 [!UICONTROL Adobe Experience Platform 에지 네트워크]. JavaScript 라이브러리 외에 [!UICONTROL Adobe Experience Platform] 웹 SDK 구성에 도움이 되는 확장입니다.

자세한 내용은 *[!UICONTROL Adobe Experience Platform 웹 SDK]* 도움말:

* 포괄적인 정보의 경우: [이란? [!UICONTROL Adobe Experience Platform 웹 SDK]](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* 관련 정보의 경우 [!DNL Target]: [[!DNL Target] 개요](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html)

## 자습서

다음 튜토리얼은 구현에 도움이 됩니다.

### 구현 [!DNL Adobe Experience Cloud] 포함 [!DNL Platform Web SDK]

구현 방법 알아보기 [!DNL Experience Cloud] 을 사용하는 애플리케이션 [!DNL Adobe Experience Platform Web SDK] 포함 [이 자습서](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=ko-KR). 관련 정보의 경우 [!DNL Target]을 참조하십시오. [설정 [!DNL Target] Platform Web SDK 사용](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).

### 마이그레이션 [!DNL Target] at.js 2.*x* 끝 [!DNL Platform Web SDK]

을(를) 마이그레이션하는 방법 알아보기 [!DNL Target] at.js 2.*x* (으)로 [!DNL Adobe Experience Platform Web SDK] 포함 [이 자습서](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html).

## 권장 설명서

이외에도 [!UICONTROL Platform Web SDK] 위에서 언급한 설명서, 이 안내서의 항목에는 [!UICONTROL Platform Web SDK] 과 관련되어 [!DNL Target] 기능.

| 기능 | 설명/링크 |
| --- | --- |
| [활동 QA](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) | 에서 QA URL 사용 [!DNL Target] 변경되지 않는 미리 보기 링크, 선택적 대상 타깃팅 및 라이브 활동 데이터에서 세그먼트화된 QA 보고를 사용하여 간편한 엔드 투 엔드 활동 QA를 수행할 수 있습니다. 활동 QA를 사용하여 다음을 완전히 테스트할 수 있습니다. [!DNL Target] 활동을 라이브로 시작하기 전에<p>다음을 참조하십시오 [Target JavaScript 라이브러리 QA 모드 호환성](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#compatibility) 및 [URL 미리보기](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#preview). |
| [[!UICONTROL Analytics for Target] (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) | [!UICONTROL Target을 위한 Adobe Analytics] (A4T)은 을 기반으로 활동을 만들 수 있는 솔루션 간 통합입니다 [!DNL Analytics] 전환 지표 및 대상 세그먼트. A4T 통합에서는 Analytics 보고서를 사용하여 결과를 검사할 수 있습니다.<p>다음을 참조하십시오 [지원되는 활동 유형](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html#section_F487896214BF4803AF78C552EF1669AA) 및 [Adobe Experience Platform 웹 SDK 구현을 위한 구현 단계](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html#platform). |
| [대상자](https://experienceleague.adobe.com/docs/target/using/audiences/target.html) | 의 대상 [!DNL Target] 타깃팅된 활동에서 콘텐츠 및 경험을 보게 되는 사용자를 결정합니다.<p>다음을 참조하십시오 [대상 목록 사용](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#use-list) 및 [여러 대상 결합](https://experienceleague.adobe.com/docs/target/using/audiences/combining-multiple-audiences.html). |
| [대상자 만들기](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=ko-KR) | [!DNL Adobe Experience Platform]에서 생성된 대상자를 사용하면 더 풍부한 고객 데이터를 제공하여 보다 효과적인 개인화를 실현할 수 있습니다.<p>다음을 참조하십시오 [Adobe Experience Platform의 대상 사용](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#aep). |
| [오퍼 결정](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | 다음에서 생성된 오퍼 결정 추가 [!DNL Adobe Journey Optimizer] 끝 [!DNL Target] 웹 및 모바일에서의 방문자에 대한 다음 번 베스트 오퍼를 결정하고 제공하는 활동(수동 A/B 테스트 또는 경험 타깃팅). |
| [리디렉션 오퍼 - A4T FAQ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html) | 리디렉션 오퍼를 사용하면 방문자의 브라우저가 새 페이지로 리디렉션됩니다.<p>다음을 참조하십시오 [다음을 수행합니다. [!UICONTROL Adobe Experience Platform 웹 SDK] a4T에 대한 리디렉션 오퍼 지원](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html#platform) |
| [응답 토큰](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) | 응답 토큰을 사용하면 을 보낼 수 있습니다. [!DNL Target] Google Analytics 및 기타 타사 통합에 대한 데이터입니다.<p>다음을 참조하십시오 [Platform Web SDK를 통해 Google Analytics에게 데이터 전송](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html#sending-data-to-google-analytics-via-platform-web-sdk) 을 클릭하여 이 작업을 수행하는 방법에 대한 코드 샘플을 확인하십시오. |
| [단일 페이지 애플리케이션 구현](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html) 다음에서 *[!UICONTROL Platform Web SDK] 개요* 가이드. | [!UICONTROL Adobe Experience Platform 웹 SDK] 은 단일 페이지 애플리케이션(SPA)과 같은 차세대 클라이언트측 기술에 대한 개인화를 실행하도록 기업을 지원하는 다양한 기능을 제공합니다. |
| [TLS(전송 계층 보안) 암호화 변경 사항](../../before-implement/tls-transport-layer-security-encryption.md) | TLS(전송 계층 보안)를 사용하면 가장 높은 보안 표준을 유지하고 고객 데이터의 안전을 강화할 수 있습니다. |
