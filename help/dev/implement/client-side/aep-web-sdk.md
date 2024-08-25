---
keywords: Adobe Experience Platform Web SDK, aep web sdk, web sdk, sdk, adobe experience cloud, platform edge network, adobe experience platform edge network, edge network, aep edge network, Adobe Experience Platform Web SDK0
description: '[!UICONTROL Adobe Experience Platform Web SDK]을(를) 사용하여 [!UICONTROL AEP Edge Network]을(를) 통해 [!UICONTROL Adobe Experience Cloud]의 다양한 서비스와 상호 작용하는 방법에 대해 알아봅니다.'
title: '[!UICONTROL Experience Platform Web SDK]을(를) 사용하여 구현하려면 어떻게 해야 합니까?'
feature: AEP Web SDK
exl-id: 35ee60d2-3d6d-4169-9f22-b2aef4c6548b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 8%

---

# [!UICONTROL Adobe Experience Platform Web SDK]

[!UICONTROL Adobe Experience Platform Web SDK](AEP Web SDK)은 [!UICONTROL Adobe Experience Cloud]의 고객이 [!UICONTROL Adobe Experience Platform Edge Network]을(를) 통해 [!DNL Adobe Experience Cloud]([!DNL Target] 포함)의 다양한 서비스와 상호 작용할 수 있도록 하는 클라이언트측 JavaScript 라이브러리입니다. JavaScript 라이브러리 외에 웹 SDK 구성에 도움이 되는 [!UICONTROL Adobe Experience Platform] 확장도 있습니다.

자세한 내용은 *[!UICONTROL Adobe Experience Platform Web SDK]* 도움말에서 다음 링크를 참조하십시오.

* 전체 정보: [내용: [!UICONTROL Adobe Experience Platform Web SDK]](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [!DNL Target]에 대한 정보: [[!DNL Target] 개요](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html)

## 자습서

다음 튜토리얼은 구현에 도움이 됩니다.

### [!DNL Platform Web SDK](으)로 [!DNL Adobe Experience Cloud] 구현

[이 자습서](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=ko)에서 [!DNL Adobe Experience Platform Web SDK]을(를) 사용하여 [!DNL Experience Cloud] 응용 프로그램을 구현하는 방법을 알아봅니다. [!DNL Target]에 대한 자세한 내용은 Platform Web SDK로 [설정 [!DNL Target] 튜토리얼 섹션](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html)을 참조하십시오.

### at.js 2에서 [!DNL Target] 마이그레이션.*x*&#x200B;에서 [!DNL Platform Web SDK](으)로

at.js 2에서 [!DNL Target] 구현을 마이그레이션하는 방법을 알아봅니다.[이 자습서](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html)를 사용하여 [!DNL Adobe Experience Platform Web SDK]에 대한 *x*.

## 권장 설명서

위에 언급된 [!UICONTROL Platform Web SDK] 설명서 외에도 이 안내서의 항목에는 [!DNL Target] 기능 및 기능과 관련된 [!UICONTROL Platform Web SDK]과(와) 관련된 정보도 있습니다.

| 기능 | 설명/링크 |
| --- | --- |
| [활동 QA](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) | [!DNL Target]의 QA URL을 사용하여, 변경되지 않는 미리 보기 링크를 통한 간편한 엔드 투 엔드 활동 QA, 선택적 대상 타깃팅, 라이브 활동 데이터에서 세그먼트화된 QA 보고를 수행할 수 있습니다. 활동 QA를 사용하면 [!DNL Target] 활동을 라이브로 시작하기 전에 완전히 테스트할 수 있습니다.<p>[Target JavaScript 라이브러리 QA 모드 호환성](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#compatibility) 및 [미리 보기 URL](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#preview)을 참조하십시오. |
| [[!UICONTROL Analytics for Target](A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) | [!UICONTROL Adobe Analytics for Target]&#x200B;(A4T)은 [!DNL Analytics] 전환 지표 및 대상자 세그먼트를 기반으로 하는 활동을 생성할 수 있는 솔루션 간 통합입니다. A4T 통합을 통해 Analytics 보고서를 사용하여 결과를 검사할 수 있습니다.<p>[지원되는 활동 유형](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html#section_F487896214BF4803AF78C552EF1669AA) 및 [Adobe Experience Platform Web SDK 구현에 대한 구현 단계](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html#platform)를 참조하십시오. |
| [대상자](https://experienceleague.adobe.com/docs/target/using/audiences/target.html) | [!DNL Target]의 대상은 타깃팅된 활동에서 콘텐츠 및 경험을 보게 되는 사용자를 결정합니다.<p>[대상 목록 사용](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#use-list) 및 [여러 대상 결합](https://experienceleague.adobe.com/docs/target/using/audiences/combining-multiple-audiences.html)을 참조하세요. |
| [대상자 만들기](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=ko-KR) | [!DNL Adobe Experience Platform]에서 만든 대상을 사용하면 더 풍부한 고객 데이터를 제공하여 보다 효과적인 개인화를 실현할 수 있습니다.<p>[Adobe Experience Platform 대상 사용](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#aep)을 참조하세요. |
| [오퍼 결정](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | [!DNL Adobe Journey Optimizer]에서 만든 오퍼 결정을 [!DNL Target] 활동(수동 A/B 테스트 또는 경험 타깃팅)에 추가하여 웹과 모바일에서 방문자에 대한 다음 최상의 오퍼를 결정하고 전달합니다. |
| [리디렉션 오퍼 - A4T FAQ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html) | 리디렉션 오퍼를 사용하면 방문자의 브라우저가 새 페이지로 리디렉션됩니다.<p>[A4T에 대해 [!UICONTROL Adobe Experience Platform Web SDK]에서 리디렉션 오퍼를 지원합니까?](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html#platform)를 참조하십시오. |
| [응답 토큰](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) | 응답 토큰을 사용하면 [!DNL Target] 데이터를 Google Analytics 및 다른 타사 통합에 보낼 수 있습니다.<p>이 작업을 수행하는 방법에 대한 코드 샘플을 보려면 [Platform Web SDK를 통해 Google Analytics에게 데이터 보내기](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html#sending-data-to-google-analytics-via-platform-web-sdk)를 참조하십시오. |
| *[!UICONTROL Platform Web SDK]개요* 안내서의 [단일 페이지 응용 프로그램 구현](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html). | [!UICONTROL Adobe Experience Platform Web SDK]에서는 단일 페이지 애플리케이션(SPA)과 같은 차세대 클라이언트측 기술에 대한 개인화를 실행하도록 기업을 지원하는 다양한 기능을 제공합니다. |
| [TLS(전송 계층 보안) 암호화 변경 사항](../../before-implement/tls-transport-layer-security-encryption.md) | TLS(전송 계층 보안)를 사용하면 가장 높은 보안 표준을 유지하고 고객 데이터의 안전을 강화할 수 있습니다. |
