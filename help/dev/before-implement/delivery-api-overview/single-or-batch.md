---
title: Adobe Target 배달 API 단일 또는 일괄 배달
description: '[!UICONTROL Adobe Target Delivery API]개의 단일 또는 일괄 게재 호출을 사용하는 방법'
keywords: 배달 api
exl-id: 525cd1f2-616a-486c-8f49-8117615500bb
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# 단일 또는 일괄 게재

[!UICONTROL Adobe Target Delivery API]은(는) 단일 또는 일괄 게재 호출을 지원합니다. 서버에서 단일 또는 여러 mbox에 대한 콘텐츠를 요청할 수 있습니다.

단일 호출 대 일괄 호출을 수행하기로 결정할 때 성능 비용을 측정합니다. 사용자에게 표시해야 하는 모든 콘텐츠를 알고 있는 경우, 가장 좋은 방법은 여러 개의 단일 게재 호출을 방지하기 위해 단일 배치 게재 호출로 모든 mbox에 대한 콘텐츠를 검색하는 것입니다.

## 단일 게재 호출

[!UICONTROL Adobe Target Delivery API]을(를) 통해 하나의 mbox에 대해 사용자에게 표시할 경험을 검색할 수 있습니다. 단일 게재 호출을 수행하는 경우 사용자를 위한 mbox에 대한 추가 콘텐츠를 검색하려면 다른 서버 호출을 시작해야 합니다. 이 작업은 시간이 지남에 따라 매우 비용이 많이 소요될 수 있으므로 단일 배달 API 호출을 사용할 때 접근 방식을 평가해야 합니다.

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
    "execute": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      }
    ]
  }
}'
```

위의 단일 게재 호출 예제에서 웹 채널의 `mbox`:`SummerOffer`에 대해 `tntId`: `abcdefghijkl00023.1_1`을(를) 사용하여 사용자에게 표시하도록 경험이 검색됩니다. 이 단일 게재 호출은 다음 응답을 생성합니다.

```
{
  "status": 200,
  "requestId": "25e0cc42-3d7b-456a-8b49-af60c1fb23d9",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.1_1"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "execute": {
      "mboxes": [
          {
              "index": 1,
              "name": "SummerOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                      "type": "html",
                  }
              ]
          }
      ]
    }
}
```

응답에서 `content` 필드에는 SummerOffer mbox에 해당하는 웹에 대해 사용자에게 표시되는 경험을 설명하는 HTML이 포함됩니다.

### 페이지 로드 실행

AB가 바닥글이나 머리글에 있는 글꼴을 테스트하는 것과 같이 웹 채널에서 페이지를 로드할 때 표시되어야 하는 경험이 있는 경우 `execute` 필드에 `pageLoad`을(를) 지정하여 적용해야 하는 모든 수정 사항을 검색할 수 있습니다.

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
  "execute": {
    "pageLoad": {}
  }
}'
```

위의 샘플 호출은 `https://target.enablementadobe.com/react/demo/#/` 페이지가 로드될 때 사용자에게 표시할 모든 경험을 검색합니다.

```
{
      "status": 200,
      "requestId": "355ebc47-edb6-481f-aeae-ae55d71afaca",
      "client": "demo",
      "id": {
          "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
      },
      "edgeHost": "mboxedge28.tt.omtrdc.net",
      "execute": {
          "pageLoad": {
              "options": [
                  {
                      "content": [
                          {
                              "type": "setHtml",
                              "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > NAV.nav:eq(0) > DIV.container:eq(0) > DIV.nav-right:eq(0) > A.nav-item:eq(0)",
                              "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > NAV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > A:nth-of-type(1)",
                              "content": "Modified Home"
                          }
                      ],
                      "type": "actions"
                  }
              ],
              "metrics": [
                  {
                      "type": "click",
                      "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > FORM.col-md-4:eq(0) > DIV.form-group:eq(0) > BUTTON.btn:eq(0)",
                      "eventToken": "QPaLjCeI9qKCBUylkRQKBg=="
                  }
              ]
          }
      }
  }
```

`content` 필드에서 페이지 로드 시 적용해야 하는 수정 사항을 검색할 수 있습니다. 위의 예에서는 헤더의 링크 이름을 *수정된 홈*&#x200B;으로 지정해야 합니다.

## 일괄 처리된 게재 호출

각 호출에서 단일 mbox를 사용하여 여러 게재 호출을 수행하는 대신 mbox 일괄 처리를 사용하여 한 번의 게재 호출을 수행하면 불필요한 서버 호출이 줄어들 수 있습니다. 성능 향상을 위해서는 서버 호출 횟수를 가능한 한 최소화해야 합니다.

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
    "execute": {
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

위의 일괄 처리된 게재 호출 예제에서 여러 `mbox`:`SummerOffer`, `SummerShoesOffer` 및 `SummerDressOffer`에 대해 `tntId`: `abcdefghijkl00023.1_1`을(를) 가진 사용자에게 표시할 경험이 검색됩니다. 이 사용자를 위해 여러 mbox에 대한 경험을 표시해야 하므로 이러한 요청을 일괄 처리하고 세 개의 개별 게재 호출 대신 하나의 서버 호출을 수행할 수 있습니다.

```
{
  "status": 200,
  "requestId": "fe15286f-effb-434f-85d8-c3db804075ce",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.28_120"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "execute": {
      "mboxes": [
          {
              "index": 1,
              "name": "SummerOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                      "type": "html",

                  }
              ]
          },
          {
              "index": 2,
              "name": "SummerShoesOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next shoe purchase</b></p>",
                      "type": "html",
                  }
              ]
          },
          {
              "index": 3,
              "name": "SummerDressOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next dress purchase</b></p>",
                      "type": "html",
                  }
              ]
          }
      ]
  }
}
```

위의 응답에서 각 mbox의 `content` 필드 내에서 각 mbox에 대해 사용자에게 표시할 경험의 HTML 표현을 검색할 수 있음을 알 수 있습니다.
