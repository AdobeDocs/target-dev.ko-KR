---
title: Adobe Recommendations API란?
description: 이 안내서는 Adobe Target Recommendations API를 사용하여 Recommendations 카탈로그 및 사용자 지정 기준을 구성하고 관리할 뿐만 아니라 배달 API를 사용하여 권장 사항 콘텐츠를 검색하는 실습 방법을 개발자에게 안내합니다.
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 0d03c650-0b00-44b8-a794-10e5d738e42c
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 2%

---

# Adobe Recommendations API 개요

Recommendations과 관련된 API는 다음과 같습니다 [관리 API](../../before-administer/target-api-overview.md) 이를 통해 다음을 수행할 수 있습니다.

* 권장 제품 또는 콘텐츠의 카탈로그 관리
* Recommendations 알고리즘 및 활동 관리

Target 사용 [배달 API](../../implement/delivery-api/overview.md) Recommendations을 사용하면 다음 작업도 수행할 수 있습니다.

* 웹, 모바일, 이메일, 사물인터넷(IOT) 및 기타 채널에 표시할 수 있도록 JSON, HTML 또는 XML 객체로 권장 사항을 검색합니다.

## 설명

Recommendations API에 대한 이 안내서는 개발자가 Recommendations API를 사용하여 Recommendations 카탈로그 및 사용자 지정 기준을 구성하고 관리할 뿐만 아니라 배달 API를 사용하여 권장 사항 콘텐츠를 검색하는 실습 방법을 안내합니다. 이를 통해 다음과 같은 작업을 수행할 수 있습니다.

* Recommendations API를 사용하여 엔티티 구성 및 관리
* Recommendations API를 사용하여 사용자 지정 기준 구성 및 관리
* 배달 API와 함께 Recommendations을 사용하여 권장 사항을 사용하면 HTML이 아닌 장치가 발생하는 방법을 이해합니다

## 대상자

이 안내서는 API 또는 Recommendations API Target을 처음 사용하는 개발자를 위한 것입니다.

## 전제 조건 {#prerequisites}

Target 관리 API에는 다음이 필요합니다 [Adobe 인증 설정](../configure-authentication.md). Recommendations API를 사용하기 전에 이를 구성해야 합니다.

## 리소스

이 안내서를 이해하고 성공적으로 따르는 데 필요한 다음 리소스를 참고하십시오.

| 리소스 | 세부 사항 |
| --- | --- |
| Postman | 가져오기 [Postman 앱](https://www.postman.com/downloads/) 운영 체제용. Postman basic은 계정 생성이 무료입니다. 일반적으로 Adobe Target API를 사용하는 데 필요하지 않지만, Postman을 사용하면 API 워크플로를 보다 쉽게 수행할 수 있으며, Adobe Target에서는 API를 실행하고 작동 방법을 학습하는 데 도움이 되는 여러 Postman 컬렉션을 제공합니다. 이 안내서의 나머지 부분에서는 Postman에 대한 작업 지식을 전제로 합니다. 도움이 필요하면 를 참조하십시오. [Postman 설명서](https://learning.getpostman.com/). |
| 참조 | 이 안내서의 나머지 부분에서 다음 리소스에 익숙하다고 가정합니다.<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Target 관리 및 프로필 API 설명서](../../administer/admin-api/admin-api-overview-new.md)</li><li>[Recommendations API 설명서](https://developers.adobetarget.com/api/recommendations/)</li></UL> |
