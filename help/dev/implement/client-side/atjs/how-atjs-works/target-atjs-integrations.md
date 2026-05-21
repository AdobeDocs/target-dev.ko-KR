---
keywords: at.js 통합, 지원되는 통합, 지원되지 않는 통합, 타사 통합
description: '[!UICONTROL Analytics for Target]​(A4T), [!UICONTROL Experience Cloud ID Service] 등을 포함하여  [!DNL Adobe Target] at.js에서 지원하는(그리고 지원되지 않는) 통합을 참조하십시오.'
title: at.js는 어떤 통합을 지원합니까?
feature: at.js
exl-id: d2c61e77-5fc7-4c35-905b-76b8c4f9df4b
TQID: https://experienceleague.adobe.com/RdcxcIGufo2O5aKPqIAJVINkCzZ1Brcv8EXiX1n4buc
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ceid: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2: id: df62f171-ac37-440f-8f0f-f41a72ebdd34id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: e0eb8757-182f-49f3-94a4-1587d16f5094id: e6ff21d3-dec6-4298-8590-7c749fffaf78id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 486
ht-degree: 56%

---

# at.js 통합

[!DNL Adobe Target]과의 통합과 at.js 관련 지원 상태에 대한 정보입니다.

여기에서 지원되지 않거나 언급되지 않은 통합에 대한 강력한 요구가 있는 경우에는 계정 담당자 또는 컨설턴트에게 문의하십시오.

## 지원되는 통합

| 통합 | 세부 사항 |
|--- |--- |
| [!UICONTROL Analytics for Target]&#x200B;(A4T) | [Adobe Target용 보고 소스로서의 Adobe Analytics (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)를 참조하십시오. |
| [!UICONTROL Profiles & Audiences]&#x200B;(P&amp;A) | *핵심 서비스 사용 안내서*&#x200B;에서 [대상](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html?lang=ko-KR)을 참조하세요. |
| [!UICONTROL Experience Cloud ID Service] | [Adobe Experience Cloud ID 서비스 설명서](https://experienceleague.adobe.com/docs/id-service/using/home.html)를 참조하십시오. |
| [!UICONTROL Tags in Adobe Experience Platform] | [!UICONTROL Tags in Adobe Experience Platform]은(는) [!DNL Adobe]의 차세대 태그 관리 기능입니다. [!UICONTROL Tags]은(는) 관련 고객 환경을 향상시키는 데 필요한 분석, 마케팅 및 광고 태그를 배포하고 관리하는 간단한 방법을 고객에게 제공합니다. [구현 [!DNL Target] Adobe Experience Platform 사용](../how-to-deployatjs/implement-target-using-adobe-launch.md)을 참조하십시오. |
| [!UICONTROL Adobe Experience Manager]&#x200B;(AEM) Cloud Service | [!UICONTROL AEM Cloud Service]을(를) 사용하면 AEM 워크플로 내에서 [!UICONTROL A/B Test] 및 [!UICONTROL Experience Targeting] 활동을 만들 수 있습니다. FP-11577 이상을 사용하는 [!UICONTROL Adobe Experience Manager] 6.2에서 at.js를 지원합니다. 자세한 내용은 [통합 [!DNL Adobe Target]](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html)을 참조하고 AEM 버전을 선택하세요. |
| [!UICONTROL AEM Experience Fragments] | [!DNL Target] 활동의 AEM에서 만든 경험 조각을 사용하면 AEM의 편의성과 기능을 [!DNL Target]의 강력한 AI(Automated Intelligence) 및 기계 학습(ML) 기능을 결합하여 경험을 다양한 규모로 테스트 및 개인화할 수 있습니다.  AEM에서는 모든 콘텐츠 및 에셋을 중앙 위치에 가져와서 개인화 전략을 실행합니다. AEM을 사용하면 코드를 작성하지 않고도 한 위치에서 데스크탑, 태블릿 및 휴대 디바이스의 콘텐츠를 쉽게 만들 수 있습니다. 모든 장치를 위해 페이지를 만들 필요가 없이, 콘텐츠를 사용하여 각 경험이 자동으로 조정됩니다.  [AEM 경험 구성요소](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html)를 참조하십시오. |

## 지원되지 않는 통합

| 통합 | 세부 사항 |
|--- |--- |
| [!DNL Target]에서 [!DNL SiteCatalyst]&#x200B;(으)로의 통합 | [!DNL SiteCatalyst] UI에서 보고를 수행할 수 있도록 페이지 호출을 통해 캠페인 및 레서피 ID를 [!DNL SiteCatalyst]에 전송하는 통합입니다. 이 기능은 A4T로 대체되었습니다. |
| [!DNL Target]에서 [!DNL SiteCatalyst]&#x200B;(으)로의 통합 | evar 및 prop를 기반으로 성공 지표와 사용자 프로필을 빌드할 수 있도록 `"SiteCatalyst: Event"` 및 `"SiteCatalyst: Purchase"`라는 mbox 호출을 수행하는 통합입니다. 이 기능은 A4T 및 P&amp;A로 대체되었습니다. |
| 기존 [!DNL Audience Manager]&#x200B;(AAM)에서 [!DNL Target] 통합으로 | 프런트엔드 API 호출을 수행하여 AAM 세그먼트를 검색한 다음, 이 세그먼트들을 페이지의 모든 mbox 호출에서 mbox 매개 변수로서 전송하는 통합입니다. |

## 타사 통합

| 통합 | 세부 사항 |
|--- |--- |
| 기타 태그 관리자 | at.js는 비Adobe 태그 관리 플랫폼에서 작동해야 하지만 다른 공급업체가 개발한 사용자 지정 통합 기능을 사용하는 데에는 주의하십시오. 더 이상 at.js에 없는 내부 mbox.js 함수에 공급업체의 통합이 종속될 수 있습니다. |
| 타사 데이터 제공자(예: Demandbase, Bluekai, 날씨 API) | Target의 사용자 프로파일링을 보완하는 데 사용되는 다양한 타사 데이터 공급업체는 at.js [데이터 제공자](../atjs-functions/targetglobalsettings.md#data-providers) 기능을 사용하여 통합할 수 있습니다. |
