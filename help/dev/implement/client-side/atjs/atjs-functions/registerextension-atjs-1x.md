---
keywords: registerExtension, registerextension, register extension, at.js, function, function, clientCode, serverDomain, globalMboxName, globalMboxAutoCreate, timeout, registerExtension2
description: ' [!DNL Adobe Target] at.js JavaScript 라이브러리에 대해 [!UICONTROL registerExtension()] 함수를 사용하여 특정 확장을 등록하십시오. (at.js 1.x)'
title: '[!UICONTROL registerExtension()] 함수를 사용하는 방법'
feature: at.js
exl-id: 71decf00-84c5-4914-b0cd-bb061fa6265f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 69%

---

# [!UICONTROL registerExtension()] - at.js 1.x

특정 확장 기능을 등록하는 표준 방법을 제공합니다.

>[!NOTE]
>
>이 함수는 at.js 버전 1.*x*&#x200B;에만 사용할 수 있습니다. 이 함수는 at.js 2 릴리스에서 더 이상 사용되지 않습니다.*x*. 이 함수는 at.js 2.x와 함께 사용되는 경우 기본 콘텐츠를 반환합니다.

옵션 매개 변수는 필수이며 다음 구조를 갖습니다.

| 키 | 유형 | 필수 | 설명 |
|--- |--- |--- |--- |
| 이름 | 문자열 | 예 | 확장 이름입니다. |
| modules | 배열[문자열] | 예 | 요청된 모듈 이름을 나타내는 문자열 배열입니다. |
| 등록 | 함수 | 예 | 확장을 초기화 및 작성하는 데 사용되는 함수입니다. 이 함수는 모듈 배열에 따라 인수를 수신합니다. |

참고:

* 매개 변수 중 하나가 제공되지 않으면 예외가 발생합니다.
* 모듈 배열이 비어 있으면 예외가 발생합니다.

`[!UICONTROL registerExtension]`을(를) 사용하는 방법에 대한 자세한 내용과 예를 보려면 GitHub의 [Adobe Experience Cloud Target atjs 확장 프로그램](https://github.com/Adobe-Marketing-Cloud/target-atjs-extensions) 페이지를 참조하십시오.

## 설정 모듈 메서드

| 키 | 유형 | 설명 |
|--- |--- |--- |
| clientCode | 문자열 | 클라이언트 코드 |
| serverDomain | 문자열 | 에지 서버 도메인 |
| globalMboxName | 문자열 | [!DNL Target] 글로벌 mbox 이름 |
| globalMboxAutoCreate | 부울 | 자동 생성이 활성화되어 있는지를 나타냅니다. |
| timeout | 숫자 | 요청 시간 제한 |

## 로거 모듈 메서드

| 키 | 유형 | 설명 |
|--- |--- |--- |
| log | 함수 | 브라우저 콘솔에 인수의 변수 목록(있는 경우)을 로깅합니다. `mboxDebug=true`가 URL에 전달될 때만 활성화됩니다. |
| 오류 | 함수 | 브라우저 콘솔에 인수의 변수 목록을 로깅합니다. 네트워크 시간 제한, HTML 노드를 찾을 수 없음 등과 같은 심각한 오류가 있는 경우에만 활성화됩니다. |
