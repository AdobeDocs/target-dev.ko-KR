---
keywords: 클라우드 인스턴스, 공용 접미사 목록, 공용 접미사, 쿠키, 퍼스트 파티 쿠키, 퍼스트 파티 쿠키, azurewebsites.net, cloudapp.net, amazonaws.com, cloudfront.net, herokuapp.com, firebaseapp.com, targetGlobalSettings, cookieDomain, cloud instances5, cloud instances6, cloud instances7, cloud instances8, cloud instances9, 공용 접미사 list0, 공용 접미사 list1, 공용 접미사 list2, 공용 접미사 list3, 공용 접미사 list4, 공용 접미사 list5
description: 클라우드 기반 인스턴스를 사용하여  [!DNL Adobe Target] 을(를) 테스트하거나 개념 입증 목적으로 고객이 직면한 문제를 살펴봅니다(솔루션 사용).
title: 클라우드 기반 인스턴스와 함께  [!DNL Target] 을(를) 사용할 수 있습니까?
feature: at.js
exl-id: 4b24fdc0-6c74-4b29-bbf9-7a761d4564a2
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 38%

---

# [!DNL Target]에 클라우드 기반 인스턴스 사용

클라우드 기반 인스턴스를 사용하여 [!DNL Adobe Target]을 테스트할 때 고객이 직면하는 문제에 대한 정보입니다.

[!DNL Target] 고객은 테스트나 간단한 개념 입증 용도로 [!DNL Target]에 클라우드 기반 인스턴스를 사용하는 경우가 있습니다. 이러한 인스턴스에는 다음과 같은 도메인들이 포함될 수 있습니다.

`azurewebsites.net`, `cloudapp.net`, `amazonaws.com`, `cloudfront.net`, `herokuapp.com` 또는 `firebaseapp.com`

이러한 도메인 및 기타 많은 다른 도메인이 [공용 접미사 목록](https://publicsuffix.org/list/public_suffix_list.dat)에 나와 있습니다.

**문제:** 최신 브라우저에서는 이러한 도메인을 사용하는 경우 쿠키를 저장하지 않습니다.

at.js JavaScript 라이브러리는 쿠키를 사용하여 사용자를 추적하여 [!DNL [!DNL Target]]이(가) 항상 일관된 경험을 제공하도록 합니다. [!DNL Target] JavaScript 라이브러리에서 쿠키를 저장할 수 없으면 Target 요청이 비활성화됩니다.

**해결 방법:**&#x200B;공용 접미어 목록에 포함된 도메인에 클라우드 기반 인스턴스를 사용하려는 경우 `cookieDomain` 설정을 사용자 지정하는 것이 좋습니다. 자세한 내용은 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)를 참조하십시오.
