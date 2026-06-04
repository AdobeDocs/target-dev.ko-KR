---
title: Adobe Target 게재 API 개요
description: Adobe Target 게재 API 개요
keywords: 배달 api
exl-id: e760bddc-b1ae-4b7b-bff2-aba81c6b6d34
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/gPXGax6ccvZZPklT3jnZbqyOj3mCClEfSpdufAFPtSs
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 188
ht-degree: 0%

---

# 게재 API 개요

[!DNL Adobe Target Delivery API]은(는) REST를 기반으로 합니다. 이 설명서에서는 [!DNL Adobe Target] [!DNL Delivery API]을(를) 구성하는 리소스에 대해 설명합니다. HTTP 메서드는 이러한 리소스에서 작업을 실행하는 데 사용됩니다.

[!UICONTROL Adobe Target의 배달 API]를 사용하여 다음을 수행할 수 있습니다.

* 연결된 TV, 키오스크 또는 매장 내 디지털 화면과 같은 비브라우저 기반 IoT 장치뿐만 아니라 SPA 및 모바일 채널을 포함하여 웹에서 경험을 제공합니다.
* HTTP/s를 호출할 수 있는 모든 서버측 플랫폼 또는 애플리케이션에서 경험을 제공합니다.
* 사용자가 귀하의 비즈니스에 관여한 채널 또는 장치에 관계없이 일관되고 개인화된 경험을 사용자에게 제공합니다.
* 서버의 세션 내에서 사용자에 대한 경험을 캐시하므로 여러 API 호출을 방지하고 결과적으로 더 나은 성능을 얻을 수 있습니다.
* 서버측에서 [!DNL Adobe Analytics], [!DNL Adobe Audience Manager] 및 [!DNL Experience Cloud ID Service]과(와) 같은 [!DNL Adobe Experience Cloud] 제품과 원활하게 통합됩니다.

>[!NOTE]
>
>[레거시 /v1/mbox 및 /v2/batchmbox API 설명서](https://developers.adobetarget.com/api/legacy-api/index.html)에 액세스할 수 있습니다. 그러나 게재 API에서는 기능이 개발되어 기존 API로 백포팅되지 않습니다(여기에 설명됨).
