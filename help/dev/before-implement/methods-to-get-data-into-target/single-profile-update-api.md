---
keywords: 구현, 구현, 설정, 설정, 단일 프로필 업데이트
description: 데이터 가져오기 [!DNL Target] 단일 프로필 업데이트 API 사용.
title: 데이터를으로 가져오는 방법 [!DNL Target] 단일 프로필 업데이트 API를 사용하시겠습니까?
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 35%

---

# 싱글 프로필 업데이트 API

와 거의 같음 [!UICONTROL 벌크 프로필 업데이트 API] 위치: [!DNL Adobe Target], 그러나 방문자 프로필은 API 호출에서 .csv 파일 대신 한 번에 하나씩 업데이트됩니다.

## 형식

방문자는 [!DNL Target]mboxPC 값이나 `mbox3rdPartyId` 값을 통해 식별해야 합니다. Experience Cloud ID(ECID)는 지원되지 않습니다. 

## 사용 사례 예

일부 오프라인 작업을 수행하는 단일 방문자의 프로필을 업데이트하려고 합니다. 콜 센터 문의, 대출 지원, 매장 내 로열티 카드 사용, 키오스크 액세스 등의 작업을 수행할 수 있습니다.

## 메서드의 이점

프로필 속성의 개수에 대한 제한은 없습니다.

사이트를 통해 전송된 프로필 속성은 API를 통해 업데이트할 수 있으며 반대의 경우도 마찬가지입니다.

## 주의 사항

24시간 기간당 1,000,000개의 API 호출 수 제한(1백만)

프로필만 업데이트합니다. 잠재적 사용자에 대한 프로필을 만들 수 없음 [!DNL Target] 은(는) 아직 보지 못했습니다.

업데이트는 일반적으로 1시간 이내에 발생하지만 반영하는 데 24시간 정도 소요될 수 있습니다.

## 코드 예

GET 및 POST가 지원됩니다.

```
https://CLIENT.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr1=0&profile.attr2=1...
```

## 리소스

* [프로필 업데이트](https://developers.adobetarget.com/api/#updating-profiles)
