---
title: 에서 비동기 요청을 사용하는 방법 [!DNL Adobe Target] .NET SDK
description: 방법 알아보기 [!DNL Target] Java SDK는 비동기 요청을 지원하므로 유효 타겟 시간을 0으로 줄일 수 있습니다.
feature: APIs/SDKs
exl-id: fd36cc7b-a884-4e57-93c2-8aff8256109a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 4%

---

# 비동기 요청(.NET)

## 설명

서버 측 통합의 한 가지 이점은 병렬 처리를 사용하여 서버 측에서 사용할 수 있는 엄청난 대역폭과 컴퓨팅 리소스를 활용할 수 있다는 것입니다. [!DNL Target] .NET SDK는 비동기 요청을 지원하므로 쉽게 통합할 수 있습니다 [!DNL Target] 를 앱의 기존 비동기 워크플로에 추가합니다.

## 지원되는 메서드

### \.NET

```dotnet {line-numbers="true"}
Task<TargetDeliveryResponse> GetOffersAsync(TargetDeliveryRequest request);
Task<TargetDeliveryResponse> SendNotificationsAsync(TargetDeliveryRequest request);
Task<TargetAttributes> GetAttributesAsync(TargetDeliveryRequest request, params string[] mboxes);
```

## 예

샘플 비동기 SDK API 사용은 다음과 같이 나타날 수 있습니다.

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

이 예에서는 다음과 같은 항목이 있다고 가정합니다. [sdk 초기화](initialize-sdk.md).
