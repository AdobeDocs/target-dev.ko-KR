---
title: SDK 초기화
description: ' [!DNL Adobe Target] at.js JavaScript 라이브러리를 로드하는 데 필요한 모든 단계가 올바른 순서로 실행되는지 확인하십시오.'
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 250a8382-1fdd-4a70-b712-a25af5adad71
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 5%

---

# SDK 초기화

*SDK 초기화* 다이어그램의 단계에 따라 [!DNL Adobe Target] at.js JavaScript 라이브러리를 로드하는 데 필요한 모든 작업이 올바른 순서로 실행되도록 하십시오.

>[!TIP]
>
>전체 화면으로 확장하려면 이 항목의 이미지를 클릭하십시오.

## SDK 다이어그램 초기화 {#diagram}

다중 페이지 애플리케이션의 경우, 이 흐름은 페이지를 다시 로드하거나 방문자가 웹 사이트의 새 페이지로 이동할 때마다 발생합니다.

>[!NOTE]
>
>다음 그림에서 단계 번호는 아래 섹션에 해당합니다. 단계 번호는 특정 순서가 아니며 활동을 만드는 동안 [!DNL Target] UI에서 수행한 단계 순서를 반영하지 않습니다.

![SDK 다이어그램 초기화](/help/dev/patterns/recs-atjs/assets/diagram-initiaze-sdk.png){width="600" zoomable="yes"}

다음 링크를 클릭하여 원하는 섹션으로 이동합니다.

* [1.1: 방문자 API SDK 로드](#load)
* [1.2: 고객 ID 설정](#set)
* [1.3: 자동 페이지 로드 요청 구성](#automatic)
* [1.4: 플리커 처리 구성](#flicker)
* [1.5: 데이터 매핑 구성](#data-mapping)
* [1.6: 프로모션](#promotion)
* [1.7: 장바구니 기반 기준](#cart)
* [1.8: 인기도 기반 기준](#popularity)
* [1.9: 품목 기반 기준](#item)
* [1.10: 사용자 기반 기준](#user)
* [1.11: 사용자 지정 기준](#custom)
* [1.12: 포함 규칙에 사용되는 속성 제공](#inclusion)
* [1.13: excludedIds 제공](#exclude)
* [1.14: entity.event.detailsOnly=true 매개 변수 전달](#true)
* [1.15: 원격 데이터 매핑 구성](#remote)
* [1.16: at.js 로드](#web)

## 1.1: 방문자 API SDK 로드 {#load}

이 단계는 `VisitorAPI.js` 라이브러리가 올바르게 로드, 구성 및 초기화되도록 하는 데 도움이 됩니다.

+++세부 정보 보기

![방문자 API SDK 다이어그램 로드](/help/dev/patterns/recs-atjs/assets/load-visitor-combined.png){width="400" zoomable="yes"}

**전제 조건**

* 방문자 ID/API 서비스를 사용하려면 회사에 [!DNL Adobe Experience Cloud]이(가) 사용하도록 설정되어 있고 [!UICONTROL Organization ID]이(가) 있어야 합니다. 자세한 내용은 *ID 서비스 도움말* 안내서의 [Experience Cloud 요구 사항: 조직 ID](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html?){target=_blank}을 참조하세요.
* `VisitorAPI.js` 파일이 필요합니다. [!DNL Adobe Analytics]을(를) 구현한 경우 이 파일이 이미 있어야 합니다. 이 파일은 [[!DNL Adobe Experience Platform] 태그 확장](https://experienceleague.adobe.com/docs/tags.html){target=_blank}을 통해 추가하거나 [Adobe Analytics 코드 관리자](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html){target=_blank}에서 다운로드할 수도 있습니다.

**VisitorAPI.js 구성 및 참조**

자세한 내용은 [Target용 Experience Cloud 서비스 구현](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html){target=_blank}을 참조하세요.

**판독값**

* [Experience Cloud ID 서비스 개요](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html){target=_blank}
* [ID 서비스 정보](https://experienceleague.adobe.com/docs/id-service/using/intro/about-id-service.html){target=_blank}
* [쿠키 및 Experience Cloud ID 서비스](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html){target=_blank}
* [Experience Cloud ID 서비스에서 ID를 요청하고 설정하는 방법](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html){target=_blank}
* [ID 동기화 및 일치율 이해하기](https://experienceleague.adobe.com/docs/id-service/using/intro/match-rates.html){target=_blank}

**작업**

* 웹 페이지에 `VisitorAPI.js` 파일을 포함합니다.
* 방문자 ID/API 서비스에 대해 [사용 가능한 구성](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html){target=_blank}을(를) 읽어 보십시오.
* `VisitorAPI.js` 파일이 로드되면 필요한 구성을 사용하여 초기화하려면 `Visitor.getInstance` 메서드를 사용합니다.
* [사용 가능한 메서드](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html){target=_blank}를 숙지하십시오.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.2: 고객 ID 설정 {#set}

이 단계는 방문자의 알려진 ID(CRM ID, 사용자 ID 등)가 장치 간 개인화를 위해 [!DNL Adobe]의 익명 ID에 연결되어 있는지 확인하는 데 도움이 됩니다.

+++세부 정보 보기

![고객 ID 설정](/help/dev/patterns/recs-atjs/assets/set-customer-id-combined.png){width="400" zoomable="yes"}

**전제 조건**

* 방문자의 알려진 ID는 데이터 레이어에서 사용할 수 있어야 합니다.

**고객 ID 설정**
자세한 내용은 [setCustomerIDs](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html){target=_blank}을(를) 참조하십시오.

**판독값**

* [mbox3rdPartyId에 대한 실시간 프로필 동기화](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html){target=_blank}

**작업**

* `visitor.setCustomerIDs`을(를) 사용하여 방문자의 알려진 ID를 설정합니다.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.3: 자동 페이지 로드 요청 구성 {#automatic}

이 단계를 통해 at.js는 at.js JavaScript 라이브러리 파일을 로드하는 동안 페이지에 렌더링되어야 하는 모든 경험을 가져올 수 있습니다.

+++세부 정보 보기

![자동 페이지 로드 요청 구성](/help/dev/patterns/recs-atjs/assets/configure-automatic-page-request-combined.png){width="400" zoomable="yes"}

**전제 조건**

* 데이터 계층의 모든 데이터를 [!DNL Target](으)로 보낼 필요는 없습니다. 실험, 최적화 및 개인화에 유용한 데이터를 결정하려면 비즈니스 팀(디지털 마케팅 팀)과 상의하십시오. 이 데이터만 [!DNL Target](으)로 전송해야 합니다.
* PII(개인 식별 정보) 데이터를 [!DNL Target](으)로 보내지 마십시오.

**자동 페이지 로드 요청 구성**

자세한 내용은 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)를 참조하십시오.

**판독값**

[targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)의 `pageLoadEnabled` 설정에 대해 알아봅니다.

**작업**

* 자동 페이지 로드 요청을 사용하도록 설정하려면 `window.targetGlobalSettings` 개체를 수정하십시오.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.4: 플리커 처리 구성 {#flicker}

이 단계는 경험을 전달할 때 페이지 깜박임이 없는지 확인하는 데 도움이 됩니다.

+++세부 정보 보기

![깜박임 처리 다이어그램 구성](/help/dev/patterns/recs-atjs/assets/flicker-handling-combined.png){width="400" zoomable="yes"}

**전제 조건**

* at.js에서 사용하는 기본 방법을 사용하여 플리커를 제어하는 것의 장단점에 대해 웹 페이지 성능을 담당하는 팀과 논의합니다. 로더 애니메이션과 같은 사용자 지정 플리커 처리 솔루션을 사용할 수 있는 디자인 패턴을 검색할 수 있습니다. 패턴을 찾지 못한 경우 새 패턴을 요청할 수 있습니다.

**깜박임 처리 구성**

자세한 내용은 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)를 참조하십시오.

`bodyHidingEnabled`을(를) `true`(으)로 설정하면 페이지 로드 요청이 진행되는 동안 전체 페이지 본문이 숨겨집니다. 어떤 이유로든 자동 페이지 로드 요청을 활성화하지 않은 경우(예: 나중에 데이터가 준비되지 않은 경우) 이 설정을 `false`(으)로 설정하는 것이 가장 좋습니다.

APLR을 실행하지 않고 나중에 페이지 요청을 실행하려고 하기 때문에 `bodyHidingEnabled`을(를) 비활성화했거나 깜박임 처리가 필요하지 않은 경우 자체 깜박임 처리를 구현해야 합니다. 깜박임을 처리할 때는 테스트 중인 섹션을 숨기거나 테스트 중인 섹션에 두통을 표시하는 두 가지 방법을 사용할 수 있습니다.

**판독값**

* [at.js에서 플리커를 관리하는 방법](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
* [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)의 bodyHiddenStyle 및 bodyHidingEnabled 개체에 대해 알아봅니다.

**작업**

* `window.targetGlobalSettings` 개체를 수정하여 `bodyHiddenStyle` 및 `bodyHidingEnabled`을(를) 설정합니다.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.5: 데이터 매핑 구성 {#data-mapping}

이 단계는 [!DNL Target](으)로 전송해야 하는 모든 데이터가 설정되도록 하는 데 도움이 됩니다.

+++세부 정보 보기

![데이터 매핑 다이어그램](/help/dev/patterns/recs-atjs/assets/data-mapping-combined.png){width="400" zoomable="yes"}

**전제 조건**

* 데이터 레이어는 [!DNL Target](으)로 전송해야 하는 모든 데이터로 준비되어야 합니다.
* Recommendations: 프로필 보강.
   * `entity.id`을(를) 전달하여 마지막으로 본 제품에 기반한 기준을 기반으로 최근에 본 기준 및 항목에 대한 데이터를 캡처합니다.
   * 즐겨찾는 범주에 따라 인기도 기준에 대한 데이터를 캡처하려면 `entity.id`을(를) 전달합니다.
   * 사용자 지정 기준이 프로필 속성을 기반으로 하거나 임의의 기준에서 포함 규칙 필터링에 사용되는 경우 프로필 속성을 전달합니다.
* Recommendations: 제품 데이터를 수집합니다.
   * 다른 엔터티 매개 변수(예약된 매개 변수 및 사용자 지정)를 전달하여 [!DNL Recommendations]에서 제품 카탈로그를 수집하거나 업데이트할 수 있습니다.
   * [!DNL Target] UI 또는 API를 사용하여 엔터티 피드를 사용하여 제품 카탈로그를 업데이트할 수도 있습니다.

**데이터를[!DNL Target]**&#x200B;에 매핑

자세한 내용은 [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)을 참조하십시오.

**판독값**

* [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)
* [권장 사항 계획 및 구현](/help/dev/implement/recommendations/recommendations.md)
* [Recommendations 카탈로그 설정](/help/dev/implement/recommendations/recommendations.md)

**작업**

* `targetPageParams()` 함수를 사용하여 [!DNL Target](으)로 전송해야 하는 모든 필수 데이터를 설정하십시오.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.6: 프로모션 {#promotion}

프로모션된 항목을 추가하고 [!DNL Target Recommendations] [디자인](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}에서 해당 배치를 제어합니다.

+++세부 정보 보기

**사용 가능한 옵션**

* ID별 프로모션
* 컬렉션별 [홍보](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* 특성별 [승격](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**필요한 엔터티 매개 변수**

* &quot;속성별 판촉&quot; 옵션을 사용할 때 판촉의 항목 속성을 전달해야 합니다.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.7: 장바구니 기반 기준 {#cart}

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

## 1.8: 인기도 기반 기준 {#popularity}

사이트에서 항목의 전체 인기도를 기반으로 추천하거나 사용자가 좋아하거나 가장 많이 본 카테고리, 브랜드, 장르 등의 항목 인기도를 기반으로 추천합니다.

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

* `entity.categoryId` 또는 기준이 현재 항목 또는 항목 특성을 기준으로 하는 인기도 항목 특성입니다.
* 사이트에서 가장 많이 본 항목/가장 많이 판매된 항목에 대해서는 아무 것도 전달하지 않아야 합니다.

**판독값**

* [인기도 기반](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.9: 품목 기반 기준 {#item}

사용자가 보고 있거나 최근에 본 항목과 유사한 항목을 찾은 후 권장 사항을 제공합니다.

+++세부 정보 보기

**사용 가능한 기준**

* [!UICONTROL People Who Viewed This, Viewed That]
* [!UICONTROL People Who Viewed This, Bought That]
* [!UICONTROL People Who Bought This, Bought That]
* [!UICONTROL Items with Similar Attributes]

**필요한 엔터티 매개 변수**

* `entity.id` 또는 키로 사용되는 모든 프로필 특성

**판독값**

* [항목 기반](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.10: 사용자 기반 기준 {#user}

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

## 1.11: 사용자 지정 기준 {#custom}

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

## 1.12: 포함 규칙에 사용되는 속성 제공 {#inclusion}

+++세부 정보 보기

**판독값**

* [동적 및 정적 포함 규칙 사용](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.13: excludedIds 제공 {#exclude}

권장 사항에서 제외하려는 엔티티에 대한 엔티티 ID를 전달합니다. 예를 들어 장바구니에 이미 있는 항목을 제외할 수 있습니다.

+++세부 정보 보기

**판독값**

* [엔티티를 동적으로 제외할 수 있습니까?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.14: `entity.event.detailsOnly=true` 매개 변수 전달 {#true}

엔터티 특성을 사용하여 제품 또는 콘텐츠 정보를 [!DNL Target Recommendations]에 전달합니다.

+++세부 정보 보기

**판독값**

* [엔터티 특성](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=en){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.15: 원격 데이터 매핑 구성(원격)

이 단계에서는 [!DNL Target](으)로 전송해야 하는 모든 데이터가 설정되었는지 확인합니다.

+++세부 정보 보기

![원격 데이터 매핑 다이어그램](/help/dev/patterns/recs-atjs/assets/remote-data-mapping-combined.png){width="400" zoomable="yes"}

**전제 조건**

* 데이터 레이어는 [!DNL Target]에 전송해야 하는 모든 데이터로 준비되어야 합니다.

**데이터 공급자 설정**

자세한 내용은 [데이터 공급자](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers)를 참조하세요.

**판독값**

[targetPageParams 함수](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**작업**

`targetPageParams()` 함수를 사용하여 [!DNL Target](으)로 전송해야 하는 모든 필수 데이터를 설정하십시오.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.16: at.js 로드 {#web}

이 단계에서는 at.js JavaScript 라이브러리가 로드되고 초기화되도록 합니다.

+++세부 정보 보기

![Adobe Target at.js 다이어그램 로드](/help/dev/patterns/recs-atjs/assets/load-atjs-combined.png){width="400" zoomable="yes"}

**전제 조건**

* 디지털 마케팅 팀에 `at.js 2.*x*` JavaScript 라이브러리 파일을 다운로드하거나 요청하십시오.

*판독값*

* [Target 작동 방식](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html){target=_blank}
* [at.js 작동 방식](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
* [태그 관리자 없이 Target 구현](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

**작업**

실험, 최적화, 개인화 및 데이터 수집이 일어나야 하는 모든 웹 페이지에 at.js 파일을 포함합니다.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

2단계: [데이터 수집 구성](/help/dev/patterns/recs-atjs/data-collection.md)으로 진행합니다.
