---
title: Adobe Target 배달 API 고려 사항 및 알려진 제한 사항
description: 다음을 사용할 때 고려해야 할 고려 사항 및 알려진 제한 사항 [!UICONTROL Adobe Target 게재 API]?
keywords: 배달 api
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 7%

---

# 고려 사항 및 알려진 제한 사항

* 에 대한 인증이 없습니다. [!DNL Target] 게재 API.
* 이 API는 쿠키를 처리하거나 호출을 리디렉션하지 않습니다.
* 지원 대상 [!UICONTROL Automated Personalization] (AP) 및 [!UICONTROL Recommendations] 활동: 이 API에는 컨텐츠를 가져오는 두 가지 모드인 실행 모드와 미리 가져오기 모드가 있습니다. 프리페치 모드는 다음에만 사용할 수 있습니다. [!UICONTROL AB 테스트] 및 [!UICONTROL 경험 타기팅] (XT) 활동. 다음에 대해 프리페치 모드 사용 안 함 [!UICONTROL Automated Personalization] (AP), [!UICONTROL 자동 할당], [!UICONTROL 자동 Target], 또는 [!UICONTROL Recommendations] 활동 유형.
* HTTP/1.1과 HTTP/2 헤더 이름은 모두 대소문자를 구분하지 않지만, HTTP/2는 소문자 헤더 이름을 적용합니다. 자세한 내용은 [Hypertext Transfer Protocol 버전 2(HTTP/2) 설명서](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  새 로드 밸런서 인프라를 통해 방문자를 라우팅하는 엔드포인트를 사용하는 경우 해당 연결이 자동으로 HTTP/2로 업그레이드됩니다. 이 업그레이드 프로세스는 요청 헤더를 소문자 헤더로 전환하므로 잘못된 헤더로 간주되지 않습니다.

  이 문제는 라이브러리가 대/소문자를 구분하지 않는(특히 소문자가 아닌) 요청/응답 헤더를 찾도록 설정된 경우 고객에게 문제가 될 수 있습니다.