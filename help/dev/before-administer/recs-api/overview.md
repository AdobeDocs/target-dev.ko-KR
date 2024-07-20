---
title: Adobe Recommendations API란?
description: 이 안내서는 Adobe Target Recommendations API를 사용하여 Recommendations 카탈로그 및 사용자 지정 기준을 구성하고 관리할 뿐만 아니라 배달 API를 사용하여 권장 사항 콘텐츠를 검색하는 실습 방법을 개발자에게 안내합니다.
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 0d03c650-0b00-44b8-a794-10e5d738e42c
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# Adobe Recommendations API 개요

Recommendations과 관련된 API에는 다음을 수행할 수 있는 [관리 API](../../before-administer/target-api-overview.md)가 포함됩니다.

* 권장 제품 또는 콘텐츠의 카탈로그 관리
* Recommendations 알고리즘 및 활동 관리

Recommendations과 함께 Target [배달 API](../../implement/delivery-api/overview.md)를 사용하면 다음 작업도 수행할 수 있습니다.

* 웹, 모바일, 이메일, 사물인터넷(IOT) 및 기타 채널에 표시할 수 있도록 JSON, HTML 또는 XML 객체로 권장 사항을 검색합니다.

## 설명

Recommendations API에 대한 이 안내서는 개발자가 Recommendations API를 사용하여 Recommendations 카탈로그 및 사용자 지정 기준을 구성하고 관리할 뿐만 아니라 배달 API를 사용하여 권장 사항 콘텐츠를 검색하는 실습 방법을 안내합니다. 이를 통해 다음과 같은 작업을 수행할 수 있습니다.

* Recommendations API를 사용하여 엔티티 구성 및 관리
* Recommendations API를 사용하여 사용자 지정 기준 구성 및 관리
* 배달 API와 함께 Recommendations을 사용하여 권장 사항을 사용하면 HTML이 아닌 장치가 발생하는 방법을 이해합니다

## 대상자

이 안내서는 Target API 또는 Recommendations API를 처음 사용하는 개발자를 위한 것입니다.

## 전제 조건 {#prerequisites}

Target 관리 API를 사용하려면 [Adobe 인증 설정](../configure-authentication.md)이 필요합니다. Recommendations API를 사용하기 전에 이를 구성해야 합니다.

## 리소스

이 안내서를 이해하고 성공적으로 따르는 데 필요한 다음 리소스를 참고하십시오.

| 리소스 | 세부 사항 |
| --- | --- |
| Postman | 운영 체제용 [Postman 앱](https://www.postman.com/downloads/)을 가져옵니다. Postman basic은 계정 생성이 무료입니다. 일반적으로 Adobe Target API를 사용하는 데 필요하지 않지만, Postman을 사용하면 API 워크플로를 보다 쉽게 수행할 수 있으며, Adobe Target에서는 API를 실행하고 작동 방법을 학습하는 데 도움이 되는 여러 Postman 컬렉션을 제공합니다. 이 안내서의 나머지 부분에서는 Postman에 대한 작업 지식을 전제로 합니다. 도움이 필요하면 [Postman 설명서](https://learning.getpostman.com/)를 참조하십시오. |
| 참조 | 이 안내서의 나머지 부분에서 다음 리소스에 익숙하다고 가정합니다.<UL><li>[Github Adobe I/O](https://github.com/adobeio)</li><li>[Target 관리자 및 프로필 API 설명서](../../administer/admin-api/admin-api-overview-new.md)</li><li>[Recommendations API 설명서](https://developer.adobe.com/target/administer/recommendations-api/)</li></UL> |
