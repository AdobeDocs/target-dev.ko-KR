---
keywords: 구현, 구현, 설정, 설정, 벌크 프로필 업데이트
description: 데이터 가져오기 [!DNL Target] 벌크 프로필 업데이트 API 사용.
title: 데이터를으로 가져오는 방법 [!DNL Target] 벌크 프로필 업데이트 API를 사용하시겠습니까?
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 60%

---

# 벌크 프로필 업데이트 API

API를 통해 .csv 파일을으로 보냅니다. [!DNL Adobe Target] (많은 방문자에 대한 방문자 프로필 업데이트 포함) 각 방문자 프로필은 하나의 호출에서 여러 개의 인페이지 프로필 속성으로 업데이트할 수 있습니다.

이 옵션은 다음과 같은 몇 가지 차이점이 있는 고객 속성과 유사합니다.

* 고객 속성은 다음을 수행하는 동안 FTP 업로드를 사용합니다 [!UICONTROL Target 벌크 프로필 업데이트 API] 는 HTTP POST API를 사용합니다.
* 고객 속성 데이터를 공유할 수 있는 대상 [!DNL Analytics]. [!UICONTROL 벌크 프로필 업데이트는 Target에서만 사용할 수 있습니다.]
* 사용자 프로필 작성을 지원하는 고객 속성 [!DNL Target] 은(는) 아직 조회하지 않았습니다. 벌크 프로필 업데이트 API 업데이트 기존 [!DNL Target] 프로필만.
* 고객 속성을 사용하려면 ECID(Experience Cloud ID)와 소스 ID(예: CRM ID 또는 로열티 ID)를 사용해야 합니다.
* 벌크 프로필 업데이트 API에는 TNT ID나 `mbox3rdPartyId`를 사용해야 합니다.
* `mbox3rdPartyID`에서 더하기 기호(+)와 슬래시(/)는 보낼 수 없습니다.

## 형식

.csv 파일은 각 방문자를 참조해야 합니다 [!DNL Target] PCID 또는 `mbox3rdPartyId`. Experience Cloud ID(ECID)는 지원되지 않습니다. 모든 프로필 속성/값은 API를 통해 생성 및 업데이트됩니다. 형식 세부 사항은 API 설명서에 나와 있습니다.

## 예시 사용 사례

CRM 또는 기타 내부 시스템은 페이지 구현에서 프로필 데이터를 노출하지 않고 Target에 지속적으로 업데이트하고자 하는 방문자에 대한 중요 데이터를 저장합니다.

## 메서드의 이점

프로필 속성의 개수에 대한 제한은 없습니다.

사이트를 통해 전송된 프로필 속성은 API를 통해 업데이트할 수 있으며 반대의 경우도 마찬가지입니다.

## 주의 사항

묶음 파일의 크기는 50MB 미만이어야 합니다. 또한 총 행 수는 업로드당 500,000개 행을 초과하지 않아야 합니다.

이후 묶음에서 24시간 동안 업로드할 수 있는 행 수에는 제한이 없습니다. 그러나 영업 시간 동안 처리 프로세스를 조절하여 다른 프로세스가 효율적으로 실행되도록 할 수도 있습니다.

동일한 thirdPartyIds 간에 mbox를 호출하지 않고 연속적인 [V2 배치 업데이트를 호출](https://developers.adobetarget.com/api/#updating-profiles)하면 첫 번째 배치 업데이트 호출에서 업데이트된 속성을 재정의합니다.

## 코드 예

[프로필 업데이트](https://developers.adobetarget.com/api/#updating-profiles)를 참조하십시오.

### 관련 정보 링크

[프로필 업데이트](https://developers.adobetarget.com/api/#updating-profiles)
