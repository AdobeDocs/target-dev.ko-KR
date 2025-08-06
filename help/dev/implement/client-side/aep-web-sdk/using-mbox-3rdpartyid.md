---
title: mbox3rdPartyId에 대한 실시간 프로필 동기화
description: ' [!DNL Adobe Experience Platform Web SDK]에서 mbox3rdPartyId를 사용하는 방법에 대해 알아봅니다.'
keywords: 개인화;target;adobe target;renderDecisions;sendEvent;mbox3rdPartyId;
feature: AEP Web SDK
source-git-commit: 27759841c8d6a4ac4cc72e735f1dc6512c71aea5
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 4%

---

# mbox3rdPartyId란?

`mbox3rdPartyId`의 [!DNL Adobe Target]은(는) 회사의 충성도 프로그램을 위한 멤버십 ID와 같은 회사의 방문자 ID입니다.

방문자가 회사 사이트에 로그인하면 일반적으로 회사는 방문자 계정, 로열티 카드, 멤버십 번호 또는 해당 회사에 대한 기타 적용 가능한 식별자에 연결되는 ID를 만듭니다. [자세히 알아보기](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html#)

## `mbox3rdPartyId`과(와) 함께 [!DNL Platform Web SDK]을(를) 사용하는 방법

### 1단계: `Target Third Party ID Namespace` 구성

mbox 타사 ID로 사용할 ID 네임스페이스를 사용하여 `Target Third Party ID Namespace`데이터스트림[에서 ](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview)을(를) 구성합니다. [ID 네임스페이스에 대해 자세히 알아보기](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html)

![Target 타사 ID 네임스페이스 필드를 표시하는 Experience Platform UI.](/help/dev/implement/client-side/aep-web-sdk/assets/mbox3rdpartyid.png)

### 2단계: `mbox3rdpartyId`을(를) [!DNL Target]에 보내기

1단계에서 구성한 ID 네임스페이스를 사용하여 `mbox3rdpartyId` 명령의 [!DNL Target]을(를) `sendEvent`(으)로 보냅니다.
[ID 전송에 대해 자세히 알아보기](../../identity/overview.md#syncing-identities)

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
