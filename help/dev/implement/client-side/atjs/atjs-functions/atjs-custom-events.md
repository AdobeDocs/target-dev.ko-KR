---
keywords: 사용자 지정 이벤트, at.js, 요청 실패, 요청 성공, 콘텐츠 렌더링 실패, 콘텐츠 렌더링 성공, 라이브러리 로드됨, 요청 시작, 콘텐츠 렌더링 시작, 콘텐츠 렌더링 오퍼 없음, 콘텐츠 렌더링 리디렉션, 사용자 지정 이벤트2
description: 다음에 대한 사용자 지정 이벤트 사용 [!DNL Adobe Target] mbox 요청 또는 오퍼가 실패하거나 성공하면 알림을 받을 at.js JavaScript 라이브러리입니다.
title: at.js 사용자 지정 이벤트는 어떻게 사용합니까?
feature: at.js
exl-id: a4baed9a-9eb8-4343-9834-709b03e44ca2
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 74%

---

# at.js 사용자 지정 이벤트

mbox 요청 또는 오퍼가 실패하거나 성공하는 경우를 알려주는 `at.js custom events`에 대한 정보입니다.

이전에 mbox.js(사용 중단됨)에서는 페이지에서 실행되는 다른 JavaScript 코드가 내부에서 진행되는 상황을 알지 못했습니다. at.js가 발전하면서 이 문제를 해결할 수 있는 기회가 생겼습니다.

고객에 따르면, 다음을 포함하여 알림을 받기 원하는 몇 가지 시나리오가 있습니다.

* 시간 초과, 잘못된 상태 코드, JSON 구문 분석 오류 등으로 인해 mbox 요청이 실패한 경우
* mbox 요청이 성공한 경우
* mbox 요소 누락, 선택기를 찾을 수 없음 등으로 인해 오퍼 렌더링이 실패한 경우
* 오퍼 렌더링이 성공한 경우 DOM 변경 사항이 적용된 경우

사전 정의된 이벤트에는 이벤트 유형에 따라 필수 데이터를 추출할 수 있는 구조가 있습니다.

다른 시나리오에서 이벤트를 사용할 수 있게 하도록 사용자 정의 이벤트에는 이벤트 개체(핸들러에 전달)의 detail 속성에 지정된 페이로드 개체가 있습니다. 또한 문자열을 이벤트 이름으로 전달하지 않도록 하기 위해 `adobe.target.event` 네임스페이스를 사용하여 이벤트가 상수로 표시됩니다.

## 구조

| 키 | 유형 | 설명 |
|--- |--- |--- |
| 유형 | 문자열 | at.js와의 상호 작용을 추적, 디버깅 및 사용자 지정하는 데 도움이 되도록 알림을 받으려는 몇 가지 시나리오가 있습니다.<p>아래에 나열된 각 사용자 지정 이벤트는 &quot;상수&quot; 및 &quot;문자열 값&quot;의 두 가지 형식을 갖습니다.<ul><li>**상수**: 앞에 `adobe.target.event.`를 추가하고, 모두 대문자로 표시하고 밑줄 문자를 포함합니다. at.js가 로드된 *후*, mbox 응답이 수신되기 *전에* 사용자 지정 이벤트에 가입하려면 상수를 사용하십시오.</li><li>**문자열 값**: 소문자로 나타내고 대시를 포함합니다. at.js가 로드되기 *전*&#x200B;에 사용자 지정 이벤트에 가입하려면 문자열 값을 사용하십시오.</li></ul>**요청이 실패했습니다**<p>상수: `adobe.target.event.REQUEST_FAILED`<p>문자열 값: `at-request-failed`<p>설명: 시간 초과, 잘못된 상태 코드, JSON 구문 분석 오류 등으로 인해 mbox 요청이 실패했습니다.<p>**요청 성공**<p>상수: `adobe.target.event.REQUEST_SUCCEEDED`<p>문자열 값: `at-request-succeeded`<p>설명: mbox 요청이 성공했습니다.<p>**컨텐츠 렌더링 실패**<p>상수: `adobe.target.event.CONTENT_RENDERING_FAILED`<p>문자열 값: `at-content-rendering-failed`<p>설명: mbox 요소 누락, 선택기를 찾을 수 없음 등으로 인해 오퍼 렌더링이 실패했습니다.<p>**컨텐츠 렌더링 성공**<p>상수: `adobe.target.event.CONTENT_RENDERING_SUCCEEDED`<p>문자열 값: `at-content-rendering-succeeded`<p>설명: 오퍼 렌더링이 성공했습니다. DOM 변경 사항이 적용된 경우<p>**라이브러리가 로드됨**<p>상수: `adobe.target.event.LIBRARY_LOADED`<p>문자열 값: `at-library-loaded`<p>설명: 이 이벤트는 at.js가 완전히 로드된 시간을 추적하는 데 이상적입니다. 이 이벤트를 사용하여 글로벌 mbox 실행을 사용자 지정할 수 있습니다. 또한 이 이벤트를 사용하여 글로벌 mbox를 비활성화한 후 이 이벤트를 수신하여 나중에 글로벌 mbox를 실행할 수도 있습니다.<p>**요청 시작**<p>상수: `adobe.target.event.REQUEST_START`<p>문자열 값: `at-request-start`<p>설명: 이 이벤트는 HTTP 요청이 실행되기 전에 시작됩니다. 리소스 시간 설정 API를 사용하는 성능 측정에 이 이벤트를 사용할 수 있습니다.<p>**컨텐츠 렌더링 시작**<p>상수: `adobe.target.event.CONTENT_RENDERING_START`<p>문자열 값: `at-content-rendering-start`<p>설명: 이 이벤트는 선택기 폴링이 시작되고 컨텐츠가 페이지로 렌더링되기 전에 시작됩니다. 이 이벤트를 사용하여 컨텐츠 렌더링 진행 상태를 추적할 수 있습니다.<p>**컨텐츠 렌더링에 오퍼가 없음**<p>상수: `adobe.target.event.CONTENT_RENDERING_NO_OFFERS`<p>문자열 값: `at-content-rendering-no-offers`<p>설명: 반환된 오퍼가 없는 경우에 이 이벤트가 시작됩니다.<p>**컨텐츠 렌더링 리디렉션**<p>상수: `adobe.target.event.CONTENT_RENDERING_REDIRECT`<p>문자열 값: `at-content-rendering-redirect`<p>설명: 오퍼가 리디렉션이고 [!DNL Target] 은 다른 URL로 리디렉션됩니다. |
| mbox | 문자열 | mbox 이름 |
| message | 문자열 | 발생한 사항, 오류 메시지 등과 같이 사람이 읽을 수 있는 설명을 포함합니다. |
| tracking | 개체 | `sessionId` 및 `deviceId`를 포함합니다. 일부 경우에 `deviceId`이 에지 서버에서 검색할 수 없기 때문에 [!DNL Target]가 누락될 수 있습니다. |
| 유형 | 문자열 | **온디바이스 의사 결정 아티팩트 성공**<p>상수:<p>`adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED`<p>문자열 값: `artifactDownloadSucceeded`<p>설명: 온디바이스 의사 결정 아티팩트가 성공적으로 다운로드되면 호출됩니다.<p>**온디바이스 의사 결정 아티팩트 실패**<p>상수: `adobe.target.event.ARTIFACT_DOWNLOAD_FAILED`<p>문자열 값: `artifactDownloadFailed`<p>설명: 온디바이스 의사 결정 아티팩트가 다운로드되지 않으면 호출됩니다. |

## 사용

```javascript {line-numbers="true"}
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(event) { 
  console.log('Event', event); 
});
```

## 교육 비디오: 응답 토큰 및 at.js 사용자 지정 이벤트 ![튜토리얼 배지](../../../assets/tutorial.png)

다음 비디오를 시청하여 응답 토큰 및 at.js 사용자 지정 이벤트를 사용하여 의 프로필 정보를 공유하는 방법을 학습하십시오 [!DNL Target] 타사 시스템으로 이동합니다.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)
