---
title: ' [!DNL Adobe Target] Java SDK에서 비동기 요청을 사용하는 방법'
description: ' [!DNL Target] Java SDK가 비동기 요청을 지원하여 효과적인 대상 시간을 0으로 줄이는 방법에 대해 알아봅니다.'
feature: APIs/SDKs
exl-id: e11f8d16-76f6-4d39-822a-34a1cf7f623f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 3%

---

# 비동기 요청(Java)

## 설명

서버 측 통합의 한 가지 이점은 병렬 처리를 사용하여 서버 측에서 사용할 수 있는 엄청난 대역폭과 컴퓨팅 리소스를 활용할 수 있다는 것입니다. [!DNL Target] Java SDK는 비동기 요청을 지원하므로 유효 대상 시간을 0으로 줄일 수 있습니다.

## 지원되는 메서드

### 메서드

```javascript {line-numbers="true"}
CompletableFuture<TargetDeliveryResponse> getOffersAsync(TargetDeliveryRequest request);
CompletableFuture<ResponseStatus> sendNotificationsAsync(TargetDeliveryRequest request);
CompletableFuture<Attributes> getAttributesAsync(TargetDeliveryRequest targetRequest, String ...mboxes);
```

## 예

샘플 `Spring` 응용 프로그램 컨트롤러는 다음과 같이 표시될 수 있습니다.

### 샘플 컨트롤러

```javascript {line-numbers="true"}
@RestController
public class TargetRestController {

    @Autowired
    private TargetClient targetJavaClient;

    @GetMapping("/mboxTargetOnlyAsync")
        public TargetDeliveryResponse mboxTargetOnlyAsync(
                @RequestParam(name = "mbox", defaultValue = "server-side-mbox") String mbox,
                HttpServletRequest request, HttpServletResponse response) {
            ExecuteRequest executeRequest = new ExecuteRequest()
                    .mboxes(getMboxRequests(mbox));

            TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
                    .context(getContext(request))
                    .execute(executeRequest)
                    .cookies(getTargetCookies(request.getCookies()))
                    .build();
            CompletableFuture<TargetDeliveryResponse> targetResponseAsync =
                    targetJavaClient.getOffersAsync(targetDeliveryRequest);
            targetResponseAsync.thenAccept(tr -> setCookies(tr.getCookies(), response));
            simulateIO();
            TargetDeliveryResponse targetResponse = targetResponseAsync.join();
            return targetResponse;
        }

    /**
     * Function for simulating network calls like other microservices and database calls
     */
    private void simulateIO() {
        try {
            Thread.sleep(200L);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

}
```

이 예제에서는 Spring Bean으로 [SDK를 초기화했습니다](initialize-sdk.md). 사용 가능한 유틸리티 메서드 [가 있다고 가정합니다](utility-methods.md).

[!DNL Target] 요청이 `simulateIO` 전에 실행되며 실행될 때까지 대상 결과도 준비되어야 합니다. 그렇지 않더라도 대부분의 경우 상당한 절감 효과가 있을 것이다.
