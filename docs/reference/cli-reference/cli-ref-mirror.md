---
title: NuGet CLI 미러 명령
description: nuget.exe 미러 명령에 대 한 참조
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6ecd5c11383f78fdaeb01090366a8ffe294b4f8b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779169"
---
# <a name="mirror-command-nuget-cli"></a>미러 명령 (NuGet CLI)

**적용 대상:** 패키지 게시 &bullet; **지원 버전:** 3.2 이상에서 사용 되지 않음

패키지와 해당 종속성을 지정 된 원본 리포지토리에서 대상 리포지토리로 미러링합니다.

> [!NOTE]
> 이전에 NuGet 2.x에서이 명령을 지 원하는 NuGet.ServerExtensions.dll 및 NuGet-Signed.exe (nuget.exe로 NuGet-Signed.exe 이름 바꾸기)는 더 이상 다운로드할 수 없습니다. 이와 유사한 명령을 사용 하려면 [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/)를 시도 합니다.

## <a name="usage"></a>사용량

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

여기서 `<packageID>` 는 미러링할 패키지 이거나 `<configFilePath>` `packages.config` 미러링할 패키지가 나열 된 파일을 식별 합니다.

는 `<listUrlTarget>` 원본 리포지토리를 지정 하 고 `<publishUrlTarget>` 대상 리포지토리를 지정 합니다.

대상 리포지토리가 `https://machine/repo` [NuGet. Server](../../hosting-packages/nuget-server.md)를 실행 하는 경우 목록 및 푸시 url은 `https://machine/repo/nuget` `https://machine/repo/api/v2/package` 각각 및입니다.

## <a name="options"></a>옵션

- **`-ApiKey`**

  대상 리포지토리의 API 키입니다. 존재 하지 않는 경우 구성 파일에 지정 된 항목 ( `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux))이 사용 됩니다.

- **`-Help`**

  명령에 대 한 도움말 정보를 표시 합니다.

- **`-NoCache`**

  NuGet이 캐시 된 패키지를 사용 하지 못하도록 합니다. [전역 패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요.

- **`-Noop`**

  수행할 작업을 기록 하지만 작업을 수행 하지는 않습니다. 푸시 작업의 성공 여부를 가정 합니다.

- **`-PreRelease`**

  미러링 작업에 시험판 패키지를 포함 합니다.

- **`-Source`**

  미러링할 패키지 원본의 목록입니다. 소스를 지정 하지 않으면 구성 파일에 정의 된 소스 (위 ApiKey 참조)가 사용 되 고, 아무것도 지정 되지 않은 경우 nuget.org가 사용 됩니다.

- **`-Timeout`**

  서버에 푸시하는 제한 시간 (초)을 지정 합니다.  기본값은 300초(5분)입니다.

- **`-Version`**

  설치할 패키지의 버전입니다. 지정 하지 않으면 최신 버전이 미러링됩니다.

[환경 변수](cli-ref-environment-variables.md) 참조

## <a name="examples"></a>예

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
