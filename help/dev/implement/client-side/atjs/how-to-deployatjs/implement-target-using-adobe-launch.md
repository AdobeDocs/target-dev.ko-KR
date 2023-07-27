---
keywords: 구현, 구현, 구현, adobe launch, launch, 경쟁, 리디렉션, 경험 platform launch, platform launch, 태그, adobe platform, 구현2
description: 구현 방법 알아보기 [!DNL Adobe Target] at.js 라이브러리 [!DNL Adobe Experience Platform]를 사용하는 것이 좋습니다. Target 구현 방법.
title: 구현 방법 [!DNL Target] 사용 [!DNL Adobe Experience Platform]?
feature: Implement Server-side
exl-id: 0a325871-194a-479c-a3bf-294e3dde3e9a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 8%

---

# [!DNL Target]을 사용하여[!DNL Adobe Experience Platform]구현 

의 태그 [!DNL Adobe Experience Platform] 의 차세대 태그 관리 기능입니다. [!DNL Adobe]. 태그는 관련 고객 환경을 향상하는 데 필요한 분석, 마케팅 및 광고 태그를 배포하고 관리하는 간단한 방법을 고객에게 제공합니다.

>[!NOTE]
>
>Adobe Experience Platform Launch은 의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. [!DNL Adobe Experience Platform]. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 다음 사항을 참조하십시오 [문서](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?) 용어 변경에 대한 통합 참조.

다음 표에는 자세한 정보를 얻을 수 있는 다양한 소스가 나열되어 있습니다.

| 리소스 | 세부 사항 |
|--- |--- |
| [Adobe Target 추가](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/target.html#implement-solutions) | 이 자습서에서는 를 구현하는 단계별 지침을 제공합니다 [!DNL Target] 에 태그가 있는 웹 사이트에서 [!DNL Adobe Experience Platform]. 다뤄지는 주제에는 at.js JavaScript 라이브러리 추가, 글로벌 mbox 실행, 매개 변수 추가 및 다른 솔루션과의 통합이 있습니다. 이 문서는 Adobe Experience Platform 및 기타 Adobe Experience Cloud 솔루션을 구현하는 방법을 보여 주는 대규모 자습서의 일부입니다. |
| [빠른 시작 안내서](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html) | 관련 고객 환경을 향상하는 데 필요한 분석, 마케팅 및 광고 태그를 배포하고 관리하는 방법에 대한 정보입니다. |
| [Adobe [!DNL Target] 확장 개요](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html) | 구현에 대한 정보 [!DNL Target] 사용 [!DNL Adobe Experience Platform]. |

## 를 사용하여 at.js를 구현할 때의 이점 [!DNL Target] 확장

다음 장점은 의 태그를 사용하는 경우에만 적용됩니다 [!DNL Adobe Experience Platform] at.js 구현 이러한 이유로 Adobe은에서 태그를 사용할 것을 강력히 제안합니다 [!DNL Adobe Experience Platform] at.js의 수동 구현이 아닙니다.

* **해결 [!DNL Adobe Analytics] 및 [!DNL Target] 경쟁 조건:** 이유: [!DNL Analytics] 이(가) [!DNL Target] 호출, [!DNL Target] 호출이에 연결되지 않음 [!DNL Analytics] 호출합니다. 이러한 시퀀싱은 잘못된 데이터를 초래할 수 있습니다. 다음 [!DNL Target] 확장은 [!DNL Analytics] 비콘 호출은 [!DNL Target] 호출이 성공했는지 여부에 상관없이 완료됨. 에서 태그 사용 [!DNL Adobe Experience Platform] 은 수동으로 구현할 때 발생할 수 있는 데이터 불일치 문제를 해결합니다.

  >[!NOTE]
  >
  >에서 비콘 보내기 작업 사용 [!DNL Adobe Analytics] 확장 [!DNL Analytics] 호출 대기 시간 [!DNL Target] 호출합니다. 직접 전화를 거시면 `s.t()` 또는 `s.tl()` 사용자 지정 코드 사용, [!DNL Analytics] 통화는 다음 시간까지 기다리지 않습니다. [!DNL Target] 통화가 완료되었습니다.

* **잘못된 리디렉션 오퍼 처리 방지:** 다음을 보유한 경우: [!DNL Target] 및 [!DNL Analytics] 페이지에서, Target에 의해 실행되는 리디렉션 오퍼가 있으면 다음과 같은 상황이 발생할 수 있습니다. [!DNL Analytics] 추적기는 사용자가 다른 URL로 리디렉션되기 때문에 요청을 실행하지 말아야 할 때 요청을 실행합니다. 를 구현하는 경우 [!DNL Target] 및 [!DNL Analytics] 의 태그를 통해 [!DNL Adobe Experience Platform], 이 문제가 발생하지 않습니다. 에서 태그 사용 [!DNL Adobe Experience Platform], [!DNL Target] 지시 [!DNL Analytics] 을(를) 중단하려면 [!DNL Analytics] beacon 요청.
