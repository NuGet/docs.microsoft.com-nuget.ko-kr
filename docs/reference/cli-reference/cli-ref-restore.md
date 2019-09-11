---
title: NuGet CLI 복원 명령
description: Nuget.exe restore 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 211f24ff67c06da00d6a014e679cc422d493d6d5
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959739"
---
# <a name="restore-command-nuget-cli"></a>restore 명령 (NuGet CLI)

**적용 대상:** 패키지 &bullet; 사용 **지원 버전:** 2.7+

`packages` 폴더에서 누락 된 패키지를 다운로드 하 여 설치 합니다. NuGet 4.0 + 및 PackageReference 형식과 함께 사용 하는 경우 필요한 경우 `<project>.nuget.props` `obj` 폴더에 파일을 생성 합니다. 파일은 소스 제어에서 생략할 수 있습니다.

Mac에서 CLI를 사용 하는 Mac OSX 및 Linux에서 패키지 복원은 PackageReference에서 지원 되지 않습니다.

## <a name="usage"></a>사용

```cli
nuget restore <projectPath> [options]
```

여기서 `<projectPath>` 는 솔루션 `packages.config` 또는 파일의 위치를 지정 합니다. 동작 세부 정보는 아래 [설명 부분](#remarks) 을 참조 하세요.

## <a name="options"></a>변수

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | 적용할 NuGet 설정 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| DirectDownload | *(4.0 이상)* 는 이진 또는 메타 데이터로 캐시를 채우지 않고 패키지를 직접 다운로드 합니다. |
| DisableParallelProcessing | 여러 패키지를 동시에 복원 하지 않습니다. |
| FallbackSource | *(3.2 이상)* 주 또는 기본 원본에서 패키지를 찾을 수 없는 경우 대체로 사용할 패키지 원본 목록입니다. 세미콜론을 사용 하 여 목록 항목을 구분 합니다. |
| ForceEnglishOutput | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| Help | 명령어에 대한 도움말을 표시합니다. |
| MSBuildPath | *(4.0 이상)* 명령에 사용할 MSBuild의 경로를 지정 합니다 `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 이상)* 이 명령에 사용할 MSBuild의 버전을 지정 합니다. 지원 되는 값은 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9입니다. 기본적으로 경로에 MSBuild가 선택 되어 있으며, 그렇지 않은 경우 기본적으로 설치 되어 있는 MSBuild의 가장 높은 버전으로 설정 됩니다. |
| NoCache | NuGet이 캐시 된 패키지를 사용 하지 못하도록 합니다. [전역 패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| OutputDirectory | 패키지가 설치 되는 폴더를 지정 합니다. 폴더를 지정 하지 않으면 현재 폴더가 사용 됩니다. 또는 `PackagesDirectory` `packages.config` 를`SolutionDirectory` 사용 하지 않는 한 파일을 사용 하 여 복원할 때 필요 합니다.|
| PackageSaveMode | 패키지 설치 후 저장할 파일 유형을 지정 합니다. `nuspec`, `nupkg`또는 `nuspec;nupkg`중 하나입니다. |
| PackagesDirectory | `OutputDirectory`와 같습니다. 또는 `OutputDirectory` `packages.config` 를`SolutionDirectory` 사용 하지 않는 한 파일을 사용 하 여 복원할 때 필요 합니다. |
| Project2ProjectTimeOut | 프로젝트 간 참조를 확인 하는 제한 시간 (초)입니다. |
| 폴더 | *(4.0 이상)* UWP 및 .NET Core 프로젝트에 대 한 모든 참조 프로젝트를 복원 합니다. 을 사용 하 `packages.config`는 프로젝트에는 적용 되지 않습니다. |
| RequireConsent | 패키지를 다운로드 하 고 설치 하기 전에 패키지 복원이 사용 되는지 확인 합니다. 자세한 내용은 [패키지 복원](../../consume-packages/package-restore.md)을 참조 하세요. |
| SolutionDirectory | 솔루션 폴더를 지정 합니다. 솔루션에 대 한 패키지를 복원 하는 경우 유효 하지 않습니다. 또는 `PackagesDirectory` `packages.config` 를`OutputDirectory` 사용 하지 않는 한 파일을 사용 하 여 복원할 때 필요 합니다. |
| Source | 복원에 사용할 패키지 원본 (Url)의 목록을 지정 합니다. 생략 하는 경우 명령은 구성 파일에 제공 된 소스를 사용 합니다. [NuGet 동작 구성](../../consume-packages/configuring-nuget-behavior.md)을 참조 하세요. 세미콜론을 사용 하 여 목록 항목을 구분 합니다. |
| Verbosity | 출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="remarks"></a>설명

Restore 명령은 다음 단계를 수행 합니다.

1. 복원 명령의 작업 모드를 결정 합니다.

   | projectPath 파일 형식 | 동작 |
   | --- | --- |
   | 솔루션 (폴더) | NuGet은 `.sln` 파일을 찾은 후 해당 파일을 사용 하 고, 그렇지 않으면 오류를 제공 합니다. `(SolutionDir)\.nuget`는 시작 폴더로 사용 됩니다. |
   | `.sln`파일과 | 솔루션에 의해 식별 되는 패키지를 복원 합니다. 을 사용 하는 `-SolutionDirectory` 경우 오류를 제공 합니다. `$(SolutionDir)\.nuget`는 시작 폴더로 사용 됩니다. |
   | `packages.config`또는 프로젝트 파일 | 파일에 나열 된 패키지를 복원 하 여 종속성을 확인 하 고 설치 합니다. |
   | 기타 파일 형식 | 파일이 위와 같이 `.sln` 파일 이라고 가정 합니다. 솔루션이 아닌 경우 NuGet에서 오류를 제공 합니다. |
   | (projectPath를 지정 하지 않음) | <ul><li>NuGet은 현재 폴더에 있는 솔루션 파일을 찾습니다. 단일 파일이 있는 경우 해당 파일은 패키지를 복원 하는 데 사용 됩니다. 여러 솔루션을 찾은 경우 NuGet은 오류를 제공 합니다.</li><li>솔루션 파일이 없는 경우 NuGet은를 `packages.config` 찾고이를 사용 하 여 패키지를 복원 합니다.</li><li>솔루션이 나 `packages.config` 파일이 없으면 NuGet에서 오류를 제공 합니다.</ul> |

2. 다음 우선 순위 순서를 사용 하 여 패키지 폴더를 결정 합니다. 이러한 폴더를 찾을 수 없는 경우 NuGet에서 오류를 제공 합니다.

    - 로 `-PackagesDirectory`지정 된 폴더입니다.
    - 의 `repositoryPath` 값입니다.`Nuget.Config`
    - 지정 된 폴더`-SolutionDirectory`
    - `$(SolutionDir)\packages`

3. 솔루션에 대 한 패키지를 복원할 때 NuGet은 다음 작업을 수행 합니다.
    - 솔루션 파일을 로드 합니다.
    - `$(SolutionDir)\.nuget\packages.config` 에`packages` 나열 된 솔루션 수준 패키지를 폴더에 복원 합니다.
    - `$(ProjectDir)\packages.config` 에`packages` 나열 된 패키지를 폴더에 복원 합니다. 지정 된 각 패키지에 대해를 지정 하지 않으면 `-DisableParallelProcessing` 패키지를 병렬로 복원 합니다.

## <a name="examples"></a>예

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
