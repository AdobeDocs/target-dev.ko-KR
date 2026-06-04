---
title: Experience Platform Web SDK의 A4T 데이터에 대한 서버측 로깅
description: Experience Platform Web SDK을 사용하여 Adobe Analytics for Target(A4T)에 대한 서버측 로깅을 활성화하는 방법을 알아봅니다.
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;웹;sdk;플랫폼;로깅;
feature: Implementation
exl-id: 716f7343-69a6-44d7-baec-a0a0df1b6e1f
TQID: https://experienceleague.adobe.com/I7-G2VO2AN3qFsgkk4JX2Pg6WJfZq0HZkcGL4XQNoWg
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 161
ht-degree: 1%

---

# [!DNL Experience Platform Web SDK]의 A4T 데이터에 대한 서버측 로깅

[!DNL Adobe Experience Platform Web SDK]을(를) 사용하면 [!UICONTROL Experience Platform Edge Network]에서 [!UICONTROL Target용 Adobe Analytics]&#x200B;(A4T) 기능을 구현할 수 있습니다. 서버측 로깅이 활성화되면 Edge Network을 통해 전송된 모든 [!DNL Analytics] 히트는 히트 결합 프로세스를 거치지 않고 서버측에서 [!DNL Target] 세부 정보로 보강됩니다.

데이터 스트림 구성에서 [!DNL Analytics]을(를) 사용하도록 설정한 경우 [!DNL Analytics]에 대한 서버측 로깅이 사용하도록 설정됩니다.

![Analytics 데이터 스트림 구성 사용](/help/dev/implement/a4t/assets/enable-analytics-datastream.png)

다음 다이어그램은 서버측 [!DNL Analytics] 로깅이 활성화된 경우 데이터가 시스템을 통해 어떻게 이동하는지를 보여 줍니다.

![서버측 로깅 흐름](/help/dev/implement/a4t/assets/analytics-server-side-logging.png)

## 다음 단계

이 안내서에서는 웹 SDK의 A4T 데이터에 대한 서버측 로깅을 다룹니다. 클라이언트측에서 A4T 데이터를 처리하는 방법에 대한 자세한 내용은 [클라이언트측 로깅](/help/dev/implement/a4t/client-side-logging.md)에 대한 안내서를 참조하십시오.
