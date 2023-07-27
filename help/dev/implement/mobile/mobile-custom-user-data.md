---
keywords: 모바일 앱, 모바일 앱 데이터 전송, target 모바일 앱, 모바일 사용자 지정 사용자 데이터, 모바일 앱 사용자 지정 데이터
description: 위치 또는 사용자에 대한 추가 정보를 (으)로 전송하는 방법에 대해 알아봅니다. [!DNL Adobe Target] 를 이름-값 쌍으로 사용하여 사용자 지정 대상을 작성할 수 있습니다.
title: iOS 앱에서 사용자 지정 사용자 데이터를 보내려면 어떻게 해야 합니까?
feature: Implement Mobile
exl-id: 9cf8e8fd-1898-43b1-b339-d7a21cb35d57
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 55%

---

# iOS - 사용자 지정 사용자 데이터 전송

위치 또는 사용자에 대한 추가 정보를 다음으로 보낼 수 있습니다. [!DNL Target] 이름-값 쌍으로 사용됩니다.

>[!IMPORTANT]
>
>지원 [!DNL Adobe Mobile] 버전 4.*x* SDK는 2021년 8월 31일부로 종료되었으며 더 이상 다음에 대해 권장되지 않습니다. [!DNL Adobe Target] 모바일 사용자.
>
>다음 [모바일 앱용 Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/){target=_blank} 는 권장되는 전원 공급 솔루션입니다 [!DNL Adobe Experience Cloud] 모바일 앱의 솔루션 및 서비스.

이 정보는 사용자 지정 대상(예: 25,000마일 이상 떨어진 사용자) 작성 및 보고 작업에 사용할 수 있습니다.

를 사용하여 보낼 수 있는 두 가지 유형의 매개 변수가 있습니다 [!DNL Target] 호출:

* **mbox 매개 변수**: Mbox 매개 변수는 세션 간에 지속되지 않습니다.
* **프로필 매개 변수**: 프로필 매개 변수는 방문자 프로필 저장소에 저장되며 세션 간에 지속됩니다. mbox 매개 변수는 지속되지 않습니다. 일부 키가 예약되어 있지만, 프로필 및 mbox 매개 변수 둘 다 사용자 지정 키-값 쌍으로 지정할 수 있습니다.

일부 예약된 키가 있지만 프로필 및 mbox 매개 변수 둘 다 사용자 지정 키-값 쌍을 포함할 수 있습니다.

1. 사전을 만듭니다.

   먼저 전달할 값으로 사전을 만듭니다. [!DNL Target]. 편의를 위해 `welcomeMessageCampaign` 메서드 내에 사전을 추가하면 범위에 대해 걱정할 필요가 없습니다.

   다음은 샘플 사전입니다. 복사한 후 `(void)welcomeMessageCampaign` 내부에 붙여넣을 수 있습니다. `userLevel` 및 `userMiles`와 같은 키의 값은 이 예에서 하드 코딩됩니다. 일반적으로 사용자가 해당 변수를 제공합니다.

   ```
   NSDictionary *targetParams = [[NSDictionary alloc] initWithObjectsAndKeys: 
                                 @"platinum",@"userLevel", 
                                 @26500,@"userMiles", 
                                 @"1067007",@"entity.id", 
                                 @"dealsapp.qa", @"host", 
                                 @"fashion",@"entity.categoryId", 
                                 @"millenial", @"profile.persona", 
                                 @"cohort_5", @"profile.cohort", 
                                 nil];
   ```

   * 접두어 프로필(예: `profile.persona`)이 있는 키는 사용자 프로필에 저장됩니다.

     이러한 프로필 속성은 여러 활동 및 채널에서 사용할 수 있습니다.

   * 접두사가 없는 키(예: `userMiles`)는 mbox 매개 변수입니다.

     이러한 매개 변수는 세션 중에만 사용 가능합니다.

   * 접두부 엔티티가 있는 키(예: `entity.category.id`)는 제품 권장 사항에 사용됩니다.

1. 데이터를 확인합니다.
   1. 애플리케이션 `didFinishLaunchingWithOptions`에서 주석 처리를 해제하거나 `[ADBMobile setDebugLogging:YES];`를 추가합니다.

      이렇게 하면 자세한 디버그 로그가 인쇄됩니다.
   1. 앱을 빌드합니다.
   1. 매개 변수가 대상 호출에 전달되었는지 확인합니다.

      디버그 콘솔에서 목표 위치 이름을 검색합니다. 방금 전달한 모든 매개 변수를 사용한 `YOUR-CLIENT-CODE.tt.omtrdc.net`에 대한 호출이 표시됩니다.

      이미지 를 클릭하여 전체 너비로 확장합니다.

      ![디버그 콘솔의 Target 위치](/help/dev/implement/mobile/assets/mobile-debug.png "디버그 콘솔의 Target 위치"){zoomable=&quot;yes&quot;}

   에서 이러한 매개 변수를 사용하여 대상을 작성하고 컨텐츠 표시를 제한하거나 타깃팅할 수 있습니다 [!DNL Target].
