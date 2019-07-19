---
title: NuGet CLI 미러 명령
description: Nuget.exe 미러 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327670"
---
# <a name="mirror-command-nuget-cli"></a>mirror 명령(NuGet CLI)

**적용 대상:** 패키지 게시 &bullet; **지원 버전:** 3.2 이상에서 사용 되지 않음

패키지와 해당 종속성을 지정 된 원본 리포지토리에서 대상 리포지토리로 미러링합니다.

> [!NOTE]
> 3\.2 이전 NuGet 버전에 대해이 명령을 [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)사용 하려면로 이동 하 고, 안정적인 최신 릴리스를 선택 하 고,를 로컬 디스크에 다운로드 `nuget.exe` `NuGet.ServerExtensions.dll` 하 고, `Nuget-Signed.exe` 로 이름을 바꿉니다 `Nuget-Signed.exe` .

## <a name="usage"></a>사용법

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

여기서 `<packageID>` 는 미러링할 패키지 이거나 `<configFilePath>` 미러링할 패키지가 나열 된 `packages.config` 파일을 식별 합니다.

는 `<listUrlTarget>` 원본 리포지토리를 지정 하 고 `<publishUrlTarget>` 대상 리포지토리를 지정 합니다.

`https://machine/repo` 대상 리포지토리가 [NuGet. Server](../../hosting-packages/nuget-server.md)를 실행 하는 경우 목록 및 `https://machine/repo/nuget` 푸시 url은 각각 및 `https://machine/repo/api/v2/package`입니다.

## <a name="options"></a>변수

| 옵션 | 설명 |
| --- | --- |
| ApiKey | 대상 리포지토리에 대한 API 키입니다. 존재 하지 않는 경우 구성 파일에 지정 된 항목 (`%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux))이 사용 됩니다. |
| Help | 명령어에 대한 도움말을 표시합니다. |
| NoCache | NuGet이 캐시 된 패키지를 사용 하지 못하도록 합니다. [전역 패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요. |
| Noop | 수행할 작업을 기록 하지만 작업을 수행 하지는 않습니다. 푸시 작업의 성공 여부를 가정 합니다. |
| PreRelease | 미러링 작업에 시험판 패키지를 포함 합니다. |
| Source | 미러링할 패키지 원본의 목록입니다. 소스를 지정 하지 않으면 구성 파일에 정의 된 소스 (위 ApiKey 참조)가 사용 되 고, 아무것도 지정 되지 않은 경우 nuget.org가 사용 됩니다. |
| 제한 시간 | 서버에 푸시하는 제한 시간 (초)을 지정 합니다. 기본값은 300 초 (5 분)입니다. |
| 버전 | 설치할 패키지의 버전입니다. 지정 하지 않으면 최신 버전이 미러링됩니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="examples"></a>예제

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
