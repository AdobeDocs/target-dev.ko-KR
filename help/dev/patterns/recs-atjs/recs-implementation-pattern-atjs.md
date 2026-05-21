---
title: at.js를 사용한 권장 사항 구현 패턴
description: at.js를 사용하는 Recommendations에 대한 구현 패턴을 사용하는 방법을 이해합니다
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: d568cd1d-acc3-42e0-ae2c-5787e6f361f8
TQID: https://experienceleague.adobe.com/uYNa5mL-8ffPS-ddjnQzILnPFMbjNJqKZDmQT8qFeGA
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c4147b6e-073b-4d3c-9ab1-d60f2f4434efid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 152
ht-degree: 0%

---

# at.js 개요를 사용하는 [!DNL Recommendations] 구현 패턴

이 구현 패턴은 [at.js JavaScript 라이브러리](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)를 사용할 때 [!DNL Adobe Target Recommendations] 구현을 이해하고 만드는 데 도움이 됩니다.

이미지를 클릭하여 전체 화면으로 확장합니다.

![Adobe Target 아키텍처 다이어그램](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

이미지의 숫자는 작업 순서를 나타내지 않습니다.

1. [!DNL Adobe Target] 및 [!DNL Experience Cloud ID Service]용 클라이언트측 SDK
1. [!DNL Target Delivery API] 통화
1. [!UICONTROL Experience Cloud ID]&#x200B;(ECID) 획득 호출
1. 벌크 프로필 업데이트 API 및 [!DNL Customer Attributes]&#x200B;(CA) 서비스
1. 고객의 데이터 소스에서 [!DNL Target] 프로필 스토어로 프로필 데이터 수집
1. 프로필 및 행동 데이터 수집 및 방문자에게 표시할 경험 결정
1. 페이지에서 렌더링되는 경험
1. at.js는 페이지에서 경험을 렌더링합니다

각 패턴은 서로 다른 부분으로 구성되어 있으며 각 부분은 [!DNL Target] 구현에 대한 중요한 구현 요구 사항에 해당합니다.

각 부분은 이 안내서의 별도 문서에 설명되어 있습니다.

* [SDK 초기화](/help/dev/patterns/recs-atjs/initialize-sdk.md)
* [데이터 수집 구성](/help/dev/patterns/recs-atjs/data-collection.md)
* [경험 렌더링](/help/dev/patterns/recs-atjs/render-experiences.md)
* [타겟에게 알림](/help/dev/patterns/recs-atjs/notify-target.md)
