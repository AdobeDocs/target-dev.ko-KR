---
title: 방문자를 식별하는 Adobe Target 배달 API
description: 내에서 사용자를 식별하려면 어떻게 합니까 [!DNL Adobe Target]?
keywords: 배달 api
exl-id: 5b8c28aa-caad-44a9-880a-3c5f844e47b2
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 9%

---

# 방문자 식별

내에서 방문자를 식별할 수 있는 방법에는 여러 가지가 있습니다 [!DNL Adobe Target].

Target은 다음 세 가지 식별자를 사용합니다.

| 필드 이름 | 설명 |
| --- | --- |
| `tntId` | 다음 `tntId` 는 의 기본 식별자입니다. [!DNL Target] 사용자용입니다. 이 ID를 제공하거나 [!DNL Target] 요청에 포함되지 않은 경우 이 자동으로 생성됩니다. |
| `thirdPartyId` | 다음 `thirdPartyId` 는 모든 호출에서 보낼 수 있는 사용자의 회사 식별자입니다. 사용자가 회사 사이트에 로그인하면 일반적으로 회사는 방문자 계정, 로열티 카드, 멤버십 번호 또는 해당 회사에 대한 기타 적용 가능한 식별자에 연결되는 ID를 만듭니다. |
| `marketingCloudVisitorId` | 다음 `marketingCloudVisitorId` 는 서로 다른 Adobe 솔루션 간에 데이터를 병합하고 공유하는 데 사용됩니다. 다음 `marketingCloudVisitorId` Adobe Analytics 및 Adobe Audience Manager과의 통합에 필요합니다. |
| `customerIds` | Experience Cloud 방문자 ID와 함께, 추가 [고객 ID](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) 각 방문자에 대해 인증된 상태를 활용할 수 있습니다. |

## [!DNL Target] ID

다음 [!DNL Target] ID 또는 `tntId` 디바이스 ID로 볼 수 있습니다. 이 `tntId` 다음에 의해 자동으로 생성됨: [!DNL Target] 요청에 제공되지 않는 경우. 이후 후속 요청에는 이 항목이 포함되어야 합니다 `tntId` 는 사용자가 사용하는 장치에 올바른 콘텐츠를 전달할 수 있도록 합니다.

```http {line-numbers="true"}
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
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

위의 예제 호출은 `tntId` 을 전달할 필요가 없습니다. 이 시나리오에서는 [!DNL Target]  다음을 생성합니다. `tntId` 여기에 표시된 대로 응답에 제공합니다.

```URI {line-numbers="true"}
{
  "status": 200,
  "requestId": "5b586f83-890c-46ae-93a2-610b1caa43ef",
  "client": "demo",
  "id": {
      "tntId": "10abf6304b2714215b1fd39a870f01afc.28_20"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  ...
}
```

생성됨 `tntId` 은(는) `10abf6304b2714215b1fd39a870f01afc.28_20`. 이 점을 참고하십시오. `tntId` 을(를) 호출할 때 사용해야 합니다. [!UICONTROL Adobe Target 게재 API] 세션 간 동일한 사용자용

## Marketing Cloud 방문자 ID

다음 `marketingCloudVisitorId` 는 Experience Cloud의 모든 솔루션에서 방문자를 식별하는 범용 및 영구 ID입니다. 조직이 ID 서비스를 구현하면 이 ID를 사용하여 Adobe Target, Adobe Analytics 또는 Adobe Audience Manager과 같은 다른 Experience Cloud 솔루션에서 동일한 사이트 방문자와 해당 데이터를 식별할 수 있습니다. 다음 사항에 유의하십시오. `marketingCloudVisitorId` 를 활용하고 Analytics 및 Audience Manager과 통합할 때 필요합니다.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "marketingCloudVisitorId": "10527837386392355901041112038610706884"
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

위의 예제 호출은 `marketingCloudVisitorId` Experience Cloud ID 서비스에서 검색한 값이 Adobe Target으로 전달됩니다. 이 시나리오에서는 [!DNL Target] 다음을 생성합니다. `tntId` 제공된 에 매핑될 원래 호출에 전달되지 않았기 때문에 `marketingCloudVisitorId` 아래 응답에서 볼 수 있듯이.

## 타사 ID

조직에서 ID를 사용하여 방문자를 식별하는 경우 다음을 사용할 수 있습니다 `thirdPartyID` 콘텐츠를 게재할 수 있습니다. 그러나 다음을 제공해야 합니다. `thirdPartyID` 마다 [!UICONTROL Adobe Target 게재 API] 전화해.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "thirdPartyId": "B234A029348"
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

위의 예제 호출은 `thirdPartyId`: 웹, 모바일 또는 IoT 채널에서 비즈니스와 상호 작용하는지 여부에 관계없이 비즈니스에서 최종 사용자를 식별하는 데 사용하는 영구 ID입니다. 즉, `thirdPartyId` 은 여러 채널에서 활용할 수 있는 사용자 프로필 데이터를 참조합니다. 이 시나리오에서는 [!DNL Target] 다음을 생성합니다. `tntId`, 원래 호출로 전달되지 않았으므로 제공된 호출에 매핑됩니다. `thirdPartyId` 아래 응답에서 볼 수 있듯이.

```
{
    "status": 200,
    "requestId": "55de9886-bd14-4dee-819c-7d1633b79b90",
    "client": "demo",
    "id": {
        "tntId": "10abf6304b2714215b1fd39a870f01afc.28_20",
        "thirdPartyId": "B234A029348"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    ...
}
```

## Customer ID

[고객 ID](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) 를 추가하여 Experience Cloud 방문자 ID와 연결할 수 있습니다. 전송할 때마다 `customerIds` 다음 `marketingCloudVisitorId` 도 제공해야 합니다. 또한, 각각의 인증 상태와 함께 제공될 수 있다 `customerId` 각 방문자에 대해. 다음 인증 상태를 고려할 수 있습니다.

| 인증 상태 | 사용자 상태 |
| --- | --- |
| `unknown` | 알 수 없음 또는 인증되지 않음. 이 상태는 디스플레이 광고를 클릭하여 사이트에 도착한 방문자와 같은 시나리오에 사용할 수 있습니다. |
| `authenticated` | 사용자는 현재 웹 사이트 또는 앱에서 활성 세션으로 인증됩니다. |
| `logged_out` | 사용자가 인증되었지만 로그아웃되었습니다. 사용자가 인증된 상태에서 연결을 끊으려고 했습니다. 사용자가 더 이상 인증됨으로 처리되는 것을 원치 않습니다. |

고객 ID가에 있을 때만 주의하십시오 `authenticated` 상태는 저장되고 고객 id에 연결된 Target 프로필 데이터를 프로필 참조합니다. 고객 ID가 인 경우 `unknown` 또는 `logged_out` state, 고객 id는 무시되며, 이와 연결될 수 있는 모든 사용자 프로필 데이터는 대상 타기팅에 활용되지 않습니다.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e044f14e1faeeba02d6ab23439914e' \
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
        "marketingCloudVisitorId" : "2304820394812039",
        "customerIds": [{
          "id": "134325423",
          "integrationCode" : "crm_data",
          "authenticatedState" : "authenticated"
        }]
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
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

위의 예제 호출은 를 보내는 방법을 보여 줍니다. `customerId` 다음 포함 `authenticatedState`. 전송 시 `customerId`, `integrationCode`, `id`, 및 `authenticatedState` 및 `marketingCloudVisitorId` 필수 항목입니다. 다음 `integrationCode` 은(는) 의 별칭입니다 [고객 특성 파일](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=ko-KR) CRS를 통해서 제공했습니다.

## 병합된 프로필

다음을 결합할 수 있습니다 `tntId`, `thirdPartyID`, 및 `marketingCloudVisitorId` 동일한 요청에서. 이 시나리오에서는 Adobe Target이 이러한 모든 ID의 매핑을 유지하고 방문자에게 고정합니다. 프로필의 기능 알아보기 [실시간으로 병합 및 동기화](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) 다른 식별자 사용.

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e044f14e1faeeba02d6ab23439914e' \
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
        "marketingCloudVisitorId" : "2304820394812039",
        "tntId": "d359234570e044f14e1faeeba02d6ab23439914e.28_78",
        "thirdPartyId":"23423432"
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

위의 예제 호출은 를 결합하는 방법을 보여 줍니다 `tntId`, `thirdPartyID`, 및 `marketingCloudVisitorId` 동일한 요청에서. 세 개의 ID도 모두 응답에서 반환됩니다.
