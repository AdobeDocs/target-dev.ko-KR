---
title: 경험 렌더링
description: 경험을 렌더링하는 데 필요한 모든 단계가 올바른 순서로 실행되는지 확인하십시오.
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 7cf0c70b-a4bc-46f4-9b33-099bdb7dd9a9
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 4%

---

# 경험 렌더링

경험을 렌더링하는 데 필요한 모든 작업이 올바른 순서로 실행되도록 하려면 *경험 렌더링* 다이어그램의 단계를 따르십시오.

>[!NOTE]
>
>*SDK 초기화*&#x200B;에서 [자동 페이지 로드 요청 구성 단계](/help/dev/patterns/recs-atjs/initialize-sdk.md#automatic) 동안 자동 페이지 로드 요청을 활성화한 경우, Adobe Target SDK를 호출하여 지역 위치 요청을 사용하여 추가 경험을 렌더링하려는 경우가 아니면 이 활동을 건너뛸 수 있습니다.

>[!TIP]
>
>전체 화면으로 확장하려면 이 항목의 이미지를 클릭하십시오.

## 경험 다이어그램 렌더링 {#diagram}

at.js에서 사용할 수 있는 자동 기본 플리커 처리는 [!UICONTROL Automatic Page Load Request]을(를) 활성화한 경우에만 적용됩니다. 이 옵션은 [!DNL Target]에서 경험을 가져오는 동안 전체 HTML 본문을 숨깁니다. 이 경우 깜박임을 처리하는 것은 사용자의 책임입니다. 지침을 위해 깜박임 처리에 사용할 수 있는 구현 패턴을 검색합니다.

>[!NOTE]
>
>다음 그림에서 단계 번호는 아래 섹션에 해당합니다. 단계 번호는 특정 순서가 아니며 활동을 만드는 동안 [!DNL Target] UI에서 수행한 단계 순서를 반영하지 않습니다.

![경험 다이어그램 렌더링](/help/dev/patterns/recs-atjs/assets/diagram-render-experiences-new.png){width="600" zoomable="yes"}

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

활동을 만드는 동안 [!DNL Target] UI에서 전면 또는 후면 프로모션을 선택하여 프로모션된 항목을 추가하고 권장 사항 디자인에서 해당 배치를 제어합니다.

+++세부 정보 보기

**사용 가능한 옵션**

* ID별 프로모션
* 컬렉션별 [홍보](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* 특성별 [승격](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**필요한 엔터티 매개 변수**

* &quot;속성별 판촉&quot; 옵션을 사용할 때 판촉의 항목 속성을 전달해야 합니다.

**판독값**

* [프로모션 추가](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/adding-promotions.html){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.2: 장바구니 기반 기준 {#cart}

사용자의 장바구니 콘텐츠를 기반으로 추천을 제공합니다.

+++세부 정보 보기

**사용 가능한 기준**

* [!UICONTROL People Who Viewed These, Viewed Those]
* [!UICONTROL People Who Viewed These, Bought Those]
* [!UICONTROL People Who Bought These, Bought Those]

**필요한 엔터티 매개 변수**

* cartIds

**판독값**

* [장바구니 기반](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.3: 인기도 기반 기준 {#popularity}

사이트에서 항목의 전체 인기도를 기반으로 추천하거나 방문자가 가장 좋아하거나 가장 많이 본 카테고리, 브랜드, 장르 등의 항목 인기도를 기반으로 추천합니다.

+++세부 정보 보기

**사용 가능한 기준**

* [!UICONTROL Most Viewed Across the Site]
* [!UICONTROL Most Viewed by Category]
* [!UICONTROL Most Viewed by Item Attribute]
* [!UICONTROL Top Sellers Across the Site]
* [!UICONTROL Top Sellers by Category]
* [!UICONTROL Top Sellers by Item Attribute]
* [!UICONTROL Top by Analytics Metric]

**필요한 엔터티 매개 변수**

* `entity.categoryId` 또는 기준이 현재 또는 항목 특성을 기준으로 하는 인기도 항목 특성입니다.
* 사이트에서 가장 많이 본 항목/가장 많이 판매된 항목에 대해서는 아무 것도 전달하지 않아야 합니다.

**판독값**

* [인기도 기반](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.4: 품목 기반 기준 {#item}

사용자가 보고 있거나 최근에 본 항목과 유사한 항목을 찾은 후 권장 사항을 제공합니다.

+++세부 정보 보기

**사용 가능한 기준**

* [!UICONTROL People Who Viewed This, Viewed That]
* [!UICONTROL People Who Viewed This, Bought That]
* [!UICONTROL People Who Bought This, Bought That]
* [!UICONTROL Items with Similar Attributes]

**필요한 엔터티 매개 변수**

* `entity.id`
* 프로필 속성을 키로 사용하는 경우

**판독값**

* [항목 기반](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.5: 사용자 기반 기준 {#user}

사용자의 행동을 기반으로 권장 사항을 제공합니다.

+++세부 정보 보기

**사용 가능한 기준**

* [!UICONTROL Recently Viewed Items]
* [!UICONTROL Recommended for You]

**필요한 엔터티 매개 변수**

* `entity.id`

**판독값**

* [사용자 기반](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.6: 사용자 지정 기준 {#custom}

업로드하는 사용자 지정 파일을 기반으로 권장 사항을 제공합니다.

+++세부 정보 보기

**사용 가능한 기준**

* [!UICONTROL Custom algorithm]

**필요한 엔터티 매개 변수**

`entity.id` 또는 사용자 지정 알고리즘의 키로 사용되는 특성

**판독값**

* [사용자 지정 기준](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.7: 포함 규칙에 사용되는 속성 제공 {#inclusion}

+++세부 정보 보기

**판독값**

* [동적 및 정적 포함 규칙 사용](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.8: excludedIds 제공 {#exclude}

권장 사항에서 제외하려는 엔티티에 대한 엔티티 ID를 전달합니다. 예를 들어 장바구니에 이미 있는 항목을 제외할 수 있습니다.

+++세부 정보 보기

**판독값**

* [엔티티를 동적으로 제외할 수 있습니까?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.9: [!DNL Recommendations]에 대한 제품 카탈로그를 업데이트하려면 엔터티 특성을 제공하십시오. {#entity-attributes}

+++세부 정보 보기

**판독값**

* [엔터티 특성](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

[!DNL Target] UI를 사용하여 [제품 피드](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank}를 만들어 [!DNL Recommendations]에 대한 제품 카탈로그를 업데이트하여 이 단계를 수행할 수도 있습니다.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.10: 포함 규칙의 키로 사용되는 프로필 속성 제공 {#keys}

위에서 언급한 모든 Recommendations 기준에서 포함 규칙의 키로 사용되는 프로필 속성을 제공합니다.

+++ 세부 정보 보기

**판독값**

* [프로필 특성](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.11: 페이지 로드 요청 실행 {#fire}

이 단계는 요청에서 `execute` > `pageLoad` 페이로드로 [!DNL Delivery API] 호출을 트리거합니다. `getOffers()` 메서드는 경험을 가져오고 `applyOffers()`은(는) 페이지에서 경험을 렌더링합니다. [시각적 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank}(VEC)에서 작성된 경험을 렌더링하려면 `pageLoad` 요청이 필요합니다.

+++세부 정보 보기

![페이지 로드 요청 다이어그램 실행](/help/dev/patterns/recs-atjs/assets/fire-page-load-request-combined.png){width="400" zoomable="yes"}

**전제 조건**

* 모든 데이터 매핑은 `targetPageParams` 함수를 사용하여 수행해야 합니다.

**판독값**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**작업**

* `getOffers` 및 `applyOffers` 메서드를 사용하여 페이지 로드 요청 API 호출을 사용하여 경험을 가져옵니다.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 3.12: 지역 위치 요청 실행(#location)

이 단계는 요청에서 `execute` > `mboxes` 페이로드로 [!DNL Delivery API] 호출을 트리거합니다. `getOffers` 메서드는 경험을 가져오고 `applyOffers`은(는) 경험을 페이지에 렌더링합니다. `execute` > `mboxes` 페이로드 아래에서 두 개 이상의 mbox를 보낼 수 있습니다.

+++세부 정보 보기

![지역 위치 요청 다이어그램 실행](/help/dev/patterns/recs-atjs/assets/fire-regional-location-request-combined.png){width="400" zoomable="yes"}

**전제 조건**

* 모든 데이터 매핑은 `targetPageParams` 함수를 사용하여 수행해야 합니다.

**판독값**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**작업**

* `getOffers` 및 `applyOffers` 메서드를 사용하여 페이지 로드 요청 API 호출을 사용하여 경험을 가져옵니다.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

4단계: [대상에게 알림](/help/dev/patterns/recs-atjs/notify-target.md)을 진행합니다.
