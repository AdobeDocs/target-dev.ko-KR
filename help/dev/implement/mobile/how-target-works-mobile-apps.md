---
description: ' [!DNL Adobe Mobile SDK] 을(를) 사용하여 모바일 앱 방문자에게 최적의 경험을 표시하는 방법에 대해 알아보십시오.'
title: ' [!DNL Target] 은(는) 모바일 앱에서 어떻게 작동합니까?'
feature: Implement Mobile
exl-id: 33001f01-fde6-48cb-ac02-d1a632b2150d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 22%

---

# 모바일 앱에서 [!DNL Target]이(가) 작동하는 방식

[!DNL Adobe Mobile SDK]이(가) [!DNL Target] 서버에 연결하여 사용자에게 올바른 경험을 제공하기 위해 다른 데이터 포인트와 함께 콘텐츠를 가져옵니다.

>[!IMPORTANT]
>
>[!DNL Adobe Mobile] 버전 4를 지원합니다.*x* SDK는 2021년 8월 31일부로 종료되었으며 [!DNL Adobe Target] 모바일 사용자에게는 더 이상 권장되지 않습니다.
>
>[모바일 앱용 Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/){target=_blank}은(는) 모바일 앱에서 [!DNL Adobe Experience Cloud] 솔루션과 서비스를 제공하는 데 권장되는 솔루션입니다.

## [!DNL Target]개 위치 및 성공 지표

*타겟 위치*&#x200B;는 mbox라고도 합니다. 앱에서 식별된 위치는 테스트나 개인화에 사용할 수 있습니다(예: 홈 화면의 환영 메시지). 이러한 위치는 테스트 작성 프로세스 중에 식별됩니다.

*[성공 지표](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html)*&#x200B;은(는) 특정 활동이 성공했는지(서명, 구매, 티켓 예약 등) 여부를 식별하는, 사용자가 수행하는 작업입니다.

![대체 이미지](assets/mobile-target-location.png)

* **[!DNL Target]위치:** 등록 단추 아래에 표시되는 콘텐츠입니다.

  이 특정 사용자는 오후 6시까지 무료 배송을 제공합니다. 이 위치는 A/B 테스트 및 개인화를 실행하기 위해 여러 [!DNL Target] 활동에서 다시 사용할 수 있습니다.

* **성공 지표:** 사용자가 등록 단추를 탭할 때 수행하는 작업입니다.

**SDK에서 [!DNL Target]이(가) 작동하는 방식을 이해합니다**

![대체 이미지](assets/how-target-mobile-works.png)
