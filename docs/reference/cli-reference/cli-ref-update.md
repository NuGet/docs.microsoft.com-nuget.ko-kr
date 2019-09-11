---
title: NuGet CLI 업데이트 명령
description: Nuget.exe update 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327510"
---
# <a name="update-command-nuget-cli"></a>update 명령(NuGet CLI)

**적용 대상:** 패키지 &bullet; 사용 **지원 버전:** 모두

프로젝트의 모든 패키지(`packages.config` 사용)를 사용 가능한 최신 버전으로 업데이트합니다. 을`update`실행 하기 전에 [' 복원 '](cli-ref-restore.md) 을 실행 하는 것이 좋습니다. 개별 패키지를 업데이트 하려면 버전 번호를 [`nuget install`](cli-ref-install.md) 지정 하지 않고를 사용 합니다 .이 경우 NuGet은 최신 버전을 설치 합니다.

참고: `update` 는 Mono (Mac OSX 또는 Linux)에서 실행 되는 CLI 또는 PackageReference 형식을 사용 하는 경우에는 작동 하지 않습니다.

이러한 참조가 이미 있는 경우이 명령은프로젝트파일의어셈블리참조도업데이트합니다.`update` 업데이트 된 패키지에 추가 된 어셈블리가 있으면 새 참조가 추가 *되지 않습니다* . 새 패키지 종속성에도 해당 어셈블리 참조가 추가 되지 않습니다. 이러한 작업을 업데이트의 일부로 포함 하려면 패키지 관리자 UI 또는 패키지 관리자 콘솔을 사용 하 여 Visual Studio에서 패키지를 업데이트 합니다.

이 명령은 *-self* 플래그를 사용 하 여 nuget.exe 자체를 업데이트 하는 데도 사용할 수 있습니다.

## <a name="usage"></a>사용

```cli
nuget update <configPath> [options]
```

여기서 `<configPath>` 는 프로젝트의 `packages.config` 종속성을 나열 하는 또는 솔루션 파일을 식별 합니다.

## <a name="options"></a>변수

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | 적용할 NuGet 설정 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| FileConflictAction | 프로젝트에서 참조 하는 기존 파일을 덮어쓰거나 무시 하도록 요청 된 경우 수행할 동작을 지정 합니다. 값은 *overwrite, ignore, none*입니다. |
| ForceEnglishOutput | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| Help | 명령어에 대한 도움말을 표시합니다. |
| ID | 업데이트할 패키지 Id의 목록을 지정 합니다. |
| MSBuildPath | *(4.0 이상)* 명령에 사용할 MSBuild의 경로를 지정 합니다 `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 이상)* 이 명령에 사용할 MSBuild의 버전을 지정 합니다. 지원 되는 값은 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9입니다. 기본적으로 경로에 MSBuild가 선택 되어 있으며, 그렇지 않은 경우 기본적으로 설치 되어 있는 MSBuild의 가장 높은 버전으로 설정 됩니다. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| PreRelease | 시험판 버전으로 업데이트할 수 있습니다. 이미 설치 된 시험판 패키지를 업데이트 하는 경우에는이 플래그가 필요 하지 않습니다. |
| RepositoryPath | 패키지가 설치 되는 로컬 폴더를 지정 합니다. |
| 색상 | 설치 된 패키지와 동일한 주 버전 및 부 버전 내에서 가장 높은 버전의 업데이트만 사용할 수 있도록 지정 합니다. |
| 자체 | Nuget.exe를 최신 버전으로 업데이트 합니다. 다른 모든 인수는 무시 됩니다. |
| Source | 업데이트에 사용할 패키지 원본 (Url) 목록을 지정 합니다. 생략 하는 경우 명령은 구성 파일에 제공 된 소스를 사용 합니다. [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md)을 참조 하세요. |
| Verbosity | 출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다. |
| 버전 | 하나의 패키지 ID와 함께 사용 하는 경우 업데이트할 패키지의 버전을 지정 합니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="examples"></a>예제

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
