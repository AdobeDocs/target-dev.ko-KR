---
keywords: targetPageParamsAll, targetpageparamsall, PageParamsAll, pageparamsall, 페이지 매개 변수, 페이지 매개 변수, at.js, 함수, 함수, targetPageParamsAll0
description: 사용 [!UICONTROL targetPageParamsAll()] 함수 [!DNL Adobe Target] at.js JavaScript 라이브러리를 사용하여 요청 코드 외부에서 모든 mbox에 매개 변수를 첨부할 수 있습니다.
title: 사용 방법 [!UICONTROL targetPageParamsAll()] 기능?
feature: at.js
exl-id: 32045e60-6904-42a1-bf71-fd7e167a829f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 55%

---

# [!UICONTROL targetPageParamsAll()]

이 방법을 사용하면 요청 코드의 외부에서 모든 mbox에 매개 변수를 첨부할 수 있습니다.

이 메서드는 여러 mbox 호출에 대해 동일한 매개 변수 집합을 포함하는 데 매우 유용합니다. 이 함수는 고객이 정의해야 합니다. 페이지의 모든 mbox 요청에 전달될 매개 변수 배열을 반환해야 합니다. 이 함수는 at.js가 로드되기 전이나 **[!UICONTROL 관리]** > **[!UICONTROL 구현]** > **[!UICONTROL 편집]** > **[!UICONTROL 코드 설정]** > **[!UICONTROL 라이브러리 헤더]**.

다음을 사용하여 target-global-mbox에 매개 변수를 전달할 수 있습니다. [!UICONTROL targetPageParamsAll()] 다음 방법 중 하나로 작동합니다.

* 앰퍼샌드로 구분된 목록
* 배열
* JSON 개체

## 예

Ampersand-delimited 목록(값은 URL으로 인코딩되어야 함):

```javascript {line-numbers="true"}
function targetPageParamsAll() { 
    return "param1=value1&param2=value2&p3=hello%20world"; 
}
```

배열(값은 URL으로 인코딩될 필요가 없음):

```javascript {line-numbers="true"}
targetPageParamsAll = function() { 
     return ["a=1", "b=2", "c=hello world"]; 
};
```

JSON(값은 URL으로 인코딩될 필요가 없음):

```javascript {line-numbers="true"}
targetPageParamsAll = function() { 
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
