---
title: 프로필 업데이트
description: Adobe Target 프로필 API를 사용하여 방문자 데이터를  [!DNL Target](으)로 보내는 방법을 알아봅니다.
contributors: https://github.com/icaraps
exl-id: 482a4175-1d02-47e9-a5c0-dd00e8560773
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/jclCuF4pe3JwAN-2RhQ9NfA5KtEfKUuawlmrE3aS0bQ
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 217
ht-degree: 1%

---

# 프로필 업데이트

사용자 프로필에는 연령, 성별, 구매한 제품, 마지막으로 방문한 시간 등과 같은 웹 페이지 방문자의 인구 통계학적 및 행동 정보가 포함되어 있습니다. [!DNL Adobe Target]은(는) 이 정보를 사용하여 각 방문자에게 제공하는 콘텐츠를 개인화합니다.

각 방문자에 대한 프로필 정보는 쿠키 또는 서드파티 앱에 저장됩니다.

웹 페이지에서 [!DNL Target] 코드([at.js](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md) 또는 [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md))를 구현하는 경우 쿠키의 프로필 정보가 프로필 매개 변수를 사용하여 [!DNL Target]에 전달됩니다. [!DNL Target]은(는) 방문자의 쿠키에서 생성한 `pcID`을(를) 통해 각 방문자를 고유하게 식별합니다. 그러나 `mbox3rdPartyIds`을(를) 사용하여 mbox 호출을 통해 외부 앱의 프로필 매개 변수를 전달할 수 있습니다.

[!DNL Target]과의 페이지 기반 통합의 일부로 보낼 수 없거나 보내지 않으려는 [!DNL Target]에 보낼 방문자에 대한 프로필 데이터가 있는 경우 [!DNL Adobe Target] 프로필 API를 사용하십시오. 페이지에서 사용할 수 없는 CRM(고객 관계 관리) 또는 POS(판매 지점) 시스템의 데이터일 수 있습니다. 또는 이 데이터가 페이지에서 전달하는 것이 적절하지 않은 보다 민감한 특성일 수 있습니다.

API를 통해 프로필을 업데이트하는 방법에는 두 가지가 있습니다.

* [싱글 프로필 업데이트 API](/help/dev/administer/profile-api/profile-single-api.md)
* [일괄 처리를 통한 벌크 프로필 업데이트](/help/dev/administer/profile-api/profile-bulk-api.md)
