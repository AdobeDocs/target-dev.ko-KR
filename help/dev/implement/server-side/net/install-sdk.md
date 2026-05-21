---
title: .NET SDK 설치
description: ' [!DNL Adobe Target] .NET SDK을 설치하는 방법을 알아봅니다.'
feature: APIs/SDKs
exl-id: 3cc84775-4692-4d14-9e82-db2873140835
TQID: https://experienceleague.adobe.com/438ax3dEUclYIa42EvOLyBBuRngsZLHRDXabumxp0F8
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 63
ht-degree: 0%

---

# .NET SDK 설치

.NET SDK은 [NuGet](https://www.nuget.org/packages/Adobe.Target.Client)에 의해 배포됩니다. 시작하려면 `Package Manage` 또는 `.NET CLI`을(를) 통해 설치하여 종속성으로 추가하십시오.

## 패키지 관리자

>[!BEGINTABS]

>[!TAB 패키지 관리자]

```csharp {line-numbers="true"}
Install-Package Adobe.Target.Client
```

>[!TAB .NET CLI]

```csharp {line-numbers="true"}
dotnet add package Adobe.Target.Client
```

>[!ENDTABS]

오픈 소스 코드는 [https://github.com/adobe/target-dotnet-sdk](https://github.com/adobe/target-dotnet-sdk)에서 찾을 수 있습니다.
