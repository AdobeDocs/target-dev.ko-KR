---
keywords: 글로벌 mbox, 글로벌 mbox 사용자 지정, at.js 편집, at.js, at.js 구현
description: 에서 at.js에 대한 글로벌 mbox를 사용자 지정하는 방법을 알아봅니다. [!UICONTROL 관리]-[!UICONTROL 구현] 페이지 위치 [!DNL Adobe Target].
title: 글로벌 mbox를 사용자 지정하는 방법
feature: at.js
exl-id: f7809c3d-6e77-4bbe-8da3-4ab0a448c801
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 17%

---

# 글로벌 mbox 사용자 지정

을(를) 사용자 지정하는 데 도움이 되는 정보 [!DNL Adobe Target] at.js에 대한 글로벌 mbox.

1. **[!UICONTROL 관리]** > **[!UICONTROL 구현]**&#x200B;을 클릭합니다.

1. 사용 안 함 **[!UICONTROL 페이지 로드가 활성화됨(글로벌 mbox를 자동으로 만들기)]**&#x200B;을(를) 만든 다음 활동을 전달하는 데 사용할 사용자 지정 글로벌 mbox의 이름을 추가합니다 [!DNL Target].

>[!WARNING]
>
>다른 글로벌 mbox를 선택하면 변경 사항이 자동으로 저장됩니다.

이 사용자 지정 mbox도 클릭 추적에 사용됩니다.

![custom-global-mbox](../../assets/custom-global-mbox.png)

1. 사이트에서 at.js 라이브러리를 구현합니다.

   다음을 참조하십시오 [at.js를 배포하는 방법](/help/dev/implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md) 추가 정보.

1. 전환 시간을 릴리스에 맞춰 지정합니다.

   다음에 대한 준비가 되면 [!DNL Target] 향후 모든 활동에 글로벌 mbox를 사용하기 위해 이 단계를 진행할 수 있습니다.

   위의 2단계에서 사용되는 이름과 일치하도록 사용자 지정 글로벌 mbox의 이름을 업데이트합니다.


>[!WARNING]
>
>계정의 모든 활동이 이 mbox와 동기화됩니다. 활동이 계속 작동할 수 있도록 글로벌 mbox가 사이트에 있는지 확인하십시오. 로 만든 영향을 받는 활동을 편집하고 다시 저장해야 합니다. [!UICONTROL 시각적 경험 작성기] (VEC) 이 mbox와 동기화됩니다. 에서 만든 활동을 다시 저장할 필요는 없습니다. [!UICONTROL 양식 기반 경험 작성기] 또는 API를 통해 게시할 수 있습니다.
