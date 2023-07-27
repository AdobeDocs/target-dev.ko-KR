---
keywords: 모바일 앱, 모바일 앱 SDK, target 모바일 앱, 모바일 target sdk, 모바일 앱 SDK, SDK에서 Target 사용
description: 모바일 앱에 Adobe Mobile Services SDK를 추가하는 방법을 알아봅니다.
title: 활성화 방법 [!DNL Target] 다음에서 [!DNL Adobe Mobile SDK]?
feature: Implement Mobile
exl-id: 4263b96a-23c8-4513-8302-00080122181d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 49%

---

# 사용 [!DNL Target] SDK에서

추가 [!UICONTROL Adobe Mobile Services SDK] 앱에 연결합니다.

>[!IMPORTANT]
>
>지원 [!DNL Adobe Mobile] 버전 4.*x* SDK는 2021년 8월 31일부로 종료되었으며 더 이상 다음에 대해 권장되지 않습니다. [!DNL Adobe Target] 모바일 사용자.
>
>다음 [모바일 앱용 Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/){target=_blank} 는 권장되는 전원 공급 솔루션입니다 [!DNL Adobe Experience Cloud] 모바일 앱의 솔루션 및 서비스.

1. 앱에 Adobe Mobile Services SDK를 설치하지 않은 경우 Analytics 또는 Experience Cloud 자격 증명을 사용하고 [Adobe Mobile Services](https://mobilemarketing.adobe.com/) 웹 사이트에서 SDK를 다운로드합니다.

1. 추가 [!DNL Adobe Mobile Services SDK] 앱에 연결합니다.

   [핵심 구현 및 라이프사이클](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/dev-qs.html)에서 지침을 찾을 수 있습니다.

1.  클라이언트 코드, 시간 제한을 추가하고, SSL을 활성화합니다. 

   Experience Cloud에서 Mobile Services를 열고 **[!UICONTROL 앱 설정 관리]** > **[!UICONTROL SDK Target 옵션]**&#x200B;으로 이동합니다.

   사용자 추가 [!DNL Target] clientcode 및 timeout. 클라이언트 코드는 계정 또는 회사에 고유합니다. 시간 제한은 다음 시간까지의 시간(초)입니다. [!DNL Target] 는 기본 콘텐츠를 표시하기 전에 응답을 기다립니다. Adobe Mobile Services의 앱 설정 관리 페이지에서 **[!UICONTROL HTTPS 사용]** 옵션이 선택되어 있는지 확인합니다. HTTPS가 활성화되어 있지 않을 경우 허용 목록에 추가하다를 활성화하지 않으면 iOS+의 모든 호출이 차단됩니다. [!DNL Target] 서버입니다.

   ![대체 이미지](assets/mobile-clientcode.png)

1. 앱을 만들었거나 찾은 후에 앱 설정을 찾고 원하는 SDK를 다운로드합니다.

   ![대체 이미지](assets/download-sdk.png)

>[!WARNING]
>
> 모바일 마케팅 인터페이스에 액세스할 수 없는 경우 앱 코드의 구성 파일에서 직접 변경할 수 있습니다. 그러나 변경 사항이 사용자 인터페이스의 설정 페이지와 동기화되지 않습니다.
