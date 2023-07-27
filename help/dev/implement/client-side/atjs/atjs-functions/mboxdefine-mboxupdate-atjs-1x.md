---
keywords: mboxDefine, mboxdefine, mboxDefine, mboxUpdate, mboxupdate, mbox 업데이트, at.js, 함수, 함수, mboxDefine0
description: 사용 [!UICONTROL mboxDefine()] 및 [!UICONTROL mboxUpdate()] 에 대한 함수 [!DNL Adobe Target] at.js JavaScript 라이브러리 를 사용하여 mbox를 정의하거나 업데이트합니다. (at.js 1.x)
title: 사용 방법 [!UICONTROL mboxDefine()] 및 [!UICONTROL mboxUpdate()] 기능?
feature: at.js
exl-id: 0a7dbea2-1cbd-4a5b-ba68-4c76a88d65c4
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 52%

---

# [!UICONTROL mboxDefine()] 및 [!UICONTROL mboxUpdate()] - at.js 1.x

에서 mbox 정의 및 업데이트 [!DNL Adobe Target].

>[!NOTE]
>
>이 함수들은 at.js 버전 1.*x*&#x200B;에만 사용할 수 있습니다. 이러한 함수는 at.js 2 릴리스에서 더 이상 사용되지 않습니다.*x*. 이러한 함수는 at.js 2와 함께 사용되는 경우 기본 콘텐츠를 반환합니다.*x*.

`[!UICONTROL mboxDefine()]` 및 `[!UICONTROL mboxCreate()]`은 오퍼가 표시되어야 하는 HTML DIV 요소에 연결되어 있습니다. 이러한 HTML DIV 요소에는 `mboxDefault` 클래스가 있어야 합니다. HTML 요소에 이 클래스가 첨부되어 있지 않으면 깜박임이 느껴질 수 있습니다.

## mboxDefine

nodeId와 mbox 이름 사이에 내부 매핑을 만들되, 요청을 실행하지 마십시오. `[!UICONTROL mboxUpdate()]`와 함께 사용됩니다. mbox.js(사용 중단됨)에서 at.js로 간편하게 전환하기 위해 at.js에 주로 내장되어 있습니다.

## mboxUpdate

요청을 실행하고 `nodeId`()의 `mboxDefine()`로 식별되는 요소에 오퍼를 적용합니다. `[!UICONTROL mboxCreate]`로 시작된 mbox를 업데이트하는 데도 사용할 수 있습니다. mbox.js(사용 중단됨)에서 at.js로 간편하게 전환하기 위해 at.js에 주로 내장되어 있습니다. `mboxDefine()`/ `mboxUpdate()`는 선택기 옵션을 사용하여 [adobe.target.getOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) 및 [adobe.target.applyOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md)로 대체할 수 있습니다.

## 예

```javascript {line-numbers="true"}
<div id="someId" class="mboxDefault"></div> 
<script> 
 mboxDefine('someId','mboxName','param1=value1','param2=value2'); 
 mboxUpdate('mboxName','param3=value3','param4=value4'); 
</script>
```
