---
title: Target SDK 시작하기
description: Adobe Target SDK를 사용하려면 어떻게 합니까?
feature: APIs/SDKs
exl-id: a5ae9826-7bb5-41de-8796-76edc4f5b281
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---

# [!DNL Target]개의 SDK 시작

시작하고 실행하려면 선택한 언어로 첫 번째 [장치 내 의사 결정](../on-device-decisioning/overview.md) 기능 플래그 활동을 만드는 것이 좋습니다.

* Node.js
* Java
* .NET
* Python

## 단계 요약

1. 조직에 대해 온디바이스 의사 결정 활성화
1. SDK 설치
1. SDK 초기화
1. [!DNL Adobe Target] [!UICONTROL A/B Test] 활동에서 기능 플래그 설정
1. 응용 프로그램에서 기능 구현 및 렌더링
1. 애플리케이션의 이벤트에 대한 추적 구현
1. [!UICONTROL A/B Test] 활동 활성화

## 1. 조직에 대해 온디바이스 의사 결정 사용

디바이스에서 의사 결정을 사용하면 [!UICONTROL A/B Test] 활동이 거의 0에 가까운 대기 시간에 실행됩니다. 이 기능을 사용하려면 **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]**(으)로 이동하여 **[!UICONTROL On-Device Decisioning]** 토글을 활성화하십시오.

![대체 이미지](assets/asset-odd-toggle.png)

>[!NOTE]
>
>**[!UICONTROL On-Device Decisioning]** 전환을 활성화하거나 비활성화하려면 **[!UICONTROL Admin]** 또는 **[!UICONTROL Approver]** [사용자 역할](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html)이(가) 있어야 합니다.

**[!UICONTROL On-Device Decisioning]** 전환을 활성화한 후 [!DNL Adobe Target]에서 클라이언트에 대한 [규칙 아티팩트](../on-device-decisioning/rule-artifact-overview.md)를 생성하기 시작합니다.

## 2. SDK 설치

Node.js, Java 및 Python의 경우 터미널의 프로젝트 디렉터리에서 다음 명령을 실행합니다. .NET의 경우 [NuGet에서 설치](https://www.nuget.org/packages/Adobe.Target.Client)하여 종속성으로 추가하십시오.

>[!BEGINTABS]

>[!TAB NPM(Node.js)]

```js {line-numbers="true"}
npm i @adobe/target-nodejs-sdk -P
```

>[!TAB Java(Maven)]

```javascript {line-numbers="true"}
<dependency>
   <groupId>com.adobe.target</groupId>
   <artifactId>java-sdk</artifactId>
   <version>2.0</version>
</dependency>
```

>[!TAB .NET(Bash)]

```bash {line-numbers="true"}
dotnet add package Adobe.Target.Client
```

>[!TAB Python(pip)]

```python {line-numbers="true"}
pip install target-python-sdk
```

>[!ENDTABS]

## 3. SDK 초기화

규칙 아티팩트는 SDK 초기화 단계 중에 다운로드됩니다. 초기화 단계를 사용자 정의하여 아티팩트가 다운로드되고 사용되는 방법을 결정할 수 있습니다.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
   client: "<your target client code>",
   organizationId: "your EC org id",
   decisioningMethod: "on-device",
   events: {
      clientReady: targetClientReady
      }
};

const tClient = TargetClient.create(CONFIG);

function targetClientReady() {
   //Adobe Target SDK has now downloaded the JSON artifact locally, which contains the activity details.
   //We will see how to use the artifact here very soon.
}
```

>[!TAB Java(Maven)]

```javascript {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
   .client("testClient")
   .organizationId("ABCDEF012345677890ABCDEF0@AdobeOrg")
   .build();
TargetClient targetClient = TargetClient.create(config);
```

>[!TAB .NET(C#)]

```csharp {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("testClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
   .Build();
this.targetClient.Initialize(targetClientConfig);
```

>[!TAB Python]

```python {line-numbers="true"}
from target_python_sdk import TargetClient

def target_client_ready():
   # Adobe Target SDK has now downloaded the JSON artifact locally, which contains the activity details.
   # We will see how to use the artifact here very soon.

CONFIG = {
   "client": "<your target client code>",
   "organization_id": "your EC org id",
   "decisioning_method": "on-device",
   "events": {
      "client_ready": target_client_ready
   }
}

target_client = TargetClient.create(CONFIG)
```

>[!ENDTABS]

## 4. [!DNL Adobe Target] [!UICONTROL A/B Test] 활동에서 기능 플래그를 설정합니다

1. [!DNL Target]에서 **[!UICONTROL Activities]** 페이지로 이동한 다음 **[!UICONTROL Create Activity]** > **[!UICONTROL A/B test]**&#x200B;을(를) 선택합니다.

   ![대체 이미지](assets/asset-ab.png)

1. **[!UICONTROL Create A/B Test Activity]** 모달에서 기본 웹 옵션을 선택한 상태로 둡니다(1). **[!UICONTROL Form]**&#x200B;을(를) 경험 작성기로 선택합니다(2). **[!UICONTROL No Property Restrictions]**(3)을(를) 사용하여 **[!UICONTROL Default Workspace]**&#x200B;을(를) 선택한 다음 **[!UICONTROL Next]**(4)을(를) 클릭합니다.

   ![대체 이미지](assets/asset-form.png)

1. 활동을 만드는 **[!UICONTROL Experiences]** 단계에서 **[!UICONTROL Add Experience]**(2)을(를) 클릭하여 활동의 이름(1)을 입력하고 두 번째 경험인 경험 B를 추가합니다. 선택한 위치 이름을 입력합니다(3). 예를 들어 `ondevice-featureflag` 또는 `homepage-addtocart-featureflag`은(는) 기능 플래그 테스트의 대상을 나타내는 위치 이름입니다.  아래 예제에서 `ondevice-featureflag`은(는) 경험 B에 대해 정의된 위치입니다. 필요에 따라 대상 세분화(4)를 추가하여 활동에 대한 자격을 제한할 수 있습니다.

   ![대체 이미지](assets/asset-location.png)

1. 같은 페이지의 **[!UICONTROL CONTENT]** 섹션에서 아래와 같이 드롭다운(1)의 **[!UICONTROL Create JSON Offer]**&#x200B;을(를) 선택합니다.

   ![대체 이미지](assets/asset-offer.png)

1. 표시되는 **[!UICONTROL JSON Data]** 텍스트 상자에 유효한 JSON 개체(2)를 사용하여 각 경험(1)에 대한 기능 플래그 변수를 입력합니다.

   경험 A에 대한 기능 플래그 변수를 입력합니다.

   ![대체 이미지](assets/asset-json_a.png)

   **(경험 A에 대한 샘플 JSON, 이상)**

   ```json {line-numbers="true"}
   {
      "enabled" : true,
      "flag" : "expA"
   }
   ```

   경험 B에 대한 기능 플래그 변수를 입력합니다.

   ![대체 이미지](assets/asset-json_b.png)

   **(경험 B에 대한 샘플 JSON, 이상)**

   ```json {line-numbers="true"}
   {
      "enabled" : true,
      "flag" : "expB"
   }
   ```

1. **[!UICONTROL Next]**(1)을(를) 클릭하여 **[!UICONTROL Targeting]** 활동 만들기 단계로 진행합니다.

   ![대체 이미지](assets/asset-next_2_t.png)

1. 아래 표시된 **[!UICONTROL Targeting]** 단계 예제에서 대상 타깃팅(2)은 단순성을 위해 모든 방문자의 기본 세트에 남아 있습니다. 즉, 활동이 타깃팅되지 않습니다. 그러나 참고 Adobe은 항상 프로덕션 활동의 대상을 타기팅하는 것을 권장합니다. **[!UICONTROL Next]**(3)을(를) 클릭하여 **[!UICONTROL Goals & Settings]** 활동 만들기 단계로 진행합니다.

   ![대체 이미지](assets/asset-next_2_g.png)

1. **[!UICONTROL Goals & Settings]** 단계에서 **[!UICONTROL Reporting Source]**&#x200B;을(를) **[!UICONTROL Adobe Target]**(1)(으)로 설정합니다. 사이트의 전환 지표에 따라 세부 정보를 지정하여 **[!UICONTROL Goal Metric]**&#x200B;을(를) **[!UICONTROL Conversion]**(으)로 정의합니다(2). **[!UICONTROL Save & Close]**(3)을(를) 클릭하여 활동을 저장합니다.

   ![대체 이미지](assets/asset-conv.png)

## 5. 응용 프로그램에서 기능 구현 및 렌더링

[!DNL Target]에서 기능 플래그 변수를 설정한 후 해당 변수를 사용하도록 응용 프로그램 코드를 수정하십시오. 예를 들어 애플리케이션에서 기능 플래그를 가져온 후 이를 사용하여 기능을 활성화하고 방문자가 자격을 부여받은 경험을 렌더링할 수 있습니다.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity
​
let featureFlags = {};
​
function targetClientReady() {
   tClient.getAttributes(["ondevice-featureflag"]).then(function(response) {
      const featureFlags = response.asObject("ondevice-featureflag");
      if(featureFlags.enabled && featureFlags.flag !== "expA") { //Assuming "expA" is control
         console.log("Render alternate experience" + featureFlags.flag);
      }
      else {
         console.log("Render default experience");
      }
   });
}
```

>[!TAB Java(Maven)]

```javascript {line-numbers="true"}
MboxRequest mbox = new MboxRequest().name("ondevice-featureflag").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
   .context(new Context().channel(ChannelType.WEB))
   .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
   .build();
Attributes attributes = targetClient.getAttributes(request, "ondevice-featureflag");
String flag = attributes.getString("ondevice-featureflag", "flag");
```

>[!TAB .NET(C#)]

```csharp {line-numbers="true"}
var mbox = new MboxRequest(index: 0, name: "ondevice-featureflag");
var deliveryRequest = new TargetDeliveryRequest.Builder()
   .SetContext(new Context(ChannelType.Web))
   .SetExecute(new ExecuteRequest(mboxes: new List<MboxRequest> { mbox }))
   .Build();
var attributes = targetClient.GetAttributes(request, "ondevice-featureflag");
var flag = attributes.GetString("ondevice-featureflag", "flag");
```

>[!TAB Python]

```python {line-numbers="true"}
# ... Code removed for brevity

feature_flags = {}

def target_client_ready():
   attribute_provider = target_client.get_attributes(["ondevice-featureflag"])
   feature_flags = attribute_provider.as_object(mbox_name="ondevice-featureflag")
   if feature_flags.get("enabled") and feature_flags.get("flag") != "expA": # Assuming "expA" is control
      print("Render alternate experience {}".format(feature_flags.get("flag")))
   else:
      print("Render default experience")
```

>[!ENDTABS]

## 6. 애플리케이션의 이벤트에 대한 추가 추적 구현

선택적으로 sendNotification() 함수를 사용하여 전환 추적을 위한 추가 이벤트를 보낼 수 있습니다.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity
​
//When a conversion happens
TargetClient.sendNotifications({
   targetCookie,
   "request" : {
      "notifications" : [
      {
         type: "display",
         timestamp : Date.now(),
         id: "conversion",
         mbox : {
            name : "orderConfirm"
         },
         order : {
            id: "BR9389",
            total : 98.93,
            purchasedProductIds : ["J9393", "3DJJ3"]
         }
      }
      ]
   }
})
```

>[!TAB Java(Maven)]

```javascript {line-numbers="true"}
Notification notification = new Notification();
notification.setId("conversion");
notification.setImpressionId(UUID.randomUUID().toString());
notification.setType(MetricType.DISPLAY);
notification.setTimestamp(System.currentTimeMillis());
Order order = new Order("BR9389");
order.total(98.93);
order.purchasedProductIds(["J9393", "3DJJ3"]);
notification.setOrder(order);

TargetDeliveryRequest notificationRequest =
   TargetDeliveryRequest.builder()
      .context(new Context().channel(ChannelType.WEB))
      .notifications(Collections.singletonList(notification))
      .build();

NotificationDeliveryService notificationDeliveryService = new NotificationDeliveryService();
notificationDeliveryService.sendNotification(notificationRequest);
```

>[!TAB .NET(C#)]

```csharp {line-numbers="true"}
var order = new Order
{
   Id = "BR9389",
   Total = 98.93M,
   PurchasedProductIds = new List<string> { "J9393", "3DJJ3" },
};
​
var notification = new Notification
{
   Id = "conversion",
   ImpressionId = Guid.NewGuid().ToString(),
   Type = MetricType.Display,
   Timestamp = DateTimeOffset.UtcNow.ToUnixTimeMilliseconds(),
   Order = order,
};
​
var notificationRequest = new TargetDeliveryRequest.Builder()
   .SetContext(new Context(ChannelType.Web))
   .SetNotifications(new List<Notification> {notification})
   .Build();
​
targetClient.SendNotifications(notificationRequest);
```

>[!TAB Python]

```python {line-numbers="true"}
# ... Code removed for brevity

# When a conversion happens
notification_mbox = NotificationMbox(name="orderConfirm")
order = Order(id="BR9389, total=98.93, purchased_product_ids=["J9393", "3DJJ3"])
notification = Notification(
   id="conversion",
   type=MetricType.DISPLAY,
   timestamp=1621530726000,  # Epoch time in milliseconds
   mbox=notification_mbox,
   order=order
)
notification_request = DeliveryRequest(notifications=[notification])


target_client.send_notifications({
   "target_cookie": target_cookie,
   "request" : notification_request
})
```

>[!ENDTABS]

## 7. [!UICONTROL A/B Test] 활동 활성화

1. **[!UICONTROL Activate]**(1)을(를) 클릭하여 [!UICONTROL A/B Test] 활동을 활성화합니다.

   >[!NOTE]
   >
   >이 단계를 수행하려면 **[!UICONTROL Approver]** 또는 **[!UICONTROL Publisher]** [사용자 역할](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html)이 있어야 합니다.

   ![대체 이미지](assets/asset-activate.png)
