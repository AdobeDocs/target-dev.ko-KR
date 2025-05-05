---
title: 기능 테스트에 대한 롤아웃 관리
description: '[!UICONTROL on-device decisioning]을(를) 사용하여 기능 테스트에 대한 롤아웃을 관리하는 방법을 알아봅니다.'
feature: APIs/SDKs
exl-id: caa91728-6ac0-4583-a594-0c8fe616342d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# 기능 테스트에 대한 롤아웃 관리

## 단계 요약

1. 조직에 대해 [!UICONTROL on-device decisioning] 사용
1. [!UICONTROL A/B Test] 활동 만들기
1. 기능 및 롤아웃 설정 정의
1. 응용 프로그램에서 기능 구현 및 렌더링
1. 애플리케이션의 이벤트에 대한 추적 구현
1. A/B 활동 활성화
1. 필요에 따라 롤아웃 및 트래픽 할당 조정

## 1. 조직에 대해 [!UICONTROL on-device decisioning] 사용

온디바이스 의사 결정을 활성화하면 A/B 활동이 거의 0에 가까운 지연 시간에 실행됩니다. 이 기능을 사용하려면 [!DNL Adobe Target]에서 **[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]**(으)로 이동하여 **[!UICONTROL On-Device Decisioning]** 전환을 사용하도록 설정하십시오.

![대체 이미지](assets/asset-odd-toggle.png)

>[!NOTE]
>
>[!UICONTROL On-Device Decisioning] 전환을 활성화하거나 비활성화하려면 관리자 또는 승인자 [사용자 역할](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html?lang=ko)이(가) 있어야 합니다.

[!UICONTROL On-Device Decisioning] 전환을 활성화한 후 [!DNL Adobe Target]에서 클라이언트에 대한 *규칙 아티팩트*&#x200B;를 생성하기 시작합니다.

## 2. [!UICONTROL A/B Test] 활동 만들기

1. [!DNL Adobe Target]에서 **[!UICONTROL Activities]** 페이지로 이동한 다음 **[!UICONTROL Create Activity]** > **[!UICONTROL A/B test]**&#x200B;을(를) 선택합니다.

   ![대체 이미지](assets/asset-ab.png)

1. **[!UICONTROL Create A/B Test Activity]** 모달에서 기본 **[!UICONTROL Web]** 옵션을 선택한 상태로 둡니다(1). **[!UICONTROL Form]**&#x200B;을(를) 경험 작성기로 선택합니다(2). **[!UICONTROL No Property Restrictions]**(3)을(를) 사용하여 **[!UICONTROL Default Workspace]**&#x200B;을(를) 선택하고 **[!UICONTROL Next]**(4)을(를) 클릭합니다.

   ![대체 이미지](assets/asset-form.png)

## 3. 기능 및 롤아웃 설정 정의

활동 만들기 **[!UICONTROL Experiences]** 단계에서 활동의 이름을 입력합니다(1). 기능에 대한 롤아웃을 관리할 애플리케이션 내의 위치 이름(2)을 입력합니다. 예를 들어 `ondevice-rollout` 또는 `homepage-addtocart-rollout`은(는) 기능 롤아웃을 관리할 대상을 나타내는 위치 이름입니다. 아래 예제에서 `ondevice-rollout`은(는) 경험 A에 대해 정의된 위치입니다. 선택적으로 대상 세분화(4)를 추가하여 활동에 대한 자격을 제한할 수 있습니다.

![대체 이미지](assets/asset-location-rollout.png)

1. 같은 페이지의 **[!UICONTROL Content]** 섹션에서 아래와 같이 드롭다운(1)의 **[!UICONTROL Create JSON Offer]**&#x200B;을(를) 선택합니다.

   ![대체 이미지](assets/asset-offer.png)

1. 표시되는 **[!UICONTROL JSON Data]** 텍스트 상자에 유효한 JSON 개체(2)를 사용하여 경험 A(1)에서 이 활동으로 롤아웃하려는 기능에 대한 기능 플래그 변수를 입력합니다.

   ![대체 이미지](assets/asset-json-a-rollout.png)

1. **[!UICONTROL Next]**(1)을(를) 클릭하여 **[!UICONTROL Targeting]** 활동 만들기 단계로 진행합니다.

   ![대체 이미지](assets/asset-next-2-t-rollout.png)

1. **[!UICONTROL Targeting]** 단계에서는 단순성을 위해 **[!UICONTROL All Visitors]** 대상(1)을 유지합니다. 하지만 트래픽 할당 (2)를 10%로 조정합니다. 이렇게 하면 사이트 방문자의 10%로만 기능이 제한됩니다. 다음(3)을 클릭하여 **[!UICONTROL Goals & Settings]** 단계로 진행합니다.

   ![대체 이미지](assets/asset-next-2-g-rollout.png)

1. **[!UICONTROL Goals & Settings]** 단계에서 **[!UICONTROL Adobe Target]** (1)을(를) **[!UICONTROL Reporting Source]**(으)로 선택하여 [!DNL Adobe Target] UI에서 활동 결과를 봅니다.

1. 활동을 측정할 **[!UICONTROL Goal Metric]**&#x200B;을(를) 선택하십시오. 이 예에서 성공적인 전환은 사용자가 orderConfirm (2) 위치에 도달했는지 여부에 의해 표시된 대로 사용자가 항목을 구매했는지 여부를 기반으로 합니다.

1. **[!UICONTROL Save & Close]**(3)을(를) 클릭하여 활동을 저장합니다.

   ![대체 이미지](assets/asset-conv-rollout.png)

## 4. 응용 프로그램에서 기능 구현 및 렌더링

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
targetClient.getAttributes(["ondevice-rollout"]).then(function(attributes) {
      const featureFlags = attributes.asObject("ondevice-rollout");

      // Your flag variables are now available in the featureFlags object variable.
      //If you failed to qualify for the Activity, you will have an empty object.
      console.log(featureFlags);
    });
```

>[!TAB Java]

```java {line-numbers="true"}
    Attributes attrs = targetJavaClient.getAttributes(targetDeliveryRequest, "ondevice-rollout");
    Map<String, Object> featureFlags = attrs.toMboxMap("ondevice-rollout");
​
    // Your flag variables are now available in the featureFlags object variable.
    //If you failed to qualify for the Activity, you will have an empty object.
    System.out.println(featureFlags);
```

>[!ENDTABS]

## 5. 애플리케이션의 이벤트에 대한 추적 구현

응용 프로그램에서 기능 플래그 변수를 사용할 수 있게 만든 후에는 이미 응용 프로그램의 일부인 모든 기능을 활성화할 수 있습니다. 방문자가 활동에 대한 자격이 없다면 대상자로 정의된 10% 버킷의 일부로 포함되지 않았음을 의미합니다.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity

if(featureFlags.enable == "yes") { //Fell within 10% traffic
    console.log("Render Feature");
}
else {
    console.log("Disable Feature");
}

// alternatively, the getValue method could be used on the Attributes object.

if(attributes.getValue("ondevice-rollout", "enable") === "yes") { //Fell within 10% traffic
    console.log("Render Feature");
}
else {
    console.log("Disable Feature");
}
```

>[!TAB Java]

```java {line-numbers="true"}
//... Code removed for brevity
​
if("yes".equals(String.valueOf(featureFlags.get("enable")))) { //Fell within 10% traffic
    System.out.println("Render Feature");
}
else {
    System.out.println("Disable Feature");
}
​
// alternatively, the getString method could be used on the Attributes object.
​
if("yes".equals(attrs.getString("ondevice-rollout", "enable"))) { //Fell within 10% traffic
    System.out.println("Render Feature");
}
else {
    System.out.println("Disable Feature");
}
```

>[!ENDTABS]

## 6. 롤아웃 활동 활성화

![대체 이미지](assets/asset-activate-rollout.png)

## 7. 필요에 따라 롤아웃 및 트래픽 할당 조정

활동을 활성화한 후에는 언제든지 편집하여 필요에 따라 트래픽 할당을 늘리거나 줄입니다.

초기 롤아웃의 성공으로 인해 트래픽 할당이 10%에서 50%로 증가합니다.

![대체 이미지](assets/asset-adjust-rollout.png)
