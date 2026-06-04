---
title: 데이터 수집 구성
description: 데이터 수집에 필요한 모든 작업이 올바른 순서로 실행되는지 확인합니다.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 66e0f18d-c78c-463b-8c47-132ef6332927
TQID: https://experienceleague.adobe.com/fg3xJnwYAVyz-N-xzT5Piu35Ajd2UMEvuTvTQs2wj3c
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 401
ht-degree: 1%

---

# 데이터 수집 구성

*데이터 수집* 다이어그램의 단계에 따라 데이터 수집에 필요한 모든 작업이 올바른 순서로 실행되도록 하십시오.

>[!TIP]
>
>전체 화면으로 확장하려면 이 항목의 이미지를 클릭하십시오.

데이터 레이어는 페이지 로드 중에 준비되거나 페이지 로드 후 데이터 레이어가 변경됩니다.

[SDK 초기화 단계](/help/dev/patterns/recs-atjs/initialize-sdk.md) 동안 이미 데이터를 매핑한 경우 다음 경우에 이 다이어그램의 단계를 실행해야 합니다.

* 데이터 레이어는 동일한 페이지에서 어떤 방식으로든 확장되므로 해당 추가 데이터를 [!DNL Target]&#x200B;(으)로 전송하려고 합니다.
* 제품 카탈로그 데이터를 [!DNL Target Recommendations]&#x200B;(으)로 보내려고 합니다.

## 데이터 다이어그램 수집 {#diagram}

다음 그림에서 단계 번호는 아래 섹션에 해당합니다.

![데이터 수집 다이어그램](/help/dev/patterns/recs-atjs/assets/data-collection-diagram.png){width="600" zoomable="yes"}

다음 링크를 클릭하여 원하는 섹션으로 이동합니다.

* [2.1: 데이터 매핑 구성](#configure)
* [2.2 엔티티 속성에 대한 링크](#entity-attributes)
* [2.3 Adobe Target Track API 실행](#fire-api)

## 2.1: 데이터 매핑 구성 {#configure}

이 단계는 [!DNL Adobe Target]&#x200B;(으)로 전송해야 하는 모든 데이터가 설정되도록 하는 데 도움이 됩니다.

+++세부 정보 보기

![데이터 매핑 다이어그램 구성](/help/dev/patterns/recs-atjs/assets/configure-data-mapping-combined.png){width="400" zoomable="yes"}

**전제 조건**

* 데이터 레이어는 [!DNL Target]에 전송해야 하는 모든 데이터로 준비되어야 합니다.

**판독값**

[targetPageParams 함수](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**작업**

`targetPageParams()` 함수를 사용하여 [!DNL Target]&#x200B;(으)로 전송해야 하는 모든 필수 데이터를 설정하십시오.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 2.2: 엔티티 속성에 연결 {#entity-attributes}

엔터티 특성에 연결하여 [!DNL Target Recommendations]에 대한 제품 카탈로그를 업데이트합니다.

+++세부 정보 보기

**판독값**

* [엔티티 속성](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**고려 사항**

* 엔터티 특성을 전달하는 또 다른 방법은 [!DNL Target] UI에서 제품 카탈로그를 업데이트하여 [권장 사항 제품 피드](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank}를 사용하는 것입니다.
* 엔티티 속성 전달은 데이터 레이어에서 제품 카탈로그 데이터를 사용할 수 있는 페이지에만 적용할 수 있습니다.
* 모든 호출에서 `entity.event.detailsOnly=true` 매개 변수를 전달하는 것이 우선됩니다.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 2.3 Adobe Target Track API 실행 {#fire-api}

이 단계는 [!DNL Target]&#x200B;(으)로 전송해야 하는 모든 데이터를 전송하는 데 도움이 됩니다.

+++세부 정보 보기

![Adobe Target 추적 API 다이어그램 실행](/help/dev/patterns/recs-atjs/assets/fire-track-api-combined.png){width="400" zoomable="yes"}

**전제 조건**

* 모든 데이터 매핑은 [targetPageParams 함수](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)를 사용하여 수행되어야 합니다.

**판독값**

* [adobe.target.trackEvent() 메서드](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)

**작업**

[adobe.target.trackEvent() 메서드](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)을(를) 사용하여 [!DNL Target]&#x200B;(으)로 보내야 하는 모든 데이터를 보냅니다.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

3단계 진행: [경험 렌더링](/help/dev/patterns/recs-atjs/render-experiences.md)
