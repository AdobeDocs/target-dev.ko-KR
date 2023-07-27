---
keywords: apple, ITP, 지능형 추적 방지, experience cloud id, ecid, itp
description: 다음에 대해 알아보기 [!DNL Adobe Target] 및 Safari 사용자의 개인 정보를 보호하려는 Apple ITP(Intelligent Tracking Prevention) 이니셔티브의 영향입니다.
title: 은 어떻게 합니까? [!DNL Target] Apple ITP 지원을 처리하시겠습니까?
feature: Privacy & Security
exl-id: 6deee03b-df86-4d0d-999c-b11855ddfda5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 32%

---

# Apple ITP(Intelligent Tracking Prevention) 2.x

ITP(Intelligent Tracking Prevention)는 Safari 사용자의 개인 정보를 보호하기 위한 Apple의 이니셔티브입니다. 2017년에 있었던 ITP의 첫 번째 릴리스에서는 타사 쿠키의 사용을 타깃팅했습니다. 실제로 Apple은 타사 쿠키를 완전히 차단했습니다. 타사 쿠키는 일반적으로 방문자를 추적하고 방문자 데이터를 수집하는 데 사용되기 때문에 광고 기술 및 마테크(martech) 기업의 심각한 문제 요소였습니다. 이제 Apple은 Safari 내에서 타사 쿠키가 사용되는 방법에 대해 제한 사항을 적용하려고 합니다.

이러한 ITP 버전에는 다음과 같은 제한 사항이 포함됩니다.

| 버전 | 세부 사항 |
| --- | --- |
| [ITP 2.1](https://webkit.org/blog/8613/intelligent-tracking-prevention-2-1/) | `document.cookie` API를 사용하여 브라우저에 배치된 클라이언트측 쿠키가 7일 만료로 설정됩니다.<br />2019년 2월 21일 릴리스 |
| [ITP 2.2](https://webkit.org/blog/8828/intelligent-tracking-prevention-2-2/) | 7일 만료 시간을 1일로 크게 단축했습니다.<br />2019년 4월 24일 릴리스 |
| [ITP 2.3](https://webkit.org/blog/9521/intelligent-tracking-prevention-2-3/) | localStorage 사용 또는 JavaScript 사용 등 몇 가지 해결 방법 제거 `Document.referrer property`.<br />2019년 9월 23일 릴리스<br />CNAME 클로킹 방어 기능은 Safari 14, macOS Big Sur, Catalina, Mojave, iOS 14 및 iPadOS 14에서 출시된 ITP에 적용됩니다. 서드파티 CNAME 잠금 HTTP 응답으로 만든 모든 쿠키는 7일 후에 만료되도록 설정됩니다.<br />2020년 11월 12일에 발표됩니다. |

## 나에게 어떤 영향이 있습니까? [!DNL Target] 고객?

Target은 페이지에 배포할 JavaScript 라이브러리를 제공하여 [!DNL Target] 은 방문자에게 실시간 개인화를 제공할 수 있습니다. 세 개 있습니다 [!DNL Target] JavaScript 라이브러리 at.js 1.*x*, at.js 2.*x*, [!DNL Adobe Experience Cloud Web SDK] 클라이언트 측 위치 [!DNL Target] 를 통해 방문자의 브라우저에 쿠키 `document.cookie` API. 그 결과, [!DNL Target] 쿠키는 Apple의 ITP 2.1, 2.2 및 2.3에 의해 영향을 받으며, 7일(ITP 2.1 사용) 및 1일(ITP 2.2 및 ITP 2.3 사용) 후에 만료됩니다.

Apple ITP 2.x의 영향 [!DNL Target] 다음 영역에서:

| 영향 | 세부 사항 |
| --- | --- |
| 고유 방문자 수의 잠재적 증가 | 만료 창이 7일(ITP 2.1 사용) 및 1일(ITP 2.2 및 ITP 2.3 사용)로 설정되어 있으므로 Safari 브라우저에서 발생하는 고유 방문자 수가 증가하는 것을 볼 수 있습니다. 방문자가 7일(ITP 2.1) 또는 1일(ITP 2.2 및 ITP 2.3) 이후 도메인을 재방문하는 경우, [!DNL Target] 을(를) 새로 배치해야 합니다. [!DNL Target] 만료된 쿠키 대신 도메인의 쿠키. 사용자가 동일하지만 새 [!DNL Target] 쿠키는 새 고유 방문자로 해석됩니다. |
| [!DNL Target] 활동에 대한 전환 기간 감소 | [!DNL Target] 활동의 방문자 프로필에는 의사 결정에 대해 전환 기간이 감소될 수 있습니다. [!DNL Target] 쿠키는 방문자를 식별하고 개인화를 위해 사용자 프로필 속성을 저장하는 데 사용됩니다. 주어진 [!DNL Target] 삭제된 항목에 연결되어 있던 사용자 프로필 데이터인 7일(ITP 2.1) 또는 1일(ITP 2.2 및 2.3) 이후 Safari에서 쿠키가 만료될 수 있습니다 [!DNL Target] 쿠키는 의사 결정에 사용할 수 없습니다. |
| 3rdPartyID를 기반으로 하는 프로필 스크립트 | 만료 창이 7일(ITP 2.1 사용) 및 1일(ITP 2.2 및 ITP 2.3 사용)로 설정되어 있으므로 [프로필 스크립트](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html) 3rdPartyID를 기반으로 하는 쿠키는 만료 시 작동을 중지합니다. |
| iOS 디바이스에서 QA/미리보기 URL | 만료 창이 7일(ITP 2.1 사용) 및 1일(ITP 2.2 및 ITP 2.3 사용)로 설정되어 있으므로 [QA/미리보기 URL](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) URL이 3rdPartyID 쿠키를 기반으로 하므로 만료 시 가 작동을 중지합니다. |

## 현재 [!DNL Target] 구현이 영향을 받습니까?

Experience Cloud ID(ECID) 라이브러리를 사용하는 경우 [!DNL Target] JavaScript 라이브러리, 구현은 이 문서에 나열된 방식으로 영향을 받습니다. [Safari ITP 2.1이 Adobe Experience Cloud 및 Experience Platform 고객에게 미치는 영향](https://medium.com/adobetech/safari-itp-2-1-impact-on-adobe-experience-cloud-customers-9439cecb55ac).
