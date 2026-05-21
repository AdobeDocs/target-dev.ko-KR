---
keywords: 구현, 구현, 설정, 설정, 데이터 공급자
description: 데이터 공급자를 사용하여  [!DNL Target] 에 데이터를 가져옵니다.
title: 데이터 공급자를 사용하여  [!DNL Target] 에 데이터를 가져오려면 어떻게 해야 합니까?
feature: Implementation
exl-id: 9971bd96-f736-4965-afe2-b4901c12d006
TQID: https://experienceleague.adobe.com/e8uMaGcACjHiaIT4WSlbKry82mhLHUDTSKmCuuhoWgw
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 314
ht-degree: 50%

---

# 데이터 공급자

데이터 공급자는 타사에서 [!DNL Adobe Target]&#x200B;(으)로 데이터를 쉽게 전달할 수 있는 기능입니다.

>[!NOTE]
>
>데이터 공급자는 at.js 1.3 이상이 필요합니다.

## 형식

`window.targetGlobalSettings.dataProviders` 설정은 데이터 공급자의 배열입니다.

각 데이터 공급자 구조에 대한 자세한 내용은 [데이터 공급자](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers)를 참조하십시오.

## 예시 사용 사례

날씨 서비스, DMP 또는 사용자 지정 웹 서비스와 같은 타사로부터 데이터를 수집합니다. 그런 다음, 이 데이터를 사용하여 대상자, Target 콘텐츠를 작성하고 방문자 프로필을 보강할 수 있습니다.

## 메서드의 이점

이 설정을 사용하면 고객이 Demandbase, BlueKai 및 사용자 지정 서비스와 같은 타사 데이터 공급자로부터 데이터를 수집하고, 글로벌 mbox 요청의 mbox 매개 변수로 데이터를 [!DNL Target]에 전달할 수 있습니다.

비동기 및 동기 요청을 통해 여러 공급자로부터 데이터를 수집하도록 지원합니다.

이 접근 방식을 사용하면 각 공급자에 대해 독립적인 시간 제한을 포함하여 페이지 성능에 미치는 영향을 제한하면서, 기본 페이지 콘텐츠의 깜박임을 쉽게 관리할 수 있습니다

## 주의 사항

`window.targetGlobalSettings.dataProviders`에 추가된 데이터 공급자가 비동기 상태인 경우 병렬로 실행됩니다. 최소 대기 시간을 허용하기 위해 방문자 API 요청이 `window.targetGlobalSettings.dataProviders`에 추가된 함수와 함께 실행됩니다.

at.js는 데이터를 캐시하려고 하지 않습니다. 데이터 공급자는 데이터를 한 번만 가져오는 경우 데이터가 캐시되는지 확인해야 하고, 공급자 함수가 호출될 때 두 번째 호출을 위해 캐시 데이터를 제공해야 합니다.

## 코드 예

[데이터 공급자](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers)에서 몇 가지 예를 볼 수 있습니다.

## 관련 정보 링크

문서: [데이터 공급자](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers)

## 교육 비디오:

* [Adobe Target에서 데이터 공급자 사용](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/use-data-providers-to-integrate-third-party-data.html)
* [Adobe Target에서 데이터 공급자 구현](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/implement-data-providers-to-integrate-third-party-data.html)
