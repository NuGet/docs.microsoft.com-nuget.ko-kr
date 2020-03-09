---
title: Visual Studio에서 NuGet 패키지 설치 및 관리
description: NuGet 패키지 작업을 위해 Visual Studio에서 NuGet 패키지 관리자 UI를 사용하는 방법에 대한 지침입니다.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 3adceac8c725d9ea1610aea090753c9c1d8bc818
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231009"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a><span data-ttu-id="f1d3b-103">Visual Studio에서 NuGet 패키지 관리자를 사용하여 패키지 설치 및 관리</span><span class="sxs-lookup"><span data-stu-id="f1d3b-103">Install and manage packages in Visual Studio using the NuGet Package Manager</span></span>

<span data-ttu-id="f1d3b-104">Windows의 Visual Studio의 NuGet 패키지 관리자 UI를 사용하여 프로젝트 및 솔루션에서 NuGet 패키지를 쉽게 설치, 제거 및 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="f1d3b-105">Mac용 Visual Studio 환경의 경우 [프로젝트에 NuGet 패키지 포함](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json).</span></span> <span data-ttu-id="f1d3b-106">패키지 관리자 UI는 Visual Studio Code에 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="f1d3b-107">Visual Studio 2015에서 NuGet 패키지 관리자가 누락된 경우 **도구 > 확장 및 업데이트...** 를 선택하고 *NuGet 패키지 관리자* 확장을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="f1d3b-108">Visual Studio에서 확장 설치 관리자를 사용할 수 없는 경우 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)에서 직접 확장을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="f1d3b-109">Visual Studio 2017부터 NuGet 및 NuGet 패키지 관리자는 .NET 관련 워크로드와 함께 자동으로 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="f1d3b-110">Visual Studio 설치 관리자에서 **개별 구성 요소 > 코드 도구 > NuGet 패키지 관리자** 옵션을 선택하여 따로 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="f1d3b-111">패키지 찾기 및 설치</span><span class="sxs-lookup"><span data-stu-id="f1d3b-111">Find and install a package</span></span>

1. <span data-ttu-id="f1d3b-112">**솔루션 탐색기**에서 **참조** 또는 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리...** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![NuGet 패키지 관리 메뉴 옵션](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="f1d3b-114">**찾아보기** 탭은 현재 선택된 원본의 패키지를 인지도별로 표시합니다([패키지 원본](#package-sources) 참조).</span><span class="sxs-lookup"><span data-stu-id="f1d3b-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="f1d3b-115">왼쪽 위의 검색 상자를 사용하여 특정 패키지를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="f1d3b-116">목록에서 패키지를 선택하여 해당 정보를 표시합니다. 이 경우 버전 선택드롭다운과 함께 **설치** 단추도 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![NuGet 패키지 관리 대화 상자의 찾아보기 탭](media/Search.png)

1. <span data-ttu-id="f1d3b-118">드롭다운에서 원하는 버전을 선택하고 **설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="f1d3b-119">Visual Studio는 패키지와 해당 종속성을 프로젝트에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="f1d3b-120">사용 조건에 동의하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="f1d3b-121">설치가 완료되면 추가된 패키지가 **설치됨** 탭에 나타납니다. 패키지는 솔루션 탐색기의 **참조** 노드에도 표시되어, `using` 문을 사용하여 프로젝트에서 해당 패키지를 참조할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![솔루션 탐색기의 참조](media/References.png)

> [!Tip]
> <span data-ttu-id="f1d3b-123">검색에 시험판 버전을 포함하고 버전 드롭다운에서 시험판 버전을 사용할 수 있도록 하려면 **시험판 포함** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

> [!Note]
> <span data-ttu-id="f1d3b-124">NuGet에는 프로젝트에서 패키지를 사용할 수 있는 두 가지 형식([`PackageReference`](package-references-in-project-files.md) 및 [`packages.config`](../reference/packages-config.md))이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-124">NuGet has two formats in which a project may use packages: [`PackageReference`](package-references-in-project-files.md) and [`packages.config`](../reference/packages-config.md).</span></span> <span data-ttu-id="f1d3b-125">[Visual Studio의 옵션 창에서 기본값을 설정할 수 있습니다](Package-Restore.md#choose-default-package-management-format).</span><span class="sxs-lookup"><span data-stu-id="f1d3b-125">[The default can be set in Visual Studio's options window](Package-Restore.md#choose-default-package-management-format).</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="f1d3b-126">패키지 제거</span><span class="sxs-lookup"><span data-stu-id="f1d3b-126">Uninstall a package</span></span>

1. <span data-ttu-id="f1d3b-127">**솔루션 탐색기**에서 **참조** 또는 원하는 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리...** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-127">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="f1d3b-128">**설치됨** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-128">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="f1d3b-129">제거할 패키지를 선택하고(필요한 경우 검색을 사용하여 목록 필터링) **제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-129">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![패키지 제거](media/UninstallPackage.png)

1. <span data-ttu-id="f1d3b-131">패키지를 제거할 때 **시험판 포함** 및 **패키지 원본** 컨트롤은 아무런 영향도 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-131">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="f1d3b-132">패키지 업데이트</span><span class="sxs-lookup"><span data-stu-id="f1d3b-132">Update a package</span></span>

1. <span data-ttu-id="f1d3b-133">**솔루션 탐색기**에서 **참조** 또는 원하는 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리...** 를 선택합니다. (웹 사이트 프로젝트에서 **Bin** 폴더를 마우스 오른쪽 단추로 클릭합니다.)</span><span class="sxs-lookup"><span data-stu-id="f1d3b-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="f1d3b-134">**업데이트** 탭을 선택하여 선택한 패키지 원본의 사용 가능한 업데이트가 있는 패키지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-134">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="f1d3b-135">업데이트 목록에 시험판 패키지를 포함하려면 **시험판 포함**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-135">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="f1d3b-136">업데이트할 패키지를 선택하고 오른쪽의 드롭다운에서 원하는 버전을 선택하고 **업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-136">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![패키지 업데이트](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="f1d3b-138">일부 패키지의 경우 **업데이트** 단추가 사용하지 않도록 설정되고 "SDK에서 암시적으로 참조됩니다.”(또는 “자동 참조됨")이라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-138">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="f1d3b-139">이 메시지는 패키지가 더 큰 프레임워크 또는 SDK의 일부이며 독립적으로 업데이트해서는 안 됨을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-139">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="f1d3b-140">(이러한 패키지는 내부적으로 `<IsImplicitlyDefined>True</IsImplicitlyDefined>`로 표시됩니다.) 예를 들어 `Microsoft.NETCore.App`은 .NET Core SDK의 일부이며 패키지 버전은 애플리케이션에서 사용하는 런타임 프레임워크의 버전과 동일하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-140">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="f1d3b-141">새 버전의 ASP.NET Core 및 .NET Core 런타임을 가져오려면 [.NET Core 설치를 업데이트](https://aka.ms/dotnet-download)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-141">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="f1d3b-142">[.NET Core 메타패키지 및 버전 관리에 대한 자세한 내용은 이 문서를 참조하세요.](/dotnet/core/packages)</span><span class="sxs-lookup"><span data-stu-id="f1d3b-142">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="f1d3b-143">이 문서는 일반적으로 사용되는 다음 패키지에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-143">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="f1d3b-144">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="f1d3b-144">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="f1d3b-145">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="f1d3b-145">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="f1d3b-146">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="f1d3b-146">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="f1d3b-147">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="f1d3b-147">NETStandard.Library</span></span>

    ![암시적 참조 또는 자동 참조로 표시된 예제 패키지](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="f1d3b-149">여러 패키지를 최신 버전으로 업데이트하려면 목록에서 해당 패키지를 선택하고 목록 위의 **업데이트** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-149">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="f1d3b-150">**설치됨** 탭에서 개별 패키지를 업데이트할 수도 있습니다. 이 경우 패키지에 대한 세부 정보에는 버전 선택기(**시험판 포함** 옵션의 영향을 받음) 및 **업데이트** 단추가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-150">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="manage-packages-for-the-solution"></a><span data-ttu-id="f1d3b-151">솔루션 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="f1d3b-151">Manage packages for the solution</span></span>

<span data-ttu-id="f1d3b-152">솔루션의 패키지를 관리하는 것은 여러 프로젝트를 동시에 사용할 수 있는 편리한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-152">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="f1d3b-153">**도구 > Nuget 패키지 관리자 > 솔루션에 대한 NuGet 패키지 관리...** 메뉴 명령을 선택하거나 솔루션을 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리...** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-153">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![솔루션에 대한 NuGet 패키지 관리](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="f1d3b-155">솔루션의 패키지를 관리할 때 UI를 사용하여 작업의 영향을 받는 프로젝트를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-155">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![솔루션의 패키지를 관리할 경우의 프로젝트 선택기](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="f1d3b-157">통합 탭</span><span class="sxs-lookup"><span data-stu-id="f1d3b-157">Consolidate tab</span></span>

<span data-ttu-id="f1d3b-158">개발자들은 일반적으로 동일한 솔루션의 여러 프로젝트에서 동일한 NuGet 패키지의 여러 버전을 사용하는 것이 적절하지 않다고 생각합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-158">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="f1d3b-159">솔루션의 패키지를 관리하도록 선택하면 패키지 관리자 UI에서 **통합** 탭을 합니다. 이 탭에서는 고유한 버전 번호가 있는 패키지가 솔루션의 여러 다른 프로젝트에서 사용되는 경우를 쉽게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-159">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![패키지 관리자 UI 통합 탭](media/ConsolidateTab.png)

<span data-ttu-id="f1d3b-161">이 예제에서 ClassLibrary1 프로젝트는 EntityFramework 6.2.0을 사용하지만, ConsoleApp1는 EntityFramework 6.1.0을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-161">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="f1d3b-162">패키지 버전을 통합하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-162">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="f1d3b-163">프로젝트 목록에서 업데이트할 프로젝트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-163">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="f1d3b-164">**버전** 제어에서 모든 프로젝트에서 사용할 버전(예: Entityframework 6.2.0)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-164">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="f1d3b-165">**설치** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-165">Select the **Install** button.</span></span>

<span data-ttu-id="f1d3b-166">패키지 관리자가 선택한 모든 프로젝트에 선택한 패키지 버전을 설치하면, 해당 패키지가 더 이상 **통합** 탭에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-166">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="f1d3b-167">패키지 원본</span><span class="sxs-lookup"><span data-stu-id="f1d3b-167">Package sources</span></span>

<span data-ttu-id="f1d3b-168">Visual Studio에서 패키지를 가져오는 원본을 변경하려면 원본 선택기에서 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-168">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![패키지 관리자 UI의 패키지 원본 선택기](media/PackageSourceDropDown.png)

<span data-ttu-id="f1d3b-170">패키지 원본을 관리하려면</span><span class="sxs-lookup"><span data-stu-id="f1d3b-170">To manage package sources:</span></span>

1. <span data-ttu-id="f1d3b-171">아래에 설명된 패키지 관리자 UI에서 **설정** 아이콘을 선택하거나 **도구 > 옵션** 명령을 사용하고 **NuGet 패키지 관리자**로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-171">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![패키지 관리자 UI 설정 아이콘](media/PackageSourceSettings.png)

1. <span data-ttu-id="f1d3b-173">다음과 같이 **패키지 원본** 노드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-173">Select the **Package Sources** node:</span></span>

    ![패키지 원본 옵션](media/options.png)

1. <span data-ttu-id="f1d3b-175">원본을 추가하려면 **+** 를 선택하고 이름을 편집한 후 **원본** 제어에서 URL 또는 경로를 입력하고 **업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-175">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="f1d3b-176">이제 원본이 선택기 드롭다운에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-176">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="f1d3b-177">패키지 원본을 변경하려면 해당 패키지 원본을 선택하고 **이름** 및 **원본** 상자에서 편집한 후 **업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-177">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="f1d3b-178">패키지 원본을 사용하지 않도록 설정하려면 목록에서 이름 왼쪽에 있는 확인란을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-178">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="f1d3b-179">패키지 원본을 제거하려면 해당 패키지 원본을 선택한 다음, **X** 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-179">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="f1d3b-180">위쪽 및 아래쪽 화살표 단추를 사용해도 패키지 원본의 우선 순위는 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-180">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="f1d3b-181">Visual Studio는 패키지 소스의 순서를 무시하고, 소스가 요청에 응답하는 순서대로 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-181">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="f1d3b-182">자세한 내용은 [패키지 복원](../consume-packages/package-restore.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-182">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="f1d3b-183">삭제 후 패키지 원본이 다시 표시되면 컴퓨터 수준 또는 사용자 수준 `NuGet.Config` 파일에 나열될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-183">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="f1d3b-184">이러한 파일의 위치를 [일반 NuGet 구성](../consume-packages/configuring-nuget-behavior.md)에서 확인한 후, 파일을 수동으로 편집하거나 [nuget sources 명령](../reference/nuget-exe-CLI-reference.md)을 사용하여 원본을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-184">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../reference/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="f1d3b-185">패키지 관리자 옵션 제어</span><span class="sxs-lookup"><span data-stu-id="f1d3b-185">Package manager Options control</span></span>

<span data-ttu-id="f1d3b-186">패키지를 선택하면 패키지 관리자 UI에서 버전 선택기 아래에 확장 가능한 작은 **옵션** 컨트롤이 표시됩니다(여기에는 축소형과 확장형이 모두 표시됨).</span><span class="sxs-lookup"><span data-stu-id="f1d3b-186">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="f1d3b-187">일부 프로젝트 형식의 경우 **미리 보기 창 표시** 옵션만 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-187">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![패키지 관리자 옵션](media/PackageManagerUIOptions.png)

<span data-ttu-id="f1d3b-189">다음 섹션에서는 이러한 옵션에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-189">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="f1d3b-190">미리 보기 창 표시</span><span class="sxs-lookup"><span data-stu-id="f1d3b-190">Show preview window</span></span>

<span data-ttu-id="f1d3b-191">이 옵션을 선택하면 패키지를 설치하기 전에 선택한 패키지의 종속성이 모달 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-191">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![예제 미리 보기 대화 상자](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="f1d3b-193">설치 및 업데이트 옵션</span><span class="sxs-lookup"><span data-stu-id="f1d3b-193">Install and Update Options</span></span>

<span data-ttu-id="f1d3b-194">(일부 프로젝트 형식에는 사용할 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="f1d3b-194">(Not available for all project types.)</span></span>

<span data-ttu-id="f1d3b-195">**종속성 동작**은 NuGet에서 설치할 종속 패키지의 버전을 결정하는 방법을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-195">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="f1d3b-196">*종속성 무시*는 설치 중인 패키지를 중단하는 종속성의 설치를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-196">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="f1d3b-197">*최하위*[기본값]는 선택한 기본 패키지의 요구 사항을 충족하는 최소 버전 번호의 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-197">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="f1d3b-198">*최상위 패치*는 주 및 부 버전 번호는 같지만 최상위 패치 번호는 다른 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-198">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="f1d3b-199">예를 들어, 버전 1.2.2를 지정한 경우 1.2로 시작하는 최고 버전이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-199">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="f1d3b-200">*최상위 부*는 주 버전 번호는 같지만 최상위 부 번호와 패치 번호는 다른 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-200">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="f1d3b-201">버전 1.2.2를 지정한 경우 1로 시작하는 최고 버전이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-201">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="f1d3b-202">*최상위*는 패키지의 사용 가능한 최상위 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-202">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="f1d3b-203">**파일 충돌 작업**은 NuGet이 프로젝트 또는 로컬 컴퓨터에 이미 있는 패키지를 처리하는 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-203">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="f1d3b-204">*프롬프트*는 기존 패키지를 유지할지 아니면 덮어쓸지 묻는 메시지를 요청하도록 NuGet에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-204">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="f1d3b-205">*모두 무시*는 기존 패키지 덮어쓰기를 건너뛰도록 NuGet에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-205">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="f1d3b-206">*모두 덮어쓰기*는 기존 패키지를 덮어쓰도록 NuGet에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-206">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="f1d3b-207">제거 옵션</span><span class="sxs-lookup"><span data-stu-id="f1d3b-207">Uninstall Options</span></span>

<span data-ttu-id="f1d3b-208">(일부 프로젝트 형식에는 사용할 수 없습니다.)</span><span class="sxs-lookup"><span data-stu-id="f1d3b-208">(Not available for all project types.)</span></span>

<span data-ttu-id="f1d3b-209">**종속성 제거**: 이 옵션을 선택하면 프로젝트의 다른 곳에서 참조되지 않는 모든 종속 패키지가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-209">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="f1d3b-210">**관련 종속성이 있더라도 강제 제거**: 이 옵션을 선택하면 프로젝트에서 아직 참조되고 있더라도 패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-210">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="f1d3b-211">일반적으로 **종속성 제거**와 함께 사용하여 패키지 및 설치한 종속성을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-211">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="f1d3b-212">그러나 이 옵션을 사용하면 프로젝트에서 참조가 손상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-212">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="f1d3b-213">이러한 경우 [다른 패키지를 다시 설치](../consume-packages/reinstalling-and-updating-packages.md)해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f1d3b-213">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
