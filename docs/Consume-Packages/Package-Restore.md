---
title: "NuGet 패키지 복원 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "복원을 사용하지 않도록 설정하고 버전을 제한하는 방법을 포함하여 NuGet에서 프로젝트가 종속된 패키지를 복원하는 방법을 간략히 설명합니다."
keywords: "NuGet 패키지 복원, NuGet 패키지 설치, 패키지 설치, 패키지 복원, 종속성 버전, 자동 복원 사용 해제, 패키지 버전 제한"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 761ef86a70e0a681449dc9fe86d6a52ac2b19bb1
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="package-restore"></a><span data-ttu-id="0292e-104">패키지 복원</span><span class="sxs-lookup"><span data-stu-id="0292e-104">Package Restore</span></span>

<span data-ttu-id="0292e-105">더 깨끗한 개발 환경을 촉진하고 리포지토리 크기를 줄이기 위해 NuGet **패키지 복원**은 프로젝트가 빌드되기 전에 참조된 모든 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="0292e-106">&mdash;Mono의 Visual Studio, .NET Core 2.0 이상 및 xbuild에서 사용 가능한&mdash; 널리 사용되는 이 기능은 패키지를 소스 제어에 저장하지 않고도 프로젝트에서 모든 종속성을 사용할 수 있게 합니다(패키지 이진 파일을 제외하도록 리포지토리를 구성하는 방법은 [패키지 및 소스 제어](../consume-packages/packages-and-source-control.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="0292e-106">This widely-used feature&mdash;available in Visual Studio, .NET Core 2.0+, and xbuild on Mono&mdash;ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span> <span data-ttu-id="0292e-107">언제든지 수동으로 패키지를 복원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-107">You can also manually restore packages at any time.</span></span>

<span data-ttu-id="0292e-108">빌드 서버의 패키지 복원에 대한 자세한 내용은 [TFBuild를 사용하여 패키지 복원](../consume-packages/team-foundation-build.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0292e-108">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="0292e-109">패키지 복원 개요</span><span class="sxs-lookup"><span data-stu-id="0292e-109">Package restore overview</span></span>

<span data-ttu-id="0292e-110">패키지를 복원하려면 먼저 필요에 따라 프로젝트의 직접 종속성을 설치한 다음 전체 종속성 그래프에서 해당 패키지의 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-110">Restoring packages first installs the direct dependencies of a project as needed, then installing any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="0292e-111">패키지가 아직 설치되지 않은 경우 NuGet은 먼저 [캐시](../consume-packages/managing-the-nuget-cache.md)에서 검색을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-111">If a package is not already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="0292e-112">패키지가 캐시에 없으면 NuGet은 활성화된 모든 소스에서 해당 패키지를 다운로드 (및 캐시) 하려고 합니다([NuGet 동작 구성](Configuring-NuGet-Behavior.md) 참조). Visual Studio에서 소스는 **도구 > 옵션 > NuGet 패키지 관리자 > 패키지 소스** 목록에도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-112">If the package is not in the cache, NuGet then attempts to download (and cache) the package from all enabled sources (see [Configuring NuGet behavior](Configuring-NuGet-Behavior.md)); sources also appear in the  **Tools > Options > NuGet Package Manager > Package Sources** list in Visual Studio).</span></span> <span data-ttu-id="0292e-113">NuGet은 패키지 소스의 순서를 무시하고, 소스가 요청에 응답하는 순서대로 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-113">NuGet ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span>

> [!Note]
> <span data-ttu-id="0292e-114">NuGet은 모든 소스가 확인될 때까지 패키지 복원 실패를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-114">NuGet does not indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="0292e-115">이때 NuGet은 목록의 마지막 소스에 대한 실패만 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-115">At that time, NuGet reports the failure for only the last source in the list.</span></span> <span data-ttu-id="0292e-116">이러한 오류는 각 소스에 대한 오류가 개별적으로 표시되지 않았더라도 패키지가 다른 *어떤* 소스에도 존재하지 않음을 암시합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-116">The error implies that the package wasn't present on *any* of the other sources, even though errors are not shown for each of those sources individually.</span></span>

<span data-ttu-id="0292e-117">패키지 복원은 다음과 같은 방법으로 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-117">Package restore is triggered in the following ways:</span></span>

- <span data-ttu-id="0292e-118">**dotnet CLI**: 프로젝트 파일([PackageReference](../consume-packages/package-references-in-project-files.md) 참조)에 나열된 패키지를 복원하는 [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-118">**dotnet CLI**: use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="0292e-119">.NET Core 2.0 이상에서는 `dotnet build` 및 `dotnet run`을 통해 복원이 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-119">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span>

- <span data-ttu-id="0292e-120">**패키지 관리자 UI(Windows에서 Visual Studio)**: 패키지는 템플릿에서 프로젝트를 만들 경우 및 프로젝트를 빌드할 경우( [패키지 복원 사용 및 사용 안 함](#enabling-and-disabling-package-restore)에 설명된 옵션에 따라) 패키지가 자동으로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-120">**Package Manager UI (Visual Studio on Windows)**: Packages are restored automatically when creating a project from a template and when building a project (subject to the option described in [Enabling and disabling package restore](#enabling-and-disabling-package-restore)).</span></span> <span data-ttu-id="0292e-121">NuGet 4.0 이상에서 .NET Core SDK 기반 프로젝트가 변경되면 자동으로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-121">In NuGet 4.0+, restore also happens automatically when changes are made to a .NET Core SDK-based project.</span></span>

    <span data-ttu-id="0292e-122">수동으로 복원하려면 솔루션 탐색기에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 복원**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-122">To restore manually, right-click the solution in Solution Explorer and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="0292e-123">하나 이상의 개별 패키지가 제대로 설치되지 않은 경우(즉, 솔루션 탐색기에 오류 아이콘이 표시됨)에는 패키지 관리자 UI를 사용하여 영향을 받는 패키지를 제거하고 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-123">If one or more individual packages are still not installed properly (meaning that Solution Explorer shows an error icon), then use the Package Manager UI to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="0292e-124">[패키지 다시 설치 및 업데이트](../consume-packages/reinstalling-and-updating-packages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0292e-124">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

    <span data-ttu-id="0292e-125">"이 프로젝트는 이 컴퓨터에 없는 NuGet 패키지를 참조합니다." 또는 "하나 이상의 NuGet 패키지를 복원해야 하지만 동의하지 않아 복원할 수 없습니다."라는 오류 메시지가 표시되면 [패키지 복원 사용 설정/해제](#enabling-and-disabling-package-restore)의 지침에 따라 자동 복원을 설정하세요.</span><span class="sxs-lookup"><span data-stu-id="0292e-125">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

- <span data-ttu-id="0292e-126">**NuGet CLI**: 프로젝트 파일([PackageReference](../consume-packages/package-references-in-project-files.md) 참조) 또는 [packages.config](../reference/packages-config.md) 파일에 나열된 패키지를 복원하는 [nuget restore](../tools/cli-ref-restore.md) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-126">**NuGet CLI**: use the [nuget restore](../tools/cli-ref-restore.md) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)) or in a [packages.config](../reference/packages-config.md) file.</span></span> <span data-ttu-id="0292e-127">솔루션 파일을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-127">You can also specify a solution file.</span></span>

- <span data-ttu-id="0292e-128">**MSBuild**: 프로젝트 파일([PackageReference](../consume-packages/package-references-in-project-files.md) 참조)에 나열된 패키지를 복원하는 [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-128">**MSBuild**: use the [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) command, which restores packages packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="0292e-129">Visual Studio 2017에 포함된 NuGet 4.x 이상 및 MSBuild 15.1 이상에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-129">Available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017.</span></span> <span data-ttu-id="0292e-130">`nuget restore` 및 `dotnet restore`는 모두 해당 프로젝트에 대해 이 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-130">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span>

- <span data-ttu-id="0292e-131">**Visual Studio Team Services**: Team Services에 대한 빌드 정의를 만들 때 빌드 작업 전에 [NuGet 복원](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) 또는 [.NET Core 복원](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) 작업을 정의에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-131">**Visual Studio Team Services**: When creating a build definition on Team Services, include the [NuGet restore](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) or [.NET Core Restore](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) task in the definition before any build task.</span></span> <span data-ttu-id="0292e-132">이 작업은 여러 빌드 템플릿에 기본적으로 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-132">This task is included by default in a number of build templates.</span></span>

- <span data-ttu-id="0292e-133">**Team Foundation Server**: TFS 2013 이상은 TFS 2013용 팀 빌드 템플릿을 사용할 경우 빌드 중에 패키지를 자동으로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-133">**Team Foundation Server**: TFS 2013 and later automatically restores packages during build, provided that you're using a Team Build Template for TFS 2013 or later.</span></span> <span data-ttu-id="0292e-134">이전 버전 TFS의 경우 위의 명령줄 복원 옵션 중 하나를 호출하는 빌드 단계를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-134">For earlier version of TFS, you can include a build step to invoke one of the command-line restore options above.</span></span> <span data-ttu-id="0292e-135">선택적으로 빌드 템플릿을 TFS 2013으로 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-135">You can optionally migrate the build template to TFS 2013.</span></span> <span data-ttu-id="0292e-136">자세한 내용은 [Team Foundation 빌드를 사용하여 패키지 복원 연습](../consume-packages/team-foundation-build.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0292e-136">For more information, see the [Walkthrough of package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="0292e-137">패키지 복원 사용 설정/해제</span><span class="sxs-lookup"><span data-stu-id="0292e-137">Enabling and disabling package restore</span></span>

<span data-ttu-id="0292e-138">패키지 복원은 주로 Visual Studio에서 **도구 > 옵션 > NuGet 패키지 관리자**를 통해 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-138">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![NuGet 패키지 관리자 옵션을 통한 패키지 복원 동작 제어](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="0292e-140">**NuGet이 누락된 패키지를 다운로드하도록 허용**: `NuGet.Config` 파일(Windows의 경우 `%AppData%\NuGet\NuGet.Config`, Mac/Linux의 경우 `~/.nuget/NuGet/NuGet.Config`)의 `packageRestore/enabled` 설정을 아래와 같이 변경하여 모든 형태의 패키지 복원을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-140">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `NuGet.Config` file as shown below (`%AppData%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="0292e-141">Visual Studio에서 이 설정을 사용하면 솔루션의 상황에 맞는 메뉴에서 **NuGet 패키지 복원** 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-141">In Visual Studio, this setting allows the **Restore NuGet Packages** command on the solution's context menu to work.</span></span>

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
    >  <span data-ttu-id="0292e-142">Visual Studio를 시작하거나 빌드를 시작하기 전에 **EnableNuGetPackageRestore**이라는 환경 변수를 TRUE 또는 FALSE 값으로 설정하여 `packageRestore/enabled` 설정을 전역으로 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-142">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="0292e-143">**Visual Studio에서 빌드 시 누락된 패키지를 자동으로 확인**: `NuGet.Config` 파일(Windows의 경우 `%AppData%\NuGet\NuGet.Config`, Mac/Linux의 경우 `~/.nuget/NuGet/NuGet.Config`)의 `packageRestore/automatic` 설정을 아래와 같이 변경하여 자동 복원을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-143">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore by changing the `packageRestore/automatic` setting in the `NuGet.Config` file as shown below (`%AppData%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="0292e-144">이 옵션을 설정하면 Visual Studio에서 빌드를 실행할 경우 누락된 모든 패키지가 자동으로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-144">When this option is set, running a build from Visual Studio automatically restores any missing packages.</span></span> <span data-ttu-id="0292e-145">이 옵션은 MSBuild를 사용하여 명령줄에서 실행되는 빌드에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-145">The option does not affect builds run from the command line using MSBuild.</span></span>

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

<span data-ttu-id="0292e-146">해당 참조는 [NuGet.Config 파일 - packageRestore 섹션](../reference/nuget-config-file.md#packagerestore-section)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0292e-146">For reference, see the [NuGet config file - packageRestore section](../reference/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="0292e-147">경우에 따라 개발자 또는 회사에서 컴퓨터의 모든 사용자에 대해 패키지 복원을 사용하거나 사용하지 않도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-147">In some cases, a developer or company might want to enable or disable package restore for all users on a computer.</span></span> <span data-ttu-id="0292e-148">이렇게 하려면 위의 동일한 설정을 `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`에 있는 전역 NuGet 구성 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-148">This is done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="0292e-149">개별 사용자는 프로젝트 수준에서 필요에 따라 선택적으로 복원을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-149">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="0292e-150">NuGet에서 여러 구성 파일의 우선 순위를 지정하는 방법에 대한 자세한 내용은 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0292e-150">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="0292e-151">복원을 사용하여 패키지 버전 제한</span><span class="sxs-lookup"><span data-stu-id="0292e-151">Constraining package versions with restore</span></span>

<span data-ttu-id="0292e-152">메서드를 통해 패키지를 복원하는 경우 NuGet은 `packages.config` 또는 프로젝트 파일에 지정된 제약 조건을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-152">When restoring packages through any method, NuGet honors any constraints specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="0292e-153">`packages.config`: 종속성의 `allowedVersion` 속성에서 버전 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-153">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="0292e-154">[패키지 다시 설치 및 업데이트](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0292e-154">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="0292e-155">예:</span><span class="sxs-lookup"><span data-stu-id="0292e-155">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="0292e-156">PackageReference: 종속성의 버전 번호를 사용하여 버전 범위를 직접 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0292e-156">PackageReference: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="0292e-157">예:</span><span class="sxs-lookup"><span data-stu-id="0292e-157">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="0292e-158">모든 경우에 [패키지 버전 관리](../reference/package-versioning.md)에서 설명한 표기법을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="0292e-158">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0292e-159">문제 해결</span><span class="sxs-lookup"><span data-stu-id="0292e-159">Troubleshooting</span></span>

<span data-ttu-id="0292e-160">[패키지 복원 문제 해결](package-restore-troubleshooting.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0292e-160">See [Troubleshooting package restore](package-restore-troubleshooting.md).</span></span>