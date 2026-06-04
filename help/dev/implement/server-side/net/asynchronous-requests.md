---
title: ' [!DNL Adobe Target] .NET SDK에서 비동기 요청을 사용하는 방법'
description: ' [!DNL Target] Java SDK이 효과적인 대상 시간을 0으로 줄일 수 있는 비동기 요청을 지원하는 방법에 대해 알아봅니다.'
feature: APIs/SDKs
exl-id: fd36cc7b-a884-4e57-93c2-8aff8256109a
TQID: https://experienceleague.adobe.com/E9rNmPdXe7HYg7XlIffpC4opGM9X6fFoHK-u0oLI-XE
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 91
ht-degree: 4%

---

# 비동기 요청(.NET)

## 설명

서버 측 통합의 한 가지 이점은 병렬 처리를 사용하여 서버 측에서 사용할 수 있는 엄청난 대역폭과 컴퓨팅 리소스를 활용할 수 있다는 것입니다. [!DNL Target] .NET SDK은 비동기 요청을 지원하므로 [!DNL Target]을(를) 앱의 기존 비동기 워크플로우에 쉽게 통합할 수 있습니다.

## 지원되는 메서드

### \.NET

```dotnet {line-numbers="true"}
Task<TargetDeliveryResponse> GetOffersAsync(TargetDeliveryRequest request);
Task<TargetDeliveryResponse> SendNotificationsAsync(TargetDeliveryRequest request);
Task<TargetAttributes> GetAttributesAsync(TargetDeliveryRequest request, params string[] mboxes);
```

## 예

비동기 SDK API 사용 샘플은 다음과 같이 표시될 수 있습니다.

### \.NET

```dotnet {line-numbers="true"}
var deliveryRequest = new TargetDeliveryRequest.Builder()
    .SetExecute(new ExecuteRequest(mboxes: new List<MboxRequest> { new MboxRequest(index: 1, name: "a1-serverside-ab") }))
    .Build();

var response = await this.targetClient.GetOffersAsync(deliveryRequest);

var notificationRequest = new TargetDeliveryRequest.Builder()
    .SetSessionId(response.Request.SessionId)
    .SetTntId(response.Response?.Id?.TntId)
    .SetNotifications(new List<Notification>
        {
            new (id: "1", type: MetricType.Display, timestamp: DateTimeOffset.UtcNow.ToUnixTimeMilliseconds(),
                mbox: new NotificationMbox("product1", "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"),
                tokens: new List<string> { "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==" })
        })
    .Build();

var notificationResponse = await this.targetClient.SendNotificationsAsync(notificationRequest);
```

이 예제에서는 사용자가 [SDK을 초기화했습니다](initialize-sdk.md)라고 가정합니다.
