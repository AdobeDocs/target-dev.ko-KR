---
title: Adobe Target 프로필 API
description: Adobe Target 프로필 API를 사용하여 방문자 데이터를  [!DNL Target](으)로 보내는 방법을 알아봅니다.
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 480cbbbe-4822-48c3-80d4-53628dee57b0
source-git-commit: e2462d12cf58ab5a588c13a96df5e6abafb9d675
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 1%

---

# [!DNL Adobe Target Profiles API] 개요

[!DNL Adobe Target]은(는) 모든 개별 사용자에 대한 프로필을 만들고 유지 관리합니다. 이 프로필은 [!DNL Target] 에지 클러스터에 저장되며 방문할 때마다 실시간으로 업데이트됩니다.

## [!DNL Target] 프로필 구조

Target 프로필은 다음 객체로 구성됩니다.

| 개체 | 세부 사항 |
| --- | --- |
| `clientcode` | 프로필이 연결된 [!DNL Target] 클라이언트 코드입니다. |
| `visitorId` | 프로필용 식별자. `tntid`, `thirdpartyid` 또는 `marketingcloudvisitorid`일 수 있습니다. |
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
