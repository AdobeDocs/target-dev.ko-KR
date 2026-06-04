---
title: Experience Platform Web SDK에서 A4T(Adobe Analytics for Target) 로그인
description: Experience Platform Web SDK을 사용하여 A4T(Adobe Analytics for Target) 데이터 수집을 제어하는 방법에 대해 알아봅니다.
seo-title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;로깅;analytics;sdk;web sdk;
feature: Implementation
exl-id: 886588bf-4416-4f1e-aecc-467e48c8fb23
TQID: https://experienceleague.adobe.com/cShqvj3wSialxA-ajnROnIpzjuz66pNg3CLM6l2xPLg
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: a94ced60-8199-4549-b453-ede2acb4101e
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 265
ht-degree: 1%

---

# [!DNL Experience Platform Web SDK]에서 [!DNL Adobe Analytics for Target]&#x200B;(A4T) 로깅

개인화에 [!DNL Adobe Target]을(를) 사용하는 경우 성과 측정에 사용할 시스템을 선택할 수 있습니다. 각 [Target 활동](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html)을 통해 [!DNL Target] 보고와 Adobe [!DNL Analytics] 보고 중에서 선택할 수 있습니다.

[!DNL Analytics] 보고를 사용하는 경우 [!DNL Target]이(가) [!DNL Analytics]에게 다음 내용을 전달해야 합니다.

* 방문자가 입력한 [!DNL Target]개 활동
* 어떤 경험을 보았습니까
* 전환에 도달함

[!DNL Adobe Experience Platform Web SDK]은(는) [!UICONTROL Analytics for Target]&#x200B;(A4T) 사용 사례에 대해 두 가지 유형의 [!DNL Analytics] 로깅을 지원합니다.

| 로깅 방법 | 설명 |
| --- | --- |
| 서버측 [!DNL Analytics] 로깅 | Edge Network을 통해 전송된 모든 [!DNL Analytics]개의 히트는 히트 결합 프로세스를 거치지 않고도 서버측에서 [!DNL Target]개의 세부 정보로 보강됩니다. |
| 클라이언트측 [!DNL Analytics] 로깅 | [!DNL Target] 데이터가 클라이언트측에서 반환되므로 [데이터 삽입 API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html)를 사용하여 데이터를 수동으로 늘리고 [!DNL Analytics]에 보낼 수 있습니다. |

로깅 메서드는 구성된 [데이터스트림](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview)에서 [!DNL Adobe Analytics]을(를) 사용하는지 여부에 따라 결정됩니다.

![로깅 방법 결정 흐름](/help/dev/implement/a4t/assets/analytics-logging.png)

## 다음 단계

이 문서에서는 웹 SDK의 A4T 데이터에 대한 다양한 로깅 방법에 대해 간략하게 소개했습니다. 이러한 각 방법에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [Experience Platform Web SDK의 A4T 데이터에 대한 서버측 로깅](/help/dev/implement/a4t/client-side-logging.md)
* [Experience Platform Web SDK의 A4T 데이터에 대한 클라이언트측 로깅](/help/dev/implement/a4t/client-side-logging.md)
