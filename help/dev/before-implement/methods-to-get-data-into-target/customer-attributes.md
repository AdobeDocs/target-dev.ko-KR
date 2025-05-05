---
keywords: 구현, 구현, 설정, 설정, 고객 속성
description: 고객 특성을 사용하여  [!DNL Target] 에 데이터를 가져옵니다.
title: 고객 특성을 사용하여  [!DNL Target] 에 데이터를 가져오려면 어떻게 해야 합니까?
feature: Implementation
exl-id: d05cdd38-ba7c-4f29-a0ef-ae68619e7617
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 14%

---

# 고객 속성

고객 특성을 사용하면 FTP를 통해 방문자 프로필 데이터를 [!DNL Adobe Experience Cloud]에 업로드할 수 있습니다. 업로드한 후에는 [!DNL Adobe Analytics] 및 [!DNL Adobe Target]의 데이터를 사용합니다.

Target Standard 고객은 5개의 특성을 적용할 수 있으며 [!DNL Target Premium] 고객은 200개의 특성을 적용할 수 있습니다.

## 형식

ECID(ID) 및 특성 이름/값 쌍이 [!DNL Experience Cloud]인 .csv 파일이 FTP를 통해 업로드되거나 Experience Cloud UI에서 수동으로 업로드됩니다.

## 예시 사용 사례

CRM 또는 기타 내부 시스템에는 [!DNL Target] 및 [!DNL Analytics]을(를) 포함하여 [!DNL Adobe Experience Cloud]과(와) 공유할 중요한 정보가 저장되어 있습니다.

## 메서드의 이점

[!DNL Target]이(가) 아직 방문자를 보지 못했더라도 고객 데이터를 업로드하면 Target에서 해당 방문자에 대한 프로필 항목이 만들어집니다.

[!DNL Target] 및 [!DNL Analytics]에서 동일한 데이터를 자동으로 사용할 수 있습니다.

FTP는 API보다 간단한 구현 방법일 수 있습니다.

## 주의 사항

Target Standard 고객은 5개의 특성을 적용할 수 있으며 [!DNL Target Premium] 고객은 200개의 특성을 적용할 수 있습니다.

페이지에서가 아니라 고객 속성을 통해서만 값을 업데이트할 수 있습니다.

Experience Cloud ID(ECID) 구현이 필요합니다.

## 코드 예

자세한 내용은 [고객 특성 원본을 만들고 데이터 파일을 업로드](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html?lang=ko)하는 방법을 참조하십시오.

### 관련 정보 링크

[고객 특성 원본을 만들고 데이터 파일을 업로드](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html?lang=ko)합니다.
