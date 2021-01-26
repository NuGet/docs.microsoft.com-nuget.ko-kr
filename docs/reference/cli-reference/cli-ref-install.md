---
title: NuGet CLI 설치 명령
description: nuget.exe install 명령에 대 한 참조
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 34b79bfa7a0dddf5da6b5c465293caec49129f6c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779261"
---
# <a name="install-command-nuget-cli"></a>install 명령 (NuGet CLI)

**적용 대상:** 패키지 사용 &bullet; **지원 버전:** 모두

패키지를 다운로드 하 여 프로젝트에 설치 합니다. 기본적으로 현재 폴더는 지정 된 패키지 소스를 사용 합니다.

> [!Tip]
> 프로젝트의 컨텍스트 외부에서 직접 패키지를 다운로드 하려면 [nuget.org](https://www.nuget.org) 의 패키지 페이지를 방문 하 여 **다운로드** 링크를 선택 합니다.

지정 된 원본이 없으면 전역 구성 파일 `%appdata%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)에 나열 된 소스가 사용 됩니다. 자세한 내용은 [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md) 을 참조 하세요.

특정 패키지를 지정 하지 않으면는 `install` 프로젝트의 파일에 나열 된 모든 패키지를 설치 하 `packages.config` 여와 유사 하 게 만듭니다 [`restore`](cli-ref-restore.md) .

`install`이 명령은 프로젝트 파일을 수정 하지 않습니다 `packages.config` .이 방법에서는 `restore` 패키지를 디스크에만 추가 하지만 프로젝트의 종속성은 변경 하지 않는다는 점에서와 비슷합니다.

종속성을 추가 하려면 Visual Studio에서 패키지 관리자 UI 또는 콘솔을 통해 패키지를 추가 하거나를 수정 `packages.config` 하 고 또는를 실행 `install` `restore` 합니다.

## <a name="usage"></a>사용량

```cli
nuget install <packageID | configFilePath> [options]
```

여기서는 `<packageID>` 최신 버전을 사용 하 여 설치할 패키지의 이름을, 또는 `<configFilePath>` `packages.config` 설치할 패키지를 나열 하는 파일을 식별 합니다. 옵션을 사용 하 여 특정 버전을 나타낼 수 있습니다 `-Version` .

## <a name="options"></a>옵션

- **`-ConfigFile`**

  적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.

- **`-DependencyVersion`**

  *(4.4 +)* 사용할 종속성 패키지의 버전은 다음 중 하나일 수 있습니다.<br/><ul><li>*가장 낮음* (기본값): 가장 낮은 버전</li><li>*HighestPatch*: 최하위 주, 최저 부, 최고 패치가 있는 버전</li><li>*HighestMinor*: 최하위 주, 가장 높은 부, 최고 패치가 있는 버전</li><li>*최고*: 최고 버전</li><li>*무시*: 종속성 패키지가 사용 되지 않습니다.</li></ul>

- **`-DirectDownload`**

  메타 데이터 또는 이진 파일을 사용 하 여 캐시를 채우지 않고 직접 다운로드 합니다.

- **`-DisableParallelProcessing`**

  여러 패키지를 동시에 설치할 수 없도록 설정 합니다.

- **`-x|-ExcludeVersion`**

  패키지 이름만 사용 하 고 버전 번호를 사용 하 여 라는 이름의 폴더에 패키지를 설치 합니다.

- **`-FallbackSource`**

  *(3.2 이상)* 주 또는 기본 원본에서 패키지를 찾을 수 없는 경우 대체로 사용할 패키지 원본 목록입니다.

- **`-ForceEnglishOutput`**

  *(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.

- **`-Framework`**

  *(4.4 +)* 종속성을 선택 하는 데 사용 되는 대상 프레임 워크입니다. 지정 하지 않으면 기본값은 ' a l l '입니다.

- **`-?|-help`**

  명령에 대 한 도움말 정보를 표시 합니다.

- **`-NoCache`**

  NuGet이 캐시 된 패키지를 사용 하지 못하도록 합니다. [전역 패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요.

- **`-NonInteractive`**

  사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.

- **`-OutputDirectory`**

  패키지가 설치 되는 폴더를 지정 합니다. 폴더를 지정 하지 않으면 현재 폴더가 사용 됩니다.

- **`-PackageSaveMode`**

  패키지 설치 후 저장할 파일 유형을 지정 합니다., 또는 중 하나 `nuspec` 입니다 `nupkg` `nuspec;nupkg` .

- **`-PreRelease`**

  시험판 패키지를 설치할 수 있습니다. 이 플래그는를 사용 하 여 패키지를 복원 하는 경우에는 필요 하지 않습니다 `packages.config` .

- **`-RequireConsent`**

  패키지를 다운로드 하 고 설치 하기 전에 패키지 복원이 사용 되는지 확인 합니다. 자세한 내용은 [패키지 복원](../../consume-packages/package-restore.md)을 참조 하세요.

- **`-SolutionDirectory`**

  패키지를 복원할 솔루션의 루트 폴더를 지정 합니다.

- **`-Source`**

   사용할 패키지 원본 (Url) 목록을 지정 합니다. 생략 하는 경우 명령은 구성 파일에 제공 된 소스를 사용 합니다. [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md)을 참조 하세요.

- **`-Verbosity [normal|quiet|detailed]`**

  출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.

- **`-Version`**

  설치할 패키지의 버전을 지정합니다.

[환경 변수](cli-ref-environment-variables.md) 참조

## <a name="examples"></a>예

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
