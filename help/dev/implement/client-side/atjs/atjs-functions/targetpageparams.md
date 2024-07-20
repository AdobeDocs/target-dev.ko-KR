---
keywords: targetPageParams, targetpageparams, pageParams, pageparams, 페이지 매개 변수, 페이지 매개 변수, at.js, 함수, 함수, targetPageParams0
description: ' [!DNL Adobe Target] at.js JavaScript 라이브러리에 대해 [!UICONTROL targetPageParams()] 함수를 사용하여 요청 코드 외부에서 글로벌 mbox에 매개 변수를 연결합니다.'
title: '[!UICONTROL targetPageParams()] 함수를 사용하는 방법'
feature: at.js
exl-id: 274e4d1f-843a-443b-ad98-7139dc4a13f8
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 68%

---

# [!UICONTROL targetPageParams()]

이 방법을 사용하면 요청 코드의 외부에서 글로벌 mbox에 매개 변수를 첨부할 수 있습니다.

이 함수는 여러 mbox 호출에 대해 동일한 매개 변수 집합을 포함하는 데 매우 유용합니다. 이 함수는 고객이 정의해야 합니다. 글로벌 mbox 요청에만 전달될 매개 변수 배열을 반환해야 합니다. 이 함수는 at.js가 로드되기 전에 또는 **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit]** > **[!UICONTROL Library Header]**&#x200B;에서 정의할 수 있습니다.

다음 방법 중 하나로 `[!UICONTROL targetPageParams()]` 함수를 사용하여 target-global-mbox에 매개 변수를 전달할 수 있습니다.

* 앰퍼샌드로 구분된 목록
* 배열
* JSON 개체

## 예

Ampersand-delimited 목록(값은 URL으로 인코딩되어야 함):

```javascript {line-numbers="true"}
function targetPageParams() { 
    return "param1=value1&param2=value2&p3=hello%20world"; 
}
```

배열(값은 URL으로 인코딩될 필요가 없음):

```javascript {line-numbers="true"}
targetPageParams = function() { 
     return ["a=1", "b=2", "c=hello world"]; 
};
```

JSON(값은 URL으로 인코딩될 필요가 없음):

```javascript {line-numbers="true"}
targetPageParams = function() { 
  return { 
    "a": 1, 
    "b": 2, 
    "profile": { 
        "age": 26, 
        "country": { 
          "city": "San Francisco" 
        } 
      } 
  }; 
};
```
