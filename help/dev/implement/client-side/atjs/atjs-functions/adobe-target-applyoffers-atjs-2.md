---
keywords: adobe.target.applyOffers, applyOffers, applyOffers, apply 오퍼, at.js, 함수, 함수,
description: ' [!DNL Adobe Target] at.js JavaScript 라이브러리에 대해 [!UICONTROL adobe.target.applyOffers()] 함수를 사용하여 응답에 여러 오퍼를 적용합니다. (at.js 2.x)'
title: '[!UICONTROL adobe.target.applyOffers()] 함수를 사용하는 방법'
feature: at.js
exl-id: c391e3f4-fdf1-4e33-8dcb-6bf46e390538
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 80%

---

# [!UICONTROL adobe.target.applyOffers(options)] - at.js 2.x

이 함수를 사용하면 `adobe.target.getOffers()`로 검색된 오퍼를 두 개 이상 적용할 수 있습니다.

>[!NOTE]
>
>이 함수는 at.js 2.*x*. 이 함수는 at.js 버전 1.*x*&#x200B;에는 사용할 수 없습니다.

| 키 | 유형 | 필수? | 설명 |
| --- | --- | --- | --- |
| selector | 문자열 | 아니오 | [!DNL Target]이 오퍼 컨텐츠를 배치해야 하는 HTML 요소를 식별하는 데 사용되는 HTML 요소 또는 CSS 선택기입니다. 선택기를 제공하지 않으면 [!DNL Target]에서 사용할 HTML 요소를 HTML HEAD으로 간주합니다. |
| 응답 | 개체 | 예 | `getOffers()`의 응답 개체.<br />아래의 &quot;요청&quot; 표를 참조하십시오. |

## 응답

>[!NOTE]
>
>아래 나열된 모든 필드에 허용되는 유형에 대한 자세한 내용은 [배달 API 설명서](/help/dev/implement/delivery-api/overview.md)를 참조하십시오.

| 필드 이름 | 설명 |
| --- | --- |
| response > prefetch > views > options > content | &quot;선택 사항&quot;의 컨텐츠가 잘 정의되어 있지 않으며 선택 사항 유형/템플릿 구조에 직접적으로 의존합니다. |
| response > prefetch > views > options > type | 선택 사항 유형. &quot;컨텐츠&quot; 필드의 유형을 반영합니다. 지원되는 유형은 작업입니다. |
| response > prefetch > views > state | 보기에 대한 디스플레이 알림과 함께 전달해야 하는 불투명 보기 상태 토큰 |
| response > prefetch > views > options > responseTokens | 현재 선택 사항이 처리 중일 때 수집된 `responseTokens`의 맵을 포함합니다. |
| response > prefetch > views > analytics > payload | 보기를 적용한 후 [!DNL Analytics]에 전송해야 하는 클라이언트측 통합을 위한 [!DNL Analytics] 페이로드입니다. |
| response > prefetch > views > trace | 보기당 미리 가져오기 호출에 대한 모든 추적 데이터를 포함하는 개체.<br />추적 개체에는 추적용 버전도 포함됩니다.<br />추적 개체에는 현재 보기에 대한 세부 정보도 포함됩니다. |
| response > prefetch > views > options > eventToken | 이벤트 로깅은 선택 사항별로 수행됩니다. 적용된 모든 선택 사항에 대해 각각의 이벤트 토큰을 알림 토큰 목록에 추가해야 합니다. 보기는 여러 선택 사항으로 구성됩니다. 모든 선택 사항이 적용되어 표시되면 모든 `eventTokens`이 알림에 포함되어야 합니다. |
| response > prefetch > views > name | 사람이 읽을 수 있는 보기 이름. |
| response > prefetch > views > metrics | 감시하고 [!DNL Target]에 알려야 하는 보고 지표. 현재, 클릭 지표만 지원됩니다. 요소를 클릭하면 적절한 `eventTokens`가 수집되고 알림이 전송되어야 합니다. |
| response > prefetch > views > key | 보기를 식별하는 키 또는 지문. |
| response > prefetch > views > id | 보기의 ID. |
| 응답 > 알림 > ID | 알림 ID. |
| response > notifications > events > type | 알림, 클릭 또는 표시의 유형. |
| response > notifications > events > trace | 알림 이벤트에 대한 추적. |
| response > notifications > events > token | 알림 이벤트와 함께 전송된 토큰. |
| response > notifications > events > timestamp | 알림 이벤트와 함께 전송된 타임스탬프. |
| response > notifications > events > errorCode | 알림이 실패한 경우 코드가 실패 이유를 나타냅니다. |
| response > notifications > events | 현재 알림에 대해 기록되었거나 기록되지 않은 이벤트. |
| response > notifications | 기록되었거나 실패한 알림을 가리킵니다. |
| response > execute > mboxes > mbox > trace | 개별 mbox 요청에 대한 모든 추적 데이터를 포함하는 개체. |
| response > execute > mboxes > mbox > responseTokens | 특정 mbox 요청 실행을 위한 `responseTokens`의 맵을 포함합니다. |
| response > execute > mboxes > mbox > option > content | &quot;선택 사항&quot;의 컨텐츠가 잘 정의되어 있지 않으며 선택 사항 유형/템플릿 구조에 직접적으로 의존합니다. |
| response > execute > mboxes > mbox > option > type | 선택 사항 유형. &quot;컨텐츠&quot; 필드의 유형을 반영합니다. 지원되는 유형은 html, 리디렉션, JSON 및 다이내믹입니다. |
| response > execute > mboxes > mbox > options | 응답 선택 사항. |
| response > execute > mboxes > mbox > metrics > eventToken | 클릭 이벤트의 토큰. |
| response > execute > mboxes > mbox > metrics > type | &quot;click&quot; |
| response > execute > mboxes > mbox > metrics | `clickThrough` 지표 목록을 포함합니다. |
| response > execute > mboxes > mbox > mbox | mbox의 이름. |
| response > execute > mboxes > mbox >index | 응답이 요청에서 나온 이 색인이 있는 mbox용임을 나타냅니다. |
| response > execute > mboxes > mbox > analytics > payload | mbox가 적용된 후 [!DNL Analytics](으)로 전송해야 하는 클라이언트측 통합을 위한 [!DNL Analytics] 페이로드입니다. (A4T 사용 &quot;캠페인&quot; 섹션을 참조하십시오.) |
| response > execute > mboxes | 실행된 mbox 목록. |
| response > execute > pageLoad > options > content | &quot;선택 사항&quot;의 컨텐츠가 잘 정의되어 있지 않으며 선택 사항 유형/템플릿 구조에 직접적으로 의존합니다. |
| response > execute > pageLoad > options > type | 선택 사항 유형. &quot;컨텐츠&quot; 필드의 유형을 반영합니다. 지원되는 유형은 html, 리디렉션, JSON, 다이내믹 및 작업입니다. |
| response > execute > pageLoad > options | 보기를 기준으로 그룹화되지 않은 선택 사항(target-global-mbox + 보기를 기준으로 그룹화되지 않은 보기를 사용하는 활동의 선택 사항). |
| response > execute > pageLoad > metrics | 특정 보기에 속하도록 설정되지 않은 클릭 지표. |
| response > execute > pageLoad > trace | pageLoad 요청에 대한 모든 추적 데이터를 포함하는 개체. |
| response > execute > pageLoad > analytics > payload | 페이지 로드 콘텐츠가 적용된 후 [!DNL Analytics](으)로 전송해야 하는 클라이언트측 통합을 위한 [!DNL Analytics] 페이로드입니다. (A4T 사용 &quot;캠페인&quot; 섹션을 참조하십시오.) |

## [!UICONTROL applyOffers()] 호출 예

```javascript {line-numbers="true"}
adobe.target.applyOffers({response:{
  "execute": {
    "pageLoad": {
      "options": [{
        "type": "html",
        "content": "page-load"
      },
      {
        "type": "actions",
        "content": [{
          "type": "setHtml",
          "content": "<h1>Container 1</h1>",
          "selector": "#container1",
          "cssSelector": "#container1"
        },
        {
          "type": "setHtml",
          "content": "<h3>Container 3</h3>",
          "selector": "#container3",
          "cssSelector": "#container3"
        }]
      }],
 
 
      "metrics": [{
        "type": "click",
        "selector": "#container1",
        "eventToken": "page-load-click-metric" 
      }]
    }
  }
}});
```

## `[!UICONTROL getOffers()]` 및 `[!UICONTROL applyOffers()]`이(가) Promise 기반이므로 이 함수를 사용하는 Promise 체인 호출 예

```javascript {line-numbers="true"}
adobe.target.getOffers({...})
.then(response => adobe.target.applyOffers({ response: response }))
.then(() => console.log("Success"))
.catch(error => console.log("Error", error));
```

getOffers()를 사용하는 방법에 대한 자세한 예는 getOffers [설명서](adobe-target-getoffers-atjs-2.md)를 참조하십시오.

### 페이지 로드 요청 예


```javascript {line-numbers="true"}
adobe.target.getOffers({
    request: {
        execute: {
            pageLoad: {}
        }
    }
}).
then(response => adobe.target.applyOffers({ response: response }))
.then(() => console.log("Success"))
.catch(error => console.log("Error", error));
```
