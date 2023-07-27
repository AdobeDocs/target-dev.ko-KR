---
keywords: adobe.target.applyOffer, applyOffer, applyOffer, applyOffer, at.js, 함수, 함수, $8
description: 사용 [!UICONTROL adobe.target.applyOffer()] 함수 [!DNL Adobe Target] at.js JavaScript 라이브러리를 사용하여 응답 콘텐츠를 적용할 수 있습니다.
title: 사용 방법 [!UICONTROL adobe.target.applyOffer()] 기능?
feature: at.js
exl-id: 957bbe92-8012-4bd5-95d6-1ae38b72bb16
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 69%

---

# [!UICONTROL adobe.target.applyOffer(옵션)]

이 함수는 의 응답 콘텐츠를 적용하는 데 사용됩니다. [!DNL Adobe Target].

>[!NOTE]
>
>`applyOffer`를 사용하려면 `mbox` 매개 변수가 필요합니다. mbox 이름이 지정되지 않은 경우 오류가 발생합니다.

옵션 매개 변수는 필수이며 다음 구조를 갖습니다.

| 키 | 유형 | 필수 | 설명 |
|--- |--- |--- |--- |
| mbox | 문자열 | 예 | Mbox 이름<br />at.js 1.3.0(및 이후 버전)을 사용하면 Target에서 mbox 키를 사용하도록 강제 적용합니다. 이 키는 과거에는 필요했지만 현재 Target에서는 이 키를 적용하여 적절한 유효성 검사가 수행되는지와 고객이 함수를 올바르게 사용하고 있는지를 확인합니다. |
| selector | 문자열 또는 DOM 요소 | 아니오 | Target이 오퍼 컨텐츠를 배치해야 하는 HTML 요소를 식별하는 데 사용되는 HTML 요소 또는 CSS 선택기입니다. 선택기를 제공하지 않으면 Target은 HTML 요소가 HTML HEAD을 사용해야 한다고 가정합니다. |
| 오퍼 | 배열 | 예 | 요소에 적용되어야 하는 배열 작업입니다. |

## 예

다음 예제는 `[!UICONTROL getOffer]` 및 `[!UICONTROL applyOffer]`를 함께 사용하는 방법을 보여 줍니다.

```javascript {line-numbers="true"}
adobe.target.getOffer({   
  "mbox": "mbox",   
  "success": function(offers) {           
        adobe.target.applyOffer( {  
           "mbox": "mbox", 
           "offer": offers  
        } ); 
  },   
  "error": function(status, error) {           
      if (console && console.log) { 
        console.log(status); 
        console.log(error); 
      } 
  }, 
 "timeout": 5000 
}); 
```
