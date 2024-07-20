---
keywords: target 구현, 구현, at.js 구현, 태그 관리자, 온디바이스 의사 결정, 디바이스 의사 결정
description: 설정(계정 세부 정보, 구현 방법 등)을 지정하는 방법을 알아봅니다. 태그 관리자를 사용하지 않고  [!DNL Adobe Target] at.js 라이브러리를 구현합니다.
title: 태그 관리자 없이  [!DNL Target] 을(를) 구현할 수 있습니까?
feature: Implement Server-side
exl-id: f675ae21-105d-4aa3-9926-59291f1136b5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 35%

---

# 태그 관리자 없이 [!DNL Target] 구현

태그 관리자 또는 [!DNL Adobe Experience Platform]의 태그를 사용하지 않고 [!DNL Adobe Target]을(를) 구현하는 방법에 대한 정보입니다.

>[!NOTE]
>
>[Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)의 태그는 [!DNL Target] 및 at.js 라이브러리를 구현하는 기본 방법입니다. [!DNL Adobe Experience Platform]의 태그를 사용하여 [!DNL Target]을(를) 구현하는 경우 다음 정보를 적용할 수 없습니다.

구현 페이지에 액세스하려면 **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**&#x200B;을(를) 클릭합니다.

이 페이지에서 다음 설정을 지정할 수 있습니다.

* 계정 세부 정보
* 구현 방법
* 프로필 API
* 디버거 도구
* 개인정보 보호

>[!NOTE]
>
>[!DNL Target] Standard/Premium UI에서 또는 REST API를 사용하여 설정하는 대신 at.js 라이브러리의 설정을 재정의할 수 있습니다. 자세한 내용은 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)를 참조하십시오.

## 계정 세부 정보

다음 계정 세부 사항을 볼 수 있습니다. 이러한 설정은 변경할 수 없습니다.

| 설정 | 설명 |
| --- | --- |
| [!UICONTROL Client Code] | 클라이언트 코드는 [!DNL Target] API를 사용할 때 종종 필요한 클라이언트별 문자 시퀀스입니다. |
| [!UICONTROL IMS Organization ID] | 이 ID는 구현을 Adobe Experience Cloud 계정에 연결합니다. |
| [!UICONTROL On-Device Decisioning] | 디바이스에서 의사 결정을 활성화하려면 토글을 &quot;켜기&quot; 위치로 밉니다.<p>온디바이스 의사 결정을 사용하면 서버에서 A/B 및 경험 타깃팅(XT) 캠페인을 캐시하고 거의 0에 가까운 지연 시간에 메모리 내 의사 결정을 수행할 수 있습니다. 자세한 내용은 [온디바이스 의사 결정 소개](../../../server-side/sdk-guides/on-device-decisioning/overview.md)를 참조하십시오. |
| [!UICONTROL Include all existing on-device decisioning qualified activities in the artifact] | (조건부) 이 옵션은 온디바이스 의사 결정을 활성화하는 경우 표시됩니다.<p>온디바이스 의사 결정에 적합한 모든 라이브 [!DNL Target] 활동을 아티팩트에 자동으로 포함하려면 토글을 &quot;켜짐&quot; 위치로 밉니다.<p>이 토글을 끄면 생성된 규칙 아티팩트에 포함할 온디바이스 의사 결정 활동을 다시 만들고 활성화해야 합니다. |

## 구현 방법

구현 방법 패널에서 다음 설정을 구성할 수 있습니다.

### 전역 설정

>[!NOTE]
>
>이러한 설정은 모든 [!DNL Target] .js 라이브러리에 적용됩니다. 구현 방법 섹션에서 변경을 수행한 후 라이브러리를 다운로드하여 구현에서 업데이트해야 합니다.

| 설정 | 설명 |
| --- | --- |
| [!UICONTROL Page load enabled (Auto-create global mbox)] | 각 페이지 로드 시 자동으로 실행할 at.js 파일에 글로벌 mbox 호출을 포함할지 여부를 선택하십시오. |
| [!UICONTROL Global mbox] | 글로벌 mbox의 이름을 선택하십시오. 기본적으로 이 이름은 target-global-mbox입니다.<p>at.js를 사용하는 mbox 이름에 앰퍼샌드(&amp;)를 포함한 특수 문자를 사용할 수 있습니다. |
| [!UICONTROL Timeout (seconds)] | 정의된 기간 내에 [!DNL Target]이 컨텐츠에 응답하지 않으면 서버 호출 제한 시간이 초과되어 기본 컨텐츠가 표시됩니다. 방문자 세션 동안 추가 호출이 계속 시도됩니다. 기본값은 5초입니다.<p>at.js 라이브러리는 `XMLHttpRequest`의 시간 제한 설정을 사용합니다. 시간 제한은 요청이 실행될 때 시작되며 [!DNL Target]이(가) 서버에서 응답을 받을 때 중지됩니다. 자세한 내용은 Mozilla Developer Network의 [XMLHttpRequest.timeout](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/timeout)을 참조하십시오.<p>응답을 받기 전에 지정된 시간 제한이 초과되면 기본 컨텐츠가 표시되고, 모든 데이터 수집은 [!DNL Target] 에지에서 발생하므로 방문자는 활동의 참가자로 카운트될 수 있습니다. 요청이 [!DNL Target] 에지에 도달하면 방문자가 카운트됩니다.<p>시간 제한 설정을 구성할 때에는 다음 사항을 고려하십시오.<ul><li>값이 너무 낮으면, 방문자가 활동의 참가자로 카운트될 수 있음에도 불구하고 사용자에게 대부분의 시간 동안 기본 컨텐츠가 표시될 수 있습니다.</li><li>값이 너무 높으면, 확장된 기간 동안 본문 숨기기를 사용하는 경우 방문자에게 웹 페이지의 빈 영역이 표시되거나 빈 페이지가 표시될 수 있습니다.</li></ul>mbox 응답 시간을 자세히 알아보려면 브라우저의 개발자 도구에서 네트워크 탭을 살펴보십시오. 타사 웹 성과 모니터링 도구(예: Catchpoint)를 사용할 수도 있습니다.<p>**참고**: [visitorApiTimeout](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#visitorapitimeout) 설정을 사용하면 [!DNL Target]에서 너무 오랫동안 방문자 API 응답을 기다리지 않습니다. 이 설정과 여기에 설명된 at.js에 대한 시간 초과 설정은 서로 영향을 주지 않습니다. |
| [!UICONTROL Profile Lifetime] | 이 설정은 방문자 프로필이 저장되어 있는 기간을 결정합니다. 기본적으로, 프로필은 2주 동안 저장됩니다. 이 설정은 최대 90일까지 늘릴 수 있습니다.<p>프로필 라이프타임 설정을 변경하려면 [Client Care](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html#reference_ACA3391A00EF467B87930A450050077C)에 문의하십시오. |

### 주요 구현 방법

>[!NOTE]
>
>[!DNL Adobe Target]은(는) at.js 1을 모두 지원합니다.*x*&#x200B;와 at.js 2 모두에 있는 Hide Body(본문 숨기기) 및 Show Body(본문 표시) 호출을 보여줍니다.*x*. 지원되는 버전을 실행 중인지 확인하려면 at.js의 주요 버전 중 가장 최근의 업데이트로 업그레이드하십시오.

원하는 at.js 버전을 다운로드하려면 해당 **다운로드** 단추를 클릭하십시오.

at.js 설정을 편집하려면 원하는 at.js 버전 옆의 **[!UICONTROL Edit]**&#x200B;을(를) 클릭합니다.

>[!WARNING]
>
>이러한 기본 설정을 변경하기 전에 [Client Care](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html#reference_ACA3391A00EF467B87930A450050077C)에 문의하여 현재 구현에 영향을 주지 않도록 하십시오.

위에서 설명한 설정 외에도 다음과 같은 특정 at.js 설정을 사용할 수 있습니다.

| 설정 | 설명 |
|--- |--- |
| 도메인 간 | at.js v1의 경우&#x200B;*x*&#x200B;에서 `enabled`(브라우저가 자사 쿠키와 타사 쿠키 모두를 설정)을 선택하여 도메인 간 기능이 `disabled`(브라우저에서 사용자 도메인의 쿠키만 설정), `x only`(브라우저에서 Target의 도메인에서만 쿠키 설정) 또는 둘 다인지 여부를 지정합니다. at.js v2.10 이상 버전의 경우 도메인 간 기능이 `enabled`(브라우저는 퍼스트 파티 쿠키와 타사 쿠키를 모두 설정함)인지 `disabled`(브라우저는 타사 쿠키를 설정하지 않음)인지를 지정합니다. |
| 사용자 정의 라이브러리 헤더 | 라이브러리의 맨 위에 포함할 사용자 지정 JavaScript를 추가하십시오. |
| 사용자 지정 라이브러리 바닥글 | 라이브러리의 맨 아래에 포함할 사용자 지정 JavaScript를 추가하십시오. |

### 프로필 API

API를 통해 묶음 업데이트에 대한 인증을 활성화 또는 비활성화하고 프로필 인증 토큰을 생성합니다.

자세한 내용은 [프로필 API 설정](/help/dev/before-implement/methods-to-get-data-into-target/profile-api-settings.md)을 참조하세요.

### 디버거 도구

고급 [!DNL Target] 디버깅 도구를 사용하려면 인증 토큰을 생성하십시오. **[!UICONTROL Generate New Authentication Token]** 아이콘을 클릭합니다.

![새 인증 토큰 생성](../../../../before-implement/methods-to-get-data-into-target/assets/debugger-auth-token.png)

### 개인정보 보호

이 설정을 사용하면 적용 가능한 데이터 개인 정보 보호 법률에 따라 [!DNL Target]을(를) 사용할 수 있습니다.

방문자 IP 주소 난독화 드롭다운 목록에서 원하는 설정을 선택합니다.

* 마지막 옥텟 난독화
* 전체 IP 난독화
* 없음

자세한 내용은 [개인 정보](/help/dev/before-implement/privacy/privacy.md)를 참조하십시오.

>[!NOTE]
>
>at.js 버전 0.9.3 및 이전 버전에서 레거시 브라우저 지원 옵션을 사용할 수 있습니다. 이 선택 사항은 at.js 버전 0.9.4에서 제거되었습니다. at.js에서 지원하는 브라우저 목록이 필요하면 [지원되는 브라우저](/help/dev/before-implement/supported-browsers.md)를 참조하십시오.<p>이전 브라우저는 CORS(Cross Origin Resource Sharing)를 완전히 지원하지는 않는 오래된 브라우저입니다. 이러한 브라우저에는 버전 11 이전의 Internet Explorer 브라우저와 Safari 버전 6 및 그 이전 버전이 포함됩니다. 이전 브라우저 지원이 비활성화되어 있으면 [!DNL Target]이(가) 이러한 브라우저의 보고서에서 콘텐츠를 전달하거나 방문자 수를 계산하지 않았습니다. 이 옵션이 활성화되면 올바른 고객 경험을 위해 이전 브라우저에서 품질 보증을 수행하는 것이 좋습니다.

## at.js 다운로드

[!DNL Target] 인터페이스 또는 다운로드 API를 사용하여 라이브러리를 다운로드하는 지침.

>[!NOTE]
>
>[Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)은(는) [!DNL Target] 및 at.js 라이브러리를 구현하는 기본 방법입니다. [!DNL Adobe Experience Platform]의 태그를 사용하여 [!DNL Target]을(를) 구현하는 경우 다음 정보를 적용할 수 없습니다.
>
>[!DNL Adobe Target]은(는) at.js 1을 모두 지원합니다.*x*&#x200B;와 at.js 2 모두에 있는 Hide Body(본문 숨기기) 및 Show Body(본문 표시) 호출을 보여줍니다.*x*. 지원되는 버전을 실행 중인지 확인하려면 at.js의 주요 버전 중 가장 최근의 업데이트로 업그레이드하십시오. 각 버전에 대한 자세한 내용은 [at.js 버전 세부 사항](/help/dev/implement/client-side/atjs/target-atjs-versions.md)을 참조하십시오.

### [!DNL Target] 인터페이스를 사용하여 at.js 다운로드

[!DNL Target] 인터페이스에서 at.js를 다운로드하려면 다음을 수행하십시오.

1. **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**&#x200B;을(를) 클릭합니다.
1. 구현 방법 섹션에서 원하는 at.js 버전 옆에 있는 **[!UICONTROL Download]** 단추를 클릭합니다.

### [!DNL Target] 다운로드 API를 사용하여 at.js 다운로드

API를 사용하여 at.js를 다운로드하려면 다음을 수행하십시오.

1. 클라이언트 코드를 가져옵니다.

   클라이언트 코드는 [!DNL Target] 인터페이스의 **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** 페이지 맨 위에서 사용할 수 있습니다.

1. 관리 번호를 가져옵니다.

   다음 URL을 로드하십시오.

   ```
   https://admin.testandtarget.omniture.com/rest/v1/endpoint/<varname>client code</varname>
   ```

   `client code`을(를) 1단계의 클라이언트 코드로 바꿉니다.

   이 URL을 로드한 결과는 다음 예와 유사해야 합니다.

   ```
   { 
     "api": "https://admin6.testandtarget.omniture.com/admin/rest/v1" 
   }
   ```

   이 예에서 &quot;6&quot;은 관리 번호입니다.

1. at.js를 다운로드합니다.

   다음 구조로 이 URL을 로드합니다. 이 URL을 로드하면 사용자 지정된 at.js 파일의 다운로드가 시작됩니다.

   ```
   https://admin<varname>admin number</varname>.testandtarget.omniture.com/admin/rest/v1/libraries/atjs/download?client=<varname>client code</varname>&version=<version number>
   ```

   * `admin number`을(를) 관리자 번호로 바꿉니다.
   * `client code`을(를) 1단계의 클라이언트 코드로 바꿉니다.
   * `version number`을(를) 원하는 at.js 버전 번호(예: 2.2)로 바꾸십시오.

>[!WARNING]
>
>[!DNL Target] 팀에서는 at.js의 현재 버전과 바로 전 버전, 이렇게 두 버전만 유지 관리합니다. 지원되는 버전을 실행 중인지 확인하려면 at.js를 필요에 따라 업그레이드하십시오. 각 버전에 대한 자세한 내용은 [at.js 버전 세부 사항](/help/dev/implement/client-side/atjs/target-atjs-versions.md)을 참조하십시오.

## at.js 구현

at.js는 웹 사이트에 있는 모든 페이지의 `<head>` 요소에 구현되어야 합니다.

[Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)의 태그와 같이 태그 관리자를 사용하지 않는 일반적인 [!DNL Target]의 구현은 다음과 같습니다.

```
<!doctype html> 
<html> 
<head> 
    <meta charset="utf-8"> 
    <title>Title of the Page</title> 
    <!--Preconnect and DNS-Prefetch to improve page load time--> 
    <link rel="preconnect" href="//<client code>.tt.omtrdc.net"> 
    <link rel="dns-prefetch" href="//<client code>.tt.omtrdc.net"> 
    <!--/Preconnect and DNS-Prefetch--> 
    <!--Data Layer to enable rich data collection and targeting--> 
    <script> 
        var digitalData = { 
            "page": { 
                "pageInfo": { 
                    "pageName": "Home" 
                } 
            } 
        }; 
    </script> 
    <!--/Data Layer--> 
    <!-- targetPageParams(), targetPageParamsAll(), Data Providers or targetGlobalSettings() functions to enrich the visitor profile or modify the library settings--> 
    <script> 
        targetPageParams = function() { 
            return { 
                "a": 1, 
                "b": 2, 
                "pageName": digitalData.page.pageInfo.pageName, 
                "profile": { 
                    "age": 26, 
                    "country": { 
                        "city": "San Francisco" 
                    } 
                } 
            }; 
        }; 
    </script> 
    <!--/targetPageParams()--> 
 
    <!--jQuery or other helper libraries should be implemented before at.js if you would like to use their methods in Target--> 
    <script src="jquery-3.3.1.min.js"></script> 
    <!--/jQuery--> 
    <!--Target's JavaScript SDK, at.js--> 
    <script src="at.js"></script> 
    <!--/at.js--> 
</head>
<body> 
    The default content of the page 
</body> 
</html>
```

다음 중요 참고 사항을 고려하십시오.

* HTML5 문서 형식(예: `<!doctype html>`)을 사용해야 합니다. 지원되지 않거나 오래된 doctype으로 인해 [!DNL Target]에서 요청할 수 없습니다.
* 사전 연결 및 미리 가져오기는 웹 페이지 로드 속도를 높일 수 있는 옵션입니다. 이러한 구성을 사용하는 경우 `<client code>`을(를) 고유한 클라이언트 코드로 바꾸십시오. 클라이언트 코드는 **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** 페이지에서 가져올 수 있습니다.
* 데이터 계층이 있는 경우 at.js가 로드되기 전에 페이지의 `<head>`에 가능한 많은 항목을 정의하는 것이 최적입니다. 이 배치는 [!DNL Target]에서 개인화를 위해 이 정보를 사용할 수 있는 최대 기능을 제공합니다.
* `targetPageParams()`, `targetPageParamsAll()`, Data Providers, `targetGlobalSettings()`과(와) 같은 특수 [!DNL Target] 함수는 데이터 계층 뒤, at.js가 로드되기 전에 정의해야 합니다. 또는 이러한 함수를 at.js 설정 편집 페이지의 라이브러리 헤더 섹션에 저장하고 at.js 라이브러리 자체의 일부로 저장할 수 있습니다. 이러한 함수에 대한 자세한 내용은 [at.js 함수](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md)를 참조하십시오.
* jQuery와 같은 JavaScript 도우미 라이브러리를 사용하는 경우 [!DNL Target] 경험을 작성할 때 해당 구문과 메서드를 사용할 수 있도록 [!DNL Target] 앞에 포함하십시오.
* 페이지의 `<head>`에 at.js를 포함합니다.

## 전환 추적

주문 확인 mbox는 사이트의 주문에 대한 세부 사항을 기록하고 매출 및 주문을 기준으로 보고할 수 있도록 합니다. 또한 주문 확인 mbox는 &quot;제품 x를 구입한 사람이 제품 y도 구입함&quot;과 같은 권장 사항 알고리즘을 유도할 수도 있습니다.

>[!NOTE]
>
>사용자가 웹 사이트에서 구매를 수행하는 경우, 보고를 위해 Analytics for [!DNL Target](A4T)을 사용하더라도 Adobe은 주문 확인 mbox를 구현하는 것을 권장합니다.

1. 주문 상세 정보 페이지에서 아래의 모델에 따라 mbox 스크립트를 삽입합니다.
1. WORDS IN CAPITAL LETTERS를 카탈로그의 동적 또는 정적 값과 교체합니다.

   >[!TIP]
   >
   >mbox에 주문 정보를 전달할 수도 있습니다(`orderConfirmPage`(으)로 이름을 지정할 필요가 없음). 주문 정보를 동일한 캠페인 내의 여러 mbox에 전달할 수도 있습니다.

   ```
   <script type="text/javascript"> 
   adobe.target.trackEvent({ 
       "mbox": "orderConfirmPage", 
       "params":{  
           "orderId": "ORDER ID FROM YOUR ORDER PAGE",  
           "orderTotal": "ORDER TOTAL FROM YOUR ORDER PAGE",  
           "productPurchasedId": "PRODUCT ID FROM YOUR ORDER PAGE, PRODUCT ID2, PRODUCT ID3"  
       } 
   }); 
   </script> 
   ```

>[!NOTE]
>
>주문 확인 mbox에서 쉼표를 사용하여 여러 제품 ID를 구분합니다.

주문 확인 mbox에서는 다음 매개 변수를 사용합니다.

| 매개 변수 | 설명 |
|--- |--- |
| orderId | 전환 계산을 위해 주문을 식별하는 고유한 값<p>`orderId`은(는) 고유해야 합니다. 보고서에서 중복 주문은 무시됩니다. |
| orderTotal | 구매품의 통화 가치<p>통화 기호를 전달하지 마십시오. 소수점(쉼표 아님)을 사용하여 십진수 값을 표시합니다. |
| productPurchasedId(선택 사항) | 주문에서 구입한 제품 ID가 쉼표로 구분된 목록<p>이러한 제품 ID는 추가 보고 분석을 지원하기 위해 감사 보고서에 표시됩니다. |
