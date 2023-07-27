---
title: 속성을 사용하여 기능 테스트 실행
description: 속성을 사용하여 기능 테스트 실행
feature: APIs/SDKs
exl-id: c89d337c-20a9-454c-930c-79d9217e23b6
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---

# 속성을 사용하여 기능 테스트 실행

## 단계 요약

1. 사용 [!UICONTROL 온디바이스 의사 결정] (조직)
1. 만들기 [!UICONTROL A/B 테스트] 활동
1. A 및 B 정의
1. 대상자 추가
1. 트래픽 할당 설정
1. 트래픽 분포를 변형으로 설정
1. 보고 설정
1. KPI 추적을 위한 지표 추가
1. 속성을 사용하여 기능 테스트를 실행하는 코드 구현
1. 전환 이벤트를 추적하는 코드 구현
1. 속성을 사용하여 기능 테스트 활성화

>[!NOTE]
>
>소매 전자 상거래 회사라고 가정합니다. 고객이 제품 카탈로그를 검색하고 정렬할 때 전환율을 높이려고 합니다. 특정 정렬 알고리즘과 페이지 매김 전략이 다른 것보다 더 나은 결과를 얻는다는 가설이 있습니다. 이러한 이론을 테스트하기 위해 최종 사용자를 위한 다양한 정렬 옵션을 사용하여 정렬 위젯의 재설계와 관련된 기능 테스트를 실행하도록 결정합니다. 이 기능 테스트가 거의 0에 가까운 지연에서 실행되어 사용자 경험에 부정적인 영향을 주지 않고 결과를 왜곡하지 않도록 하려는 경우

## 1. 활성화 [!UICONTROL 온디바이스 의사 결정] (조직)

온디바이스 의사 결정을 활성화하면 A/B 활동이 거의 0에 가까운 지연 시간에 실행됩니다. 이 기능을 사용하려면 다음 위치로 이동하십시오. **[!UICONTROL 관리]** > **[!UICONTROL 구현]** > **[!UICONTROL 계정 세부 정보]** 위치: [!DNL Adobe Target], 및 활성화 **[!UICONTROL 온디바이스 의사 결정]** 토글.

![대체 이미지](assets/asset-odd-toggle.png)

>[!NOTE]
>
>관리자 또는 승인자가 있어야 합니다. [사용자 역할](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) 을(를) 활성화 또는 비활성화하려면 **[!UICONTROL 온디바이스 의사 결정]** 토글.

활성화 후 **[!UICONTROL 온디바이스 의사 결정]** 전환, [!DNL Adobe Target] 생성 시작 *규칙 아티팩트* 클라이언트.

## 2. 만들기 [!UICONTROL A/B 테스트] 활동

1. 위치 [!DNL Adobe Target]로 이동한 다음 **[!UICONTROL 활동]** 페이지를 선택한 다음 **[!UICONTROL 활동 만들기]** > **[!UICONTROL A/B 테스트]**.

   ![대체 이미지](assets/asset-ab.png)

1. 다음에서 **[!UICONTROL A/B 테스트 활동 만들기]** 모달, 기본값 유지 **[!UICONTROL 웹]** 옵션 선택됨 (1), 선택 **[!UICONTROL 양식]** 경험 작성기 (2)로서 **[!UICONTROL 기본 작업 영역]** 포함 **[!UICONTROL 속성 제한 없음]** (3) 및 클릭 **[!UICONTROL 다음]** (4)

   ![대체 이미지](assets/asset-form.png)

## 3. A 및 B 정의

1. 다음에서 **[!UICONTROL 경험]** 활동 만들기 단계에서 활동(1)의 이름을 입력하고 다음을 클릭하여 두 번째 경험인 경험 B를 추가합니다. **[!UICONTROL 경험 추가]** (2) 단추. 속성을 사용하여 기능 테스트를 실행할 응용 프로그램 내의 위치(3)의 이름을 입력합니다. 아래 표시된 예에서는 `product-results-page` 은 경험 A에 대해 정의된 위치입니다. (또한 경험 B에 대해 정의된 위치입니다.)

   ![대체 이미지](assets/asset-location.png)

   **[!UICONTROL 경험 A]** 은 비즈니스 논리에 다음과 같은 작업을 수행하도록 신호를 보내는 JSON을 포함합니다.

   * 를 통해 정렬 알고리즘 기능 시작 `test_sorting` 기능 플래그
   * 에 정의된 권장 정렬 알고리즘 실행 `sorting_algorithm _**_attribute`
   * 에 정의된 페이지 매김 전략에 정의된 대로 페이지당 50개 제품 반환 `pagination_limit`

1. 경험 A에서 을(를) 클릭하여 콘텐츠를 다음으로 변경합니다. **[!UICONTROL 기본 컨텐츠]** 을 선택하여 JSON에 추가 **[!UICONTROL JSON 오퍼 만들기]** 아래 (1)과 같이.

   ![대체 이미지](assets/asset-offer.png)

1. 다음을 사용하여 JSON 정의 `test_sorting`, `sorting_algorithm`, 및 `pagination_limit` 페이지 매김 제한이 50개인 권장 정렬 알고리즘을 시작하는 데 사용되는 플래그 및 속성입니다.

   >[!NOTE]
   >
   >날짜 [!DNL Adobe Target] 사용자를 버킷팅하여 경험 A를 봅니다. 그러면 예제에 정의된 속성이 포함된 JSON이 반환됩니다. 코드에서 기능 플래그의 값을 확인해야 합니다 `test_sorting` 을 클릭하여 정렬 기능을 켜야 하는지 확인합니다. 이 경우 의 권장 값을 사용합니다. `sorting_algorithm` 제품 목록 보기에서 추천 제품을 표시하는 속성입니다. 애플리케이션에 표시되는 제품의 한도는 50입니다. 이 값은 `pagination_limit` 특성.

   ![대체 이미지](assets/asset-sorting.png)

   **[!UICONTROL 경험 B]** 는 비즈니스 논리에 다음과 같은 작업을 수행하도록 신호를 보내는 JSON을 정의합니다.

   * test_sorting 기능 플래그를 통해 정렬 알고리즘 기능 시작
   * 실행 `best_sellers` 에 정의된 정렬 알고리즘 `sorting_algorithm _**_attribute`
   * 에 정의된 페이지 매김 전략에 정의된 대로 페이지당 50개 제품 반환 `pagination_limit`

   >[!NOTE]
   >
   >날짜 [!DNL Adobe Target] 사용자가 경험 B를 볼 수 있도록 버킷팅하면 예제에 정의된 속성이 있는 JSON이 반환됩니다. 코드에서 기능 플래그의 값을 확인해야 합니다 `test_sorting` 을 클릭하여 정렬 기능을 켜야 하는지 확인합니다. 이 경우 다음을 사용합니다. `best_sellers` 값 `sorting_algorithm` 제품 목록 보기에서 베스트셀러 제품을 표시하는 속성. 애플리케이션에 표시되는 제품의 한도는 50입니다. 이 값은 `pagination_limit` 특성.

   ![대체 이미지](assets/asset-sorting-b.png)

## 4. 대상자 추가

다음에서 **[!UICONTROL 타겟팅]** 단계, 유지 **[!UICONTROL 모든 방문자]** 대상입니다. 이렇게 하면 정렬 기능의 영향과 결과에 가장 큰 영향을 미치는 알고리즘 및 항목 수를 이해할 수 있습니다.

![대체 이미지](assets/asset-audience-b.png)

## 5. 트래픽 할당 설정

정렬 알고리즘 및 페이지 매김 전략을 테스트할 방문자의 비율을 정의합니다. 즉, 이 테스트를 롤아웃할 사용자의 비율은 얼마입니까? 이 예에서 이 테스트를 로그인한 모든 사용자에게 배포하려면 트래픽 할당을 100%로 유지합니다.

![대체 이미지](assets/asset-allocation-100.png)

## 6. 트래픽 분포를 변형으로 설정

페이지당 50개 제품 제한으로 권장 대 베스트셀러 정렬 알고리즘을 보게 되는 방문자의 비율을 정의합니다. 이 예에서는 트래픽 분포를 경험 A와 B 간에 50/50으로 분할합니다.

![대체 이미지](assets/asset-variations-50.png)

## 7. 보고 설정

다음에서 **[!UICONTROL 목표 및 설정]** 단계, 선택 **[!UICONTROL Adobe Target]** (으)로 **[!UICONTROL 보고 소스]** 에서 A/B 테스트 결과를 보려면 [!DNL Adobe Target] UI 또는 선택 **[!UICONTROL Adobe Analytics]** Adobe Analytics UI에서 이를 확인할 수 있습니다.

![대체 이미지](assets/asset-reporting-b.png)

## 8. KPI 추적을 위한 지표 추가

선택 **[!UICONTROL 목표 지표]** 속성을 사용하여 피쳐 테스트를 측정합니다. 이 예에서 성공은 표시된 정렬 알고리즘 및 페이지 매김 전략에 따라 사용자가 제품을 구매하는지 여부에 따라 결정됩니다.

## 9. 속성을 사용하여 기능 테스트를 애플리케이션에 구현합니다

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const options = {
  client: "testClient",
  organizationId: "ABCDEF012345677890ABCDEF0@AdobeOrg",
  decisioningMethod: "on-device",
  events: {
    clientReady: targetClientReady
  }
};
const targetClient = TargetClient.create(options);

function targetClientReady() {
  return targetClient.getAttributes(["product-results-page"]).then(function(attributes) {
    const test_sorting = attributes.getValue("product-results-page", "test-sorting");
    const sorting_algorithm = attributes.getValue("product-results-page", "sorting_algorithm");
    const pagination_limit = attributes.getValue("product-results-page", "pagination_limit");
  });
}
```

>[!TAB Java]

```java {line-numbers="true"}
import com.adobe.target.edge.client.ClientConfig;
import com.adobe.target.edge.client.TargetClient;
import com.adobe.target.delivery.v1.model.ChannelType;
import com.adobe.target.delivery.v1.model.Context;
import com.adobe.target.delivery.v1.model.ExecuteRequest;
import com.adobe.target.delivery.v1.model.MboxRequest;
import com.adobe.target.edge.client.entities.TargetDeliveryRequest;
import com.adobe.target.edge.client.model.TargetDeliveryResponse;

ClientConfig config = ClientConfig.builder()
    .client("testClient")
    .organizationId("ABCDEF012345677890ABCDEF0@AdobeOrg")
    .build();
TargetClient targetClient = TargetClient.create(config);
MboxRequest mbox = new MboxRequest().name("product-results-page").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
    .context(new Context().channel(ChannelType.WEB))
    .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
    .build();
Attributes attributes = targetClient.getAttributes(request, "product-results-page");
String testSorting = attributes.getString("product-results-page", "test-sorting");
String sortingAlgorithm = attributes.getString("product-results-page", "sorting_algorithm");
String paginationLimit = attributes.getString("product-results-page", "pagination_limit");
```

>[!ENDTABS]

## 10. 전환 이벤트를 추적하는 코드 구현

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity

//When a conversion happens
TargetClient.sendNotifications({
    targetCookie,
    "request" : {
      "notifications" : [
        {
          type: "click",
          timestamp : Date.now(),
          id: "conversion",
          mbox : {
            name : "product-results-page"
          }
        }
      ]
    }
})
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);

ExecuteRequest executeRequest = new ExecuteRequest();

NotificationDeliveryService notificationDeliveryService = new NotificationDeliveryService();

Notification notification = new Notification();
notification.setId("conversion");
notification.setImpressionId(UUID.randomUUID().toString());
notification.setType(MetricType.CLICK);
notification.setTimestamp(System.currentTimeMillis());
notification.setTokens(
    Collections.singletonList(
        "IbG2Jz2xmHaqX7Ml/YRxRGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="));

TargetDeliveryRequest targetDeliveryRequest =
    TargetDeliveryRequest.builder()
        .context(context)
        .execute(executeRequest)
        .notifications(Collections.singletonList(notification))
        .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
notificationDeliveryService.sendNotification(request);

Attributes attributes = targetClient.getAttributes(request, "product-results-page");
String testSorting = attributes.getString("product-results-page", "test-sorting");
String sortingAlgorithm = attributes.getString("product-results-page", "sorting_algorithm");
String paginationLimit = attributes.getString("product-results-page", "pagination_limit");
```

>[!ENDTABS]

## 11. 속성을 사용하여 기능 테스트 활성화

![대체 이미지](assets/asset-activate.png)
