---
keywords: 쿠키, 쿠키, 쿠키 삭제, 삭제 [!DNL Target] cookie, google chrome, chrome, mozilla firefox, firefox, microsoft edge, safari, cookie1
description: 을(를) 삭제하는 방법에 대해 알아보기 [!DNL Target] 브라우저 쿠키를 활성화하여 경험의 유효성을 검사할 수 있습니다.
title: 삭제 방법 [!DNL Target] 쿠키?
feature: Privacy & Security
exl-id: c975c47f-8d81-4abe-aa89-f65275a73002
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# 삭제 [!DNL Target] 쿠키

다음을 삭제할 수 있습니다. [!DNL Adobe Target] 테스트 중에 모든 경험의 유효성을 검사할 수 있는 브라우저 쿠키 (mbox) .

없는 경우 [!DNL Target] 쿠키(mbox): 새 방문자로 간주되고 새 경험이 표시됩니다. 모든 브라우저 쿠키를 삭제하지 않고 mbox를 삭제하는 몇 가지 방법이 있습니다.

>[!NOTE]
>
>나열된 브라우저 및 버전에 대해 다음 지침이 올바릅니다. 특정 브라우저 또는 버전에 대한 지침을 보려면 인터넷을 검색하십시오.

## 삭제 [!DNL Target] Google Chrome의 쿠키

버전 84.0.4147.105

1. 다음을 클릭합니다. **[!UICONTROL 크롬]** 메뉴 > **[!UICONTROL 환경 설정]**.
1. 다음을 클릭합니다. **[!UICONTROL 개인 정보 보호 및 보안]** 탭.
1. 클릭 **[!UICONTROL 쿠키 및 기타 사이트 데이터]**.
1. 클릭 **[!UICONTROL 모든 쿠키 및 사이트 데이터 보기]**.
1. 확장 `adobe.com` 섹션에서 **mbox** 쿠키를 누른 다음 삭제 아이콘(X)을 누릅니다.

## 삭제 [!DNL Target] mozilla Firefox의 쿠키

버전 79.0

### 과(와) 관련된 모든 쿠키 삭제 `adobe.com`

1. 다음을 클릭합니다. **[!UICONTROL Firefox]** 메뉴 > **[!UICONTROL 환경 설정]**.
1. 다음을 클릭합니다. **[!UICONTROL 개인 정보 보호 및 보안]** 탭.
1. 아래 **쿠키 및 사이트 데이터*, 클릭 **[!UICONTROL 데이터 관리]**.
1. 다음 항목 선택 `adobe.com` 사이트 를 클릭한 다음 **[!UICONTROL 선택 항목 제거]**.

>[!WARNING]
>
>이렇게 하면 와(과) 관련된 모든 쿠키가 삭제됩니다. `adobe.com` 사이트. 사이트에 대한 개별 쿠키를 삭제하려면 아래 지침을 따르십시오.

### 개별 쿠키(mbox) 삭제

1. Firefo에서 **[!UICONTROL 도구]** > **[!UICONTROL 웹 개발자]** > **[!UICONTROL Storage Inspector]**.
1. 다음을 클릭합니다. **[!UICONTROL 고급]** 탭.
1. 삭제할 쿠키가 있는 웹 페이지로 이동합니다.
1. 확장 **[!UICONTROL 쿠키]** 섹션을 클릭한 다음 `https://experience.adobe.com`.
1. 마우스 오른쪽 단추 클릭 **[!UICONTROL mbox]** 쿠키, 를 차례로 클릭합니다. **[!UICONTROL 삭제]**.

## 삭제 [!DNL Target] Microsoft Edge의 쿠키

버전 84.0.522.52

1. 다음을 클릭합니다. **[!UICONTROL Microsoft Edge]** 메뉴 > **[!UICONTROL 환경 설정]**.
1. 다음을 클릭합니다. **[!UICONTROL 사이트 권한]** 탭.
1. 클릭 **[!UICONTROL 쿠키 및 사이트 데이터]**.
1. 클릭 **[!UICONTROL 모든 쿠키 및 사이트 데이터 보기]**.
1. 확장 `adobe.com` 섹션에서 **mbox** 쿠키를 누른 다음 삭제 아이콘(X)을 누릅니다.

## 삭제 [!DNL Target] Apple Safari의 쿠키

버전 13.1.2

### 과(와) 관련된 모든 쿠키 삭제 `adobe.com`

1. 다음을 클릭합니다. **[!UICONTROL Safari]** 메뉴 > **[!UICONTROL 환경 설정]**.
1. 다음을 클릭합니다. **[!UICONTROL 개인 정보 보호]** 탭.
1. 클릭 **[!UICONTROL 웹 사이트 데이터 관리]**.
1. 삭제할 쿠키의 사이트를 선택한 다음 를 클릭합니다. **[!UICONTROL 제거]**.

>[!WARNING]
>
>이렇게 하면 와(과) 관련된 모든 쿠키가 삭제됩니다. `adobe.com` 사이트. 사이트에 대한 개별 쿠키를 삭제하려면 아래 지침을 따르십시오.

### 개별 쿠키(mbox) 삭제

1. 다음을 클릭합니다. **[!UICONTROL Safari]** 메뉴 > **[!UICONTROL 환경 설정]**.
1. 다음을 클릭합니다. **[!UICONTROL 고급]** 탭.
1. 다음 항목 선택 **[!UICONTROL 메뉴 모음에 Develop 메뉴 표시]** 옵션을 선택합니다.
1. 삭제할 쿠키가 있는 웹 페이지로 이동합니다.
1. 다음을 클릭합니다. **[!UICONTROL 개발]** 메뉴 > **[!UICONTROL 웹 검사기 표시]**.
1. 다음을 클릭합니다. **[!UICONTROL 스토리지]** 탭.
1. 확장 **[!UICONTROL 쿠키]** 섹션을 클릭한 다음 `www.adobe.com`.
1. 마우스 오른쪽 단추 클릭 **mbox** 쿠키, 를 차례로 클릭합니다. **[!UICONTROL 삭제]**.
