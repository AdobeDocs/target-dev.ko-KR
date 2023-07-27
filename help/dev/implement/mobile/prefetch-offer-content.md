---
keywords: offer, 프리페치, iOS, android, sdk, mobile, mobile sdk, $8
description: 사용 [!DNL Adobe Target] 서버 응답을 캐시하여 가능한 한 적은 시간에 오퍼 컨텐츠를 가져오도록 iOS 및 Android Mobile SDK의 미리 가져오기 기능.
title: 모바일 앱용 오퍼 컨텐츠를 미리 가져올 수 있습니까?
feature: Implement Mobile
exl-id: 6f8e8298-f1e9-46f0-828f-717c7d632077
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 39%

---

# 오퍼 콘텐츠 미리 가져오기

[!DNL Target] 미리 가져오기 기능은 iOS 및 Android Mobile SDK를 사용하여 서버 응답을 캐시하여 가능한 한 적은 시간에 오퍼 컨텐츠를 가져옵니다.

>[!IMPORTANT]
>
>지원 [!DNL Adobe Mobile] 버전 4.*x* SDK는 2021년 8월 31일부로 종료되었으며 더 이상 다음에 대해 권장되지 않습니다. [!DNL Adobe Target] 모바일 사용자.
>
>다음 [모바일 앱용 Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/){target=_blank} 는 권장되는 전원 공급 솔루션입니다 [!DNL Adobe Experience Cloud] 모바일 앱의 솔루션 및 서비스.

이 프로세스는 로드 시간을 줄이고, 다중 네트워크 호출을 방지하며, 모바일 앱 사용자가 방문한 mbox를 [!DNL Target]에 알려줄 수 있도록 해줍니다. 모든 콘텐츠는 미리 가져오기 호출 중에 검색되고 캐시되며, 이 콘텐츠는 지정된 mbox 이름에 대해 캐시된 콘텐츠를 포함하는 이후의 모든 호출에 대한 캐시에서 검색됩니다.

iOS 및 Android Mobile SDK에서 미리 가져오기 방법을 사용할 때는 다음 제한 사항을 고려하십시오.

* 미리 가져오기 콘텐츠는 실행 간에는 지속되지 않으며, 애플리케이션이 상주하는 동안 또는 `clearPrefetchCache()` 메서드가 호출될 때까지 캐시됩니다.
* 미리 가져오기 기능은 다음에 대해 지원되지 않습니다. [!UICONTROL 자동 할당] 및 [!UICONTROL 자동 Target] 트래픽 할당 방법, 대상 [!UICONTROL Automated Personalization] 또는 [!UICONTROL Recommendations] 활동 유형 또는 [A/B 또는 XT 활동 내 권장 사항 오퍼](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-as-an-offer.html).

미리 가져오기 방법, 공용 클래스 및 코드 샘플을 포함한 자세한 내용은 다음을 참조하십시오.

* **iOS:**  [iOS에서 오퍼 컨텐츠 미리 가져오기](https://experienceleague.adobe.com/docs/mobile-services/ios/target-ios/c-mob-target-prefetch-ios.html) 다음에서 *Mobile Services iOS SDK 도움말*.
* **Android:**  [Android에서 오퍼 컨텐츠 미리 가져오기](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html) 다음에서 *Mobile Services Android SDK 도움말*.
