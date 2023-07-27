---
keywords: 글로벌 mbox, at.js 구현
description: 에서 글로벌 mbox에 대해 알아보기 [!DNL Adobe Target], a name used to refer to the single server call made at the top of each web page in your [!DNL Target] 구현.
title: 글로벌 mbox란?
feature: at.js
exl-id: 572c1dc6-5cdd-427a-9458-e5ec49990cf8
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 73%

---

# 글로벌 mbox 이해

[!DNL Adobe Target] 구현에서 각 웹 페이지의 맨 위에서 수행된 단일 서버 호출을 참조하는 데 사용되는 이름인 글로벌 mbox에 대한 정보입니다.

기본적으로 글로벌 mbox에는 `target-global-mbox`라는 이름이 지정됩니다. 필요한 경우 이 이름을 해당 계정용으로 바꿀 수 있습니다.

일반 mbox(비글로벌 mbox)와 글로벌 mbox 사이에는 다음과 같이 몇 가지 차이점이 있습니다.

| 일반 mbox | 글로벌 mbox |
|--- |--- |
| 일반 mbox는 일반적으로 컨텐츠를 `<DIV>` 태그로 둘러싸고 있습니다. | 글로벌 mbox는 &quot;비어 있는&quot; 상태이며 컨텐츠를 둘러싸지 않습니다. |
| 한 활동의 컨텐츠만 일반 mbox에서 전달할 수 있습니다. | 여러 활동의 컨텐츠를 글로벌 mbox에 대한 하나의 응답으로 전달할 수 있습니다. |

여러 활동이 글로벌 mbox를 통해 또는 여러 일반 mbox를 통해 전달되는 경우 Target [우선 순위 결정](https://experienceleague.adobe.com/docs/target/using/activities/priority.html) 활동(또는 활동)이 웹 페이지에 전달되는 기준이 됩니다.

추가적인 페이지 수준 데이터를 [!DNL Target] 함수를 사용하여 글로벌 mbox와 함께 `[!UICONTROL targetPageParams]`에 전송할 수 있습니다. 이것은 mbox 매개 변수 기능과 비슷합니다. 자세한 내용은 [글로벌 Mbox에 매개 변수 전달](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md)을 참조하십시오.
