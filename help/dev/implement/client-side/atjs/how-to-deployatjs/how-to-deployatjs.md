---
keywords: 구현, at.js, Javascript 라이브러리
description: ' [!DNL Adobe Experience Platform] 의 태그를 사용하거나 태그 관리자 없이  [!DNL Adobe Target]  at.js JavaScript 라이브러리를 배포하는 방법에 대해 알아봅니다.'
title: at.js를 배포하는 방법은 무엇입니까?
feature: Implement Server-side
exl-id: e62cb27e-ea80-462b-90f8-0a033b128031
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 10%

---

# at.js를 배포하는 방법

[!DNL Adobe Experience Platform]의 태그를 사용하거나 태그 관리자 없이 [!DNL Adobe Target] JavaScript 라이브러리 at.js를 배포하는 방법에 대한 정보입니다.

다음 방법을 사용하여 at.js를 배포할 수 있습니다.

* **[Adobe Experience Platform에서 태그를 사용 [!DNL Target] 구현](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)**: [!DNL Adobe Experience Platform]의 태그는 Adobe의 차세대 태그 관리 기능입니다. 태그는 관련 고객 환경을 향상하는 데 필요한 분석, 마케팅 및 광고 태그를 배포하고 관리하는 간단한 방법을 고객에게 제공합니다.

>[!NOTE]
>
> [!DNL Adobe Experience Platform Launch] 가 [!DNL Adobe Experience Platform]의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=ko)를 참조하십시오.

* **[태그 관리자 없이  [!DNL Target] 구현](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)**: 태그 관리자(예: [!DNL Adobe Experience Platform]의 태그)를 사용하지 않고 [!DNL Target]을(를) 구현할 수 있습니다.
* **타사 태그 관리자를 사용하여 [!DNL Target]을(를) 구현**: [Adobe Experience Platform의 태그](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)는 [!DNL Target]을(를) 구현하는 기본 방법입니다. 그러나 Tealium, Ensighten 및 Google 태그를 포함한 타사 태그 관리자를 사용하여 [!DNL Target]을(를) 구현할 수도 있습니다. Launch를 사용할 때의 이점 목록을 보려면 [확장을 사용하여 at.js를 구현할 때의 이점](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md#advantages-of-implementing-atjs-using-the-target-extension)을 참조하십시오. [!DNL Adobe Target] 

  그러나 태그 관리자 없이 [!DNL Target]을(를) 구현하는 방법을 알고 있으면 사이트 코드에서 at.js를 하드 코딩하는 대신 타사 태그 관리자를 사용하여 쉽게 구현할 수 있습니다.

  타사 태그 관리자를 사용하여 [!DNL Target]을(를) 구현하는 데 도움이 되는 두 가지 관련 항목은 다음과 같습니다.

   * [구현하기 전에](/help/dev/before-implement/prepare-to-implement-target.md)
   * [태그 관리자 없이  [!DNL Target] 구현](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

  자세한 내용은 타사 태그 관리자 설명서를 참조하십시오.

SPA(단일 페이지 앱)을 사용할 때 [!DNL Target]을(를) 구현하려면 [단일 페이지 애플리케이션 구현](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)을 참조하십시오.
