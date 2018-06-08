---
title: NuGet 패키지 복원
description: 복원을 사용하지 않도록 설정하고 버전을 제한하는 방법을 포함하여 NuGet에서 프로젝트가 종속된 패키지를 복원하는 방법을 간략히 설명합니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 34da7f5800671f03df6728e0b948c560f73fd13c
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817049"
---
# <a name="package-restore"></a><span data-ttu-id="c8385-103">패키지 복원</span><span class="sxs-lookup"><span data-stu-id="c8385-103">Package Restore</span></span>

<span data-ttu-id="c8385-104">더 정돈된 개발 환경을 촉진하고 리포지토리 크기를 줄이기 위해 NuGet **패키지 복원**은 프로젝트 파일 또는 `packages.config`에 나열된 프로젝트의 종속성을 모두 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-104">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all a project's dependencies as listed in either the project file or `packages.config`.</span></span> <span data-ttu-id="c8385-105">Visual Studio는 프로젝트가 빌드될 때 패키지를 자동으로 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-105">Visual Studio can restore packages automatically when a project is built.</span></span> <span data-ttu-id="c8385-106">`dotnet build` 및 `dotnet run` 명령(.NET Core 2.0 이상)도 자동 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-106">The `dotnet build` and `dotnet run` commands (.NET Core 2.0+) also perform an automatic restore.</span></span> <span data-ttu-id="c8385-107">또한 Visual Studio, `nuget restore`, `dotnet restore` 및 Mono의 xbuild를 통해 언제든 패키지를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-107">You can also restore packages at any time through Visual Studio, `nuget restore`, `dotnet restore`, and xbuild on Mono.</span></span>

<span data-ttu-id="c8385-108">패키지 복원은 소스 제어에 해당 패키지를 저장하지 않고 프로젝트의 종속성을 모두 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-108">Package restore makes sure that all a project's dependencies are available without storing those packages in source control.</span></span> <span data-ttu-id="c8385-109">패키지 이진 파일을 제외하도록 리포지토리를 구성하는 방법은 [패키지 및 소스 제어](../consume-packages/packages-and-source-control.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8385-109">See [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries.</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="c8385-110">패키지 복원 개요</span><span class="sxs-lookup"><span data-stu-id="c8385-110">Package restore overview</span></span>

<span data-ttu-id="c8385-111">패키지를 복원하려면 먼저 필요에 따라 프로젝트의 직접 종속성을 설치한 다음, 전체 종속성 그래프에서 해당 패키지의 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-111">Restoring packages first installs the direct dependencies of a project as needed, then installs any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="c8385-112">패키지가 아직 설치되지 않은 경우 NuGet은 먼저 [캐시](../consume-packages/managing-the-global-packages-and-cache-folders.md)에서 검색을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-112">If a package is not already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> <span data-ttu-id="c8385-113">패키지가 캐시에 없으면 NuGet은 활성화된 모든 소스에서 패키지를 다운로드하려고 합니다([NuGet 동작 구성](Configuring-NuGet-Behavior.md) 참조). Visual Studio에서 소스는 **도구 > 옵션 > NuGet 패키지 관리자 > 패키지 소스** 목록에도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-113">If the package is not in the cache, NuGet then attempts to download the package from all enabled sources (see [Configuring NuGet behavior](Configuring-NuGet-Behavior.md); sources also appear in the  **Tools > Options > NuGet Package Manager > Package Sources** list in Visual Studio).</span></span> <span data-ttu-id="c8385-114">복원하는 동안 NuGet은 패키지 소스의 순서를 무시하고, 소스가 요청에 응답하는 순서대로 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-114">During restore, NuGet ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span>

> [!Note]
> <span data-ttu-id="c8385-115">NuGet은 모든 소스가 확인될 때까지 패키지 복원 실패를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-115">NuGet does not indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="c8385-116">이때 NuGet은 목록의 마지막 소스에 대한 실패만 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-116">At that time, NuGet reports a failure for only the last source in the list.</span></span> <span data-ttu-id="c8385-117">이러한 오류는 각 소스에 대한 오류가 개별적으로 표시되지 않았더라도 패키지가 다른 *어떤* 소스에도 존재하지 않음을 암시합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-117">The error implies that the package wasn't present on *any* of the other sources, even though errors are not shown for each of those sources individually.</span></span>

<span data-ttu-id="c8385-118">패키지 복원은 다음과 같은 방법으로 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-118">Package restore is triggered in the following ways:</span></span>

- <span data-ttu-id="c8385-119">**dotnet CLI**: 프로젝트 파일([PackageReference](../consume-packages/package-references-in-project-files.md) 참조)에 나열된 패키지를 복원하는 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-119">**dotnet CLI**: use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="c8385-120">.NET Core 2.0 이상에서는 `dotnet build` 및 `dotnet run`을 통해 복원이 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-120">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span>

- <span data-ttu-id="c8385-121">**패키지 관리자 UI(Windows에서 Visual Studio)**: 패키지는 템플릿에서 프로젝트를 만들 경우 및 프로젝트를 빌드할 경우( [패키지 복원 사용 및 사용 안 함](#enabling-and-disabling-package-restore)에 설명된 옵션에 따라) 패키지가 자동으로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-121">**Package Manager UI (Visual Studio on Windows)**: Packages are restored automatically when creating a project from a template and when building a project (subject to the option described in [Enabling and disabling package restore](#enabling-and-disabling-package-restore)).</span></span> <span data-ttu-id="c8385-122">NuGet 4.0 이상에서 .NET Core SDK 기반 프로젝트가 변경되면 자동으로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-122">In NuGet 4.0+, restore also happens automatically when changes are made to a .NET Core SDK-based project.</span></span>

    <span data-ttu-id="c8385-123">수동으로 복원하려면 솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 복원**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-123">To restore manually, right-click the solution in Solution Explorer and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="c8385-124">하나 이상의 개별 패키지가 제대로 설치되지 않은 경우(즉, 솔루션 탐색기에 오류 아이콘이 표시됨)에는 패키지 관리자 UI를 사용하여 영향을 받는 패키지를 제거하고 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-124">If one or more individual packages are still not installed properly (meaning that Solution Explorer shows an error icon), then use the Package Manager UI to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="c8385-125">[패키지 다시 설치 및 업데이트](../consume-packages/reinstalling-and-updating-packages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8385-125">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

    <span data-ttu-id="c8385-126">"이 프로젝트는 이 컴퓨터에 없는 NuGet 패키지를 참조합니다." 또는 "하나 이상의 NuGet 패키지를 복원해야 하지만 동의하지 않아 복원할 수 없습니다."라는 오류 메시지가 표시되면 [패키지 복원 사용 설정/해제](#enabling-and-disabling-package-restore)의 지침에 따라 자동 복원을 설정하세요.</span><span class="sxs-lookup"><span data-stu-id="c8385-126">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span> <span data-ttu-id="c8385-127">[패키지 복원 문제 해결](Package-restore-troubleshooting.md)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8385-127">Also see [Package restore troubleshooting](Package-restore-troubleshooting.md).</span></span>

- <span data-ttu-id="c8385-128">**NuGet CLI**: 프로젝트 파일 또는 `packages.config`에 나열된 패키지를 복원하는 [nuget restore](../tools/cli-ref-restore.md) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-128">**NuGet CLI**: use the [nuget restore](../tools/cli-ref-restore.md) command, which restores packages listed in the project file or in `packages.config`.</span></span> <span data-ttu-id="c8385-129">솔루션 파일을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-129">You can also specify a solution file.</span></span>

- <span data-ttu-id="c8385-130">**MSBuild**: 프로젝트 파일(PackageReference만)에 나열된 패키지를 복원하는 [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-130">**MSBuild**: use the [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) command, which restores packages packages listed in the project file (PackageReference only).</span></span> <span data-ttu-id="c8385-131">Visual Studio 2017에 포함된 NuGet 4.x 이상 및 MSBuild 15.1 이상에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-131">Available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017.</span></span> <span data-ttu-id="c8385-132">`nuget restore` 및 `dotnet restore`는 모두 해당 프로젝트에 대해 이 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-132">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span>

- <span data-ttu-id="c8385-133">**Visual Studio Team Services**: Team Services에 대한 빌드 정의를 만들 때 빌드 작업 전에 [NuGet 복원](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) 또는 [.NET Core 복원](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) 작업을 정의에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-133">**Visual Studio Team Services**: When creating a build definition on Team Services, include the [NuGet restore](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) or [.NET Core Restore](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) task in the definition before any build task.</span></span> <span data-ttu-id="c8385-134">이 작업은 여러 빌드 템플릿에 기본적으로 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-134">This task is included by default in a number of build templates.</span></span>

- <span data-ttu-id="c8385-135">**Team Foundation Server**: TFS 2013 이상은 TFS 2013용 팀 빌드 템플릿을 사용할 경우 빌드 중에 패키지를 자동으로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-135">**Team Foundation Server**: TFS 2013 and later automatically restores packages during build, provided that you're using a Team Build Template for TFS 2013 or later.</span></span> <span data-ttu-id="c8385-136">이전 버전 TFS의 경우 위의 명령줄 복원 옵션 중 하나를 호출하는 빌드 단계를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-136">For earlier version of TFS, you can include a build step to invoke one of the command-line restore options above.</span></span> <span data-ttu-id="c8385-137">선택적으로 빌드 템플릿을 TFS 2013으로 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-137">You can optionally migrate the build template to TFS 2013.</span></span> <span data-ttu-id="c8385-138">자세한 내용은 [Team Foundation 빌드를 사용하여 패키지 복원 연습](../consume-packages/team-foundation-build.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8385-138">For more information, see the [Walkthrough of package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="c8385-139">패키지 복원 사용 설정/해제</span><span class="sxs-lookup"><span data-stu-id="c8385-139">Enabling and disabling package restore</span></span>

<span data-ttu-id="c8385-140">패키지 복원은 주로 Visual Studio에서 **도구 > 옵션 > NuGet 패키지 관리자**를 통해 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-140">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![NuGet 패키지 관리자 옵션을 통한 패키지 복원 동작 제어](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="c8385-142">**NuGet이 누락된 패키지를 다운로드하도록 허용**: `NuGet.Config` 파일(Windows의 경우 `%AppData%\NuGet\NuGet.Config`, Mac/Linux의 경우 `~/.nuget/NuGet/NuGet.Config`)의 `packageRestore/enabled` 설정을 아래와 같이 변경하여 모든 형태의 패키지 복원을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-142">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `NuGet.Config` file as shown below (`%AppData%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="c8385-143">Visual Studio에서 이 설정을 사용하면 솔루션의 상황에 맞는 메뉴에서 **NuGet 패키지 복원** 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-143">In Visual Studio, this setting allows the **Restore NuGet Packages** command on the solution's context menu to work.</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  <span data-ttu-id="c8385-144">Visual Studio를 시작하거나 빌드를 시작하기 전에 **EnableNuGetPackageRestore**이라는 환경 변수를 TRUE 또는 FALSE 값으로 설정하여 `packageRestore/enabled` 설정을 전역으로 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-144">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="c8385-145">**Visual Studio에서 빌드 시 누락된 패키지를 자동으로 확인**: `NuGet.Config` 파일(Windows의 경우 `%AppData%\NuGet\NuGet.Config`, Mac/Linux의 경우 `~/.nuget/NuGet/NuGet.Config`)의 `packageRestore/automatic` 설정을 아래와 같이 변경하여 자동 복원을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-145">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore by changing the `packageRestore/automatic` setting in the `NuGet.Config` file as shown below (`%AppData%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="c8385-146">이 옵션을 설정하면 Visual Studio에서 빌드를 실행할 경우 누락된 모든 패키지가 자동으로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-146">When this option is set, running a build from Visual Studio automatically restores any missing packages.</span></span> <span data-ttu-id="c8385-147">이 옵션은 MSBuild를 사용하여 명령줄에서 실행되는 빌드에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-147">The option does not affect builds run from the command line using MSBuild.</span></span>

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

<span data-ttu-id="c8385-148">해당 참조는 [NuGet.Config 파일 - packageRestore 섹션](../reference/nuget-config-file.md#packagerestore-section)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8385-148">For reference, see the [NuGet config file - packageRestore section](../reference/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="c8385-149">경우에 따라 개발자 또는 회사에서 컴퓨터의 모든 사용자에 대해 패키지 복원을 사용하거나 사용하지 않도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-149">In some cases, a developer or company might want to enable or disable package restore for all users on a computer.</span></span> <span data-ttu-id="c8385-150">이렇게 하려면 위의 동일한 설정을 `%ProgramData%\NuGet\Config`(Windows, Visual Studio용 특정 `\{IDE}\{Version}\{SKU}\` 폴더에 있을 수 있음) 또는 `~/.local/share`(Mac/Linux)에 있는 전역 NuGet 구성 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-150">To do this, add the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config` (Windows, potentially under a specific `\{IDE}\{Version}\{SKU}\` folder for Visual Studio) or `~/.local/share` (Mac/Linux).</span></span> <span data-ttu-id="c8385-151">개별 사용자는 프로젝트 수준에서 필요에 따라 선택적으로 복원을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-151">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="c8385-152">NuGet에서 여러 구성 파일의 우선 순위를 지정하는 방법에 대한 자세한 내용은 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8385-152">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

> [!Important]
> <span data-ttu-id="c8385-153">`nuget.config`에서 `packageRestore` 설정을 바로 편집할 경우 Visual Studio를 다시 시작해야 옵션 대화 상자에 최신 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-153">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="c8385-154">복원을 사용하여 패키지 버전 제한</span><span class="sxs-lookup"><span data-stu-id="c8385-154">Constraining package versions with restore</span></span>

<span data-ttu-id="c8385-155">메서드를 통해 패키지를 복원하는 경우 NuGet은 `packages.config` 또는 프로젝트 파일에 지정된 제약 조건을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-155">When restoring packages through any method, NuGet honors any constraints specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="c8385-156">`packages.config`: 종속성의 `allowedVersion` 속성에서 버전 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-156">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="c8385-157">[패키지 다시 설치 및 업데이트](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8385-157">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="c8385-158">예:</span><span class="sxs-lookup"><span data-stu-id="c8385-158">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="c8385-159">프로젝트 파일(PackageReference): 종속성의 버전 번호를 사용하여 버전 범위를 직접 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-159">Project file (PackageReference): Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="c8385-160">예:</span><span class="sxs-lookup"><span data-stu-id="c8385-160">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="c8385-161">모든 경우에 [패키지 버전 관리](../reference/package-versioning.md)에서 설명한 표기법을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="c8385-161">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="forcing-restore-from-package-sources"></a><span data-ttu-id="c8385-162">패키지 소스에서 강제로 복원</span><span class="sxs-lookup"><span data-stu-id="c8385-162">Forcing restore from package sources</span></span>

<span data-ttu-id="c8385-163">기본적으로 NuGet 복원 작업은 *global-packages* 및 *http-cache* 폴더의 패키지를 사용합니다. 이 내용은 [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md)(전역 패키지 및 캐시 폴더 관리)에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-163">By default, NuGet restore operations use packages from the *global-packages* and *http-cache* folders, which are described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="c8385-164">*global-packages* 폴더를 사용하지 않으려면 다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-164">To avoid using the *global-packages* folder, do one of the following:</span></span>

- <span data-ttu-id="c8385-165">`nuget locals global-packages -clear` 또는 `dotnet nuget locals global-packages --clear`를 사용하여 폴더를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-165">Clear the folder using `nuget locals global-packages -clear` or `dotnet nuget locals global-packages --clear`</span></span>
- <span data-ttu-id="c8385-166">복원 작업을 수행하기 전에 다음 방법 중 하나를 사용하여 *global-packages* 폴더의 위치를 임시로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-166">Temporarily change the location of the *global-packages* folder before the restore operation using one of the following methods:</span></span>
  - <span data-ttu-id="c8385-167">NUGET_PACKAGES 환경 변수를 다른 폴더로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-167">Set the NUGET_PACKAGES environment variable to a different folder.</span></span>
  - <span data-ttu-id="c8385-168">`globalPackagesFolder`(PackageReference를 사용할 경우) 또는 `repositoryPath`(`packages.config`를 사용할 경우)를 설정하는 `NuGet.Config` 파일을 다른 폴더에 만듭니다([구성 설정](../reference/nuget-config-file.md#config-section) 참조).</span><span class="sxs-lookup"><span data-stu-id="c8385-168">Create a `NuGet.Config` file that sets `globalPackagesFolder` (if using PackageReference) or `repositoryPath` (if using `packages.config`) to a different folder (see [configuration settings](../reference/nuget-config-file.md#config-section)</span></span>
  - <span data-ttu-id="c8385-169">MSBuild에만 해당: `RestorePackagesPath` 속성에 다른 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-169">MSBuild only: specify a different folder with the `RestorePackagesPath` property.</span></span>

<span data-ttu-id="c8385-170">캐시를 HTTP 소스로 사용하지 않으려면 다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-170">To avoid using the cache for HTTP sources, do one of the following:</span></span>

- <span data-ttu-id="c8385-171">`nuget restore`에 `-NoCache` 옵션 또는 `dotnet restore`에 `--no-cache` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-171">Use the `-NoCache` option with `nuget restore` or the `--no-cache` option with `dotnet restore`.</span></span> <span data-ttu-id="c8385-172">이러한 옵션은 Visual Studio 패키지 관리자 UI나 콘솔을 통한 복원 작업에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-172">These options do not affect restore operations through the Visual Studio Package Manager UI or Console.</span></span>
- <span data-ttu-id="c8385-173">`nuget locals http-cache -clear` 또는 `dotnet nuget locals http-cache --clear`를 사용하여 캐시를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-173">Clear the cache using `nuget locals http-cache -clear` or `dotnet nuget locals http-cache --clear`.</span></span>
- <span data-ttu-id="c8385-174">임시로 NUGET_HTTP_CACHE_PATH 환경 변수를 다른 폴더로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c8385-174">Temporarily set of the NUGET_HTTP_CACHE_PATH environment variable to a different folder.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c8385-175">문제 해결</span><span class="sxs-lookup"><span data-stu-id="c8385-175">Troubleshooting</span></span>

<span data-ttu-id="c8385-176">[패키지 복원 문제 해결](package-restore-troubleshooting.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c8385-176">See [Troubleshooting package restore](package-restore-troubleshooting.md).</span></span>