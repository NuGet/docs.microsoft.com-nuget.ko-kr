---
title: nuget.exe CLI를 사용하여 NuGet 패키지 관리
description: nuget.exe CLI를 사용하여 NuGet 패키지를 작업하기 위한 지침입니다.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: 9eefed6f2c1a362f27c4a5d33d07645d743379fa
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317742"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>nuget.exe CLI를 사용하여 패키지 관리

CLI 도구를 사용하면 프로젝트 및 솔루션에서 NuGet 패키지를 쉽게 업데이트하고 복원할 수 있습니다. 이 도구는 Windows에서 모든 NuGet 기능을 제공하며 Mono로 실행 중일 경우 Mac 및 Linux에서 대부분의 기능도 제공합니다.

`nuget.exe` CLI는 .NET Framework 프로젝트 및 SDK 스타일이 아닌 프로젝트(예: .NET Standard 라이브러리를 대상으로 하는 비 SDK 스타일 프로젝트)에 대한 것입니다. `PackageReference`로 마이그레이션된 SDK 스타일이 아닌 프로젝트를 사용하는 경우 대신 `dotnet` CLI를 사용합니다. `nuget.exe` CLI에는 패키지 참조에 대한 [packages.config](../reference/packages-config.md) 파일이 필요합니다.

> [!NOTE]
> 대부분의 시나리오에서는 PackageReference에 `packages.config`를 사용하는 [SDK 스타일이 아닌 프로젝트를 마이그레이션](../reference/migrate-packages-config-to-package-reference.md)한 다음, `nuget.exe` CLI 대신 `dotnet` CLI를 사용하는 것이 좋습니다. 현재 C++ 및 ASP.NET 프로젝트에는 마이그레이션이 제공되지 않습니다.

이 문서에서는 가장 일반적인 몇 가지 `nuget.exe` CLI 명령에 대한 기본 사용법을 보여줍니다. 이러한 명령의 대부분의 경우, CLI 도구는 프로젝트 파일이 명령에 지정되지 않는 한 현재 디렉터리에서 프로젝트 파일을 찾습니다. 사용할 수 있는 명령 및 전체 목록은 [nuget.exe CLI 참조](../reference/nuget-exe-cli-reference.md)를 참조하세요.

## <a name="prerequisites"></a>전제 조건

- `nuget.exe` CLI를 설치하려면 [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe)에서 다운로드하고, 해당 `.exe` 파일을 적합한 폴더에 저장하고, 해당 폴더를 PATH 환경 변수에 추가합니다.

## <a name="install-a-package"></a>패키지 설치

[설치](../reference/cli-reference/cli-ref-install.md) 명령은 지정된 패키지 소스를 사용하여 현재 폴더를 기본값으로 프로젝트에 패키지를 다운로드하고 설치합니다. 새 패키지를 프로젝트 루트 디렉터리의 *패키지* 폴더에 설치합니다.

> [!IMPORTANT]
> `install` 명령은 프로젝트 파일이나 *packages.config*을 수정하지 않습니다. 이러한 방식으로 패키지를 디스크에만 추가하지만 프로젝트의 종속성은 변경하지 않는다는 점에서 `restore`와 유사합니다. 종속성을 추가하려면 패키지 관리자 UI 또는 Visual Studio의 콘솔을 통해 패키지를 추가하거나 *packages.config*를 수정한 다음, `install` 또는 `restore` 중 하나를 실행합니다.

1. 명령줄을 열고 프로젝트 파일이 포함된 디렉터리로 전환합니다.

2. 다음 명령을 사용하여 NuGet 패키지를 *패키지* 폴더에 설치합니다.

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    `Newtonsoft.json` 패키지를 *패키지* 폴더에 설치하려면 다음 명령을 사용합니다.

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

또는 다음 명령을 사용하여 기존 `packages.config` 파일을 통해 NuGet 패키지를 *패키지* 폴더에 설치할 수 있습니다. 이렇게 하면 패키지가 프로젝트 종속성에 추가되지 않고 로컬로 설치됩니다.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>특정 버전의 패키지 설치

[설치](../reference/cli-reference/cli-ref-install.md) 명령을 사용할 때 버전이 지정되지 않은 경우 NuGet은 패키지의 최신 버전을 설치합니다. 특정 버전의 Nuget 패키지를 설치할 수도 있습니다.

```cli
nuget install <packageID | configFilePath> -Version <version>
```

예를 들어 `Newtonsoft.json` 패키지의 버전 12.0.1을 추가하려면 다음 명령을 사용합니다.

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

`install`의 제한 사항 및 동작에 대한 자세한 내용은 [패키지 설치](#install-a-package)를 참조하세요.

## <a name="remove-a-package"></a>패키지 제거

하나 이상의 패키지를 삭제하려면 *패키지* 폴더에서 제거할 패키지를 삭제합니다.

패키지 다시 설치하려면 `restore` 또는 `install` 명령을 사용합니다.

## <a name="list-packages"></a>패키지 나열

[list](../reference/cli-reference/cli-ref-list.md) 명령을 사용하여 지정된 소스에서 패키지 목록을 표시할 수 있습니다. `-Source` 옵션을 사용하여 검색을 제한합니다.

```cli
nuget list -Source <source>
```

예를 들어 *패키지* 폴더에 패키지를 나열합니다.

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

검색 용어를 사용하는 경우 패키지 이름, 태그 및 패키지 설명이 검색에 포함됩니다.

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>개별 패키지 업데이트

패키지 버전을 지정하지 않는 한 `install` 명령을 사용할 때 NuGet은 패키지의 최신 버전을 설치합니다.

## <a name="update-all-packages"></a>모든 패키지 업데이트

[업데이트](../reference/cli-reference/cli-ref-update.md) 명령을 사용하여 모든 패키지를 업데이트합니다. 프로젝트의 모든 패키지(`packages.config` 사용)를 사용 가능한 최신 버전으로 업데이트합니다. `update`를 실행하기 전에 `restore`를 실행하는 것이 좋습니다.

```cli
nuget update
```

## <a name="restore-packages"></a>패키지 복원

[복원](../reference/cli-reference/cli-ref-restore.md) 명령을 사용하면 *패키지* 폴더에서 누락된 모든 패키지를 다운로드하고 설치할 수 있습니다.

`restore`는 디스크에만 패키지를 추가하지만 프로젝트의 종속성은 변경하지 않습니다. 프로젝트 종속성을 복원하려면 `packages.config`를 수정한 다음, `restore` 명령을 사용합니다.

다른 `nuget.exe` CLI 명령을 사용할 때처럼 명령줄을 열고 프로젝트 파일이 포함된 디렉터리로 전환합니다.

`restore`를 사용하여 패키지를 복원하려면 다음을 수행합니다.

```cli
nuget restore MySolution.sln
```