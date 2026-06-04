---
keywords: server side, 서버측, api, sdk, node.js, nodejs, node js, recommendations api, api, api, server side1
description: ' [!DNL Adobe Target] 서버측 배달 API, SDK 및 [!DNL Target Recommendations] API에 대해 알아봅니다.'
title: ' [!DNL Target] 서버측 배달 API 및 SDK에 대한 자세한 내용은 어디에서 확인할 수 있습니까?'
feature: Implement Server-side
exl-id: 3eb0a789-cf1a-4d02-acf7-3c895bcb662f
TQID: https://experienceleague.adobe.com/x5WKb9Eenz2bw-idOnxlpWdtiivTx05n38sNXEt3DNc
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: b050e0cd-2ddd-42cd-a71b-5d9e1fdf75e0id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: a6cc21b9-1a36-4fa6-9c61-4acd04d9c88cid: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2id: d095671a-1355-40aa-8b5f-06c33c68080bid: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 618
ht-degree: 12%

---

# 서버 측: [!DNL Target] 구현

[!DNL Adobe Target]개의 서버측 배달 API, SDK 및 [!DNL Target Recommendations]개의 API에 대한 정보입니다.

>[!NOTE]
>
>구현에서 클라이언트측에서 at.js 및 [!DNL AppMeasurement]을(를) 사용하는 경우 아래에 설명된 [!UICONTROL Target 배달 API] 및 서버측 SDK를 사용해야 합니다.
>
>구현에서 [!UICONTROL Adobe Experience Platform Web SDK]를 사용하는 경우 [[!UICONTROL Adobe Experience Platform] [!UICONTROL Edge Network Server API]](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview){target=_blank}를 사용해야 합니다.

다음 프로세스는 [!DNL Target]의 서버 측 구현 시 발생합니다.

1. 클라이언트 장치는 서버를 통해 경험을 요청합니다.
1. 서버가 해당 요청을 [!DNL Target]에 전송합니다.
1. [!DNL Target]에서 응답을 다시 서버로 전송합니다.
1. 서버는 렌더링하기 위해 클라이언트 장치에 전달할 경험을 결정합니다.

경험이 브라우저에 표시되지 않아도 됩니다. 경험은 음성 도우미를 통해 또는 시각적이지 않은 경험 또는 브라우저를 기반으로 하지 않는 디바이스를 통해 이메일이나 키오스크에 표시될 수 있습니다. 서버가 클라이언트와 [!DNL Target] 사이에 존재하기 때문에 제어력과 보안이 필요하거나 서버에서 실행하려는 복잡한 백엔드 프로세스가 있는 경우에 이러한 유형의 구현이 이상적입니다.

>[!NOTE]
>
>처음 방문자는 클라이언트측에서만 초기화할 수 있습니다. 처음 방문자 *은(는) 서버측에서 초기화할 수*&#x200B;없습니다. 이는 서드파티 demdex 쿠키에 따라 달라지는 ECID로 인해 발생하며, 따라서 브라우저가 포함된 구현에서 Visitor API.js를 통해 초기화해야 합니다.

다음 섹션은 다양한 서버측 API 및 SDK에 대한 자세한 정보를 제공합니다.

## 서버 측 배달 API

링크: [서버 측 배달 API](/help/dev/implement/delivery-api/overview.md)

`/rest/v1/delivery`

[!DNL Target] 배달 API를 통해 다음을 수행할 수 있습니다.

* SPA 및 모바일 채널을 비롯한 웹과 연결된 TV, 키오스크 또는 매장 내 디지털 화면과 같은 비브라우저 기반 IoT 장치 전반에 걸쳐 경험을 제공합니다.
* HTTP/s를 호출할 수 있는 모든 서버측 플랫폼 또는 애플리케이션에서 경험을 제공합니다.
* 방문자가 비즈니스에 참여하는 데 사용한 채널 또는 장치에 관계없이 방문자에게 일관되고 개인화된 경험을 제공합니다.
* 서버의 세션 내에 방문자를 위한 경험을 캐시하므로 여러 API 호출을 방지할 수 있으므로 성능이 향상됩니다.
* 서버측에서 Adobe Analytics, Adobe Audience Manager(AAM) 및 Experience Cloud ID 서비스 와 같은 Adobe Experience Cloud 제품과 원활하게 통합됩니다.

## 서버측 SDK

[!DNL Adobe Target] 서버측 SDK 설명서를 통해 선택한 언어로 서버에 [!DNL Target]을(를) 구현할 수 있습니다.

* [Node.js](node-js/overview.md)
* [Java](java/overview.md)
* [.NET](net/overview.md)
* [Python](python/overview.md)

[!DNL Adobe Target]의 서버측 SDK를 통해 다음을 수행할 수 있습니다.

* **거의 0에 가까운 대기 시간**&#x200B;에 **기능 플래그 지정**, **롤아웃**, **A/B 실험**&#x200B;을 실행하고 실행하십시오.
* **SPA** 및 **모바일 채널**&#x200B;과(와) 연결된 TV, 키오스크 또는 매장 내 디지털 화면과 같은 비브라우저 기반 **사물인터넷(IoT) 장치**&#x200B;를 포함하여 **웹**&#x200B;에서 경험을 전달하십시오.
* 사용자가 귀하의 비즈니스에 참여한 채널 또는 장치에 관계없이 **ML(기계 학습) 기반의 개인화된 경험**&#x200B;을 사용자에게 전달합니다.
* **Adobe Experience Cloud와 원활하게 통합** 서버 측에서 **Adobe Analytics**, **Adobe Audience Manager** 및 **Experience Cloud ID 서비스**&#x200B;와 같은 제품

[디바이스에서 의사 결정](sdk-guides/on-device-decisioning/overview.md)을 통해 간단한 기능 플래그 지정 사용 사례를 실행하는 방법을 알아보려면 [시작하기](sdk-guides/getting-started/getting-started.md) 페이지를 참조하세요.

[샘플 앱](sdk-guides/sample-apps/sample-apps.md)을 확인해 보세요.

## [!DNL Target Recommendations] API

링크: [Target Recommendations API](https://developers.adobetarget.com/api/recommendations) 및 [Adobe Recommendations API 개요](../../before-administer/recs-api/overview.md)

Recommendations API를 사용하면 [!DNL Target] Recommendations 서버와 프로그래밍 방식으로 상호 작용할 수 있습니다. 이러한 API는 일반적으로 [!DNL Target] 사용자 인터페이스를 통해 수행하는 기능을 수행하기 위해 다양한 애플리케이션 스택과 통합될 수 있습니다.
