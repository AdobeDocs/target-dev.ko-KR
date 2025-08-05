---
keywords: target 개발자 안내서, 개요;홈
title: Adobe Target 개발자 안내서
description: ' [!DNL Adobe Target] 을(를) 구현하고 관리하며 해당 API 및 SDK를 사용하여 작업하려면 어떻게 해야 합니까?'
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 655cff9b-fc04-45cf-9068-5c6c32b70d79
source-git-commit: 599aa4c965e331bb2681523d50708a03fc933875
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 6%

---

# [!DNL Adobe Target] 개발자 안내서

**([설명서 업데이트 [!DNL Target] 보기](https://experienceleague.adobe.com/docs/target/using/release-notes/doc-change.html?lang=ko){target=_blank})**

이 *[!DNL Adobe Target]개발자 안내서*&#x200B;은(는) [!DNL Target]을(를) 구현하고 관리하기 위한 API 및 SDK 설명서를 포함하여 [!DNL Target] 개발자를 위한 리소스 및 안내서를 제공합니다.

>[!NOTE]
>
>이 안내서 외에 다음과 같은 [!DNL Adobe Target] 안내서도 이용할 수 있습니다.
>
>* [*[!DNL Adobe Target] 비즈니스 실무자 안내서&#x200B;*](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=ko_KR){target=_blank}
>
>* [*[!DNL Adobe Target] 튜토리얼&#x200B;*](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=ko-KR){target=_blank}
>
>릴리스 정보는 [ 비즈니스 실무자 안내서](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html?lang=ko){target=_blank}의 *[!DNL Adobe Target]Target 릴리스 정보(현재)*&#x200B;를 참조하십시오.

## 구현 시작하기

**[구현하기 전에](/help/dev/before-implement/considerations-before-you-implement-target.md)**: [!DNL Adobe Target]을(를) 구현하기 전에 고려해야 할 사항입니다.

## 클라이언트측 구현

[**Adobe Experience Platform Web SDK**](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md): [!DNL Adobe Experience Platform Web SDK]을(를) 사용하면 [!DNL Experience Cloud]을(를) 통해 [!DNL Target]&#x200B;([!UICONTROL Adobe Experience Edge Network] 포함)의 다양한 서비스와 상호 작용할 수 있습니다.

[**Target at.js JavaScript 라이브러리**](/help/dev/implement/client-side/overview.md): at.js JavaScript 라이브러리는 웹 구현에 대한 페이지 로드 시간을 향상시키고, 보안을 강화하고, 단일 페이지 애플리케이션에 대해 더 나은 구현 옵션을 제공합니다.

## 서버측 구현

[**Target SDK 개요**](implement/server-side/server-side-overview.md): 온디바이스 의사 결정을 포함하여 [!DNL Adobe Target]개의 SDK를 시작합니다.

[**Node.js SDK**](implement/server-side/node-js/overview.md): [!DNL Target] Node.js SDK 사용 방법.

[**Java SDK**](implement/server-side/java/overview.md): [!DNL Target] Java SDK 사용 방법.

[**.NET SDK**](implement/server-side/net/overview.md): [!DNL Target] .NET SDK 사용 방법

[**Python SDK**](implement/server-side/python/overview.md): [!DNL Target] Python SDK 사용 방법.

## 하이브리드 구현

[**하이브리드 배포**](implement/hybrid/hybrid-overview.md): 클라이언트측과 서버측 구현의 조합을 사용하여 [!DNL Target]을(를) 구현합니다.

## 권장 사항 구현

[**권장 사항 구현**](implement/recommendations/recommendations.md): [!DNL Adobe Target Recommendations]을(를) 계획하고 구현합니다.

## 모바일 앱 구현

[**AEP Mobile SDK 개요**](implement/mobile/overview.md): [!DNL Adobe Target]개의 Mobile SDK를 사용하여 [!DNL Adobe Experience Platform]을(를) 구현하는 방법에 대한 개요입니다.

[**AEP Mobile SDK 참조**](https://developer.adobe.com/client-sdks/documentation/): [!DNL Adobe Target]개의 Mobile SDK를 사용하여 [!DNL Adobe Experience Platform]을(를) 구현합니다.

## 이메일 구현

[**전자 메일 개요**](implement/email/overview.md): 전자 메일에 [!DNL Adobe Target]을(를) 구현하는 방법에 대한 개요입니다.

## API 안내서

[**소개**](before-administer/target-api-overview.md): [!DNL Adobe Target] API 개요.

[**[!DNL Target Delivery API]**](/help/dev/implement/delivery-api/overview.md): [!DNL Adobe Target] 배달 API를 사용하여 연결된 TV, 키오스크 또는 매장 내 디지털 화면과 같은 비브라우저 기반 IoT 장치뿐만 아니라 웹 및 모바일 채널에서 경험을 전달할 수 있습니다.

[**[!DNL Target Admin API]**](administer/admin-api/admin-api-overview-new.md): [!DNL Adobe Target] 관리 API를 사용하여 속성, 활동, 대상, 오퍼, 속성, 보고서, mbox, 호스트, 환경 등을 관리합니다.

[**[!DNL Target Profile API]**](/help/dev/administer/profile-api/profiles-api.md): [!DNL Adobe Target] 사용자 프로필 정보를 검색합니다.

[**[!DNL Target Reporting API]**](https://developer.adobe.com/target/administer/admin-api/#tag/Reports): [!UICONTROL A/B Test] 및 [!UICONTROL Automated Personalization] 활동 보고서 데이터를 검색합니다.

[**[!DNL Target Recommendations API]**](https://developer.adobe.com/target/administer/recommendations-api/): [!DNL Target Recommendations] API를 사용합니다.

[**[!DNL Target Models API]**](administer/models-api/models-api-overview.md): [!DNL Target] 기계 학습 모델에 사용되는 기능을 정의할 차단 목록을 관리합니다.

[**Admin Console API**](https://developer.adobe.com/umapi/): Adobe User Management 및 User Sync API를 통해 사용자 및 제품 권한을 관리합니다.

[**[!DNL Adobe Experience Platform Edge Network Server API]**](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=ko): 다양한 데이터 수집, 개인화, 광고 및 마케팅 사용 사례에 [!DNL Adobe Experience Platform Edge Network Server] API를 사용하십시오.

## 리소스

* [Adobe 오픈 소스 리포지토리](https://github.com/adobe)
* [Target 노드 JS SDK Source](https://github.com/adobe/target-nodejs-sdk)
* [Target 노드 JS SDK 예제 리포지토리](https://github.com/adobe/target-nodejs-sdk-samples)
* [Target Java SDK Source](https://github.com/adobe/target-java-sdk)
* [Target Java SDK 예제 저장소](https://github.com/adobe/target-java-sdk-samples)
* [Target 구현](./before-implement/prepare-to-implement-target.md)
* [대상 관리](./before-administer/target-api-overview.md)
* [Adobe Target 개발 문서 GitHub 리포지토리](https://github.com/AdobeDocs/target-developers)
* [Adobe Target 릴리스 노트](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html?lang=ko)
* [Adobe Target 비즈니스 사용 안내서](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=ko_KR)

