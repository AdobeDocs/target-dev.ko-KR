---
keywords: at.js, 함수, javascript 라이브러리
description: ' [!DNL Adobe Target]의 at.js JavaScript 라이브러리의 1.x 및 2.x 버전과 함께 사용할 수 있는 함수 목록을 봅니다.'
title: at.js에서 사용할 수 있는 함수는 무엇입니까?
feature: at.js
exl-id: 1efed365-8a74-4c85-bdb1-8daaaf53d642
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 58%

---

# at.js 함수

[!DNL Adobe Target] at.js JavaScript 라이브러리와 함께 사용할 수 있는 함수 목록입니다. 자세한 내용 및 예를 보려면 함수 열의 링크를 클릭합니다.

| 함수 | 세부 사항 |
| --- | --- |
| [[!UICONTROL adobe.target.getOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) | 이 함수는 [!DNL Target] 오퍼를 가져오는 요청을 실행합니다. `adobe.target.applyOffer()`와 함께 사용하여 응답을 처리하거나 자체적인 성공 처리를 사용할 수 있습니다. |
| [[!UICONTROL adobe.target.getOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)<P>(at.js 2.x) | 이 함수를 사용하면 여러 mbox를 전달하여 여러 오퍼를 검색할 수 있습니다. 또한 활성 활동의 모든 보기에 대해 여러 오퍼를 검색할 수 있습니다.<P>**참고:** 이 함수는 at.js 2.x에서 도입되었습니다. 이 함수는 at.js 버전 1.*x*. |
| [[!UICONTROL adobe.target.applyOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md) | 이 함수는 응답 콘텐츠를 적용하는 데 사용됩니다. |
| [[!UICONTROL adobe.target.applyOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)<P>(at.js 2.x) | 이 함수를 사용하면 [!UICONTROL adobe.target.getOffers()]로 검색된 오퍼를 두 개 이상 적용할 수 있습니다.<P>**참고:** 이 함수는 at.js 2.x에서 도입되었습니다. 이 함수는 at.js 버전 1.*x*. |
| [[!UICONTROL adobe.target.triggerView (viewName, options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)<P>(at.js 2.x) | 이 함수는 새 페이지를 로드할 때마다 또는 페이지의 구성 요소가 다시 렌더링될 때 호출할 수 있습니다.<P> [!UICONTROL Visual Experience Composer]&#x200B;(VEC)을 사용하여 [!UICONTROL A/B Test] 및 [!UICONTROL Experience Targeting]&#x200B;(XT) 활동을 만들려면 SPA(단일 페이지 애플리케이션)에 대해 이 함수를 구현해야 합니다. |
| [[!UICONTROL adobe.target.trackEvent(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) | 이 함수는 클릭 및 전환과 같은 사용자 작업을 보고하라는 요청을 실행하며, 응답에 있는 활동을 전달하지는 않습니다. |
| [[!UICONTROL mboxCreate(mbox,params)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxcreate-atjs.md)<P>(at.js 1.x) | 요청을 실행하고 mboxDefault 클래스 이름을 사용하는 가장 가까운 DIV에 오퍼를 적용합니다.<P>**참고:** 이 함수는 at.js 버전 1.*x*&#x200B;에만 사용할 수 있습니다. 이 함수는 at.js 2.x의 릴리스에서 더 이상 사용되지 않으며, at.js 2.x에서 사용하는 경우 기본 콘텐츠를 반환합니다. |
| [[!UICONTROL mboxDefine(options)] 및 [!UICONTROL mboxUpdate(options)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxdefine-mboxupdate-atjs-1x.md)<P>(at.js 1.x) | mbox를 정의하고 업데이트합니다.<P>**참고:** 이 함수는 at.js 버전 1.*x*&#x200B;에만 사용할 수 있습니다. 이 함수는 at.js 2.x의 릴리스에서 더 이상 사용되지 않으며, at.js 2.x에서 사용하는 경우 기본 콘텐츠를 반환합니다. |
| [[!UICONTROL targetGlobalSettings(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) | `[!UICONTROL targetGlobalSettings()]` UI에서 또는 REST API를 사용하여 설정하는 대신 [!DNL Target Standard/Premium]을(를) 사용하여 at.js 라이브러리의 설정을 재정의할 수 있습니다.<ul><li>데이터 공급자: 이 설정을 사용하여 고객은 Demandbase, BlueKai 및 사용자 지정 서비스와 같은 타사 데이터 공급자로부터 데이터를 수집하고, 글로벌 mbox의 mbox 매개 변수가 요청할 때 Target으로 데이터를 전달할 수 있습니다.</li></ul> |
| [[!UICONTROL targetPageParams(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) | 이 방법을 사용하면 요청 코드의 외부에서 글로벌 mbox에 매개 변수를 첨부할 수 있습니다. |
| [[!UICONTROL targetPageParamsAll(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparamsall.md) | 이 방법을 사용하면 요청 코드의 외부에서 모든 mbox에 매개 변수를 첨부할 수 있습니다. |
| [[!UICONTROL registerExtension(options)]](/help/dev/implement/client-side/atjs/atjs-functions/registerextension-atjs-1x.md)<P>(at.js 1.x) | 특정 확장 기능을 등록하는 표준 방법을 제공합니다.<P>**참고:** 이 함수는 at.js 버전 1.*x*&#x200B;에만 사용할 수 있습니다. 이 함수는 at.js 2.x의 릴리스에서 더 이상 사용되지 않으며, at.js 2.x에서 사용하는 경우 기본 콘텐츠를 반환합니다. |
| [[!UICONTROL at.js custom events]](/help/dev/implement/client-side/atjs/atjs-functions/atjs-custom-events.md) | at.js 사용자 지정 이벤트는 mbox 요청 또는 오퍼가 실패하거나 성공하면 알려줍니다. |
| [[!UICONTROL adobe.target.sendNotifications(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)<P>(at.js 2.1.0) | 이 함수는 [!DNL Target] 또는 `[!UICONTROL adobe.target.applyOffer()]`을(를) 사용하지 않고 경험을 렌더링할 때 `[!UICONTROL adobe.target.applyOffers()]` Edge에 알림을 보냅니다.<P>**참고**: 이 함수는 at.js 2.1.0에서 처음 소개되었으며, 2.1.0 이상 버전에서 사용할 수 있습니다. |
