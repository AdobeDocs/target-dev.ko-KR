---
title: 디스플레이 또는 클릭 알림 보내기 대상 [!DNL Adobe Target] Python SDK 사용
description: sendNotifications()를 사용하여 디스플레이 또는 클릭 알림을 보내는 방법 알아보기 [!DNL Adobe Target] 측정 및 보고용.
feature: APIs/SDKs
exl-id: 03827b18-a546-4ec8-8762-391fcb3ac435
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 8%

---

# 알림 보내기(Python)

## 설명

`send_notifications()` 디스플레이 또는 클릭 알림을 전송하는 데 사용됨 [!DNL Adobe Target] 측정 및 보고용.

>[!NOTE]
>
>다음의 경우 `execute` 필수 매개 변수가 있는 오브젝트가 요청 자체 내에 있는 경우 적격 활동에 대해 노출이 자동으로 증가합니다.

노출을 자동으로 증가시키는 SDK 메서드는 다음과 같습니다.

* `get_offers()`
* `get_attributes()`

다음과 같은 경우 `prefetch` 개체가 요청 내에 전달되고 mbox가 있는 활동에 대한 노출이 자동으로 증가하지 않습니다. `prefetch` 개체. `Send_notifications()` 노출 및 전환을 늘리기 위해 프리페치된 경험에 사용해야 합니다.

## 방법

### send_notifications

```python {line-numbers="true"}
target_client.send_notifications(options)
```

## 매개 변수

`options` 에는 다음 구조가 있습니다.

| 이름 | 유형 | 필수 | 기본값 | 설명 |
| --- | --- | --- | --- | --- |
| 요청 | DeliveryRequest | 예 | 없음 | 을 준수합니다. [[!UICONTROL Target 배달 API]](/help/dev/implement/delivery-api/overview.md) 요청 |
| target_cookie | str | no | 없음 | [!DNL Target] cookie |
| target_location_hint | str | no | 없음 | [!DNL Target] 지역 힌트 |
| consumer_id | str | no | 없음 | 여러 호출을 결합할 때 서로 다른 소비자 ID가 제공되어야 합니다 |
| customer_ids | 목록[고객 ID] | no | 없음 | VisitorId 호환 형식의 고객 ID 목록 |
| session_id | str | no | 없음 | 여러 요청을 연결하는 데 사용됨 |
| callback | 호출 가능 | no | 없음 | 요청을 비동기식으로 처리하는 경우 응답이 준비되면 콜백이 호출됩니다 |
| err_callback | 호출 가능 | no | 없음 | 요청을 비동기적으로 처리하는 경우 예외가 발생하면 오류 콜백이 호출됩니다 |

## 반환

`Returns` a `TargetDeliveryResponse` 를 동기식으로 호출하거나(기본값) `AsyncResult` 콜백과 함께 호출되는 경우입니다. `TargetDeliveryResponse` 에는 다음 구조가 있습니다.

| 이름 | 유형 | 설명 |
| --- | --- | --- |
| 응답 | DeliveryResponse | 을 준수합니다. [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) 응답 |
| target_cookie | dict | [!DNL Target] cookie |
| target_location_hint_cookie | dict | [!DNL Target] 위치 힌트 쿠키 |
| analytics_details | 목록[Analytics 응답] | [!DNL Analytics] 클라이언트측의 경우 페이로드 [!DNL Analytics] 사용 |
| 추적 |  | 목록[dict] | 모든 요청 mbox/보기에 대해 집계된 추적 데이터 |
| response_tokens | 목록[dict] | 의 목록 [응답 &#x200B; 토큰](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) |
| meta | dict | 온디바이스 의사 결정에 사용하기 위한 추가 의사 결정 메타데이터 |

## 예

먼저, 을 빌드합니다. [!UICONTROL Target 배달 API] 다음에 대한 콘텐츠 프리페치 요청 `home` 및 `product1` mbox.

### Python

```python {line-numbers="true"}
mboxes = [MboxRequest(name="home"),
          MboxRequest(name="product1")]
prefetch = PrefetchRequest(mboxes=mboxes)
delivery_request = DeliveryRequest(prefetch=prefetch)

# Next, we fetch the offers via Target Python SDK getOffers() API
response = target_client.get_offers({ "request": delivery_request })
```

성공적인 응답에는 다음이 포함됩니다. [!UICONTROL Target 배달 API] 요청된 mbox에 대해 프리페치된 콘텐츠가 포함된 응답 개체. 샘플 `target_response["response"]` 개체(dict 형식)는 다음과 같이 표시될 수 있습니다.

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

mbox를 확인합니다. `name` 및 `state` 필드 및 `eventToken` 각 Target 컨텐츠 옵션의 필드입니다. 다음에서 제공해야 합니다. `send_notifications()` 각 콘텐츠 옵션이 표시되는 즉시 요청합니다. 다음을 가정해 보겠습니다. `product1` mbox가 브라우저가 아닌 장치에 표시되었습니다. 알림 요청은 다음과 같이 표시됩니다.

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

mbox 상태와 이에 해당하는 이벤트 토큰이 모두 포함되어 있습니다. [!DNL Target] 프리페치 응답에서 전달된 오퍼. 알림 요청을 빌드했다면 다음으로 전송할 수 있습니다. [!DNL Target] 를 통해 `send_notifications()` API 메서드:

### Python

```python {line-numbers="true"}
response = target_client.send_notifications({ "request": notification_request })
```
