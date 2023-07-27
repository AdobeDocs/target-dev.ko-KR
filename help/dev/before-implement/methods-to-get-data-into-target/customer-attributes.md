---
keywords: 구현, 구현, 설정, 설정, 고객 속성
description: 데이터 가져오기 [!DNL Target] 고객 속성을 사용합니다.
title: 데이터를으로 가져오는 방법 [!DNL Target] 고객 속성을 사용하시겠습니까?
feature: Implementation
exl-id: d05cdd38-ba7c-4f29-a0ef-ae68619e7617
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 18%

---

# 고객 속성

고객 속성을 사용하면 FTP를 통해 방문자 프로필 데이터를 [!DNL Adobe Experience Cloud]. 업로드했으면 의 데이터를 사용합니다. [!DNL Adobe Analytics] 및 [!DNL Adobe Target].

Target Standard 고객은 5개의 특성, [!DNL Target Premium] 고객은 200개의 속성을 적용할 수 있습니다.

## 형식

이 포함된 .csv 파일 [!DNL Experience Cloud] ID(ECID) 및 속성 이름/값 쌍은 FTP를 통해 업로드되거나 Experience Cloud UI에서 수동으로 업로드됩니다.

## 예시 사용 사례

CRM 또는 기타 내부 시스템은 공유할 중요한 정보를 저장합니다 [!DNL Adobe Experience Cloud], 포함 [!DNL Target] 및 [!DNL Analytics].

## 메서드의 이점

고객 데이터를 업로드하면 다음과 같은 경우에도 Target에서 해당 방문자에 대한 프로필 항목이 만들어집니다 [!DNL Target] 은(는) 아직 방문자를 보지 못했습니다.

동일한 데이터는에서 자동으로 사용할 수 있습니다. [!DNL Target] 및 [!DNL Analytics].

FTP는 API보다 간단한 구현 방법일 수 있습니다.

## 주의 사항

Target Standard 고객은 5개의 특성, [!DNL Target Premium] 고객은 200개의 속성을 적용할 수 있습니다.

페이지에서가 아니라 고객 속성을 통해서만 값을 업데이트할 수 있습니다.

Experience Cloud ID(ECID) 구현이 필요합니다.

## 코드 예

세부 사항은 다음 위치에서 찾을 수 있습니다. [고객 속성 소스를 만들고 데이터 파일 업로드](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html).

### 관련 정보 링크

[고객 속성 소스를 만들고 데이터 파일 업로드](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html).
