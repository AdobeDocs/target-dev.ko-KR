---
keywords: 구현, 구현, 설정, 설정, 페이지 매개 변수, tomcat, url 인코딩, 인페이지 프로필 속성, mbox 매개 변수, 인페이지 프로필 속성, 스크립트 프로필 속성, 벌크 프로필 업데이트 API, 단일 파일 업데이트 API, 고객 속성, 구현5, 구현6, 구현7, 구현8, 구현9, 구현0, 구현1, 구현2, 구현3, 구현4, 구현5, 데이터 공급자, dataprovider, 데이터 공급자
description: ' [!DNL Target] (페이지 매개 변수, 프로필 특성, 스크립트 프로필 특성, 데이터 공급자, 단일 및 벌크 프로필 업데이트 API, 고객 특성)에 데이터를 가져옵니다.'
title: 데이터를 Target으로 가져오려면 어떻게 해야 합니까?
feature: Implementation
exl-id: a54e306a-ea8e-4d3f-bc5d-b5895b6b9a84
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 34%

---

# 메서드 개요

데이터를 Adobe Target으로 가져오는 데 사용할 수 있는 다양한 방법에 대한 정보입니다.

사용 가능한 방법은 다음과 같습니다.

| 방법 | 세부 사항 |
| --- | --- |
| [페이지 매개 변수](page-parameters.md)<br />(&quot;mbox 매개 변수&quot;라고도 함) | 페이지 매개 변수는 나중에 사용할 수 있도록 방문자 프로필에 저장되지 않은 페이지 코드를 통해 직접 전달된 이름/값 쌍입니다.<br />페이지 매개 변수는 나중에 타깃팅할 때 방문자 프로필과 함께 저장할 필요가 없는 페이지 데이터를 [!DNL Target] (으)로 보내는 데 유용합니다. 대신 이 값은 페이지나, 특정 페이지에서 사용자가 취하는 행동을 설명하는 데 사용됩니다. |
| [페이지 내 프로필 특성](in-page-profile-attributes.md)<br />(&quot;mbox 내 프로필 특성&quot;이라고도 함) | 인페이지 프로필 속성은 나중에 사용할 수 있도록 방문자 프로필에 저장된 페이지 코드를 통해 직접 전달된 이름/값 쌍입니다.<br />페이지 내 프로필 속성을 사용하면 나중에 타기팅 및 세분화를 위해 사용자별 데이터를 Target의 프로필에 저장할 수 있습니다. |
| [스크립트 프로필 속성](script-profile-attributes.md) | 스크립트 프로필 특성은 [!DNL Target] 솔루션에 정의된 이름/값 쌍입니다. 서버 호출에 대해 Target 서버에서 JavaScript 코드 조각을 실행하여 값을 결정합니다.<br />사용자는 mbox 호출당, 방문자가 대상 및 활동 멤버십에 대해 평가되기 전에 실행되는 작은 코드 조각을 작성합니다. |
| [데이터 공급자](data-providers.md) | 데이터 공급자를 사용하면 타사의 데이터를 Target에 쉽게 전달할 수 있습니다. |
| [벌크 프로필 업데이트 API](bulk-profile-update-api.md) | API를 통해 많은 방문자에 대한 방문자 프로필 업데이트와 함께 .csv 파일을 [!DNL Target] (으)로 보냅니다. 각 방문자 프로필은 하나의 호출에서 여러 개의 인페이지 프로필 속성으로 업데이트할 수 있습니다. |
| [싱글 프로필 업데이트 API](single-profile-update-api.md) | 벌크 프로필 업데이트 API와 거의 동일하지만, 한 방문자 프로필이 .csv 파일 대신 API 호출에서 한 번에 하나씩 업데이트됩니다. |
| [고객 속성](customer-attributes.md) | 고객 속성을 사용하면 FTP를 통해 방문자 프로필 데이터를 Experience Cloud에 업로드할 수 있습니다. 업로드한 후에는 Adobe Analytics 및 Adobe Target의 데이터를 사용합니다. |
