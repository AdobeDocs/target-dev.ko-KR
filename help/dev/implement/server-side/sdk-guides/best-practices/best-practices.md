---
title: 온디바이스 의사 결정 사용 시 모범 사례
description: ' [!DNL Adobe Target]에서 [!UICONTROL on-device decisioning]을(를) 사용할 때의 모범 사례 알아보기'
feature: Implement Server-side
exl-id: a0ca014d-ad9f-4ecc-961d-cb7ba236507f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# 모범 사례

[!DNL Adobe]은(는) [!UICONTROL on-device decisioning]을(를) 사용할 때 다음 모범 사례를 권장합니다.

## 의사 결정 방법이 &quot;온디바이스&quot;인 경우의 모범 사례

의사 결정 방법으로 &quot;온디바이스&quot;를 사용하는 경우 방문자가 웹 페이지를 처음 로드하면 아티팩트가 다운로드됩니다. 첫 번째 페이지 로드 시 발생해야 하는 모든 활동 자격(캐시 없음)은 아티팩트가 완전히 다운로드된 후에만 발생합니다. 새 익명 방문자에 대해 활동 자격이 빠르게 수행되도록 하기 위해 따를 수 있는 특정 모범 사례가 있습니다.

* 아티팩트에 있지 않은 &quot;디바이스에서&quot; 가능 활동을 비활성화합니다.
* Target Premium이 있는 경우 [속성/작업 공간](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=ko-KR)을 사용하여 작업 공간별로 다른 아티팩트 파일을 만들 수 있습니다.
* 합법적인 이유로 인해 아티팩트 파일이 매우 커지면 &quot;hybrid&quot; 의사 결정 방법을 사용할 수 있습니다. 이 메서드를 사용하면 아티팩트를 병렬로 다운로드할 수 있으며 아티팩트가 다운로드될 때까지 모든 Target API 호출이 중단됩니다. 이 접근 방식에 대한 자세한 내용은 아래의 &quot;하이브리드&quot; 의사 결정 모드에 대한 모범 사례 섹션을 참조하십시오.
* 단일 페이지 응용 프로그램(SPA)이 있는 경우 [!DNL Adobe]에서는 첫 번째 페이지 로드 중에 응용 프로그램의 기본 JavaScript 파일을 로드하기 전에 at.js를 로드하고 초기화하는 것이 좋습니다. 이 접근 방식은 훨씬 이전에 아티팩트 다운로드를 시작하므로 더 빠른 경험 렌더링을 제공합니다.

## 의사 결정 방법이 &quot;하이브리드&quot;인 경우의 모범 사례

의사 결정 메서드로 &quot;hybrid&quot;를 사용하는 경우 아티팩트가 동시에 다운로드됩니다. 아티팩트가 다운로드될 때까지 &quot;위치&quot;가 디바이스에서 사용 가능한 경우에도 모든 [!DNL Target] API 호출이 회선됩니다. 이 동작은 모든 `getOffers()` 호출에 대한 기본값이며 대부분의 상황에서 최상의 성능을 제공합니다. `decisioningMethod`을(를) `on-device`(으)로 설정하여 `getOffers()`의 기본 동작을 변경하는 경우 다음 모범 사례에 따라 오류를 방지하고 최상의 성능을 보장하십시오.

* 페이지가 처음 로드될 때 `decisioningMethod`을(를) `on-device`(으)로 사용하여 `getOffers()`을(를) 호출하기로 결정한 경우 오류를 방지하려면 &quot;ARTIFACT_DOWNLOAD_SUCCEEDED&quot; at.js 이벤트 처리기 내에서 호출해야 합니다. 아티팩트가 매우 큰 경우 이 접근 방식을 사용하는 모든 &quot;위치&quot;는 아티팩트가 완전히 다운로드된 후에만 렌더링되므로 경험 렌더링이 지연될 수 있습니다. [!DNL Adobe]에서는 이 방법을 거의 사용하지 않는 것이 좋습니다. 이 접근 방식을 사용할 때 위의 &quot;장치 내&quot; 모범 사례 섹션에서 아티팩트 크기를 줄이는 모범 사례를 따르십시오.
