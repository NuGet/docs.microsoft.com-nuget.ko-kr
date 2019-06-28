---
title: 설치 하 고 Visual Studio에서 NuGet 패키지 관리
description: Visual Studio에서 NuGet 패키지 관리자 UI를 사용 하 여 NuGet 패키지 사용에 대 한 지침입니다.
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 97e5de3f07199cd3c6a645749c8f2f1603ca630e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426246"
---
# <a name="install-and-manage-packages-in-visual-studio"></a><span data-ttu-id="1e1b6-103">설치 하 고 Visual Studio에서 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="1e1b6-103">Install and manage packages in Visual Studio</span></span>

<span data-ttu-id="1e1b6-104">Windows의 Visual Studio에서 NuGet 패키지 관리자 UI를 사용 하면 쉽게 설치, 제거 및 프로젝트 및 솔루션의 NuGet 패키지를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="1e1b6-105">Mac 용 Visual Studio의 환경에 대해서 [NuGet 패키지 포함 프로젝트에서](/visualstudio/mac/nuget-walkthrough)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="1e1b6-106">패키지 관리자 UI를 Visual Studio Code를 사용 하 여 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="1e1b6-107">Visual Studio 2015에서 NuGet 패키지 관리자를 누락 하는 경우 확인 **도구 > 확장 및 업데이트 하는 중...**  검색 된 *NuGet 패키지 관리자* 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="1e1b6-108">Visual Studio에 확장 설치 관리자를 사용할 수 없습니다 경우에서 직접 확장을 다운로드할 [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="1e1b6-109">Visual Studio 2017부터 NuGet 및 NuGet 패키지 관리자를 자동으로 설치 된. NET 관련 워크 로드입니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="1e1b6-110">선택 하 여 개별적으로 설치 합니다 **개별 구성 요소 > 코드 도구 > NuGet 패키지 관리자** Visual Studio 설치 관리자에서 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="1e1b6-111">찾기 및 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-111">Finding and installing a package</span></span>

1. <span data-ttu-id="1e1b6-112">**솔루션 탐색기**, 중 하나를 마우스 오른쪽 단추로 클릭 **참조가** 프로젝트 및 선택 **NuGet 패키지 관리...** .</span><span class="sxs-lookup"><span data-stu-id="1e1b6-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![NuGet 패키지 메뉴 옵션 관리](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="1e1b6-114">합니다 **찾아보기** 탭에서 현재 선택한 소스에서 널리 사용 되 고 패키지가 표시 됩니다 (참조 [패키지 원본](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="1e1b6-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="1e1b6-115">왼쪽 위에 검색 상자를 사용 하 여 특정 패키지를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="1e1b6-116">하며 해당 정보를 표시 하려면 목록에서 패키지를 선택 합니다 **설치** 버전 선택 드롭다운 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![NuGet 패키지 대화 찾아보기 탭 관리](media/Search.png)

1. <span data-ttu-id="1e1b6-118">드롭다운 목록에서 원하는 버전을 선택 하 고 선택 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="1e1b6-119">Visual Studio 프로젝트에 패키지 및 해당 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="1e1b6-120">라이선스에 동의 하 라는 메시지가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="1e1b6-121">설치가 완료 되 면 추가 패키지에 표시 된 **설치 됨** 탭 합니다. 패키지에도 나열 됩니다는 **참조가** 프로젝트에서를 참조할 수를 나타내는 솔루션 탐색기의 노드 `using` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![솔루션 탐색기의 참조](media/References.png)

> [!Tip]
> <span data-ttu-id="1e1b6-123">검색의 시험판 버전 포함 되도록 시험판 버전에서 사용할 수 있는 드롭다운을 선택 합니다 **시험판 포함** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="1e1b6-124">패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-124">Uninstalling a package</span></span>

1. <span data-ttu-id="1e1b6-125">**솔루션 탐색기**, 중 하나를 마우스 오른쪽 단추로 클릭 **참조가** 원하는 프로젝트를 마우스 또는 **NuGet 패키지 관리...** .</span><span class="sxs-lookup"><span data-stu-id="1e1b6-125">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="1e1b6-126">선택 된 **설치 됨** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-126">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="1e1b6-127">(필요한 경우 목록을 필터링 하려면 검색을 사용 합니다.)를 제거 하려면 패키지 선택 및 선택 **제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-127">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![패키지를 제거합니다.](media/UninstallPackage.png)

1. <span data-ttu-id="1e1b6-129">합니다 **시험판 포함** 하 고 **패키지 원본** 컨트롤 영향을 주지 않습니다 패키지를 제거 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-129">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="1e1b6-130">패키지를 업데이트 하는 중</span><span class="sxs-lookup"><span data-stu-id="1e1b6-130">Updating a package</span></span>

1. <span data-ttu-id="1e1b6-131">**솔루션 탐색기**, 중 하나를 마우스 오른쪽 단추로 클릭 **참조가** 원하는 프로젝트를 마우스 또는 **NuGet 패키지 관리...** . (웹 사이트 프로젝트에서 마우스 오른쪽 단추로 클릭 합니다 **Bin** 폴더입니다.)</span><span class="sxs-lookup"><span data-stu-id="1e1b6-131">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="1e1b6-132">선택 된 **업데이트** 선택한 패키지 원본에서 사용 가능한 업데이트가 있는 패키지를 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-132">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="1e1b6-133">선택 **시험판 포함** 업데이트 목록에 시험판 패키지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-133">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="1e1b6-134">패키지, 업데이트 하 고, 오른쪽의 드롭다운 목록에서 원하는 버전을 선택 하 고, 선택를 선택한 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-134">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![패키지를 업데이트 하는 중](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="1e1b6-136">일부 패키지는 **업데이트** 단추가 비활성화 되 고 있는지 "암시적으로 참조 하는 SDK" 라는 메시지가 나타납니다 (또는 "AutoReferenced").</span><span class="sxs-lookup"><span data-stu-id="1e1b6-136">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="1e1b6-137">이 메시지는 패키지를 더 큰 프레임 워크 또는 SDK의 일부 이며 독립적으로 업데이트 되지 않아야 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-137">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="1e1b6-138">(이러한 패키지는 내부적으로 표시 `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) 예를 들어 `Microsoft.NETCore.App` .NET Core SDK의 일부인 아니며 패키지 버전의 응용 프로그램에서 사용 하는 런타임 프레임 워크 버전과 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-138">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="1e1b6-139">해야 [.NET Core 설치를 업데이트](https://aka.ms/dotnet-download) 새 버전의 ASP.NET Core 및.NET Core 런타임을 가져오려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-139">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="1e1b6-140">[.NET Core 메타 패키지 및 버전 관리에 대 한 자세한 내용은이 문서를 참조 하세요.](/dotnet/core/packages)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-140">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="1e1b6-141">이 일반적으로 사용 되는 패키지에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-141">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="1e1b6-142">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="1e1b6-142">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="1e1b6-143">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="1e1b6-143">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="1e1b6-144">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="1e1b6-144">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="1e1b6-145">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="1e1b6-145">NETStandard.Library</span></span>

    ![참조 또는 AutoReferenced로 암시적으로 표시 되는 예제 패키지](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="1e1b6-147">선택 목록에서 선택할 여러 패키지를 최신 버전으로 업데이트 하려면 합니다 **업데이트** 목록 위에 있는 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-147">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="1e1b6-148">개별 패키지를 업데이트할 수도 있습니다는 **설치 됨** 탭 합니다. 패키지에 대 한 세부 정보를 버전 선택기를 포함 하는 예제의 경우 (적용 된 **시험판 포함** 옵션) 및 **업데이트** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-148">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="1e1b6-149">솔루션에 대 한 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="1e1b6-149">Managing packages for the solution</span></span>

<span data-ttu-id="1e1b6-150">동시에 여러 프로젝트를 사용 하 여 작업 하는 편리한 방법을 솔루션의 패키지를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-150">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="1e1b6-151">선택 된 **도구 > NuGet 패키지 관리자 > 솔루션용 NuGet 패키지 관리...**  메뉴 명령을 실행 하거나 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리...** :</span><span class="sxs-lookup"><span data-stu-id="1e1b6-151">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![솔루션용 NuGet 패키지 관리](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="1e1b6-153">솔루션에 대 한 패키지를 관리 하는 경우 UI 작업의 영향을 받는 프로젝트를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-153">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![프로젝트 선택기 솔루션에 대 한 패키지를 관리 하는 경우](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="1e1b6-155">통합 탭</span><span class="sxs-lookup"><span data-stu-id="1e1b6-155">Consolidate tab</span></span>

<span data-ttu-id="1e1b6-156">개발자가 일반적으로 고려 잘못 된 방법은 동일한 솔루션 내의 여러 프로젝트에서 동일한 NuGet 패키지의 서로 다른 버전을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-156">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="1e1b6-157">패키지 관리자 UI를 제공 하는 솔루션의 패키지를 관리 하려는 경우는 **통합** 를 쉽게 확인할 수 있습니다 고유한 버전 번호를 사용 하 여 패키지를 솔루션의 다른 프로젝트에서 사용 되는 위치 탭:</span><span class="sxs-lookup"><span data-stu-id="1e1b6-157">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![패키지 관리자 UI 통합 탭](media/ConsolidateTab.png)

<span data-ttu-id="1e1b6-159">이 예제에서는 ClassLibrary1 프로젝트 ConsoleApp1 6.1.0 EntityFramework를 사용 하는 반면 6.2.0, EntityFramework를 사용한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-159">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="1e1b6-160">패키지 버전을 통합 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-160">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="1e1b6-161">프로젝트 목록에서 업데이트할 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-161">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="1e1b6-162">이러한 모든 프로젝트에 사용할 버전을 선택 합니다 **버전** EntityFramework 6.2.0 등의 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-162">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="1e1b6-163">선택 된 **설치** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-163">Select the **Install** button.</span></span>

<span data-ttu-id="1e1b6-164">패키지 관리자는 선택한 모든 프로젝트에는 패키지에 더 이상 나타나지 선택한 패키지 버전을 설치 합니다 **통합** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-164">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="1e1b6-165">패키지 소스</span><span class="sxs-lookup"><span data-stu-id="1e1b6-165">Package sources</span></span>

<span data-ttu-id="1e1b6-166">Visual Studio는 패키지를 가져올 소스를 변경 하려면 원본 선택기에서 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-166">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![패키지 관리자 UI에서에서 패키지 원본 선택기](media/PackageSourceDropDown.png)

<span data-ttu-id="1e1b6-168">패키지 소스를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-168">To manage package sources:</span></span>

1. <span data-ttu-id="1e1b6-169">선택 합니다 **설정을** 패키지 관리자 UI에서 아이콘 아래에 설명 된 또는 사용 합니다 **도구 > 옵션** 를 스크롤하여 명령 **NuGet 패키지 관리자**:</span><span class="sxs-lookup"><span data-stu-id="1e1b6-169">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![패키지 관리자 UI 설정 아이콘](media/PackageSourceSettings.png)

1. <span data-ttu-id="1e1b6-171">선택 된 **패키지 원본** 노드:</span><span class="sxs-lookup"><span data-stu-id="1e1b6-171">Select the **Package Sources** node:</span></span>

    ![패키지 원본 옵션](media/options.png)

1. <span data-ttu-id="1e1b6-173">소스를 추가 하려면 선택 **+** 이름을 편집 하 고, URL 또는 경로 입력 합니다 **소스** 컨트롤을 선택한 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-173">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="1e1b6-174">이제 원본 선택기 드롭다운 목록에에서 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-174">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="1e1b6-175">패키지 소스를 변경 하려면 선택, 편집에 **이름** 및 **원본** 입력란과 선택 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-175">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="1e1b6-176">패키지 소스를 해제 하려면 목록에서 이름 왼쪽에 상자를 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-176">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="1e1b6-177">패키지 소스를 제거 하려면 선택 하 고 다음을 선택 합니다 **X** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-177">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="1e1b6-178">사용 하 고 아래쪽 화살표 단추 패키지 원본의 우선 순위 변경 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-178">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="1e1b6-179">Visual Studio는 먼저 요청에 응답 하도록 소스가에서 패키지를 사용 하 여 패키지 소스의 순서를 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-179">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="1e1b6-180">자세한 내용은 [패키지 복원](../consume-packages/package-restore.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-180">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="1e1b6-181">패키지 소스를 삭제 한 후 다시 나타나면, 컴퓨터 수준 또는 사용자 수준에 나타날 수 있습니다 `NuGet.Config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-181">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="1e1b6-182">참조 [일반적인 NuGet 구성](../consume-packages/configuring-nuget-behavior.md) 이러한 파일의 위치에 대해 다음 원본을 제거 파일을 수동으로 편집 하거나 사용 하 여 합니다 [nuget 명령 원본](../tools/nuget-exe-CLI-reference.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-182">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="1e1b6-183">패키지 관리자 옵션 제어</span><span class="sxs-lookup"><span data-stu-id="1e1b6-183">Package manager Options control</span></span>

<span data-ttu-id="1e1b6-184">패키지 관리자 UI 표시는 작은 패키지를 선택 하면 확장 가능한 **옵션** (확장 및 축소 모두 표시) 버전 선택기 아래 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-184">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="1e1b6-185">일부 프로젝트에는 형식 에서만 합니다 **미리 보기 창 표시** 옵션이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-185">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![패키지 관리자 옵션](media/PackageManagerUIOptions.png)

<span data-ttu-id="1e1b6-187">다음 섹션에서는 이러한 옵션을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-187">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="1e1b6-188">미리 보기 창 표시</span><span class="sxs-lookup"><span data-stu-id="1e1b6-188">Show preview window</span></span>

<span data-ttu-id="1e1b6-189">옵션을 선택 하면 모달 창 종속성을 표시 하는 선택한 패키지의 패키지를 설치 하기 전에:</span><span class="sxs-lookup"><span data-stu-id="1e1b6-189">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![예제에서는 미리 보기 대화 상자](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="1e1b6-191">설치 및 업데이트 옵션</span><span class="sxs-lookup"><span data-stu-id="1e1b6-191">Install and Update Options</span></span>

<span data-ttu-id="1e1b6-192">(사용할 수 없음의 모든 프로젝트 형식에 대 한 합니다.)</span><span class="sxs-lookup"><span data-stu-id="1e1b6-192">(Not available for all project types.)</span></span>

<span data-ttu-id="1e1b6-193">**종속성 동작** NuGet 버전을 설치 하려면 종속 패키지를 결정 하는 방법 구성:</span><span class="sxs-lookup"><span data-stu-id="1e1b6-193">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="1e1b6-194">*종속성 무시* 일반적으로 설치 되는 패키지를 중단 하는 모든 종속성을 설치를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-194">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="1e1b6-195">*가장 낮은* [기본값] 기본 선택한 패키지의 요구 사항을 충족 하는 최소 버전 번호를 사용 하 여 종속성을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-195">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="1e1b6-196">*가장 높은 패치* 동일한 주 및 부 버전 번호, 있지만 패치 번호가 가장 높은 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-196">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="1e1b6-197">예를 들어 버전 1.2.2 이상을 지정 하는 경우 다음 1.2를 사용 하 여 시작 하는 가장 높은 버전을 설치할</span><span class="sxs-lookup"><span data-stu-id="1e1b6-197">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="1e1b6-198">*가장 높은 보조* 버전이 동일한 주 버전 번호를 하지만 보조 번호가 가장 높은 패치 번호와 함께 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-198">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="1e1b6-199">버전 1.2.2 이상을 지정 된 경우 다음 1로 시작 하는 가장 높은 버전을 설치할</span><span class="sxs-lookup"><span data-stu-id="1e1b6-199">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="1e1b6-200">*가장 높은* 패키지의 사용 가능한 가장 높은 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-200">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="1e1b6-201">**파일 충돌 작업** NuGet에서 프로젝트 또는 로컬 컴퓨터에 이미 있는 패키지를 처리 하는 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-201">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="1e1b6-202">*프롬프트* 유지 하거나 기존 패키지를 덮어쓸 것인지 확인 하는 NuGet에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-202">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="1e1b6-203">*모두 무시* 기존 패키지를 덮어쓰지 않으려면 NuGet에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-203">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="1e1b6-204">*모두 덮어쓰기* 기존 패키지를 덮어쓸 수는 NuGet에 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-204">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="1e1b6-205">제거 옵션</span><span class="sxs-lookup"><span data-stu-id="1e1b6-205">Uninstall Options</span></span>

<span data-ttu-id="1e1b6-206">(사용할 수 없음의 모든 프로젝트 형식에 대 한 합니다.)</span><span class="sxs-lookup"><span data-stu-id="1e1b6-206">(Not available for all project types.)</span></span>

<span data-ttu-id="1e1b6-207">**종속성을 제거**: 옵션을 선택 하면는 하지 프로젝트에서 다른 곳에서 참조 하는 경우 모든 종속 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-207">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="1e1b6-208">**에 종속 된 경우에 강제 제거**: 옵션을 선택 하면 프로젝트에서 참조 되는 경우에 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-208">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="1e1b6-209">일반적으로 함께에서 사용 됩니다 **종속성을 제거** 패키지와 관계 없이 제거할 종속성 설치 되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-209">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="1e1b6-210">그러나이 옵션을 사용 하 여 프로젝트에 대 한 손상 된 참조가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-210">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="1e1b6-211">이러한 경우 해야 [다른 패키지를 다시 설치](../consume-packages/reinstalling-and-updating-packages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e1b6-211">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
