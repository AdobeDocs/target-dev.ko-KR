---
title: Adobe Target 배달 API 미리 가져오기
description: 에서 프리페치를 사용하는 방법 [!UICONTROL Adobe Target 게재 API]?
keywords: 배달 api
exl-id: eab88e3a-442c-440b-a83d-f4512fc73e75
feature: APIs/SDKs
source-git-commit: 4ff2746b8b485fe3d845337f06b5b0c1c8d411ad
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# 미리 가져오기

프리페치를 사용하면 모바일 앱 및 서버와 같은 클라이언트가 한 요청에서 여러 mbox 또는 보기에 대한 콘텐츠를 가져오고, 로컬 캐시에 저장하고, 나중에 알릴 수 있습니다 [!DNL Target] 방문자가 해당 mbox 또는 보기를 방문하는 경우입니다.

미리 가져오기를 사용할 때는 다음 용어를 숙지해야 합니다.

| 필드 이름 | 설명 |
| --- | --- |
| `prefetch` | 가져와야 하지만 방문한 것으로 표시해서는 안 되는 mbox 및 보기 목록. 다음 [!DNL Target] Edge가 다음을 반환합니다. `eventToken` 프리페치 배열에 있는 각 mbox 또는 뷰에 대해 해당됩니다. |
| `notifications` | 이전에 미리 가져온 mbox 및 보기 목록은 방문한 것으로 표시해야 합니다. |
| `eventToken` | 콘텐츠를 미리 가져올 때 반환되는 해시된 암호화 토큰. 이 토큰은 (으)로 다시 전송되어야 합니다. [!DNL Target] 다음에서 `notifications` 배열입니다. |

## Mbox 미리 가져오기

모바일 앱 및 서버와 같은 클라이언트는 세션 내에서 지정된 방문자에 대해 여러 mbox를 미리 가져오고 캐시하여 [!UICONTROL Adobe Target 게재 API].

```shell shell-session
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

다음 범위 내 `prefetch` 필드, 하나 이상 추가 `mboxes` 세션 내의 방문자에 대해 최소 한 번 이상 미리 가져오려고 합니다. 다음에 대해 미리 가져오기 `mboxes`, 다음 응답을 받게 됩니다.

```JSON {line-numbers="true"}
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

응답 내에 `content` 방문자에게 표시할 특정 경험이 포함된 필드 `mbox`. 이 기능은 방문자가 세션 내에서 웹 또는 모바일 애플리케이션과 상호 작용하고 를 방문할 때 서버에 캐시될 때 매우 유용합니다. `mbox` 애플리케이션의 특정 페이지에서 다른 환경을 만드는 대신 캐시에서 경험을 전달할 수 있습니다 [!UICONTROL Adobe Target 게재 API] 호출합니다. 단, 경험이 다음에서 방문자에게 전달됩니다. `mbox`, a `notification` 노출 로깅이 수행되도록 배달 API 호출을 통해 전송됩니다. 이는 의 응답이 `prefetch` 호출이 캐시되므로 방문자는 해당 시간에 경험을 본 적이 없습니다. `prefetch` 호출이 발생합니다. 에 대해 자세히 알아보려면 `notification` 프로세스, 참조 [알림](notifications.md).

## 다음을 사용하여 mbox 미리 가져오기 `clickTrack` 사용 시 지표 [!UICONTROL Analytics for Target] (A4T)

[[!UICONTROL Adobe Analytics for Target]](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html){target=_blank} (A4T)은 을 기반으로 활동을 만들 수 있는 솔루션 간 통합입니다 [!DNL Analytics] 전환 지표 및 대상 세그먼트.

다음 코드 조각은 를 포함하는 mbox 미리 가져오기의 응답입니다 `clickTrack` 통지할 지표 [!DNL Analytics] 오퍼를 클릭함:

```JSON {line-numbers="true"}
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

보기는 단일 페이지 애플리케이션(SPA) 및 모바일 애플리케이션을 보다 원활하게 지원합니다. 보기는 SPA 또는 모바일 경험을 함께 구성하는 시각적 요소의 논리 그룹으로 볼 수 있습니다. 이제 게재 API를 통해 VEC가 만들어짐 [[!UICONTROL A/B 테스트]](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html){target=_blank} and [[!UICONTROL Experience Targeting]](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html){target=_blank} 에 대한 수정 사항이 있는 (X)T 활동 [SPA 보기](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md) 이제 를 프리페치할 수 있습니다.

```shell  {line-numbers="true"}
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

위의 예제 호출은에 대해 SPA VEC를 통해 생성된 모든 보기를 미리 가져옵니다. [!UICONTROL A/B 테스트] 및 웹에 대해 표시할 XT 활동 `channel`. 이 호출은 에서 모든 보기를 미리 가져옵니다. [!UICONTROL A/B 테스트] 또는 방문자가 있는 XT 활동 `tntId`:`84e8d0e211054f18af365d65f45e902b.28_131` 누가 방문합니까? `url`:`https://target.enablementadobe.com/react/demo/#/` 자격 요건.

```JSON  {line-numbers="true"}
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

다음에서 `content` 응답의 필드, 메모 메타데이터 `type`, `selector`, `cssSelector`, 및 `content`: 사용자가 페이지를 방문할 때 방문자에게 경험을 렌더링하는 데 사용됩니다. 다음 사항에 주의하십시오. `prefetched` 필요한 경우 콘텐츠를 캐시하고 사용자에게 렌더링할 수 있습니다.
