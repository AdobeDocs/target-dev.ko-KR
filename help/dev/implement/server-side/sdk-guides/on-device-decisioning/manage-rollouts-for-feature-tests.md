---
title: 기능 테스트에 대한 롤아웃 관리
description: 다음을 사용하여 기능 테스트에 대한 롤아웃을 관리하는 방법 알아보기 [!UICONTROL 온디바이스 의사 결정].
feature: APIs/SDKs
exl-id: caa91728-6ac0-4583-a594-0c8fe616342d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# 기능 테스트에 대한 롤아웃 관리

## 단계 요약

1. 사용 [!UICONTROL 온디바이스 의사 결정] (조직)
1. 만들기 [!UICONTROL A/B 테스트] 활동
1. 기능 및 롤아웃 설정 정의
1. 응용 프로그램에서 기능 구현 및 렌더링
1. 애플리케이션의 이벤트에 대한 추적 구현
1. A/B 활동 활성화
1. 필요에 따라 롤아웃 및 트래픽 할당 조정

## 1. 활성화 [!UICONTROL 온디바이스 의사 결정] (조직)

온디바이스 의사 결정을 활성화하면 A/B 활동이 거의 0에 가까운 지연 시간에 실행됩니다. 이 기능을 사용하려면 다음 위치로 이동하십시오. **[!UICONTROL 관리]** > **[!UICONTROL 구현]** > **[!UICONTROL 계정 세부 정보]** 위치: [!DNL Adobe Target], 및 활성화 **[!UICONTROL 온디바이스 의사 결정]** 토글.

![대체 이미지](assets/asset-odd-toggle.png)

>[!NOTE]
>
>관리자 또는 승인자가 있어야 합니다. [사용자 역할](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) 을(를) 활성화 또는 비활성화하려면 [!UICONTROL 온디바이스 의사 결정] 토글.

활성화 후 [!UICONTROL 온디바이스 의사 결정] 전환, [!DNL Adobe Target] 생성 시작 *규칙 아티팩트* 클라이언트.

## 2. 만들기 [!UICONTROL A/B 테스트] 활동

1. 위치 [!DNL Adobe Target]로 이동한 다음 **[!UICONTROL 활동]** 페이지를 선택한 다음 **[!UICONTROL 활동 만들기]** > **[!UICONTROL A/B 테스트]**.

   ![대체 이미지](assets/asset-ab.png)

1. 다음에서 **[!UICONTROL A/B 테스트 활동 만들기]** 모달, 기본값 유지 **[!UICONTROL 웹]** 옵션 선택됨 (1), 선택 **[!UICONTROL 양식]** 경험 작성기 (2)로서 **[!UICONTROL 기본 작업 영역]** 포함 **[!UICONTROL 속성 제한 없음]** (3) 및 클릭 **[!UICONTROL 다음]** (4)

   ![대체 이미지](assets/asset-form.png)

## 3. 기능 및 롤아웃 설정 정의

다음에서 **[!UICONTROL 경험]** 활동 만들기 단계에서 활동의 이름을 입력합니다(1). 기능에 대한 롤아웃을 관리할 애플리케이션 내의 위치 이름(2)을 입력합니다. 예를 들어,  `ondevice-rollout` 또는 `homepage-addtocart-rollout` 는 기능 롤아웃 관리 대상을 나타내는 위치 이름입니다. 아래 표시된 예에서는 `ondevice-rollout` 은 경험 A에 대해 정의된 위치입니다. 선택적으로 대상 세분화(4)를 추가하여 활동에 대한 자격을 제한할 수 있습니다.

![대체 이미지](assets/asset-location-rollout.png)

1. 다음에서 **[!UICONTROL 콘텐츠]** 동일한 페이지의 섹션에서 다음을 선택합니다. **[!UICONTROL JSON 오퍼 만들기]** (1)을 클릭합니다.

   ![대체 이미지](assets/asset-offer.png)

1. 다음에서 **[!UICONTROL JSON 데이터]** 표시되는 텍스트 상자에 유효한 JSON 개체 (2)를 사용하여 경험 A (1)에서 이 활동으로 롤아웃하려는 기능에 대한 기능 플래그 변수를 입력합니다.

   ![대체 이미지](assets/asset-json-a-rollout.png)

1. 클릭 **[!UICONTROL 다음]** (1) (으)로 이동 **[!UICONTROL 타겟팅]** 활동 만들기 단계입니다.

   ![대체 이미지](assets/asset-next-2-t-rollout.png)

1. 다음에서 **[!UICONTROL 타겟팅]** 단계, 유지 **[!UICONTROL 모든 방문자]** 대상 (1), 단순함. 하지만 트래픽 할당 (2)를 10%로 조정합니다. 이렇게 하면 사이트 방문자의 10%로만 기능이 제한됩니다. 다음(3)을 클릭하여 로 이동합니다. **[!UICONTROL 목표 및 설정]** 단계.

   ![대체 이미지](assets/asset-next-2-g-rollout.png)

1. 다음에서 **[!UICONTROL 목표 및 설정]** 단계, 선택 **[!UICONTROL Adobe Target]** (1)을(를) (으)로 **[!UICONTROL 보고 소스]** 에서 활동 결과를 보려면 [!DNL Adobe Target] UI.

1. 선택 **[!UICONTROL 목표 지표]** 활동을 측정합니다. 이 예에서 성공적인 전환은 사용자가 orderConfirm (2) 위치에 도달했는지 여부에 의해 표시된 대로 사용자가 항목을 구매했는지 여부를 기반으로 합니다.

1. 클릭 **[!UICONTROL 저장 및 닫기]** (3) 활동을 저장합니다.

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
