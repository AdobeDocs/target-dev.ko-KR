---
keywords: 구현, 비 Javascript, mbox, adbox
description: ' [!DNL Adobe Target]을(를) 사용하여 오프사이트 구현에서 이미지를 게재하려면 AdBox를 사용하십시오. AdBox는 mbox와 유사하지만 JavaScript 대신 URL로 제어됩니다.'
title: 이미지용 Adbox를 만들려면 어떻게 해야 합니까?
feature: Implement Email
exl-id: ad1eb6c4-7a16-4054-ae76-57971261e931
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 71%

---

# 이미지용 Adbox 만들기

[!DNL Adobe Target]을(를) 사용하여 오프사이트 구현에서 이미지를 게재하려면 AdBox를 사용하십시오.

AdBox는 mbox와 비슷하지만 JavaScript가 아니라 URL로 제어됩니다. AdBox는 &quot;광고&quot; mbox(또는 AdBox)를 자신의 Adobe 계정으로 로드하는 특별한 AdBox URL로 만들어집니다. 이 AdBox를 활동에서 mbox 대신 사용합니다. 이메일 또는 기타 비 자바스크립트 구현에서 직접 이미지 참조 대신 AdBox URL을 사용합니다.

올바른 설정을 선택하는 데 도움이 필요하면 [JavaScript 기반이 아닌 구현](/help/dev/implement/email/overview.md)을 참조하세요.

1. AdBox URL을 만듭니다.

   ```
   https://myClientCode.tt.omtrdc.net/m2/myClientCode/ubox/
   image?mbox=emailHeroImage123_320x200&
   mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fimg%2Flogo%2Egif
   ```

   * 여기서 `myClientCode`는 회사의 클라이언트 코드입니다. 회사의 클라이언트 코드는 모두 소문자이고 특수 문자를 포함하지 않습니다.

     클라이언트 코드는 [!DNL Target] 인터페이스의 **[!UICONTROL Administation]** > **[!UICONTROL Implementation]** 페이지 맨 위에서 사용할 수 있습니다.

   * 여기서 `image`는 호출 유형입니다. 이 경우 이미지입니다.

   * 여기서 `emailHeroImage123_320x200`은 AdBox의 이름입니다.

   * 여기서 `http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fimg%2Flogo%2Egif`는 mbox의 기본 콘텐츠입니다. 이것은 이미지여야 합니다.

     이것은 URL로 인코딩되어야 하고 절대 참조여야 합니다. [HTML URL 인코딩 참조](https://www.w3schools.com/tags/ref_urlencode.asp)를 사용하여 URL을 빠르게 인코딩할 수 있습니다.

1. 각 대체 이미지에 대한 [리디렉션 오퍼](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html)를 만듭니다.

   >[!NOTE]
   >
   >AdBox는 리디렉션 오퍼 또는 기본 컨텐츠 오퍼와 함께 로드되어야 합니다. 다른 오퍼 유형은 작동하지 않습니다. AdBox는 URL이므로 수신하는 URL만 표시할 수 있으며, 따라서 리디렉션 오퍼만 작동합니다.

1. 활동을 만듭니다.

   목표를 충족하는 올바른 설정을 알려면 [비JavaScript 기반 구현](/help/dev/implement/email/overview.md)을 참조하십시오.

1. 활동에 대한 QA를 완료합니다.

   우수 사례로, 더미 페이지를 만들고 모든 경험, 기본 컨텐트 및 보고서가 모든 브라우저 유형에서 모든 환경에 대해 예상대로 작동하는지 확인합니다.

1. 활동을 실행합니다.
