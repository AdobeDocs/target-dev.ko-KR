---
keywords: adobe.target.triggerView, triggerView, trigger view, trigger view, at.js, functions, function, viewName, viewname, view name, view name, adobe.target.triggerView1
description: 에 adobe.target.triggerView() 함수 사용 [!DNL Adobe Target] SPA(단일 페이지 애플리케이션)에서 사용할 at.js JavaScript 라이브러리입니다. (at.js 2.x)
title: adobe.target.triggerView() 함수를 사용하는 방법
feature: at.js
exl-id: d6130c56-4e77-4668-ad21-a5b335f8b234
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 37%

---

# adobe.target.triggerView (viewName, options) - at.js 2.x

이 함수는 새 페이지를 로드할 때마다 또는 페이지의 구성 요소가 다시 렌더링될 때 호출할 수 있습니다. `adobe.target.triggerView()` 를 사용하려면 SPA(단일 페이지 애플리케이션)에 대해 를 구현해야 합니다. [!UICONTROL 시각적 경험 작성기] (VEC) [!UICONTROL A/B 테스트] 및 [!UICONTROL 경험 타기팅] (XT) 활동. If `[!UICONTROL adobe.target.triggerView()]` 가 사이트에서 구현되지 않으면 SPA에 VEC를 사용할 수 없습니다. 자세한 내용은 [단일 페이지 애플리케이션 구현](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)을 참조하십시오.

>[!NOTE]
>
>이 함수는 at.js 2.*x*. 이 함수는 at.js 버전 1.*x*&#x200B;와 다른 2.0에 도입된 차이점을 자세히 알 수 있습니다.

| 매개 변수 | 유형 | 필수? | 설명 |
| --- | --- | --- | --- |
| viewName | 문자열 | 예 | 보기를 표현할 문자열 유형으로 모든 이름을 전달합니다. 이 보기 이름은 [!UICONTROL 수정 사항] 마케터가 작업을 만들고 실행할 수 있는 VEC 패널 [!UICONTROL A/B 테스트] 및 [!UICONTROL 경험 타기팅] XT 활동 |
| options | 개체 | 아니오 |  |
| options > page | 부울 | 아니오 | **TRUE**: 페이지의 기본값은 true입니다. page=true일 때 노출 수가 증가하면 [!DNL Target] 백엔드에 알림이 전송됩니다.<P>알림은 항상 다음에 대해 `[!UICONTROL triggerView]` options > page가 false로 설정된 경우를 제외하고 가 호출됩니다.<P>**FALSE:** page=false일 때 노출 수가 증가하면 알림이 전송되지 않습니다. 이 접근 방식은 오퍼가 있는 페이지에서 구성 요소를 다시 렌더링하려는 경우에만 사용해야 합니다.<P>**참고**: 다음과 같은 경우 VEC의 사용자 지정 코드 오퍼가 다시 렌더링되지 않습니다. `[!UICONTROL triggerView()]` 이(가) 다음으로 호출됨 `{page: false}` 을 옵션으로 추가합니다. |

## 예: True

활동 노출 횟수 및 기타 지표를 늘리기 위해 백엔드로 알림을 전송하는 `[!UICONTROL triggerView()]`[!DNL Target] 호출.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView")
```

## 예: False

노출 계산을 위해 백엔드에 전송된 알림을 전송하지 않은 `[!UICONTROL triggerView()]`[!DNL Target] 호출.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView", {page: false})
```

## 예: 다음을 사용하여 약속 체인화 `getoffers()` 및 `applyOffers()`

실행하려면 `triggerView()` 다음과 같은 경우 `getOffers()` 약속이 해결되었습니다. 실행하는 것이 중요합니다. `triggerView()` 아래 예와 같이 최종 블록에서. VEC가 다음을 감지하는 데 필요합니다. `Views` 작성 모드에서.

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
