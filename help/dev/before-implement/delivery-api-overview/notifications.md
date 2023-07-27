---
title: Adobe Target 배달 API 알림
description: 을 사용하여 알림을 실행하는 방법 [!UICONTROL Adobe Target 게재 API]?
keywords: 배달 api
exl-id: 711388fd-2c1f-4ca4-939f-c56dc4bdc04a
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 알림

프리페치된 mbox 또는 보기가 최종 사용자에게 방문되거나 렌더링될 때 알림을 실행해야 합니다.

알림을 올바른 mbox 또는 보기에 대해 실행하려면 해당하는 을 추적해야 합니다 `eventToken` 각 mbox 또는 보기에 대해 올바른 알림 `eventToken` 보고를 올바르게 반영하려면 해당 mbox 또는 보기를 실행해야 합니다.

## 프리페치된 Mbox에 대한 알림

한 번의 게재 호출을 통해 하나 이상의 알림을 전송할 수 있습니다. 추적해야 하는 지표가 다음 중 하나인지 확인합니다. `click` 또는 `display` 각 mbox마다 `type` 알림이 올바르게 반영될 수 있습니다. 또한 를 전달합니다. `id` 를 통해 알림이 올바르게 전송되었는지 확인할 수 있도록 각 알림에 대해[!UICONTROL  Adobe Target 게재 API]. 다음 `timestamp` 다음으로 전달해야 하는 중요한 항목이기도 합니다. [!DNL Target] 다음을 나타낼 때: `click` 또는 `display` 보고 목적으로 주어진 mbox에 대해 발생했습니다.

```
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '{
    "id": {
      "tntId": "abcdefghijkl00023.1_1"
    },
    "context": {
      "channel": "web",
      "browser" : {
        "host" : "demo"
      },
      "address" : {
        "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
      },
      "screen" : {
        "width" : 1200,
        "height": 1400
      }
    },
      "notifications": [
      {
      "id" : "SummerOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
      },
    {
      "id" : "SummerShoesOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerShoesOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
      },
    {
      "id" : "SummerDressOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerDressOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
    } 
    ]
  }'
```

위의 예제 호출을 수행하면 을 나타내는 응답이 발생합니다. `notifications` 요청이 정상적으로 처리되었습니다.

```
{
  "status": 200,
  "requestId": "36014eed-4772-4c48-a9e2-e532762b6a85",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.28_20"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "notifications": [
      {
          "id": "SummerOfferNotification"
      },
      {
          "id": "SummerDressOfferNotification"
      },
      {
          "id": "SummerShoesOfferNotification"
      }
  ]
}
```

모두 `notifications` 전송 대상: [!DNL Target] 이(가) 올바르게 처리되면 `notifications` 응답에 배열이 표시됩니다. 단, `notifications` `id` 누락되었습니다. `notification` 통과하지 않았습니다. 이 시나리오에서는 성공할 때까지 재시도 논리를 적용할 수 있습니다 `notification` 응답이 검색되었습니다. API 호출이 차단되어 성능 지연이 발생하지 않도록 재시도 논리에 시간 제한이 지정되어 있는지 확인하십시오.

## 프리페치된 보기에 대한 알림

한 번의 게재 호출을 통해 하나 이상의 알림을 전송할 수 있습니다. 추적해야 하는 지표가 다음 중 하나인지 확인합니다. `click` 또는 `display` 알림 유형이 올바르게 반영될 수 있도록 각 mbox에 대해 . 또한 를 전달합니다. `id` 를 통해 알림이 올바르게 전송되었는지 확인할 수 있도록 각 알림에 대해 [!UICONTROL Adobe Target 게재 API]. 타임스탬프도 전달해야 합니다. [!DNL Target] 다음을 나타낼 때: `click` 또는 `display` 은(는) 보고 목적으로 주어진 보기에 대해 발생했습니다.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
  },
  "context": {
    "channel": "web",
    "browser": {
      "host": "target.enablementadobe.com"
    },
    "address": {
      "url": "https://target.enablementadobe.com/react/demo/#/"
    }
  },
  "notifications": [{
      "id": "228",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "checkout-express",
      }
    },
    {
      "id": "5",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "home",
      }
    },
    {
      "id": "6",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "products",
      }
    }
  ]
}'
```

위의 예제 호출을 수행하면 을 나타내는 응답이 발생합니다. `notifications` 요청이 정상적으로 처리되었습니다.

```
{
    "status": 200,
    "requestId": "85cc7394-c19a-4398-9b8b-bbee1e4c4579",
    "client": "demo",
    "id": {
        "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "notifications": [
        {
            "id": "5"
        },
        {
            "id": "6"
        },
        {
            "id": "228"
        }
    ]
}
```

모두 `notifications` 전송 대상:  [!DNL Target] 이(가) 올바르게 처리되면 `notifications` 응답에 배열이 표시됩니다. 단, `notifications` `id` 이(가) 누락되어 해당 특정 알림이 전달되지 않았습니다. 이 시나리오에서는 성공적인 알림 응답이 검색될 때까지 재시도 논리를 적용할 수 있습니다. API 호출이 차단되어 성능 지연이 발생하지 않도록 재시도 논리에 시간 제한이 지정되어 있는지 확인하십시오.
