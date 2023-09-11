---
title: 구현 패턴 개요
description: 구현 패턴을 사용하는 방법 이해
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 7a79eb1d263cf42529a5a1b1ca1f9de4db218a49
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# 구현 패턴 개요

[!DNL Adobe Target] 구현 패턴을 통해 다음을 이해하고 만들 수 있습니다. [!DNL Target] 구현.

이미지를 클릭하여 전체 화면으로 확장합니다.

![Adobe Target 아키텍처 다이어그램](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

이미지의 숫자는 작업 순서를 나타내지 않습니다.

1. 용 클라이언트측 SDK [!DNL Adobe Target] 및 [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] 호출
1. ECID 획득 호출
1. 벌크 프로필 업데이트 API 및 [!DNL Customer Attributes] (CA) 서비스
1. 고객의 데이터 소스에서 다음으로 프로필 데이터 수집 [!DNL Target] 프로필 저장소
1. 프로필/행동 데이터 수집 및 최종 사용자에게 표시할 경험 결정
1. 페이지에서 렌더링되는 경험
1. at.js는 페이지에서 경험을 렌더링합니다

각 패턴은 서로 다른 부품으로 구성됩니다. 각 부분은 다음을 위한 중요한 구현 요구 사항에 해당합니다. [!DNL Target] 구현.

각 부분은 이 안내서의 별도 페이지에 설명되어 있습니다. 예를 들어 [[!DNL Recommendations] at.js를 사용한 구현 패턴](/help/dev/patterns/recs-atjs/recs-implementation-pattern-atjs.md) 에는 다음 페이지가 포함되어 있습니다.

* SDK 초기화
* 데이터 수집 구성
* 렌더링 경험
* 알림 [!DNL Target]

