---
keywords: 구현, at.js 비javascript, adbox, 리디렉터, mbox
description: AdBox 또는 리디렉터 사용과 같이 JavaScript이 아닌 시나리오에서  [!DNL Adobe Target] 을(를) 구현하는 방법에 대해 알아봅니다.
title: 이메일에 대해  [!DNL Target] 을(를) 구현하려면 어떻게 해야 합니까?
feature: Implement Email
exl-id: dda00b75-5d58-4405-ae58-75e7883a30ed
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 63%

---

# 이메일: [!DNL Target] 구현

AdBox 또는 리디렉터 사용과 같이 JavaScript 이외의 시나리오에서 [!DNL Target]을(를) 구현하는 방법에 대한 정보입니다.

광고와 다른 오프사이트 컨텐츠에 대한 방문을 추적할 수 있습니다. 사이트 내부 및 외부에서 동일한 사용자를 식별하며 전체적으로 웹에서 일관된 웹 경험을 제공할 수 있습니다. 단일 URL을 사용하는 AdBox에서는 JavaScript 또는 at.js 없이 테스트할 수 있습니다.

AdBox는 at.js가 없는 사이트(예: 계열사)에 유용합니다. 활동에 동적 크리에이티브가 필요한 경우(예를 들어 장바구니에서 중단된 광고에 제품을 표시해야 하는 경우) AdBox를 사용할 수 없습니다.

AdBox 광고 및 리디렉터는 모든 종류의 활동에 사용할 수 있습니다. 다음 표에서는 AdBox 및 리디렉터의 특징과 각각을 사용하는 시점을 비교하여 설명합니다.

| | 목적 | 사용 조건 | URL 구조 | 오퍼 유형 | 오퍼 컨텐츠 |
|--- |--- |--- |--- |--- |--- |
| AdBox | 여러 가지 이미지를 광고에 반환 | 광고 컨텐츠를 변경하기 위해 | `clientcode&#x200B;.tt.&#x200B;omtrdc&#x200B;.net/&#x200B;m2&#x200B;/&#x200B;clientcode/ubox/&#x200B;image?` | 리디렉션 오퍼 | 이미지의 URL |
| 리디렉터 | 방문자를 다른 웹 페이지로 리디렉션 | 광고의 랜딩 페이지를 변경하기 위해 | `clientcode&#x200B;.tt.omtrdc.net/&#x200B;m2/clientcode&#x200B;/ubox/page?` | 리디렉션 오퍼 | 페이지의 URL |

## 보안 모범 사례

리디렉터를 사용하면 오픈 리디렉션 취약점의 위험에 노출될 수 있습니다. 리디렉터 링크를 서드파티가 무단으로 사용하지 않도록 하려면, 기본 리디렉션 URL 도메인에 &quot;승인된 호스트&quot;를 사용하여 허용 목록에 추가하다하는 것이 좋습니다. [!DNL Target]은(는) 리디렉션을 허용할 호스트 허용 목록에 추가하다 도메인을 사용합니다. 자세한 내용은 *호스트*&#x200B;에서  [!DNL Target][&#128279;](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html#allowlist)(으)로 mbox 호출을 보내도록 승인된 호스트를 지정하는 허용 목록 만들기를 참조하십시오.

## 제한

* 표준 mbox와 같은 클라이언트측 시간 제한이 없습니다. [!DNL Target]이(가) 완전히 다운된 경우 광고 방문자는 기본값도 아닌 콘텐츠를 볼 수 없습니다.
* 타사 쿠키를 사용하여 방문을 추적합니다. PCId가 다를 경우, 기본적으로 방문자의 타사 프로필은 기존의 자사 프로필과 병합됩니다.
* AdBox 자체에서 자사 쿠키를 사용하려면 URL에 mbox 세션을 전달해야 합니다. 계정 담당자에게 이 작업을 수행하도록 요청하십시오.
* 자사 쿠키를 사용하여 광고 클릭을 추적하려면 URL에 mbox 세션을 전달합니다. 계정 담당자에게 이 작업을 수행하도록 요청하십시오.
* 동일한 페이지에서 AdBox를 두 개 이상 사용하려면 URL에 mbox 세션을 전달해야 합니다. 계정 담당자에게 이 작업을 수행하도록 요청하십시오. 리디렉터가 실제로 두 번째 페이지에 있으므로 동일한 페이지에 AdBox와 리디렉터 링크가 각각 하나씩 있을 수 있습니다.
