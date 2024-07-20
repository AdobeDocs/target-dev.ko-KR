---
title: .NET SDK를 사용하여  [!DNL Adobe Target] 에 디스플레이 또는 클릭 알림 보내기
description: 측정 및 보고를 위해 sendNotifications()를 사용하여 디스플레이를 보내거나  [!DNL Adobe Target] 에 알림을 클릭하는 방법에 대해 알아봅니다.
feature: APIs/SDKs
exl-id: 724e787c-af53-4152-8b20-136f7b5452e1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 1%

---

# 알림 보내기(.NET)

## 설명

`SendNotifications()`은(는) 측정 및 보고를 위해 [!DNL Adobe Target]에게 디스플레이 또는 클릭 알림을 보내는 데 사용됩니다.

>[!NOTE]
>
>필수 매개 변수가 있는 `Execute` 개체가 요청 자체에 있으면 자격 있는 활동에 대해 자동으로 노출이 증가합니다.

노출을 자동으로 증가시키는 SDK 메서드는 다음과 같습니다.

* `GetOffers()`
* `GetAttributes()`

요청 내에서 `Prefetch` 개체가 전달되면 `Prefetch` 개체 내에 mbox가 있는 활동에 대한 노출이 자동으로 증가하지 않습니다. `SendNotifications()`은(는) 노출 및 전환을 늘리기 위해 미리 가져온 경험에 사용해야 합니다.

## 방법

### 선택 사항에서

```dotnet {line-numbers="true"}
TargetDeliveryResponse TargetClient.SendNotifications(TargetDeliveryRequest request)
```

## 예

먼저 `home` 및 `product1` mbox에 대한 콘텐츠를 미리 가져오기 위한 [!UICONTROL Target Delivery API] 요청을 빌드해 보겠습니다.

### \.NET

```dotnet {line-numbers="true"}
var mboxRequests = new List<MboxRequest>
    {
        new (index: 1, name: "home"),
        new (index: 2, name: "product1"),
    };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .SetPrefetch(new PrefetchRequest(mboxes: mboxRequests))
    .Build();

// Next, we fetch the offers via Target .NET SDK GetOffers() API
var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
```

성공적인 응답에는 요청된 mbox에 대해 미리 가져온 콘텐츠가 포함된 [!DNL Target Delivery API] 응답 개체가 포함됩니다. 샘플 `targetResponse.Response` 개체는 다음과 같이 표시될 수 있습니다.

### \.NET

```dotnet {line-numbers="true"}
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

각 [!DNL Target] 콘텐츠 옵션에서 `mbox` 이름 및 `state` 필드와 `eventToken` 필드를 메모하십시오. 각 콘텐츠 옵션이 표시되는 즉시 `SendNotifications()` 요청에 제공해야 합니다. `product1` mbox가 브라우저가 아닌 장치에 표시되었다고 가정해 보겠습니다. 알림 요청은 다음과 같이 표시됩니다.

### \.NET

```dotnet {line-numbers="true"}
var mboxNotifications = new List<Notification>
{
    new (id: "1", type: MetricType.Display, timestamp: DateTimeOffset.UtcNow.ToUnixTimeMilliseconds(),
        mbox: new NotificationMbox("product1", "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"),
        tokens: new List<string> { "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==" })
}; 

var mboxNotificationRequest = new TargetDeliveryRequest.Builder()
    .SetNotifications(mboxNotifications)
    .Build();
```

미리 가져오기 응답에 전달된 [!DNL Target] 오퍼에 해당하는 이벤트 토큰과 mbox 상태가 모두 포함되어 있습니다. 알림 요청을 빌드하면 `SendNotifications()` API 메서드를 통해 [!DNL Target]에 보낼 수 있습니다.

### \.NET

```dotnet {line-numbers="true"}
var notificationResponse = targetClient.SendNotifications(mboxNotificationRequest);
```
