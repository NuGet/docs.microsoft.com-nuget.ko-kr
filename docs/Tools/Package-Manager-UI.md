---
title: "NuGet 패키지 관리자 UI 참조 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
description: "NuGet 패키지를 사용 하기 위한 Visual Studio에서 NuGet 패키지 관리자 UI를 사용 하기 위한 지침입니다."
keywords: "NuGet 패키지 관리자 UI에서 NuGet 패키지 관리자 Visual Studio에서 NuGet 패키지, NuGet 사용자 인터페이스를 관리 하는 Visual Studio에서 NuGet UI"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0ff60c3cecee5fd9b7f698d2abed7553f5d89c1d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-package-manager-ui"></a><span data-ttu-id="bc8c8-104">NuGet 패키지 관리자 UI</span><span class="sxs-lookup"><span data-stu-id="bc8c8-104">NuGet Package Manager UI</span></span>

<span data-ttu-id="bc8c8-105">Windows에서 Visual Studio에서 NuGet 패키지 관리자 UI를 사용 하면 쉽게 설치, 제거 및 프로젝트와 솔루션에서 NuGet 패키지를 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-105">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="bc8c8-106">Mac 용 Visual Studio에서 차원에서 참조 [프로젝트에 포함 하는 NuGet 패키지](/visualstudio/mac/nuget-walkthrough)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-106">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="bc8c8-107">패키지 관리자 UI를 Visual Studio 코드 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-107">The Package Manager UI is not included with Visual Studio Code.</span></span>

<span data-ttu-id="bc8c8-108">항목 내용:</span><span class="sxs-lookup"><span data-stu-id="bc8c8-108">In this topic:</span></span>

- [<span data-ttu-id="bc8c8-109">찾기 및 설치 패키지 (찾아보기 탭)</span><span class="sxs-lookup"><span data-stu-id="bc8c8-109">Finding and installing a package (Browse tab)</span></span>](#finding-and-installing-a-package)
- [<span data-ttu-id="bc8c8-110">(설치 됨 탭) 패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-110">Uninstalling a package (Installed tab)</span></span>](#uninstalling-a-package)
- <span data-ttu-id="bc8c8-111">[업데이트 패키지 (설치 됨 및 업데이트 탭)](#updating-a-package) (포함 된 ["SDK에서 참조 된 암시적 으로" 또는 "AutoReferenced" 메시지](#implicit_reference))</span><span class="sxs-lookup"><span data-stu-id="bc8c8-111">[Updating a package (Installed and Updates tabs)](#updating-a-package) (includes the ["Implicitly referenced by an SDK" or "AutoReferenced" message](#implicit_reference))</span></span>
- <span data-ttu-id="bc8c8-112">[솔루션에 대 한 패키지 관리](#managing-packages-for-the-solution) (동시에 여러 프로젝트 작업).</span><span class="sxs-lookup"><span data-stu-id="bc8c8-112">[Managing packages for the solution](#managing-packages-for-the-solution) (working with multiple projects at the same time).</span></span>
- [<span data-ttu-id="bc8c8-113">패키지 원본</span><span class="sxs-lookup"><span data-stu-id="bc8c8-113">Package sources</span></span>](#package-sources)
- [<span data-ttu-id="bc8c8-114">패키지 관리자 옵션 제어</span><span class="sxs-lookup"><span data-stu-id="bc8c8-114">Package manager Options control</span></span>](#package-manager-options-control)

> [!Note]
> <span data-ttu-id="bc8c8-115">Visual Studio 2015의 NuGet 패키지 관리자를 누락 하는 경우 확인 **도구 > 확장 및 업데이트 중...**  검색 한는 *NuGet 패키지 관리자* 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-115">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="bc8c8-116">Visual studio에서 확장명 설치 관리자를 사용 하는 경우에서 직접 확장을 다운로드 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-116">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="bc8c8-117">Visual Studio 2017에 NuGet 및 NuGet 패키지 관리자 자동으로 함께 설치 됩니다. NET 관련 작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-117">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="bc8c8-118">선택 하 여 개별적으로 설치 된 **개별 구성 요소 > 코드 도구 > NuGet 패키지 관리자** Visual Studio 2017 설치 관리자에 대 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-118">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="bc8c8-119">찾기 및 설치 패키지</span><span class="sxs-lookup"><span data-stu-id="bc8c8-119">Finding and installing a package</span></span>

1. <span data-ttu-id="bc8c8-120">**솔루션 탐색기**, 단추로 클릭 하 고 **참조** 또는 프로젝트를 선택 **NuGet 패키지 관리...** .</span><span class="sxs-lookup"><span data-stu-id="bc8c8-120">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![메뉴 옵션 NuGet 패키지 관리](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="bc8c8-122">**찾아보기** 인기도 순서로 현재 선택 된 소스에서 패키지를 표시 하는 탭 (참조 [원본 패키지](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="bc8c8-122">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="bc8c8-123">홈페이지에서 검색 상자를 사용 하 여 특정 패키지를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-123">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="bc8c8-124">또한 수 있는 해당 정보를 표시 하려면 목록에서 패키지를 선택는 **설치** 함께 버전 선택 드롭 다운 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-124">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![NuGet 패키지 대화 찾아보기 탭 관리](media/Search.png)

1. <span data-ttu-id="bc8c8-126">드롭다운 목록에서 원하는 버전을 선택 하 고 선택 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-126">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="bc8c8-127">Visual Studio 프로젝트에 패키지 및 해당 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-127">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="bc8c8-128">사용 조건에 동의 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-128">You may be asked to accept license terms.</span></span> <span data-ttu-id="bc8c8-129">설치가 완료 되 면 추가 패키지에 표시 된 **설치 됨** 탭 합니다. 패키지에도 나열 됩니다는 **참조** 에서 사용 하 여 프로젝트에 참조할 수 있는지를 나타내는 솔루션 탐색기의 노드 `using` 문.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-129">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![솔루션 탐색기의 참조가](media/References.png)

> [!Tip]
    > <span data-ttu-id="bc8c8-131">검색에서 시험판 버전을 포함 하 고 시험판 버전에서 사용할 수 있도록 버전의 드롭다운 목록에서 선택 된 **시험판 포함** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-131">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="bc8c8-132">패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-132">Uninstalling a package</span></span>

1. <span data-ttu-id="bc8c8-133">**솔루션 탐색기**, 단추로 클릭 하 고 **참조** 또는 원하는 프로젝트를 선택 **NuGet 패키지 관리...** .</span><span class="sxs-lookup"><span data-stu-id="bc8c8-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="bc8c8-134">선택 된 **설치 됨** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-134">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="bc8c8-135">(필요한 경우 목록을 필터링 하려면 검색을 사용 합니다.)을 제거 하려는 패키지 선택 및 선택 **제거**합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-135">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![패키지를 제거합니다.](media/UninstallPackage.png)

1. <span data-ttu-id="bc8c8-137">**preprelease 포함** 및 **패키지 원본** 컨트롤 효과가 없습니다. 패키지를 제거 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-137">Note that the **Include preprelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="bc8c8-138">패키지를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-138">Updating a package</span></span>

1. <span data-ttu-id="bc8c8-139">**솔루션 탐색기**, 단추로 클릭 하 고 **참조** 또는 원하는 프로젝트를 선택 **NuGet 패키지 관리...** . (웹 사이트 프로젝트에서 마우스 오른쪽 단추로 클릭는 **Bin** 폴더입니다.)</span><span class="sxs-lookup"><span data-stu-id="bc8c8-139">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="bc8c8-140">선택 된 **업데이트** 탭 선택 된 패키지 소스에서 사용 가능한 업데이트가 있는 패키지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-140">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="bc8c8-141">선택 **시험판 포함** 업데이트 목록에 시험판 패키지를 포함 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-141">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="bc8c8-142">패키지 업데이트, 오른쪽의 드롭다운 목록에서 원하는 버전을 선택 및 선택를 선택한 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-142">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![패키지를 업데이트합니다.](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="bc8c8-144">일부 패키지에 대 한는 **업데이트** 단추가 비활성화 되 고 "암시적으로 참조 함을 SDK에서" 없다는 메시지가 표시 (또는 "AutoReferenced").</span><span class="sxs-lookup"><span data-stu-id="bc8c8-144">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="bc8c8-145">메시지는 Microsoft.NETCore.App 또는 Microsoft.NETStandard.Library, 같은 패키지를 더 큰 프레임 워크 또는 SDK의 일부 이며 독립적으로 업데이트 되지 않아야 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-145">The message indicates that the package, such as Microsoft.NETCore.App or Microsoft.NETStandard.Library, is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="bc8c8-146">(이러한 packagee로 내부적으로 표시 된 `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) 패키지를 업데이트 하려면 속해 있는 SDK를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-146">(Such packagee are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) To update the package, update the SDK to which it belongs.</span></span>

    ![참조 또는 AutoReferenced로 암시적으로 표시 되는 예제 패키지](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="bc8c8-148">고 목록에서 선택 여러 패키지의 최신 버전으로 업데이트 하려면는 **업데이트** 목록 위의 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-148">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="bc8c8-149">개별 패키지를 업데이트할 수도 있습니다는 **설치 됨** 탭 합니다. 패키지에 대 한 세부 정보에서 버전 선택기를 포함 하는 경우 (에 **Include 시험판** 옵션) 및 **업데이트** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-149">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="bc8c8-150">솔루션에 대 한 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="bc8c8-150">Managing packages for the solution</span></span>

<span data-ttu-id="bc8c8-151">패키지를 솔루션에 대 한 관리는 동시에 여러 프로젝트와 함께 작업 하는 편리한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-151">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="bc8c8-152">선택 된 **도구 > NuGet 패키지 관리자 > 솔루션용 NuGet 패키지 관리...**  메뉴 명령을 실행 하거나 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리...** :</span><span class="sxs-lookup"><span data-stu-id="bc8c8-152">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![솔루션에 대 한 NuGet 패키지 관리](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="bc8c8-154">솔루션에 대 한 패키지를 관리 하는 경우 UI는 실행 작업의 영향을 받는 프로젝트를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-154">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![솔루션에 대 한 패키지를 관리 하는 경우 프로젝트 선택기](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="bc8c8-156">탭 통합</span><span class="sxs-lookup"><span data-stu-id="bc8c8-156">Consolidate tab</span></span>

<span data-ttu-id="bc8c8-157">개발자가 일반적으로 고려 동일한 솔루션의 다른 프로젝트에서 서로 다른 버전의 같은 NuGet 패키지를 사용 하는 잘못 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-157">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="bc8c8-158">패키지 관리자 UI를 제공 하는 솔루션에 대 한 패키지를 관리 하려는 경우는 **통합** 를 쉽게 확인할 수 있습니다 고유한 버전 번호를 사용 하 여 패키지 솔루션의 다른 프로젝트에서 사용 되는 위치 탭:</span><span class="sxs-lookup"><span data-stu-id="bc8c8-158">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![패키지 관리자 UI 통합 탭](media/ConsolidateTab.png)

<span data-ttu-id="bc8c8-160">이 예제에서는 ClassLibrary1 프로젝트 ConsoleApp1 6.2.0 EntityFramework를 사용 하는 반면 6.2.0, EntityFramework를 사용 중인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-160">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.2.0.</span></span> <span data-ttu-id="bc8c8-161">패키지 버전을 통합 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-161">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="bc8c8-162">프로젝트 목록에서 업데이트할 프로젝트를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-162">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="bc8c8-163">이러한 모든 프로젝트에 사용할 버전을 선택는 **버전** EntityFramework 6.2.0 같은 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-163">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="bc8c8-164">선택 된 **설치** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-164">Select the **Install** button.</span></span>

<span data-ttu-id="bc8c8-165">패키지 관리자는 패키지에 더 이상 나타나지는 선택한 모든 프로젝트로 선택된 된 패키지 버전을 설치는 **통합** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-165">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="bc8c8-166">패키지 원본</span><span class="sxs-lookup"><span data-stu-id="bc8c8-166">Package sources</span></span>

<span data-ttu-id="bc8c8-167">Visual Studio는 패키지를 가져올 소스를 변경 하려면 소스 선택기에서 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-167">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![패키지 관리자 UI에서에서 패키지 원본 선택기](media/PackageSourceDropDown.png)

<span data-ttu-id="bc8c8-169">관리 하려면 패키지 소스:</span><span class="sxs-lookup"><span data-stu-id="bc8c8-169">To manage package sources:</span></span>

1. <span data-ttu-id="bc8c8-170">선택은 **설정** 패키지 관리자 UI에서 아이콘 아래에 설명 된 하거나 사용 하 여는 **도구 > 옵션** 명령를 스크롤하여 **NuGet 패키지 관리자**:</span><span class="sxs-lookup"><span data-stu-id="bc8c8-170">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![패키지 관리자 UI 설정 아이콘](media/PackageSourceSettings.png)

1. <span data-ttu-id="bc8c8-172">선택 된 **패키지 소스** 노드:</span><span class="sxs-lookup"><span data-stu-id="bc8c8-172">Select the **Package Sources** node:</span></span>

    ![패키지 소스 옵션](media/options.png)

1. <span data-ttu-id="bc8c8-174">소스를 추가 하려면 선택  **+** , 이름을 편집 하 고, URL 또는 경로 입력의 **소스** 컨트롤을 선택 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-174">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="bc8c8-175">이제 원본 선택기 드롭다운에에서 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-175">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="bc8c8-176">패키지 소스를 변경 하려면 선택에서 항목을 편집 하 고 **이름** 및 **소스** 상자 및 선택 **업데이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-176">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="bc8c8-177">패키지 소스를 사용 하지 않으려면 목록의 이름 왼쪽에 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-177">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="bc8c8-178">패키지 소스를 제거 하려면 선택 하 고 다음 선택에서 **X** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-178">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="bc8c8-179">위쪽 및 아래쪽 화살표 단추를 패키지 소스 우선 순위를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-179">Use the up and down arrow buttons to change the priority order of the package sources.</span></span> <span data-ttu-id="bc8c8-180">Visual Studio 프로젝트에 대 한 패키지를 복원 하는 경우 이러한 소스 우선 순위 순서 대로 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-180">Visual Studio searches these sources in the priority order when restoring packages for a project.</span></span> <span data-ttu-id="bc8c8-181">자세한 내용은 참조 [패키지를 복원](../Consume-Packages/Package-Restore.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-181">For more information, see [Package restore](../Consume-Packages/Package-Restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="bc8c8-182">패키지 소스 삭제 한 후 다시 경우 컴퓨터 수준 또는 사용자 수준에 나타날 수 있습니다 `NuGet.Config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-182">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="bc8c8-183">참조 [NuGet 구성 동작](../Consume-Packages/Configuring-NuGet-Behavior.md) 이러한 파일의 위치에 대 한 다음 제거 소스 파일을 수동으로 편집 하거나 사용 하 여는 [nuget 명령 원본](../tools/nuget-exe-CLI-reference.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-183">See [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="bc8c8-184">패키지 관리자 옵션 제어</span><span class="sxs-lookup"><span data-stu-id="bc8c8-184">Package manager Options control</span></span>

<span data-ttu-id="bc8c8-185">패키지를 선택한 경우 패키지 관리자 UI는 작고를 표시 하는 확장 가능한 **옵션** (축소 및 확장 모두 표시) 버전 선택기 아래에 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-185">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="bc8c8-186">일부 프로젝트에 대 한 형식 에서만 **미리 보기 창 표시** 옵션이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-186">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![패키지 관리자 옵션](media/PackageManagerUIOptions.png)

<span data-ttu-id="bc8c8-188">다음 섹션에서는 이러한 옵션에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-188">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="bc8c8-189">미리 보기 창 표시</span><span class="sxs-lookup"><span data-stu-id="bc8c8-189">Show preview window</span></span>

<span data-ttu-id="bc8c8-190">옵션을 선택 하면 모달 창 종속성을 표시 하는 선택한 패키지의 패키지를 설치 하기 전에:</span><span class="sxs-lookup"><span data-stu-id="bc8c8-190">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![예제에서는 미리 보기 대화 상자](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="bc8c8-192">설치 및 업데이트 옵션</span><span class="sxs-lookup"><span data-stu-id="bc8c8-192">Install and Update Options</span></span>

<span data-ttu-id="bc8c8-193">(사용할 수 없음 모든 프로젝트 형식에 대 한 합니다.)</span><span class="sxs-lookup"><span data-stu-id="bc8c8-193">(Not available for all project types.)</span></span>

<span data-ttu-id="bc8c8-194">**종속성 동작은** NuGet 설치할 종속성 패키지의 버전을 결정 하는 방법 구성:</span><span class="sxs-lookup"><span data-stu-id="bc8c8-194">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="bc8c8-195">*종속성 무시* 일반적으로 설치 되는 패키지를 중단 시키는 모든 종속성을 설치를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-195">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="bc8c8-196">*가장 낮은* [기본값] 기본 선택한 패키지의 요구 사항을 충족 하는 최소 버전 번호와 종속성을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-196">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="bc8c8-197">*가장 높은 패치* 같은 주 및 부 버전 번호는 있지만 패치 번호가 가장 높은 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-197">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="bc8c8-198">예를 들어 1.2.2 버전을 지정 하는 경우 다음 1.2로 시작 하는 가장 높은 버전을 설치할</span><span class="sxs-lookup"><span data-stu-id="bc8c8-198">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="bc8c8-199">*가장 높은 보조* 버전이 주 버전 번호가 같은 있지만 부 버전 번호가 가장 높은 패치 번호와 함께 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-199">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="bc8c8-200">1.2.2 버전을 지정 하는 경우 다음 1로 시작 하는 가장 높은 버전을 설치할</span><span class="sxs-lookup"><span data-stu-id="bc8c8-200">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="bc8c8-201">*가장 높은* 패키지의 사용 가능한 가장 높은 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-201">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="bc8c8-202">**충돌 작업 파일** NuGet 패키지는 프로젝트 또는 로컬 컴퓨터에 이미 있는 처리 방법을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-202">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="bc8c8-203">*Prompt* NuGet 유지 하거나 기존 패키지를 덮어쓸 것인지 확인 하도록 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-203">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="bc8c8-204">*모두 무시* 모든 기존 패키지를 덮어쓰지 않으려면 NuGet 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-204">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="bc8c8-205">*모두 덮어쓰기* 모든 기존 패키지를 덮어쓸 수는 NuGet을 지시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-205">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="bc8c8-206">제거 옵션</span><span class="sxs-lookup"><span data-stu-id="bc8c8-206">Uninstall Options</span></span>

<span data-ttu-id="bc8c8-207">(사용할 수 없음 모든 프로젝트 형식에 대 한 합니다.)</span><span class="sxs-lookup"><span data-stu-id="bc8c8-207">(Not available for all project types.)</span></span>

<span data-ttu-id="bc8c8-208">**종속성을 제거**: 옵션을 선택 하면 프로젝트의 다른 곳에서 참조 되지 하는 경우 모든 종속 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-208">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="bc8c8-209">**에 종속성이 있더라도 강제 제거**: 옵션을 선택 하면 프로젝트에서 참조 되는 경우에 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-209">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="bc8c8-210">이 일반적으로 함께에서 사용 되어 **종속성을 제거** 패키지와 관계 없이 제거할 종속성 설치 되는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-210">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="bc8c8-211">그러나이 옵션을 사용 하 여 프로젝트에서 참조가 손상된 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-211">Using this option may, however, lead to a broken references in the project.</span></span> <span data-ttu-id="bc8c8-212">이러한 경우 해야 할 수 있습니다 [다른 패키지를 다시 설치](../consume-packages/reinstalling-and-updating-packages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bc8c8-212">In such cases you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
