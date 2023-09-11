---
title: 구현 패턴 개요
description: 구현 패턴을 사용하는 방법 이해
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: e15513f5c52240536ccf41f16ba7f4dc6dbf9a04
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 구현 패턴 개요

[!DNL Adobe Target] 구현 패턴을 통해 다음을 이해하고 만들 수 있습니다. [!DNL Target] 구현.

이미지를 클릭하여 전체 화면으로 확장합니다.

![Adobe Target 아키텍처 다이어그램](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

이미지의 숫자는 작업 순서를 나타내지 않습니다.

1. 용 클라이언트측 SDK [!DNL Adobe Target] 및 [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] 호출
1. [!UICONTROL EXPERIENCE CLOUD ID] (ECID) 획득 호출
1. 벌크 프로필 업데이트 API 및 [!DNL Customer Attributes] (CA) 서비스
1. 고객의 데이터 소스에서 다음으로 프로필 데이터 수집 [!DNL Target] 프로필 저장소
1. 프로필 및 행동 데이터 수집 및 방문자에게 표시할 경험 결정
1. 페이지에서 렌더링되는 경험
1. at.js는 페이지에서 경험을 렌더링합니다

각 패턴은 서로 다른 부분으로 구성되며 각 부분은 의 중요한 구현 요구 사항에 해당합니다. [!DNL Target] 구현.

이 안내서에서는 각 부분에 대해 별도의 주제로 설명합니다. 예를 들어 [[!DNL Recommendations] at.js를 사용한 구현 패턴](/help/dev/patterns/recs-atjs/recs-implementation-pattern-atjs.md) 에는 다음 항목이 포함되어 있습니다.

* SDK 초기화
* 데이터 수집 구성
* 렌더링 경험
* 알림 [!DNL Target]

