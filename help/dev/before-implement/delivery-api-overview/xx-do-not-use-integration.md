---
title: Experience Cloud과 통합
description: Experience Cloud과 통합
keywords: 배달 api
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 7%

---

<!-- The content on this page was originally pulled from the legacy Delivery API doc site, and was subsequently found to be an outdated version of information now found on [Implement > Server-side > Integration > A4T Reporting](../../implement/server-side/sdk-guides/integration-with-experience-cloud/a4t-reporting.md) and [Implement > Server-side > Integration > AAM Segments](../../implement/server-side/sdk-guides/integration-with-experience-cloud/aam-segments.md). Therefore sunsetting this page, but not deleting it from the repo immediately, pending a more thorough examination to avoid inadvertently deleting relevant content. -->


# Experience Cloud과 통합

## Adobe Analytics for Target (A4T)

서버에서 Target 배달 API 호출이 실행되면 Adobe Target은 해당 사용자에 대한 경험을 반환하며 그 외에도 Adobe Target은 Adobe Analytics 페이로드를 다시 호출자에게 반환하거나 자동으로 Adobe Analytics에 전달합니다. Target 활동 정보를 서버측의 Adobe Analytics으로 보내려면 다음과 같이 충족해야 하는 몇 가지 전제 조건이 있습니다.

1. 활동은 Adobe Target UI에서 Adobe Analytics을 보고 소스로 설정되며 계정은 A4T에 대해 활성화됩니다
1. Adobe Marketing Cloud 방문자 ID는 API 사용자에 의해 생성되며, Target 게재 API 호출이 실행될 때 사용할 수 있습니다

### Adobe Target은 Analytics 페이로드를 자동으로 전달합니다

Adobe Target은 다음 식별자가 제공되면 서버측을 통해 Adobe Analytics에 analytics 페이로드를 자동으로 전달할 수 있습니다.

1. `supplementalDataId` - Adobe Analytics과 Adobe Target 사이를 연결하는 데 사용되는 ID
1. `trackingServer` - Adobe Analytics 서버 Adobe Target과 Adobe Analytics에서 데이터를 올바르게 연결하려면 Adobe Target과 Adobe Analytics 모두에 동일한 `supplementalDataId`을(를) 전달해야 합니다.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
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
      "id": {
        "marketingCloudVisitorId": "2304820394812039"
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "analytics": {
          "supplementalDataId" : "23423498732598234",
          "trackingServer": "ags041.sc.omtrdc.net",
          "logging": "server_side"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          }
        ]
      }
    }'
```

### Adobe Target에서 Analytics 페이로드 검색

Adobe Target 배달 API 소비자는 해당 mbox에 대한 Adobe Analytics 페이로드를 검색할 수 있으므로 소비자가 [데이터 삽입 API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)를 통해 페이로드를 Adobe Analytics에 보낼 수 있습니다. 서버측 Adobe Target 호출이 실행되면 `client_side`을(를) 요청의 `logging` 필드에 전달합니다. 이렇게 하면 Analytics를 보고 소스로 사용하는 활동에 mbox가 있는 경우 페이로드가 반환됩니다.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
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
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "analytics": {
          "logging": "client_side"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
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

`logging` = `client_side`을(를) 지정하면 아래와 같이 `mbox` 필드에 페이로드를 받게 됩니다.

```
{
    "status": 200,
    "requestId": "4b8855a5-8354-4ac4-8ae7-c551f7c0bb8a",
    "client": "demo",
    "id": {
        "tntId": "d359234570e04f14e1faeeba02d6ab9914e.28_7"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "execute": {
        "mboxes": [
            {
                "index": 1,
                "name": "homepage",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                        "type": "html",

                    }
                ],
                "analytics": {
                    "payload": {
                        "pe": "tnt",
                        "tnta": "285408:0:0|2"
                    }
                }
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

Target의 응답에 `analytics` -> `payload` 속성에 있는 항목이 있으면 그대로 Adobe Analytics에 전달합니다. Analytics는 이 페이로드를 처리하는 방법을 알고 있습니다. 이 작업은 다음 형식을 사용하여 GET 요청에서 수행할 수 있습니다.

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/0/CODEVERSION?pe=tnt&tnta={payload}&mid={mid}&vid={vid}&aid={aid}
```

### 쿼리 문자열 매개 변수 및 변수

| 필드 이름 | 필수 | 설명 |
| --- | --- | --- |
| `rsid` | 예 | 보고서 세트 ID |
| `pe` | 예 | 페이지 이벤트. 항상 `tnt`(으)로 설정 |
| `tnta` | 예 | `analytics` -> `payload` -> `tnta`의 Target 서버에서 반환된 Analytics 페이로드 |
| `mid` | Marketing Cloud 방문자 ID |  |

### 필수 헤더 값

| 헤더 이름 | 헤더 값 |
| --- | --- |
| 호스트 | Analytics 데이터 수집 서버(예: adobeags421.sc.omtrdc.net) |

### 샘플 A4T 데이터 삽입 HTTP Get 호출

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0?pe=tnt&tnta=285408:0:0|2&mid=2304820394812039
```

## Adobe Audience Manager

Adobe Target 배달 API를 통해 Adobe Audience Manager(AAM) 세그먼트를 활용할 수도 있습니다. AAM 세그먼트를 활용하려면 다음 필드를 제공해야 합니다.

| 필드 이름 | 필수 | 설명 |
| --- | --- | --- |
| `locationHint` | 예 | DCS 위치 힌트는 프로필을 검색하기 위해 히트할 AAM DCS 끝점을 결정하는 데 사용됩니다. 1보다 크거나 같아야 합니다. |
| `marketingCloudVisitorId` | 예 | Marketing Cloud 방문자 ID |
| `blob` | 예 | AAM Blob을 사용하여 추가 데이터를 AAM으로 보낼 수 있습니다. 비워 둘 수 없으며 크기는 1024 미만이어야 합니다. |

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
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
      "id": {
        "marketingCloudVisitorId": "2304820394812039"
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "audienceManager": {
          "locationHint": 9,
          "blob": "32fdghkjh34kj5h43"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
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
