---
title: Java SDK를 사용하여  [!DNL Adobe Target] 에 디스플레이 또는 클릭 알림 보내기
description: 측정 및 보고를 위해 sendNotifications()를 사용하여 디스플레이를 보내거나  [!DNL Adobe Target] 에 알림을 클릭하는 방법에 대해 알아봅니다.
feature: APIs/SDKs
exl-id: 9231b480-f50f-40d1-ab06-0b9f2a2d79e3
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 2%

---

# 알림 보내기(Java)

## 설명

`sendNotifications()`은(는) 측정 및 보고를 위해 [!DNL Adobe Target]에게 디스플레이 또는 클릭 알림을 보내는 데 사용됩니다.

>[!NOTE]
>
>필수 매개 변수가 있는 `execute` 개체가 요청 자체에 있으면 자격 있는 활동에 대해 자동으로 노출이 증가합니다.

노출을 자동으로 증가시키는 SDK 메서드는 다음과 같습니다.

* `getOffers()`
* `getAttributes()`

요청 내에서 `prefetch` 개체가 전달되면 `prefetch` 개체 내에 mbox가 있는 활동에 대한 노출이 자동으로 증가하지 않습니다. `sendNotifications()`은(는) 노출 및 전환을 늘리기 위해 미리 가져온 경험에 사용해야 합니다.

## 방법

### 만들기

```javascript {line-numbers="true"}
ResponseStatus TargetClient.sendNotifications(TargetDeliveryRequest request)
```

## 예

먼저 `home` 및 `product1` mbox에 대한 콘텐츠를 미리 가져오기 위한 [!DNL Target Delivery API] 요청을 빌드해 보겠습니다.

### 미리 가져오기

```javascript {line-numbers="true"}
List<MboxRequest> mboxRequests = new ArrayList<>();
mboxRequests.add((MboxRequest) new MboxRequest().name("home").index(1));
mboxRequests.add((MboxRequest) new MboxRequest().name("product1").index(2));
PrefetchRequest prefetchMboxesRequest = new PrefetchRequest().setMboxes(mboxRequests)

// Next, we fetch the offers via Target Java SDK getOffers() API
TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
```

성공적인 응답에는 요청된 mbox에 대해 미리 가져온 콘텐츠가 포함된 [!UICONTROL Target Delivery API] 응답 개체가 포함됩니다. 샘플 `targetResponse.response` 개체는 다음과 같을 수 있습니다.

### 응답

```javascript {line-numbers="true"}
{
  "status": 200,
  "requestId": "e8ac2dbf5f7d4a9f9280f6071f24a01e",
  "id": {
    "tntId": "08210e2d751a44779b8313e2d2692b96.21_27"
  },
  "client": "adobetargetmobile",
  "edgeHost": "mboxedge21.tt.omtrdc.net",
  "prefetch": {
    "mboxes": [
      {
        "index": 0,
        "name": "home",
        "options": [
          {
            "type": "html",
            "content": "HOME OFFER",
            "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
            "responseTokens": {
              "profile.memberlevel": "0",
              "geo.city": "dublin",
              "activity.id": "302740",
              "experience.name": "Experience B",
              "geo.country": "ireland"
            }
          }
        ],
        "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
      },
      {
        "index": 1,
        "name": "product1",
        "options": [
          {
            "type": "html",
            "content": "TEST OFFER 1",
            "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
            "responseTokens": {
              "profile.memberlevel": "0",
              "geo.city": "dublin",
              "activity.id": "302740",
              "experience.name": "Experience B",
              "geo.country": "ireland"
            }
          }
        ],
        "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
      }
    ]
  }
}
```

각 [!DNL Target] 콘텐츠 옵션에서 mbox `name` 및 `state` 필드와 `eventToken` 필드를 확인합니다. 각 콘텐츠 옵션이 표시되는 즉시 `sendNotifications()` 요청에 제공해야 합니다. `product1` mbox가 브라우저가 아닌 장치에 표시되었다고 가정해 보겠습니다. 알림 요청은 다음과 같이 표시됩니다.

### 요청

```javascript {line-numbers="true"}
TargetDeliveryRequest mboxNotificationRequest = TargetDeliveryRequest.builder().notifications(new ArrayList() {{
    add(new Notification()
            .id("1")
            .timestamp(System.currentTimeMillis())
            .type(MetricType.DISPLAY)
            .mbox(new NotificationMbox()
                    .name("product1")
                    .state("J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U")
            )
            .tokens(Arrays.asList(new String[]{"t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="}))
    );
}}).build();
```

미리 가져오기 응답에 전달된 [!DNL Target] 오퍼에 해당하는 이벤트 토큰과 mbox 상태가 모두 포함되었습니다. 알림 요청을 빌드하면 `sendNotifications()` API 메서드를 통해 [!DNL Target]에 보낼 수 있습니다.

### 응답

```javascript {line-numbers="true"}
ResponseStatus notificationResponse = targetJavaClient.sendNotifications(mboxNotificationRequest);
```
