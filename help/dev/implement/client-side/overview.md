---
keywords: 구현, 구현, at.js, adobe experience platform web sdk, aep web sdk
description: ' [!DNL Adobe Target] (AEP Web SDK) 또는 at.js JavaScript 라이브러리를 사용하여 클라이언트측 웹용  [!DNL Adobe Experience Platform Web SDK] 을(를) 구현하는 방법에 대해 알아봅니다.'
title: 클라이언트측 웹용  [!DNL Target] 을(를) 구현하는 방법
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
source-git-commit: 7e2f1620c839393051432485192a45ddda2390a0
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 28%

---

# 개요: 클라이언트측 웹용 [!DNL Target] 구현

클라이언트측 [!DNL Adobe Target]의 구현에서 [!DNL Target]은 활동과 연관된 경험을 클라이언트 브라우저에 직접 전달합니다. 브라우저는 표시할 경험을 결정하고 표시합니다. 클라이언트측 구현에서는 WYSIWYG 편집기, [시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=ko) (VEC) 또는 [양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=ko)인 비시각적 인터페이스를 사용하여 활동 및 개인화 경험을 만들 수 있습니다.

[!DNL Target] 클라이언트측을 구현하려면 다음 JavaScript 라이브러리 중 하나를 사용해야 합니다.

* [Adobe Experience Platform 웹 SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)

  [!UICONTROL Adobe Experience Platform Web SDK]을(를) 사용하면 [!DNL Adobe Experience Cloud]을(를) 통해 [!DNL Target]&#x200B;([!UICONTROL Adobe Experience Edge Network] 포함)의 다양한 서비스와 상호 작용할 수 있습니다. [!UICONTROL Adobe Experience Platform Web SDK]&#x200B;(으)로 마이그레이션하려면 [내용 [!UICONTROL Adobe Experience Platform Web SDK]](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)을(를) 참조하십시오.

* [[!DNL Target] at.js JavaScript 라이브러리](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)

  at.js JavaScript 라이브러리는 웹 구현에 대한 페이지 로드 시간을 향상시키고, 보안을 강화하고, 단일 페이지 애플리케이션에 대해 더 나은 구현 옵션을 제공합니다. at.js로 마이그레이션하도록 선택한 경우 [At.js 작동 방식](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) 및 [[!DNL Adobe Target] 스킬 빌더: 개발자 채팅, Adobe Target의 mbox.js를 at.js로 마이그레이션](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true)을 참조하십시오.


두 구현 접근 방식의 차이점에 대해 알아보려면 [at.js 라이브러리와 웹 SDK 비교](/help/dev/implement/client-side/aep-web-sdk/web-sdk-atjs-comparison.md)를 참조하십시오.