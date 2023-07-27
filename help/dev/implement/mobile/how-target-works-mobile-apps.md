---
description: 사용 방법 알아보기 [!DNL Adobe Mobile SDK] 모바일 앱 방문자에게 최적의 경험을 보여 줍니다.
title: 은 어떻게 합니까? [!DNL Target] 모바일 앱에서 작업?
feature: Implement Mobile
exl-id: 33001f01-fde6-48cb-ac02-d1a632b2150d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 34%

---

# 방법 [!DNL Target] 모바일 앱에서 작동

다음 [!DNL Adobe Mobile SDK] 에 문의 [!DNL Target] 사용자에게 올바른 경험을 보여주기 위해 다른 데이터 포인트와 함께 콘텐츠를 가져오는 서버입니다.

>[!IMPORTANT]
>
>지원 [!DNL Adobe Mobile] 버전 4.*x* SDK는 2021년 8월 31일부로 종료되었으며 더 이상 다음에 대해 권장되지 않습니다. [!DNL Adobe Target] 모바일 사용자.
>
>다음 [모바일 앱용 Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/){target=_blank} 는 권장되는 전원 공급 솔루션입니다 [!DNL Adobe Experience Cloud] 모바일 앱의 솔루션 및 서비스.

## [!DNL Target] 위치 및 성공 지표

*타겟 위치*&#x200B;는 mbox라고도 합니다. 앱에서 식별된 위치는 테스트나 개인화에 사용할 수 있습니다(예: 홈 화면의 환영 메시지). 이러한 위치는 테스트 작성 프로세스 중에 식별됩니다.

A *[성공 지표](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html)*&#x200B;는 특정 활동이 성공했는지(서명, 구매, 티켓 예약 등) 여부를 식별하는, 사용자가 수행하는 작업입니다.

![대체 이미지](assets/mobile-target-location.png)

* **[!DNL Target]위치:** 등록 단추 아래에 표시되는 컨텐츠입니다.

  이 특정 사용자는 오후 6시까지 무료 배송을 제공합니다. 이 위치는 여러 곳에서 재사용할 수 있습니다. [!DNL Target] A/B 테스트 및 개인화를 실행하는 활동.

* **성공 지표:** 사용자가 등록 버튼을 탭하는 경우 사용자가 수행하는 작업입니다.

**방법 이해 [!DNL Target] sdk에서 작동**

![대체 이미지](assets/how-target-mobile-works.png)
