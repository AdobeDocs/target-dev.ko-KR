---
keywords: targetPageParamsAll, targetpageparamsall, PageParamsAll, pageparamsall, 페이지 매개 변수, 페이지 매개 변수, at.js, 함수, 함수, targetPageParamsAll0
description: ' [!DNL Adobe Target] at.js JavaScript 라이브러리에 대해 [!UICONTROL targetPageParamsAll()] 함수를 사용하여 요청 코드 외부에서 모든 mbox에 매개 변수를 연결합니다.'
title: '[!UICONTROL targetPageParamsAll()] 함수를 사용하는 방법'
feature: at.js
exl-id: 32045e60-6904-42a1-bf71-fd7e167a829f
TQID: https://experienceleague.adobe.com/A2sZYp7CeE3-zGcqfbvgo32auAtXBKN0dYNa84grs1Q
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
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 160
ht-degree: 70%

---

# [!UICONTROL targetPageParamsAll()]

이 방법을 사용하면 요청 코드의 외부에서 모든 mbox에 매개 변수를 첨부할 수 있습니다.

이 메서드는 여러 mbox 호출에 대해 동일한 매개 변수 집합을 포함하는 데 매우 유용합니다. 이 함수는 고객이 정의해야 합니다. 페이지의 모든 mbox 요청에 전달될 매개 변수 배열을 반환해야 합니다. 이 함수는 at.js가 로드되기 전에 또는 **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit]** > **[!UICONTROL Code Settings]** > **[!UICONTROL Library Header]**&#x200B;에서 정의할 수 있습니다.

다음 방법 중 하나로 [!UICONTROL targetPageParamsAll()] 함수를 사용하여 target-global-mbox에 매개 변수를 전달할 수 있습니다.

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
