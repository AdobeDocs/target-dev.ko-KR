---
title: Adobe Target 프로필 API
description: Adobe Target 프로필 API를 사용하여 방문자 데이터를 (으)로 보내는 방법 알아보기 [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
source-git-commit: 289299a52e5611c0da341f313aa4a447fcf3666a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---

# [!DNL Adobe Target Profiles API] 개요

[!DNL Adobe Target] 모든 개별 사용자에 대한 프로필을 만들고 유지 관리합니다. 이 프로필은 [!DNL Target] 에지 클러스터 및 가 방문할 때마다 실시간으로 업데이트됩니다.

## 프로필 [!DNL Postman] 컬렉션

[!DNL Postman] 는 API 호출을 쉽게 실행할 수 있도록 하는 애플리케이션입니다. 이 [!DNL Postman] 컬렉션에 다음 항목이 모두 포함됨 [!DNL Profile API] 호출. 클릭 [Postman에서 실행](https://www.getpostman.com/collections/ec7376f9028977ccaa99){target=_blank} 프로필 API 컬렉션을 가져올 수 있습니다.

## 레거시 프로필 API 설명서.

이전 프로필 API 설명서는 여기에서 찾을 수 있습니다. [https://developers.adobetarget.com/api/#profiles](https://developers.adobetarget.com/api/#profiles){target=_blank}

## 의 구조 [!DNL Target] 프로필

Target 프로필은 다음 객체로 구성됩니다.

| 개체 | 세부 사항 |
| --- | --- |
| `clientcode` | 다음 [!DNL Target] 프로필이 연결된 클라이언트 코드입니다. |
| `visitorId` | 프로필용 식별자. 다음과 같을 수 있습니다. `tntid`, `thirdpartyid`, 또는 `marketingcloudvisitorid`. |
| `modifiedAt` | 프로필이 마지막으로 업데이트된 시점의 타임스탬프입니다. |
| `profileAttributes` | 해당 개별 프로필에 키-값 쌍으로 저장된 모든 프로필 속성 목록입니다. |

### 샘플 프로필 구조

```
{
    "client": "<your-tenant-name>",
    "visitorId": "a1-mbox3rdPartyId",
    "modifiedAt": "2017-08-18T17:53:39.003-04:00",
    "profileAttributes": {
        "insurance": {
            "value": "false",
            "modifiedAt": "2017-07-31T20:34:55.625-04:00"
        },
        "country": {
            "value": "france",
            "modifiedAt": "2017-07-31T14:26:30.879-04:00"
        },
        "checking": {
            "value": "true",
            "modifiedAt": "2017-07-31T20:34:55.625-04:00"
        },
        "user.memberlevel": {
            "value": "0.0",
            "modifiedAt": "2017-08-09T18:18:04.661-04:00"
        },
        "param1": {
            "value": "value1",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "param2": {
            "value": "value2",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "firstSessionStart": {
            "value": "1500648715286",
            "modifiedAt": "2017-07-21T10:51:55.286-04:00"
        },
        "entity.name": {
            "value": "my-entityName",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "entity.id": {
            "value": "my-entityId",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        }
    }
}
```
