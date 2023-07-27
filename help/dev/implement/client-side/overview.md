---
keywords: 구현, 구현, at.js, adobe experience platform web sdk, aep web sdk
description: 구현 방법 알아보기 [!DNL Adobe Target] 를 사용하는 클라이언트측 웹용 [!DNL Adobe Experience Platform Web SDK] (AEP Web SDK) 또는 at.js JavaScript 라이브러리입니다.
title: 구현 방법 [!DNL Target] 클라이언트측 웹용
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 30%

---

# 개요: 구현 [!DNL Target] 클라이언트측 웹용

클라이언트측 [!DNL Adobe Target]의 구현에서 [!DNL Target]은 활동과 연관된 경험을 클라이언트 브라우저에 직접 전달합니다. 브라우저는 표시할 경험을 결정하고 표시합니다. 클라이언트측 구현에서는 WYSIWYG 편집기, [시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC) 또는 [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)인 비시각적 인터페이스를 사용하여 활동 및 개인화 경험을 만들 수 있습니다.

구현하려면 [!DNL Target] 클라이언트측에서는 다음 JavaScript 라이브러리 중 하나를 사용해야 합니다.

* [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk.md)

  다음 [!UICONTROL Adobe Experience Platform 웹 SDK] 에서 다양한 서비스와 상호 작용할 수 있습니다. [!DNL Adobe Experience Cloud] (포함) [!DNL Target])을 통해 [!UICONTROL Adobe Experience Edge Network]. 로 마이그레이션하고자 하는 경우 [!UICONTROL Adobe Experience Platform 웹 SDK], 참조 [이란? [!UICONTROL Adobe Experience Platform 웹 SDK]](/help/dev/implement/client-side/aep-web-sdk.md).

* [[!DNL Target] at.js JavaScript 라이브러리](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md)

  at.js JavaScript 라이브러리는 웹 구현에 대한 페이지 로드 시간을 향상시키고, 보안을 강화하고, 단일 페이지 애플리케이션에 대해 더 나은 구현 옵션을 제공합니다. at.js로 마이그레이션하도록 선택하는 경우 다음을 참조하십시오. [At.js 작동 방식](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) 및 [[!DNL Adobe Target] 스킬 빌더: 개발자 채팅, Adobe Target의 mbox.js를 at.js로 마이그레이션](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true).
