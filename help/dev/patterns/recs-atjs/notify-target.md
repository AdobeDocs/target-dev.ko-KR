---
title: 타겟에게 알림
description: ' [!DNL Target] 에 의해 추적해야 하는 모든 이벤트가 trackEvent 메서드를 사용하여 전송되는지 확인합니다.'
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: efccadab-d139-4423-8613-c2743d87b3a0
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 1%

---

# [!DNL Target]에게 알림

이 단계를 완료하면 [!DNL Adobe Target] (으)로 전송해야 하는 모든 이벤트가 `trackEvent` 메서드를 사용하여 전송됩니다.

[!DNL Target]에서 추적해야 하는 모든 이벤트는 기본 전환 이벤트 또는 성공 지표일 수 있습니다.

>[!TIP]
>
>전체 화면으로 확장하려면 이 항목의 이미지를 클릭하십시오.

## [!DNL Target] 다이어그램 알림 {#diagram}

다음 그림의 단계 번호는 아래 섹션에 해당합니다.

![대상 다이어그램에 알림](/help/dev/patterns/recs-atjs/assets/diagram-notify-target.png){width="600" zoomable="yes"}

## 4.1: [!DNL Adobe Target] 추적 API 실행

이 단계는 [!DNL Target] (으)로 전송해야 하는 모든 이벤트를 `trackEvent` 메서드를 사용하여 전송하도록 하는 데 도움이 됩니다.

+++세부 정보 보기

![Adobe Target 추적 API 다이어그램 실행](/help/dev/patterns/recs-atjs/assets/fire-adobe-target-track-api-diagram-combined.png){width="400" zoomable="yes"}

아래 *필수 구성 요소* 섹션에 언급된 대로 주문 전환 특성을 보냅니다. mbox 이름은 상관없지만 `orderConfirmPage`을(를) 사용하도록 변환하는 것입니다.

이 호출에는 주문 전환 속성을 포함할 필요가 없습니다. 이러한 호출은 기본 전환 이벤트 전에 미니 전환 이벤트로 간주할 수 있는 성공 지표를 이상적으로 기록합니다. `CardIds`은(는) `Add to Cart` 이벤트를 기반으로 장바구니 기반 권장 사항에 포함되어야 합니다.

**전제 조건**

* 비즈니스 팀과 만나 전환 또는 성공 지표로 간주할 수 있는 모든 이벤트를 식별합니다. 또한 수익을 생성하는 전환 이벤트를 식별해야 해당 세부 정보를 이벤트 데이터와 함께 [!DNL Target] (으)로 보낼 수 있습니다.
* 전환 이벤트와 함께 보낼 수 있도록 데이터 레이어에서 다음 속성을 사용할 수 있는지 확인합니다. 전환 이벤트는 제품 구매 또는 장바구니에 추가 이벤트와 같은 매출을 생성합니다.

   * `productPurchaseId`: 주문의 일부로 구매한 제품 ID입니다. 쉼표를 사용하여 여러 제품을 구분하십시오.
   * `orderTotal`: 구매에 대한 주문 총계입니다.
   * `orderId`: 구매의 주문 ID.

  다음 그림은 [!UICONTROL Confirmation] 페이지에서만 실행해야 하는 [규칙  [!DNL tags] in [!DNL Experience Platform]](https://experienceleague.adobe.com/docs/tags.html?lang=ko){target=_blank}을(를) 보여 줍니다.

  ![작업 구성 페이지](/help/dev/patterns/recs-atjs/assets/action-configuration.png){width="400" zoomable="yes"}

* 장바구니 추가에 대한 이벤트를 추적하는 경우 `cartIds`을(를) 매개 변수로 보내십시오. `cardIds`에 대해 쉼표로 구분된 제품 ID 목록을 전달할 수 있습니다.

**판독값**

* [adobe.target.trackEvent() 메서드](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
* 장바구니 기반 기준용 [장바구니 ID](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=ko#cart-based){target=_blank}

**작업**

* `adobe.target-trackEvent()` 메서드를 사용하여 [!DNL Target] (으)로 전송해야 하는 모든 데이터를 보냅니다.
