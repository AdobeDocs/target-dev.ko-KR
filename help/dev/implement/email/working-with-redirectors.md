---
keywords: 구현, mbox.js 비Javascript, 리디렉터, 클릭당 비용, 클릭당 수익
description: ' [!DNL Adobe Target] 활동에서 mbox를 사용하는 방법과 유사하게, 전자 메일 구현에서 리디렉터를 사용하는 방법을 알아봅니다.'
title: 리디렉터는 어떻게 작동합니까?
feature: Implement Email
exl-id: 072368ff-9f17-4709-ac2d-c9e1f0d888bb
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 64%

---

# 리디렉터 작업

리디렉터는 테스트에서 mbox를 사용하는 것과 비슷한 방법으로 사용됩니다.

리디렉터는 계정에 리디렉터 mbox(리디렉터)를 로드하는 특수 리디렉터 URL을 사용하여 만듭니다. 이 리디렉터는 테스트에서 mbox를 사용하는 것과 비슷한 방법으로 사용됩니다. 리디렉터 URL을 광고의 대상 링크로 광고 네트워크에 제출하십시오.

리디렉터를 사용하여 다음을 수행합니다.

* 디스플레이 광고에서 사이트로의 클릭 수 추적
* 단일 중앙 집중식 보고서를 만들어 여러 광고 네트워크의 디스플레이 광고에 대한 클릭 수 추적
* 디스플레이 광고 대상을 다양하게 지정

  예를 들어 홈 페이지, 카테고리 페이지 및 제품 페이지에 동일한 배너가 랜딩됩니다.

* 가장 많은 전환을 생성하는 랜딩 페이지 찾기

올바른 설정을 결정하는 데 도움이 필요하면 [JavaScript 기반이 아닌 구현](/help/dev/implement/email/overview.md)을 참조하세요.

## 리디렉터 만들기

리디렉터를 사용하기 전에 먼저 리디렉터를 만들어야 합니다.

1. 기본 대상을 포함하여 광고의 대상 변형을 결정합니다.
1. 리디렉터 URL을 만듭니다.

   ```
   https://<your_testandtarget_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox
   /​page?mbox=redirectorlink_456
   &mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fusualdestination%2Ehtm
   ```

   * 여기서 `yourclientcode`는 회사의 클라이언트 코드입니다. 회사의 클라이언트 코드는 모두 소문자이고 특수 문자를 포함하지 않습니다.

     클라이언트 코드는 [!DNL Target] 인터페이스의 **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** 페이지 맨 위에서 사용할 수 있습니다.

   * `redirectorlink_456` 은 캠페인 및 테스트에서 사용할 계정에 나타나는 리디렉터 mbox의 이름입니다.

     리디렉터는 다른 mbox와 다르게 작동하지만 계정에서는 다른 mbox처럼 나타납니다. 계정에서 표준 유형 mbox와 쉽게 구분되도록 리디렉터 이름을 지정하십시오.  우수 사례로, mbox 이름을 &#39;redirectorlink&#39;로 시작하십시오.

   * 여기서 `http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fusualdestination%2Ehtm`은 기본 대상입니다.

     이것은 URL로 인코딩되어야 하고 절대 참조여야 합니다. [HTML URL 인코딩 참조](https://www.w3schools.com/tags/ref_urlencode.asp)를 사용하여 URL을 빠르게 인코딩할 수 있습니다.

   >[!WARNING]
   >
   >리디렉터를 사용하면 오픈 리디렉션 취약점의 위험에 노출될 수 있습니다. 타사에서 리디렉터 링크를 무단으로 사용하지 않도록 하려면 Adobe허용 목록에 추가하다 에서 &quot;승인된 호스트&quot;를 사용하여 기본 리디렉션 URL 도메인을 리디렉션하는 것이 좋습니다. [!DNL Target]은(는) 리디렉션을 허용할 호스트 허용 목록에 추가하다 도메인을 사용합니다. 자세한 내용은 *호스트*&#x200B;에서  [!DNL Target][&#128279;](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=ko#allowlist)(으)로 mbox 호출을 보내도록 승인된 호스트를 지정하는 허용 목록 만들기를 참조하십시오.

1. 리디렉터의 유효성을 확인합니다.
   1. *보안 모범 사례*: 리디렉터에서 사용되는 도메인이 위에 표시된 대로 허용 목록에추가된인지 확인하십시오. 허용 목록에추가된이 아닌 도메인을 사용하는 경우 Adobe은 해당 도메인에 대한 모든 호출을 차단하여 악의적인 행위자가 리디렉터를 사용하여 악의적인 도메인으로 리디렉션하지 못하도록 합니다.
   2. 리디렉터 URL을 브라우저에 삽입하고 새로 고칩니다.
   3. 계정에 로그인하고 mbox 목록을 새로 고친 후 새 리디렉터가 mbox로 나열되는지 확인합니다.
1. 하나의 광고에 대해 서로 다른 대상을 테스트할 경우 각 버전에 대해 [리디렉션 오퍼](https://experienceleague.adobe.com/docs/target/using/experiences/vec/redirect-offer.html?lang=ko)를 만듭니다.
1. 캠페인을 만듭니다.

   목표를 충족하는 올바른 설정을 알려면 [비JavaScript 기반 구현](/help/dev/implement/email/overview.md)을 참조하십시오.
1. 캠페인에 대한 QA를 완료합니다.

   리디렉터 URL이 포함된 `<a href>`를 사용하여 더미 페이지를 만듭니다. 예:

   ```
   <a href=https://<your_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox/​page?mbox=
   
   redirectorlink_456&mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2F​usualdestination%2Ehtm>
   ```

1. 모든 경험, 기본 컨텐츠 및 보고서가 모든 브라우저 유형에서 모든 환경에 대해 예상대로 작동하는지 확인합니다.

   >[!NOTE]
   >
   >리디렉터는 mbox의 오퍼 미리 보기 또는 찾아보기에서 지원되지 않습니다. 브라우저에서 직접 경험을 미리 봅니다. 또한 `mboxDebug`은(는) 리디렉터에서 작동하지 않습니다.

1. 전체 리디렉터 URL을 광고 대상으로 디스플레이 광고 네트워크에 제출합니다.

## 리디렉터를 사용하여 클릭당 비용 및 클릭당 매출 전달

리디렉터를 사용하여 클릭당 비용과 클릭당 수익을 전달하는 방법에 대한 정보입니다.

### 클릭당 비용 전달

리디렉터를 사용하여 클릭당 비용을 전달합니다.

>[!NOTE]
>
>가장 좋은 방법은 **[!UICONTROL Score per visit]** 참여 지표를 사용하여 비용 값을 결정하는 것입니다.

`&mboxPageValue=-value`를 URL에 추가합니다. 음수입니다.

예: 클릭당 0.1센트 비용의 경우

```
https://<your_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox/​page?mbox=redirectorlink_456
&mboxPageValue=-0.1&mboxDefault=​https://www.yourcompany.com/usualdestination.htm
```

### 클릭당 수익 전달

리디렉터를 사용하여 클릭당 매출을 전달합니다.

>[!NOTE]
>
>가장 좋은 방법은 **[!UICONTROL Score per visit]** 참여 지표를 사용하여 매출액 값을 결정하는 것입니다.

`&mboxPageValue=value`를 URL에 추가합니다.

예: 클릭당 0.1센트 매출액의 경우

```
https://<​your_clientcode>​​​​.tt​​.omtrdc​.net/​​m2/​yourclientcode/​ubox/​​​page?mbox=redirectorlink_456
&mboxPageValue=0.1​&mbox​Default=​​http%3A%2F%2Fwww%2E​yourcompany%2Ecom​%2Fusualdestination%2Ehtm
```
