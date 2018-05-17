---
title: NuGet CLI 설치 명령
description: Nuget.exe 설치 명령에 대 한 참조
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 1c6ec1181f2f619eb8a4f2d87f7910f25b98e0f4
ms.sourcegitcommit: 00c4c809c69c16fcf4d81012eb53ea22f0691d0b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2018
---
# <a name="install-command-nuget-cli"></a>install 명령(NuGet CLI)

**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 모든

다운로드 하 고 지정 된 패키지 소스를 사용 하 여 현재 폴더를 프로젝트에 패키지를 설치 합니다.

> [!Tip]
> 프로젝트의 컨텍스트 외부 직접 패키지를 다운로드 하려면 패키지의 페이지를 방문 하십시오 [nuget.org](https://www.nuget.org) 선택 하 고는 **다운로드** 링크 합니다.

글로벌 구성 파일에 나열 된 원본이 지정 된 경우 `%appdata%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), 사용 됩니다. 참조 [NuGet 구성 동작](../consume-packages/configuring-nuget-behavior.md) 추가 세부 정보에 대 한 합니다.

특정 패키지를 지정 하는 경우 `install` 프로젝트의에 나열 된 패키지를 모두 설치 `packages.config` 파일 그룹과 같이 [ `restore` ](cli-ref-restore.md)합니다.

`install` 프로젝트 파일 수정 되지 않도록 또는 `packages.config`; 비슷하지만 이런 방식에서 `restore` 한다는 점에서 것만 디스크에 패키지를 추가 하면 프로젝트의 종속성을 변경 하지 않습니다.

종속성을 추가 하려면 Visual Studio에서 패키지 관리자 UI 또는 콘솔을 통해 패키지를 추가 하거나 수정 `packages.config` 하나를 실행 하 고 `install` 또는 `restore`합니다.

## <a name="usage"></a>사용법

```cli
nuget install <packageID | configFilePath> [options]
```

여기서 `<packageID>` (최신 버전 사용)를 설치 하려면 패키지 이름을 지정 하거나 `<configFilePath>` 식별는 `packages.config` 설치할 패키지를 나열 하는 파일입니다. 특정 버전을 나타낼 수 있습니다는 `-Version` 옵션입니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | 적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| DependencyVersion | *(4.4 +)*  기본 종속성 확인 하는 동작을 재정의 하는 특정 버전을 지정 합니다. |
| DisableParallelProcessing | 동시에 여러 패키지를 설치 하는 데 사용 하지 않습니다. |
| ExcludeVersion | 패키지 이름과 버전 번호가 아닙니다 라는 폴더를 패키지를 설치 합니다. |
| FallbackSource | *(3.2 +)*  패키지 주에서 찾을 수 없는 경우 대체도 사용할 패키지 소스 목록 또는 기본 소스입니다. |
| ForceEnglishOutput | *(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 프레임워크 | *(4.4 +)*  대상 프레임 워크 종속성을 선택 하는 데 사용 합니다. 기본값은 'Any' 형식 지정 하지 않은 경우입니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| NoCache | 캐시 된 패키지를 사용 하 여 NuGet을 방지 합니다. 참조 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| OutputDirectory | 패키지 설치 되는 폴더를 지정 합니다. 없는 폴더를 지정 하는 경우 현재 폴더가 사용 됩니다. |
| PackageSaveMode | 패키지 설치 후 저장할 파일의 형식을 지정 합니다: 중 `nuspec`, `nupkg`, 또는 `nuspec;nupkg`합니다. |
| PreRelease | 시험판 패키지를를 설치할 수 있습니다. 사용 하 여 패키지를 복원 하는 경우이 플래그는 필요 하지 `packages.config`합니다. |
| RequireConsent | 다운로드 하 고 패키지를 설치 하기 전에 패키지를 복원 활성화 되어 있는지 확인 합니다. 자세한 내용은 참조 [패키지 복원](../consume-packages/package-restore.md)합니다. |
| SolutionDirectory | 패키지를 복원 하도록 솔루션의 루트 폴더를 지정 합니다. |
| 소스 | (Url)로 패키지 소스 목록의 사용 하도록 지정 합니다. 구성 파일에 제공 된 원본을 사용 하 여 생략 된 경우, 참조 [NuGet 구성 동작](../consume-packages/configuring-nuget-behavior.md)합니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다. |
| 버전 | 설치할 패키지의 버전을 지정 합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
