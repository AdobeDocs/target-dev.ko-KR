---
title: 에서 이벤트 구독 [!DNL Adobe Target] .NET SDK
description: .NET SDK 내에서 발생하는 다양한 이벤트에 가입하는 방법에 대해 알아봅니다. [!UICONTROL OnDeviceDecisioningHandler] 개체.
feature: APIs/SDKs
exl-id: 7578033f-3de5-4d13-9739-46ad1269ec5f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 5%

---

# SDK 이벤트(.NET)

## 설명

날짜 [sdk 초기화](initialize-sdk.md), 선택 사항 `OnDeviceDecisioningReady` 위임은 다음에서 제공할 수 있습니다. `TargetClientConfig` 개체. SDK가 디바이스에서 메서드 호출을 수행할 준비가 되면 호출됩니다. 두 명의 다른 위임자도 이 작업을 처리할 수 있습니다. [!UICONTROL 온디바이스 의사 결정] 아티팩트 다운로드.

## 이벤트

특정 이벤트에 대해 다음 위임을 구성할 수 있습니다.

| 이름 | 인수 | 설명 |
| --- | --- | --- |
| OnDeviceDecisioningReady | 없음 | 클라이언트가 처음 다음에 대해 준비될 때 한 번만 호출됩니다. [!UICONTROL 온디바이스 의사 결정] |
| ArtifactDownloadSucceeded | 아티팩트 파일의 문자열 내용 | 다음에 대해 호출될 때마다 [!UICONTROL 온디바이스 의사 결정] 아티팩트가 다운로드됨 |
| ArtifactDownloadFailed | 예외 | 를 다운로드하지 못할 때마다 호출됩니다. [!UICONTROL 온디바이스 의사 결정] 아티팩트 |

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
