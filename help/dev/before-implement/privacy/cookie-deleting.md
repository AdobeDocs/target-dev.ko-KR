---
keywords: 쿠키, 쿠키, 쿠키 삭제, 삭제 [!DNL Target] cookie, google chrome, chrome, mozilla firefox, firefox, microsoft edge, safari, cookie1
description: 환경을 확인할 수 있도록  [!DNL Target] 브라우저 쿠키를 삭제하는 방법을 알아봅니다.
title: ' [!DNL Target] 쿠키를 삭제하려면 어떻게 해야 합니까?'
feature: Privacy & Security
exl-id: c975c47f-8d81-4abe-aa89-f65275a73002
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 3%

---

# [!DNL Target] 쿠키 삭제

테스트 중에 모든 경험의 유효성을 검사할 수 있도록 [!DNL Adobe Target] 브라우저 쿠키(mbox)를 삭제할 수 있습니다.

[!DNL Target] 쿠키(mbox)가 없으면 새 방문자로 간주되어 새 경험을 표시합니다. 모든 브라우저 쿠키를 삭제하지 않고 mbox를 삭제하는 몇 가지 방법이 있습니다.

>[!NOTE]
>
>나열된 브라우저 및 버전에 대해 다음 지침이 올바릅니다. 특정 브라우저 또는 버전에 대한 지침을 보려면 인터넷을 검색하십시오.

## Google Chrome에서 [!DNL Target] 쿠키 삭제

버전 84.0.4147.105

1. **[!UICONTROL Chrome]** 메뉴 > **[!UICONTROL Preferences]**&#x200B;을(를) 클릭합니다.
1. **[!UICONTROL Privacy and Security]** 탭을 클릭합니다.
1. **[!UICONTROL Cookies and other site data]** 아이콘을 클릭합니다.
1. **[!UICONTROL See all cookies and site data]** 아이콘을 클릭합니다.
1. `adobe.com` 섹션을 확장하고 **mbox** 쿠키를 선택한 다음 삭제 아이콘(X)을 클릭합니다.

## Mozilla Firefox에서 [!DNL Target] 쿠키를 삭제합니다.

버전 79.0

### `adobe.com`과(와) 연결된 모든 쿠키 삭제

1. **[!UICONTROL Firefox]** 메뉴 > **[!UICONTROL Preferences]**&#x200B;을(를) 클릭합니다.
1. **[!UICONTROL Privacy and Security]** 탭을 클릭합니다.
1. **쿠키 및 사이트 데이터*&#x200B;에서 **[!UICONTROL Manage Data]**&#x200B;을(를) 클릭합니다.
1. `adobe.com` 사이트를 선택한 다음 **[!UICONTROL Remove Selected]**&#x200B;을(를) 클릭합니다.

>[!WARNING]
>
>`adobe.com` 사이트와 연결된 모든 쿠키가 삭제됩니다. 사이트에 대한 개별 쿠키를 삭제하려면 아래 지침을 따르십시오.

### 개별 쿠키(mbox) 삭제

1. Firefo에서 **[!UICONTROL Tools]** > **[!UICONTROL Web Developer]** > **[!UICONTROL Storage Inspector]**&#x200B;을(를) 클릭합니다.
1. **[!UICONTROL Advanced]** 탭을 클릭합니다.
1. 삭제할 쿠키가 있는 웹 페이지로 이동합니다.
1. **[!UICONTROL Cookies]** 섹션을 확장한 다음 `https://experience.adobe.com`을(를) 클릭합니다.
1. **[!UICONTROL mbox]** 쿠키를 마우스 오른쪽 단추로 클릭한 다음 **[!UICONTROL Delete]**&#x200B;을(를) 클릭합니다.

## Microsoft Edge에서 [!DNL Target] 쿠키 삭제

버전 84.0.522.52

1. **[!UICONTROL Microsoft Edge]** 메뉴 > **[!UICONTROL Preferences]**&#x200B;을(를) 클릭합니다.
1. **[!UICONTROL Site Permissions]** 탭을 클릭합니다.
1. **[!UICONTROL Cookies and site data]** 아이콘을 클릭합니다.
1. **[!UICONTROL See all cookies and site data]** 아이콘을 클릭합니다.
1. `adobe.com` 섹션을 확장하고 **mbox** 쿠키를 선택한 다음 삭제 아이콘(X)을 클릭합니다.

## Apple Safari에서 [!DNL Target] 쿠키 삭제

버전 13.1.2

### `adobe.com`과(와) 연결된 모든 쿠키 삭제

1. **[!UICONTROL Safari]** 메뉴 > **[!UICONTROL Preferences]**&#x200B;을(를) 클릭합니다.
1. **[!UICONTROL Privacy]** 탭을 클릭합니다.
1. **[!UICONTROL Manage Website Data]** 아이콘을 클릭합니다.
1. 삭제할 쿠키의 사이트를 선택한 다음 **[!UICONTROL Remove]**&#x200B;을(를) 클릭합니다.

>[!WARNING]
>
>`adobe.com` 사이트와 연결된 모든 쿠키가 삭제됩니다. 사이트에 대한 개별 쿠키를 삭제하려면 아래 지침을 따르십시오.

### 개별 쿠키(mbox) 삭제

1. **[!UICONTROL Safari]** 메뉴 > **[!UICONTROL Preferences]**&#x200B;을(를) 클릭합니다.
1. **[!UICONTROL Advanced]** 탭을 클릭합니다.
1. **[!UICONTROL Show Develop menu in menu bar]** 옵션을 선택하십시오.
1. 삭제할 쿠키가 있는 웹 페이지로 이동합니다.
1. **[!UICONTROL Develop]** 메뉴 > **[!UICONTROL Show Web Inspector]**&#x200B;을(를) 클릭합니다.
1. **[!UICONTROL Storage]** 탭을 클릭합니다.
1. **[!UICONTROL Cookies]** 섹션을 확장한 다음 `www.adobe.com`을(를) 클릭합니다.
1. **mbox** 쿠키를 마우스 오른쪽 단추로 클릭한 다음 **[!UICONTROL Delete]**&#x200B;을(를) 클릭합니다.
