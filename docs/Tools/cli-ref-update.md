---
title: "NuGet CLI 명령 업데이트 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe update 명령에 대 한 참조"
keywords: "nuget 업데이트 참조에 업데이트 패키지 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6acf3a74e5c26bc4e2cef9b0db4a72442d311449
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="update-command-nuget-cli"></a>업데이트 명령 (NuGet CLI)

**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 모든

프로젝트의 모든 패키지를 업데이트 (사용 하 여 `packages.config`)를 사용할 수 있는 최신 버전입니다. 실행 하는 것이 좋습니다. ['restore'](cli-ref-restore.md) 실행 하기 전에 `update`합니다. (사용 하 여 개별 패키지를 업데이트 하려면 [ `nuget install` ](cli-ref-install.md) 사례 NuGet 최신 버전을 설치 하는 버전 번호를 지정 하지 않고.)

참고: `update` PackageReference 형식을 사용할 때 모노 (Mac OSX 또는 Linux)에서 또는 실행 하는 CLI 호환 되지 않습니다.

`update` 명령은 또한 프로젝트 파일에서 어셈블리 참조를 업데이트, 이미 참조 하는 것 제공 존재 합니다. 업데이트 된 패키지에 추가 된 어셈블리를 새 참조는 *하지* 추가 합니다. 또한 새 패키지 종속 파일의 어셈블리 참조 추가 필요가 없습니다. 이러한 작업에 대 한 업데이트의 일부로 포함 하려면 패키지 관리자 UI 또는 패키지 관리자 콘솔을 사용 하 여 Visual Studio에서 패키지를 업데이트 합니다.

Nuget.exe 자체를 업데이트 하려면이 명령을 사용할 수도 있습니다를 사용 하는 *-자체* 플래그입니다.

## <a name="usage"></a>사용법

```cli
nuget update <configPath> [options]
```

여기서 `<configPath>` 중 하나를 식별 하는 `packages.config` 또는 솔루션 파일을 프로젝트의 종속성을 나열 합니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | 적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| FileConflictAction | 덮어쓰거나 프로젝트에서 참조 하는 기존 파일을 무시 하도록 요청 될 때 수행할 동작을 지정 합니다. 값은 *덮어쓰기, none 무시*합니다. |
| ForceEnglishOutput | *(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| ID | 패키지를 업데이트 하는 Id의 목록을 지정 합니다. |
| MSBuildPath | *(4.0 이상)*  우선 순위를 차지 명령으로 사용 하는 MSBuild의 경로 지정 `-MSBuildVersion`합니다. |
| MSBuildVersion | *(3.2 +)*  이 명령과 함께 사용할 MSBuild의 버전을 지정 합니다. 지원 되는 값은 4, 12, 14, 15입니다. 경로에 MSBuild 선택은 기본적으로 그렇지 않은 경우 기본값이 가장 높은 설치 된 버전의 MSBuild 됩니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| 시험판 | 시험판 버전에 업데이트를 허용 합니다. 이미 설치 되어 있는 시험판 패키지를 업데이트 하는 경우에이 플래그가 필요 하지 않습니다. |
| RepositoryPath | 패키지 설치 된 로컬 폴더를 지정 합니다. |
| 안전 | 업데이트 하는 동일한 주 및 부 버전에서 사용할 수 있는 가장 높은 버전으로 설치 된 패키지가 설치를 지정 합니다. |
| 자체 | Nuget.exe; 최신 버전으로 업데이트 다른 모든 인수는 무시 됩니다. |
| 소스 | 업데이트를 사용 하도록 (Url)로 패키지 소스 목록을 지정 합니다. 구성 파일에 제공 된 원본을 사용 하 여 생략 된 경우, 참조 [NuGet 구성 동작](../consume-packages/configuring-nuget-behavior.md)합니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다. |
| 버전 | 하나의 패키지 ID를 사용할 때는 업데이트할 패키지의 버전을 지정 합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
