---
title: NuGet 패키지 복원
description: 복원을 사용하지 않도록 설정하고 버전을 제한하는 방법을 포함하여 NuGet에서 프로젝트가 종속된 패키지를 복원하는 방법을 간략히 설명합니다.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: c1f1957c58839ac763238938b476eb0882c56a59
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428440"
---
# <a name="restore-packages-using-package-restore"></a><span data-ttu-id="108d7-103">패키지 복원을 사용하여 패키지 복원</span><span class="sxs-lookup"><span data-stu-id="108d7-103">Restore packages using Package Restore</span></span>

<span data-ttu-id="108d7-104">더 정돈된 개발 환경을 촉진하고 리포지토리 크기를 줄이기 위해 NuGet **패키지 복원**은 프로젝트 파일 또는 `packages.config`에 나열된 프로젝트의 종속성을 모두 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-104">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all of a project's dependencies listed in either the project file or `packages.config`.</span></span> <span data-ttu-id="108d7-105">.NET Core 2.0+ `dotnet build` 및 `dotnet run` 명령은 자동 패키지 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-105">The .NET Core 2.0+ `dotnet build` and `dotnet run` commands do an automatic package restore.</span></span> <span data-ttu-id="108d7-106">Visual Studio는 프로젝트를 빌드할 때 패키지를 자동으로 복원할 수 있으며 Visual Studio, `nuget restore`, `dotnet restore` 및 Mono의 xbuild를 통해 언제든지 패키지를 복원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-106">Visual Studio can restore packages automatically when it builds a project, and you can restore packages at any time through Visual Studio, `nuget restore`, `dotnet restore`, and xbuild on Mono.</span></span>

<span data-ttu-id="108d7-107">패키지 복원은 모든 프로젝트의 종속성을 소스 제어에 저장하지 않고 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-107">Package Restore makes sure that all a project's dependencies are available, without having to store them in source control.</span></span> <span data-ttu-id="108d7-108">패키지 이진 파일을 제외하도록 소스 제어 리포지토리를 구성하려면 [패키지 및 소스 제어](../consume-packages/packages-and-source-control.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="108d7-108">To configure your source control repository to exclude the package binaries, see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> 

## <a name="package-restore-overview"></a><span data-ttu-id="108d7-109">패키지 복원 개요</span><span class="sxs-lookup"><span data-stu-id="108d7-109">Package Restore overview</span></span>

<span data-ttu-id="108d7-110">패키지 복원은 먼저 필요에 따라 프로젝트의 직접 종속성을 설치한 다음, 전체 종속성 그래프에서 해당 패키지의 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-110">Package Restore first installs the direct dependencies of a project as needed, then installs any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="108d7-111">패키지가 아직 설치되지 않은 경우 NuGet은 먼저 [캐시](../consume-packages/managing-the-global-packages-and-cache-folders.md)에서 검색을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-111">If a package isn't already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> <span data-ttu-id="108d7-112">패키지가 캐시에 없는 경우 NuGet은 Visual Studio에서 **도구** > **옵션** > **NuGet 패키지 관리자** > **패키지 원본**의 목록에 있는 사용 가능한 모든 소스에서 패키지를 다운로드하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-112">If the package isn't in the cache, NuGet tries to download the package from all enabled sources in the list at **Tools** > **Options** > **NuGet Package Manager** > **Package Sources** in Visual Studio.</span></span> <span data-ttu-id="108d7-113">복원하는 동안 NuGet은 패키지 소스의 순서를 무시하고, 소스가 요청에 응답하는 순서대로 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-113">During restore, NuGet ignores the order of package sources, and uses the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="108d7-114">NuGet 동작 방식에 대한 자세한 내용은 [일반적인 NuGet 구성](Configuring-NuGet-Behavior.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="108d7-114">For more information about how NuGet behaves, see [Common NuGet configurations](Configuring-NuGet-Behavior.md).</span></span> 

> [!Note]
> <span data-ttu-id="108d7-115">NuGet은 모든 소스가 확인될 때까지 패키지 복원 실패를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-115">NuGet doesn't indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="108d7-116">이때 NuGet은 목록의 마지막 소스에 대한 실패만 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-116">At that time, NuGet reports a failure for only the last source in the list.</span></span> <span data-ttu-id="108d7-117">이러한 오류는 각 소스에 대한 오류가 개별적으로 표시되지 않았더라도 패키지가 다른 *어떤* 소스에도 존재하지 않음을 암시합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-117">The error implies that the package wasn't present on *any* of the other sources, even though errors aren't shown for each of those sources individually.</span></span>

## <a name="restore-packages"></a><span data-ttu-id="108d7-118">패키지 복원</span><span class="sxs-lookup"><span data-stu-id="108d7-118">Restore packages</span></span>

<span data-ttu-id="108d7-119">패키지 복원은 프로젝트 파일( *.csproj*) 또는 *packages.config* 파일에서 패키지 참조와 일치하는 올바른 상태에 대한 모든 패키지 종속성을 설치하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-119">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="108d7-120">(Visual Studio에서 참조는 솔루션 탐색기의 **종속성 \ NuGet** 또는 **참조** 노드 아래에 표시됩니다.)</span><span class="sxs-lookup"><span data-stu-id="108d7-120">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.)</span></span>

1. <span data-ttu-id="108d7-121">프로젝트 파일의 패키지 참조가 올바른 경우 기본 설정 도구를 사용하여 패키지를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-121">If the package references in your project file are correct, use your preferred tool to restore packages.</span></span>

   - <span data-ttu-id="108d7-122">[Visual Studio](#restore-using-visual-studio)([자동 복원](#restore-packages-automatically-using-visual-studio) 또는 [수동 복원](#restore-packages-manually-using-visual-studio))</span><span class="sxs-lookup"><span data-stu-id="108d7-122">[Visual Studio](#restore-using-visual-studio) ([automatic restore](#restore-packages-automatically-using-visual-studio) or [manual restore](#restore-packages-manually-using-visual-studio))</span></span>
   - [<span data-ttu-id="108d7-123">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="108d7-123">dotnet CLI</span></span>](#restore-using-the-dotnet-cli)
   - [<span data-ttu-id="108d7-124">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="108d7-124">nuget.exe CLI</span></span>](#restore-using-the-nugetexe-cli)
   - [<span data-ttu-id="108d7-125">MSBuild</span><span class="sxs-lookup"><span data-stu-id="108d7-125">MSBuild</span></span>](#restore-using-msbuild)
   - [<span data-ttu-id="108d7-126">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="108d7-126">Azure Pipelines</span></span>](#restore-using-azure-pipelines)
   - [<span data-ttu-id="108d7-127">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="108d7-127">Azure DevOps Server</span></span>](#restore-using-azure-devops-server)

   <span data-ttu-id="108d7-128">프로젝트 파일( *.csproj*) 또는 *packages.config* 파일의 패키지 참조가 잘못된 경우(패키지 복원 이후 원하는 상태와 일치하지 않는 경우) 패키지를 설치하거나 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-128">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead.</span></span>

   <span data-ttu-id="108d7-129">PackageReference를 사용하는 프로젝트의 경우 성공적으로 복원된 후 패키지는 *global-packages* 폴더에 있어야 하며 `obj/project.assets.json` 파일이 다시 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-129">For projects using PackageReference, after a successful restore, the package should be present in the *global-packages* folder and the `obj/project.assets.json` file is recreated.</span></span> <span data-ttu-id="108d7-130">`packages.config`를 사용하는 프로젝트의 경우 패키지는 프로젝트의 `packages` 폴더에 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-130">For projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="108d7-131">이제 프로젝트가 성공적으로 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-131">The project should now build successfully.</span></span> 

2. <span data-ttu-id="108d7-132">패키지 복원을 실행한 후에도 누락된 패키지 또는 패키지 관련 오류(예: Visual Studio의 솔루션 탐색기에 있는 오류 아이콘)가 계속 발생하는 경우 [패키지 복원 오류 문제 해결](package-restore-troubleshooting.md)에 설명된 지침을 따르거나 [패키지를 다시 설치하고 업데이트](../consume-packages/reinstalling-and-updating-packages.md)해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-132">After running Package Restore, if you still experience missing packages or package-related errors (such as error icons in Solution Explorer in Visual Studio), you may need to follow instructions described in [Troubleshooting Package Restore errors](package-restore-troubleshooting.md) or, alternatively, [reinstall and update packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>

   <span data-ttu-id="108d7-133">Visual Studio에서 패키지 관리자 콘솔은 패키지를 다시 설치하기 위한 여러 가지 유연한 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-133">In Visual Studio, the Package Manager Console provides several flexible options for reinstalling packages.</span></span> <span data-ttu-id="108d7-134">[패키지 업데이트 사용](reinstalling-and-updating-packages.md#using-update-package)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="108d7-134">See [Using Package-Update](reinstalling-and-updating-packages.md#using-update-package).</span></span>

## <a name="restore-using-visual-studio"></a><span data-ttu-id="108d7-135">Visual Studio를 사용하여 복원</span><span class="sxs-lookup"><span data-stu-id="108d7-135">Restore using Visual Studio</span></span>

<span data-ttu-id="108d7-136">Windows의 Visual Studio에서 다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-136">In Visual Studio on Windows, either:</span></span>

- <span data-ttu-id="108d7-137">패키지를 자동으로 복원 또는</span><span class="sxs-lookup"><span data-stu-id="108d7-137">Restore packages automatically, or</span></span>

- <span data-ttu-id="108d7-138">패키지를 수동으로 복원.</span><span class="sxs-lookup"><span data-stu-id="108d7-138">Restore packages manually</span></span>

### <a name="restore-packages-automatically-using-visual-studio"></a><span data-ttu-id="108d7-139">Visual Studio를 사용하여 자동으로 패키지 복원</span><span class="sxs-lookup"><span data-stu-id="108d7-139">Restore packages automatically using Visual Studio</span></span>

<span data-ttu-id="108d7-140">패키지 복원은 [패키지 복원 사용 및 사용 안 함](#enable-and-disable-package-restore-in-visual-studio) 옵션에 따라 템플릿에서 프로젝트를 만들거나 프로젝트를 빌드할 때 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-140">Package Restore happens automatically when you create a project from a template or build a project, subject to the options in [Enable and disable package restore](#enable-and-disable-package-restore-in-visual-studio).</span></span> <span data-ttu-id="108d7-141">NuGet 4.0 이상에서는 SDK 스타일 프로젝트(일반적으로 .NET Core 또는 .NET Standard 프로젝트)가 변경되면 자동으로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-141">In NuGet 4.0+, restore also happens automatically when you make changes to a SDK-style project (typically a .NET Core or .NET Standard project).</span></span>

1. <span data-ttu-id="108d7-142">**도구** > **옵션** > **NuGet 패키지 관리자**를 선택한 후 **패키지 복원**에서 **Visual Studio에서 빌드 시 누락된 패키지를 자동으로 확인**을 선택하여 자동 패키지 복원을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-142">Enable automatic package restore by choosing **Tools** > **Options** > **NuGet Package Manager**, and then selecting **Automatically check for missing packages during build in Visual Studio** under **Package Restore**.</span></span>

   <span data-ttu-id="108d7-143">비 SDK 스타일 프로젝트의 경우 먼저 **NuGet이 누락된 패키지를 다운로드하도록 허용**을 선택하여 자동 복원 옵션을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-143">For non-SDK-style projects, you first need to select **Allow NuGet to download missing packages** to enable the automatic restore option.</span></span>

1. <span data-ttu-id="108d7-144">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-144">Build the project.</span></span>

   <span data-ttu-id="108d7-145">하나 이상의 개별 패키지가 아직 제대로 설치되지 않은 경우 **솔루션 탐색기**에 오류 아이콘이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-145">If one or more individual packages still aren't installed properly, **Solution Explorer** shows an error icon.</span></span> <span data-ttu-id="108d7-146">마우스 오른쪽 단추를 클릭하고 **NuGet 패키지 관리**를 선택하고 **패키지 관리자**를 사용하여 영향을 받은 패키지를 제거하고 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-146">Right-click and select **Manage NuGet Packages**, and use **Package Manager** to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="108d7-147">자세한 내용은 [패키지 다시 설치 및 업데이트](../consume-packages/reinstalling-and-updating-packages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="108d7-147">For more information, see [Reinstall and update packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

   <span data-ttu-id="108d7-148">"이 프로젝트는 이 컴퓨터에 없는 NuGet 패키지를 참조합니다." 또는 "하나 이상의 NuGet 패키지를 복원해야 하지만 동의하지 않아 복원할 수 없습니다."라는 오류 메시지가 표시되면 [자동 복원을 사용하도록 설정](#enable-and-disable-package-restore-in-visual-studio)하세요.</span><span class="sxs-lookup"><span data-stu-id="108d7-148">If you see the error "This project references NuGet package(s) that are missing on this computer," or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," [enable automatic restore](#enable-and-disable-package-restore-in-visual-studio).</span></span> <span data-ttu-id="108d7-149">이전 프로젝트의 경우 [자동 패키지 복원으로 마이그레이션](#migrate-to-automatic-package-restore-visual-studio)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="108d7-149">For older projects, also see [Migrate to automatic package restore](#migrate-to-automatic-package-restore-visual-studio).</span></span> <span data-ttu-id="108d7-150">[패키지 복원 문제 해결](Package-restore-troubleshooting.md)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="108d7-150">Also see [Package Restore troubleshooting](Package-restore-troubleshooting.md).</span></span>

### <a name="restore-packages-manually-using-visual-studio"></a><span data-ttu-id="108d7-151">Visual Studio를 사용하여 수동으로 패키지 복원</span><span class="sxs-lookup"><span data-stu-id="108d7-151">Restore packages manually using Visual Studio</span></span>

1. <span data-ttu-id="108d7-152">**도구** > **옵션** > **NuGet 패키지 관리자**를 선택하여 패키지 복원을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-152">Enable package restore by choosing **Tools** > **Options** > **NuGet Package Manager**.</span></span> <span data-ttu-id="108d7-153">**패키지 복원** 옵션에서 **NuGet이 누락된 패키지를 다운로드하도록 허용**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-153">Under **Package Restore** options, select **Allow NuGet to download missing packages**.</span></span>

1. <span data-ttu-id="108d7-154">**솔루션 탐색기**에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 복원**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-154">In **Solution Explorer**, right click the solution and select **Restore NuGet Packages**.</span></span>

   <span data-ttu-id="108d7-155">하나 이상의 개별 패키지가 아직 제대로 설치되지 않은 경우 **솔루션 탐색기**에 오류 아이콘이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-155">If one or more individual packages still aren't installed properly, **Solution Explorer** shows an error icon.</span></span> <span data-ttu-id="108d7-156">마우스 오른쪽 단추를 클릭하고 **NuGet 패키지 관리**를 선택한 후 **패키지 관리자**를 사용하여 영향을 받은 패키지를 제거하고 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-156">Right-click and select **Manage NuGet Packages**, and then use **Package Manager** to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="108d7-157">자세한 내용은 [패키지 다시 설치 및 업데이트](../consume-packages/reinstalling-and-updating-packages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="108d7-157">For more information, see [Reinstall and update packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

   <span data-ttu-id="108d7-158">"이 프로젝트는 이 컴퓨터에 없는 NuGet 패키지를 참조합니다." 또는 "하나 이상의 NuGet 패키지를 복원해야 하지만 동의하지 않아 복원할 수 없습니다."라는 오류 메시지가 표시되면 [자동 복원을 사용하도록 설정](#enable-and-disable-package-restore-in-visual-studio)하세요.</span><span class="sxs-lookup"><span data-stu-id="108d7-158">If you see the error "This project references NuGet package(s) that are missing on this computer," or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," [enable automatic restore](#enable-and-disable-package-restore-in-visual-studio).</span></span> <span data-ttu-id="108d7-159">이전 프로젝트의 경우 [자동 패키지 복원으로 마이그레이션](#migrate-to-automatic-package-restore-visual-studio)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="108d7-159">For older projects, also see [Migrate to automatic package restore](#migrate-to-automatic-package-restore-visual-studio).</span></span> <span data-ttu-id="108d7-160">[패키지 복원 문제 해결](Package-restore-troubleshooting.md)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="108d7-160">Also see [Package Restore troubleshooting](Package-restore-troubleshooting.md).</span></span>

### <a name="enable-and-disable-package-restore-in-visual-studio"></a><span data-ttu-id="108d7-161">Visual Studio에서 패키지 복원 사용 및 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="108d7-161">Enable and disable package restore in Visual Studio</span></span>

<span data-ttu-id="108d7-162">Visual Studio에서 주로 **도구** > **옵션** > **NuGet 패키지 관리자**를 통해 패키지 복원을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-162">In Visual Studio, you control Package Restore primarily through **Tools** > **Options** > **NuGet Package Manager**:</span></span>

![NuGet 패키지 관리자 옵션을 통한 패키지 복원 제어](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="108d7-164">**NuGet이 누락된 패키지를 다운로드하도록 허용**은 `NuGet.Config` 파일(Windows의 경우 `%AppData%\NuGet\`, Mac/Linux의 경우 `~/.nuget/NuGet/`)의 [packageRestore 섹션](../reference/nuget-config-file.md#packagerestore-section)에서 `packageRestore/enabled` 설정을 변경하여 모든 형태의 패키지 복원을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-164">**Allow NuGet to download missing packages** controls all forms of package restore by changing the `packageRestore/enabled` setting in the [packageRestore section](../reference/nuget-config-file.md#packagerestore-section) of the `NuGet.Config` file, at `%AppData%\NuGet\` on Windows, or `~/.nuget/NuGet/` on Mac/Linux.</span></span> <span data-ttu-id="108d7-165">이 설정을 사용하면 Visual Studio의 솔루션 컨텍스트 메뉴에서 **NuGet 패키지 복원** 명령을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-165">This setting also enables the **Restore NuGet Packages** command on the solution's context menu in Visual Studio, .</span></span>

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
  > <span data-ttu-id="108d7-166">`packageRestore/enabled` 설정을 전역적으로 재정의하려면 Visual Studio를 시작하거나 빌드를 시작하기 전에 환경 변수 **EnableNuGetPackageRestore**를 True 또는 False 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-166">To globally override the `packageRestore/enabled` setting, set the environment variable **EnableNuGetPackageRestore** with a value of True or False before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="108d7-167">**Visual Studio에서 빌드 시 누락된 패키지를 자동으로 확인**은 `NuGet.Config` 파일의 [packageRestore 섹션](../reference/nuget-config-file.md#packagerestore-section)에서 `packageRestore/automatic` 설정을 변경하여 자동 복원을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-167">**Automatically check for missing packages during build in Visual Studio** controls automatic restore by changing the `packageRestore/automatic` setting in the [packageRestore section](../reference/nuget-config-file.md#packagerestore-section) of the `NuGet.Config` file.</span></span> <span data-ttu-id="108d7-168">이 옵션을 True로 설정하면 Visual Studio에서 빌드를 실행할 경우 누락된 모든 패키지가 자동으로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-168">When this option is set to True, running a build from Visual Studio automatically restores any missing packages.</span></span> <span data-ttu-id="108d7-169">이 설정은 MSBuild 명령줄에서 실행되는 빌드에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-169">This setting doesn't affect builds run from the MSBuild command line.</span></span>

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

<span data-ttu-id="108d7-170">컴퓨터의 모든 사용자에 대해 패키지 복원을 활성화하거나 비활성화하기 위해 개발자 또는 회사가 구성 설정을 글로벌 `nuget.config` 파일에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-170">To enable or disable Package Restore for all users on a computer, a developer or company can add the configuration settings to the global `nuget.config` file.</span></span> <span data-ttu-id="108d7-171">글로벌 `nuget.config`는 `%ProgramData%\NuGet\Config`의 Windows, 경우에 따라 특정 `\{IDE}\{Version}\{SKU}\` Visual Studio 폴더 또는 `~/.local/share`의 Mac/Linux에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-171">The global `nuget.config` is in Windows at `%ProgramData%\NuGet\Config`, sometimes under a specific `\{IDE}\{Version}\{SKU}\` Visual Studio folder, or in Mac/Linux at `~/.local/share`.</span></span> <span data-ttu-id="108d7-172">개별 사용자는 프로젝트 수준에서 필요에 따라 선택적으로 복원을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-172">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="108d7-173">NuGet에서 여러 구성 파일의 우선순위를 지정하는 방법에 대한 자세한 내용은 [일반적인 NuGet 구성](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="108d7-173">For more details on how NuGet prioritizes multiple config files, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

> [!Important]
> <span data-ttu-id="108d7-174">`nuget.config`에서 `packageRestore` 설정을 바로 편집할 경우 Visual Studio를 다시 시작해야 **옵션** 대화 상자에 최신 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-174">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio, so that the **Options** dialog box shows the current values.</span></span>

### <a name="choose-default-package-management-format"></a><span data-ttu-id="108d7-175">기본 패키지 관리 형식 선택</span><span class="sxs-lookup"><span data-stu-id="108d7-175">Choose default package management format</span></span>

![NuGet 패키지 관리자 옵션을 통해 기본 패키지 관리 형식 제어](media/Restore-02-PackageFormatOptions.png)

<span data-ttu-id="108d7-177">NuGet에는 프로젝트에서 패키지를 사용할 수 있는 두 가지 형식([`PackageReference`](package-references-in-project-files.md) 및 [`packages.config`](../reference/packages-config.md))이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-177">NuGet has two formats in which a project may use packages: [`PackageReference`](package-references-in-project-files.md) and [`packages.config`](../reference/packages-config.md).</span></span> <span data-ttu-id="108d7-178">기본 형식은 **패키지 관리** 제목 아래의 드롭다운에서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-178">The default format can be selected from the drop-down under the **Package Management** heading.</span></span> <span data-ttu-id="108d7-179">프로젝트의 첫 번째 패키지를 설치할 때 확인하는 옵션도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-179">An option to be prompted when the first package is installed in a project is also available.</span></span>

> [!Note]
> <span data-ttu-id="108d7-180">프로젝트에서 두 패키지 관리 형식을 모두 지원하지 않는 경우 프로젝트와 호환되는 패키지 관리 형식이 사용되므로, 옵션에 설정된 기본 형식이 아닐 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-180">If a project does not support both package management formats, the package management format used will be the one that's compatible with the project, and therefore may not be the default set in the options.</span></span> <span data-ttu-id="108d7-181">또한 옵션 창에서 해당 옵션을 선택했더라도 NuGet에서 첫 번째 패키지 설치 시 선택 메시지를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-181">Additionally, NuGet will not prompt for selection on first package installation, even if the option is selected in the options window.</span></span>
>
> <span data-ttu-id="108d7-182">패키지 관리자 콘솔을 사용하여 프로젝트의 첫 번째 패키지를 설치하는 경우, 옵션 창에서 해당 옵션을 선택했더라도 NuGet에서 형식을 선택하라는 메시지를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-182">If Package Manager Console is used to install the first package in a project, NuGet will not prompt for format selection, even if the option is selected in the options window.</span></span>

## <a name="restore-using-the-dotnet-cli"></a><span data-ttu-id="108d7-183">dotnet CLI를 사용하여 복원</span><span class="sxs-lookup"><span data-stu-id="108d7-183">Restore using the dotnet CLI</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> <span data-ttu-id="108d7-184">누락 된 패키지 참조를 프로젝트 파일에 추가 하려면 [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x)를 사용합니다. 이 패키지는 또한 `restore` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-184">To add a missing package reference to the project file, use [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x), which also runs the `restore` command.</span></span>

## <a name="restore-using-the-nugetexe-cli"></a><span data-ttu-id="108d7-185">nuget.exe CLI를 사용하여 복원</span><span class="sxs-lookup"><span data-stu-id="108d7-185">Restore using the nuget.exe CLI</span></span>

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> <span data-ttu-id="108d7-186">`restore` 명령은 프로젝트 파일 또는 *packages.config*를 수정하지 않습니다. 종속성을 추가하려면 패키지 관리자 UI 또는 Visual Studio의 콘솔을 통해 패키지를 추가하거나 *packages.config*를 수정한 다음, `install` 또는 `restore` 중 하나를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-186">The `restore`command does not modify a project file or *packages.config*. To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

## <a name="restore-using-msbuild"></a><span data-ttu-id="108d7-187">MSBuild를 사용하여 복원</span><span class="sxs-lookup"><span data-stu-id="108d7-187">Restore using MSBuild</span></span>

<span data-ttu-id="108d7-188">프로젝트 파일에 나열된 패키지를 PackageReference로 복원하려면 [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-188">To restore packages listed in the project file with PackageReference, use the the [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) command.</span></span> <span data-ttu-id="108d7-189">이 명령은 Visual Studio 2017 이상 버전에 포함된 NuGet 4.x 이상 및 MSBuild 15.1 이상에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-189">This command is available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017 and higher versions.</span></span> <span data-ttu-id="108d7-190">`nuget restore` 및 `dotnet restore`는 모두 해당 프로젝트에 대해 이 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-190">Both `nuget restore` and `dotnet restore` use this command for applicable projects.</span></span>

1. <span data-ttu-id="108d7-191">개발자 명령 프롬프트를 엽니다(**검색** 상자에 **개발자 명령 프롬프트** 입력).</span><span class="sxs-lookup"><span data-stu-id="108d7-191">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="108d7-192">(일반적으로 **시작** 메뉴에서 “Visual Studio용 개발자 명령 프롬프트”를 시작하는 것이 좋습니다. MSBuild에 필요한 모든 경로로 구성되기 때문입니다.)</span><span class="sxs-lookup"><span data-stu-id="108d7-192">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

2. <span data-ttu-id="108d7-193">프로젝트 파일을 포함하는 폴더로 전환하고 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-193">Switch to the folder containing the project file and type the following command.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

3. <span data-ttu-id="108d7-194">다음 명령을 입력하여 프로젝트를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-194">Type the following command to rebuild the project.</span></span>

   ```cmd
   msbuild
   ```

   <span data-ttu-id="108d7-195">MSBuild 출력이 빌드가 성공적으로 완료되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-195">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="restore-using-azure-pipelines"></a><span data-ttu-id="108d7-196">Azure Pipelines를 사용하여 복원</span><span class="sxs-lookup"><span data-stu-id="108d7-196">Restore using Azure Pipelines</span></span>

<span data-ttu-id="108d7-197">Azure Pipelines에서 빌드 정의를 만들 때 빌드 작업 전에 NuGet [복원](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) 또는 .NET Core [복원](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) 작업을 정의에 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-197">When you create a build definition in Azure Pipelines, include the NuGet [restore](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) or .NET Core [restore](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) task in the definition before any build tasks.</span></span> <span data-ttu-id="108d7-198">몇 가지 빌드 템플릿에는 기본적으로 복원 작업이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-198">Some build templates include the restore task by default.</span></span>

## <a name="restore-using-azure-devops-server"></a><span data-ttu-id="108d7-199">Azure DevOps Server를 사용하여 복원</span><span class="sxs-lookup"><span data-stu-id="108d7-199">Restore using Azure DevOps Server</span></span>

<span data-ttu-id="108d7-200">Azure DevOps Server 및 TFS 2013 이상에서는 TFS 2013 이상 팀 빌드 템플릿을 사용하는 경우 빌드 중에 패키지를 자동으로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-200">Azure DevOps Server and TFS 2013 and later automatically restore packages during build, if you're using a TFS 2013 or later Team Build template.</span></span> <span data-ttu-id="108d7-201">이전 TFS 버전의 경우 명령줄 복원 옵션을 실행하는 빌드 단계를 포함하거나 필요에 따라 빌드 템플릿을 최신 버전으로 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-201">For earlier TFS versions, you can include a build step to run a command-line restore option, or optionally migrate the build template to a later version.</span></span> <span data-ttu-id="108d7-202">자세한 내용은 [Team Foundation 빌드를 사용하여 패키지 복원 설정](../consume-packages/team-foundation-build.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="108d7-202">For more information, see [Set up package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="constrain-package-versions-with-restore"></a><span data-ttu-id="108d7-203">복원을 사용하여 패키지 버전 제한</span><span class="sxs-lookup"><span data-stu-id="108d7-203">Constrain package versions with restore</span></span>

<span data-ttu-id="108d7-204">어떤 방법으로든 NuGet에서 패키지를 복원하는 경우 `packages.config` 또는 프로젝트 파일에 지정된 제약 조건을 준수합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-204">When NuGet restores packages through any method, it honors any constraints you specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="108d7-205">`packages.config`에서 종속성의 `allowedVersion` 속성에 버전 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-205">In `packages.config`, you can specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="108d7-206">자세한 내용은 [업그레이드 버전 제한](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="108d7-206">See [Constrain upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) for more information.</span></span> <span data-ttu-id="108d7-207">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="108d7-207">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="108d7-208">프로젝트 파일에서 PackageReference를 사용하여 종속성 범위를 직접 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-208">In a project file, you can use PackageReference to specify a dependency's range directly.</span></span> <span data-ttu-id="108d7-209">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="108d7-209">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="108d7-210">모든 경우에 [패키지 버전 관리](../concepts/package-versioning.md)에서 설명한 표기법을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="108d7-210">In all cases, use the notation described in [Package versioning](../concepts/package-versioning.md).</span></span>

## <a name="force-restore-from-package-sources"></a><span data-ttu-id="108d7-211">패키지 소스에서 강제로 복원</span><span class="sxs-lookup"><span data-stu-id="108d7-211">Force restore from package sources</span></span>

<span data-ttu-id="108d7-212">기본적으로 NuGet 복원 작업은 *global-packages* 및 *http-cache* 폴더의 패키지를 사용합니다. 이 내용은 [글로벌 패키지 및 캐시 폴더 관리](managing-the-global-packages-and-cache-folders.md)에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-212">By default, NuGet restore operations use packages from the *global-packages* and *http-cache* folders, which are described in [Manage the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="108d7-213">*global-packages* 폴더를 사용하지 않으려면 다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-213">To avoid using the *global-packages* folder, do one of the following:</span></span>

- <span data-ttu-id="108d7-214">`nuget locals global-packages -clear` 또는 `dotnet nuget locals global-packages --clear`를 사용하여 폴더를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-214">Clear the folder using `nuget locals global-packages -clear` or `dotnet nuget locals global-packages --clear`.</span></span>
- <span data-ttu-id="108d7-215">복원 작업을 수행하기 전에 다음 방법 중 하나를 사용하여 *global-packages* 폴더의 위치를 임시로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-215">Temporarily change the location of the *global-packages* folder before the restore operation, using one of the following methods:</span></span>
  - <span data-ttu-id="108d7-216">NUGET_PACKAGES 환경 변수를 다른 폴더로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-216">Set the NUGET_PACKAGES environment variable to a different folder.</span></span>
  - <span data-ttu-id="108d7-217">`globalPackagesFolder`(PackageReference를 사용할 경우) 또는 `repositoryPath`(`packages.config`를 사용할 경우)를 설정하는 `NuGet.Config` 파일을 다른 폴더에 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-217">Create a `NuGet.Config` file that sets `globalPackagesFolder` (if using PackageReference) or `repositoryPath` (if using `packages.config`) to a different folder.</span></span> <span data-ttu-id="108d7-218">자세한 내용은 [구성 설정](../reference/nuget-config-file.md#config-section)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="108d7-218">For more information, see [configuration settings](../reference/nuget-config-file.md#config-section).</span></span>
  - <span data-ttu-id="108d7-219">MSBuild에만 해당: `RestorePackagesPath` 속성을 사용하여 다른 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-219">MSBuild only: Specify a different folder with the `RestorePackagesPath` property.</span></span>

<span data-ttu-id="108d7-220">캐시를 HTTP 소스로 사용하지 않으려면 다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-220">To avoid using the cache for HTTP sources, do one of the following:</span></span>

- <span data-ttu-id="108d7-221">`nuget restore`에 `-NoCache` 옵션을 사용하거나 `dotnet restore`에 `--no-cache` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-221">Use the `-NoCache` option with `nuget restore`, or the `--no-cache` option with `dotnet restore`.</span></span> <span data-ttu-id="108d7-222">이러한 옵션은 Visual Studio 패키지 관리자 또는 콘솔을 통한 복원 작업에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-222">These options don't affect restore operations through the Visual Studio Package Manager or console.</span></span>
- <span data-ttu-id="108d7-223">`nuget locals http-cache -clear` 또는 `dotnet nuget locals http-cache --clear`를 사용하여 캐시를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-223">Clear the cache using `nuget locals http-cache -clear` or `dotnet nuget locals http-cache --clear`.</span></span>
- <span data-ttu-id="108d7-224">임시로 NUGET_HTTP_CACHE_PATH 환경 변수를 다른 폴더로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-224">Temporarily set the NUGET_HTTP_CACHE_PATH environment variable to a different folder.</span></span>

## <a name="migrate-to-automatic-package-restore-visual-studio"></a><span data-ttu-id="108d7-225">자동 패키지 복원으로 마이그레이션(Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="108d7-225">Migrate to automatic package restore (Visual Studio)</span></span>

<span data-ttu-id="108d7-226">NuGet 2.6 이하 버전의 경우 이전에는 MSBuild 통합 패키지 복원이 지원되었지만 더 이상은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-226">For NuGet 2.6 and earlier, an MSBuild-integrated package restore was previously supported but that is no longer true.</span></span> <span data-ttu-id="108d7-227">일반적으로 Visual Studio에서 솔루션을 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 복원 사용**을 선택하여 사용하도록 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-227">(It was typically enabled by right-clicking a solution in Visual Studio and selecting **Enable NuGet Package Restore**).</span></span> <span data-ttu-id="108d7-228">프로젝트에서 더 이상 지원되지 않는 MSBuild 통합 패키지 복원을 사용하는 경우 자동 패키지 복원으로 마이그레이션하세요.</span><span class="sxs-lookup"><span data-stu-id="108d7-228">If your project uses the deprecated MSBuild-integrated package restore, please migrate to automatic package restore.</span></span>

<span data-ttu-id="108d7-229">MSBuild 통합 패키지 복원을 사용하는 프로젝트에는 일반적으로 *.nuget* 폴더가 있으며 이 폴더에는 3개의 파일 *NuGet.config*, *nuget.exe* 및 *NuGet.targets*가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-229">Projects that use MSBuild-Integrated package restore typically contain a *.nuget* folder with three files: *NuGet.config*, *nuget.exe*, and *NuGet.targets*.</span></span> <span data-ttu-id="108d7-230">*Nuget.targets* 파일의 존재 여부에 따라 NuGet에서 MSBuild 통합 방법을 계속 사용하는지가 결정되므로 마이그레이션 동안 이 파일을 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-230">The presence of a *NuGet.targets* file determines whether NuGet will continue to use the MSBuild-untegrated approach, so this file must be removed during the migration.</span></span>

<span data-ttu-id="108d7-231">자동 패키지 복원으로 마이그레이션하려면(Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="108d7-231">To migrate to automatic package restore:</span></span>

1. <span data-ttu-id="108d7-232">Visual Studio를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-232">Close Visual Studio.</span></span>
2. <span data-ttu-id="108d7-233">*.nuget/nuget.exe* 및 *.nuget/NuGet.targets*를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-233">Delete *.nuget/nuget.exe* and *.nuget/NuGet.targets*.</span></span>
3. <span data-ttu-id="108d7-234">각 프로젝트 파일에 대해 `<RestorePackages>` 요소를 제거하고 *NuGet.targets*에 대한 참조를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-234">For each project file, remove the `<RestorePackages>` element and remove any reference to *NuGet.targets*.</span></span>

<span data-ttu-id="108d7-235">자동 패키지 복원을 테스트하려면</span><span class="sxs-lookup"><span data-stu-id="108d7-235">To test the automatic package restore:</span></span>

1. <span data-ttu-id="108d7-236">솔루션에서 *packages* 폴더를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-236">Remove the *packages* folder from the solution.</span></span>
2. <span data-ttu-id="108d7-237">Visual Studio에서 해당 솔루션을 열고 빌드를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-237">Open the solution in Visual Studio and start a build.</span></span>

   <span data-ttu-id="108d7-238">자동 패키지 복원은 각 종속성 패키지를 다운로드한 후, 소스 제어에 추가하지 않은 상태로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="108d7-238">Automatic package restore should download and install each dependency package, without adding them to source control.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="108d7-239">문제 해결</span><span class="sxs-lookup"><span data-stu-id="108d7-239">Troubleshooting</span></span>

<span data-ttu-id="108d7-240">[패키지 복원 문제 해결](package-restore-troubleshooting.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="108d7-240">See [Troubleshoot package restore](package-restore-troubleshooting.md).</span></span>
