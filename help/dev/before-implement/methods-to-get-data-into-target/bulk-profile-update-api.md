---
keywords: 구현, 구현, 설정, 설정, 벌크 프로필 업데이트 api
description: 데이터 가져오기 [!DNL Target] 사용 [!UICONTROL 벌크 프로필 업데이트 API].
title: 데이터를으로 가져오는 방법 [!DNL Target] 사용 [!UICONTROL 벌크 프로필 업데이트 API]?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: af9db32d59bdf32f2b9fade267922803250377dd
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 23%

---

# 벌크 프로필 업데이트 API

API를 통해 .csv 파일을으로 보냅니다. [!DNL Adobe Target] (많은 방문자에 대한 방문자 프로필 업데이트 포함) 각 방문자 프로필은 하나의 호출에서 여러 개의 인페이지 프로필 속성으로 업데이트할 수 있습니다.

이 옵션은 과 유사합니다. [!UICONTROL 고객 속성] 몇 가지 차이점이 있습니다.

* [!UICONTROL 고객 속성] ftp 업로드를 사용합니다. 다음 [!UICONTROL Target 벌크 프로필 업데이트 API] 는 HTTP POST API를 사용합니다.
* [!UICONTROL 고객 속성] 데이터 공유 대상: [!DNL Analytics]. [!UICONTROL 벌크 프로필 업데이트] 다음에서만 사용할 수 있습니다. [!DNL Target].
* [!UICONTROL 고객 속성] 사용자를 위한 프로필 만들기 지원 [!DNL Target] 은(는) 아직 조회하지 않았습니다.
   * [!UICONTROL 벌크 프로필 업데이트 API] v2: 각각에 대해 모든 매개 변수 값을 지정할 필요는 없습니다 `pcId`. 프로필은 다음에 대해 만들어집니다. `pcId` 또는 `mbox3rdPartyId` 에서 찾을 수 없음 [!DNL Target].
   * [!UICONTROL 벌크 프로필 업데이트 API] v1: [!UICONTROL 벌크 프로필 업데이트 API] 기존 업데이트 [!DNL Target] 프로필만. v1을 사용하는 경우 프로필이 누락에 대해 생성되지 않습니다 `pcIds` 또는 `mbox3rdPartyIds`.
* [!UICONTROL 고객 속성] 을(를) 사용해야 함 [!UICONTROL EXPERIENCE CLOUD ID] (ECID) 및 CRM ID 또는 고객 충성도 ID와 같은 소스 ID의 사용.
* 다음 [!UICONTROL 벌크 프로필 업데이트 API] 는 TNT ID 또는 `mbox3rdPartyId`.
* `mbox3rdPartyID`에서 더하기 기호(+)와 슬래시(/)는 보낼 수 없습니다.

## 형식

.csv 파일은 를 통해 각 방문자를 참조해야 합니다 [!DNL Target] PCID 또는 `mbox3rdPartyId`. 다음 [!UICONTROL EXPERIENCE CLOUD ID] (ECID)는 지원되지 않습니다. 모든 프로필 속성/값은 API를 통해 생성 및 업데이트됩니다. 형식 세부 사항은 API 설명서에 나와 있습니다.

## 예시 사용 사례

CRM 또는 기타 내부 시스템에는 지속적으로 업데이트하려는 방문자에 대한 중요한 데이터가 저장됩니다 [!DNL Target], 페이지 구현에서 프로필 데이터를 노출하지 않습니다.

## 메서드의 이점

* 프로필 속성의 개수에 대한 제한은 없습니다.
* 사이트를 통해 전송된 프로필 속성은 API를 통해 또는 그 반대로 업데이트할 수 있습니다.

## 주의 사항

* 묶음 파일의 크기는 50MB 미만이어야 합니다. 또한 총 행 수는 업로드당 500,000개 행을 초과하지 않아야 합니다.
* 업데이트는 일반적으로 1시간 이내에 발생하지만 반영하는 데 24시간 정도 소요될 수 있습니다.
* 후속 배치에서 24시간 동안 업로드할 수 있는 행 수에는 제한이 없습니다. 그러나 영업 시간 동안 처리 프로세스를 조절하여 다른 프로세스가 효율적으로 실행되도록 할 수도 있습니다.
* 동일한 항목 사이에 mbox 호출이 없는 연속적인 V2 배치 업데이트 호출 `thirdPartyIds` 첫 번째 배치 업데이트 호출에서 업데이트된 속성을 재정의합니다.

## 리소스

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)