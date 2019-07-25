---
title: NuGet 패키지 복원
description: 복원을 사용하지 않도록 설정하고 버전을 제한하는 방법을 포함하여 NuGet에서 프로젝트가 종속된 패키지를 복원하는 방법을 간략히 설명합니다.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 0df2b0ebcf438fba99291558f1cf929dcb32618b
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68316982"
---
# <a name="package-restore-options"></a><span data-ttu-id="afd21-103">패키지 복원 옵션</span><span class="sxs-lookup"><span data-stu-id="afd21-103">Package Restore options</span></span>

<span data-ttu-id="afd21-104">더 정돈된 개발 환경을 촉진하고 리포지토리 크기를 줄이기 위해 NuGet **패키지 복원**은 프로젝트 파일 또는 `packages.config`에 나열된 프로젝트의 종속성을 모두 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-104">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all of a project's dependencies listed in either the project file or `packages.config`.</span></span> <span data-ttu-id="afd21-105">.NET Core 2.0+ `dotnet build` 및 `dotnet run` 명령은 자동 패키지 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-105">The .NET Core 2.0+ `dotnet build` and `dotnet run` commands do an automatic package restore.</span></span> <span data-ttu-id="afd21-106">Visual Studio는 프로젝트를 빌드할 때 패키지를 자동으로 복원할 수 있으며 Visual Studio, `nuget restore`, `dotnet restore` 및 Mono의 xbuild를 통해 언제든지 패키지를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-106">Visual Studio can restore packages automatically when it builds a project, and you can restore packages at any time through Visual Studio, `nuget restore`, `dotnet restore`, and xbuild on Mono.</span></span>

<span data-ttu-id="afd21-107">패키지 복원은 모든 프로젝트의 종속성을 소스 제어에 저장하지 않고 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-107">Package Restore makes sure that all a project's dependencies are available, without having to store them in source control.</span></span> <span data-ttu-id="afd21-108">패키지 이진 파일을 제외하도록 소스 제어 리포지토리를 구성하려면 [패키지 및 소스 제어](../consume-packages/packages-and-source-control.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afd21-108">To configure your source control repository to exclude the package binaries, see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> 

## <a name="package-restore-overview"></a><span data-ttu-id="afd21-109">패키지 복원 개요</span><span class="sxs-lookup"><span data-stu-id="afd21-109">Package Restore overview</span></span>

<span data-ttu-id="afd21-110">패키지 복원은 먼저 필요에 따라 프로젝트의 직접 종속성을 설치한 다음, 전체 종속성 그래프에서 해당 패키지의 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-110">Package Restore first installs the direct dependencies of a project as needed, then installs any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="afd21-111">패키지가 아직 설치되지 않은 경우 NuGet은 먼저 [캐시](../consume-packages/managing-the-global-packages-and-cache-folders.md)에서 검색을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-111">If a package isn't already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> <span data-ttu-id="afd21-112">패키지가 캐시에 없는 경우 NuGet은 Visual Studio에서 **도구** > **옵션** > **NuGet 패키지 관리자** > **패키지 원본**의 목록에 있는 사용 가능한 모든 소스에서 패키지를 다운로드하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-112">If the package isn't in the cache, NuGet tries to download the package from all enabled sources in the list at **Tools** > **Options** > **NuGet Package Manager** > **Package Sources** in Visual Studio.</span></span> <span data-ttu-id="afd21-113">복원하는 동안 NuGet은 패키지 소스의 순서를 무시하고, 소스가 요청에 응답하는 순서대로 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-113">During restore, NuGet ignores the order of package sources, and uses the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="afd21-114">NuGet 동작 방식에 대한 자세한 내용은 [일반적인 NuGet 구성](Configuring-NuGet-Behavior.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afd21-114">For more information about how NuGet behaves, see [Common NuGet configurations](Configuring-NuGet-Behavior.md).</span></span> 

> [!Note]
> <span data-ttu-id="afd21-115">NuGet은 모든 소스가 확인될 때까지 패키지 복원 실패를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-115">NuGet doesn't indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="afd21-116">이때 NuGet은 목록의 마지막 소스에 대한 실패만 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-116">At that time, NuGet reports a failure for only the last source in the list.</span></span> <span data-ttu-id="afd21-117">이러한 오류는 각 소스에 대한 오류가 개별적으로 표시되지 않았더라도 패키지가 다른 *어떤* 소스에도 존재하지 않음을 암시합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-117">The error implies that the package wasn't present on *any* of the other sources, even though errors aren't shown for each of those sources individually.</span></span>

## <a name="restore-packages"></a><span data-ttu-id="afd21-118">패키지 복원</span><span class="sxs-lookup"><span data-stu-id="afd21-118">Restore packages</span></span>

<span data-ttu-id="afd21-119">다음 방법 중 하나로 패키지 복원을 트리거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-119">You can trigger Package Restore in any of the following ways:</span></span>

- <span data-ttu-id="afd21-120">**Visual Studio**: Windows의 Visual Studio에서 다음 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-120">**Visual Studio**: In Visual Studio on Windows, use one of the following methods.</span></span>

    - <span data-ttu-id="afd21-121">패키지를 자동으로 복원.</span><span class="sxs-lookup"><span data-stu-id="afd21-121">Restore packages automatically.</span></span> <span data-ttu-id="afd21-122">패키지 복원은 [패키지 복원 사용 및 사용 안 함](#enable-and-disable-package-restore-visual-studio) 옵션에 따라 템플릿에서 프로젝트를 만들거나 프로젝트를 빌드할 때 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-122">Package Restore happens automatically when you create a project from a template or build a project, subject to the options in [Enable and disable package restore](#enable-and-disable-package-restore-visual-studio).</span></span> <span data-ttu-id="afd21-123">NuGet 4.0 이상에서는 SDK 스타일 프로젝트(일반적으로 .NET Core 또는 .NET Standard 프로젝트)가 변경되면 자동으로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-123">In NuGet 4.0+, restore also happens automatically when you make changes to a SDK-style project (typically a .NET Core or .NET Standard project).</span></span>

    - <span data-ttu-id="afd21-124">패키지를 수동으로 복원.</span><span class="sxs-lookup"><span data-stu-id="afd21-124">Restore packages manually.</span></span> <span data-ttu-id="afd21-125">수동으로 복원하려면 **솔루션 탐색기**에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 복원**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-125">To restore manually, right-click the solution in **Solution Explorer** and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="afd21-126">하나 이상의 개별 패키지가 아직 제대로 설치되지 않은 경우 **솔루션 탐색기**에 오류 아이콘이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-126">If one or more individual packages still aren't installed properly, **Solution Explorer** shows an error icon.</span></span> <span data-ttu-id="afd21-127">마우스 오른쪽 단추를 클릭하고 **NuGet 패키지 관리**를 선택하고 **패키지 관리자**를 사용하여 영향을 받은 패키지를 제거하고 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-127">Right-click and select **Manage NuGet Packages**, and use **Package Manager** to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="afd21-128">자세한 내용은 [패키지 다시 설치 및 업데이트](../consume-packages/reinstalling-and-updating-packages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afd21-128">For more information, see [Reinstall and update packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

    <span data-ttu-id="afd21-129">"이 프로젝트는 이 컴퓨터에 없는 NuGet 패키지를 참조합니다." 또는 "하나 이상의 NuGet 패키지를 복원해야 하지만 동의하지 않아 복원할 수 없습니다."라는 오류 메시지가 표시되면 [자동 복원을 사용하도록 설정](#enable-and-disable-package-restore-visual-studio)하세요.</span><span class="sxs-lookup"><span data-stu-id="afd21-129">If you see the error "This project references NuGet package(s) that are missing on this computer," or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," [enable automatic restore](#enable-and-disable-package-restore-visual-studio).</span></span> <span data-ttu-id="afd21-130">또한 [자동 패키지 복원으로 마이그레이션](#migrate-to-automatic-package-restore-visual-studio) 및 [패키지 복원 문제 해결](Package-restore-troubleshooting.md)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afd21-130">Also, see [Migrate to automatic package restore](#migrate-to-automatic-package-restore-visual-studio) and [Package Restore troubleshooting](Package-restore-troubleshooting.md).</span></span>

- <span data-ttu-id="afd21-131">**dotnet CLI**: 명령줄에서 프로젝트를 포함하는 폴더로 전환한 후 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 명령을 사용하여 프로젝트 파일에 나열된 패키지를 [PackageReference](../consume-packages/package-references-in-project-files.md)로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-131">**dotnet CLI**: In the command line, switch to the folder that contains your project, and then use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command to restore packages listed in the project file with [PackageReference](../consume-packages/package-references-in-project-files.md).</span></span> <span data-ttu-id="afd21-132">.NET Core 2.0 이상에서는 `dotnet build` 및 `dotnet run` 명령을 통해 복원이 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-132">With .NET Core 2.0 and later, restore happens automatically with the `dotnet build` and `dotnet run` commands.</span></span>  

- <span data-ttu-id="afd21-133">**nuget.exe CLI**: 명령줄에서 프로젝트를 포함하는 폴더로 전환한 후 [nuget restore](../reference/cli-reference/cli-ref-restore.md) 명령을 사용하여 프로젝트나 솔루션 파일 또는 `packages.config`에 나열된 패키지를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-133">**nuget.exe CLI**: In the command line, switch to the folder that contains your project, and then use the [nuget restore](../reference/cli-reference/cli-ref-restore.md) command to restore packages listed in a project or solution file, or in `packages.config`.</span></span> 

- <span data-ttu-id="afd21-134">**MSBuild**: [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) 명령을 사용하여 프로젝트 파일에 나열된 패키지를 PackageReference로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-134">**MSBuild**: Use the [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) command to restore packages listed in the project file with PackageReference.</span></span> <span data-ttu-id="afd21-135">이 명령은 Visual Studio 2017 이상 버전에 포함된 NuGet 4.x 이상 및 MSBuild 15.1 이상에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-135">This command is available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017 and higher versions.</span></span> <span data-ttu-id="afd21-136">`nuget restore` 및 `dotnet restore`는 모두 해당 프로젝트에 대해 이 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-136">Both `nuget restore` and `dotnet restore` use this command for applicable projects.</span></span>

- <span data-ttu-id="afd21-137">**Azure Pipelines**: Azure Pipelines에서 빌드 정의를 만들 때 빌드 작업 전에 NuGet [복원](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) 또는 .NET Core [복원](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) 작업을 정의에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-137">**Azure Pipelines**: When you create a build definition in Azure Pipelines, include the NuGet [restore](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) or .NET Core [restore](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) task in the definition before any build tasks.</span></span> <span data-ttu-id="afd21-138">몇 가지 빌드 템플릿에는 기본적으로 복원 작업이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-138">Some build templates include the restore task by default.</span></span>

- <span data-ttu-id="afd21-139">**Azure DevOps Server**: Azure DevOps Server 및 TFS 2013 이상에서는 TFS 2013 이상 팀 빌드 템플릿을 사용하는 경우 빌드 중에 패키지를 자동으로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-139">**Azure DevOps Server**: Azure DevOps Server and TFS 2013 and later automatically restore packages during build, if you're using a TFS 2013 or later Team Build template.</span></span> <span data-ttu-id="afd21-140">이전 TFS 버전의 경우 명령줄 복원 옵션을 실행하는 빌드 단계를 포함하거나 필요에 따라 빌드 템플릿을 최신 버전으로 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-140">For earlier TFS versions, you can include a build step to run a command-line restore option, or optionally migrate the build template to a later version.</span></span> <span data-ttu-id="afd21-141">자세한 내용은 [Team Foundation 빌드를 사용하여 패키지 복원 설정](../consume-packages/team-foundation-build.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afd21-141">For more information, see [Set up package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="enable-and-disable-package-restore-visual-studio"></a><span data-ttu-id="afd21-142">패키지 복원 사용 및 사용 안 함(Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="afd21-142">Enable and disable package restore (Visual Studio)</span></span>

<span data-ttu-id="afd21-143">Visual Studio에서 주로 **도구** > **옵션** > **NuGet 패키지 관리자**를 통해 패키지 복원을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-143">In Visual Studio, you control Package Restore primarily through **Tools** > **Options** > **NuGet Package Manager**:</span></span>

![NuGet 패키지 관리자 옵션을 통한 패키지 복원 제어](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="afd21-145">**NuGet이 누락된 패키지를 다운로드하도록 허용**은 `NuGet.Config` 파일(Windows의 경우 `%AppData%\NuGet\`, Mac/Linux의 경우 `~/.nuget/NuGet/`)의 [packageRestore 섹션](../reference/nuget-config-file.md#packagerestore-section)에서 `packageRestore/enabled` 설정을 변경하여 모든 형태의 패키지 복원을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-145">**Allow NuGet to download missing packages** controls all forms of package restore by changing the `packageRestore/enabled` setting in the [packageRestore section](../reference/nuget-config-file.md#packagerestore-section) of the `NuGet.Config` file, at `%AppData%\NuGet\` on Windows, or `~/.nuget/NuGet/` on Mac/Linux.</span></span> <span data-ttu-id="afd21-146">이 설정을 사용하면 Visual Studio의 솔루션 컨텍스트 메뉴에서 **NuGet 패키지 복원** 명령을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-146">This setting also enables the **Restore NuGet Packages** command on the solution's context menu in Visual Studio, .</span></span>

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
  > <span data-ttu-id="afd21-147">`packageRestore/enabled` 설정을 전역적으로 재정의하려면 Visual Studio를 시작하거나 빌드를 시작하기 전에 환경 변수 **EnableNuGetPackageRestore**를 True 또는 False 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-147">To globally override the `packageRestore/enabled` setting, set the environment variable **EnableNuGetPackageRestore** with a value of True or False before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="afd21-148">**Visual Studio에서 빌드 시 누락된 패키지를 자동으로 확인**은 `NuGet.Config` 파일의 [packageRestore 섹션](../reference/nuget-config-file.md#packagerestore-section)에서 `packageRestore/automatic` 설정을 변경하여 자동 복원을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-148">**Automatically check for missing packages during build in Visual Studio** controls automatic restore by changing the `packageRestore/automatic` setting in the [packageRestore section](../reference/nuget-config-file.md#packagerestore-section) of the `NuGet.Config` file.</span></span> <span data-ttu-id="afd21-149">이 옵션을 True로 설정하면 Visual Studio에서 빌드를 실행할 경우 누락된 모든 패키지가 자동으로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-149">When this option is set to True, running a build from Visual Studio automatically restores any missing packages.</span></span> <span data-ttu-id="afd21-150">이 설정은 MSBuild 명령줄에서 실행되는 빌드에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-150">This setting doesn't affect builds run from the MSBuild command line.</span></span>

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

<span data-ttu-id="afd21-151">컴퓨터의 모든 사용자에 대해 패키지 복원을 활성화하거나 비활성화하기 위해 개발자 또는 회사가 구성 설정을 글로벌 `nuget.config` 파일에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-151">To enable or disable Package Restore for all users on a computer, a developer or company can add the configuration settings to the global `nuget.config` file.</span></span> <span data-ttu-id="afd21-152">글로벌 `nuget.config`는 `%ProgramData%\NuGet\Config`의 Windows, 경우에 따라 특정 `\{IDE}\{Version}\{SKU}\` Visual Studio 폴더 또는 `~/.local/share`의 Mac/Linux에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-152">The global `nuget.config` is in Windows at `%ProgramData%\NuGet\Config`, sometimes under a specific `\{IDE}\{Version}\{SKU}\` Visual Studio folder, or in Mac/Linux at `~/.local/share`.</span></span> <span data-ttu-id="afd21-153">개별 사용자는 프로젝트 수준에서 필요에 따라 선택적으로 복원을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-153">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="afd21-154">NuGet에서 여러 구성 파일의 우선순위를 지정하는 방법에 대한 자세한 내용은 [일반적인 NuGet 구성](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afd21-154">For more details on how NuGet prioritizes multiple config files, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

> [!Important]
> <span data-ttu-id="afd21-155">`nuget.config`에서 `packageRestore` 설정을 바로 편집할 경우 Visual Studio를 다시 시작해야 **옵션** 대화 상자에 최신 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio, so that the **Options** dialog box shows the current values.</span></span>

## <a name="constrain-package-versions-with-restore"></a><span data-ttu-id="afd21-156">복원을 사용하여 패키지 버전 제한</span><span class="sxs-lookup"><span data-stu-id="afd21-156">Constrain package versions with restore</span></span>

<span data-ttu-id="afd21-157">어떤 방법으로든 NuGet에서 패키지를 복원하는 경우 `packages.config` 또는 프로젝트 파일에 지정된 제약 조건을 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-157">When NuGet restores packages through any method, it honors any constraints you specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="afd21-158">`packages.config`에서 종속성의 `allowedVersion` 속성에 버전 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-158">In `packages.config`, you can specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="afd21-159">자세한 내용은 [업그레이드 버전 제한](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afd21-159">See [Constrain upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) for more information.</span></span> <span data-ttu-id="afd21-160">예:</span><span class="sxs-lookup"><span data-stu-id="afd21-160">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="afd21-161">프로젝트 파일에서 PackageReference를 사용하여 종속성 범위를 직접 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-161">In a project file, you can use PackageReference to specify a dependency's range directly.</span></span> <span data-ttu-id="afd21-162">예:</span><span class="sxs-lookup"><span data-stu-id="afd21-162">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="afd21-163">모든 경우에 [패키지 버전 관리](../reference/package-versioning.md)에서 설명한 표기법을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="afd21-163">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="force-restore-from-package-sources"></a><span data-ttu-id="afd21-164">패키지 소스에서 강제로 복원</span><span class="sxs-lookup"><span data-stu-id="afd21-164">Force restore from package sources</span></span>

<span data-ttu-id="afd21-165">기본적으로 NuGet 복원 작업은 *global-packages* 및 *http-cache* 폴더의 패키지를 사용합니다. 이 내용은 [글로벌 패키지 및 캐시 폴더 관리](managing-the-global-packages-and-cache-folders.md)에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-165">By default, NuGet restore operations use packages from the *global-packages* and *http-cache* folders, which are described in [Manage the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="afd21-166">*global-packages* 폴더를 사용하지 않으려면 다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-166">To avoid using the *global-packages* folder, do one of the following:</span></span>

- <span data-ttu-id="afd21-167">`nuget locals global-packages -clear` 또는 `dotnet nuget locals global-packages --clear`를 사용하여 폴더를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-167">Clear the folder using `nuget locals global-packages -clear` or `dotnet nuget locals global-packages --clear`.</span></span>
- <span data-ttu-id="afd21-168">복원 작업을 수행하기 전에 다음 방법 중 하나를 사용하여 *global-packages* 폴더의 위치를 임시로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-168">Temporarily change the location of the *global-packages* folder before the restore operation, using one of the following methods:</span></span>
  - <span data-ttu-id="afd21-169">NUGET_PACKAGES 환경 변수를 다른 폴더로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-169">Set the NUGET_PACKAGES environment variable to a different folder.</span></span>
  - <span data-ttu-id="afd21-170">`globalPackagesFolder`(PackageReference를 사용할 경우) 또는 `repositoryPath`(`packages.config`를 사용할 경우)를 설정하는 `NuGet.Config` 파일을 다른 폴더에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-170">Create a `NuGet.Config` file that sets `globalPackagesFolder` (if using PackageReference) or `repositoryPath` (if using `packages.config`) to a different folder.</span></span> <span data-ttu-id="afd21-171">자세한 내용은 [구성 설정](../reference/nuget-config-file.md#config-section)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afd21-171">For more information, see [configuration settings](../reference/nuget-config-file.md#config-section).</span></span>
  - <span data-ttu-id="afd21-172">MSBuild에만 해당: `RestorePackagesPath` 속성을 사용하여 다른 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-172">MSBuild only: Specify a different folder with the `RestorePackagesPath` property.</span></span>

<span data-ttu-id="afd21-173">캐시를 HTTP 소스로 사용하지 않으려면 다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-173">To avoid using the cache for HTTP sources, do one of the following:</span></span>

- <span data-ttu-id="afd21-174">`nuget restore`에 `-NoCache` 옵션을 사용하거나 `dotnet restore`에 `--no-cache` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-174">Use the `-NoCache` option with `nuget restore`, or the `--no-cache` option with `dotnet restore`.</span></span> <span data-ttu-id="afd21-175">이러한 옵션은 Visual Studio 패키지 관리자 또는 콘솔을 통한 복원 작업에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-175">These options don't affect restore operations through the Visual Studio Package Manager or console.</span></span>
- <span data-ttu-id="afd21-176">`nuget locals http-cache -clear` 또는 `dotnet nuget locals http-cache --clear`를 사용하여 캐시를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-176">Clear the cache using `nuget locals http-cache -clear` or `dotnet nuget locals http-cache --clear`.</span></span>
- <span data-ttu-id="afd21-177">임시로 NUGET_HTTP_CACHE_PATH 환경 변수를 다른 폴더로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-177">Temporarily set the NUGET_HTTP_CACHE_PATH environment variable to a different folder.</span></span>

## <a name="migrate-to-automatic-package-restore-visual-studio"></a><span data-ttu-id="afd21-178">자동 패키지 복원으로 마이그레이션(Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="afd21-178">Migrate to automatic package restore (Visual Studio)</span></span>

<span data-ttu-id="afd21-179">NuGet 2.6 이하 버전의 경우 이전에는 MSBuild 통합 패키지 복원이 지원되었지만 더 이상은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-179">For NuGet 2.6 and earlier, an MSBuild-integrated package restore was previously supported but that is no longer true.</span></span> <span data-ttu-id="afd21-180">일반적으로 Visual Studio에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 복원 사용**을 선택하여 사용하도록 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-180">(It was typically enabled by right-clicking a solution in Visual Studio and selecting **Enable NuGet Package Restore**).</span></span> <span data-ttu-id="afd21-181">프로젝트에서 더 이상 지원되지 않는 MSBuild 통합 패키지 복원을 사용하는 경우 자동 패키지 복원으로 마이그레이션하세요.</span><span class="sxs-lookup"><span data-stu-id="afd21-181">If your project uses the deprecated MSBuild-integrated package restore, please migrate to automatic package restore.</span></span>

<span data-ttu-id="afd21-182">MSBuild 통합 패키지 복원을 사용하는 프로젝트에는 일반적으로 *.nuget* 폴더가 있으며 이 폴더에는 3개의 파일 *NuGet.config*, *nuget.exe* 및 *NuGet.targets*가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-182">Projects that use MSBuild-Integrated package restore typically contain a *.nuget* folder with three files: *NuGet.config*, *nuget.exe*, and *NuGet.targets*.</span></span> <span data-ttu-id="afd21-183">*Nuget.targets* 파일의 존재 여부에 따라 NuGet에서 MSBuild 통합 방법을 계속 사용하는지가 결정되므로 마이그레이션 동안 이 파일을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-183">The presence of a *NuGet.targets* file determines whether NuGet will continue to use the MSBuild-untegrated approach, so this file must be removed during the migration.</span></span>

<span data-ttu-id="afd21-184">자동 패키지 복원으로 마이그레이션하려면(Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="afd21-184">To migrate to automatic package restore:</span></span>

1. <span data-ttu-id="afd21-185">Visual Studio를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-185">Close Visual Studio.</span></span>
2. <span data-ttu-id="afd21-186">*.nuget/nuget.exe* 및 *.nuget/NuGet.targets*를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-186">Delete *.nuget/nuget.exe* and *.nuget/NuGet.targets*.</span></span>
3. <span data-ttu-id="afd21-187">각 프로젝트 파일에 대해 `<RestorePackages>` 요소를 제거하고 *NuGet.targets*에 대한 참조를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-187">For each project file, remove the `<RestorePackages>` element and remove any reference to *NuGet.targets*.</span></span>

<span data-ttu-id="afd21-188">자동 패키지 복원을 테스트하려면</span><span class="sxs-lookup"><span data-stu-id="afd21-188">To test the automatic package restore:</span></span>

1. <span data-ttu-id="afd21-189">솔루션에서 *packages* 폴더를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-189">Remove the *packages* folder from the solution.</span></span>
2. <span data-ttu-id="afd21-190">Visual Studio에서 해당 솔루션을 열고 빌드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-190">Open the solution in Visual Studio and start a build.</span></span>

   <span data-ttu-id="afd21-191">자동 패키지 복원은 각 종속성 패키지를 다운로드한 후, 소스 제어에 추가하지 않은 상태로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="afd21-191">Automatic package restore should download and install each dependency package, without adding them to source control.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="afd21-192">문제 해결</span><span class="sxs-lookup"><span data-stu-id="afd21-192">Troubleshooting</span></span>

<span data-ttu-id="afd21-193">[패키지 복원 문제 해결](package-restore-troubleshooting.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="afd21-193">See [Troubleshoot package restore](package-restore-troubleshooting.md).</span></span>
