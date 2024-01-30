---
title: 프로필 가져오기
description: Adobe Target 프로필 API를 사용하여에서 사용할 방문자 데이터를 가져오는 방법에 대해 알아봅니다 [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: b422ae68-49b3-4d60-9ea4-0fa67b6934b0
source-git-commit: b8ccfdcaff6aa17a325727df0a9ffd716e44519b
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# 프로필 가져오기

A [!DNL Target] 세 가지 방법으로 프로필을 가져올 수 있습니다. `[!DNL Experience Cloud Visitor ID]` (`ECID`), `tntid` 또는 `thirdPartyId`.

## 사용 [!DNL Experience Cloud Visitor ID] (ECID)

다음을 기반으로 프로필을 가져올 수 있습니다. `ECID`. HTTP 메서드는 GET 형식이어야 합니다.

URL은 다음 예제와 비슷합니다.

```
https://<clientCode>.tt.omtrdc.net/rest/v1/profiles/marketingCloudVisitorId/<ECID>?client=<clientCode>
```

바꾸기 `<clientCode>` (으)로 [!DNL Target] [!UICONTROL 클라이언트 코드] 및 `<ECID>` (으)로 [!DNL Experience Cloud Visitor ID] ([!DNL Marketing Cloud Visitor ID]).

## tntid 사용

[!DNL Target] 자동으로 할당 `tntid` 모든 요청에 대해

다음 예는 를 사용하여 프로필을 가져오도록 요청 형식을 보여 줍니다. `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/your-tnt-id?client=<your-client-code>
```

바꾸기 `<your-client-code>` 및 `your-tnt-id` 및 GET 요청을 실행합니다. 다음은 를 사용한 프로필 가져오기 호출의 예입니다. `tntid`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/111492025094307-353046?client=<your-client-code>
```

## thirdPartyId 사용

[!DNL Adobe Target] 고유한 식별자(예: CRM id)로 프로필을 늘릴 수 있습니다. `uuid`, 멤버십 번호 등).

다음을 참조하십시오 [프로필 업데이트](/help/dev/administer/profile-api/profile-api-overview.md) 을(를) 첨부하는 방법에 대해 알아보려면 `thirdPartyId` 을(를) 내 프로필에 추가합니다.

다음 예는 를 사용하여 프로필을 가져오도록 요청 형식을 보여 줍니다. `thirdPartyId`:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/your-thirdpartyid?client=<your-client-code>
```

바꾸기 `<your-client-code>` 및 `your-thirdpartyid` 및 GET 요청을 실행합니다. 다음은 를 사용한 프로필 가져오기 호출의 예입니다. [!UICONTROL thirdpartyid]:

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/a1-mbox3rdPartyId?client=<your-client-code>
```

이 호출이 수행되면, [!DNL Target] 는 edge 요청에 언급된 클러스터에서 먼저 프로필을 찾으려고 시도하거나 프로필이 있는 모든 곳에서 프로필을 찾아서 컨텐츠를 반환합니다. 프로필 콘텐츠는 JSON 형식으로 반환됩니다.

## 인증

다음 [!DNL Target Profile API] 에서 인증을 켜서 보안을 설정할 수 있습니다. [!DNL Target] 여기에 설명된 대로 UI를 사용하십시오. 인증이 켜지면 모든 프로필 API 요청에 요청 헤더에 프로필 인증 토큰이 설정되어 있어야 합니다. 를 사용하여 토큰 자체를 생성할 수 있습니다. [!DNL Target] UI 또는 의 위에 설명된 단계 사용 [프로필 인증 토큰](https://developers.adobetarget.com/api/#authentication-tokens){target=_blank} 섹션.

## 미터링

이러한 호출은 mbox 호출에 포함되지 않습니다.

## 오류 처리

에 대한 호출의 경우 `/thirdPartyId` 유효하지 않거나 만료된 경우 `thirdPartyId` 지정됨:

```
{"status" : 404, "message" : "No profile found for client <client_code> with third party id=<third_party_id>"}
```

프로필을 찾을 수 없거나 만료된 경우:

```
{"status" : 404, "message" : "No profile found for client <client_code> with mboxPC=<mbox_pc>"}
```
