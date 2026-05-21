---
title: mbox3rdPartyId에 대한 실시간 프로필 동기화
description: ' [!DNL Adobe Experience Platform Web SDK]에서 mbox3rdPartyId를 사용하는 방법에 대해 알아봅니다.'
keywords: 개인화;target;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
feature: AEP Web SDK
exl-id: 1c5067ef-38b3-4bf1-bd39-ea0f2cbd1074
TQID: https://experienceleague.adobe.com/Ej2sYVnBD9orRTlsMQG85JJV7dvn-9gnABDa0b8uBlM
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eeb
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 170
ht-degree: 24%

---

# mbox3rdPartyId 사용

[!DNL Adobe Target]의 `mbox3rdPartyId`은(는) 회사의 충성도 프로그램을 위한 멤버십 ID와 같은 회사의 방문자 ID입니다.

방문자가 회사 사이트에 로그인하면 일반적으로 회사는 방문자 계정, 로열티 카드, 멤버십 번호 또는 해당 회사에 대한 기타 적용 가능한 식별자에 연결되는 ID를 만듭니다. [자세히 알아보기](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html)

## [!DNL Platform Web SDK]과(와) 함께 `mbox3rdPartyId`을(를) 사용하는 방법

### 1단계: `Target Third Party ID Namespace` 구성

mbox 타사 ID로 사용할 ID 네임스페이스를 사용하여 [데이터스트림](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview)에서 `Target Third Party ID Namespace`을(를) 구성합니다. [ID 네임스페이스에 대해 자세히 알아보기](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html)

![Target 타사 ID 네임스페이스 필드를 표시하는 Experience Platform UI.](/help/dev/implement/client-side/aep-web-sdk/assets/mbox3rdpartyid.png)

### 2단계: `mbox3rdpartyId`을(를) [!DNL Target]에 보내기

1단계에서 구성한 ID 네임스페이스를 사용하여 `sendEvent` 명령의 `mbox3rdpartyId`을(를) [!DNL Target]&#x200B;(으)로 보냅니다.
[ID 전송에 대해 자세히 알아보기](/help/dev/implement/client-side/aep-web-sdk/using-mbox-3rdpartyid.md)

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Replace `ID_NAMESPACE` with the namespace you have configured in Step 1.
        {
          "id": "1234",
          "authenticatedState": "authenticated"
        }
      ]
    }
  }
});
```
