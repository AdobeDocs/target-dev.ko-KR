---
title: ' [!DNL Adobe Target] Java SDK에서 이벤트 구독'
description: '[!UICONTROL OnDeviceDecisioningHandler] 개체를 사용하여 Java SDK 내에서 발생하는 다양한 이벤트를 구독하는 방법에 대해 알아봅니다.'
feature: APIs/SDKs
exl-id: f2d56762-6bf7-4c6b-9c14-fb20e5cfd60d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 5%

---

# SDK 이벤트(Java)

## 설명

[SDK를 초기화](initialize-sdk.md)할 때 선택적 `OnDeviceDecisioningHandler` 개체가 `ClientConfig` 개체에 제공될 수 있습니다. SDK 내에서 발생하는 다양한 이벤트를 구독하는 데 사용할 수 있습니다. 예를 들어 `onDeviceDecisioningReady` 이벤트는 SDK에서 메서드 호출을 수행할 준비가 되었을 때 호출되는 콜백 함수와 함께 사용할 수 있습니다.

## 이벤트

`OnDeviceDecisioningHandler` 개체에 특정 이벤트에 대해 호출되는 다음 콜백이 포함되어 있습니다.

| 이름 | 인수 | 설명 |
| --- | --- | --- |
| onDeviceDecisionReady | 없음 | 클라이언트가 [!UICONTROL on-device decisioning]에 대해 처음 준비될 때 한 번만 호출됩니다. |
| artifactDownloadSucceeded | 아티팩트 파일의 바이트[] 내용 | [!UICONTROL on-device decisioning] 아티팩트가 다운로드될 때마다 호출됩니다. |
| artifactDownloadFailed | 예외 | [!UICONTROL on-device decisioning] 아티팩트를 다운로드하지 못할 때마다 호출됩니다. |

## 예

### SDK 이벤트

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .defaultDecisioningMethod(DecisioningMethod.ON_DEVICE)
        .onDeviceDecisioningHandler(new OnDeviceDecisioningHandler() {
            @Override
            public void onDeviceDecisioningReady() {
                // make getOffers requests
                makeTargetRequests();
            }

            @Override
            public void artifactDownloadSucceeded(byte[] artifactData) {
                System.out.println("The artifact was successfully downloaded.");
            }

            @Override
            public void artifactDownloadFailed(TargetClientException e) {
                System.out.println("The artifact failed to download.");
            }
        }).build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);


void makeTargetRequests() {
    List<MboxRequest> mboxRequests = new ArrayList<>();
    mboxRequests.add((MboxRequest) new MboxRequest().name("a1-serverside-ab").index(1));

    TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
            .context(new Context().channel(ChannelType.WEB))
            .execute(new ExecuteRequest().setMboxes(mboxRequests))
            .build();

    TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
}
```
