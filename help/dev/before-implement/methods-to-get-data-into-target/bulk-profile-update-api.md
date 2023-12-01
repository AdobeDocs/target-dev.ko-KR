---
keywords: 구현, 구현, 설정, 설정, 벌크 프로필 업데이트 api
description: 데이터 가져오기 [!DNL Target] 사용 [!UICONTROL 벌크 프로필 업데이트 API].
title: 데이터를으로 가져오는 방법 [!DNL Target] 사용 [!UICONTROL 벌크 프로필 업데이트 API]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: 43f4fb8345a77ccb0e112fe196e7e0944cc468c9
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 4%

---

# 벌크 프로필 업데이트 API

다음 [!DNL Adobe Target] [!UICONTROL 벌크 프로필 업데이트 API] 배치 파일을 사용하여 웹 사이트에 대한 여러 방문자의 사용자 프로필을 일괄적으로 업데이트할 수 있습니다.

사용 [!UICONTROL 벌크 프로필 업데이트 API], 많은 사용자에 대해 프로필 매개 변수 형식으로 자세한 방문자 프로필 데이터를 편리하게 보낼 수 있습니다. [!DNL Target] 모든 외부 소스에서 외부 소스에는 일반적으로 웹 페이지에서 사용할 수 없는 CRM(고객 관계 관리) 또는 POS(판매 지점) 시스템이 포함될 수 있습니다.

## [!UICONTROL 고객 속성] 및 [!UICONTROL 벌크 프로필 업데이트 API]

이 옵션은 과 유사합니다. [!UICONTROL 고객 속성] 몇 가지 차이점이 있습니다.

* [!UICONTROL 고객 속성] ftp 업로드를 사용합니다. 다음 [!UICONTROL Target 벌크 프로필 업데이트 API] 는 HTTP POST API를 사용합니다.
* [!UICONTROL 고객 속성] 데이터 공유 대상: [!DNL Analytics]. 다음 [!UICONTROL 벌크 프로필 업데이트] 다음에서만 사용할 수 있습니다. [!DNL Target].
* [!UICONTROL 고객 속성] 사용자를 위한 프로필 만들기 지원 [!DNL Target] 은(는) 아직 조회하지 않았습니다.
   * [!UICONTROL 벌크 프로필 업데이트 API] v2: 각각에 대해 모든 매개 변수 값을 지정할 필요는 없습니다 `pcId`. 프로필은 다음에 대해 만들어집니다. `pcId` 또는 `mbox3rdPartyId` 에서 찾을 수 없음 [!DNL Target].
   * [!UICONTROL 벌크 프로필 업데이트 API] v1: [!UICONTROL 벌크 프로필 업데이트 API] 기존 업데이트 [!DNL Target] 프로필만. v1을 사용하는 경우 프로필이 누락에 대해 생성되지 않습니다 `pcIds` 또는 `mbox3rdPartyIds`.
* [!UICONTROL 고객 속성] 을(를) 사용해야 함 [!UICONTROL EXPERIENCE CLOUD ID] (ECID) 및 CRM ID 또는 고객 충성도 ID와 같은 소스 ID의 사용.
* 다음 [!UICONTROL 벌크 프로필 업데이트 API] 는 TNT ID 또는 `mbox3rdPartyId`.
* `mbox3rdPartyID`에서 더하기 기호(+)와 슬래시(/)는 보낼 수 없습니다.

## 리소스

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)