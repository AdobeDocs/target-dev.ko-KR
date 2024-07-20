---
keywords: at.js 릴리스, at.js 버전, 단일 페이지 앱, spa, 교차 도메인, 교차 도메인
description: ' [!DNL Adobe Target] at.js 1.x에서 at.js 2.x로 업그레이드하는 방법에 대해 알아보십시오. 시스템 흐름 다이어그램을 검사하고, 새로운 함수 및 더 이상 사용되지 않는 함수에 대해 알아봅니다.'
title: at.js 버전 1.x에서 버전 2.x로 업그레이드하는 방법은 무엇입니까?
feature: at.js
exl-id: fbfa5743-0fa5-44c6-89b3-fdee9b50e126
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '2939'
ht-degree: 61%

---

# at.js 1에서 업그레이드at.js 2에 대한 *x*.*x*

[!DNL Adobe Target]의 최신 at.js 버전에서는 차세대 클라이언트측 기술에 대한 개인화를 실행하도록 기업을 지원하는 다양한 기능을 제공합니다. 이 새로운 버전은 단일 페이지 애플리케이션(SPA)과 조화로운 상호 작용을 하도록 at.js를 업그레이드하는 데 주력하고 있습니다.

at.js 2.이전 버전에서 사용할 수 없는 *x*:

* 페이지 로드 시 모든 오퍼를 캐시하여 여러 서버 호출을 하나의 서버 호출로 줄일 수 있습니다.
* 오퍼가 기존 서버 호출로 인해 초래되는 지연 없이 캐시를 통해 즉시 표시되므로 사이트에서 최종 사용자의 경험을 크게 향상시킬 수 있습니다.
* 간단한 1줄의 코드 및 일회용 개발자 설정으로 마케터가 SPA에서 VEC를 통해 [!UICONTROL A/B Test] 및 [!UICONTROL Experience Targeting](XT) 활동을 만들고 실행할 수 있도록 할 수 있습니다.

## at.js 2.*x 시스템 다이어그램*

다음 다이어그램은 at.js 2의 워크플로우를 이해하는 데 도움이 됩니다.보기가 있는 *x* 및 이를 통해 SPA 통합이 어떻게 향상되었는지 알아봅니다. at.js 2에서 사용되는 개념의 도입을 보다 잘 이해하려면 다음을 수행하십시오.*x*, [단일 페이지 응용 프로그램 구현](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)을 참조하세요.

이미지 를 클릭하여 전체 너비로 확장합니다.

![at.js 2.x가 있는 Target 흐름](/help/dev/implement/client-side/assets/system-diagram-atjs-20.png "at.js 2.x가 있는 Target 흐름"){zoomable="yes"}

| 호출 | 세부 사항 |
| --- | --- |
| 1 | 사용자가 인증되면 호출에서 [!UICONTROL Experience Cloud ID]를 반환합니다. 다른 호출은 고객 ID를 동기화합니다. |
| 2 | at.js 라이브러리는 동기식으로 로드되며 문서 본문을 숨깁니다.<P>at.js는 페이지에 구현된 코드 조각을 미리 숨기는 선택 사항을 사용하여 비동기식으로 로드할 수도 있습니다. |
| 3 | 모든 구성된 매개변수(MCID, SDID 및 고객 ID)를 포함하는 페이지 로드 요청이 이루어집니다. |
| 4 | 프로필 스크립트가 실행된 다음 프로필 저장소에 반영됩니다. 저장소는 대상 라이브러리의 적절한 대상(예: [!DNL Adobe Analytics], [!DNL Audience Manager]에서 공유되는 대상 등)을 요청합니다.<P>고객 속성은 묶음 프로세스를 통해 프로필 저장소로 전송됩니다. |
| 5 | [!DNL Target]에서는 URL 요청 매개변수 및 프로필 데이터를 기반으로 현재 페이지 및 미래 보기를 위해 방문자에게 반환할 활동 및 경험을 결정합니다. |
| 6 | 타기팅된 콘텐츠는 다시 페이지로 전송되며, 원할 경우 추가적인 개인화를 위한 프로필 값을 포함할 수 있습니다.<P>현재 페이지의 타깃팅된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다.<P>`triggerView()`을(를) 통해 보기를 트리거할 때 추가적인 서버 호출 없이 즉시 적용할 수 있도록 브라우저에서 캐시된 SPA의 사용자 동작에 대한 결과로서 표시되는 보기를 위한 타깃팅된 콘텐츠입니다. |
| 7 | [!UICONTROL Analytics] 데이터가 데이터 수집 서버로 전송됩니다. |
| 8 | 대상 데이터는 SDID를 통해 [!UICONTROL Analytics] 데이터와 일치하고 [!UICONTROL Analytics] 보고 저장소로 처리됩니다.<P>그런 다음 [!UICONTROL Analytics] 데이터는 [!UICONTROL Analytics for Target](A4T) 보고서를 통해 [!UICONTROL Analytics] 및 [!DNL Target] 모두에서 볼 수 있습니다. |

이제 SPA에서 `triggerView()`가 구현될 때 그곳이 어디든, 보기 및 작업은 캐시에서 검색되고 서버 호출 없이 사용자에게 표시됩니다. `triggerView()`는 또한 노출 수를 증가시키고 기록하기 위해 [!DNL Target] 백엔드에 알림을 요청합니다.

이미지 를 클릭하여 전체 너비로 확장합니다.

![Target 흐름 at.js 2.*x* triggerView](/help/dev/implement/client-side/assets/atjs-20-triggerview.png "Target 흐름 at.js 2.*x* triggerView"){zoomable="yes"}

| 호출 | 세부 사항 |
| --- | --- |
| 1 | 보기를 렌더링하고 작업을 적용하여 시각적 요소를 수정하기 위해 SPA에서 `triggerView()`가 호출됩니다. |
| 2 | 보기용으로 타기팅된 콘텐츠를 캐시에서 읽습니다. |
| 3 | 타기팅된 콘텐츠는 기본 콘텐츠의 플리커 없이 가능한 한 빨리 나타납니다. |
| 4 | 활동 및 증분 지표에서 방문자를 계산하기 위해 알림 요청이 [!DNL Target] 프로필 스토어에 전송됩니다. |
| 5 | [!UICONTROL Analytics] 데이터가 데이터 수집 서버로 전송되었습니다. |
| 6 | [!DNL Target] 데이터가 SDID를 통해 [!UICONTROL Analytics] 데이터와 일치하고 [!UICONTROL Analytics] 보고 저장소로 처리됩니다. 그런 다음 [!UICONTROL Analytics] 데이터는 A4T 보고서를 통해 [!UICONTROL Analytics] 및 [!DNL Target] 모두에서 볼 수 있습니다. |

## at.js 2.*x*

at.js 2.[Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) 확장의 태그를 통해 *x*&#x200B;합니다.

>[!NOTE]
>
>[!DNL Adobe Experience Platform]의 태그를 사용하여 at.js를 배포하는 것이 좋습니다.
>
>또는
>
>at.js 2.[!DNL Target] UI를 사용하여 *x*&#x200B;을(를) 배포하고 선택한 [메서드를 사용하여 ](/help/dev/implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md)을(를) 배포합니다.

## 사용 중단된 at.js 함수

at.js 2에서는 더 이상 사용되지 않는 몇 가지 함수가 있습니다.*x*.

>[!WARNING]
>
>이렇게 더 이상 사용되지 않는 함수가 at.js 2.*x*&#x200B;이(가) 배포되었습니다. 콘솔 경고가 표시됩니다. 업그레이드할 때 권장되는 접근 방법은 at.js 2의 배포를 테스트하는 것입니다.스테이징 환경에서 *x*&#x200B;을(를) 실행하고 콘솔에 기록된 모든 경고를 하나하나 다 확인하고, 사용이 중단된 함수를 at.js 2에 도입된 새로운 함수로 변환해야 합니다.*x*.

아래에는 사용이 중단된 함수와 그에 해당하는 새로운 함수가 있습니다. 전체 함수 목록이 필요하면 [at.js 함수](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md)를 참조하십시오.

>[!NOTE]
>
>at.js 2.** x는 `mboxDefault` 표시 요소를 더 이상 자동으로 사전에 숨기지 않습니다. 따라서 고객은 사이트에서 수동으로 또는 태그 관리자를 통해 사전 숨김 로직을 수용해야 합니다.

### mboxCreate(mbox,params)

**설명**:

요청을 실행하고 `mboxDefault` 클래스 이름을 사용하는 가장 가까운 DIV에 오퍼를 적용합니다.

**예**:

```html {line-numbers="true"}
<div class="mboxDefault">
  default content to replace by offer
</div>
<script>
  mboxCreate('mboxName','param1=value1','param2=value2');
</script>
```

**at.js 2.*x*에 상응**

`mboxCreate(mbox, params)`의 대체 함수는 `getOffer()`와 `applyOffer()`입니다.

**예**:

```html {line-numbers="true"}
<div class="mboxDefault"> 
  default content to replace by offer 
</div> 
<script> 
  var el = document.currentScript.previousElementSibling;
  adobe.target.getOffer({
    mbox: "mboxName",
    params: {
      param1: "value1",
      param2: "value2"
    },
    success: function(offer) {
      adobe.target.applyOffer({
        mbox: "mboxName",
        selector: el,
        offer: offer
      });
    },
    error: function(error) {
      console.error(error);
      el.style.visibility = "visible";
    }
  });
</script> 
```

### mboxDefine() 및 mboxUpdate()

**설명**:

요소와 mbox 이름 사이에 내부 매핑을 만들되, 요청을 실행하지 마십시오. 요청을 실행하고 `mboxDefine()`에서 nodeId로 식별되는 요소에 오퍼를 적용하는 `mboxUpdate()`와 함께 사용됩니다. `mboxCreate`로 시작된 mbox를 업데이트하는 데도 사용할 수 있습니다. 

**예**:

```html {line-numbers="true"}
<div id="someId" class="mboxDefault"></div>
<script>
 mboxDefine('someId','mboxName','param1=value1','param2=value2');
 mboxUpdate('mboxName','param3=value3','param4=value4');
</script>
```

**at.js 2.*X*에 상응**:

`mboxDefine()`과 `mboxUpdate`의 대체 함수는 `getOffer()`와 `applyOffer()`이며 `applyOffer()`에서는 선택기 선택 사항이 사용됩니다. 이 접근 방식에서는 ID가 있는 선택기뿐만 아니라 CSS 선택기를 사용하여 오퍼를 요소에 매핑할 수 있습니다.

**예**:

```html {line-numbers="true"}
<div id="someId" class="mboxDefault"> 
  default content to replace by offer 
</div> 
<script> 
  adobe.target.getOffer({
    mbox: "mboxName",
    params: {
      param1: "value1",
      param2: "value2",
      param3: "value3",
      param4: "value4" 
    },
    success: function(offer) {
      adobe.target.applyOffer({
        mbox: "mboxName",
        selector: "#someId",
        offer: offer
      });
    },
    error: function(error) {
      console.error(error);
      var el = document.getElementById("someId");
      el.style.visibility = "visible";
    }
  });
</script>
```

### adobe.target.registerExtension()

**설명**:

특정 확장 기능을 등록하는 표준 방법을 제공합니다.

이 함수는 더 이상 지원되지 않으므로 사용해서는 안 됩니다.

## 의 사용이 중단된 함수, 새로운 함수 및 지원되는 at.js 함수에 대한 요약 정보 2.*x*

| 메서드 | 지원됨? | 신규? | 삭제 예정?<P>(기본 컨텐츠가 표시됩니다.) |
| --- | --- | --- | --- |
| `getOffer()` | 예 |  |  |
| `getOffers()` |  | 예 |  |
| `applyOffer()` | 예 |  |  |
| `applyOffers()` |  | 예 |  |
| `triggerView()` |  | 예 |  |
| `trackEvent()` | 예 |  |  |
| `mboxCreate()` |  |  | 예 |
| `mboxDefine()`<P>`mboxUpdate()` |  |  | 예 |
| `targetGlobalSettings()` | 예 |  |  |
| `Data Providers` | 예 |  |  |
| `targetPageParams()` | 예 |  |  |
| `targetPageParamsAll()` | 예 |  |  |
| `registerExtension()` |  |  | 예 |
| `At.js Custom Events` | 예 |  |  |

## 제한 사항 및 콜아웃

다음 제한 사항 및 콜아웃을 알아 두십시오.

### 전환 추적

전환 추적에 `mboxCreate()`을 사용하는 고객은 `trackEvent()`나 `getOffer()`를 사용해야 합니다.

### 오퍼 게재

`mboxCreate()`을 `getOffer()`나 `applyOffer()`로 대체하지 않는 고객의 경우 오퍼가 게재되지 않을 수 있습니다.

### at.js 2.*x*&#x200B;는 at.js 1.*x*&#x200B;이(가) 다른 페이지에 있습니까?

예. 방문자 프로필은 서로 다른 버전 및 라이브러리를 사용하는 여러 페이지 간에 보존됩니다. 쿠키 형식은 동일합니다.

### at.js 2의 새로운 API 사용.*x*

at.js 2.*x에서는 배달 API라고 하는 새 API를 사용합니다.* at.js가 [!DNL Target] Edge Server를 올바로 호출하는지를 디버깅하기 위해 브라우저의 개발자 도구에 있는 네트워크 탭을 &quot;배달&quot;, &quot;`tt.omtrdc.net`&quot; 또는 클라이언트 코드로 필터링할 수 있습니다. 또한 [!DNL Target]에서 키-값 쌍 대신 JSON 페이로드를 전송하는 것을 보게 됩니다.

### [!DNL Target] 글로벌 Mbox가 더 이상 사용되지 않습니다.

at.js 2.*x*&#x200B;님, 더 이상 네트워크 호출에 &quot;`target-global-mbox`&quot;이(가) 보이지 않습니다. 대신 아래와 같이 [!DNL Target] 서버로 전송된 JSON 페이로드에서 &quot;`target-global-mbox`&quot; 구문을 &quot;`execute > pageLoad`&quot;(으)로 대체했습니다.

```json {line-numbers="true"}
{
  "id": {
    // ...
  },
  "context": {
    "channel": "web",
    // ...
  },
  "execute": {
    "pageLoad": {}
  }
}
```

기본적으로 글로벌 mbox 개념은 페이지 로드 시 오퍼와 콘텐츠를 검색할지 여부를 [!DNL Target]에서 알 수 있도록 하기 위해 도입되었습니다. 따라서 최신 버전에서는 이 기능을 더욱 명확하게 했습니다.

### at.js에서 글로벌 mbox 이름이 문제가 됩니까?

고객은 **[!UICONTROL Target]** > **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit at.js Settings]**&#x200B;을(를) 통해 글로벌 mbox 이름을 지정할 수 있습니다. 이 설정은 [!DNL Target] Edge Server에서 execute > pageLoad를 [!DNL Target] UI에 나타나는 글로벌 mbox 이름으로 변환하는 데 사용됩니다. 이렇게 변환하면 고객은 계속해서 서버 측 API, 양식 기반 작성기, 프로필 스크립트를 사용할 수 있으며 글로벌 mbox 이름을 사용하여 대상을 만들 수 있습니다. 또한 at.js 1을 사용하는 페이지가 여전히 있는 경우 동일한 글로벌 mbox 이름이 **[!UICONTROL Administration]** > **[!UICONTROL Visual Experience Composer]** 페이지에도 구성되도록 하는 것이 좋습니다.다음 그림과 같이 *x*&#x200B;입니다.

![at.js 수정 대화 상자](../assets/modify-atjs.png)

및

![사용자 지정 글로벌 mbox](../assets/custom-global-mbox.png)

### at.js 2에 대해 글로벌 mbox 자동 만들기 설정을 켜야 합니까?*x*&#x200B;를 사용하는 SPA에서)하면 어떻게 될까요.

대부분의 경우, 그렇습니다. 이 설정은 at.js 2에 알려 줍니다.페이지 로드 시 [!DNL Target] Edge Server에 대한 요청을 실행하는 *x*. 글로벌 mbox가 execute > pageLoad로 변환되므로 페이지 로드 시 요청을 개시하려면 이 설정이 켜져 있어야 합니다.

### Target 글로벌 mbox 이름이 at.js 2에서 지정되지 않았더라도 기존 VEC 활동이 계속 작동합니까?*x*&#x200B;를 사용하는 SPA에서)하면 어떻게 될까요.

예. execute > pageLoad는 `target-global-mbox`처럼 [!DNL Target] 백엔드에서 처리됩니다.

### 양식 기반 활동을 `target-global-mbox`에 타깃팅하는 경우 이러한 활동이 계속 작동합니까?

예. execute > pageLoad는 [!DNL Target]처럼 `target-global-mbox` Edge Server에서 처리됩니다.

### 지원되는 at.js 2와 지원되지 않는 at.js 2.*x* 설정

| 설정 | 지원됨? |
| --- | --- |
| X-Domain | 아니오 |
| 글로벌 mbox를 자동으로 만들기 | 예 |
| 글로벌 mbox 이름 | 예 |

### at.js 2.x에서 도메인 간 추적 지원

도메인 간 추적을 통해 여러 도메인 간에 방문자를 연결할 수 있습니다. 각 도메인에 대해 새 쿠키를 만들어야 하기 때문에 방문자가 도메인에서 도메인으로 이동할 때 추적하기가 어렵습니다. 도메인 간 추적을 수행하기 위해 [!DNL Target]은 타사 쿠키를 사용하여 도메인 간에 방문자를 추적합니다. 이를 통해 `siteA.com`과(와) `siteB.com`에 이르는 [!DNL Target] 활동을 만들 수 있으며 방문자가 고유한 도메인을 탐색할 때 동일한 경험을 유지합니다. 이 기능은 [!DNL Target]의 타사 및 퍼스트 파티 쿠키 동작에 연결되어 있습니다.

>[!NOTE]
>
>도메인 간 추적은 at.js 2.10부터 지원되지만 at.js 2.2.10 이전 *x*. 도메인 간 추적은 at.js 2에서 지원됩니다.at.js 2.*x*&#x200B;에서 지원됩니다.

[!DNL Target]에서 타사 쿠키가 `<CLIENTCODE>.tt.omtrdc.net`에 저장됩니다. 자사 쿠키는 `clientdomain.com`에 저장됩니다. 첫 번째 요청은 `mboxSession` 및 `mboxPC`라는 타사 쿠키를 설정하는 HTTP 응답 헤더를 반환하는 반면, 리디렉션 요청이 추가 매개 변수(`mboxXDomainCheck=true`)를 사용하여 다시 전송됩니다. 브라우저가 타사 쿠키를 수락하면 리디렉션 요청에 해당 쿠키가 포함되고 경험이 반환됩니다. 여기서는 HTTP GET 메서드를 사용하므로 이 워크플로우가 가능합니다.

단, at.js 2.*x*, HTTP GET이 사용되지 않습니다. 대신 HTTP POST은 at.js 2.[!DNL Target] Edge 서버에 JSON 페이로드를 전송하기 위한 *x*. HTTP POST을 사용하면 브라우저가 서드파티 쿠키를 지원하는지 여부를 확인하는 리디렉션 요청이 중단됨을 의미합니다. 이것은 HTTP GET 요청은 멱등 트랜잭션이 아니지만 HTTP POST는 비멱등이어서 임의로 반복되면 안 되기 때문입니다. 따라서 at.js 2.*x*(2.10 이전)은(는) 기본적으로 지원되지 않습니다. at.js 1.*x*&#x200B;는 도메인 간 추적을 위한 기본 지원을 제공합니다.

at.js v2.10 이상에 대해 도메인 간 추적을 사용하려면 다음 중 하나를 수행할 수 있습니다.

1. at.js 2와 함께 [ECID 라이브러리 v4.3.0+](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html?lang=ko-KR)을(를) 설치합니다.*x*. ECID 라이브러리는 도메인 간에 방문자를 식별하는 데 사용되는 영구 ID를 관리하기 위해 존재합니다. ECID library v4.3.0+ 및 at.js 2.*x*&#x200B;를 설치한 뒤 고유한 도메인을 확장하고 사용자를 추적할 수 있는 활동을 만들 수 있습니다. 이 기능은 세션이 만료된 후에만 작동합니다.

1. at.js v2.10 이상이 있는 경우 ECID 라이브러리를 설치하는 대신 **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**&#x200B;의 [!DNL Target] UI에서 도메인 간 설정을 활성화할 수 있습니다. (또는 at.js 코드에서 _crossDomain_ 옵션을 _enabled_(으)로 설정할 수 있습니다.)

at.js v2 버전에 대해 도메인 간 추적을 사용하려면&#x200B;*x* 2.10 이전에 위의 옵션 #1을 구현할 수 있습니다(ECID 라이브러리 설치).

### 글로벌 mbox 자동 만들기가 지원됨

이 설정은 at.js 2에 알려 줍니다.*x*&#x200B;을(를) 사용하여 페이지 로드 시 [!DNL Target] Edge Server에 대한 요청을 실행합니다. 글로벌 mbox가 execute > pageLoad로 변환되고, [!DNL Target] Edge Server가 이를 해석하므로 고객은 페이지 로드 시 요청을 개시하려면 이 설정을 켜야 합니다.

### 글로벌 mbox 이름이 지원됨

고객은 **[!UICONTROL Target]** > **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Edit]**&#x200B;을(를) 통해 글로벌 mbox 이름을 지정할 수 있습니다. 이 설정은 [!DNL Target] Edge Server에서 execute > pageLoad를 입력된 글로벌 mbox 이름으로 변환하는 데 사용됩니다. 이렇게 변환하면 고객은 계속해서 서버 측 API, 양식 기반 작성기, 프로필 스크립트를 사용할 수 있으며 글로벌 mbox를 타깃팅하는 대상을 만들 수 있습니다.

### 아래의 at.js 사용자 지정 이벤트는 `triggerView()`에 적용할 수 있습니까? 아니면 `applyOffer()`나 `applyOffers()`에만 적용할 수 있습니까?

* `adobe.target.event.CONTENT_RENDERING_FAILED`
* `adobe.target.event.CONTENT_RENDERING_SUCCEEDED`
* `adobe.target.event.CONTENT_RENDERING_NO_OFFERS`
* `adobe.target.event.CONTENT_RENDERING_REDIRECT`

at.js 사용자 지정 이벤트는 `triggerView()`에도 적용할 수 있습니다.

### &amp;lbrace;`"page" : "true"`&amp;rbrace;를 사용하여 `triggerView()`을(를) 호출하면 [!DNL Target] 백엔드에 알림이 전송되고 노출이 증가합니다. 이렇게 되면 프로필 스크립트도 실행됩니까?

[!DNL Target] 백엔드에 미리 가져오기 호출이 수행되면 프로필 스크립트가 실행됩니다. 그런 다음 영향을 받은 프로필 데이터가 암호화되어 클라이언트측으로 다시 전달됩니다. `{"page": "true"}`인 `triggerView()`를 호출하면 암호화된 프로필 데이터와 함께 알림이 전송됩니다. 이때 [!DNL Target] 백엔드가 프로필 데이터를 해독하고 데이터베이스에 저장합니다.

### 플리커를 관리하기 위해 `triggerView()`를 호출하기 전에 사전 숨김 코드를 추가해야 합니까?

아니요. `triggerView()`를 호출하기 전에 사전 숨김(pre-hiding) 코드를 추가할 필요는 없습니다. at.js 2.*x에서는 보기가 표시되고 적용되기 전에 사전 숨김 및 플리커(깜박임) 로직을 관리합니다.*

### at.js 1.대상을 만들기 위한 *x* 매개 변수는 at.js 2에서 지원되지 않습니다.*x*&#x200B;를 사용하는 SPA에서)하면 어떻게 될까요.

다음 at.js 1.x 매개 변수는 at.js 2를 사용할 때 현재 대상 만들기에 대해 *지원되지 않음*&#x200B;입니다.*x*:

* browserHeight
* browserWidth
* browserTimeOffset
* screenHeight
* screenWidth
* screenOrientation
* colorDepth
* devicePixelRatio
* vst.* 매개 변수(아래 참조)

### at.js 2.*x* 가 vst를 사용하여 대상자 만들기를 지원하지 않습니다.* 매개 변수

at.js 1.*x*&#x200B;에서 vst를 사용할 수 있습니다.* 대상을 만들 mbox 매개 변수입니다. 이것은 at.js 1.*x*&#x200B;이(가) mbox 매개 변수를 [!DNL Target] 백 엔드로 보냈습니다. at.js 2로 마이그레이션한 후&#x200B;*x*, at.js 2이므로 이 매개 변수를 사용하여 대상을 더 이상 만들 수 없습니다.*x*&#x200B;에서 mbox 매개 변수를 다르게 보냅니다.

## at.js 호환성

다음 표에서는 다양한 활동 유형, 통합, 기능 및 at.js 함수와의 at.js 2.*x* 호환성과 다양한 활동 유형, 통합, 기능 및 at.js 함수.

### 활동 유형

| 유형 | 지원됨? |
| --- | --- |
| [!UICONTROL A/B Test] | 예 |
| [!UICONTROL Auto-Allocate] | 예 |
| [!UICONTROL Auto-Target] | 예 |
| [!UICONTROL Experience Targeting] | 예 |
| [!UICONTROL Multivariate Test] | 예 |
| [!UICONTROL Automated Personalization] | 예 |
| [!DNL Recommendations] | 예 |

>[!NOTE]
>
>[!UICONTROL Auto-Target] 활동은 at.js 2를 통해 지원됩니다.모든 수정 사항이 `Page Load Event`에 적용되면 *x* 및 VEC가 실행됩니다. 수정 사항이 특정 보기에 추가되면 [!UICONTROL A/B Test], [!UICONTROL Auto-Allocate] 및 [!UICONTROL Experience Targeting](XT) 활동만 지원됩니다.

### 통합

| 유형 | 지원됨? |
| --- | --- |
| [!UICONTROL Analytics for Target](A4T) | 예 |
| 대상자 | 예 |
| 고객 속성 | 예 |
| AEM 경험 구성요소 | 예 |
| [Adobe Experience Platform 확장](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) | 예 |
| 디버거 | 예 |
| Auditor | at.js 2에 대한 규칙이 아직 업데이트되지 않았습니다.*x* |
| [GDPR](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md)에 대한 옵트인 지원 | [at.js 버전 2.1.0](/help/dev/implement/client-side/atjs/target-atjs-versions.md#atjs-version-210-june-3-2019) 이상에서 지원됩니다. |
| [!DNL Adobe Target]에서 제공하는 AEM Enhanced Personalization | 아니오 |

### 기능

| 기능 | 지원됨? |
| --- | --- |
| X-Domain | 아니오 |
| 속성/작업 공간 | 예 |
| QA 링크 | 예 |
| 양식 기반 경험 작성기 | 예 |
| 시각적 경험 작성기(VEC) | 예 |
| 사용자 지정 코드 | 예 |
| [응답 토큰](#response-tokens) | 예 |
| 클릭 추적 | 예 |
| 여러 활동 전달 | 예 |
| targetGlobalSettings | 예(하지만 x-domain은 아님) |
| at.js 메서드 | 다음을 제외한 모든 기능이 지원됩니다.<P>`mboxCreate()`<P>`mboxUpdate()`<P>`mboxDefine()`<P>기본 컨텐츠를 표시합니다. |

### 쿼리 문자열 매개 변수

| 매개 변수 | 지원됨? |
| --- | --- |
| `?mboxDisable` | 예 |
| `?mboxDisable` | 예 |
| `?mboxTrace` | 예 |
| `?mboxSession` | 아니요 |
| `?mboxOverride.browserIp` | 예 |

## 응답 토큰

at.js 2.*x*&#x200B;는 at.js 1.*x*&#x200B;와 마찬가지로 사용자 지정 이벤트 `at-request-succeeded`를 사용하여 응답 토큰을 표시합니다. `at-request-succeeded` 사용자 지정 이벤트를 사용한 코드 예에 대해서는 [응답 토큰](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)을 참조하십시오.

## at.js 1.at.js 2에 대한 *x* 매개 변수입니다.*x* 페이로드 매핑

이 섹션에서는 at.js 1.*x*&#x200B;와 at.js 2 모두에 있는 Hide Body(본문 숨기기) 및 Show Body(본문 표시) 호출을 보여줍니다.*x*.

매개 변수 매핑을 찾기 전에 이러한 라이브러리 버전에서 사용 중인 엔드포인트가 다음과 같이 변경되었습니다.

* at.js 1.*x* - `http://<client code>.tt.omtrdc.net/m2/<client code>/mbox/json`
* at.js 2.*x* - `http://<client code>.tt.omtrdc.net/rest/v1/delivery`

또 다른 중요한 차이점은 다음과 같습니다.

* at.js 1.*x* - 클라이언트 코드가 경로의 일부입니다.
* at.js 2.*x* - 클라이언트 코드는 다음과 같은 쿼리 문자열 매개 변수로 전송됩니다.
  `http://<client code>.tt.omtrdc.net/rest/v1/delivery?client=democlient`

다음 섹션에는 at.js 1.*x* 매개 변수, 설명 및 해당 2입니다.*x* JSON 페이로드(해당되는 경우):

### at_property

(at.js 1.*x* 매개 변수)

[엔터프라이즈 사용자 권한](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=ko-KR)에 사용됩니다.

```json {line-numbers="true"}
{
  ....
  "property": {
    "token": "1213213123122313121"
  }
  ....
}
```

### mboxHost

(at.js 1.*x* 매개 변수)

[!DNL Target] 라이브러리가 실행되는 페이지의 도메인입니다.

at.js 2.*x* JSON 페이로드:

```json {line-numbers="true"}
{
  "context": {
    "browser": {
       "host": "test.com"
    }
  }
}
```

### webGLRenderer

(at.js 1.*x* 매개 변수)

브라우저의 WEB GL 렌더러 기능입니다. 장치 탐지 메커니즘에서 방문자의 장치가 데스크탑, iPhone, Android 장치 등인지 판별하는 데 사용됩니다.

at.js 2.*x* JSON 페이로드:

```json {line-numbers="true"}
{
  "context": {
    "browser": {
       "webGLRenderer": "AMD Radeon Pro 560X OpenGL Engine"
    }
  }
}
```

### mboxURL

(at.js 1.*x* 매개 변수)

페이지 URL입니다.

at.js 2.*x* JSON 페이로드:

```json {line-numbers="true"}
{
  "context": {
    "address": {
       "url": "http://test.com"
    }
  }
}
```

### mboxReferrer

(at.js 1.*x* 매개 변수)

페이지 레퍼러입니다.

at.js 2.*x* JSON 페이로드:

```json {line-numbers="true"}
{
  "context": {
    "address": {
       "referringUrl": "http://google.com"
    }
  }
}
```

### mbox (the name) equals to global mbox

(at.js 1.*x* 매개 변수)

배달 API에는 더 이상 글로벌 mbox 개념이 없습니다. JSON 페이로드에서 `execute > pageLoad`를 사용해야 합니다.

at.js 2.*x* JSON 페이로드:

```json {line-numbers="true"}
{
  "execute": {
    "pageLoad": {
       "parameters": ....
       "profileParameters": ...
       .....
    }
  }
}
```

### mbox (the name) is *not* equal to global mbox

(at.js 1.*x* 매개 변수)

mbox 이름을 사용하려면 `execute > mboxes`에 전달합니다. mbox에는 인덱스와 이름이 필요합니다.

at.js 2.*x* JSON 페이로드:

```json {line-numbers="true"}
{
  "execute": {
    "mboxes": [{
       "index": 0,
       "name": "some-mbox",
       "parameters": ....
       "profileParameters": ...
       .....
    }]
  }
}
```

### mboxId

(at.js 1.*x* 매개 변수)

더 이상 사용되지 않습니다.

### mboxCount

(at.js 1.*x* 매개 변수)

더 이상 사용되지 않습니다.

### mboxRid

(at.js 1.*x* 매개 변수)

디버깅을 지원하기 위해 다운스트림 시스템에서 사용한 요청 ID입니다.

at.js 2.*x* JSON 페이로드:

```json {line-numbers="true"}
{
  "requestId": "2412234442342"
  ....
}
```

### mboxTime

(at.js 1.*x* 매개 변수)

더 이상 사용되지 않습니다.

### mboxSession

(at.js 1.*x* 매개 변수)

세션 ID가 배달 API 엔드포인트에 쿼리 문자열 매개 변수(`sessionId`)로 전송됩니다.

### mboxPC

(at.js 1.*x* 매개 변수)

TNT ID가 `id > tntId`에 전달됩니다.

at.js 2.*x* JSON 페이로드:

```json {line-numbers="true"}
{
  "id": {
    "tntId": "ca5ddd7e33504c58b70d45d0368bcc70.21_3"
  }
  ....
}
```

### mboxMCGVID

(at.js 1.*x* 매개 변수)

Marketing Cloud 방문자 ID가 `id > marketingCloudVisitorId`에 전달됩니다.

at.js 2.*x* JSON 페이로드:

```json {line-numbers="true"}
{
  "id": {
    "marketingCloudVisitorId": "797110122341429343505"
  }
  ....
}
```

### `vst.aaaa.id` 및 `vst.aaaa.authState`

(at.js 1.*x* 매개 변수)

고객 ID를 `id > customerIds`에 전달해야 합니다.

at.js 2.*x* JSON 페이로드:

```json {line-numbers="true"}
{
  "id": {
    "customerIds": [{
       "id": "1232131",
       "integrationCode": "aaaa",
       "authenticatedState": "....."
     }]
  }
  ....
}
```

### mbox3rdPartyId

(at.js 1.*x* 매개 변수)

다른 [!DNL Target] ID를 연결하는 데 사용되는 고객 타사 ID입니다.

at.js 2.*x* JSON 페이로드:

```json {line-numbers="true"}
{
  "id": {
    "thirdPartyId": "1232312323123"
  }
  ....
}
```

### mboxMCSDID

(at.js 1.*x* 매개 변수)

SDID(보충 데이터 ID)라고도 합니다. `experienceCloud > analytics > supplementalDataId`에 전달해야 합니다.

at.js 2.*x* JSON 페이로드:

```json {line-numbers="true"}
{
  "experienceCloud": {
    "analytics": {
      "supplementalDataId": "1212321132123131"
    }
  }
  ....
}
```

### vst.trk

(at.js 1.*x* 매개 변수)

[!UICONTROL Analytics] 추적 서버입니다. `experienceCloud > analytics > trackingServer`에 전달해야 합니다.

at.js 2.*x* JSON 페이로드:

```json {line-numbers="true"}
{
  "experienceCloud": {
    "analytics": {
      "trackingServer": "analytics.test.com"
    }
  }
  ....
}
```

### vst.trks

(at.js 1.*x* 매개 변수)

Analytics 추적 서버가 안전합니다. `experienceCloud > analytics > trackingServerSecure`에 전달해야 합니다.

at.js 2.*x* JSON 페이로드:

```json {line-numbers="true"}
{
  "experienceCloud": {
    "analytics": {
      "trackingServerSecure": "secure-analytics.test.com"
    }
  }
  ....
}
```

### mboxMCGLH

(at.js 1.*x* 매개 변수)

Audience Manager 위치 힌트입니다. `experienceCloud > audienceManager > locationHint`에 전달해야 합니다.

at.js 2.*x* JSON 페이로드:

```json {line-numbers="true"}
{
  "experienceCloud": {
    "audienceManager": {
      "locationHint": 9
    }
  }
  ....
}
```

### mboxAAMB

(at.js 1.*x* 매개 변수)

Audience Manager Blob입니다. `experienceCloud > audienceManager > blob`에 전달해야 합니다.

at.js 2.*x* JSON 페이로드:

```json {line-numbers="true"}
{
  "experienceCloud": {
    "audienceManager": {
      "blob": "2142342343242342"
    }
  }
  ....
}
```

### mboxVersion

(at.js 1.*x* 매개 변수)

버전은 버전 매개 변수를 통해 쿼리 문자열 매개 변수로 전송됩니다.

## 교육 비디오: at.js 2.*x* 아키텍처 다이어그램 ![개요 배지](../../assets/overview.png)

at.js 2.*x*&#x200B;은(는) SPA에 대한 Adobe [!DNL Target]의 지원을 개선하고 다른 Experience Cloud 솔루션과 통합됩니다. 다음 비디오에서는 모든 것이 어떻게 합쳐지는지 설명합니다.

>[!VIDEO](https://video.tv.adobe.com/v/26250/?quality=12)

[at.js 2 이해 를 참조하십시오.자세한 내용은 *x*&#x200B;을(를) 작동시킵니다](https://experienceleague.adobe.com/docs/target-learn/tutorials/implementation/understanding-how-atjs-20-works.html).
