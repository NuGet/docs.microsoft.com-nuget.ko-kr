---
title: 설치 하 고 PowerShell을 사용 하 여 Visual Studio에서 NuGet 패키지 관리
description: Visual Studio에서 NuGet 패키지 관리자 콘솔을 사용 하 여 패키지를 사용 하 여 작업에 대 한 지침입니다.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 11ec25598d3110ba84dec5044642e205e13346af
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426212"
---
# <a name="install-and-manage-packages-using-powershell-in-visual-studio"></a><span data-ttu-id="bcaab-103">설치 하 고 PowerShell을 사용 하 여 Visual Studio에서 패키지를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-103">Install and manage packages using PowerShell in Visual Studio</span></span>

<span data-ttu-id="bcaab-104">NuGet 패키지 관리자 콘솔에서 사용할 수 있습니다 [NuGet PowerShell 명령을](../tools/powershell-reference.md) 를 찾으려면 설치, 제거 및 NuGet 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="bcaab-105">콘솔을 사용 하는 패키지 관리자 UI 작업을 수행 하는 방법을 제공 하지 않는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="bcaab-106">사용 하도록 `nuget.exe` 콘솔에서 CLI 명령 참조 [콘솔에서 nuget.exe CLI를 사용 하 여](#using-the-nugetexe-cli-in-the-console)입니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="bcaab-107">콘솔은 Windows에서 Visual Studio에 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="bcaab-108">Visual Studio Code 또는 Mac 용 Visual Studio를 사용 하 여 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="bcaab-109">찾기 및 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-109">Find and install a package</span></span>

<span data-ttu-id="bcaab-110">예를 들어, 찾기 및 패키지를 설치 하는 간단한 세 단계로 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="bcaab-111">Visual Studio에서 프로젝트/솔루션을 열고 사용 하 여 콘솔을 엽니다는 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="bcaab-112">설치 하려는 패키지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-112">Find the package you want to install.</span></span> <span data-ttu-id="bcaab-113">이 이미 알고 있는 경우 3 단계로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="bcaab-114">설치 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="bcaab-115">사용 하 여 콘솔에서 사용할 수 있는 모든 작업을 수행할 수도 있습니다는 [NuGet CLI](../tools/nuget-exe-cli-reference.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-115">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="bcaab-116">그러나 콘솔 명령 Visual Studio 및 저장 된 프로젝트/솔루션의 컨텍스트 내에서 작동 하 고 종종 해당 해당 CLI 명령 보다를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="bcaab-117">예를 들어, 콘솔을 통해 패키지를 설치 하는 CLI 명령의 반면 프로젝트에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="bcaab-118">이 따라서 일반적으로 Visual Studio에서 작업 하는 개발자는 cli 콘솔을 사용 하 여 선호 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="bcaab-119">많은 콘솔 작업 알려진된 경로 이름을 사용 하 여 Visual Studio에서 열린 솔루션에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="bcaab-120">저장 되지 않은 솔루션 또는 솔루션이 없는 경우 오류를 볼 수 있습니다, "솔루션이 열려 있지 되거나 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="bcaab-121">중인지 열기 및 저장 된 솔루션입니다. "</span><span class="sxs-lookup"><span data-stu-id="bcaab-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="bcaab-122">이 콘솔을 솔루션 폴더를 확인할 수 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="bcaab-123">저장 되지 않은 솔루션을 저장 하거나 만들고 계정이 없는 경우 솔루션을 저장를 열고 오류를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="bcaab-124">콘솔 및 콘솔 컨트롤 열기</span><span class="sxs-lookup"><span data-stu-id="bcaab-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="bcaab-125">콘솔을 사용 하 여 Visual Studio에서 엽니다는 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="bcaab-126">콘솔은 정렬 하 고 원하는 대로 정할 수 있을 수 있는 Visual Studio 창 (참조 [Visual Studio에서 창 레이아웃 사용자 지정](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="bcaab-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="bcaab-127">기본적으로 콘솔 명령은 창의 맨 위에 있는 컨트롤에 설정 된 대로 특정 패키지 소스를 프로젝트에 대해 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![패키지 원본 및 프로젝트에 대 한 패키지 관리자 콘솔을 제어합니다.](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="bcaab-129">다른 패키지 소스 및/또는 프로젝트를 선택 하면 후속 명령에 대 한 이러한 기본값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="bcaab-130">기본값을 변경 하지 않고 이러한 설정을 overrride에 대부분의 명령은 지원 `-Source` 고 `-ProjectName` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="bcaab-131">패키지 소스를 관리 하려면 기어 아이콘을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="bcaab-132">이것이 바로 가기를 합니다 **도구 > 옵션 > NuGet 패키지 관리자 > 패키지 소스** 대화 상자에 설명 된 대로 합니다 [패키지 관리자 UI](package-manager-ui.md#package-sources) 페이지.</span><span class="sxs-lookup"><span data-stu-id="bcaab-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="bcaab-133">또한 프로젝트 선택기의 오른쪽에 컨트롤을 콘솔의 내용을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![패키지 관리자 콘솔 설정 및 일반 컨트롤](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="bcaab-135">맨 오른쪽 단추를 장기 실행 명령을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="bcaab-136">예를 들어 실행 `Get-Package -ListAvailable -PageSize 500` 정도 실행 하는 데 몇 분 정도 걸릴 수 있습니다 (예: nuget.org)를 기본 원본에서 상위 500 패키지를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![패키지 관리자 콘솔 중지 제어](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="bcaab-138">패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-138">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="bcaab-139">참조 [Install-package](../tools/ps-ref-install-package.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-139">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="bcaab-140">에 설명 된 대로 동일한 단계를 수행 하는 콘솔에 패키지를 설치 [패키지를 설치 하는 경우](../concepts/package-installation-process.md), 다음 내용을 추가 하 여:</span><span class="sxs-lookup"><span data-stu-id="bcaab-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="bcaab-141">콘솔을 암시 된 계약을 사용 하 여 해당 창에서 해당 사용 약관을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="bcaab-142">약관에 동의 하지 않는 경우 패키지를 즉시 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="bcaab-143">또한 패키지에 대 한 참조를 프로젝트 파일에 추가 되 고 나타나는 **솔루션 탐색기** 아래의 합니다 **참조** 직접 프로젝트 파일의 변경 내용을 보려면 프로젝트를 저장 해야 하는 노드를 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="bcaab-144">패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-144">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="bcaab-145">참조 [Uninstall-package](../tools/ps-ref-uninstall-package.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-145">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="bcaab-146">사용 하 여 [패키지 가져오기](../tools/ps-ref-get-package.md) 현재 식별자를 찾아야 할 경우 기본 프로젝트에 설치 된 모든 패키지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-146">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="bcaab-147">패키지를 제거한 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="bcaab-148">프로젝트 (및 모든 관리 형식을 사용 중인)에서 패키지에 대 한 참조를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="bcaab-149">참조에 더 이상 나타나지 **솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="bcaab-150">(에서 제거 하는지 확인 하려면 프로젝트를 다시 작성 해야 합니다 **Bin** 폴더입니다.)</span><span class="sxs-lookup"><span data-stu-id="bcaab-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="bcaab-151">변경 내용이 되돌리는 `app.config` 또는 `web.config` 패키지가 설치 된 경우.</span><span class="sxs-lookup"><span data-stu-id="bcaab-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="bcaab-152">나머지 패키지 없음 해당 종속성을 사용 하는 경우 종속성을 제거 이전에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="bcaab-153">패키지를 업데이트 하는 중</span><span class="sxs-lookup"><span data-stu-id="bcaab-153">Updating a package</span></span>

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

<span data-ttu-id="bcaab-154">참조 [패키지 가져오기](../tools/ps-ref-get-package.md) 고 [업데이트 패키지](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="bcaab-154">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="bcaab-155">패키지 찾기</span><span class="sxs-lookup"><span data-stu-id="bcaab-155">Finding a package</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

<span data-ttu-id="bcaab-156">참조 [Find-package](../tools/ps-ref-find-package.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-156">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="bcaab-157">Visual Studio 2013 및 이전 버전에서는 사용할 [패키지 가져오기](../tools/ps-ref-get-package.md) 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-157">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="bcaab-158">콘솔의 가용성</span><span class="sxs-lookup"><span data-stu-id="bcaab-158">Availability of the console</span></span>

<span data-ttu-id="bcaab-159">Visual Studio 2017부터, NuGet 및 NuGet 패키지 관리자를 자동으로 설치 됩니다 하나를 선택 합니다. NET 관련 워크 로드. 설치할 수 있습니다도 개별적으로 확인 하 여 합니다 **개별 구성 요소 > 코드 도구 > NuGet 패키지 관리자** Visual Studio 설치 관리자에서 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="bcaab-160">Visual Studio 2015 및 이전 버전의 NuGet 패키지 관리자를 누락 하는 경우 확인 하는 또한 **도구 > 확장 및 업데이트 하는 중...**  및 NuGet 패키지 관리자 확장명을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="bcaab-161">Visual Studio에 확장 설치 관리자를 사용할 수 없습니다 경우에서 직접 확장을 다운로드할 수 있습니다 [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="bcaab-162">Mac 용 Visual Studio를 사용 하 여 현재 사용 가능한 패키지 관리자 콘솔 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="bcaab-163">그러나 해당 명령을 통해 사용할 수는 [NuGet CLI](nuget-exe-CLI-reference.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-163">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="bcaab-164">Mac 용 visual Studio NuGet 패키지 관리를 위한 UI가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="bcaab-165">참조 [NuGet 패키지 포함 프로젝트에서](/visualstudio/mac/nuget-walkthrough)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="bcaab-166">패키지 관리자 콘솔을 Visual Studio Code를 사용 하 여 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="bcaab-167">패키지 관리자 콘솔 확장</span><span class="sxs-lookup"><span data-stu-id="bcaab-167">Extending the Package Manager Console</span></span>

<span data-ttu-id="bcaab-168">일부 패키지는 콘솔에 대 한 새 명령을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="bcaab-169">예를 들어 `MvcScaffolding` 와 같은 명령을 만듭니다 `Scaffold` 아래 그림을 생성 하는 ASP.NET MVC 컨트롤러 및 보기:</span><span class="sxs-lookup"><span data-stu-id="bcaab-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![설치 및 MvcScaffold 사용](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="bcaab-171">NuGet PowerShell 프로필 설정</span><span class="sxs-lookup"><span data-stu-id="bcaab-171">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="bcaab-172">PowerShell 프로필을 사용 하면 PowerShell을 사용 하 여 어디서 나 자주 사용 하는 명령을 사용할 수 있도록 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="bcaab-173">NuGet은 일반적으로 다음 위치에 있는 NuGet 관련 프로필을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="bcaab-174">프로필을 찾으려면 입력 `$profile` 콘솔에서:</span><span class="sxs-lookup"><span data-stu-id="bcaab-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="bcaab-175">자세한 내용은 참조 [Windows PowerShell 프로필](https://technet.microsoft.com/library/bb613488.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcaab-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="bcaab-176">콘솔에서 nuget.exe CLI를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="bcaab-176">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="bcaab-177">확인 합니다 [ `nuget.exe` CLI](nuget-exe-cli-reference.md) 패키지 관리자 콘솔에서 사용할 수 있는 설치를 [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) 콘솔에서 패키지:</span><span class="sxs-lookup"><span data-stu-id="bcaab-177">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
