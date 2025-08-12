---
title: Experience Platform Web SDK의 A4T 데이터에 대한 서버측 로깅
description: Experience Platform Web SDK을 사용하여 Adobe Analytics for Target(A4T)에 대한 서버측 로깅을 활성화하는 방법을 알아봅니다.
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;웹;sdk;플랫폼;로깅;
feature: Implementation
source-git-commit: b1b0424bfe61fb8b4e88723e6bb2c565d75f8351
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 1%

---

# [!DNL Experience Platform Web SDK]의 A4T 데이터에 대한 서버측 로깅

[!DNL Adobe Experience Platform Web SDK]을(를) 사용하면 [!UICONTROL Adobe Analytics for Target]에서 [!UICONTROL Experience Platform Edge Network]&#x200B;(A4T) 기능을 구현할 수 있습니다. 서버측 로깅이 활성화되면 Edge Network을 통해 전송된 모든 [!DNL Analytics] 히트는 히트 결합 프로세스를 거치지 않고 서버측에서 [!DNL Target] 세부 정보로 보강됩니다.

데이터 스트림 구성에서 [!DNL Analytics]을(를) 사용하도록 설정한 경우 [!DNL Analytics]에 대한 서버측 로깅이 사용하도록 설정됩니다.

![Analytics 데이터 스트림 구성 사용](/help/dev/implement/a4t/assets/enable-analytics-datastream.png)

다음 다이어그램은 서버측 [!DNL Analytics] 로깅이 활성화된 경우 데이터가 시스템을 통해 어떻게 이동하는지를 보여 줍니다.

![서버측 로깅 흐름](/help/dev/implement/a4t/assets/analytics-server-side-logging.png)

## 다음 단계

이 안내서에서는 웹 SDK의 A4T 데이터에 대한 서버측 로깅을 다룹니다. 클라이언트측에서 A4T 데이터를 처리하는 방법에 대한 자세한 내용은 [클라이언트측 로깅](/help/dev/implement/a4t/client-side-logging.md)에 대한 안내서를 참조하십시오.