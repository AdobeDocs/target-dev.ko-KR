---
keywords: adobe.target.applyOffer, applyOffer, applyOffer, applyOffer, at.js, 함수, 함수, $8
description: ' [!DNL Adobe Target] at.js JavaScript 라이브러리에 대해 [!UICONTROL adobe.target.applyOffer()] 함수를 사용하여 응답 콘텐츠를 적용하십시오.'
title: '[!UICONTROL adobe.target.applyOffer()] 함수를 사용하는 방법은 무엇입니까?'
feature: at.js
exl-id: 957bbe92-8012-4bd5-95d6-1ae38b72bb16
TQID: https://experienceleague.adobe.com/lrjsIl-gKu1SnrZapxYcoDObvUCGG2ht58QtWbQkYts
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d851e2344279caeae25e4823ca86b9c17efd63
workflow-type: tm+mt
source-wordcount: 173
ht-degree: 68%

---

# [!UICONTROL adobe.target.applyOffer(옵션)]

이 함수는 [!DNL Adobe Target]에 응답 콘텐츠를 적용하는 데 사용됩니다.

>[!NOTE]
>
>`applyOffer`를 사용하려면 `mbox` 매개 변수가 필요합니다. mbox 이름이 지정되지 않은 경우 오류가 발생합니다.

옵션 매개 변수는 필수이며 다음 구조를 갖습니다.

| 키 | 유형 | 필수 | 설명 |
|--- |--- |--- |--- |
| mbox | 문자열 | 예 | Mbox 이름<br />at.js 1.3.0(및 이후 버전)을 사용하면 Target에서 mbox 키를 사용하도록 강제 적용합니다. 이 키는 과거에는 필요했지만 현재 Target에서는 이 키를 적용하여 적절한 유효성 검사가 수행되는지와 고객이 함수를 올바르게 사용하고 있는지를 확인합니다. |
| selector | 문자열 또는 DOM 요소 | 아니오 | Target이 오퍼 컨텐츠를 배치해야 하는 HTML 요소를 식별하는 데 사용되는 HTML 요소 또는 CSS 선택기입니다. 선택기를 제공하지 않으면 Target에서는 HTML 요소가 HTML HEAD를 사용해야 한다고 가정합니다. |
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


