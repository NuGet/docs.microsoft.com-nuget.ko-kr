---
title: NuGet 패키지 복원
description: 복원을 사용하지 않도록 설정하고 버전을 제한하는 방법을 포함하여 NuGet에서 프로젝트가 종속된 패키지를 복원하는 방법을 간략히 설명합니다.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 3b64c035886818496339fe1bdd8f9abce060278a
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467804"
---
# <a name="package-restore"></a>패키지 복원

더 정돈된 개발 환경을 촉진하고 리포지토리 크기를 줄이기 위해 NuGet **패키지 복원**은 프로젝트 파일 또는 `packages.config`에 나열된 프로젝트의 종속성을 모두 설치합니다. .NET Core 2.0+ `dotnet build` 및 `dotnet run` 명령은 자동 패키지 복원을 수행합니다. Visual Studio는 프로젝트를 빌드할 때 패키지를 자동으로 복원할 수 있으며 Visual Studio, `nuget restore`, `dotnet restore` 및 Mono의 xbuild를 통해 언제든지 패키지를 복원할 수 있습니다.

패키지 복원은 모든 프로젝트의 종속성을 소스 제어에 저장하지 않고 사용할 수 있도록 합니다. 패키지 이진 파일을 제외하도록 소스 제어 리포지토리를 구성하려면 [패키지 및 소스 제어](../consume-packages/packages-and-source-control.md)를 참조하세요. 

## <a name="package-restore-overview"></a>패키지 복원 개요

패키지 복원은 먼저 필요에 따라 프로젝트의 직접 종속성을 설치한 다음, 전체 종속성 그래프에서 해당 패키지의 종속성을 설치합니다.

패키지가 아직 설치되지 않은 경우 NuGet은 먼저 [캐시](../consume-packages/managing-the-global-packages-and-cache-folders.md)에서 검색을 시도합니다. 패키지가 캐시에 없는 경우 NuGet은 Visual Studio에서 **도구** > **옵션** > **NuGet 패키지 관리자** > **패키지 원본**의 목록에 있는 사용 가능한 모든 소스에서 패키지를 다운로드하려고 시도합니다. 복원하는 동안 NuGet은 패키지 소스의 순서를 무시하고, 소스가 요청에 응답하는 순서대로 패키지를 사용합니다. NuGet 동작 방식에 대한 자세한 내용은 [일반적인 NuGet 구성](Configuring-NuGet-Behavior.md)을 참조하세요. 

> [!Note]
> NuGet은 모든 소스가 확인될 때까지 패키지 복원 실패를 표시하지 않습니다. 이때 NuGet은 목록의 마지막 소스에 대한 실패만 보고합니다. 이러한 오류는 각 소스에 대한 오류가 개별적으로 표시되지 않았더라도 패키지가 다른 *어떤* 소스에도 존재하지 않음을 암시합니다.

다음 방법 중 하나로 패키지 복원을 트리거할 수 있습니다.

- **dotnet CLI**: [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 명령을 사용하여 프로젝트 파일에 나열된 패키지를 [PackageReference](../consume-packages/package-references-in-project-files.md)로 복원합니다. .NET Core 2.0 이상에서는 `dotnet build` 및 `dotnet run` 명령을 통해 복원이 자동으로 수행됩니다.  

- **패키지 관리자**: Windows의 Visual Studio에서 패키지 복원은 [패키지 복원 활성화 및 비활성화](#enable-and-disable-package-restore) 옵션에 따라 템플릿에서 프로젝트를 만들거나 프로젝트를 빌드할 때 자동으로 수행됩니다. NuGet 4.0 이상에서는 .NET Core SDK 기반 프로젝트가 변경되면 자동으로 복원됩니다.

    패키지를 수동으로 복원하려면 **솔루션 탐색기**에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 복원**을 선택합니다. 하나 이상의 개별 패키지가 아직 제대로 설치되지 않은 경우 **솔루션 탐색기**에 오류 아이콘이 표시됩니다. 마우스 오른쪽 단추를 클릭하고 **NuGet 패키지 관리**를 선택하고 **패키지 관리자**를 사용하여 영향을 받은 패키지를 제거하고 다시 설치합니다. 자세한 내용은 [패키지 다시 설치 및 업데이트](../consume-packages/reinstalling-and-updating-packages.md)를 참조하세요.

    "이 프로젝트는 이 컴퓨터에 없는 NuGet 패키지를 참조합니다." 또는 "하나 이상의 NuGet 패키지를 복원해야 하지만 동의하지 않아 복원할 수 없습니다."라는 오류 메시지가 표시되면 [자동 복원을 사용하도록 설정](#enable-and-disable-package-restore)하세요. [패키지 복원 문제 해결](Package-restore-troubleshooting.md)도 참조하세요.

- **nuget.exe CLI**: [nuget restore](../tools/cli-ref-restore.md) 명령을 사용하여 프로젝트나 솔루션 파일 또는 `packages.config`에 나열된 패키지를 복원합니다. 

- **MSBuild**: [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) 명령을 사용하여 프로젝트 파일에 나열된 패키지를 PackageReference로 복원합니다. 이 명령은 Visual Studio 2017 이상 버전에 포함된 NuGet 4.x 이상 및 MSBuild 15.1 이상에서만 사용할 수 있습니다. `nuget restore` 및 `dotnet restore`는 모두 해당 프로젝트에 대해 이 명령을 사용합니다.

- **Azure Pipelines**: Azure Pipelines에서 빌드 정의를 만들 때 빌드 작업 전에 NuGet [복원](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) 또는 .NET Core [복원](/azure/devops/pipelines/tasks/build/dotnet-core#restore-nuget-packages) 작업을 정의에 포함합니다. 몇 가지 빌드 템플릿에는 기본적으로 복원 작업이 포함되어 있습니다.

- **Azure DevOps Server**: Azure DevOps Server 및 TFS 2013 이상에서는 TFS 2013 이상 팀 빌드 템플릿을 사용하는 경우 빌드 중에 패키지를 자동으로 복원합니다. 이전 TFS 버전의 경우 명령줄 복원 옵션을 실행하는 빌드 단계를 포함하거나 필요에 따라 빌드 템플릿을 최신 버전으로 마이그레이션할 수 있습니다. 자세한 내용은 [Team Foundation 빌드를 사용하여 패키지 복원 설정](../consume-packages/team-foundation-build.md)을 참조하세요.

## <a name="enable-and-disable-package-restore"></a>패키지 복원 활성화 및 비활성화

Visual Studio에서 주로 **도구** > **옵션** > **NuGet 패키지 관리자**를 통해 패키지 복원을 제어합니다.

![NuGet 패키지 관리자 옵션을 통한 패키지 복원 제어](media/Restore-01-AutoRestoreOptions.png)

- **NuGet이 누락된 패키지를 다운로드하도록 허용**은 `NuGet.Config` 파일(Windows의 경우 `%AppData%\NuGet\`, Mac/Linux의 경우 `~/.nuget/NuGet/`)의 [packageRestore 섹션](../reference/nuget-config-file.md#packagerestore-section)에서 `packageRestore/enabled` 설정을 변경하여 모든 형태의 패키지 복원을 제어합니다. 이 설정을 사용하면 Visual Studio의 솔루션 컨텍스트 메뉴에서 **NuGet 패키지 복원** 명령을 사용할 수도 있습니다.

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    
  > [!Note]
  > `packageRestore/enabled` 설정을 전역적으로 재정의하려면 Visual Studio를 시작하거나 빌드를 시작하기 전에 환경 변수 **EnableNuGetPackageRestore**를 True 또는 False 값으로 설정합니다.

- **Visual Studio에서 빌드 시 누락된 패키지를 자동으로 확인**은 `NuGet.Config` 파일의 [packageRestore 섹션](../reference/nuget-config-file.md#packagerestore-section)에서 `packageRestore/automatic` 설정을 변경하여 자동 복원을 제어합니다. 이 옵션을 True로 설정하면 Visual Studio에서 빌드를 실행할 경우 누락된 모든 패키지가 자동으로 복원됩니다. 이 설정은 MSBuild 명령줄에서 실행되는 빌드에 영향을 주지 않습니다.

    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

컴퓨터의 모든 사용자에 대해 패키지 복원을 활성화하거나 비활성화하기 위해 개발자 또는 회사가 구성 설정을 글로벌 `nuget.config` 파일에 추가할 수 있습니다. 글로벌 `nuget.config`는 `%ProgramData%\NuGet\Config`의 Windows, 경우에 따라 특정 `\{IDE}\{Version}\{SKU}\` Visual Studio 폴더 또는 `~/.local/share`의 Mac/Linux에 있습니다. 개별 사용자는 프로젝트 수준에서 필요에 따라 선택적으로 복원을 사용하도록 설정할 수 있습니다. NuGet에서 여러 구성 파일의 우선순위를 지정하는 방법에 대한 자세한 내용은 [일반적인 NuGet 구성](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)을 참조하세요.

> [!Important]
> `nuget.config`에서 `packageRestore` 설정을 바로 편집할 경우 Visual Studio를 다시 시작해야 **옵션** 대화 상자에 최신 값이 표시됩니다.

## <a name="constrain-package-versions-with-restore"></a>복원을 사용하여 패키지 버전 제한

어떤 방법으로든 NuGet에서 패키지를 복원하는 경우 `packages.config` 또는 프로젝트 파일에 지정된 제약 조건을 준수합니다.

- `packages.config`에서 종속성의 `allowedVersion` 속성에 버전 범위를 지정할 수 있습니다. 자세한 내용은 [업그레이드 버전 제한](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)을 참조하세요. 예:

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- 프로젝트 파일에서 PackageReference를 사용하여 종속성 범위를 직접 지정할 수 있습니다. 예:

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

모든 경우에 [패키지 버전 관리](../reference/package-versioning.md)에서 설명한 표기법을 사용하세요.

## <a name="force-restore-from-package-sources"></a>패키지 소스에서 강제로 복원

기본적으로 NuGet 복원 작업은 *global-packages* 및 *http-cache* 폴더의 패키지를 사용합니다. 이 내용은 [글로벌 패키지 및 캐시 폴더 관리](managing-the-global-packages-and-cache-folders.md)에 설명되어 있습니다.

*global-packages* 폴더를 사용하지 않으려면 다음 중 하나를 수행합니다.

- `nuget locals global-packages -clear` 또는 `dotnet nuget locals global-packages --clear`를 사용하여 폴더를 지웁니다.
- 복원 작업을 수행하기 전에 다음 방법 중 하나를 사용하여 *global-packages* 폴더의 위치를 임시로 변경합니다.
  - NUGET_PACKAGES 환경 변수를 다른 폴더로 설정합니다.
  - `globalPackagesFolder`(PackageReference를 사용할 경우) 또는 `repositoryPath`(`packages.config`를 사용할 경우)를 설정하는 `NuGet.Config` 파일을 다른 폴더에 만듭니다. 자세한 내용은 [구성 설정](../reference/nuget-config-file.md#config-section)을 참조하세요.
  - MSBuild에만 해당: `RestorePackagesPath` 속성을 사용하여 다른 폴더를 지정합니다.

캐시를 HTTP 소스로 사용하지 않으려면 다음 중 하나를 수행합니다.

- `nuget restore`에 `-NoCache` 옵션을 사용하거나 `dotnet restore`에 `--no-cache` 옵션을 사용합니다. 이러한 옵션은 Visual Studio 패키지 관리자 또는 콘솔을 통한 복원 작업에는 영향을 주지 않습니다.
- `nuget locals http-cache -clear` 또는 `dotnet nuget locals http-cache --clear`를 사용하여 캐시를 지웁니다.
- 임시로 NUGET_HTTP_CACHE_PATH 환경 변수를 다른 폴더로 설정합니다.

## <a name="troubleshooting"></a>문제 해결

[패키지 복원 문제 해결](package-restore-troubleshooting.md)을 참조하세요.
