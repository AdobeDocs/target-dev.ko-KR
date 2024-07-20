---
keywords: adobe.target.getOffers, getOffers, getoffers, 오퍼 가져오기, at.js, 함수, 함수, $8
description: ' [!DNL Adobe Target] at.js 라이브러리에 대한 [!UICONTROL adobe.target.getOffers()] 함수와 해당 옵션을 사용하여 여러 [!DNL Target] 오퍼를 가져오는 요청을 실행합니다. (at.js 2.x)'
title: '[!UICONTROL adobe.target.getOffers()] 함수를 사용하는 방법'
feature: at.js
exl-id: b96a3018-93eb-49e7-9aed-b27bd9ae073a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1317'
ht-degree: 62%

---

# [!UICONTROL adobe.target.getOffers()] - at.js 2.x

이 함수를 사용하면 여러 mbox를 전달하여 여러 오퍼를 검색할 수 있습니다. 또한 활성 활동의 모든 보기에 대해 여러 오퍼를 검색할 수 있습니다.

>[!NOTE]
>
>이 함수는 at.js 2.x에서 도입되었으며, at.js 버전 1.*x*&#x200B;에는 사용할 수 없습니다.

| 키 | 유형 | 필수? | 설명 |
| --- | --- | --- | --- |
| `consumerId` | 문자열 | 아니오 | 기본값이 제공되지 않을 경우 기본값은 클라이언트의 글로벌 mbox입니다. 이 키는 A4T 통합에 사용되는 SDID(Supplemental Data ID)를 생성하는 데 사용됩니다.<P>`getOffers()`을(를) 사용할 때 각 호출은 새 SDID를 생성합니다. 동일한 페이지에 여러 개의 mbox 요청이 있고 SDID를 유지하려는 경우(target-global-mbox의 SDID와 [!DNL Adobe Analytics] SDID가 일치하도록) `consumerId` 매개 변수를 사용하십시오.<P>`getOffers()`에 &quot;mbox1&quot;, &quot;mbox2&quot; 및 &quot;mbox3&quot;이라는 mbox가 3개 있는 경우 `getOffers()` 호출에 `consumerId: "mbox1, mbox2, mbox3"`을(를) 포함하십시오. |
| `decisioningMethod` | 문자열 | 아니오 | &quot;서버측&quot;, &quot;온디바이스&quot;, &quot;하이브리드&quot; |
| `request` | 개체 | 예 | 아래의 &quot;요청&quot; 표를 참조하십시오. |
| `timeout` | 숫자 | 아니오 | 요청 시간 제한. 지정하지 않으면 기본값 at.js 시간 제한이 사용됩니다. |

## 요청

>[!NOTE]
>
>아래 나열된 모든 필드에 허용되는 유형에 대한 자세한 내용은 [배달 API 설명서](/help/dev/implement/delivery-api/overview.md)를 참조하십시오.

| 필드 이름 | 필수? | 제한 | 설명 |
| --- | --- | --- | --- |
| request > id | 아니오 |  | `tntId`, `thirdPartyId`, `marketingCloudVisitorId` 중 하나는 필수입니다. |
| request > id > thirdPartyId | 아니오 | 최대 크기 = 128. |  |  |
| Request > experienceCloud | 아니오 |  |  |
| Request > experienceCloud > analytics | 아니오 |  | Adobe Analytics 통합 |
| Request > experienceCloud > analytics > logging | 아니오 | 페이지에서 다음을 구현해야 합니다.<ul><li>방문자 ID 서비스</li><li>Appmeasurement.js</li></ul> | 지원되는 값은 다음과 같습니다.<P>**client_side**: 지정하면 [!UICONTROL Data Insertion API]을(를) 통해 [!UICONTROL Adobe Analytics]에 보내는 데 사용해야 하는 호출자에게 분석 페이로드가 반환됩니다.<P>**server_side**: [!DNL Target] 및 [!DNL Analytics] 백엔드가 보고 목적으로 SDID를 사용하여 호출을 함께 연결하는 기본값입니다. |
| request > prefetch | 아니오 |  |  |
| request > prefetch > views | 아니오 | 최대 개수 50.<P>이름은 비워둘 수 없습니다.<P>이름 길이 `<=` 128.<P>값 길이 `<=` 5000입니다.<P>이름은 &quot;profile&quot;로 시작하면 안 됩니다.<P>허용되지 않는 이름: &quot;orderId&quot;, &quot;orderTotal&quot;, &quot;productPurchasedId&quot;. | 활성 활동에서 적절한 보기를 검색하는 데 사용할 매개 변수를 전달합니다. |
| request > prefetch > views > profileParameters | 아니오 | 최대 개수 50.<P>이름은 비워둘 수 없습니다.<P>이름 길이 `<=` 128.<P>값 길이 `<=` 5000입니다.<P>문자열 값만 허용합니다.<P>이름은 &quot;profile&quot;로 시작하면 안 됩니다. | 활성 활동에서 적절한 보기를 검색하는 데 사용할 프로필 매개 변수를 전달합니다. |
| request > prefetch > views > product | 아니오 |  |  |
| request > prefetch > views > product -> id | 아니오 | 비어 있지 않음.<P>최대 크기 = 128. | 활성 활동에서 적절한 보기를 검색하는 데 사용할 제품 ID를 전달합니다. |
| request > prefetch > views > product > categoryId | 아니오 | 비어 있지 않음.<P>최대 크기 = 128. | 활동에서 적절한 보기를 검색하는 데 사용할 제품 카테고리 ID를 전달합니다. |
| request > prefetch > views > order | 아니오 |  |  |
| request > prefetch > views > order > id | 아니오 | 최대 길이 = 250. | 활성 활동에서 적절한 보기를 검색하는 데 사용할 주문 ID를 전달합니다. |
| request > prefetch > views > order > total | 아니오 | 총 `>=`개 | 활성 활동에서 적절한 보기를 검색하는 데 사용할 주문 합계를 전달합니다. |
| request > prefetch > views > order > purchasedProductIds | 아니오 | 빈 값이 없습니다.<P>각 값의 최대 길이는 50자입니다.<P>쉼표로 연결 및 구분됩니다.<P>제품 ID의 총 길이는 `<=` 250입니다. | 활성 활동에서 적절한 보기를 검색하는 데 사용할 구입 제품 ID를 전달합니다. |
| request > execute | 아니오 |  |  |
| request > execute > pageLoad | 아니오 |  |  |
| request > execute > pageLoad > parameters | 아니오 | 최대 개수 50.<P>이름은 비워둘 수 없습니다.<P>이름 길이 `<=` 128.<P>값 길이 `<=` 5000입니다.<P>문자열 값만 허용합니다.<P>이름은 &quot;profile&quot;로 시작하면 안 됩니다.<P>허용되지 않는 이름: &quot;orderId&quot;, &quot;orderTotal&quot;, &quot;productPurchasedId&quot;. | 페이지가 로드될 때 지정된 매개 변수로 오퍼를 검색합니다. |
| request > execute > pageLoad > profileParameters | 아니오 | 최대 개수 50.<P>이름은 비워둘 수 없습니다.<P>이름 길이 `<=` 128.<P>값 길이 `<=`256.<P>이름은 &quot;profile&quot;로 시작하면 안 됩니다.<P>문자열 값만 허용합니다. | 페이지가 로드될 때 지정된 프로필 매개 변수로 오퍼를 검색합니다. |
| request > execute > pageLoad > product | 아니오 |  |  |
| request > execute > pageLoad > product -> id | 아니오 | 비어 있지 않음.<P>최대 크기 = 128. | 페이지가 로드될 때 지정된 제품 ID로 오퍼를 검색합니다. |
| request > execute > pageLoad > product > categoryId | 아니오 | 비어 있지 않음.<P>최대 크기 = 128. | 페이지가 로드될 때 지정된 카테고리 ID로 오퍼를 검색합니다. |
| request > execute > pageLoad > order | 아니오 |  |  |
| request > execute > pageLoad > order > id | 아니오 | 최대 길이 = 250. | 페이지가 로드될 때 지정된 주문 ID로 오퍼를 검색합니다. |
| request > execute > pageLoad > order > total | 아니오 | `>=` 0. | 페이지가 로드될 때 지정된 주문 합계로 오퍼를 검색합니다. |
| request > execute > pageLoad > order > purchasedProductIds | 아니오 | 빈 값이 없습니다.<P>각 값의 최대 길이는 50자입니다.<P>쉼표로 연결 및 구분됩니다.<P>제품 ID의 총 길이는 `<=` 250입니다. | 페이지가 로드될 때 지정된 구입 제품 ID로 오퍼를 검색합니다. |
| request > execute > mboxes | 아니오 | 최대 크기 = 50.<P>null 요소가 없습니다. |  |
| request > execute > mboxes>mbox | 예 | 비어 있지 않음.<P>&#39;-clicked&#39; 접미사가 없습니다.<P>최대 크기 = 250.<P>허용되는 문자: `'-, ._\/=:;&!@#$%^&*()_+|?~[]{}'` | mbox 이름. |
| request > execute > mboxes>mbox>index | 예 | null 아님<P>고유.<P>`>=` 0. | 색인은 mbox가 처리되는 순서를 나타내지 않습니다. 몇 개의 지역 mbox가 있는 웹 페이지에서와 마찬가지로, 처리되는 순서를 지정할 수 없습니다. |
| request > execute > mboxes > mbox > parameters | 아니오 | 최대 개수 = 50.<P>이름은 비워둘 수 없습니다.<P>이름 길이 `<=` 128.<P>문자열 값만 허용합니다.<P>값 길이 `<=` 5000입니다.<P>이름은 &quot;profile&quot;로 시작하면 안 됩니다.<P>허용되지 않는 이름: &quot;orderId&quot;, &quot;orderTotal&quot;, &quot;productPurchasedId&quot;. | 지정된 매개 변수를 사용하여 주어진 mbox에 대한 오퍼를 검색합니다. |
| request > execute > mboxes>mbox>profileParameters | 아니오 | 최대 개수 = 50.<P>이름은 비워둘 수 없습니다.<P>이름 길이 `<=` 128.<P>문자열 값만 허용합니다.<P>값 길이 `<=`256.<P>이름은 &quot;profile&quot;로 시작하면 안 됩니다. | 지정된 프로필 매개 변수를 사용하여 주어진 mbox에 대한 오퍼를 검색합니다. |
| request > execute > mboxes>mbox > product | 아니오 |  |  |
| request > execute > mboxes > mbox > product > id | 아니오 | 비어 있지 않음.<P>최대 크기 = 128. | 지정된 제품 ID를 사용하여 주어진 mbox에 대한 오퍼를 검색합니다. |
| request > execute > mboxes > mbox > product > categoryId | 아니오 | 비어 있지 않음.<P>최대 크기 = 128. | 지정된 제품 카테고리 ID를 사용하여 주어진 mbox에 대한 오퍼를 검색합니다. |
| request > execute > mboxes > mbox > order | 아니오 |  |  |
| request > execute > mboxes>mbox > order > id | 아니오 | 최대 길이 = 250. | 지정된 주문 ID를 사용하여 주어진 mbox에 대한 오퍼를 검색합니다. |
| request > execute > mboxes > mbox > order > total | 아니오 | `>=` 0. | 지정된 주문 합계를 사용하여 주어진 mbox에 대한 오퍼를 검색합니다. |
| request > execute > mboxes > mbox > order > purchasedProductIds | 아니오 | 빈 값이 없습니다.<P>각 값의 최대 길이 = 50.<P>쉼표로 연결 및 구분됩니다.<P>제품 ID의 총 길이는 `<=` 250입니다. | 지정된 주문 구입 제품 ID를 사용하여 주어진 mbox에 대한 오퍼를 검색합니다. |

## 모든 보기에 대해 [!UICONTROL getOffers()] 호출

```javascript {line-numbers="true"}
adobe.target.getOffers({
    request: {
      prefetch: {
        views: [{}]
    }
  }
});
```

## [!UICONTROL getOffers()]을(를) 호출하여 온디바이스 의사 결정

```javascript {line-numbers="true"}
adobe.target.getOffers({ 

  decisioningMethod:"on-device", 
  request: { 
    execute: { 
      mboxes: [ 
        { 
          index: 0, 
          name: "homepage" 
        } 
      ] 
    } 
 } 
}); 
```

## 전달된 매개 변수 및 프로필 매개 변수를 사용하여 최신 보기를 검색하기 위해 [!UICONTROL getOffers()] 호출

```javascript {line-numbers="true"}
adobe.target.getOffers({
  request: {
    "prefetch": {
      "views": [
        {
          "parameters": {
            "ad": "1"
          },
          "profileParameters": {
            "age": 23
          }
        }
      ]
    }
  }
});
```

## 전달된 매개 변수와 프로필 매개 변수를 사용하여 mbox를 검색하기 위해 [!UICONTROL getOffers()] 호출

```javascript {line-numbers="true"}
adobe.target.getOffers({
  request: {
    execute: {
      mboxes: [
        {
          index: 0,
          name: "first-mbox"
        },
        {
          index: 1,
          name: "second-mbox",
          parameters: {
            a: 1
          },
          profileParameters: {
            b: 2
          }
        }
      ]
    }
  }
});
```

## [!UICONTROL getOffers()]을(를) 호출하여 클라이언트 측에서 분석 페이로드를 검색합니다.

```javascript {line-numbers="true"}
adobe.target.getOffers({
      request: {
        experienceCloud: {
          analytics: {
            logging: "client_side"
          }
        },
        prefetch: {
          mboxes: [{
            index: 0,
            name: "a1-serverside-xt"
          }]
        }
      }
    })
    .then(console.log)
```

**응답**:

```javascript {line-numbers="true"}
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "bucharest",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "romania"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}
```

[데이터 삽입 API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)를 통해 페이로드를 [!DNL Adobe Analytics]에 전달할 수 있습니다.

## [!UICONTROL getOffers()] 및 [!UICONTROL applyOffers()]을(를) 통해 여러 mbox에서 데이터를 가져와 렌더링합니다.

at.js 2.x를 사용하면 `[!UICONTROL getOffers()]` API를 통해 여러 mbox를 가져올 수 있습니다. 여러 mbox에 대한 데이터를 가져온 다음 CSS 선택기에서 식별한 다른 위치에 데이터를 렌더링하는 데 `[!UICONTROL applyOffers()]`를 사용할 수도 있습니다.

다음 예는 at.js 2.x가 구현된 간단한 HTML 페이지를 보여줍니다.

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>at.js 2.x, multiple selectors and multiple mboxes</title>
  <script src="at.js"></script>
</head>
<body>
  <div id="container1">Default content 1</div>
  
  <div id="container2">Default content 2</div>

  <div id="container3">Default content 3</div>
</body>
</html>
```

[!DNL Target]에서 받은 콘텐츠를 통해 수정할 컨테이너가 3개 있다고 가정합니다. 각 mbox에 각 컨테이너로 렌더링할 콘텐츠가 있는 세 개의 mbox에 대해 단일 요청을 구성할 수 있습니다.

요청 및 렌더링 코드는 다음 예제와 비슷합니다.

```javascript {line-numbers="true"}
adobe.target.getOffers({
  request: {
    prefetch: {
      mboxes: [
        {
          index: 0,
          name: "mbox1"
        },
        {
          index: 1,
          name: "mbox2"
        },
        {
          index: 2,
          name: "mbox3"
        }
      ]
    }
  }
})
.then(response => {
  // get all mboxes from response
  const mboxes = response.prefetch.mboxes;
  let count = 1;

  mboxes.forEach(el => {
    adobe.target.applyOffers({
      selector: "#container" + count,
      response: {
        prefetch: {
          mboxes: [el]
        }
      }
    });

    count += 1;
  });
});
```

`request > prefetch > mboxes` 섹션에는 세 개의 다른 mbox가 있습니다. 요청이 성공적으로 완료되면 `response > prefetch > mboxes`에서 각 mbox에 대한 응답을 받게 됩니다. 응답 및 렌더링에 사용할 위치가 있으면 [!DNL Target]에서 검색된 콘텐츠를 렌더링하도록 `applyOffers()`를 호출할 수 있습니다. 이 예에는 다음 매핑이 있습니다.

* mbox1 > CSS selector #container1
* mbox2 > CSS selector #container2
* mbox3 > CSS selector #container3

이 예에서는 count 변수를 사용하여 CSS 선택기를 구성합니다. 실제 시나리오에서는 CSS 선택기와 mbox 간에 다른 매핑을 사용할 수 있습니다.

이 예제에서는 `prefetch > mboxes`를 사용하지만 `execute > mboxes`를 사용할 수도 있습니다. `getOffers()`에서 미리 가져오기 작업을 실행하는 경우 `applyOffers()` 호출에서도 미리 가져오기 작업을 실행해야 합니다.

## [!UICONTROL getOffers()]을(를) 호출하여 페이지 로드를 수행합니다.

다음 예제에서는 at.js 2에서 [!UICONTROL getOffers()]을(를) 사용하여 pageLoad를 수행하는 방법을 보여 줍니다.*x*

```javascript {line-numbers="true"}
adobe.target.getOffers({
    request: {
        execute: {
            pageLoad: {
                parameters: {}
            }
        }
    }
});
```
