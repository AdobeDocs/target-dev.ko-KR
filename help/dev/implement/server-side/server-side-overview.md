---
keywords: server side, 서버측, api, sdk, node.js, nodejs, node js, recommendations api, api, api, server side1
description: 에 대해 알아보기 [!DNL Adobe Target] 서버 측 배달 API, SDK 및 [!DNL Target Recommendations] API.
title: 어디에서 배울 수 있습니까 [!DNL Target] 서버 측 배달 API 및 SDK?
feature: Implement Server-side
exl-id: 3eb0a789-cf1a-4d02-acf7-3c895bcb662f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 14%

---

# 서버 측: 구현 [!DNL Target]

다음에 대한 정보: [!DNL Adobe Target] 서버 측 배달 API, SDK 및 [!DNL Target Recommendations] API.

다음 프로세스는 [!DNL Target]의 서버 측 구현 시 발생합니다.

1. 클라이언트 장치는 서버를 통해 경험을 요청합니다.
1. 서버가 해당 요청을 [!DNL Target]에 전송합니다.
1. [!DNL Target]에서 응답을 다시 서버로 전송합니다.
1. 서버는 렌더링하기 위해 클라이언트 장치에 전달할 경험을 결정합니다.

경험이 브라우저에 표시되지 않아도 됩니다. 경험은 음성 도우미를 통해 또는 시각적이지 않은 경험 또는 브라우저를 기반으로 하지 않는 디바이스를 통해 이메일이나 키오스크에 표시될 수 있습니다. 서버가 클라이언트와 [!DNL Target] 사이에 존재하기 때문에 제어력과 보안이 필요하거나 서버에서 실행하려는 복잡한 백엔드 프로세스가 있는 경우에 이러한 유형의 구현이 이상적입니다.

>[!NOTE]
>
>처음 방문자는 클라이언트측에서만 초기화할 수 있습니다. 처음 방문자 *할 수 없음* 서버측에서 초기화됩니다. 이는 서드파티 demdex 쿠키에 따라 달라지는 ECID로 인해 발생하며, 따라서 브라우저가 포함된 구현에서 Visitor API.js를 통해 초기화해야 합니다.

다음 섹션은 다양한 서버측 API 및 SDK에 대한 자세한 정보를 제공합니다.

## 서버 측 배달 API

링크: [서버 측 배달 API](/help/dev/implement/delivery-api/overview.md)

`/rest/v1/delivery`

다음을 통해 [!DNL Target] 배달 API를 사용하여 다음과 같은 작업을 수행할 수 있습니다.

* SPA 및 모바일 채널을 비롯한 웹과 연결된 TV, 키오스크 또는 매장 내 디지털 화면과 같은 비브라우저 기반 IoT 장치 전반에 경험을 제공합니다.
* HTTP/s를 호출할 수 있는 모든 서버측 플랫폼 또는 애플리케이션에서 경험을 제공합니다.
* 방문자가 비즈니스에 참여하는 데 사용한 채널 또는 장치에 관계없이 방문자에게 일관되고 개인화된 경험을 제공합니다.
* 서버의 세션 내에 방문자를 위한 경험을 캐시하므로 여러 API 호출을 방지할 수 있으므로 성능이 향상됩니다.
* Adobe Analytics, Adobe Audience Manager(AAM) 및 서버측 Experience Cloud ID 서비스와 같은 Adobe Experience Cloud 제품과 원활하게 통합됩니다.

## 서버측 SDK

다음 [!DNL Adobe Target] 서버측 SDK 설명서는 을 구현하는 데 도움이 됩니다 [!DNL Target] 원하는 언어로 서버에 게시할 수 있습니다.

* [Node.js](node-js/overview.md)
* [Java](java/overview.md)
* [.NET](net/overview.md)
* [Python](python/overview.md)

까지 [!DNL Adobe Target]의 서버측 SDK를 사용하여 다음을 수행할 수 있습니다.

* 실행 및 실행 **기능 플래그 지정**, **롤아웃**, 및 **A/B 실험** 위치: **거의 0에 가까운 지연**.
* 경험 전달 **웹**, 포함 **SPA**, 및 **모바일 채널**, 및 비브라우저 기반 **사물 인터넷(IoT) 장치** 연결된 TV, 키오스크 또는 매장 내 디지털 화면 등.
* 제공 **ML(머신 러닝) 기반의 개인화된 경험** 사용자가 귀하의 비즈니스와 어떤 채널 또는 장치를 사용하는지에 관계없이 사용자에게 전달됩니다.
* **Adobe Experience Cloud과 원활하게 통합** 제품: **Adobe Analytics**, **Adobe Audience Manager**&#x200B;및 **Experience Cloud ID 서비스** 서버측에서 가져온 것입니다.

다음을 참조하십시오. [시작](sdk-guides/getting-started/getting-started.md) 를 통해 간단한 기능 플래그 지정 사용 사례를 실행하는 방법을 알아보는 페이지 [온디바이스 의사 결정](sdk-guides/on-device-decisioning/overview.md).

다음을 확인하십시오. [샘플 앱](sdk-guides/sample-apps/sample-apps.md) 재미있게 놀고 놀기 위해서!

## [!DNL Target Recommendations] API

링크: [RECOMMENDATIONS API TARGET](https://developers.adobetarget.com/api/recommendations) 및 [Adobe Recommendations API 개요](../../before-administer/recs-api/overview.md).

Recommendations API를 사용하면 프로그래밍 방식으로 와 상호 작용할 수 있습니다 [!DNL Target] recommendations 서버입니다. 이러한 API는 일반적으로 를 통해 이루어지는 기능을 수행하기 위해 애플리케이션 스택의 범위와 통합될 수 있습니다. [!DNL Target] 사용자 인터페이스.
