---
title: NuGet CLI 설치 명령
description: Nuget.exe 설치 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f39bcc67c5f659f05ef02f2579bcf07b4481bb27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327790"
---
# <a name="install-command-nuget-cli"></a>install 명령(NuGet CLI)

**적용 대상:** 패키지 &bullet; 사용 **지원 버전:** 모두

패키지를 다운로드 하 여 프로젝트에 설치 합니다. 기본적으로 현재 폴더는 지정 된 패키지 소스를 사용 합니다.

> [!Tip]
> 프로젝트의 컨텍스트 외부에서 직접 패키지를 다운로드 하려면 [nuget.org](https://www.nuget.org) 의 패키지 페이지를 방문 하 여 **다운로드** 링크를 선택 합니다.

지정 된 원본이 없으면 전역 구성 파일 `%appdata%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)에 나열 된 소스가 사용 됩니다. 자세한 내용은 [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md) 을 참조 하세요.

특정 패키지를 지정 하지 않으면는 `install` 프로젝트의 `packages.config` 파일에 나열 된 모든 패키지를 설치 하 여와 유사 [`restore`](cli-ref-restore.md)하 게 만듭니다.

이 명령은 프로젝트 `packages.config`파일을 수정 하지 않습니다 .이 `restore` 방법에서는 패키지를 디스크에만 추가 하지만 프로젝트의 종속성은 변경 하지 않는다는 점에서와 비슷합니다. `install`

종속성을 추가 하려면 Visual Studio에서 패키지 관리자 UI 또는 콘솔을 통해 패키지를 추가 하거나를 수정 `packages.config` 하 고 `install` 또는 `restore`를 실행 합니다.

## <a name="usage"></a>사용법

```cli
nuget install <packageID | configFilePath> [options]
```

여기서 `<packageID>` 는 최신 버전을 사용 하 여 설치할 패키지의 이름을, 또는 `<configFilePath>` 설치할 패키지 `packages.config` 를 나열 하는 파일을 식별 합니다. `-Version` 옵션을 사용 하 여 특정 버전을 나타낼 수 있습니다.

## <a name="options"></a>변수

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | 적용할 NuGet 설정 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| DependencyVersion | *(4.4 +)* 사용할 종속성 패키지의 버전은 다음 중 하나일 수 있습니다.<br/><ul><li>*최저* (기본값): 가장 낮은 버전</li><li>*HighestPatch*: 최하위 주, 최저 부, 최고 패치가 있는 버전</li><li>*HighestMinor*: 최하위 주, 가장 높은 부, 최고 패치가 있는 버전</li><li>*최고*: 최고 버전</li></ul> |
| DisableParallelProcessing | 여러 패키지를 동시에 설치할 수 없도록 설정 합니다. |
| ExcludeVersion | 패키지 이름만 사용 하 고 버전 번호를 사용 하 여 라는 이름의 폴더에 패키지를 설치 합니다. |
| FallbackSource | *(3.2 이상)* 주 또는 기본 원본에서 패키지를 찾을 수 없는 경우 대체로 사용할 패키지 원본 목록입니다. |
| ForceEnglishOutput | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| 프레임워크 | *(4.4 +)* 종속성을 선택 하는 데 사용 되는 대상 프레임 워크입니다. 지정 하지 않으면 기본값은 ' a l l '입니다. |
| Help | 명령어에 대한 도움말을 표시합니다. |
| NoCache | NuGet이 캐시 된 패키지를 사용 하지 못하도록 합니다. [전역 패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| OutputDirectory | 패키지가 설치 되는 폴더를 지정 합니다. 폴더를 지정 하지 않으면 현재 폴더가 사용 됩니다. |
| PackageSaveMode | 패키지 설치 후 저장할 파일 유형을 지정 합니다. `nuspec`, `nupkg`또는 `nuspec;nupkg`중 하나입니다. |
| PreRelease | 시험판 패키지를 설치할 수 있습니다. 이 플래그는를 사용 하 여 패키지를 `packages.config`복원 하는 경우에는 필요 하지 않습니다. |
| RequireConsent | 패키지를 다운로드 하 고 설치 하기 전에 패키지 복원이 사용 되는지 확인 합니다. 자세한 내용은 [패키지 복원](../../consume-packages/package-restore.md)을 참조 하세요. |
| SolutionDirectory | 패키지를 복원할 솔루션의 루트 폴더를 지정 합니다. |
| Source | 사용할 패키지 원본 (Url) 목록을 지정 합니다. 생략 하는 경우 명령은 구성 파일에 제공 된 소스를 사용 합니다. [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md)을 참조 하세요. |
| Verbosity | 출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다. |
| 버전 | 설치할 패키지의 버전을 지정 합니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="examples"></a>예제

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
