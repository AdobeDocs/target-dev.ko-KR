---
keywords: 구현, 구현, 설정, 설정, 데이터 공급자
description: 데이터 가져오기 [!DNL Target] 데이터 공급자 사용.
title: 데이터를으로 가져오는 방법 [!DNL Target] 데이터 공급자를 사용하시겠습니까?
feature: Implementation
exl-id: 9971bd96-f736-4965-afe2-b4901c12d006
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 53%

---

# 데이터 공급자

데이터 공급자는 타사에서 로 데이터를 쉽게 전달할 수 있는 기능입니다 [!DNL Adobe Target].

>[!NOTE]
>
>데이터 공급자는 at.js 1.3 이상이 필요합니다.

## 형식

`window.targetGlobalSettings.dataProviders` 설정은 데이터 공급자의 배열입니다.

각 데이터 공급자 구조에 대한 자세한 내용은 [데이터 공급자](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers)를 참조하십시오.

## 예시 사용 사례

날씨 서비스, DMP 또는 사용자 지정 웹 서비스와 같은 타사로부터 데이터를 수집합니다. 그런 다음, 이 데이터를 사용하여 대상, Target 콘텐츠를 작성하고 방문자 프로필을 보강할 수 있습니다.

## 메서드의 이점

이 설정을 사용하면 고객이 Demandbase, BlueKai 및 사용자 지정 서비스와 같은 타사 데이터 공급자로부터 데이터를 수집하여 로 전달할 수 있습니다 [!DNL Target] 글로벌 mbox 요청에 mbox 매개 변수로 사용됩니다.

비동기 및 동기 요청을 통해 여러 공급자로부터 데이터를 수집하도록 지원합니다.

이 접근 방식을 사용하면 각 공급자에 대해 독립적인 시간 제한을 포함하여 페이지 성능에 미치는 영향을 제한하면서, 기본 페이지 콘텐츠의 깜박임을 쉽게 관리할 수 있습니다

## 주의 사항

데이터 공급자가에 추가된 경우 `window.targetGlobalSettings.dataProviders` 비동기 상태인 경우 병렬로 실행됩니다. 방문자 API 요청은에 추가된 함수와 함께 실행됩니다 `window.targetGlobalSettings.dataProviders` 최소 대기 시간을 허용합니다.

at.js는 데이터를 캐시하려고 하지 않습니다. 데이터 공급자는 데이터를 한 번만 가져오는 경우 데이터가 캐시되는지 확인해야 하고, 공급자 함수가 호출될 때 두 번째 호출을 위해 캐시 데이터를 제공해야 합니다.

## 코드 예

[데이터 공급자](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers)에서 몇 가지 예를 볼 수 있습니다.

## 관련 정보 링크

문서: [데이터 공급자](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers)

## 교육 비디오:

* [Adobe Target에서 데이터 공급자 사용](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/use-data-providers-to-integrate-third-party-data.html)
* [Adobe Target에서 데이터 공급자 구현](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/implement-data-providers-to-integrate-third-party-data.html)
