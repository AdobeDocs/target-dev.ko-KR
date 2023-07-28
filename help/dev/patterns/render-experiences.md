---
title: 경험 렌더링
description: 경험을 렌더링하는 데 필요한 모든 단계가 올바른 순서로 실행되는지 확인하십시오.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 9b65380febf64896a3885c49f8bb79e4bb33f604
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 5%

---

# 경험 렌더링

의 단계를 따릅니다. *렌더링 경험* 경험을 렌더링하는 데 필요한 모든 작업이 올바른 순서로 실행되도록 하는 다이어그램입니다.

>[!TIP]
>
>전체 화면으로 확장하려면 이 항목의 이미지를 클릭하십시오.

## 경험 다이어그램 렌더링 {#diagram}

at.js에서 사용할 수 있는 자동 기본 플리커 처리는 [!UICONTROL 자동 페이지 로드 요청] 활성화되었습니다. 이 옵션은에서 경험을 가져오는 동안 전체 HTML 본문을 숨깁니다. [!DNL Target]. 이 경우 깜박임을 처리하는 것은 사용자의 책임입니다. 지침을 위해 깜박임 처리에 사용할 수 있는 구현 패턴을 검색합니다.

다음 그림에서 단계 번호는 아래 섹션에 해당합니다.

![경험 다이어그램 렌더링](/help/dev/patterns/assets/diagram-render-experiences.png){width="600" zoomable="yes"}

다음 링크를 클릭하여 원하는 섹션으로 이동합니다.

* [3.1: 프로모션](#promotion)
* [3.2: 장바구니 기반 기준](#cart)
* [3.3: 인기도 기반 기준](#popularity)
* [3.4: 품목 기반 기준](#item)
* [3.5: 사용자 기반 기준](#user)
* [3.6: 사용자 지정 기준](#custom)
* [3.7: 포함 규칙에 사용되는 속성 제공](#inclusion)
* [3.8: excludedIds 제공](#exclude)
* [3.9: Recommendations에 대한 제품 카탈로그를 업데이트하려면 엔티티 속성을 제공하십시오](#entity-attributes)
* [3.10: 포함 규칙의 키로 사용되는 프로필 속성 제공](#keys)
* [3.11: 페이지 로드 요청 실행](#fire)
* [3.12: 지역 위치 요청 실행](#location)

## 3.1: 프로모션 {#promotion}

프로모션된 항목을 추가하고 Target Recommendations에서 해당 배치를 제어합니다. [디자인](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

+++세부 정보 보기

**사용 가능한 옵션**

* ID별 프로모션
* [컬렉션별 홍보](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [속성별 프로모션](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**필요한 엔티티 매개 변수**

* &quot;속성별 판촉&quot; 옵션을 사용할 때 판촉의 항목 속성을 전달해야 합니다.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.2: 장바구니 기반 기준 {#cart}

사용자의 장바구니 콘텐츠를 기반으로 추천을 제공합니다.

+++세부 정보 보기

**사용 가능한 기준**

* [!UICONTROL 이 항목을 보고 다른 항목도 본 사람]
* [!UICONTROL 이 항목을 보고 다른 항목을 구입한 사람]
* [!UICONTROL 이 항목을 구입하고 다른 항목도 구입한 사람]

**필요한 엔티티 매개 변수**

* cartIds

**읽기 횟수**

* [장바구니 기반](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.3: 인기도 기반 기준 {#popularity}

사이트에서 항목의 전체 인기도를 기반으로 추천하거나 사용자가 좋아하거나 가장 많이 본 카테고리, 브랜드, 장르 등의 항목 인기도를 기반으로 추천합니다.

+++세부 정보 보기

**사용 가능한 기준**

* [!UICONTROL 사이트에서 가장 많이 본 항목]
* [!UICONTROL 범주별 최고 조회수]
* [!UICONTROL 항목별 가장 많이 본 항목 속성]
* [!UICONTROL 사이트 전체 최상위 판매자]
* [!UICONTROL 범주별 최상위 판매자]
* [!UICONTROL 항목 속성별 최상위 판매자]
* [!UICONTROL Analytics 지표 상위]

**필요한 엔티티 매개 변수**

* `entity.categoryId` 또는 기준이 현재 또는 항목 속성을 기준으로 하는 경우 인기도 항목 속성을 기준으로 합니다.
* 사이트에서 가장 많이 본 항목/가장 많이 판매된 항목에 대해서는 아무 것도 전달하지 않아야 합니다.

**읽기 횟수**

* [인기도 기반](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.4: 품목 기반 기준 {#item}

사용자가 보고 있거나 최근에 본 항목과 유사한 항목을 찾은 후 권장 사항을 제공합니다.

+++세부 정보 보기

**사용 가능한 기준**

* [!UICONTROL 이 항목을 보고 다른 항목도 본 사람]
* [!UICONTROL 이 항목을 보고 다른 항목을 구입한 사람]
* [!UICONTROL 이 항목을 구입하고 다른 항목도 구입한 사람]
* [!UICONTROL 속성이 비슷한 항목]

**필요한 엔티티 매개 변수**

* `entity.id`
* 프로필 속성을 키로 사용하는 경우

**읽기 횟수**

* [항목 기반](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.5: 사용자 기반 기준 {#user}

사용자의 행동을 기반으로 권장 사항을 제공합니다.

+++세부 정보 보기

**사용 가능한 기준**

* [!UICONTROL 최근에 본 항목]
* [!UICONTROL 추천 항목]

**필요한 엔티티 매개 변수**

* `entity.id`

**읽기 횟수**

* [사용자 기반](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.6: 사용자 지정 기준 {#custom}

업로드하는 사용자 지정 파일을 기반으로 추천 만들기

+++세부 정보 보기

**사용 가능한 기준**

* [!UICONTROL 사용자 지정 알고리즘]

**필요한 엔티티 매개 변수**

`entity.id` 또는 사용자 지정 알고리즘의 키로 사용되는 속성

**읽기 횟수**

* [사용자 지정 기준](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.7: 포함 규칙에 사용되는 속성 제공 {#inclusion}

+++세부 정보 보기

**읽기 횟수**

* [동적 및 정적 포함 규칙 사용](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.8: excludedIds 제공 {#exclude}

권장 사항에서 제외하려는 엔티티에 대한 엔티티 ID를 전달합니다. 예를 들어 장바구니에 이미 있는 항목을 제외할 수 있습니다.

+++세부 정보 보기

**읽기 횟수**

* [엔티티를 동적으로 제외할 수 있습니까?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.9: 제품 카탈로그를 업데이트할 엔티티 속성을 제공합니다. [!DNL Recommendations] {#entity-attributes}

+++세부 정보 보기

**읽기 횟수**

* [엔티티 속성](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

를 사용하여 제품 피드를 만들어 이 단계를 수행할 수도 있습니다. [!DNL Target] 제품 카탈로그를 업데이트할 UI [!DNL Recommendations].

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.10: 포함 규칙의 키로 사용되는 프로필 속성 제공 {#keys}

위에서 언급한 모든 Recommendations 기준에서 포함 규칙의 키로 사용되는 프로필 속성을 제공합니다.

+++ 세부 정보 보기

**읽기 횟수**

* [프로필 속성](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.11: 페이지 로드 요청 실행 {#fire}

이 단계는 [!DNL Delivery API] 을 사용하여 호출 `execute` > `pageLoad` 요청의 페이로드입니다. 다음 `getOffers()` 메서드는 경험을 가져오고 `applyOffers()` 페이지에서 경험을 렌더링합니다. PageLoad 요청은에서 작성된 경험을 렌더링하는 데 필요합니다. [시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank} (VEC).

+++세부 정보 보기

![페이지 로드 요청 다이어그램 실행](/help/dev/patterns/assets/fire-page-load-request.png){width="100" zoomable="yes"}

**전제 조건**

* 모든 데이터 매핑은 `targetPageParams` 함수.

**읽기 횟수**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**작업**

* 사용 `getOffers` 및 `applyOffers` 페이지 로드 요청 API 호출을 사용하여 경험을 가져오는 메서드.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.12: 지역 위치 요청 실행(#location)

이 단계는 [!DNL Delivery API] 을 사용하여 호출 `execute` > `mboxes` 페이로드가 요청에 있습니다. 다음 `getOffers` 메서드는 경험을 가져오고 `applyOffers` 경험을 페이지에 렌더링합니다. 아래에서 mbox를 두 개 이상 보낼 수 있습니다. `execute` > `mboxes` 페이로드.

+++세부 정보 보기

![지리적 위치 요청 다이어그램 실행](/help/dev/patterns/assets/fire-regional-location-request.png){width="100" zoomable="yes"}

**전제 조건**

* 모든 데이터 매핑은 `targetPageParams` 함수.

**읽기 횟수**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**작업**

* 사용 `getOffers` 및 `applyOffers` 페이지 로드 요청 API 호출을 사용하여 경험을 가져오는 메서드.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)