---
keywords: 구현, 구현, 설정, 설정, 벌크 프로필 업데이트 api
description: '[!UICONTROL 벌크 프로필 업데이트 API]를 사용하여  [!DNL Target] 에 데이터를 가져옵니다.'
title: '[!UICONTROL 벌크 프로필 업데이트 API]를 사용하여  [!DNL Target] 에 데이터를 가져오려면 어떻게 해야 합니까?'
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
TQID: https://experienceleague.adobe.com/vBcIsBR6wwYr7MbRh7UJvt71ULDEq6iXVZ5spZlif-0
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 284
ht-degree: 5%

---

# 벌크 프로필 업데이트 API

[!DNL Adobe Target] [!UICONTROL 벌크 프로필 업데이트 API]를 사용하면 배치 파일을 사용하여 웹 사이트에 대한 여러 방문자의 사용자 프로필을 일괄적으로 업데이트할 수 있습니다.

[!UICONTROL 벌크 프로필 업데이트 API]를 사용하면 많은 사용자에 대한 프로필 매개 변수 형식의 자세한 방문자 프로필 데이터를 외부 소스에서 [!DNL Target]에 편리하게 보낼 수 있습니다. 외부 소스에는 일반적으로 웹 페이지에서 사용할 수 없는 CRM(고객 관계 관리) 또는 POS(판매 지점) 시스템이 포함될 수 있습니다.

[!UICONTROL 벌크 프로필 업데이트 API]를 [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)과(와) 대조합니다.

## [!UICONTROL 고객 특성]과 [!UICONTROL 벌크 프로필 업데이트 API]

이 옵션은 다음과 같은 몇 가지 차이점이 있는 [[!UICONTROL 고객 특성]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md)과 비슷합니다.

* [!UICONTROL 고객 특성]에서 FTP 업로드를 사용합니다. [!UICONTROL Target 벌크 프로필 업데이트 API]에서 HTTP POST API를 사용합니다.
* [!UICONTROL 고객 특성] 데이터를 [!DNL Analytics]과(와) 공유할 수 있습니다. [!UICONTROL 벌크 프로필 업데이트]는 [!DNL Target]에서만 사용할 수 있습니다.
* [!DNL Target] 사용자에 대한 프로필 만들기를 지원하는 [!UICONTROL 고객 특성]이(가) 아직 표시되지 않았습니다.
   * [!UICONTROL 벌크 프로필 업데이트 API] v2: 각 `pcId`에 대해 모든 매개 변수 값을 지정할 필요는 없습니다. [!DNL Target]에서 찾을 수 없는 `pcId` 또는 `mbox3rdPartyId`에 대해 프로필이 만들어집니다.
   * [!UICONTROL 벌크 프로필 업데이트 API] v1: [!UICONTROL 벌크 프로필 업데이트 API]는 기존 [!DNL Target]개의 프로필만 업데이트합니다. v1을 사용하는 경우 누락된 `pcIds` 또는 `mbox3rdPartyIds`에 대한 프로필이 만들어지지 않습니다.
* [!UICONTROL 고객 특성]에는 [!UICONTROL Experience Cloud ID]&#x200B;(ECID)와 소스 ID(예: CRM ID 또는 고객 충성도 ID)를 사용해야 합니다.
* [!UICONTROL 벌크 프로필 업데이트 API]에는 TNT ID 또는 `mbox3rdPartyId`이(가) 필요합니다.
* `mbox3rdPartyID`에서 더하기 기호(+)와 슬래시(/)는 보낼 수 없습니다.

## 리소스

자세한 내용은 다음 문서를 참조하십시오.

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)