---
title: Python SDK을 사용하여  [!DNL Adobe Target] 에 디스플레이 또는 클릭 알림 보내기
description: 측정 및 보고를 위해 sendNotifications()를 사용하여 디스플레이를 보내거나  [!DNL Adobe Target] 에 알림을 클릭하는 방법에 대해 알아봅니다.
feature: APIs/SDKs
exl-id: 03827b18-a546-4ec8-8762-391fcb3ac435
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 8%

---

# 알림 보내기(Python)

## 설명

`send_notifications()`은(는) 측정 및 보고를 위해 [!DNL Adobe Target]에게 디스플레이 또는 클릭 알림을 보내는 데 사용됩니다.

>[!NOTE]
>
>필수 매개 변수가 있는 `execute` 개체가 요청 자체에 있으면 자격 있는 활동에 대해 자동으로 노출이 증가합니다.

노출을 자동으로 증가시키는 SDK 메서드는 다음과 같습니다.

* `get_offers()`
* `get_attributes()`

요청 내에서 `prefetch` 개체가 전달되면 `prefetch` 개체 내에 mbox가 있는 활동에 대한 노출이 자동으로 증가하지 않습니다. `Send_notifications()`은(는) 노출 및 전환을 늘리기 위해 미리 가져온 경험에 사용해야 합니다.

## 방법

### send_notifications

```python {line-numbers="true"}
target_client.send_notifications(options)
```

## 매개변수

`options`의 구조는 다음과 같습니다.

| 이름 | 유형 | 필수 | 기본값 | 설명 |
| --- | --- | --- | --- | --- |
| 요청 | DeliveryRequest | 예 | 없음 | [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) 요청 준수 |
| target_cookie | str | no | 없음 | [!DNL Target] 쿠키 |
| target_location_hint | str | no | 없음 | [!DNL Target] 위치 힌트 |
| consumer_id | str | no | 없음 | 여러 호출을 결합할 때 서로 다른 소비자 ID가 제공되어야 합니다 |
| customer_ids | list[CustomerId] | no | 없음 | VisitorId 호환 형식의 고객 ID 목록 |
| session_id | str | no | 없음 | 여러 요청을 연결하는 데 사용됨 |
| callback | 호출 가능 | no | 없음 | 요청을 비동기식으로 처리하는 경우 응답이 준비되면 콜백이 호출됩니다 |
| err_callback | 호출 가능 | no | 없음 | 요청을 비동기적으로 처리하는 경우 예외가 발생하면 오류 콜백이 호출됩니다 |

## 반환

`Returns`을(를) 동기적으로 호출하는 경우 `TargetDeliveryResponse`(기본값) 또는 콜백으로 호출하는 경우 `AsyncResult`을(를) 호출합니다. `TargetDeliveryResponse`의 구조는 다음과 같습니다.

| 이름 | 유형 | 설명 |
| --- | --- | --- |
| 응답 | DeliveryResponse | [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) 응답 준수 |
| target_cookie | dict | [!DNL Target] 쿠키 |
| target_location_hint_cookie | dict | [!DNL Target] 위치 힌트 쿠키 |
| analytics_details | list[AnalyticsResponse] | 클라이언트측 [!DNL Analytics] 사용의 경우 [!DNL Analytics] 페이로드 |
| 추적 | list[dict] | 모든 요청 mbox/보기에 대해 집계된 추적 데이터 |
| response_tokens | list[dict] | [&#x200B; 응답 토큰 &#x200B; 목록](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=ko) |
| meta | dict | 온디바이스 의사 결정에 사용하기 위한 추가 의사 결정 메타데이터 |

## 예

먼저 [!UICONTROL Target Delivery API] 및 `home` mbox에 대한 콘텐츠를 미리 가져오기 위한 `product1` 요청을 빌드해 보겠습니다.

### Python

```python {line-numbers="true"}
mboxes = [MboxRequest(name="home"),
          MboxRequest(name="product1")]
prefetch = PrefetchRequest(mboxes=mboxes)
delivery_request = DeliveryRequest(prefetch=prefetch)

# Next, we fetch the offers via Target Python SDK getOffers() API
response = target_client.get_offers({ "request": delivery_request })
```

성공적인 응답에는 요청된 mbox에 대해 미리 가져온 콘텐츠가 포함된 [!UICONTROL Target Delivery API] 응답 개체가 포함됩니다. 샘플 `target_response["response"]` 개체(dict 형식)는 다음과 같이 나타날 수 있습니다.

### Python

```python {line-numbers="true"}
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

각 Target 콘텐츠 옵션에서 mbox `name` 및 `state` 필드와 `eventToken` 필드를 확인합니다. 각 콘텐츠 옵션이 표시되는 즉시 `send_notifications()` 요청에 제공해야 합니다. `product1` mbox가 브라우저가 아닌 장치에 표시되었다고 가정해 보겠습니다. 알림 요청은 다음과 같이 표시됩니다.

### Python

```python {line-numbers="true"}
notification_mbox = NotificationMbox(name="product1",
                                     state="J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U")
notification = Notification(
    id="1",
    type=MetricType.DISPLAY,
    timestamp=1621530726000,  # Epoch time in milliseconds
    mbox=notification_mbox,
    tokens=["t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="]
)
notification_request = DeliveryRequest(notifications=[notification])
```

미리 가져오기 응답에 전달된 [!DNL Target] 오퍼에 해당하는 이벤트 토큰과 mbox 상태가 모두 포함되어 있습니다. 알림 요청을 빌드하면 [!DNL Target] API 메서드를 통해 `send_notifications()`에 보낼 수 있습니다.

### Python

```python {line-numbers="true"}
response = target_client.send_notifications({ "request": notification_request })
```
