---
title: Adobe Target SDK를 사용하여 개인화 게재
description: '[!UICONTROL 온디바이스 의사 결정]을 사용하여 개인화를 전달하는 방법을 알아봅니다.'
feature: APIs/SDKs
exl-id: bac64c78-0d3a-40d7-ae2b-afa0f1b8dc4f
TQID: https://experienceleague.adobe.com/IufE4ByFgQ8WwHZ5YVHbbyvN6jBBNGCK4IC98m9zGsc
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 587
ht-degree: 1%

---

# 개인화 게재

## 단계 요약

1. 조직에 대해 [!UICONTROL 온디바이스 의사 결정] 사용
1. [!UICONTROL 경험 타깃팅]&#x200B;(XT) 활동 만들기
1. 대상자별 개인화된 경험 정의
1. 대상자당 개인화된 경험 확인
1. 보고 설정
1. KPI 추적을 위한 지표 추가
1. 애플리케이션에서 개인화된 오퍼 구현
1. 전환 이벤트를 추적하는 코드 구현
1. [!UICONTROL 경험 타깃팅]&#x200B;(XT) 개인화 활동 활성화

당신이 여행사라고 가정해 보세요. 특정 여행 패키지를 25% 할인된 가격으로 맞춤형 오퍼를 제공하고자 합니다. 오퍼가 사용자에게 반향을 일으키도록 하려면 대상 도시의 랜드마크를 표시하기로 합니다. 또한 개인화된 오퍼의 게재가 거의 0에 가까운 지연 시간에 실행되어 사용자 경험에 부정적인 영향을 주지 않고 결과를 왜곡하려고 합니다.

## &#x200B;1. 조직에 대해 [!UICONTROL 온디바이스 의사 결정] 사용

1. 온디바이스 의사 결정을 활성화하면 A/B 활동이 거의 0에 가까운 지연 시간에 실행됩니다. 이 기능을 사용하려면 [!DNL Adobe Target]에서 **[!UICONTROL 관리]** > **[!UICONTROL 구현]** > **[!UICONTROL 계정 세부 정보]**(으)로 이동한 다음 **[!UICONTROL 디바이스에서 의사 결정]** 전환을 사용하도록 설정하십시오.

   ![대체 이미지](assets/asset-odd-toggle.png)

   >[!NOTE]
   >
   >[!UICONTROL 디바이스에서 의사 결정] 전환을 활성화하거나 비활성화하려면 관리자 또는 승인자 [사용자 역할](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html)이(가) 있어야 합니다.

   **[!UICONTROL 디바이스에서 의사 결정]** 전환을 활성화한 후 [!DNL Adobe Target]에서 클라이언트에 대한 *규칙 아티팩트*&#x200B;를 생성하기 시작합니다.

## &#x200B;2. [!UICONTROL 경험 타깃팅]&#x200B;(XT) 활동 만들기

1. [!DNL Adobe Target]에서 **[!UICONTROL 활동]** 페이지로 이동한 다음 **[!UICONTROL 활동 만들기]** > **[!UICONTROL 경험 타깃팅]**&#x200B;을 선택합니다.

   ![대체 이미지](assets/asset-xt.png)

1. **[!UICONTROL 경험 타깃팅 활동 만들기]** 모달에서 기본 **[!UICONTROL Web]** 옵션을 선택한 상태로 둡니다(1). **[!UICONTROL Form]**&#x200B;을(를) 경험 작성기로 선택합니다(2). 작업 공간 및 속성을 선택합니다(3). **[!UICONTROL 다음]**(4)을 클릭합니다.

   ![대체 이미지](assets/asset-xt-next.png)

## &#x200B;3. 대상자별 개인화된 경험 정의

1. 활동 만들기 **[!UICONTROL 경험]** 단계에서 **[!UICONTROL 대상 변경]**&#x200B;을 클릭하여 캘리포니아주 샌프란시스코로 여행하려는 방문자의 대상을 만듭니다.

   ![대체 이미지](assets/asset-change-audience.png)

1. **[!UICONTROL 대상 만들기]** 모달에서 `destinationCity = San Francisco`인 사용자 지정 규칙을 정의합니다. 이는 샌프란시스코로 이동하고자 하는 사용자 그룹을 정의합니다.

   ![대체 이미지](assets/asset-audience-sf.png)

1. **[!UICONTROL 경험]** 단계에서 골든 게이트 Bridge에 대한 특별 오퍼를 렌더링할 응용 프로그램 내 위치(1)의 이름을 입력하십시오. 단, 샌프란시스코로 이동하는 경우에만 가능합니다. 여기에 표시된 예에서 홈 페이지는 **[!UICONTROL 컨텐츠]** 영역에 정의된 HTML 오퍼(2)에 대해 선택한 위치입니다.

   ![대체 이미지](assets/asset-content-sf.png)

1. **[!UICONTROL 경험 타깃팅 추가]**&#x200B;를 클릭하여 다른 타깃팅 대상을 추가하십시오. 이번에는 `destinationCity = New York`인 대상 규칙을 정의하여 New York으로 이동하려는 대상을 타기팅합니다. 응용 프로그램 내에서 엠파이어 스테이트 빌딩에 대한 특별 오퍼를 렌더링할 위치를 정의합니다. 여기에 표시된 예에서 `homepage`은(는) **[!UICONTROL 콘텐츠]** 영역에 정의된 HTML 오퍼(2)에 대해 선택한 위치입니다.

   ![대체 이미지](assets/asset-content-ny.png)

## &#x200B;4. 대상자당 개인화된 경험 확인

**[!UICONTROL 타깃팅]** 단계에서 대상자별로 원하는 개인화된 경험을 구성했는지 확인하십시오.

![대체 이미지](assets/asset-verify-sf-ny.png)

## &#x200B;5. 보고 설정

**[!UICONTROL 목표 및 설정]** 단계에서 **[!UICONTROL Adobe Target 보고]**(으)로 **[!UICONTROL Source]**&#x200B;을(를) 선택하여 [!DNL Adobe Target] UI에서 활동 결과를 보거나 **[!UICONTROL Adobe Analytics]**&#x200B;을(를) 선택하여 Adobe Analytics UI에서 활동 결과를 봅니다.

![대체 이미지](assets/asset-reporting-sf-ny.png)

## &#x200B;6. KPI 추적을 위한 지표 추가

**[!UICONTROL 목표 지표]**&#x200B;를 선택하여 활동의 성공을 측정합니다. 이 예에서 성공적인 전환은 사용자가 개인화된 대상 오퍼를 클릭하는지 여부를 기반으로 합니다.

## &#x200B;7. 애플리케이션에서 개인화된 오퍼 구현

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {      
    execute: {
      pageLoad: {
        parameters: {
          destinationCity: "San Francisco"
        }
      }
    }       
  }
})
.then(console.log)
.catch(console.error);
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

RequestDetails pageLoad = new RequestDetails();
pageLoad.setParameters(
    new HashMap<String, String>() {
      {
        put("destinationCity", "San Francisco");
      }
    });

executeRequest.setPageLoad(pageLoad);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

## &#x200B;8. 전환 이벤트를 추적하는 코드 구현

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
            name : "destinationOffer"
          }
        }
      ]
    }
})
```

>[!TAB Java]

```java {line-numbers="true"
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);

ExecuteRequest executeRequest = new ExecuteRequest();

RequestDetails pageLoad = new RequestDetails();
pageLoad.setParameters(
    new HashMap<String, String>() {
      {
        put("destinationCity", "San Francisco");
      }
    });

executeRequest.setPageLoad(pageLoad);
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
```

>[!ENDTABS]

## &#x200B;9. XT(경험 타깃팅) 활동 활성화

![대체 이미지](assets/asset-xt-activate.png)
