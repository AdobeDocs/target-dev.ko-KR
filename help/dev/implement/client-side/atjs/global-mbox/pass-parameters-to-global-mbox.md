---
keywords: 글로벌 mbox 매개 변수, targetPageParams, 쿼리 문자열, 배열, json, dtm
description: 사용 방법 알아보기 [!UICONTROL targetPageParams] 에 추가 타겟팅 또는 컨텍스트 정보를 전달하는 함수 [!DNL Adobe Target] 글로벌 mbox.
title: 글로벌 mbox에 매개 변수를 전달하려면 어떻게 합니까?
feature: at.js
exl-id: 2a6be3e4-a618-4812-9e87-b01789705c40
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 60%

---

# 글로벌 mbox에 매개 변수 전달

JavaScript `targetPageParams` 함수는에서 글로벌 mbox에 매개 변수를 전달하는 데 사용됩니다. [!DNL Adobe Target]. 이는 추가 타겟팅/컨텍스트 정보를에 전달해야 하는 모든 시나리오에서 필요합니다 [!DNL Target].

예를 들어, 권장 사항 활동에서 보고 있는 현재 제품 또는 카테고리를 표현하려면 매개 변수를 사용하십시오.

JavaScript 함수를 호출하는 코드는 글로벌 mbox가 at.js의 일부로 실행되는지 또는 페이지 코드에 수동으로 포함되는지에 관계없이 페이지에서 글로벌 mbox 앞에 와야 합니다.

>[!NOTE]
>
>글로벌 mbox뿐만 아니라 페이지의 모든 mbox에 매개 변수를 추가하려면 [targetPageParamsAll()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparamsall.md) 함수.

다음 방법 중 하나로 `target-global-mbox` 함수를 사용하여 `targetPageParams()`에 매개 변수를 전달할 수 있습니다.

* 배열
* JSON 개체
* 앰퍼샌드로 구분된 목록

이 세 가지 방법을 사용하여 매개 변수가 올바로 전달되고 있는지 확인하십시오. [Adobe Experience Cloud Debugger](https://experienceleague.adobe.com/docs/debugger/using/experience-cloud-debugger.html)를 사용하여 매개 변수 전달을 확인할 수도 있습니다.

페이지에 글로벌 mbox를 추가하려면 먼저 JavaScript 함수를 정의해야 합니다. 이름은 `targetPageParams`여야 합니다.

## 쿼리 문자열

```
p1=v1&p2=v2&p3=hello%20world
```

* 이름: `targetPageParams`
* 반환 값: URL로 인코딩된 매개 변수 값을 사용하고 &quot;&amp;&quot;로 구분된 매개 변수 값.

  예:

  이 예에서 p3에는 URL로 인코딩된 `hello world`라는 값이 있습니다.

다음 페이지 코드 예를 생각해 보십시오.

```html {line-numbers="true"}
<html> 
  <head> 
    <title>Title here..</title> 
    <script type="text/javascript"> 
        function targetPageParams() { 
          return "p1=v1&p2=v2&p3=hello%20world";
        } 
    </script> 
    <script src="mbox.js" type="text/javascript"></script> 
  </head> 
  <body>Body here... 
  </body> 
</html>
```

이 예는 mbox 가장자리에 다음 데이터를 보냅니다.

* p1=v1
* p2=v2
* p3=hello world

## 배열

```javascript {line-numbers="true"}
<!--window.-->targetPageParams = function() { 
  return ["a=1", "b=2", "c=hello world"]; 
}; 
```

값은 URL로 인코딩할 필요가 없습니다. 예를 들어, 값에 공백이 들어 있다면 공백을 인코딩할 필요가 없습니다.

이 예는 mbox 가장자리에 다음 데이터를 보냅니다.

* a=1
* b=2
* c=hello world

## JSON

JSON은 매개 변수를 전달하는 강력한 방법입니다. [!DNL Target] 는 JSON 개체 키를 사용하여 복잡한 구조를 간단한 매개 변수로 병합합니다.

```json {line-numbers="true"}
<!--window.-->targetPageParams = function() { 
  return { 
    "a": 1, 
    "b": 2, 
    "profile": { 
                  "memberStatus": Gold, 
                  "country": { 
                                "city": "San Francisco" 
                            } 
              } 
  }; 
}; 
```

값은 URL로 인코딩할 필요가 없습니다. 예를 들어 &quot;San Francisco&quot;를 사용할 때 공백을 인코딩할 필요가 없습니다. 공백으로 충분합니다.

이 예는 mbox 가장자리에 다음 데이터를 보냅니다.

* a=1
* b=2
* `profile.memberStatus`=Gold
* `profile.country.city`=San Francisco
