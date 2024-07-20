---
keywords: qa, 미리 보기, 미리 보기 링크, 모바일, 모바일 미리 보기
description: 모바일 미리 보기 링크를 사용하여 모바일 앱 활동에 대한 엔드 투 엔드 QA를 수행합니다.
title: ' [!DNL Adobe Target] Mobile에서 모바일 미리 보기 링크를 사용하는 방법은 무엇입니까?'
feature: Implement Mobile
exl-id: c0c4237a-de1f-4231-b085-f8f1e96afc13
source-git-commit: 15e42d0fb049f9243ff5468ff5f22a8e79c55c79
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 23%

---

# [!DNL Target] 모바일 미리 보기

모바일 미리 보기 링크를 사용하여 모바일 앱 활동에 대한 간단한 종단 간 QA를 수행하고 특별한 테스트 장치 없이 장치를 사용하여 다양한 경험에 등록할 수 있습니다.

모바일 미리 보기 기능을 사용하면 모바일 앱 활동을 라이브로 시작하기 전에 완전히 테스트할 수 있습니다.

## 전제 조건

1. **지원되는 SDK 버전 사용:** 모바일 미리 보기 기능을 사용하려면 해당 앱에서 해당 버전의 [!DNL Adobe Mobile SDK]을(를) 다운로드하여 설치해야 합니다.

   적절한 SDK를 다운로드하는 방법은 *[!DNL Adobe Experience Platform Mobile SDK]* 설명서의 [현재 SDK 버전](https://developer.adobe.com/client-sdks/documentation/current-sdk-versions/){target=_blank}을 참조하십시오.

1. **URL 체계 설정:** 미리 보기 링크는 URL 체계를 사용하여 앱을 엽니다. 미리 보기에 대한 고유한 URL 체계를 지정합니다.

   자세한 내용은 *[!DNL Mobile SDK]* 설명서의 *데이터 연결 UI에서 Target 확장 구성*&#x200B;에서 [시각적 미리 보기](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank}를 참조하십시오.

   다음 링크에는 추가 정보가 포함되어 있습니다.

   * **iOs**: iOS의 URL 체계 설정에 대한 자세한 내용은 *Apple 개발자* 웹 사이트에서 [앱에 대한 사용자 지정 URL 체계 정의](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target=_blank}를 참조하십시오.
   * **Android**: Android의 URL 체계 설정에 대한 자세한 내용은 *Android 개발자* 웹 사이트에서 [앱 콘텐츠에 대한 딥링크 만들기](https://developer.android.com/training/app-links/deep-linking){target=_blank}를 참조하십시오.

1. **`collectLaunchInfo` API 설정(i0S만 해당)**

   자세한 내용은 *[!DNL Mobile SDK]* 설명서의 *데이터 연결 UI에서 Target 확장 구성*&#x200B;에서 [시각적 미리 보기](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank}를 참조하십시오.

## 미리 보기 링크 생성

1. [!DNL Target] UI에서 **[!UICONTROL More Options]** 아이콘(세로 줄임표)을 클릭한 다음 **[!UICONTROL Create Mobile Preview Link]**&#x200B;을(를) 선택합니다.

   ![대체 이미지](assets/mobile-preview-create.png)

1. 미리 보려는 활동을 선택한 다음 **[!UICONTROL Generate Mobile Preview Link]**&#x200B;을(를) 클릭합니다.

   >[!NOTE]
   >
   >양식 기반 [!UICONTROL A/B Test] 및 [!UICONTROL Experience Targeting](XT) 활동만 선택할 수 있습니다.

   ![대체 이미지](assets/mobile-preview-select-activities.png)

1. 앱의 URL 체계를 지정합니다.

   URL 체계는 iOS 또는 Android 앱에 있는 것과 동일해야 합니다. 필요한 경우 iOS 및 Android에 대해 이 프로세스를 별도로 반복합니다.

   ![대체 이미지](assets/mobile-preview-enter-url-scheme.png)

1. **[!UICONTROL Generate Mobile Preview Link]**&#x200B;을(를) 클릭한 다음 링크를 복사합니다.

   ![대체 이미지](assets/mobile-preview-generate-and-copy.png)

## 장치에서 미리 보기

앱이 설치된 장치의 모바일 브라우저에서 링크를 엽니다. 이 앱은 [!DNL Apple App Store] 또는 [!DNL Google Play Store]에서 다운로드한 프로덕션 앱일 수 있습니다. 앱이 특수 빌드일 필요는 없습니다. 활성 미리 보기 링크가 있는 경우 장치에서 경험을 볼 수 있습니다.

1. 모바일 브라우저에서 링크를 엽니다.

   이전 섹션에서 복사한 링크를 [!DNL Target] UI에서 모바일 장치로 편리하게 공유할 수 있습니다(예: 텍스트, 이메일 또는 [!DNL Slack] 사용).

   |![딥 링크 1 미리 보기](assets/mobile-preview-open-deeplink.png)|![딥 링크 2 미리 보기](assets/mobile-preview-open-app.png)|

   앱이 열리고 [!DNL Target] [!UICONTROL Mobile Preview Mode]이(가) 시작됩니다.

1. 표시할 경험의 조합을 선택한 다음 **[!UICONTROL Launch Experiences]**&#x200B;을(를) 클릭합니다.

   |![모바일 미리 보기 1](assets/mobile-preview-experience-selection-1.png)|![모바일 미리 보기 2](assets/mobile-preview-experience-result-1-france.png)|![모바일 미리 보기 3](assets/mobile-preview-experience-result-1-shipfree.png)|
|![모바일 미리 보기 4](assets/mobile-preview-experience-selection-2.png)|![모바일 미리 보기 5](assets/mobile-preview-experience-result-2-aus.png)|![모바일 미리 보기 6](assets/mobile-preview-experience-result-2-10off.png)|

## 제한

* **[!UICONTROL Launch Experiences]** 단추를 클릭한 후 새 콘텐츠를 표시하려면 보기를 다시 로드해야 합니다. 가장 쉬운 방법은 다른 화면으로 전환한 다음, 변경이 발생할 것으로 예상되는 화면으로 돌아가는 것입니다.
* API-19(KitKat) 이전의 Android 버전에서는 모바일 미리 보기가 지원되지 않습니다.
