---
keywords: 글로벌 mbox, target classic, target classic의 글로벌 mbox 사용
description: 이전 구현을 위해 페이지에서 이미 글로벌 mbox를 만든 경우  [!DNL Adobe Target] 활동을 위해 이전 글로벌 mbox를 사용하는 방법에 대해 알아봅니다.
title: 이전 구현에서 글로벌 mbox를 사용할 수 있습니까?
feature: at.js
exl-id: fe608b5e-ff66-4ba2-a622-d4f7307a9ca9
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 20%

---

# 이전 구현에서 글로벌 mbox를 사용

기본적으로 [!DNL Target]은(는) [!DNL Target]에서 만든 활동을 실행하는 데 사용되는 target-global-mbox라는 글로벌 mbox를 만듭니다. 그러나 이전 구현에 대한 페이지에서 이미 글로벌 mbox를 만든 경우 [!DNL Target] 활동에 해당 mbox를 사용할 수 있습니다.

>[!NOTE]
>
>mbox 요청은 계정당 하나만 보유할 수 있습니다.

[!DNL Target]와 레거시 구현 둘 다에 기존 글로벌 mbox를 사용하려면, 몇 개의 매개 변수를 설정해야 합니다.

1. [!DNL Target](으)로 이동한 다음 **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**&#x200B;을(를) 클릭합니다.

   기본적으로 **[!UICONTROL Page load enabled (Auto-create global mbox]**&#x200B;이(가) 활성화되어 있고 사용자 지정 글로벌 mbox의 이름은 `target-global-mbox`입니다.

1. 기존 mbox를 사용하려면 **[!UICONTROL Page load enabled (Auto-create global mbox]**&#x200B;을(를) 사용하지 않도록 설정하고 **[!UICONTROL Global Mbox]** 필드에 이전에 만든 글로벌 mbox의 이름을 지정하십시오.

   글로벌 Mbox 드롭다운에 계정의 모든 mbox가 나열됩니다. 아직 존재하지 않는 mbox를 사용하려면, mbox를 만듭니다.

1. **[!UICONTROL Save]** 아이콘을 클릭합니다.

   계정 설정이 업데이트됩니다.

1. 새 at.js 파일을 다운로드하고 사이트에서 참조합니다.

   모든 기존 활동은 이전에 만들어서 구현한 활동을 포함하여, 지정된 글로벌 mbox를 사용하도록 업데이트됩니다.

## 글로벌 mbox 구현 문제 해결

다음 FAQ를 사용하여 글로벌 mbox 구현 문제를 해결할 수 있습니다.

### 글로벌 mbox가 로드되지 않거나 페이지 로드 시 글로벌 mbox 로드가 느려지는 이유는 무엇입니까?

at.js 참조가 페이지에서 첫 번째 JavaScript 호출인지 확인합니다. 이 문제에 대한 다른 해결 방법은 [글로벌 mbox 자주 묻는 질문](/help/dev/implement/client-side/atjs/global-mbox/global-mbox-faq.md)을 참조하세요.
