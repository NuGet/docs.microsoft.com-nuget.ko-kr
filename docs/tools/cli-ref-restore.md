---
title: NuGet CLI 복원 명령
description: Nuget.exe restore 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3d7a4188de4fb6f812ca19e7f9e302a5a133c58b
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425966"
---
# <a name="restore-command-nuget-cli"></a>restore 명령 (NuGet CLI)

**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 2.7+

다운로드 하 고에서 누락 된 모든 패키지를 설치 합니다 `packages` 폴더입니다. NuGet 4.0 + 및 PackageReference 형식을 사용 하는 경우 생성 한 `<project>.nuget.props` 파일에 필요한 경우는 `obj` 폴더. (소스 제어에서 파일을 생략할 수 있습니다.)

Mac OSX 및 Mono에서 CLI 사용 하 여 Linux에서 패키지를 복원 지원 되지 않습니다 (PackageReference 사용).

## <a name="usage"></a>사용법

```cli
nuget restore <projectPath> [options]
```

여기서 `<projectPath>` 솔루션의 위치를 지정 또는 `packages.config` 파일입니다. 참조 [주의](#remarks) 아래 동작 세부 정보에 대 한 합니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | 적용할 NuGet 설정 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| DirectDownload | *(4.0 이상)*  모든 이진 파일 또는 메타 데이터를 사용 하 여 캐시를 채우는 하지 않고 직접 패키지를 다운로드 합니다. |
| DisableParallelProcessing | 병렬로 여러 패키지를 복원 하는 사용 하지 않도록 설정 합니다. |
| FallbackSource | *(3.2 이상)*  패키지 주 서버에 없는 경우 대체도 사용할 패키지 원본의 목록 또는 기본 소스입니다. |
| ForceEnglishOutput | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| Help | 명령어에 대한 도움말을 표시합니다. |
| MSBuildPath | *(4.0 이상)*  보다 우선함 명령으로 사용 하는 MSBuild의 경로 지정 `-MSBuildVersion`합니다. |
| MSBuildVersion | *(3.2 이상)*  이 명령을 사용 하 여 사용할 MSBuild의 버전을 지정 합니다. 지원 되는 값은 4, 12, 14, 15.1, 15.3, 15.4에서 15.5, 15.6, 15.7, 15.8, 15.9. 경로에 MSBuild 선택은 기본적으로 그렇지 않은 경우 기본값은 MSBuild의 설치 된 가장 높은 버전으로 합니다. |
| NoCache | 캐시 된 패키지를 사용 하 여 NuGet을 방지 합니다. 참조 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| OutputDirectory | 패키지 설치 되는 폴더를 지정 합니다. 폴더는 지정 하지 않으면 현재 폴더가 사용 됩니다. 사용 하 여 복원 하는 경우 필수는 `packages.config` 파일 `PackagesDirectory` 또는 `SolutionDirectory` 사용 됩니다.|
| PackageSaveMode | 패키지를 설치한 후 파일의 형식을 지정 합니다: 중 하나 `nuspec`, `nupkg`, 또는 `nuspec;nupkg`합니다. |
| PackagesDirectory | `OutputDirectory`와 동일합니다. 사용 하 여 복원 하는 경우 필수는 `packages.config` 파일 `OutputDirectory` 또는 `SolutionDirectory` 사용 됩니다. |
| Project2ProjectTimeOut | 프로젝트 간 참조를 확인 하는 초 제한 시간입니다. |
| 재귀 | *(4.0 이상)*  UWP 및.NET Core 프로젝트에 대 한 모든 참조 프로젝트를 복원 합니다. 사용 하 여 프로젝트에 적용 되지 않습니다 `packages.config`합니다. |
| RequireConsent | 다운로드 하 고 패키지를 설치 하기 전에 패키지 복원 활성화 되어 있는지 확인 합니다. 자세한 내용은 참조 하세요 [패키지 복원](../consume-packages/package-restore.md)합니다. |
| SolutionDirectory | 솔루션 폴더를 지정합니다. 솔루션의 패키지를 복원 하는 경우 유효 하지 않습니다. 사용 하 여 복원 하는 경우 필수는 `packages.config` 파일 `PackagesDirectory` 또는 `OutputDirectory` 사용 됩니다. |
| Source | 복원에 사용할 (Url)로 패키지 소스 목록을 지정 합니다. 생략 하면 사용 하 여 구성 파일에서 제공 하는 소스를 참조 하십시오 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)합니다. |
| Verbosity | 출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="remarks"></a>설명

Restore 명령에는 다음 단계를 수행합니다.

1. Restore 명령 작업 모드를 결정 합니다.

   | projectPath 파일 형식 | 동작 |
   | --- | --- |
   | 솔루션 (폴더) | NuGet에 대 한 표시는 `.sln` 그렇지 않으면 오류를 제공 하는 사용 하 여 파일입니다. `(SolutionDir)\.nuget` 시작 폴더도 사용 됩니다. |
   | `.sln` 파일 | 솔루션에 의해 식별 되는 패키지를 복원 합니다. 에서는 오류가 발생 하는 경우 `-SolutionDirectory` 사용 됩니다. `$(SolutionDir)\.nuget` 시작 폴더도 사용 됩니다. |
   | `packages.config` 또는 프로젝트 파일 | 해결 하 고 종속성을 설치 하는 파일에 나열 된 패키지를 복원 합니다. |
   | 다른 파일 형식 | 파일으로 간주 됩니다는 `.sln` 오류가 NuGet에서는 솔루션에 없는 경우 위의; 파일입니다. |
   | (지정 되지 않은 projectPath) | <ul><li>NuGet 현재 폴더에서 솔루션 파일을 찾습니다. 해당은 패키지를 복원 하는 단일 파일이 발견 된 경우 여러 솔루션이 없으면 NuGet에서는 오류가 발생 합니다.</li><li>NuGet을 찾고 솔루션 파일이 없는 경우는 `packages.config` 를 사용 하는 패키지를 복원 합니다.</li><li>솔루션이 없는 경우 또는 `packages.config` 파일이, NuGet에서는 오류가 발생 합니다.</ul> |

2. (NuGet은 이러한 폴더의 아무 것도 없으면 오류가 제공)를 사용 하는 다음 우선 순위를 사용 하 여 패키지 폴더를 확인 합니다.

    - 사용 하 여 지정 된 폴더 `-PackagesDirectory`합니다.
    - `repositoryPath` 값 `Nuget.Config`
    - 사용 하 여 지정 된 폴더 `-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. 솔루션에 대 한 패키지를 복원할 때 NuGet는 다음을 수행 합니다.
    - 솔루션 파일을 로드합니다.
    - 에 나열 된 솔루션 수준 패키지 복원 `$(SolutionDir)\.nuget\packages.config` 에 `packages` 폴더입니다.
    - 에 나열 된 패키지를 복원 `$(ProjectDir)\packages.config` 에 `packages` 폴더입니다. 하지 않는 한 지정 된 각 패키지에 대 한 동시에 패키지를 복원 `-DisableParallelProcessing` 지정 됩니다.

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
