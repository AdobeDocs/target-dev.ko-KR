---
title: Experience Platform Web SDK에서 A4T(Adobe Analytics for Target) 로그인
description: Experience Platform Web SDK을 사용하여 A4T(Adobe Analytics for Target) 데이터 수집을 제어하는 방법에 대해 알아봅니다.
seo-title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;로깅;analytics;sdk;web sdk;
feature: Implementation
source-git-commit: b7638f7ab3fe9a6551c9d542a990e22ddb2b27a2
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 1%

---

# [!DNL Adobe Analytics for Target]에서 [!DNL Experience Platform Web SDK]&#x200B;(A4T) 로깅

개인화에 [!DNL Adobe Target]을(를) 사용하는 경우 성과 측정에 사용할 시스템을 선택할 수 있습니다. 각 [Target 활동](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=ko)을 통해 [!DNL Target] 보고와 Adobe [!DNL Analytics] 보고 중에서 선택할 수 있습니다.

[!DNL Analytics] 보고를 사용하는 경우 [!DNL Target]이(가) [!DNL Analytics]에게 다음 내용을 전달해야 합니다.

* 방문자가 입력한 [!DNL Target]개 활동
* 어떤 경험을 보았습니까
* 전환에 도달함

[!DNL Adobe Experience Platform Web SDK]은(는) [!DNL Analytics]&#x200B;(A4T) 사용 사례에 대해 두 가지 유형의 [!UICONTROL Analytics for Target] 로깅을 지원합니다.

| 로깅 방법 | 설명 |
| --- | --- |
| 서버측 [!DNL Analytics] 로깅 | Edge Network을 통해 전송된 모든 [!DNL Analytics]개의 히트는 히트 결합 프로세스를 거치지 않고도 서버측에서 [!DNL Target]개의 세부 정보로 보강됩니다. |
| 클라이언트측 [!DNL Analytics] 로깅 | [!DNL Target] 데이터가 클라이언트측에서 반환되므로 [!DNL Analytics]데이터 삽입 API[를 사용하여 데이터를 수동으로 늘리고 &#x200B;](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html?lang=ko)에 보낼 수 있습니다. |

로깅 메서드는 구성된 [!DNL Adobe Analytics]데이터스트림[에서 &#x200B;](https://experienceleague.adobe.com/ko/docs/experience-platform/datastreams/overview)을(를) 사용하는지 여부에 따라 결정됩니다.

![로깅 방법 결정 흐름](/help/dev/implement/a4t/assets/analytics-logging.png)

## 다음 단계

이 문서에서는 웹 SDK의 A4T 데이터에 대한 다양한 로깅 방법에 대해 간략하게 소개했습니다. 이러한 각 방법에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [Experience Platform Web SDK의 A4T 데이터에 대한 서버측 로깅](/help/dev/implement/a4t/client-side-logging.md)
* [Experience Platform Web SDK의 A4T 데이터에 대한 클라이언트측 로깅](/help/dev/implement/a4t/client-side-logging.md)