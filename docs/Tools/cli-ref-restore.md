---
title: "NuGet CLI 복원 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 복원 명령에 대 한 참조"
keywords: "nuget 복원 참조, 패키지 명령 복원"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2416ad652244e0ea60651147ad74a1513cdb75ff
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="restore-command-nuget-cli"></a>restore 명령 (NuGet CLI)

**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 2.7 +

다운로드 하 고 모든 패키지에서 누락 된 설치는 `packages` 폴더입니다. NuGet 4.0 이상 및 PackageReference 형식으로 사용 하는 경우 생성 된 `<project>.nuget.props` 파일에 필요한 경우는 `obj` 폴더. (소스 제어에서 파일을 생략할 수 있습니다.)

Mac OSX 및 모노에 CLI와 Linux에서 패키지를 복원 지원 되지 않습니다 PackageReference 합니다.

## <a name="usage"></a>사용법

```cli
nuget restore <projectPath> [options]
```

여기서 `<projectPath>` 솔루션의 위치를 지정 또는 `packages.config` 파일입니다. 참조 [주의](#remarks) 아래 동작 세부 정보에 대 한 합니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | 적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| DirectDownload | *(4.0 이상)*  이진 파일 및 메타 데이터에 대해 캐시를 채우지 않고 직접 패키지를 다운로드 합니다. |
| DisableParallelProcessing | 동시에 여러 패키지를 복원 하는 데 사용 하지 않습니다. |
| FallbackSource | *(3.2 +)*  패키지 주에서 찾을 수 없는 경우 대체도 사용할 패키지 소스 목록 또는 기본 소스입니다. |
| ForceEnglishOutput | *(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| MSBuildPath | *(4.0 이상)*  우선 순위를 차지 명령으로 사용 하는 MSBuild의 경로 지정 `-MSBuildVersion`합니다. |
| MSBuildVersion | *(3.2 +)*  이 명령과 함께 사용할 MSBuild의 버전을 지정 합니다. 지원 되는 값은 4, 12, 14, 15입니다. 경로에 MSBuild 선택은 기본적으로 그렇지 않은 경우 기본값이 가장 높은 설치 된 버전의 MSBuild 됩니다. |
| NoCache | NuGet 패키지를 사용 하 여 로컬 컴퓨터 캐시에서 방지 합니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| OutputDirectory | 패키지 설치 되는 폴더를 지정 합니다. 없는 폴더를 지정 하는 경우 현재 폴더가 사용 됩니다. |
| PackageSaveMode | 패키지 설치 후 저장할 파일의 형식을 지정 합니다: 중 `nuspec`, `nupkg`, 또는 `nuspec;nupkg`합니다. |
| PackagesDirectory | `OutputDirectory`와 동일합니다. |
| Project2ProjectTimeOut | 프로젝트 간 참조를 확인 하기 위한 시간 (초)의 시간이 초과 되었습니다. |
| 재귀 | *(4.0 이상)*  UWP 및.NET Core 프로젝트에 대 한 모든 참조 프로젝트를 복원 합니다. 사용 하 여 프로젝트에 적용 되지 않습니다 `packages.config`합니다. |
| RequireConsent | 다운로드 하 고 패키지를 설치 하기 전에 패키지를 복원 활성화 되어 있는지 확인 합니다. 자세한 내용은 참조 [패키지 복원](../consume-packages/package-restore.md)합니다. |
| SolutionDirectory | 솔루션 폴더를 지정합니다. 솔루션에 대 한 패키지를 복원 하는 경우 유효 하지 않습니다. |
| 소스 | 복원에 사용할 하도록 (Url)로 패키지 소스 목록을 지정 합니다. 구성 파일에 제공 된 원본을 사용 하 여 생략 된 경우, 참조 [NuGet 구성 동작](../consume-packages/configuring-nuget-behavior.md)합니다. |
| 자세한 정도 |>-출력에 표시 되는 하위 크기를 지정 하는 중: *일반*, *quiet*, *자세한*합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="remarks"></a>설명

Restore 명령에서 다음 단계를 수행합니다.

1. Restore 명령 작업 모드를 결정 합니다.
    projectPath 파일 형식 | 동작
    | --- | --- |
    솔루션 (폴더) | NuGet를 찾습니다는 `.sln` 검색 되지 않으면 오류가 발생 하는 사용 하 여 파일입니다. `(SolutionDir)\.nuget` 시작 폴더도 사용 됩니다.
    `.sln` 파일 | 솔루션;로 식별 되는 패키지를 복원 하면 오류가 발생 `-SolutionDirectory` 사용 됩니다. `$(SolutionDir)\.nuget` 시작 폴더도 사용 됩니다.
    `packages.config` 또는 프로젝트 파일 | 해결 및 종속성 설치 파일에 나열 된 패키지를 복원 합니다.
    다른 파일 형식 | 파일 것으로 간주 되는 `.sln` 오류 NuGet은 솔루션을 없으면 위와; 같은 파일입니다.
    (projectPath 지정 되지 않은) | -NuGet 현재 폴더에서 솔루션 파일을 찾습니다. 하나; 패키지를 복원 하는 데 사용 단일 파일이 발견 된 경우 NuGet 여러 솔루션 발견 되 면 오류가 발생 합니다.
    |-NuGet에 대 한 검색 솔루션 파일이 없는 경우는 `packages.config` 및이 사용 하 여 패키지를 복원 합니다.
    |-솔루션이 없는 경우 또는 `packages.config` 파일이, NuGet 오류가 발생 합니다.

1. 다음과 같은 우선 순위 (NuGet 이러한 폴더의 발견 되지 않으면 오류가 제공)를 사용 하 여 패키지 폴더를 결정 합니다.

    - 지정 된 폴더 `-PackagesDirectory`합니다.
    - `repositoryPath` 베일에서 `Nuget.Config`
    - 지정 된 폴더 `-SolutionDirectory`
    - `$(SolutionDir)\packages`

1. 솔루션에 대 한 패키지를 복원할 때 NuGet는 다음을 수행 합니다.
    - 솔루션 파일을 로드합니다.
    - 솔루션 수준 패키지에 나열 된 복원 `$(SolutionDir)\.nuget\packages.config` 에 `packages` 폴더입니다.
    - 에 나열 된 패키지를 복원 `$(ProjectDir)\packages.config` 에 `packages` 폴더입니다. 지정 된 각 패키지에 대해 병렬로 패키지 않으면 복원이 `-DisableParallelProcessing` 지정 됩니다.

## <a name="examples"></a>예제

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
