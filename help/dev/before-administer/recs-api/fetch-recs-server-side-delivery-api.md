---
title: 배달 API로 Recommendations을 가져오는 방법
description: 이 문서는 Adobe Target 배달 API를 사용하여 권장 사항 콘텐츠를 가져오는 데 필요한 단계를 개발자에게 안내합니다.
feature: APIs/SDKs, Recommendations, Administration & Configuration
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 9b391f42-2922-48e0-ad7e-10edd6125be6
source-git-commit: d98c7b890f7456de0676cadce5d6c70bc62d6140
workflow-type: tm+mt
source-wordcount: '1520'
ht-degree: 1%

---

# 배달 API를 사용하여 Recommendations 가져오기

Adobe Target 및 Adobe Target Recommendations API를 사용하여 웹 페이지에 응답을 제공할 수 있지만 앱, 화면, 콘솔, 이메일, 키오스크 및 기타 디스플레이 장치를 비롯한 HTML 기반이 아닌 경험에서도 사용할 수 있습니다. 즉, Target 라이브러리와 JavaScript를 사용할 수 없는 경우 [Target 게재 API](/help/dev/implement/delivery-api/overview.md) 에서는 개인화된 경험을 제공하기 위해 전체 Target 기능에 액세스할 수 있습니다.

>[!NOTE]
>
>실제 권장 사항(권장 제품 또는 항목)이 포함된 콘텐츠를 요청할 때 Target 배달 API를 사용하십시오.

권장 사항을 검색하려면 적절한 컨텍스트 정보로 Adobe Target Delivery API POST 호출을 전송하십시오. 이 정보에는 사용자 ID(사용자의 최근에 본 항목과 같은 프로필별 권장 사항과 함께 사용하기 위해), 관련 mbox 이름, mbox 매개 변수, 프로필 매개 변수 또는 기타 속성이 포함될 수 있습니다. 응답에는 JSON 또는 HTML 형식의 권장 entity.ids(및 다른 엔티티 데이터를 포함할 수 있음)가 포함되며, 이 값은 장치에 표시될 수 있습니다.

다음 [배달 API](/help/dev/implement/delivery-api/overview.md) for Adobe Target은 표준 Target 요청이 제공하는 모든 기존 기능을 노출합니다.

게재 API:

* RESTful 방식으로 위치 및 대상에 대한 경험 또는 오퍼를 검색할 수 있습니다.
* 인증이 필요하지 않습니다.
* POST만
* 쿠키 또는 리디렉션 호출을 처리하지 않습니다.
* 에서는 &quot;사용자 역할&quot;을 필요로 하지 않으며, 인식하지도 않습니다. 콘텐츠를 가져오거나 Target 에지 서버에 이벤트를 보고합니다.

배달 API를 사용하여 Target 경험(권장 사항 포함)을 전달하려면 다음 단계를 따르십시오.

1. 시각적 경험 작성기가 아닌 양식 기반 작성기를 사용하여 Target 활동(A/B, XT, AP 또는 Recommendations)을 만듭니다.
1. 배달 API를 사용하여 방금 만든 Target 활동으로 생성된 요청에 대한 응답을 가져옵니다.

&lt;!— 질문: 두 가지 단계가 모두 필요한 이유는 무엇입니까? mbox에 대해 양식 기반 권장 사항이 정의된 경우 게재 API를 단계별로 사용하여 결과를 검색할 수 있다는 점/이점은 무엇입니까? 양식 기반 Rec로 대상 장치에 결과를 전달하지 않는 이유는 무엇입니까?..?? A: 아래 사용 사례 참조... 결과를 표시하기 전에 더 많은 작업을 수행하기 위해 보류 중인 결과를 &quot;가로채기&quot;하려는 경우입니다. 재고 수준에 대한 실시간 비교와 같은 것입니다. --->

## 양식 기반 경험 작성기를 사용하여 추천 만들기

배달 API와 함께 사용할 수 있는 권장 사항을 만들려면 [양식 기반 작성기](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html).

1. 먼저 권장 사항에 사용할 JSON 기반 디자인을 작성 및 저장합니다. 샘플 JSON과 양식 기반 활동을 구성할 때 JSON 응답을 반환하는 방법에 대한 배경 정보는 다음 문서 를 참조하십시오. [권장 사항 디자인 만들기](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html). 이 예제에서 디자인 이름은 다음과 같습니다 *단순 JSON.*
   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

1. Target에서 다음 위치로 이동합니다. **[!UICONTROL 활동]** > **[!UICONTROL 활동 만들기]** > **[!UICONTROL Recommendations]**&#x200B;을 선택한 다음 을 선택합니다. **[!UICONTROL 양식]**.

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

1. 속성을 선택하고 **[!UICONTROL 다음]**.
1. 사용자가 권장 사항의 응답을 받을 위치를 정의합니다. 아래 예제는 이라는 위치를 사용합니다. *api_charter*. 앞에서 만든 이름이 인 JSON 기반 디자인을 선택합니다. *단순 JSON.*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
1. 권장 사항을 저장하고 활성화합니다. 그러면 결과가 생성됩니다. [결과가 준비되면](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html), 게재 API를 사용하여 게재를 검색할 수 있습니다.

## 게재 API 사용

구문 [배달 API](/help/dev/implement/delivery-api/overview.md) 은(는)

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. 클라이언트 코드가 필요합니다. 다시 말해서 클라이언트 코드는으로 이동하여 Adobe Target에서 찾을 수 있습니다. **[!UICONTROL Recommendations]** > **[!UICONTROL 설정]**. 다음을 참고하십시오. **클라이언트 코드** 의 값 **권장 사항 API 토큰** 섹션.
   ![client-code.png](assets/client-code.png)
1. 클라이언트 코드가 있으면 배달 API 호출을 구성합니다. 아래 예제는 **[!UICONTROL 웹 일괄 처리된 Mbox 배달 API 호출]** 다음에서 제공됨 [배달 API Postman 컬렉션](../../implement/delivery-api/overview.md/#section/Getting-Started/Postman-Collection), 관련 수정 수행. 예:
   * 다음 **브라우저** 및 **주소** 개체에서 제거됨 **본문**, 이는 비 HTML 사용 사례에 필요하지 않기 때문입니다
   * *api_charter* 은 이 예제에서 위치 이름으로 나열됩니다.
   * 이 권장 사항은 현재 항목 키를 Target에 전달해야 하는 콘텐츠 유사성을 기반으로 하므로 entity.id가 지정됩니다.
     ![server-side-Delivery-API-call.png](assets/server-side-delivery-api-call2.png)
쿼리 매개 변수를 올바르게 구성해야 합니다. 예를 들어 을 지정해야 합니다 `{{CLIENT_CODE}}` 필요한 경우. &lt;!— Q: 업데이트된 호출 구문에서 entity.id는 이전 버전에서와 같이 mboxParameter 대신 profileParameter로 나열됩니다. ---> &lt;!— Q: 이전 이미지 ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) 이전 첨부 텍스트: &quot;이 권장 사항은 mboxParameters를 통해 전송된 entity.id를 기반으로 하는 콘텐츠 유사 제품을 기반으로 합니다.&quot; —>
     ![client-code3](assets/client-code3.png)
1. 요청을 보냅니다. 다음에 대해 실행됩니다. *api_charter* 에서 실행 중인 활성 권장 사항이 있는 위치는 권장 엔티티 목록을 출력하는 JSON 디자인으로 정의됩니다.
1. JSON 디자인을 기반으로 응답을 받습니다.
   ![server-side-create-recs-json-response2.png](assets/server-side-create-recs-json-response2.png)
응답에는 키 ID와 권장 엔티티의 엔티티 ID가 포함됩니다.

이러한 방식으로 Recommendations에서 배달 API를 사용하면 HTML이 아닌 디바이스에서 방문자에게 권장 사항을 표시하기 전에 추가 단계를 수행할 수 있습니다. 예를 들어 최종 결과를 표시하기 전에 배달 API에서 응답을 가져와 다른 시스템(예: CMS, PIM 또는 전자 상거래 플랫폼)에서 엔티티 속성 세부 사항(재고, 가격, 등급 등)을 추가로 실시간 조회할 수 있습니다.

이 안내서에 설명된 접근 방식을 사용하면 모든 애플리케이션에서 Target의 응답을 활용하여 개인화된 추천을 제공할 수 있습니다.

## 구현 예제

다음 리소스는 다양한 비 HTML 집중 구현의 예를 제공합니다. 관련된 시스템 및 장치로 인해 모든 구현이 고유하다는 점을 기억하십시오.

| 리소스 | 세부 사항 |
| --- | --- |
| [어디서나 Adobe Target - Server Side 또는 IoT 구현](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Target 서버측 API를 활용하는 React 애플리케이션에 대한 실습 경험을 제공하는 Adobe Summit 2019 Lab. |
| [Adobe SDK가 없는 모바일 앱의 Adobe Target](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | 이 안내서에서는 Adobe SDK를 설치하지 않고 모바일 앱에서 Adobe Target을 설정하는 방법을 보여 줍니다. 이 솔루션은 Tealium SDK 웹 보기 및 원격 명령 모듈을 사용하여 Adobe 방문자 API(Experience Cloud) 및 Adobe Target API에 요청을 보내고 받습니다. |
| [Experience Platform Launch 및 Target API 구현에서 Target 확장 구성](https://developer.adobe.com/client-sdks/documentation/adobe-target/) | Experience Platform Launch에서 Target 확장을 구성하고, 앱에 Target 확장을 추가하고, Target API를 구현하여 활동을 요청하고, 오퍼를 미리 가져오고, 시각적 미리보기 모드로 전환하는 절차입니다. |
| [Adobe Target 노드 클라이언트](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | 오픈 소스 Target Node.js SDK v1.0 |
| [서버측 개요](../../implement/server-side/server-side-overview.md) | Adobe Target 서버 측 배달 API, 서버 측 배치 배달 API, Node.js SDK 및 Adobe Target Recommendations API에 대한 정보입니다. |
| [이메일의 Adobe Campaign 컨텐츠 Recommendations](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Adobe Campaign에서 Adobe Target 및 Adobe I/O Runtime을 통해 이메일에 포함된 콘텐츠 권장 사항을 활용하는 방법을 설명하는 블로그입니다. |

## API를 사용하여 Recommendations 설정 관리

대부분의 경우, 위의 섹션에 언급된 것과 같은 이유로 Adobe Target UI에서 권장 사항이 구성된 다음 Target API를 통해 사용되거나 액세스됩니다. 이러한 UI-API 조정은 일반적입니다. 그러나 경우에 따라 사용자는 API를 통해 모든 작업(결과 사용뿐만 아니라 설정도 모두 수행함)을 수행할 수 있습니다. 훨씬 덜 일반적이긴 하지만, 사용자는 를 절대적으로 구성, 실행 및 실행할 수 있습니다. *및* api를 완전히 사용하여 권장 사항 결과를 활용합니다.

우리는 다음 과정에서 배웠습니다. [이전 섹션](manage-catalog.md) Adobe Target Recommendations 엔터티를 관리하고 서버측에 전달하는 방법 마찬가지로 [Adobe Developer 콘솔](https://developer.adobe.com/console/home) Adobe Target에 로그인하지 않고도 기준, 프로모션, 컬렉션 및 디자인 템플릿을 관리할 수 있습니다. 모든 Recommendations API의 전체 목록을 찾을 수 있습니다. [여기](https://developer.adobe.com/target/administer/recommendations-api/), 그러나 다음은 참조를 위한 요약입니다.

| 리소스 | 세부 사항 |
| --- | --- |
| [컬렉션](https://developer.adobe.com/target/administer/recommendations-api/#tag/Collections) | 컬렉션 나열, 만들기, 가져오기, 편집 및 삭제 |
| [기준](https://developer.adobe.com/target/administer/recommendations-api/#tag/Criteria) | 기준을 나열하고 가져옵니다. |
| [디자인](https://developer.adobe.com/target/administer/recommendations-api/#tag/Designs) | 디자인을 나열, 작성, 가져오기, 편집, 삭제 및 확인합니다. |
| [엔티티](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities) | 엔티티를 저장, 삭제 및 가져옵니다. |
| [프로모션](https://developer.adobe.com/target/administer/recommendations-api/#tag/Promotions) | 프로모션을 나열, 생성, 가져오기, 편집 및 삭제합니다. |
| [범주 기준](https://developer.adobe.com/target/administer/recommendations-api/#tag/Category-Criteria) | 카테고리 기준을 나열, 만들기, 가져오기, 편집 및 삭제합니다. |
| [사용자 지정 기준](https://developer.adobe.com/target/administer/recommendations-api/#tag/Custom-Criteria) | 사용자 지정 기준을 나열, 만들기, 가져오기, 편집 및 삭제합니다. |
| [항목 기준](https://developer.adobe.com/target/administer/recommendations-api/#tag/Item-Criteria) | 항목 기준을 나열, 만들기, 가져오기, 편집 및 삭제합니다. |
| [인기도 기준](https://developer.adobe.com/target/administer/recommendations-api/#tag/Popularity-Criteria) | 인기도 기준을 나열, 만들기, 가져오기, 편집 및 삭제합니다. |
| [프로필 속성 기준](https://developer.adobe.com/target/administer/recommendations-api/#tag/Profile-Attribute-Criteria) | 프로필 속성 기준을 나열, 작성, 가져오기, 편집 및 삭제합니다. |
| [최근 기준](https://developer.adobe.com/target/administer/recommendations-api/#tag/Recent-Criteria) | 최근 기준을 나열, 만들기, 가져오기, 편집 및 삭제합니다. |
| [시퀀스 기준](https://developer.adobe.com/target/administer/recommendations-api/#tag/Sequence-Criteria) | 시퀀스 기준을 나열, 만들기, 가져오기, 편집 및 삭제합니다. |

## 참조 설명서

* [Adobe Target 배달 API 설명서](/help/dev/implement/delivery-api/overview.md)
* [이메일에 권장 사항 통합](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## 요약 및 검토

축하합니다! 이 안내서를 완료하면 다음 방법을 배울 수 있습니다.
* [Recommendations API를 사용하여 카탈로그 관리](manage-catalog.md)
* [Recommendations API를 사용하여 사용자 지정 기준 관리](manage-custom-criteria.md)
* [Recommendations에서 배달 API 사용](fetch-recs-server-side-delivery-api.md)
