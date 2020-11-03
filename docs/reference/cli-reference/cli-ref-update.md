---
title: NuGet CLI 업데이트 명령
description: nuget.exe update 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 106c4027f03d8e8c1d19545b3ca9b6cd5263830e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236791"
---
# <a name="update-command-nuget-cli"></a>update 명령 (NuGet CLI)

**적용 대상:** 패키지 사용 &bullet; **지원 버전:** 모두

프로젝트의 모든 패키지(`packages.config` 사용)를 사용 가능한 최신 버전으로 업데이트합니다. 을 실행 하기 전에 [' 복원 '](cli-ref-restore.md) 을 실행 하는 것이 좋습니다 `update` . 개별 패키지를 업데이트 하려면 [`nuget install`](cli-ref-install.md) 버전 번호를 지정 하지 않고를 사용 합니다 .이 경우 NuGet은 최신 버전을 설치 합니다.

참고: `update` 는 Mono (MAC OSX 또는 Linux)에서 실행 되는 CLI 또는 PackageReference 형식을 사용 하는 경우에는 작동 하지 않습니다.

`update`이러한 참조가 이미 있는 경우이 명령은 프로젝트 파일의 어셈블리 참조도 업데이트 합니다. 업데이트 된 패키지에 추가 된 어셈블리가 있으면 새 참조가 추가 *되지 않습니다* . 새 패키지 종속성에도 해당 어셈블리 참조가 추가 되지 않습니다. 이러한 작업을 업데이트의 일부로 포함 하려면 패키지 관리자 UI 또는 패키지 관리자 콘솔을 사용 하 여 Visual Studio에서 패키지를 업데이트 합니다.

이 명령은 *-self* 플래그를 사용 하 여 nuget.exe 자체를 업데이트 하는 데도 사용할 수 있습니다.

## <a name="usage"></a>사용량

```cli
nuget update <configPath> [options]
```

여기서는 `<configPath>` `packages.config` 프로젝트의 종속성을 나열 하는 또는 솔루션 파일을 식별 합니다.

## <a name="options"></a>옵션

- **`-ConfigFile`**

  적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  사용할 종속성 패키지의 버전을 지정 합니다. 다음 중 하나일 수 있습니다.<br/><ul><li>*가장 낮음* (기본값): 가장 낮은 버전</li><li>*HighestPatch* : 최하위 주, 최저 부, 최고 패치가 있는 버전</li><li>*HighestMinor* : 최하위 주, 가장 높은 부, 최고 패치가 있는 버전</li><li>*최고* : 최고 버전</li><li>*무시* : 종속성 패키지가 사용 되지 않습니다.</li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  패키지의 파일이 대상 프로젝트에 이미 있는 경우의 기본 동작을 지정 합니다. `Overwrite`항상 파일을 덮어쓰려면로 설정 합니다. 파일을 `Ignore` 건너뛰려면로 설정 합니다.

  `PromptUser`기본값은 또는가 제공 되지 않은 경우 충돌 하는 각 파일에 대해 메시지를 표시 `OverwriteAll` `IgnoreAll` 하며 나머지 모든 파일에 적용 됩니다.

- **`-ForceEnglishOutput`**

  *(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.

- **`-?|-help`**

  명령에 대 한 도움말 정보를 표시 합니다.

- **`-Id`**

  업데이트할 패키지 Id의 목록을 지정 합니다.

- **`-MSBuildPath`**

  *(4.0 이상)* 명령에 사용할 MSBuild의 경로를 지정 합니다 `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 이상)* 이 명령에 사용할 MSBuild의 버전을 지정 합니다. 지원 되는 값은 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9입니다. 기본적으로 경로에 MSBuild가 선택 되어 있으며, 그렇지 않은 경우 기본적으로 설치 되어 있는 MSBuild의 가장 높은 버전으로 설정 됩니다.

- **`-NonInteractive`**

  사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.

- **`-PreRelease`**

  시험판 버전으로 업데이트할 수 있습니다. 이미 설치 된 시험판 패키지를 업데이트 하는 경우에는이 플래그가 필요 하지 않습니다.

- **`-RepositoryPath`**

  패키지가 설치 되는 로컬 폴더를 지정 합니다.

- **`-Safe`**

  설치 된 패키지와 동일한 주 버전 및 부 버전 내에서 가장 높은 버전의 업데이트만 사용할 수 있도록 지정 합니다.

- **`-Self`**

  최신 버전으로 nuget.exe 업데이트 다른 모든 인수는 무시 됩니다.

- **`-Source`**

  업데이트에 사용할 패키지 원본 (Url) 목록을 지정 합니다. 생략 하는 경우 명령은 구성 파일에 제공 된 소스를 사용 합니다. [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md)을 참조 하세요.

- **`-Verbosity [normal|quiet|detailed]`**

  출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.

- **`-Version`**

  하나의 패키지 ID와 함께 사용 하는 경우 업데이트할 패키지의 버전을 지정 합니다.

[환경 변수](cli-ref-environment-variables.md) 참조

## <a name="examples"></a>예

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
