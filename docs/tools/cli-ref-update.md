---
title: NuGet CLI 업데이트 명령
description: Nuget.exe 업데이트 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a242d02a54fd86899cbe274ab63538b53307c1bb
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425910"
---
# <a name="update-command-nuget-cli"></a>update 명령(NuGet CLI)

**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 모든

프로젝트의 모든 패키지 업데이트 (사용 하 여 `packages.config`) 사용 가능한 최신 버전으로 합니다. 실행 하는 것이 좋습니다 ['restore'](cli-ref-restore.md) 실행 하기 전에 `update`합니다. (사용 하 여 개별 패키지를 업데이트 하려면 [ `nuget install` ](cli-ref-install.md) 사례 NuGet 최신 버전을 설치 하는 버전 번호를 지정 하지 않고.)

참고: `update` PackageReference 형식을 사용 하는 경우 Mono (Mac OSX 또는 Linux)에서 또는 실행 하는 CLI를 사용 하 여 작동 하지 않습니다.

`update` 명령은 프로젝트 파일에서 어셈블리 참조를 업데이트도, 이미 참조 된 제공 존재 합니다. 새 참조는 업데이트 된 패키지에 어셈블리를 추가 하는 경우 *되지* 추가 합니다. 또한 새 패키지 종속성 추가 어셈블리 참조는 없습니다. 이러한 작업에는 업데이트의 일부로 포함 하려면 패키지 관리자 UI 또는 패키지 관리자 콘솔을 사용 하 여 Visual Studio에서 패키지를 업데이트 합니다.

Nuget.exe 자체를 업데이트 하려면이 명령을 사용할 수도 있습니다를 사용 하는 *-자체* 플래그입니다.

## <a name="usage"></a>사용법

```cli
nuget update <configPath> [options]
```

여기서 `<configPath>` 중 하나를 식별 하는 `packages.config` 또는 프로젝트의 종속성을 나열 하는 솔루션 파일입니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | 적용할 NuGet 설정 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| FileConflictAction | 덮어쓰거나 프로젝트에서 참조 하는 기존 파일을 무시 하 라는 메시지가 표시 되는 경우 수행할 동작을 지정 합니다. 값은 *덮어쓰기, none 무시*합니다. |
| ForceEnglishOutput | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| Help | 명령어에 대한 도움말을 표시합니다. |
| ID | 패키지를 업데이트 하는 Id의 목록을 지정 합니다. |
| MSBuildPath | *(4.0 이상)*  보다 우선함 명령으로 사용 하는 MSBuild의 경로 지정 `-MSBuildVersion`합니다. |
| MSBuildVersion | *(3.2 이상)*  이 명령을 사용 하 여 사용할 MSBuild의 버전을 지정 합니다. 지원 되는 값은 4, 12, 14, 15.1, 15.3, 15.4에서 15.5, 15.6, 15.7, 15.8, 15.9. 경로에 MSBuild 선택은 기본적으로 그렇지 않은 경우 기본값은 MSBuild의 설치 된 가장 높은 버전으로 합니다. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| PreRelease | 시험판 버전으로 업데이트를 허용 합니다. 이미 설치 되어 있는 시험판 패키지를 업데이트 하는 경우이 플래그는 필요 하지 않습니다. |
| RepositoryPath | 패키지 설치 되어 있는 로컬 폴더를 지정 합니다. |
| 안전 하 게 보호 | 만 업데이트 하는 동일한 주 및 부 버전에서 사용할 수 있는 가장 높은 버전을 사용 하 여 설치 된 패키지를 설치할 때 지정 합니다. |
| 자체 | Nuget.exe를 최신 버전; 업데이트 다른 모든 인수는 무시 됩니다. |
| Source | 업데이트에 사용할 (Url)로 패키지 소스 목록을 지정 합니다. 생략 하면 사용 하 여 구성 파일에서 제공 하는 소스를 참조 하십시오 [일반적인 NuGet 구성](../consume-packages/configuring-nuget-behavior.md)합니다. |
| Verbosity | 출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다. |
| 버전 | 하나의 패키지 ID를 사용 하면 업데이트할 패키지의 버전을 지정 합니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="examples"></a>예제

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
