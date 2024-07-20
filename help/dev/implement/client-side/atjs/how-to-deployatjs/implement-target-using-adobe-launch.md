---
keywords: 구현, 구현, 구현, adobe launch, launch, 경쟁, 리디렉션, 경험 platform launch, platform launch, 태그, adobe platform, 구현2
description: Target을 구현하는 기본 방법인  [!DNL Adobe Experience Platform]을(를) 사용하여  [!DNL Adobe Target] at.js 라이브러리를 구현하는 방법을 알아봅니다.
title: ' [!DNL Adobe Experience Platform]을(를) 사용하여  [!DNL Target] 을(를) 구현하려면 어떻게 합니까?'
feature: Implement Server-side
exl-id: 0a325871-194a-479c-a3bf-294e3dde3e9a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 4%

---

# [!DNL Adobe Experience Platform]을(를) 사용하여 [!DNL Target] 구현

[!DNL Adobe Experience Platform]의 태그는 [!DNL Adobe]의 차세대 태그 관리 기능입니다. 태그는 관련 고객 환경을 향상하는 데 필요한 분석, 마케팅 및 광고 태그를 배포하고 관리하는 간단한 방법을 고객에게 제공합니다.

>[!NOTE]
>
>Adobe Experience Platform Launch이 [!DNL Adobe Experience Platform]에서 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?)를 참조하십시오.

다음 표에는 자세한 정보를 얻을 수 있는 다양한 소스가 나열되어 있습니다.

| 리소스 | 세부 사항 |
|--- |--- |
| [Adobe Target 추가](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/target.html#implement-solutions) | 이 자습서에서는 [!DNL Adobe Experience Platform]의 태그를 사용하여 웹 사이트에서 [!DNL Target]을(를) 구현하는 단계별 지침을 제공합니다. 다뤄지는 주제에는 at.js JavaScript 라이브러리 추가, 글로벌 mbox 실행, 매개 변수 추가 및 다른 솔루션과의 통합이 있습니다. 이 문서는 Adobe Experience Platform 및 기타 Adobe Experience Cloud 솔루션을 구현하는 방법을 보여 주는 대규모 자습서의 일부입니다. |
| [빠른 시작 안내서](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html) | 관련 고객 환경을 향상하는 데 필요한 분석, 마케팅 및 광고 태그를 배포하고 관리하는 방법에 대한 정보입니다. |
| [Adobe [!DNL Target] 확장 개요](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html) | [!DNL Adobe Experience Platform]을(를) 사용하여 [!DNL Target]을(를) 구현하는 방법에 대한 정보입니다. |

## [!DNL Target] 확장을 사용하여 at.js를 구현하는 이점

다음 장점은 [!DNL Adobe Experience Platform]의 태그를 사용하여 at.js를 구현하는 경우에만 적용됩니다. 따라서 Adobe은 at.js를 수동으로 구현하는 대신 [!DNL Adobe Experience Platform]에서 태그를 사용할 것을 강력히 권장합니다.

* **경합 조건 [!DNL Adobe Analytics] 및 [!DNL Target]을(를) 해결합니다.** [!DNL Analytics] 호출이 [!DNL Target] 호출 전에 실행될 수 있으므로 [!DNL Target] 호출은 [!DNL Analytics] 호출에 연결되지 않습니다. 이러한 시퀀싱은 잘못된 데이터를 초래할 수 있습니다. [!DNL Target] 확장 프로그램을 사용하면 [!DNL Target] 호출이 완료되거나 완료될 때까지 [!DNL Analytics] 비콘 호출이 대기합니다. [!DNL Adobe Experience Platform]에서 태그를 사용하면 수동으로 구현할 때 발생할 수 있는 데이터 불일치가 해결됩니다.

  >[!NOTE]
  >
  >[!DNL Analytics] 호출이 [!DNL Target] 호출을 대기하도록 [!DNL Adobe Analytics] 확장에서 비콘 보내기 작업을 사용하십시오. 사용자 지정 코드를 사용하여 `s.t()` 또는 `s.tl()`을(를) 직접 호출하는 경우 [!DNL Analytics] 호출은 [!DNL Target] 호출이 완료될 때까지 기다리지 않습니다.

* **잘못된 리디렉션 오퍼 처리 방지:** 페이지에 [!DNL Target] 및 [!DNL Analytics]이(가) 있고 Target에 의해 리디렉션 오퍼가 실행된 경우, [!DNL Analytics] 추적기가 요청을 실행하지 말아야 할 때 요청을 실행하는 상황이 발생할 수 있습니다(사용자가 다른 URL로 리디렉션되기 때문). [!DNL Adobe Experience Platform]의 태그를 통해 [!DNL Target] 및 [!DNL Analytics]을(를) 구현하면 이 문제가 발생하지 않습니다. [!DNL Adobe Experience Platform]에서 태그를 사용하면 [!DNL Target]은(는) [!DNL Analytics]에게 [!DNL Analytics] 비콘 요청을 중단하도록 지시합니다.
