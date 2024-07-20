---
title: create 메서드를 사용하여 Python SDK 초기화
description: create 메서드를 사용하여 Python SDK를 초기화하고 [!UICONTROL TargetClient]을(를) 인스턴스화하여 실험 및 개인화된 경험을 위해  [!DNL Adobe Target] 을(를) 호출하는 방법에 대해 알아봅니다.
feature: APIs/SDKs
exl-id: 3e231e8e-696d-45c7-b733-79bf99da5bec
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 17%

---

# Python SDK 초기화

설명
Python SDK를 초기화하고 [!UICONTROL Target Client]을(를) 인스턴스화하여 실험 및 개인화된 경험을 위해 [!DNL Adobe Target]을(를) 호출하려면 `create` 메서드를 사용하십시오.

## 방법

### 만들기

```python {line-numbers="true"}
TargetClient.create(options)
```

## 매개 변수

`options`의 구조는 다음과 같습니다.

| 이름 | 유형 | 필수 | 기본값 | 설명 |
| --- | --- | --- | --- | --- |
| 클라이언트 | str | 예 | 없음 | [!UICONTROL Adobe Target client ID] |
| organization_id | str | 예 | 없음 | [!UICONTROL Experience Cloud Organization ID] |
| timeout | int | 아니요 | 3000 | 시간 제한(밀리초) |
| server_domain | str | 아니요 | `client.tt.omtrdc.net` |  | 기본 호스트 이름 무시 |
| secure | 부울 | 아니요 | true | HTTP 체계를 적용하도록 설정 해제 |
| 로거 | 오브젝트 | 아니요 | 정보 로거 |  | 기본 INFO 로거를 바꿉니다. |
| target_location_hint | str | 아니요 | 없음 | [!DNL Target] 위치 힌트 |
| property_token | str | 아니요 | 없음 | [!DNL Target] 속성 토큰입니다. 여기에 지정하면 모든 get_offers 호출이 이 값을 사용합니다. |
| decisioning_method | str | 아니요 | 서버측 | 사용할 의사 결정 방법([on-device](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), 서버측, 하이브리드)을 결정합니다 |
| polling_interval | int | 아니요 | 300000(5분) | [온디바이스 의사 결정 규칙 아티팩트](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)의 폴링 간격(밀리초) |
| artifact_location | str | 아니요 | 없음 | [온디바이스 의사 결정 규칙 아티팩트](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)에 대한 정규화된 URL입니다. 내부적으로 결정된 위치를 재정의합니다. |
| artifact_payload | 오브젝트 | 아니요 | 없음 | [온디바이스 의사 결정 규칙 아티팩트](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)의 JSON 페이로드. 지정하면 URL에서 요청하는 대신 사용됩니다. |
| [events](sdk-events.md) | dict &lt;str, callable> | 아니요 | 없음 | 이벤트 이름 키와 콜백 함수 값이 있는 선택적 개체입니다 |
| environment_id | int | 아니요 | production | [!DNL Target] 환경 ID |
| 환경 | str | 아니요 | production | [!DNL Target] 환경 이름 |
| cdn_environment | str | 아니요 | production | CDN 환경 이름 |
| telemetry_enabled | 부울 | 아니요 | True | False로 설정하면 원격 분석 데이터가 [!DNL Adobe](으)로 전송되지 않습니다 |
| version | str | 아니요 | 없음 | 이 SDK의 버전 번호 |

## 예

### Python

```python {line-numbers="true"}
from target_python_sdk import TargetClient

def client_ready_callback(ready_event):
    # make calls to Adobe Target

client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
