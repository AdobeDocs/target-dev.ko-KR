---
title: SDK 초기화
description: Adobe Experience Platform Web SDK를 로드하는 데 필요한 모든 단계가 올바른 순서로 실행되는지 확인합니다.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: ca23e3d9a94d0c7b746971b10dae96e1141ef93f
workflow-type: tm+mt
source-wordcount: '1774'
ht-degree: 5%

---

# SDK 초기화

의 단계를 따릅니다. *SDK 초기화* 을 로드하는 데 필요한 모든 작업을 확인하는 다이어그램 [!DNL Adobe Target] at.js JavaScript 라이브러리는 올바른 시퀀스에서 실행됩니다.

>[!TIP]
>
>전체 화면으로 확장하려면 이 항목의 이미지를 클릭하십시오.

## SDK 다이어그램 초기화 {#diagram}

다중 페이지 애플리케이션의 경우, 이 흐름은 페이지를 다시 로드하거나 방문자가 웹 사이트의 새 페이지로 이동할 때마다 발생합니다.

다음 그림에서 단계 번호는 아래 섹션에 해당합니다.

![SDK 다이어그램 초기화](/help/dev/patterns/assets/diagram-initiaze-sdk.png){width="600" zoomable="yes"}

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

이 단계는 `VisitorAPI.js` 라이브러리가 올바르게 로드, 구성 및 초기화됩니다.

+++세부 정보 보기

![방문자 API SDK 다이어그램 로드](/help/dev/patterns/assets/load-visitor-api-sdk.png){width="100" zoomable="yes"}

**전제 조건**

* 방문자 ID/API 서비스를 사용하려면 회사에 대해 가 활성화되어 있어야 합니다. [!DNL Adobe Experience Cloud] 다음 작업을 수행합니다. [!UICONTROL 조직 ID]. 자세한 내용은 [Experience Cloud 요구 사항: 조직 ID](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html?){target=_blank} 다음에서 *ID 서비스 도움말* 가이드.
* 다음이 필요합니다. `VisitorAPI.js` 파일. 이 파일을 가져오려면 디지털 마케팅 팀에 문의하십시오.

**VisitorAPI.js 구성 및 참조**

자세한 내용은 [Target을 위한 Experience Cloud 서비스 구현](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html){target=_blank}.

**읽기 횟수**

* [Experience Cloud ID 서비스 개요](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html){target=_blank}
* [ID 서비스 정보](https://experienceleague.adobe.com/docs/id-service/using/intro/about-id-service.html){target=_blank}
* [쿠키 및 Experience Cloud ID 서비스](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html){target=_blank}
* [Experience Cloud ID 서비스에서 ID를 요청하고 설정하는 방법](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html){target=_blank}
* [ID 동기화 및 일치율 이해하기](https://experienceleague.adobe.com/docs/id-service/using/intro/match-rates.html){target=_blank}

**작업**

* 포함 `VisitorAPI.js` 웹 페이지에 있는 파일입니다.
* 에 대해 읽기 [방문자 ID/API 서비스에 사용 가능한 구성](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html){target=_blank}.
* 다음 이후 `VisitorAPI.js` 파일이 로드되었습니다. `Visitor.getInstance` 필요한 구성을 사용하여 초기화하는 방법입니다.
* 다음 사항에 대해 숙지하십시오. [사용 가능한 메서드](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html){target=_blank}.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.2: 고객 ID 설정 {#set}

이 단계는 방문자의 알려진 ID(CRM ID, 사용자 ID 등)가 의 익명 ID에 연결되어 있는지 확인하는 데 도움이 됩니다. [!DNL Adobe] 디바이스 간 개인화용.

+++세부 정보 보기

![고객 ID 설정](/help/dev/patterns/assets/set-customer-id.png){width="100" zoomable="yes"}

**전제 조건**

* 방문자의 알려진 ID는 데이터 레이어에서 사용할 수 있어야 합니다.

**고객 ID 설정**
자세한 내용은 [setCustomerID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html){target=_blank}.

**읽기 횟수**

* [mbox3rdPartyId에 대한 실시간 프로필 동기화](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html){target=_blank}

**작업**

* 사용 `visitor.setCustomerIDs` 방문자의 알려진 ID를 설정합니다.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.3: 자동 페이지 로드 요청 구성 {#automatic}

이 단계를 통해 at.js는 at.js JavaScript 라이브러리 파일을 로드하는 동안 페이지에 렌더링되어야 하는 모든 경험을 가져올 수 있습니다.

+++세부 정보 보기

![자동 페이지 로드 요청 구성](/help/dev/patterns/assets/configure-automatic-page-request.png){width="100" zoomable="yes"}

**전제 조건**

* 데이터 레이어의 모든 데이터를에 보내야 하는 것은 아닙니다. [!DNL Target]. 실험, 최적화 및 개인화에 유용한 데이터를 결정하려면 비즈니스 팀(디지털 마케팅 팀)과 상의하십시오. 이 데이터만 (으)로 전송되어야 합니다. [!DNL Target].
* 개인식별정보(PII) 데이터를 (으)로 전송하지 마십시오 [!DNL Target].

**자동 페이지 로드 요청 구성**

자세한 내용은 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)를 참조하십시오.

**읽기 횟수**

에 대해 알아보기 `pageLoadEnabled` 에서 설정 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**작업**

* 수정 `window.targetGlobalSettings` 자동 페이지 로드 요청을 활성화하는 개체입니다.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.4: 플리커 처리 구성 {#flicker}

이 단계는 경험을 전달할 때 페이지 깜박임이 없는지 확인하는 데 도움이 됩니다.

+++세부 정보 보기

![플리커 처리 다이어그램 구성](/help/dev/patterns/assets/flicker-handling.png){width="100" zoomable="yes"}

**전제 조건**

* at.js에서 사용하는 기본 방법을 사용하여 플리커를 제어하는 것의 장단점에 대해 웹 페이지 성능을 담당하는 팀과 논의합니다. 로더 애니메이션과 같은 사용자 지정 플리커 처리 솔루션을 사용할 수 있는 디자인 패턴을 검색할 수 있습니다. 패턴을 찾지 못한 경우 새 패턴을 요청할 수 있습니다.

**플리커 처리 구성**

자세한 내용은 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)를 참조하십시오.

설정 `bodyHidingEnabled` 끝 `true` 페이지 로드 요청이 진행되는 동안 전체 페이지 본문을 숨깁니다. 어떤 이유로든 자동 페이지 로드 요청을 활성화하지 않은 경우(예: 나중에 데이터가 준비되지 않음) 이 설정을 로 설정하는 것이 가장 좋습니다. `false`.

을 비활성화한 경우 `bodyHidingEnabled` aplr을 실행하지 않고 페이지 요청을 나중에 실행하려고 하거나 플리커 처리가 필요하지 않으므로 플리커 처리를 직접 구현해야 합니다. 깜박임을 처리할 때는 테스트 중인 섹션을 숨기거나 테스트 중인 섹션에 두통을 표시하는 두 가지 방법을 사용할 수 있습니다.

**읽기 횟수**

* [at.js에서 플리커를 관리하는 방법](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
* 의 bodyHiddenStyle 및 bodyHidingEnabled 개체에 대해 알아봅니다 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**작업**

* 수정 `window.targetGlobalSettings` 설정할 개체 `bodyHiddenStyle` 및 `bodyHidingEnabled`.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.5: 데이터 매핑 구성 {#data-mapping}

이 단계는 전송해야 하는 모든 데이터를 [!DNL Target] 이(가) 설정되어 있습니다.

+++세부 정보 보기

![데이터 매핑 다이어그램](/help/dev/patterns/assets/data-mapping.png){width="100" zoomable="yes"}

**전제 조건**

* 데이터 레이어는 로 전송해야 하는 모든 데이터로 준비되어야 합니다. [!DNL Target].
* Recommendations: 프로필 보강.
   * 합격 `entity.id` 마지막으로 본 제품을 기반으로 한 기준을 기반으로 하여 최근에 본 기준 및 항목에 대한 데이터를 캡처합니다.
   * 합격 `entity.id` 즐겨찾는 카테고리에 따라 인기도 기준의 데이터를 캡처합니다.
   * 사용자 지정 기준이 프로필 속성을 기반으로 하거나 임의의 기준에서 포함 규칙 필터링에 사용되는 경우 프로필 속성을 전달합니다.
* Recommendations: 제품 데이터를 수집합니다.
   * 다른 엔티티 매개 변수(예약됨 및 사용자 지정)를 전달하여 의 제품 카탈로그를 수집하거나 업데이트할 수 있습니다. [!DNL Recommendations].
   * 다음을 사용하여 엔티티 피드를 사용하여 제품 카탈로그를 업데이트할 수도 있습니다. [!DNL Target] UI 또는 API.

**데이터 매핑 대상[!DNL Target]**

자세한 내용은 [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**읽기 횟수**

* [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)
* [권장 사항 계획 및 구현](/help/dev/implement/recommendations/recommendations.md)
* [Recommendations 카탈로그 설정](/help/dev/implement/recommendations/recommendations.md)

**작업**

* 사용 `targetPageParams()` 에 전송해야 하는 모든 필수 데이터를 설정하는 함수 [!DNL Target].

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.6: 프로모션 {#promotion}

프로모션된 항목을 추가하고 [!DNL Target Recommendations] [디자인](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

+++세부 정보 보기

**사용 가능한 옵션**

* ID별 프로모션
* [컬렉션별 홍보](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [속성별 프로모션](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**필요한 엔티티 매개 변수**

* &quot;속성별 판촉&quot; 옵션을 사용할 때 판촉의 항목 속성을 전달해야 합니다.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.7: 장바구니 기반 기준 {#cart}

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

## 1.8: 인기도 기반 기준 {#popularity}

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

* `entity.categoryId` 또는 기준이 현재 품목 또는 품목 속성을 기준으로 하는 경우 인기도 항목 속성을 기준으로 합니다.
* 사이트에서 가장 많이 본 항목/가장 많이 판매된 항목에 대해서는 아무 것도 전달하지 않아야 합니다.

**읽기 횟수**

* [인기도 기반](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.9: 품목 기반 기준 {#item}

사용자가 보고 있거나 최근에 본 항목과 유사한 항목을 찾은 후 권장 사항을 제공합니다.

+++세부 정보 보기

**사용 가능한 기준**

* [!UICONTROL 이 항목을 보고 다른 항목도 본 사람]
* [!UICONTROL 이 항목을 보고 다른 항목을 구입한 사람]
* [!UICONTROL 이 항목을 구입하고 다른 항목도 구입한 사람]
* [!UICONTROL 속성이 비슷한 항목]

**필요한 엔티티 매개 변수**

* `entity.id` 또는 키로 사용되는 모든 프로필 속성

**읽기 횟수**

* [항목 기반](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.10: 사용자 기반 기준 {#user}

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

## 1.11: 사용자 지정 기준 {#custom}

업로드하는 사용자 지정 파일을 기반으로 권장 사항을 제공합니다.

+++세부 정보 보기

**사용 가능한 기준**

* [!UICONTROL 사용자 지정 알고리즘]

**필요한 엔티티 매개 변수**

`entity.id` 또는 사용자 지정 알고리즘의 키로 사용되는 속성

**읽기 횟수**

* [사용자 지정 기준](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.12: 포함 규칙에 사용되는 속성 제공 {#inclusion}

+++세부 정보 보기

**읽기 횟수**

* [동적 및 정적 포함 규칙 사용](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.13: excludedIds 제공 {#exclude}

권장 사항에서 제외하려는 엔티티에 대한 엔티티 ID를 전달합니다. 예를 들어 장바구니에 이미 있는 항목을 제외할 수 있습니다.

+++세부 정보 보기

**읽기 횟수**

* [엔티티를 동적으로 제외할 수 있습니까?](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.14: 를 전달합니다. `entity.event.detailsOnly=true` 매개 변수 {#true}

엔티티 속성을 사용하여 제품 또는 컨텐츠 정보를 로 전달 [!DNL Target Recommendations].

+++세부 정보 보기

**읽기 횟수**

* [엔티티 속성](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=en){target=_blank}

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.15: 원격 데이터 매핑 구성(원격)

이 단계에서는 전송해야 하는 모든 데이터를 [!DNL Target] 이(가) 설정되어 있습니다.

+++세부 정보 보기

![원격 데이터 매핑 다이어그램](/help/dev/patterns/assets/remote-data-mapping.png){width="100" zoomable="yes"}

**전제 조건**

* 데이터 레이어는 로 전송해야 하는 모든 데이터로 준비되어야 합니다. [!DNL Target].

**데이터 공급자 설정**

자세한 내용은 [데이터 공급자](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

**읽기 횟수**

[targetPageParams 함수](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**작업**

사용 `targetPageParams()` 에 전송해야 하는 모든 필수 데이터를 설정하는 함수 [!DNL Target].

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)

## 1.16: at.js 로드 {#web}

이 단계에서는 at.js JavaScript 라이브러리가 로드되고 초기화되도록 합니다.

+++세부 정보 보기

![Adobe Target 웹 SDK 다이어그램 로드](/help/dev/patterns/assets/load-web-sdk.png){width="100" zoomable="yes"}

**전제 조건**

* 디지털 마케팅 팀에 웹 SDK 라이브러리 파일을 다운로드하거나 문의하십시오. `at.js 2.*x*`

*읽기 횟수*

* [Target 작동 방식](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html){target=_blank}
* [at.js 작동 방식](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
* [태그 관리자 없이 Target 구현](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

**작업**

실험, 최적화, 개인화 및 데이터 수집이 일어나야 하는 모든 웹 페이지에 at.js 파일을 포함합니다.

+++

[이 페이지 상단의 다이어그램으로 돌아갑니다.](#diagram)





























