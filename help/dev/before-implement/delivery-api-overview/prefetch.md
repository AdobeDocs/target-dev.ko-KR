---
title: Adobe Target 배달 API 미리 가져오기
description: 에서 프리페치를 사용하는 방법 [!UICONTROL Adobe Target 게재 API]?
keywords: 배달 api
exl-id: eab88e3a-442c-440b-a83d-f4512fc73e75
feature: APIs/SDKs
source-git-commit: 803723d95d50cc39101d1646232446fbb0254385
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# 미리 가져오기

프리페치를 사용하면 모바일 앱 및 서버와 같은 클라이언트가 한 요청에서 여러 mbox 또는 보기에 대한 콘텐츠를 가져오고, 로컬 캐시에 저장하고, 나중에 알릴 수 있습니다 [!DNL Target] 사용자가 해당 mbox 또는 보기를 방문할 때입니다.

미리 가져오기를 활용할 때는 다음 용어를 숙지하는 것이 중요합니다.

| 필드 이름 | 설명 |
| --- | --- |
| `prefetch` | 가져와야 하지만 방문한 것으로 표시해서는 안 되는 mbox 및 보기 목록. 다음 [!DNL Target] Edge가 다음을 반환합니다. `eventToke`미리 가져오기 배열에 있는 각 mbox 또는 보기에 대해 n입니다. |
| `notifications` | 이전에 미리 가져온 mbox 및 보기 목록은 방문한 것으로 표시해야 합니다. |
| `eventToken` | 콘텐츠를 미리 가져올 때 반환되는 해시된 암호화 토큰. 이 토큰은 (으)로 다시 전송되어야 합니다. [!DNL Target] 다음에서 `notifications` 배열입니다. |

## Mbox 미리 가져오기

모바일 앱 및 서버와 같은 클라이언트는에 대한 여러 호출을 방지하기 위해 세션 내에서 지정된 사용자에 대해 여러 mbox를 미리 가져오고 캐시할 수 있습니다 [!UICONTROL Adobe Target 게재 API].

```
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=7abf6304b2714215b1fd39a870f01afc#1555632114' \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '
{
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
    "prefetch": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      },
      {
        "name" : "SummerShoesOffer",
        "index" : 2
      },
      {
        "name" : "SummerDressOffer",
        "index" : 3
      }      
    ]
  }
}'
```

다음 범위 내 `prefetch` 필드, 하나 이상 추가 `mboxes` 세션 내의 사용자에 대해 한 번에 을 미리 가져오려고 합니다. 해당 항목에 대해 미리 가져오기 `mboxes` 다음 응답을 받게 됩니다.

```
{
    "status": 200,
    "requestId": "5efee0d8-3779-4b12-a74e-e04848faf191",
    "client": "demo",
    "id": {
        "tntId": "abcdefghijkl00023.1_1"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "prefetch": {
        "mboxes": [
            {
                "index": 1,
                "name": "SummerOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                        "type": "html",
                        "eventToken": "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
                    }
                ]
            },
            {
                "index": 2,
                "name": "SummerShoesOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next shoe purchase</b></p>"
                        "type": "html",
                        "eventToken": "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
                    }
                ]
            },
            {
                "index": 3,
                "name": "SummerDressOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next dress purchase</b></p>"
                        "type": "html",
                        "eventToken": "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
                    }
                ]
            }
        ]
    }
}
```

응답 내에 `content` 특정 항목에 대해 사용자에게 표시할 경험이 포함된 필드 `mbox`. 이 기능은 사용자가 세션 내에서 웹 또는 모바일 애플리케이션과 상호 작용하고 를 방문할 때 서버에 캐시될 때 매우 유용합니다. `mbox` 애플리케이션의 특정 페이지에서 다른 환경을 만드는 대신 캐시에서 경험을 전달할 수 있습니다 [!UICONTROL Adobe Target 게재 API] 호출합니다. 단, 경험이 사용자에게에서 전달됩니다. `mbox`, a `notification` 노출 로깅이 수행되도록 배달 API 호출을 통해 전송됩니다. 이는 의 응답이 `prefetch` 호출이 캐시되므로 해당 시간에는 사용자가 경험을 보지 않았습니다. `prefetch` 호출이 발생합니다. 에 대해 자세히 알아보려면 `notification` 프로세스를 참조하십시오. [알림](notifications.md).

## 사용 시 clickTrack 지표로 mbox 미리 가져오기 [!UICONTROL Analytics for Target] (A4T)

[[!UICONTROL Adobe Analytics for Target]](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html){target=_blank} (A4T)은 을 기반으로 활동을 만들 수 있는 솔루션 간 통합입니다 [!DNL Analytics] 전환 지표 및 대상 세그먼트.

다음 코드 조각은 다음을 포함하는 mbox 미리 가져오기의 응답입니다. `clickTrack` 통지할 지표 [!DNL Analytics] 오퍼를 클릭함:

```
{
  "prefetch": {
    "mboxes": [
      {
        "index": 0,
        "name": "<mboxName>",
        "options": [
           ...
        ],
        "metrics": [
          {
            "type": "click",
            "eventToken": "<eventToken>",
             "analytics": {
               "payload": {
                 "pe": "tnt",
                 "tnta": "..."
               }
             }
          },
          }
        ],
        "analytics": {
          "payload": {
            "pe": "tnt",
            "tnta": "347565:1:0|2,347565:1:0|1"
          }
        }
      }
    ]
  }
}
```

>[!NOTE]
>
>mbox에 대한 미리 가져오기에는 [!DNL Analytics] 자격 있는 활동에 대한 페이로드만. 아직 정규화되지 않은 활동에 대한 성공 지표를 미리 가져오면 보고가 일치하지 않습니다.

## 미리 가져오기 보기

보기는 단일 페이지 애플리케이션(SPA) 및 모바일 애플리케이션을 보다 원활하게 지원합니다. 보기는 SPA 또는 모바일 경험을 함께 구성하는 시각적 요소의 논리 그룹으로 볼 수 있습니다. 이제 VEC는 게재 API를 통해 [SPA 보기](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md) 이제 를 프리페치할 수 있습니다.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=a3e7368c62d944c0855d424cd7a03ab0' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
  },
  "context": {
    "channel": "web",
    "window": {
      "width": 1819,
      "height": 842
    },
    "browser": {
      "host": "target.enablementadobe.com"
    },
    "address": {
      "url": "https://target.enablementadobe.com/react/demo/#/"
    }
  },
  "prefetch": {
    "views": [{}]
  }
}'
```

위의 예제 호출은 AB 및 XT 활동에 대해 SPA VEC를 통해 만든 모든 보기를 미리 가져와 웹에 대해 표시합니다 `channel`. 호출에서는 방문자가 사용하는 AB 또는 XT 활동에서 모든 보기를 미리 가져오려고 합니다 `tntId`:`84e8d0e211054f18af365d65f45e902b.28_131` 누가 방문합니까? `url`:`https://target.enablementadobe.com/react/demo/#/` 자격 요건.

```
{
    "status": 200,
    "requestId": "14ce028e-d2d2-4504-b3da-32740fa8dd61",
    "client": "demo",
    "id": {
        "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "prefetch": {
        "views": [
            {
                "id": 228,
                "name": "checkout-express",
                "key": "checkout-express",
                "state": "Vqfb6kYGAmzWOLf9W6E+Q/0LyS+SYe2h5tuTXzRNnkjKkZaZZr2ijp41/6AwK6fdFgADhFNC7l5efUCs9shgTw==",
                "options": [
                    {
                        "content": [
                            {
                                "type": "setHtml",
                                "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > FORM.col-md-4:eq(0) > DIV:nth-of-type(1) > DIV.mb-3:eq(2)",
                                "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(1) > FORM:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(3)",
                                "content": "<span style=\"color:#000080;\"><strong>*We charge an additional fee of $12.34 for faster delivery. If you choose express delivery get 15% off on your next order.</strong></span>"
                            }
                        ],
                        "type": "actions",
                        "eventToken": "N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                    }
                ]
            },
            {
                "id": 5,
                "name": "home",
                "key": "home",
                "state": "Vqfb6kYGAmzWOLf9W6E+Q/0LyS+SYe2h5tuTXzRNnkjKkZaZZr2ijp41/6AwK6fdFgADhFNC7l5efUCs9shgTw==",
                "options": [
                    {
                        "content": [
                            {
                                "type": "setHtml",
                                "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(1) > DIV.heading:eq(0) > H1.title:eq(0)",
                                "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > H1:nth-of-type(1)",
                                "content": "<span style=\"color:#800000;\"><strong>Trending Items</strong></span>"
                            }
                        ],
                        "type": "actions",
                        "eventToken": "N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                    }
                ]
            },
            {
                "id": 6,
                "name": "products",
                "key": "products",
                "state": "Vqfb6kYGAmzWOLf9W6E+Q/0LyS+SYe2h5tuTXzRNnkjKkZaZZr2ijp41/6AwK6fdFgADhFNC7l5efUCs9shgTw==",
                "options": [
                    {
                        "content": [
                            {
                                "type": "setStyle",
                                "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > DIV.heading:eq(0) > BUTTON.btn:eq(0)",
                                "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > BUTTON:nth-of-type(1)",
                                "content": {
                                    "background-color": "rgba(191,0,0,1)",
                                    "priority": "important"
                                }
                            }
                        ],
                        "type": "actions",
                        "eventToken": "N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                    }
                ]
            }
        ]
    }
}
```

다음에서 `content` 응답의 필드, 메모 메타데이터 `type`, `selector`, `cssSelector`, 및 `content`: 사용자가 페이지를 방문할 때 최종 사용자에게 경험을 렌더링하는 데 사용됩니다. 다음 사항에 주의하십시오. `prefetched` 필요한 경우 콘텐츠를 캐시하고 사용자에게 렌더링할 수 있습니다.
