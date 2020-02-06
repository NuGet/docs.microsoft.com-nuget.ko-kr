---
title: NuGet CLI 설치 명령
description: Nuget.exe 설치 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6c49b2406462eae6ce45c65dfd8b3a9eb1077e73
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036944"
---
# <a name="install-command-nuget-cli"></a>install 명령(NuGet CLI)

**적용 대상:** 패키지 사용 &bullet; **지원 되는 버전:** 모두

패키지를 다운로드 하 여 프로젝트에 설치 합니다. 기본적으로 현재 폴더는 지정 된 패키지 소스를 사용 합니다.

> [!Tip]
> 프로젝트의 컨텍스트 외부에서 직접 패키지를 다운로드 하려면 [nuget.org](https://www.nuget.org) 의 패키지 페이지를 방문 하 여 **다운로드** 링크를 선택 합니다.

지정 된 소스가 없으면 전역 구성 파일 `%appdata%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)에 나열 된 소스가 사용 됩니다. 자세한 내용은 [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md) 을 참조 하세요.

특정 패키지를 지정 하지 않으면 `install` 프로젝트의 `packages.config` 파일에 나열 된 모든 패키지를 설치 하 여 [`restore`](cli-ref-restore.md)와 유사 하 게 만듭니다.

`install` 명령은 프로젝트 파일이 나 `packages.config`를 수정 하지 않습니다. 이러한 방식으로 패키지를 디스크에 추가 하 고 프로젝트의 종속성을 변경 하지 않는다는 점에서 `restore`와 비슷합니다.

종속성을 추가 하려면 Visual Studio에서 패키지 관리자 UI 또는 콘솔을 통해 패키지를 추가 하거나 `packages.config` 수정한 후 `install` 또는 `restore`를 실행 합니다.

## <a name="usage"></a>사용

```cli
nuget install <packageID | configFilePath> [options]
```

(최신 버전을 사용 하 여 설치할 패키지의 이름을 `<packageID>` 하거나 설치할 패키지를 나열 하는 `packages.config` 파일을 `<configFilePath>` 식별 합니다. `-Version` 옵션을 사용 하 여 특정 버전을 나타낼 수 있습니다.

## <a name="options"></a>옵션

| 옵션 | Description |
| --- | --- |
| ConfigFile | 수정할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| DependencyVersion | *(4.4 +)* 사용할 종속성 패키지의 버전은 다음 중 하나일 수 있습니다.<br/><ul><li>*가장 낮음* (기본값): 가장 낮은 버전</li><li>*HighestPatch*: 최하위 주, 최저 부, 최고 패치가 있는 버전</li><li>*HighestMinor*: 최하위 주, 가장 높은 부, 최고 패치가 있는 버전</li><li>*최고*: 최고 버전</li><li>*무시*: 종속성 패키지가 사용 되지 않습니다.</li></ul> |
| DisableParallelProcessing | 여러 패키지를 동시에 설치할 수 없도록 설정 합니다. |
| ExcludeVersion | 패키지 이름만 사용 하 고 버전 번호를 사용 하 여 라는 이름의 폴더에 패키지를 설치 합니다. |
| FallbackSource | *(3.2 이상)* 주 또는 기본 원본에서 패키지를 찾을 수 없는 경우 대체로 사용할 패키지 원본 목록입니다. |
| ForceEnglishOutput | *(3.5 +)* 고정 영어 기반 문화권을 사용 하 여 nuget.exe를 실행 합니다. |
| 프레임워크 | *(4.4 +)* 종속성을 선택 하는 데 사용 되는 대상 프레임 워크입니다. 지정 하지 않으면 기본값은 ' a l l '입니다. |
| 도움말 | 명령어에 대한 도움말을 표시합니다. |
| NoCache | NuGet이 캐시 된 패키지를 사용 하지 못하도록 합니다. [전역 패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| OutputDirectory | 패키지가 설치 되는 폴더를 지정 합니다. 폴더를 지정 하지 않으면 현재 폴더가 사용 됩니다. |
| PackageSaveMode | 패키지 설치 후 저장할 파일 유형을 지정 합니다. `nuspec`, `nupkg`또는 `nuspec;nupkg`중 하나입니다. |
| PreRelease | 시험판 패키지를 설치할 수 있습니다. `packages.config`를 사용 하 여 패키지를 복원 하는 경우이 플래그는 필요 하지 않습니다. |
| RequireConsent | 패키지를 다운로드 하 고 설치 하기 전에 패키지 복원이 사용 되는지 확인 합니다. 자세한 내용은 [패키지 복원](../../consume-packages/package-restore.md)을 참조 하세요. |
| SolutionDirectory | 패키지를 복원할 솔루션의 루트 폴더를 지정 합니다. |
| 원본 | 사용할 패키지 원본 (Url) 목록을 지정 합니다. 생략 하는 경우 명령은 구성 파일에 제공 된 소스를 사용 합니다. [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md)을 참조 하세요. |
| 자세한 정도 | 출력에 표시 되는 세부 정보의 양을 지정 합니다. *보통*, *자동*, *자세히*입니다. |
| 버전 | 설치할 패키지의 버전을 지정합니다. |

[환경 변수](cli-ref-environment-variables.md) 참조

## <a name="examples"></a>예

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
