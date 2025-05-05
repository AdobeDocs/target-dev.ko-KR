---
title: 프로필 가져오기
description: Adobe Target 프로필 API를 사용하여  [!DNL Target]에서 사용할 방문자 데이터를 가져오는 방법에 대해 알아봅니다.
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: b422ae68-49b3-4d60-9ea4-0fa67b6934b0
source-git-commit: b8ccfdcaff6aa17a325727df0a9ffd716e44519b
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# 프로필 가져오기

[!DNL Target] 프로필은 다음 세 가지 방법으로 가져올 수 있습니다. `[!DNL Experience Cloud Visitor ID]`(`ECID`), `tntid` 또는 `thirdPartyId`을(를) 사용합니다.

## [!DNL Experience Cloud Visitor ID] (ECID) 사용

`ECID`을(를) 기반으로 프로필을 가져올 수 있습니다. HTTP 메서드는 GET 형식이어야 합니다.

URL은 다음 예제와 비슷합니다.

```
https://<clientCode>.tt.omtrdc.net/rest/v1/profiles/marketingCloudVisitorId/<ECID>?client=<clientCode>
```

`<clientCode>`을(를) [!DNL Target] [!UICONTROL Client Code] (으)로 바꾸고 `<ECID>`을(를) [!DNL Experience Cloud Visitor ID] ([!DNL Marketing Cloud Visitor ID])(으)로 바꿉니다.

## tntid 사용

[!DNL Target]은(는) 모든 요청에 대해 `tntid`을(를) 자동으로 할당합니다.

다음 예제에서는 `tntid`을(를) 사용하여 프로필을 가져오는 요청 형식을 보여 줍니다.

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/your-tnt-id?client=<your-client-code>
```

`<your-client-code>` 및 `your-tnt-id`을(를) 바꾸고 GET 요청을 실행합니다. 다음은 `tntid`을(를) 사용한 프로필 가져오기 호출의 예입니다.

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/111492025094307-353046?client=<your-client-code>
```

## thirdPartyId 사용

[!DNL Adobe Target] 프로필은 고유한 식별자(예: CRM ID, `uuid`, 멤버십 번호 등)로 추가할 수 있습니다.

프로필에 `thirdPartyId`을(를) 첨부하는 방법은 [프로필 업데이트](/help/dev/administer/profile-api/profile-api-overview.md)를 참조하세요.

다음 예제에서는 `thirdPartyId`을(를) 사용하여 프로필을 가져오는 요청 형식을 보여 줍니다.

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/your-thirdpartyid?client=<your-client-code>
```

`<your-client-code>` 및 `your-thirdpartyid`을(를) 바꾸고 GET 요청을 실행합니다. 다음은 [!UICONTROL thirdpartyid]을(를) 사용한 프로필 가져오기 호출의 예입니다.

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/a1-mbox3rdPartyId?client=<your-client-code>
```

이 호출이 수행되면 [!DNL Target]은(는) Edge 요청에서 언급된 클러스터에서 먼저 프로필을 찾으려고 시도하거나 프로필이 있는 모든 위치에서 콘텐츠를 반환하려고 시도합니다. 프로필 콘텐츠는 JSON 형식으로 반환됩니다.

## 인증

여기에 설명된 대로 [!DNL Target] UI에서 인증을 켜면 [!DNL Target Profile API]의 보안을 유지할 수 있습니다. 인증이 켜지면 모든 프로필 API 요청에 요청 헤더에 프로필 인증 토큰이 설정되어 있어야 합니다. 토큰 자체는 [!DNL Target] UI를 사용하거나 [프로필 인증 토큰](https://developers.adobetarget.com/api/#authentication-tokens){target=_blank} 섹션에서 위에 설명된 단계를 사용하여 생성할 수 있습니다.

## 미터링

이러한 호출은 mbox 호출에 포함되지 않습니다.

## 오류 처리

잘못되었거나 만료된 `thirdPartyId`을(를) 사용하여 `/thirdPartyId`을(를) 호출하는 경우:

```
{"status" : 404, "message" : "No profile found for client <client_code> with third party id=<third_party_id>"}
```

프로필을 찾을 수 없거나 만료된 경우:

```
{"status" : 404, "message" : "No profile found for client <client_code> with mboxPC=<mbox_pc>"}
```
