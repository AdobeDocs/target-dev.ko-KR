---
keywords: target 개발자 안내서, 개요
title: Adobe Target 개발자 안내서
description: ' [!DNL Adobe Target] 을 구현 및 관리하고 해당 API 및 SDK로 작업하려면 어떻게 해야 합니까?'
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 655cff9b-fc04-45cf-9068-5c6c32b70d79
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 12%

---

# [!DNL Adobe Target] 개발자 안내서

![Adobe Target 배너 이미지](/help/dev/assets/target-home-banner-simple.png)

**([보기 [!DNL Target] 설명서 업데이트 정보](https://experienceleague.adobe.com/docs/target/using/release-notes/doc-change.html){target=_blank})**

이 *[!DNL Adobe Target]개발자 안내서* 는 을 위한 리소스 및 안내서를 제공합니다. [!DNL Target] 구현 및 관리를 위한 API 및 SDK 설명서를 포함한 개발자 [!DNL Target].

>[!NOTE]
>
>이 안내서 외에 다음과 같은 [!DNL Adobe Target] 안내서도 이용할 수 있습니다.
>
>* [*[!DNL Adobe Target] 비즈니스 실무자 안내서&#x200B;*](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=ko_KR){target=_blank}
>
>* [*[!DNL Adobe Target] Tutorials *](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=ko-KR){target=_blank}
>
>릴리스 정보는 [Target 릴리스 노트(현재)](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html){target=_blank} 다음에서 *[!DNL Adobe Target]비즈니스 실무자 안내서*.

## 구현 시작하기

**[구현하기 전에](/help/dev/before-implement/considerations-before-you-implement-target.md)**: 구현하기 전에 고려해야 할 사항 [!DNL Adobe Target].

## 클라이언트측 구현

[**Adobe Experience Platform 웹 SDK**](/help/dev/implement/client-side/aep-web-sdk.md): [!DNL Adobe Experience Platform Web SDK] 에서 다양한 서비스와 상호 작용할 수 있습니다. [!DNL Experience Cloud] (포함) [!DNL Target])을 통해 [!UICONTROL Adobe Experience Edge Network].

[**Target at.js JavaScript 라이브러리**](/help/dev/implement/client-side/overview.md): at.js JavaScript 라이브러리는 웹 구현에 대한 페이지 로드 시간을 향상시키고, 보안을 강화하고, 단일 페이지 애플리케이션에 대해 더 나은 구현 옵션을 제공합니다.

## 서버측 구현

[**Target SDK 개요**](implement/server-side/server-side-overview.md): 시작하기 [!DNL Adobe Target] 온디바이스 의사 결정을 포함한 SDK.

[**Node.js SDK**](implement/server-side/node-js/overview.md): 사용 방법 [!DNL Target] Node.js SDK.

[**Java SDK**](implement/server-side/java/overview.md): 사용 방법 [!DNL Target] Java SDK.

[**.NET SDK**](implement/server-side/net/overview.md): 사용 방법 [!DNL Target] .NET SDK.

[**Python SDK**](implement/server-side/python/overview.md): 사용 방법 [!DNL Target] Python SDK.

## 하이브리드 구현

[**하이브리드 배포**](implement/hybrid/hybrid-overview.md): 구현 [!DNL Target] 클라이언트측과 서버측 구현의 조합 사용.

## Recommendations 구현

[**Recommendations 구현**](implement/recommendations/recommendations.md): 계획 및 구현 [!DNL Adobe Target Recommendations].

## 모바일 앱 구현

[**AEP Mobile SDK 개요**](implement/mobile/overview.md): 구현 방법 개요 [!DNL Adobe Target] 포함 [!DNL Adobe Experience Platform] 모바일 SDK.

[**AEP Mobile SDK 참조**](https://developer.adobe.com/client-sdks/documentation/): 구현 [!DNL Adobe Target] 포함 [!DNL Adobe Experience Platform] 모바일 SDK.

## 이메일 구현

[**이메일 개요**](implement/email/overview.md): 구현 방법 개요 [!DNL Adobe Target] 이메일.

## API 안내서

[**소개**](before-administer/target-api-overview.md): 개요 [!DNL Adobe Target] API.

[**[!DNL Target Delivery API]**](/help/dev/implement/delivery-api/overview.md): 사용 [!DNL Adobe Target] 웹 및 모바일 채널뿐만 아니라 연결된 TV, 키오스크 또는 매장 내 디지털 화면과 같은 비브라우저 기반 IoT 디바이스에서 경험을 게재하기 위한 게재 API입니다.

[**[!DNL Target Admin API]**](administer/admin-api/admin-api-overview-new.md): 사용 [!DNL Adobe Target] 속성, 활동, 대상, 오퍼, 속성, 보고서, mbox, 호스트, 환경 등을 관리하기 위한 관리 API입니다.

[**[!DNL Target Profile API]**](https://developers.adobetarget.com/api/#profiles): 검색 [!DNL Adobe Target] 사용자 프로필 정보.

[**[!DNL Target Reporting API]**](https://developer.adobe.com/target/administer/admin-api/#tag/Reports): 검색 [!UICONTROL A/B 테스트] 및 [!UICONTROL Automated Personalization] 활동 보고서 데이터입니다.

[**[!DNL Target Recommendations API]**](http://developers.adobetarget.com/api/recommendations/): 사용 [!DNL Target Recommendations] API.

[**[!DNL Target Models API]**](administer/models-api/models-api-overview.md): 차단 목록을 관리하여에 사용되는 기능 정의 [!DNL Target] 머신 러닝 모델.

[**ADMIN CONSOLE API**](https://developer.adobe.com/umapi/): 사용자 관리 Adobe 및 사용자 동기화 API를 통해 사용자 및 제품 권한을 관리합니다.

[**[!DNL Adobe Experience Platform Edge Network Server API]**](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html): 사용 [!DNL Adobe Experience Platform Edge Network Server] 다양한 데이터 수집, 개인화, 광고 및 마케팅 사용 사례를 위한 API입니다.

## 리소스

* [Adobe 오픈 소스 리포지토리](https://github.com/adobe)
* [Target 노드 JS SDK 소스](https://github.com/adobe/target-nodejs-sdk)
* [Target 노드 JS SDK 예 리포지토리](https://github.com/adobe/target-nodejs-sdk-samples)
* [Target Java SDK 소스](https://github.com/adobe/target-java-sdk)
* [Target Java SDK 예제 리포지토리](https://github.com/adobe/target-java-sdk-samples)
* [Target 구현](./before-implement/prepare-to-implement-target.md)
* [Target 관리](./before-administer/target-api-overview.md)
* [Adobe Target 개발 문서 GitHub 리포지토리](https://github.com/AdobeDocs/target-developers)
* [Adobe Target 릴리스 노트](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html)
* [Adobe Target 비즈니스 사용 안내서](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=ko_KR)
