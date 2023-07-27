---
title: 에서 이벤트 구독 [!DNL Adobe Target] Java SDK
description: 를 사용하여 Java SDK 내에서 발생하는 다양한 이벤트에 가입하는 방법을 알아봅니다. [!UICONTROL OnDeviceDecisioningHandler] 개체.
feature: APIs/SDKs
exl-id: f2d56762-6bf7-4c6b-9c14-fb20e5cfd60d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 4%

---

# SDK 이벤트(Java)

## 설명

날짜 [sdk 초기화](initialize-sdk.md), 선택 사항 `OnDeviceDecisioningHandler` 개체에서 다음 작업을 수행할 수 있습니다 `ClientConfig` 개체. SDK 내에서 발생하는 다양한 이벤트를 구독하는 데 사용할 수 있습니다. 예: `onDeviceDecisioningReady` event는 SDK가 메서드 호출을 위해 준비될 때 호출되는 콜백 함수와 함께 사용할 수 있습니다.

## 이벤트

다음 `OnDeviceDecisioningHandler` 개체에는 특정 이벤트에 대해 호출되는 다음 콜백이 포함되어 있습니다.

| 이름 | 인수 | 설명 |
| --- | --- | --- |
| onDeviceDecisionReady | 없음 | 클라이언트가 처음 다음에 대해 준비될 때 한 번만 호출됩니다. [!UICONTROL 온디바이스 의사 결정] |
| artifactDownloadSucceeded | 바이트[] 아티팩트 파일의 내용 | 다음 시간(초)마다 호출됨: [!UICONTROL 온디바이스 의사 결정] 아티팩트가 다운로드됨 |
| artifactDownloadFailed | 예외 | 를 다운로드하지 못할 때마다 호출됩니다. [!UICONTROL 온디바이스 의사 결정] 아티팩트 |

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
