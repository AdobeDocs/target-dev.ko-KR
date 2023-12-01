---
keywords: 구현, 구현, 설정, 설정, 단일 프로필 업데이트
description: 데이터 가져오기 [!DNL Target] 단일 프로필 업데이트 API 사용.
title: 데이터를으로 가져오는 방법 [!DNL Target] 사용 [!UICONTROL 단일 프로필 업데이트 API]?
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
source-git-commit: 43f4fb8345a77ccb0e112fe196e7e0944cc468c9
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---

# [!UICONTROL 단일 프로필 업데이트 API]

다음 [!DNL Adobe Target] [!UICONTROL 단일 프로필 업데이트 API] 단일 사용자에 대한 프로필 업데이트를 보낼 수 있습니다. 다음 [!UICONTROL 단일 프로필 업데이트 API] 는 과 거의 동일합니다. [!UICONTROL 벌크 프로필 업데이트 API], 그러나 방문자 프로필은 .cvs 파일 대신 API 호출에 인라인으로 한 번에 하나씩 업데이트됩니다.

다음 [!UICONTROL 단일 프로필 업데이트 API] 및 는 일반적으로 구현되지 않은 채널에서 발생하는 트랜잭션과 관련하여 업데이트가 발생해야 하는 경우에 사용됩니다 [!DNL Target]. 예를 들어 일부 오프라인 작업을 수행하는 단일 방문자의 프로필을 업데이트하려고 합니다. 콜 센터 문의, 대출 지원, 매장 내 로열티 카드 사용, 키오스크 액세스 등의 작업을 수행할 수 있습니다.

## 리소스:

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)
