---
title: 타겟에게 알림
description: 추적할 필요가 있는 모든 이벤트를 [!DNL Target] trackEvent 메서드를 사용하여 전송됩니다.
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 7a79eb1d263cf42529a5a1b1ca1f9de4db218a49
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 1%

---

# 알림 [!DNL Target]

이 단계를 완료하면 전송해야 하는 모든 이벤트를 [!DNL Adobe Target] 을 사용하여 전송됩니다. `trackEvent` 메서드를 사용합니다.

추적해야 하는 모든 이벤트 [!DNL Target] 는 기본 전환 이벤트 또는 성공 지표일 수 있습니다.

>[!TIP]
>
>전체 화면으로 확장하려면 이 항목의 이미지를 클릭하십시오.

## 알림 [!DNL Target] 다이어그램 {#diagram}

다음 그림의 단계 번호는 아래 섹션에 해당합니다.

![대상 다이어그램에 알림](/help/dev/patterns/recs-atjs/assets/diagram-notify-target.png){width="600" zoomable="yes"}

## Fire [!DNL Adobe Target] API 추적

이 단계는 로 전송해야 하는 모든 이벤트를 확인하는 데 도움이 됩니다 [!DNL Target] 을 사용하여 전송됩니다. `trackEvent` 메서드를 사용합니다.

+++세부 정보 보기

![Adobe Target 추적 API 다이어그램 실행](/help/dev/patterns/recs-atjs/assets/fire-adobe-target-track-api-diagram.png){width="300" zoomable="yes"}

에 언급된 대로 주문 전환 속성을 보냅니다. *전제 조건* 아래 섹션. mbox 이름은 중요하지 않지만 변환은 를 사용하는 것입니다 `orderConfirmPage`.

이 호출에는 주문 전환 속성을 포함할 필요가 없습니다. 이러한 호출은 기본 전환 이벤트 전에 미니 전환 이벤트로 간주할 수 있는 성공 지표를 이상적으로 기록합니다. `CardIds` 다음을 기반으로 장바구니 기반 권장 사항에 포함해야 합니다. `Add to Cart` 이벤트.

**전제 조건**

* 비즈니스 팀과 만나 전환 또는 성공 지표로 간주할 수 있는 모든 이벤트를 식별합니다. 또한 매출을 생성하는 전환 이벤트를 식별해야 해당 세부 정보를 (으)로 보낼 수 있습니다. [!DNL Target] 이벤트 데이터와 함께
* 전환 이벤트와 함께 보낼 수 있도록 데이터 레이어에서 다음 속성을 사용할 수 있는지 확인합니다. 전환 이벤트는 제품 구매 또는 장바구니에 추가 이벤트와 같은 매출을 생성합니다.

   * `productPurchaseId`: 주문의 일부로 구매한 제품 ID입니다. 쉼표를 사용하여 여러 제품을 구분하십시오.
   * `orderTotal`: 구매에 대한 주문 총액.
   * `orderId`: 구매의 주문 ID입니다.

* 장바구니 추가에 대한 이벤트를 추적하는 경우 `cartIds` 를 매개 변수로 사용하십시오. 에 대해 쉼표로 구분된 제품 ID 목록을 전달할 수 있습니다. `cardIds`.

**읽기 횟수**

* [adobe.target.trackEvent() 메서드](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
* [장바구니 기반 기준의 cartIds](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based){target=_blank}

**작업**

* 사용 `adobe.target-trackEvent()` 전송해야 하는 모든 데이터를 전송하는 메서드 [!DNL Target].







