---
title: Experience Platform Web SDK의 A4T 데이터에 대한 클라이언트측 로깅
description: Experience Platform Web SDK을 사용하여 Adobe Analytics for Target(A4T)에 대해 클라이언트측 로깅을 활성화하는 방법에 대해 알아봅니다.
seo-title: Client-side logging for A4T data in the Experience Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: target;a4t;로깅;web sdk;경험;플랫폼;
feature: Implementation
source-git-commit: 4d4ca7dcffdbaee5770084bd85c3109df0d6a8d4
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---

# [!DNL Experience Platform Web SDK]의 A4T 데이터에 대한 클라이언트측 로깅

[!DNL Adobe Experience Platform Web SDK]을(를) 사용하면 웹 응용 프로그램의 클라이언트측에서 [Target용 Adobe Analytics(A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=ko) 데이터를 수집할 수 있습니다.

클라이언트측 로깅은 관련 [!DNL Target] 데이터가 클라이언트측에서 반환됨을 의미하며, 이를 통해 데이터를 수집하고 [!DNL Analytics]과(와) 공유할 수 있습니다. [데이터 삽입 API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html?lang=ko)를 사용하여 데이터를 Analytics에 수동으로 전송하려면 이 옵션을 활성화해야 합니다.

>[!NOTE]
>
>[AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=ko)을(를) 사용하여 이 작업을 수행하는 메서드가 현재 개발 중이며 가까운 미래에 제공될 예정입니다.

이 문서에서는 [!DNL Platform Web SDK]에 대한 클라이언트측 A4T 로깅을 설정하는 단계에 대해 설명하고 일반적인 사용 사례에 대한 구현 예를 제공합니다.

## 사전 요구 사항 {#prerequisites}

이 자습서에서는 사용자가 맞춤화를 위해 [!DNL Platform Web SDK]을(를) 사용하는 것과 관련된 기본 개념 및 프로세스를 잘 알고 있다고 가정합니다. 소개가 필요한 경우 다음 설명서를 검토하십시오.

* [웹 SDK 구성](https://experienceleague.adobe.com/ko/docs/experience-platform/web-sdk/commands/configure/overview)
* [이벤트 보내기](https://experienceleague.adobe.com/ko/docs/experience-platform/web-sdk/commands/sendevent/overview)
* [개인화 콘텐츠 렌더링](https://experienceleague.adobe.com/ko/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

## [!DNL Analytics] 클라이언트측 로깅 설정 {#set-up-client-side-logging}

다음 하위 섹션에서는 [!DNL Analytics] 구현에 대해 [!DNL Platform Web SDK] 클라이언트측 로깅을 활성화하는 방법에 대해 간략히 설명합니다.

### [!DNL Analytics] 클라이언트측 로깅 사용 {#enable-analytics-client-side-logging}

구현에 대해 [!DNL Analytics] 클라이언트측 로깅을 사용하도록 설정하려면 [!DNL Adobe Analytics]데이터스트림[에서 ](https://experienceleague.adobe.com/ko/docs/experience-platform/datastreams/overview) 구성을 사용하지 않도록 설정해야 합니다.

![Analytics 데이터 스트림 구성 사용 안 함](/help/dev/implement/a4t/assets/disable-analytics-datastream.png)

### SDK에서 [!DNL A4T] 데이터를 검색하여 [!DNL Analytics]&#x200B;(으)로 보냅니다. {#a4t-to-analytics}

이 보고 메서드가 제대로 작동하려면 [!DNL A4T] 히트의 [`sendEvent`](https://experienceleague.adobe.com/ko/docs/experience-platform/web-sdk/commands/sendevent/overview) 명령에서 검색된 [!DNL Analytics] 관련 데이터를 보내야 합니다.

[!DNL Target] Edge에서 제안 응답을 계산하면 [!DNL Analytics] 클라이언트측 로깅이 활성화되었는지(예: 데이터스트림에서 [!DNL Analytics]이 비활성화되었는지) 확인합니다. 클라이언트측 로깅이 활성화되면 시스템은 응답의 각 제안에 [!DNL Analytics] 토큰을 추가합니다.

흐름은 다음과 유사합니다.

![클라이언트측 로깅 흐름](/help/dev/implement/a4t/assets/analytics-client-side-logging.png)

다음은 `interact` 클라이언트측 로깅이 활성화된 경우 [!DNL Analytics] 응답의 예입니다. [!DNL Analytics] 보고가 있는 활동에 대한 제안인 경우 `scopeDetails.characteristics.analyticsToken` 속성이 있습니다.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "experience": {
              "id": "0"
            },
            "strategies": [
              {
                "algorithmID": "0",
                "trafficType": "0"
              }
            ],
            "characteristics": {
              "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
              "analyticsToken": "434689:0:0|2,434689:0:0|1"
            }
          },
          "items": [
            {
              "id": "1184844",
              "schema": "https://ns.adobe.com/personalization/html-content-item",
              "meta": {
                "geo.state": "bucuresti",
                "activity.id": "434689",
                "experience.id": "0",
                "activity.name": "a4t test form based activity",
                "offer.id": "1184844",
                "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
              },
              "data": {
                "id": "1184844",
                "format": "text/html",
                "content": "<div> analytics impressions </div>"
              }
            }
          ]
        },
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "characteristics": {
              "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
              "analyticsToken": "434689:0:0|32767"
            }
          },
          "items": [
            {
              "id": "434689",
              "schema": "https://ns.adobe.com/personalization/measurement",
              "data": {
                "type": "click",
                "format": "application/vnd.adobe.target.metric"
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

[!UICONTROL Form-based Experience Composer] 활동에 대한 제안은 동일한 제안 아래에 콘텐츠와 클릭 지표 항목을 모두 포함할 수 있습니다. 따라서 `scopeDetails.characteristics.analyticsToken` 속성에 콘텐츠에 대한 단일 분석 토큰이 표시되지 않고 `scopeDetails.characteristics.analyticsDisplayToken` 및 `scopeDetails.characteristics.analyticsClickToken` 속성에서 디스플레이 및 클릭 분석 토큰이 모두 지정될 수 있습니다.

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "experience": {
              "id": "0"
            },
            "strategies": [
              {
                "algorithmID": "0",
                "trafficType": "0"
              }
            ],
            "characteristics": {
               "displayToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
               "clickToken": "E0gb6q1+WyFW3FMbbQJmrg==",
               "analyticsDisplayToken": "434689:0:0|2,434689:0:0|1", 
               "analyticsClickToken": "434689:0:0|32767"
            }
          },
          "items": [
            {
              "id": "1184844",
              "schema": "https://ns.adobe.com/personalization/html-content-item",
              "meta": {
                "geo.state": "bucuresti",
                "activity.id": "434689",
                "experience.id": "0",
                "activity.name": "a4t test form based activity",
                "offer.id": "1184844",
                "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
              },
              "data": {
                "id": "1184844",
                "format": "text/html",
                "content": "<div> analytics impressions </div>"
              }
            },
            {
              "id": "434689",
              "schema": "https://ns.adobe.com/personalization/measurement",
              "data": {
                "type": "click",
                "format": "application/vnd.adobe.target.metric"
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

`scopeDetails.characteristics.analyticsToken`과(와) `scopeDetails.characteristics.analyticsDisplayToken`(표시된 콘텐츠의 경우) 및 `scopeDetails.characteristics.analyticsClickToken`(클릭 지표의 경우)의 모든 값은 `tnta`데이터 삽입 API[ 호출에서 ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) 태그로 수집 및 포함되어야 하는 A4T 페이로드입니다.

>[!IMPORTANT]
>
>`analyticsToken`, `analyticsDisplayToken`, `analyticsClickToken` 속성에는 여러 토큰이 포함될 수 있으며 쉼표로 구분된 단일 문자열로 연결될 수 있습니다.
>
>다음 섹션에 제공된 구현 예제에서 여러 개의 [!DNL Analytics] 토큰이 반복적으로 수집됩니다. [!DNL Analytics] 토큰의 배열을 연결하려면 다음과 유사한 함수를 사용합니다.
>
>```javascript
>var concatenateAnalyticsPayloads = function concatenateAnalyticsPayloads(analyticsPayloads) {
>   if (analyticsPayloads.size > 1) {
>       return [].concat(analyticsPayloads).join(',');
>   }
>   return [].concat(analyticsPayloads).join();
>};
>```

## 구현 예 {#implementation-examples}

다음 하위 섹션에서는 일반적인 사용 사례에 대해 [!DNL Analytics] 클라이언트측 로깅을 구현하는 방법을 보여 줍니다.

### [!UICONTROL Form-Based Experience Composer]개 활동 {#form-based-composer}

[!DNL Platform Web SDK]을(를) 사용하여 [Adobe Target 양식 기반 경험 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=ko) 활동에서 제안 실행을 제어할 수 있습니다.

특정 결정 범위에 대한 제안을 요청하면 반환된 제안에 해당 [!DNL Analytics] 토큰이 포함됩니다. 가장 좋은 방법은 [!DNL Experience Platform Web SDK] `sendEvent` 명령을 체인한 다음 반환된 제안을 반복하여 실행하여 [!DNL Analytics] 토큰을 동시에 수집하는 것입니다.

다음과 같이 `sendEvent` 활동 범위에 대해 [!UICONTROL Form-Based Experience Composer] 명령을 트리거할 수 있습니다.

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  for (var i = 0; i < results.propositions.length; i++) {
    //Execute the propositions and collect the Analytics payload
  }
});
```

여기에서 제안을 실행하고 [!DNL Analytics]&#x200B;(으)로 전송될 페이로드를 구성하는 코드를 구현해야 합니다. 다음은 `results.propositions`에 포함될 수 있는 예입니다.

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
        "analyticsToken": "434689:0:0|2,434689:0:0|1"
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
        "analyticsToken": "434689:0:0|32767"
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434688"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
          "displayToken": "91TS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqgEt==",
          "clickToken": "Tagb6q1+WyFW3FMbbQJrtg==",
          "analyticsDisplayTokens": "434688:0:0|2,434688:0:0|1",
          "analyticsClickTokens": "434688:0:0|32767"
        }
      }
    },
    "items": [
      {
        "id": "1184845",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434688",
          "experience.id": "0",
          "activity.name": "a4t test form based activity 1",
          "offer.id": "1184845"
        },
        "data": {
          "id": "1184845",
          "format": "text/html",
          "content": "<div> analytics impressions 1</div>"
        }
      },
      {
        "id": "434688",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

콘텐츠 항목이 있는 제안에서 [!DNL Analytics] 토큰을 추출하려면 다음과 유사한 함수를 구현할 수 있습니다.

```javascript
function getDisplayAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsDisplayToken) {
    return characteristics.analyticsDisplayToken;
  }
  return characteristics.analyticsToken;
}
```

제안에는 해당 항목의 `schema` 속성으로 표시된 대로 여러 유형의 항목이 있을 수 있습니다. [!UICONTROL Form-Based Experience Composer] 활동에 대해 지원되는 제안 항목 스키마는 네 개입니다.

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA` 및 `JSON_SCHEMA`은(는) 오퍼 형식을 반영하는 스키마이며 `MEASUREMENT_SCHEMA`은(는) DOM 요소에 연결해야 하는 지표를 반영합니다.

방문자가 이전에 표시된 콘텐츠를 실제로 클릭하는 시점에 클릭 지표에 대한 [!DNL Analytics] 페이로드를 수집하여 콘텐츠 항목과는 별도로 [!DNL Analytics]에 전송해야 합니다.

이 경우 클릭 지표 A4T 페이로드를 가져오는 데 사용되는 다음 도우미 함수가 유용합니다.

```javascript
function getClickAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsClickToken) {
    return characteristics.analyticsClickToken;
  }
  return characteristics.analyticsToken;
}
```

#### 구현 요약 {#implementation-summary}

요약하면 [!UICONTROL Form-Based Experience Composer]에 [!DNL Experience Platform Web SDK] 활동을 적용할 때 다음 단계를 실행해야 합니다.

1. [!UICONTROL Form-Based Experience Composer]개의 활동 오퍼를 가져오는 이벤트를 보냅니다.
1. 페이지에 콘텐츠 변경 사항을 적용합니다.
1. `decisioning.propositionDisplay` 알림 이벤트 보내기;
1. SDK 응답에서 [!DNL Analytics] 표시 토큰을 수집하고 [!DNL Analytics] 히트에 대한 페이로드를 구성합니다.
1. [!DNL Analytics]데이터 삽입 API[를 사용하여 페이로드를 ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)에 보냅니다.
1. 전달된 제안에 클릭 지표가 있는 경우 클릭이 수행될 때 `decisioning.propositionInteract` 알림 이벤트를 전송하도록 클릭 수신기를 설정해야 합니다. `onBeforeEventSend` 이벤트를 가로채면 다음 작업이 발생하도록 `decisioning.propositionInteract` 처리기를 구성해야 합니다.
   1. [!DNL Analytics]에서 클릭 `xdm._experience.decisioning.propositions`개 토큰 수집 중
   1. [!DNL Analytics]데이터 삽입 API[!DNL Analytics]를 통해 수집된 [ 페이로드와 함께 클릭 ](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md) 히트를 보내는 중;

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  var analyticsPayload = new Set();
  results.propositions.forEach(function (proposition) {
    proposition.items.forEach(function (item) {
      if (item.schema === HTML_SCHEMA) {
        // 1. Apply offer
        // 2. Collect executed propositions and send the decisioning.propositionDisplay notification event
        // 3. Collect the display Analytics tokens
      }
      if (item.schema === MEASUREMENT_SCHEMA) {
        // Setup click listener, so that when clicked:
        // 1. Collect clicked propositions and send the decisioning.propositionInteract notification event
        // Note: onBeforeEventSend handler should be configured, so that when intercepting decisioning.propositionInteract events:
        //   1. Collect the click Analytics tokens from xdm._experience.decisioning.propositions
        //   2. Send the click Analytics hit with the collected Analytics payload via Data Insertion API
      }
    });
  });
  // Send the page view Analytics hit with the collected display Analytics payload via Data Insertion API
});
```

### [!UICONTROL Visual Experience Composer]&#x200B;(VEC) 활동 {#visual-experience-composer-acitivties}

[!DNL Platform Web SDK]을(를) 사용하면 [VEC(시각적 경험 작성기)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=ko)를 사용하여 작성된 오퍼를 처리할 수 있습니다.

>[!NOTE]
>
>이 사용 사례를 구현하는 단계는 [양식 기반 경험 작성기 활동](#form-based-composer)의 단계와 매우 유사합니다. 자세한 내용은 이전 섹션을 검토하십시오.

자동 렌더링이 활성화되면 페이지에서 실행된 제안에서 [!DNL Analytics] 토큰을 수집할 수 있습니다. 가장 좋은 방법은 [!DNL Experience Platform Web SDK] `sendEvent` 명령을 체인한 다음 반환된 제안을 반복하여 웹 SDK에서 렌더링하려고 한 제안을 필터링하는 것입니다.

**예**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  
  for (var i = 0; i < results.propositions.length; i++) {
  
    var proposition = propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getDisplayAnalyticsPayload(proposition);
      
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // Send the page view Analytics hit with collected Analytics payload via Data Insertion API
});
```

### `onBeforeEventSend`을(를) 사용하여 페이지 지표 처리 {#using-onbeforeeventsend}

[!DNL Adobe Target] 활동을 사용하면 DOM에 수동으로 연결되거나 DOM에 자동으로 연결된 다양한 지표(VEC 작성 활동)를 페이지에서 설정할 수 있습니다. 두 유형 모두 웹 페이지에서 지연된 최종 사용자 상호 작용입니다.

이를 해결하려면 [!DNL Analytics] `onBeforeEventSend` 후크를 사용하여 [!DNL Adobe Experience Platform Web SDK] 페이로드를 수집하는 것이 좋습니다. `onBeforeEventSend` 후크는 `configure` 명령을 사용하여 구성해야 하며, 데이터 스트림을 통해 전송되는 모든 이벤트에 반영됩니다.

다음은 `onBeforeEventSent`개의 히트를 트리거하도록 [!DNL Analytics]을(를) 구성하는 방법의 예입니다.

```javascript
alloy("configure", {
  datastreamId: "datastream configuration ID",
  orgId: "adobe ORG ID",
  onBeforeEventSend: function(options) {
    const xdm = options.xdm;
    const eventType = xdm.eventType;
    if (eventType === "decisioning.propositionInteract") {
      const analyticsPayloads = new Set();
      const propositions = xdm._experience.decisioning.propositions;

      for (var i = 0; i < propositions.length; i++) {
        var proposition = propositions[i];
        analyticsPayloads.add(getClickAnalyticsPayload(proposition));
      }
      // Trigger the Analytics hit
    }
  }
});
```

## 다음 단계 {#next-steps}

이 안내서에서는 [!DNL Platform Web SDK]의 A4T 데이터에 대한 클라이언트측 로깅을 다룹니다. Edge Network에서 A4T 데이터를 처리하는 방법에 대한 자세한 내용은 [서버측 로깅](/help/dev/implement/a4t/server-side-a4t.md)에 대한 안내서를 참조하십시오.