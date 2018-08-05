---
title: NuGet CLI 설치 명령
description: Nuget.exe 설치 명령에 대 한 참조
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e609b01bc14083ce212f6d4d4c6d3412f0ee316b
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508324"
---
# <a name="install-command-nuget-cli"></a>install 명령(NuGet CLI)

**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 모든

다운로드 하 고 지정 된 패키지 소스를 사용 하 여 현재 폴더를 기본값으로 프로젝트에 패키지를 설치 합니다.

> [!Tip]
> 프로젝트의 컨텍스트 외부 직접 패키지를 다운로드 하려면에 패키지의 페이지를 방문 [nuget.org](https://www.nuget.org) 선택 합니다 **다운로드** 링크.

전역 구성 파일에 없는 소스를 지정 하는 경우 나열한 `%appdata%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), 사용 됩니다. 참조 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md) 추가 세부 정보에 대 한 합니다.

없는 특정 패키지를 지정 하는 경우 `install` 프로젝트의 나열 된 모든 패키지를 설치 `packages.config` 파일을 유사 하므로 [ `restore` ](cli-ref-restore.md)합니다.

합니다 `install` 명령은 프로젝트 파일을 수정 하지 않습니다 또는 `packages.config`; 비슷합니다 이런 `restore` 것만 디스크에 패키지를 추가 하지만 프로젝트의 종속성을 변경 하지 않습니다.

종속성을 추가 하려면 Visual Studio에서 패키지 관리자 UI 또는 콘솔을 통해 패키지를 추가 또는 수정 `packages.config` 하나를 실행할 `install` 또는 `restore`합니다.

## <a name="usage"></a>사용법

```cli
nuget install <packageID | configFilePath> [options]
```

여기서 `<packageID>` (최신 버전 사용) 설치를 위해 패키지 이름 또는 `<configFilePath>` 하 게 식별 하는 `packages.config` 나열 패키지를 설치 하는 파일. 사용 하 여 특정 버전을 지정할 수 있습니다는 `-Version` 옵션입니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | NuGet 구성 파일을 적용 합니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| DependencyVersion | *(4.4 이상)*  다음 중 하나일 수 있습니다를 사용 하려면 종속성 패키지의 버전:<br/><ul><li>*가장 낮은* (기본값): 가장 낮은 버전</li><li>*HighestPatch*: 가장 낮은 주요, 가장 낮은 부 최고 패치 버전</li><li>*HighestMinor*: 가장 낮은 주 버전, 가장 높은 보조, 최고의 패치</li><li>*가장 높은*: 가장 높은 버전</li></ul> |
| DisableParallelProcessing | 병렬로 여러 패키지를 설치 하는 사용 하지 않도록 설정 합니다. |
| ExcludeVersion | 패키지 이름과 버전 번호가 없습니다 사용 하 여 폴더에 패키지를 설치 합니다. |
| FallbackSource | *(3.2 이상)*  패키지 주 서버에 없는 경우 대체도 사용할 패키지 원본의 목록 또는 기본 소스입니다. |
| ForceEnglishOutput | *(3.5 이상)*  고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 프레임워크 | *(4.4 이상)*  대상 프레임 워크 종속성을 선택 하는 데 사용 합니다. 기본값은 'Any' 지정 되지 않은 경우입니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| NoCache | 캐시 된 패키지를 사용 하 여 NuGet을 방지 합니다. 참조 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| OutputDirectory | 패키지 설치 되는 폴더를 지정 합니다. 폴더는 지정 하지 않으면 현재 폴더가 사용 됩니다. |
| PackageSaveMode | 패키지를 설치한 후 파일의 형식을 지정 합니다: 중 하나 `nuspec`, `nupkg`, 또는 `nuspec;nupkg`합니다. |
| PreRelease | 시험판 패키지를를 설치할 수 있습니다. 사용 하 여 패키지를 복원 하는 경우이 플래그는 필요 하지 `packages.config`합니다. |
| RequireConsent | 다운로드 하 고 패키지를 설치 하기 전에 패키지 복원 활성화 되어 있는지 확인 합니다. 자세한 내용은 참조 하세요 [패키지 복원](../consume-packages/package-restore.md)합니다. |
| SolutionDirectory | 패키지를 복원 하는 솔루션의 루트 폴더를 지정 합니다. |
| 소스 | 사용 하도록 (Url)로 패키지 소스 목록을 지정 합니다. 생략 하면 사용 하 여 구성 파일에서 제공 하는 소스를 참조 하십시오 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)합니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다. |
| 버전 | 설치 패키지의 버전을 지정 합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
