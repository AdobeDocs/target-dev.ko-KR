---
title: ' [!DNL Adobe Target] .NET SDK의 이벤트 구독'
description: '[!UICONTROL OnDeviceDecisioningHandler] 개체를 사용하여 .NET SDK 내에서 발생하는 다양한 이벤트를 구독하는 방법에 대해 알아봅니다.'
feature: APIs/SDKs
exl-id: 7578033f-3de5-4d13-9739-46ad1269ec5f
TQID: https://experienceleague.adobe.com/oeGknU-pW1-XjVrxn8JNEPoFBF8Gntt-vaVnqjdyTC8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 120
ht-degree: 5%

---

# SDK 이벤트(.NET)

## 설명

[SDK을 초기화](initialize-sdk.md)할 때 선택적 `OnDeviceDecisioningReady` 대리자를 `TargetClientConfig` 개체에 제공할 수 있습니다. 이 대리자는 SDK에서 장치 내 메서드 호출을 수행할 준비가 되었을 때 호출됩니다. [!UICONTROL on-device decisioning] 아티팩트 다운로드를 처리하는 데 사용할 수 있는 다른 대리자도 두 명 있습니다.

## 이벤트

특정 이벤트에 대해 다음 위임을 구성할 수 있습니다.

| 이름 | 인수 | 설명 |
| --- | --- | --- |
| OnDeviceDecisionReady | 없음 | 클라이언트가 [!UICONTROL on-device decisioning]에 대해 처음 준비될 때 한 번만 호출됩니다. |
| ArtifactDownloadSucceeded | 아티팩트 파일의 문자열 내용 | [!UICONTROL on-device decisioning] 아티팩트가 다운로드될 때마다 호출됩니다. |
| ArtifactDownloadFailed | 예외 | [!UICONTROL on-device decisioning] 아티팩트를 다운로드하지 못할 때마다 호출됩니다. |

## 예

### \.NET

```dotnet {line-numbers="true"}
var clientConfig = new TargetClientConfig.Builder("acmeclient", "1234567890@AdobeOrg")
    .SetDecisioningMethod(DecisioningMethod.OnDevice)
    .SetOnDeviceDecisioningReady(DecisioningReady)
    .SetArtifactDownloadSucceeded(artifact => Console.WriteLine("The artifact was successfully downloaded. Contents: " + artifact))
    .SetArtifactDownloadFailed(exception => Console.WriteLine("The artifact failed to download. Exception: " + exception.Message))
    .Build();

var targetClient = TargetClient.Create(clientConfig);

// ...

static void DecisioningReady()
{
    var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

    var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
        .SetExecute(new ExecuteRequest(mboxes: mboxRequests))
        .Build();

    var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
}
```
