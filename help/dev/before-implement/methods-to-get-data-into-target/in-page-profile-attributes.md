---
keywords: 구현, 구현, 설정, 설정, 페이지 매개 변수
description: 페이지 내 프로필 특성을 사용하여  [!DNL Target] 에 데이터를 가져옵니다.
title: 페이지 내 프로필 특성을 사용하여  [!DNL Target] 로 데이터를 가져오려면 어떻게 해야 합니까?
feature: Implementation
exl-id: c19fd746-21a2-4eb5-8c2a-c24806e09324
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 43%

---

# 페이지 내 프로필 속성

[!DNL Adobe Target]의 페이지 내 프로필 특성(&quot;mbox 내 프로필 특성&quot;이라고도 함)은 나중에 사용하기 위해 방문자 프로필에 저장된 페이지 코드를 통해 직접 전달되는 이름/값 쌍입니다.

인페이지 프로필 속성을 사용하면 나중에 타깃팅 및 세그멘테이션을 수행할 수 있도록 사용자별 데이터를 Target의 프로필에 저장할 수 있습니다.

## 형식

페이지 내 프로필 특성은 서버 호출을 통해 접두사가 &quot;profile&quot;인 문자열 이름/값 쌍으로 [!DNL Target]에 전달됩니다. Target에 전달됩니다.

속성 이름과 값은 사용자 지정할 수 있습니다(특정 용도로 &quot;예약된 이름&quot;도 있음).

다음은 인페이지 프로필 속성에 대한 몇 가지 예입니다.

* `profile.membershipLevel=silver`
* `profile.visitCount=3`

## 예시 사용 사례

* **로그인 정보**: 사용자의 로그인을 기준으로 비PII(개인 식별 정보) 데이터를 [!DNL Target]에 공유합니다. 이 데이터는 멤버십 상태, 주문 내역 등이 될 수 있습니다.
* **스토어 정보**: 이 사용자의 기본 설정 위치가 되는 스토어를 추적합니다.
* **이전 상호 작용**: 향후 개인화할 때 알려주기 위해 이전에 사이트에서 수행한 작업을 추적합니다.

## 메서드의 이점

데이터는 실시간으로 [!DNL Target] (으)로 전송되며 데이터가 들어오는 것과 동일한 서버 호출에서 사용할 수 있습니다.

## 주의 사항

페이지 코드 업데이트가 필요합니다(직접 또는 태그 관리 시스템 사용).

속성 및 값은 서버 호출에 표시되므로 방문자가 값을 볼 수 있습니다. 신용 범위 또는 기타 잠재적으로 개인 정보와 같은 정보를 공유하는 경우, 이 방법은 최선의 방법이 아닐 수 있습니다.

## 코드 예

targetPageParamsAll(속성을 페이지의 모든 mbox 호출에 추가합니다.):

`function targetPageParamsAll() { return "profile.param1=value1&profile.param2=value2&profile.p3=hello%20world"; }`

targetPageParams(속성을 페이지의 글로벌 mbox에 추가합니다.):

`function targetPageParams() { return profile.param1=value1&profile.param2=value2&profile.p3=hello%20world"; }`

mboxCreate 코드에 있는 속성:

`<div class="mboxDefault"> default content to replace by offer </div> <script> mboxCreate('mboxName','profile.param1=value1','profile.param2=value2'); </script>`

## 관련 정보 링크

[프로필 속성](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html)

[방문자 프로필](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html)
