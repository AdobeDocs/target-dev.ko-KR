---
keywords: gdpr, eu, 유럽 연합, 개인 정보 보호, faq, 자주 묻는 질문, 캘리포니아 소비자 개인 정보 보호법, ccpa, 개인 정보 보호, 데이터 보호, 옵트아웃, 옵트아웃, 정부, 규정, gdpr5, gdpr6, gdpr7, gdpr8, gdpr9, eu0, eu1, eu2, eu3, eu4, eu5
description: Target 및 유럽 연합 일반 데이터 정보 보호 규정(GDPR), 캘리포니아 소비자 개인정보 보호법(CCPA) 및 기타 개인정보 보호 요구 사항에 대해 알아봅니다.
title: Target은 개인정보 보호 및 데이터 보호 규정을 어떻게 처리합니까?
feature: Privacy & Security
exl-id: 40bac3c5-8e6f-4a90-ac0c-eddce1dbe6c0
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '2374'
ht-degree: 64%

---

# 개인정보 보호 및 데이터 보호 규정

유럽 연합의 일반 데이터 정보 보호 규정(GDPR), 캘리포니아 소비자 개인정보 보호법(CCPA) 및 기타 국제 개인정보 보호 요구 사항에 대한 정보입니다. 이러한 규정이 어떻게 귀사와 Adobe Target에 영향을 미치는지 알아보십시오.

## 개인정보 보호 및 일반 데이터 보호 규정(GDPR) 개요

2018년 5월 25일 자로 유럽 연합의 GDPR이 발효되었습니다. 이 규정의 의미에 대한 자세한 내용은 [GDPR 및 비즈니스](https://business.adobe.com/privacy/general-data-protection-regulation.html)를 참조하십시오.

Adobe가 기업에 소프트웨어 및 서비스를 제공할 때 Adobe는 이러한 서비스를 제공하는 과정에서 처리하고 저장하는 개인 데이터에 대한 데이터 처리자 역할을 합니다. Adobe는 데이터 처리자로서 귀사의 허가 및 지침(예: Adobe와의 계약에 명시된 내용)에 따라 개인 데이터를 처리합니다.

귀하는 데이터 관리자로서 Adobe가 귀하를 대신하여 처리하고 저장하는 개인 데이터를 결정합니다. 귀하가 Adobe Experience Cloud 솔루션을 사용하는 경우, Adobe는 귀하가 사용하는 솔루션 및 귀하의 Adobe Experience Cloud 계정에 전송하기로 선택한 정보에 따라 귀하를 위해 개인 데이터를 호스팅할 수 있습니다. 상세한 예제 목록은 [Adobe Experience Cloud 개인정보 보호](https://www.adobe.com/privacy/experience-cloud.html#collect)를 참조하십시오.

Adobe Experience Cloud은 데이터 제어자가 다음 작업을 완료할 수 있도록 하는 GDPR 지원 API를 제공합니다.

* Target 내에 저장된 데이터 주체 정보에 액세스
* Target 내에 저장된 데이터 주체 정보 삭제

자세한 내용은 다음 문서를 참조하십시오.

* [Adobe Privacy Service 개요](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html)
* [Privacy Service API 안내서](https://experienceleague.adobe.com/docs/experience-platform/privacy/api/overview.html)
* [Privacy Service UI 개요](https://experienceleague.adobe.com/docs/experience-platform/privacy/ui/overview.html)

## 캘리포니아 소비자 개인정보 보호법(CCPA) 개요

캘리포니아 소비자 개인정보 보호법(CCPA)은 캘리포니아 소비자에게 개인 정보와 관련된 새로운 권리를 제공하고 캘리포니아에서 비즈니스를 수행하는 특정 법인에 대해 데이터 보호 책임을 부과합니다. 2020년 1월 1일 자로 CCPA가 발효되었습니다.

이 법은 높은 수준에서 캘리포니아 시민에게 다음과 같은 권리를 부여합니다.

* 정보 요청(데이터 액세스)
* 개인 정보 판매 거부(서드파티와의 정보 공유를 거부할 수 있는 광범위하게 정의된 권리)
* 개인 정보 삭제
* 개인 정보가 공개 또는 판매되고 있다는 내용의 정보 제공

지난해 유럽의 개인정보 보호법(GDPR)에 부지런히 대비한 경우 이러한 권리 중 일부가 익숙할 수 있으며 수행한 작업의 많은 부분이 다른 용도로 사용될 수 있습니다.

>[!NOTE]
>
>CCPA에 적용되는 데이터를 액세스하고 삭제하는 프로세스는 GDPR과 동일합니다.

## Adobe Target 및 Adobe Experience Platform 옵트인

Target은 Adobe Experience Platform의 태그를 통해 옵트인 기능 지원을 제공하여 귀하의 동의 관리 전략을 지원합니다. 선택 기능을 통해 고객이 Target 태그를 실행하는 방법과 시기를 제어할 수 있습니다. 또한 Adobe Experience Platform을 통해 Target 태그를 사전 승인할 수 있는 옵션이 있습니다. Target at.js 라이브러리에서 옵트인을 사용하는 기능을 활성화하려면 를 사용해야 합니다 `targetGlobalSettings` 및 추가 `optinEnabled=true` 설정. Adobe Experience Platform의 확장 프로그램 설치 보기에 있는 GDPR 옵트인 드롭다운 목록에서 &quot;활성화&quot;를 선택합니다. 다음을 참조하십시오 [Adobe Experience Platform을 사용하여 Target 구현](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) 을 참조하십시오.

다음 코드 스니펫은 `optinEnabled=true` 설정을 활성화하는 방법을 보여 줍니다.

```
window.targetGlobalSettings = {
  optinEnabled: true
};
```

>[!NOTE]
>
>옵트인 기능은 at.js 버전 1.7.0 및 at.js 2.1.0 이상에서 지원됩니다. 옵트인은 at.js 버전 2.0.0 및 2.0.1에서 지원되지 않습니다.

Adobe Experience Platform을 사용하여 옵트인을 관리하는 것이 좋습니다. Target 실행 전에 동의 전략의 일부로 유용하게 사용할 수 있는 페이지에서 선택한 요소를 숨기기 위한 세부적인 제어 기능이 Adobe Experience Platform에 추가로 있습니다.

선택 기능을 사용할 때 고려해야 할 세 가지 시나리오가 있습니다.

1. **Target 태그는 Adobe Experience Platform(또는 이전에 승인된 Target의 데이터 주체)를 통해 사전 승인됩니다.** Target 태그는 예상대로 동의 및 기능을 위해 유지되지 않습니다.
1. **Target 태그가 사전 승인되지 않으며 `bodyHidingEnabled`가 FALSE:** Target 태그는 고객으로부터 동의가 수집된 후에만 실행됩니다. 동의하기 전에는 기본 콘텐츠만 사용할 수 있습니다. 동의를 받은 후 Target을 호출하여 데이터 주체(방문자)에 대해 개인화된 콘텐츠를 사용할 수 있습니다. 동의 전에는 기본 콘텐츠만 사용할 수 있으므로, 개인화될 수 있는 페이지 또는 콘텐츠의 모든 부분을 다루는 스플래시 페이지와 같은 적절한 전략을 사용하는 것이 중요합니다. 이 프로세스를 통해 데이터 주체(방문자)에 대한 경험의 일관성을 유지할 수 있습니다.
1. **Target 태그가 사전 승인되지 않으며 `bodyHidingEnabled`가 TRUE:** Target 태그는 고객으로부터 동의가 수집된 후에만 실행됩니다. 동의하기 전에는 기본 콘텐츠만 사용할 수 있습니다. 그러나 `bodyHidingEnabled`가 true로 설정되어 있으므로 `bodyHiddenStyle`은 Target 태그가 실행될 때까지 페이지에 어떤 콘텐츠가 숨겨져 있는지 나타냅니다(또는 데이터 주체에서 선택 기능을 거부하며, 이 경우 기본 콘텐츠가 표시됨). 기본적으로 `bodyHiddenStyle`은 `body { opacity:0;}`로 설정되어 있으며, 이를 사용하면 HTML 본문 태그가 숨겨집니다. 아래는 페이지 콘텐츠를 하나의 컨테이너에 배치하고 동의 관리자 대화 상자를 별도의 컨테이너에 배치하여 동의 관리자 대화 상자 이외의 페이지 본문 전체가 숨겨질 수 있도록 하는 Adobe 권장 페이지 구성입니다. 이 설정은 페이지 콘텐츠 컨테이너만 숨기도록 Target을 구성합니다. [Privacy Service 개요](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?)를 참조합시오.

   시나리오 3에 대한 권장 페이지 설정은 다음과 같습니다.

   ```
   <html> 
   <head> 
   //visitor, at.js 
   </head> 
   
   <body> 
   <div id = "consentManagerDialog"> 
   
   //consent manager html dialog goes here 
   </div> 
   
   <div id="pageContent"> 
   // page content goes here 
   </div> 
   
   </body> 
   </html> 
   ```

   `bodyHiddenStyle`이 다음과 같다고 가정합니다.

   ```
   #pageContent { opacity:0;}
   ```

## 개인정보 보호 및 데이터 보호 규정 FAQ

Target과 관련된 유럽연합 일반 데이터 보호 규칙(GDPR), 캘리포니아 소비자 개인 정보 보호법(CCPA) 및 기타 국제 개인 정보 보호 요구 사항에 대해 자주 묻는 질문(FAQ)입니다.

### 이러한 규정에 대한 Adobe 정책은 무엇입니까?

Adobe은 데이터 프로세서로서 이미 의무를 충족하거나 의무를 구현하고 있습니다. Adobe는 인증된 보안 및 개인정보 보호 제어를 통한 강력한 기반을 갖추고 있으며 2018년 5월 마감일 이전에 제품 개선을 완료했습니다. 기업 고객은 이러한 개선 사항을 구현하고 필요한 모든 정책 및 절차를 업데이트할 책임이 있습니다.

### 우리 회사는 데이터 제어자로서 사용하는 각 Adobe Experience Cloud 솔루션에 GDPR 또는 CCPA 요청을 제출해야 합니까?

아니요. Adobe은 데이터 관리자가 GDPR 및 CCPA 요구 사항을 충족하는 데 도움이 되는 중심적인 방법을 제공합니다. 데이터 제어자는 각 솔루션으로 직접 이동할 필요가 없습니다.

Target을 포함한 Experience Cloud 솔루션 전반에 대한 모든 GDPR 및 CCPA 요청은 현재 GDPR API라고 하는 중앙 Adobe API를 통해 전달됩니다. 그런 다음 API는 데이터 제어자의 Experience Cloud 솔루션 세트에 걸친 요청을 완료합니다.

### Adobe은 데이터 주체/사용자 요청에 대해 고객이 어떤 정보를 삭제할 수 있도록 허용합니까?

Target 내의 개별 방문자와 관련된 정보는 Target 방문자 프로필 내에 포함되어 있습니다. Target을 사용하면 고객이 방문자 프로필의 ID와 관련된 모든 데이터를 삭제할 수 있습니다. 프로필 데이터 Target 저장소 예시는 다음을 참조하십시오. [방문자 프로필](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html).

특정 개인을 식별하지 않는 집계 또는 익명화 데이터(예: 보고 데이터) 또는 특정 개인과 관련이 없는 데이터(예: 콘텐츠 데이터)는 사용자 삭제 요청 범위를 벗어납니다.

90일 동안 비활성 상태인 Target 방문자 프로필은 별도의 조치 없이도 기본적으로 삭제됩니다.

### 고객이 Target에 대한 GDPR 또는 CCPA 액세스 및 삭제 요청을 완료할 수 있도록 지원되는 ID는 무엇입니까?

Target은 고객 프로필을 찾기 위한 다음 ID 유형을 지원합니다.

| 사용자 ID | 네임스페이스 ID 유형 | 네임스페이스 ID | 정의 |
|--- |--- |--- |--- |
| ECID(Experience Cloud ID) | Standard | 4 | 이전에 방문자 ID 또는 Experience Cloud ID라고 했던 Adobe Experience Cloud ID입니다. 이 ID는 JavaScript API를 사용하여 찾을 수 있습니다(아래 세부 사항 참조). |
| TnT ID/쿠키 ID(TNTID) | Standard | 9 | 방문자 브라우저의 쿠키로 설정된 Target 식별자입니다. 이 ID는 JavaScript API를 사용하여 찾을 수 있습니다(아래 세부 사항 참조). |
| 서드파티 ID/CRM ID (THIRDPARTYID) | Target 관련 | 해당 없음 | Target에 고객에 대한 CRM 또는 기타 고유 식별자 정보를 제공하는 경우입니다. |

>[!NOTE]
>
>Target은 자사 및 타사 도메인 간 쿠키를 모두 지원하지만 GDPR 및 CCPA에는 자사 Target 쿠키만 권장됩니다.

###  Target은 동의 관리를 어떻게 처리합니까?

GDPR 및 CCPA에 의해 변경되는 것은 귀하가 동의를 얻어야 하는 시기가 아닌 동의를 얻는 방법입니다. 각 고객의 동의 전략은 데이터 수집에 따라 다르며 사례 및 개인정보 보호 정책을 사용합니다. 동의 관리는 지원되지 않으며 GDPR 및 CCPA에 대한 Target을 통해 수행해서는 안 됩니다.

현재 Adobe는 동의 관리 솔루션을 제공하지 않지만, 새로운 요구 사항의 일부를 해결하기 위해 시장에서 여러 가지 도구가 개발되고 있습니다. 동의 관리자를 포함하여 일반적인 개인정보 보호 도구에 대한 자세한 내용은 *국제 개인정보 보호 전문가 협회* 웹 사이트에서 [2017년 개인정보 보호 기술 공급업체 보고서](https://iapp.org/media/pdf/resource_center/Tech-Vendor-Directory-1.4.1-electronic.pdf)를 참조하십시오.

Target은 귀하의 동의 관리 전략을 지원하기 위한 Adobe Experience Platform을 통한 옵트인 기능 지원을 제공하지 않습니다. 선택 기능을 통해 고객이 Target 태그를 실행하는 방법과 시기를 제어할 수 있습니다. 또한 Adobe Experience Platform을 통해 Target 태그를 사전 승인할 수 있는 옵션이 있습니다. Adobe Experience Platform을 사용하여 옵트인을 관리하는 것이 좋습니다. Target 실행 전에 동의 전략의 일부로 유용하게 사용할 수 있는 페이지에서 선택한 요소를 숨기기 위한 세부적인 제어 기능이 Adobe Experience Platform에 추가로 있습니다.

GDPR, CCPA 및 Adobe Experience Platform에 대한 자세한 내용은 [Adobe 개인 정보 보호 JavaScript 라이브러리 및 GDPR](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html?). 또한 위의 *Adobe Target 및 Adobe Experience Platform 옵트인* 섹션을 참조하십시오.

### `AdobePrivacy.js`가 GDPR API에 정보를 제출합니까?

AdobePrivacy.js는 API에 이 정보를 제출하지 *않습니다*. 정보 제출은 고객이 직접 해야 합니다. 이 라이브러리는 브라우저에 저장된 해당 방문자에 대한 ID만 제공합니다.

### `removeIdentities`는 무엇을 제거합니까?

`removeIdentities`*는 브라우저에서 이러한 ID만을* 제거하며 Adobe 솔루션이 이를 구현했는지 여부에 따라 다릅니다.

예를 들어 Target은 해당 ID를 저장하는 쿠키를 삭제하지만, Adobe Audience Manager(AAM)은 서드파티 쿠키에 저장된 Demdex ID를 삭제하지 않습니다.

### Target GDPR 또는 CCPA 요청에 포함해야 하는 정보는 무엇입니까?

중앙 Privacy Service의 요구 사항 외에 Target에 유효한 GDPR 또는 CCPA 메시지는 다음과 같습니다.

```
{ 
    "jobId":"12345AD43E", 
    ... 
    "products":["Target",...], 
    "companyContexts":[ 
        { 
            "namespace":"imsOrgID", 
            "value":"123456789@AdobeOrg" 
        }, 
        ... 
    ], 
    "userContexts":[ 
        { 
            "namespace":"ECID", 
            "namespaceId":4, 
            "type":"standard", 
            "value":"53792210477379708453829363835595041181" 
        } 
        And/OR: 
        { 
            "namespace":"TNTID", 
            "namespaceId":9, 
            "type":"standard", 
            "value":"1234567890" 
        } 
        And/OR: 
        { 
            "namespace":"THIRDPARTYID", 
            "type":"target", 
            "value":"thirdPartyIdName" 
        }, 
        ... 
    ] 
}
```

### GDPR API를 통해 Target에서 예상할 수 있는 응답 유형은 무엇입니까?

| 요청 상태 | Target 응답 메시지 | 시나리오 |
|--- |--- |--- |
| 처리 중 | 처리 중 | Target이 GDPR 또는 CCPA 요청을 받아서 처리 중입니다. |
| 완료 | 적용할 수 없음 - 회사 컨텍스트를 적용할 수 없음 | GDPR 또는 CCPA 요청의 IMS ID가 Target 클라이언트에 매핑되지 않습니다.<br />일부 회사는 다수의 IMS ID를 보유하고 있습니다. Target이 프로비저닝되는 위치에 IMS ID를 제출합니다. |
| 완료 | 적용할 수 없음 - 사용자 컨텍스트를 찾을 수 없음 | 특정 방문자 또는 데이터 주제에 대한 GDPR 또는 CCPA 요청에 제공된 ID가 Target 프로필 저장소에 없습니다.<br />또한 이 결과는 Target에서 지원하지 않는 네임스페이스 ID 유형을 제출하려고 하는 경우 반환됩니다(지원되는 ID는 위 참조). |
| 오류 | 오류 메시지(세부 사항은 오류 유형에 따라 다름) | 요청한 데이터 주제 프로필을 가져오거나 삭제하는 중에 오류가 발생했습니다.<br />액세스 요청을 위해 Azure에 업로드하는 동안 오류가 발생했습니다. |

### Target은 액세스 요청에 대해 GDPR API로 어떤 응답을 보냅니까?

데이터 액세스 요청에 대한 응답에는 해당 방문자에 대한 Target 프로필의 요약이 포함되어 있습니다. 이 반환은 Experience Cloud GDPR API로 전송되며, 이는 데이터 제어자에 응답을 전송합니다.

다음은 샘플 Target 액세스 API 응답입니다.

```
{ 
    "jobId":"12345AD43E", 
    ... 
    "products":["Target",...], 
    "companyContexts":[ 
        { 
            "namespace":"imsOrgID", 
            "value":"123456789@AdobeOrg" 
        }, 
        ... 
    ], 
    "userContexts":[ 
        { 
            ~"namespace":"ECID", 
            "namespaceId":4, 
            "type":"standard", 
            "value":"53792210477379708453829363835595041181" 
        } 
        And/OR: 
        { 
            ~"namespace":"tntId", 
            "namespaceId":9, 
            "type":"standard", 
            "value":"1234567890" 
        } 
        And/OR: 
        { 
            "namespace":"thirdPartyId", 
            "type":"target", 
            "value":"thirdPartyIdName" 
        }, 
        ... 
    ] 
} 
```

| 필드 | 설명 |
|--- |--- |
| jobId | 중앙 GDPR API의 GDPR 또는 CCPA 작업 ID를 나타냅니다. |
| imsOrgID | 회사에 대한 고유 식별자를 제공합니다. |
| namespace | 데이터 소스라고도 합니다. 이 주제에서 &quot;고객이 Target에 대한 GDPR 또는 CCPA 액세스 및 삭제 요청을 완료할 수 있도록 지원되는 ID는 무엇입니까?&quot;를 참조하십시오. |
| 유형 | GDPR 또는 CCPA 데이터 액세스를 요청한 ID의 유형입니다. Target은 몇 가지 ID 유형을 허용하며, 그 중 일부는 표준 유형이고 일부는 Target 관련 유형입니다. 이 주제에서 &quot;고객이 Target에 대한 GDPR 또는 CCPA 액세스 및 삭제 요청을 완료할 수 있도록 지원되는 ID는 무엇입니까?&quot;를 참조하십시오. |
| value | 네임스페이스/데이터 소스의 ID입니다. 이 주제에서 &quot;고객이 Target에 대한 GDPR 또는 CCPA 액세스 및 삭제 요청을 완료할 수 있도록 지원되는 ID는 무엇입니까?&quot;를 참조하십시오. |
| 통합 코드 | 통합 코드는 데이터 소스의 친숙한 이름이며, 데이터 소스 ID를 사용하는 것보다 쉽게 데이터 소스를 추적하는 데 도움이 됩니다. |

프로필을 식별하기 위해 여러 값이 제공된 경우 유효한 식별자마다 하나의 프로필 파일을 갖습니다. 하나 이상의 프로필 파일이 Target 프로필 JSON 응답의 형식으로 GDPR 중앙 API를 통해 중앙 GDPR Azure Blob에 전송됩니다.

샘플 Target 프로필 JSON 형식은 다음 예제와 비슷합니다.

```
{"profileAttributes": 
 
"Sample_Parameter":{"value":"Gold Loyalty Status","modifiedAt":"2018-04-11T21:44:14.000-04:00"}, 
 
"user.ReturnTimeOfDay":{"value":"44.0","modifiedAt":"2018-04-11T21:44:14.000-04:00"}, 
 
"firstSessionStart":{"value":"1523497450602","modifiedAt":"2018-04-11T21:44:10.000-04:00"}, 
 
"user.sessionCountScript":{"value":"1","modifiedAt":"2018-04-11T21:44:14.000-04:00"} 
   } 
} 
```

다음 표에서는 설명용 프로필 JSON 필드를 설명합니다.

| 필드 | 설명 |
|--- |--- |
| Sample_Parameter | Target 프로필의 정보 중 다수는 데이터 관리자가 업로드하거나 직접 제공합니다. 이 예에서는 프로필 업데이트 API를 사용하여 Target 프로필에 매개 변수가 업로드되었습니다. 자세한 내용은 [데이터를 Target으로 가져오는 방법](/help/dev/before-implement/methods-to-get-data-into-target/methods-to-get-data-into-target.md)을 참조하십시오. |
| user.ReturnTimeOfDay | 이 표준 필드에는 사용자가 가장 최근에 다시 방문한 시간이 포함되어 있습니다. |
| firstSessionStart | 이 표준 필드에는 사용자의 첫 번째 세션이 시작된 시간이 포함됩니다. |
| user.sessionCountScript | Target 프로필의 정보 중 다수는 데이터 관리자가 업로드하거나 직접 제공합니다. 이 예에서 프로필 스크립트는 이 방문자가 데이터 관리자의 사이트에 대해 수행한 세션의 수를 증가시키고 있습니다. 자세한 내용은 [프로필 스크립트 속성](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html)을 참조하십시오. |

>[!NOTE]
>
>이 코드 샘플은 illustration용 Target 프로필 JSON의 축약된 버전입니다. Target 프로필의 여러 필드는 표준이 아닙니다. 반환되는 내용은 해당 방문자 프로필에 포함된 정보에 따라 다릅니다.

### Target이 IP 난독화를 지원합니까?

Target은 사용자가 IP 난독화를 GDPR 또는 CCPA 구현 전략의 일부로 사용하도록 선택하는 경우 유사 IP 탐지를 지원합니다. 자세한 내용은 [개인 정보](privacy.md/#replacement-of-last-octet-of-ip-addresses)를 참조하십시오.

### 데이터가 서드파티로 공유되거나 판매되는 것을 방지하기 위해 수행해야 하는 작업이 있습니까?

Target은 고객이 Target에서 서드파티로 직접 데이터를 공유하거나 판매하는 것을 허용하지 않으므로, Target에 대한 판매 옵트아웃은 발생하지 않습니다.
