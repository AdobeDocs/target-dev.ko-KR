---
keywords: adobe.target.triggerView, triggerView, trigger view, trigger view, at.js, functions, function, viewName, viewname, view name, view name, adobe.target.triggerView1
description: SPA(단일 페이지 애플리케이션)에서 사용하려면  [!DNL Adobe Target] at.js JavaScript 라이브러리에 대해 adobe.target.triggerView() 함수를 사용하십시오. (at.js 2.x)
title: adobe.target.triggerView() 함수를 사용하는 방법
feature: at.js
exl-id: d6130c56-4e77-4668-ad21-a5b335f8b234
TQID: https://experienceleague.adobe.com/pBC1GRKG0mxeaZ1hfaByKv2tu-XScrSJfm7lUw-3yKw
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d851e2344279caeae25e4823ca86b9c17efd63
workflow-type: tm+mt
source-wordcount: 446
ht-degree: 19%

---

# adobe.target.triggerView (viewName, options) - at.js 2.x

이 함수는 새 페이지를 로드할 때마다 또는 페이지의 구성 요소가 다시 렌더링될 때 호출할 수 있습니다. [!UICONTROL 시각적 경험 작성기]&#x200B;(VEC)를 사용하여 [!UICONTROL A/B 테스트] 및 [!UICONTROL 경험 타깃팅]&#x200B;(XT) 활동을 만들려면 단일 페이지 응용 프로그램(SPA)에 대해 `adobe.target.triggerView()`을(를) 구현해야 합니다. 사이트에서 `[!UICONTROL adobe.target.triggerView()]`이(가) 구현되지 않으면 SPA에 VEC를 사용할 수 없습니다. 자세한 내용은 [단일 페이지 애플리케이션 구현](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)을 참조하십시오.

>[!NOTE]
>
>이 함수는 at.js 2.*x*&#x200B;에서 도입되었습니다. 이 함수는 at.js 버전 1.*x*&#x200B;에서 사용할 수 없습니다.

| 매개 변수 | 유형 | 필수? | 설명 |
| --- | --- | --- | --- |
| viewName | 문자열 | 예 | 보기를 표현할 문자열 유형으로 모든 이름을 전달합니다. 이 보기 이름은 마케터가 작업을 만들고 [!UICONTROL A/B 테스트] 및 [!UICONTROL 경험 타깃팅] XT 활동을 실행하는 VEC의 [!UICONTROL 수정 사항] 패널에 표시됩니다. |
| options | 개체 | 아니오 |  |
| options > page | 부울 | 아니오 | **TRUE**: 페이지의 기본값은 true입니다. page=true일 때 노출 수가 증가하면 [!DNL Target] 백엔드에 알림이 전송됩니다.<P>`[!UICONTROL triggerView]`이(가) 호출될 때 옵션 > 페이지가 false로 설정된 경우를 제외하고 기본적으로 알림이 전송됩니다.<P>**FALSE:** page=false일 때 노출 수가 증가하면 알림이 전송되지 않습니다. 이 접근 방식은 오퍼가 있는 페이지에서 구성 요소를 다시 렌더링하려는 경우에만 사용해야 합니다.<P>**참고**: 옵션으로 `{page: false}`을(를) 사용하여 `[!UICONTROL triggerView()]`을(를) 호출하면 VEC의 사용자 지정 코드 오퍼가 다시 렌더링되지 않습니다. |

## 예: True

활동 노출 횟수 및 기타 지표를 늘리기 위해 [!DNL Target] 백엔드로 알림을 보내는 `[!UICONTROL triggerView()]` 호출.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView")
```

## 예: False

노출 계산을 위해 [!DNL Target] 백엔드에 전송된 알림을 전송하지 않은 `[!UICONTROL triggerView()]` 호출입니다.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView", {page: false})
```

## 예: `getoffers()` 및 `applyOffers()`(으)로 Promise 체인

`getOffers()` 약속이 해결될 때 `triggerView()`을(를) 실행하려면 아래 예와 같이 최종 블록에서 `triggerView()`을(를) 실행해야 합니다. VEC가 작성 모드에서 `Views`을(를) 감지하는 데 필요합니다.

```javascript {line-numbers="true"}
adobe.target.getOffers({
    'request': {
        'prefetch': {
            'views': [{
                'parameters': {}
            }]
        }
    }
}).then(function(response) {
    // Apply Offers
    adobe.target.applyOffers({
        response: response
    });
}).catch(function(error) {
    console.log("AT: getOffers failed - Error", error);
}).finally(() => {
    // Trigger View call, assuming pageView is defined elsewhere
    adobe.target.triggerView(pageView, {
        page: true
    });
    console.log('AT: View triggered on : ' + pageView);
});
```

## 예: [!UICONTROL Adobe Visual Editing Helper 확장 기능]을 사용한 `triggerView()`에 대한 최상의 호환성

[Adobe Visual Editing Helper 확장 기능](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension){target=_blank}을 사용할 때는 다음 사항을 고려하십시오.

[!DNL Chrome] 확장에 대한 [!DNL Googl]e의 새 V3 매니페스트 정책으로 인해 [!UICONTROL Visual Editing Helper 확장 기능]은(는) VEC에서 [!DNL Target] 라이브러리를 로드하기 전에 `DOMContentLoaded` 이벤트를 기다려야 합니다. 이 지연으로 인해 작성 라이브러리가 준비되기 전에 웹 페이지에서 `triggerView()` 호출이 실행되어 로드 시 보기가 채워지지 않을 수 있습니다.

이 문제를 완화하려면 페이지 `load` 이벤트에 대한 수신기를 사용합니다.

다음은 구현의 예입니다.

```javascript
function triggerViewIfLoaded() {
    adobe.target.triggerView("homeView");
}

if (document.readyState === "complete") {
    // If the page is already loaded
    triggerViewIfLoaded();
} else {
    // If the page is not yet loaded, set up an event listener
    window.addEventListener("load", triggerViewIfLoaded);
}
```




