---
title: 데이터 수집 구성
description: 데이터 수집에 필요한 모든 작업이 올바른 순서로 실행되는지 확인합니다.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 30634afc84877a4e88e08f3b2173d4c0727f4362
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 3%

---

# 데이터 수집 구성

의 단계를 따릅니다. *데이터 수집* 데이터 수집에 필요한 모든 작업이 올바른 순서로 실행되도록 하는 다이어그램입니다.

>[!TIP]
>
>전체 화면으로 확장하려면 이 항목의 이미지를 클릭하십시오.

데이터 레이어는 페이지 로드 중에 준비되거나 페이지 로드 후 데이터 레이어가 변경됩니다.

다음 기간 동안 데이터를 이미 매핑한 경우: [sdk 초기화 단계](/help/dev/patterns/recs-atjs/initialize-sdk.md), 다음과 같은 경우 이 다이어그램의 단계를 실행해야 합니다.

* 데이터 레이어는 동일한 페이지에서 어떤 방식으로든 확장되므로 해당 추가 데이터를 로 전송하려는 경우 [!DNL Target]
* 제품 카탈로그 데이터를 (으)로 보내려는 경우 [!DNL Target Recommendations]

## 데이터 다이어그램 수집 {#diagram}

다음 그림에서 단계 번호는 아래 섹션에 해당합니다.

![데이터 수집 다이어그램](/help/dev/patterns/recs-atjs/assets/data-collection-diagram.png){width="600" zoomable="yes"}

다음 링크를 클릭하여 원하는 섹션으로 이동합니다.

* [2.1: 데이터 매핑 구성](#configure)
* [2.2 엔티티 속성에 대한 링크](#entity-attributes)
* [2.3 Adobe Target Track API 실행](#fire-api)

## 2.1: 데이터 매핑 구성 {#configure}

이 단계는 전송해야 하는 모든 데이터를 [!DNL Adobe Target] 이(가) 설정되어 있습니다.

+++세부 정보 보기

![데이터 매핑 다이어그램 구성](/help/dev/patterns/recs-atjs/assets/configure-data-mapping-combined.png){width="400" zoomable="yes"}

**전제 조건**

* 데이터 레이어는 로 전송해야 하는 모든 데이터로 준비되어야 합니다. [!DNL Target].

**읽기 횟수**

[targetPageParams 함수](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**작업**

사용 `targetPageParams()` 에 전송해야 하는 모든 필수 데이터를 설정하는 함수 [!DNL Target].

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 2.2: 엔티티 속성에 연결 {#entity-attributes}

제품 카탈로그를 업데이트하기 위한 엔티티 속성에 연결 [!DNL Target Recommendations].

+++세부 정보 보기

**읽기 횟수**

* [엔티티 속성](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**고려 사항**

* 엔티티 속성을 전달하는 또 다른 방법은 [!DNL Target] 사용할 UI [Recommendations 제품 피드](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank}.
* 엔티티 속성 전달은 데이터 레이어에서 제품 카탈로그 데이터를 사용할 수 있는 페이지에만 적용할 수 있습니다.
* 전달 `entity.event.detailsOnly=true` 모든 호출의 매개 변수가 우선합니다.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 2.3 Adobe Target Track API 실행 {#fire-api}

이 단계는 전송해야 하는 모든 데이터를 [!DNL Target] 이(가) 전송됩니다.

+++세부 정보 보기

![Adobe Target 추적 API 다이어그램 실행](/help/dev/patterns/recs-atjs/assets/fire-track-api-combined.png){width="400" zoomable="yes"}

**전제 조건**

* 모든 데이터 매핑은 [targetPageParams 함수](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**읽기 횟수**

* [adobe.target.trackEvent() 메서드](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)

**작업**

사용 [adobe.target.trackEvent() 메서드](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) 로 전송해야 하는 모든 데이터를 [!DNL Target].

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

