---
title: Visual Studio에서 콘솔을 사용하여 NuGet 패키지 설치 및 관리
description: 패키지 작업을 위해 Visual Studio에서 NuGet 패키지 관리자 콘솔을 사용하는 방법에 대한 지침입니다.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 42031f7b5fe4d3c1b4dbe5e1bfbf9197014e0e88
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428578"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="6c385-103">Visual Studio에서 패키지 관리자 콘솔을 사용하여 패키지 설치 및 관리(PowerShell)</span><span class="sxs-lookup"><span data-stu-id="6c385-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="6c385-104">Nuget 패키지 관리자 콘솔에서는 [NuGet PowerShell 명령](../reference/powershell-reference.md)을 사용하여 NuGet 패키지를 찾고, 설치하고, 제거하고, 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../reference/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="6c385-105">패키지 관리자 UI에서 작업을 수행하는 방법을 제공하지 않는 경우에는 콘솔을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="6c385-106">콘솔에서 `nuget.exe` CLI 명령을 사용하려면 [콘솔에서 nuget.exe CLI 사용](#use-the-nugetexe-cli-in-the-console)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c385-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#use-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="6c385-107">콘솔은 Windows의 Visual Studio에 기본 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="6c385-108">Mac용 Visual Studio 또는 Visual Studio Code에는 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="6c385-109">패키지 찾기 및 설치</span><span class="sxs-lookup"><span data-stu-id="6c385-109">Find and install a package</span></span>

<span data-ttu-id="6c385-110">예를 들어 패키지를 찾고 설치하는 과정은 다음과 같은 세 가지 간단한 단계로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="6c385-111">Visual Studio에서 프로젝트/솔루션을 열고 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 명령을 사용하여 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="6c385-112">설치하려는 패키지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-112">Find the package you want to install.</span></span> <span data-ttu-id="6c385-113">이 패키지를 이미 알고 있는 경우 3단계로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="6c385-114">다음과 같이 Install 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="6c385-115">콘솔에서 사용할 수 있는 모든 작업은 [NuGet CLI](../reference/nuget-exe-cli-reference.md)로도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-115">All operations that are available in the console can also be done with the [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="6c385-116">그러나 콘솔 명령은 Visual Studio 및 저장된 프로젝트/솔루션의 컨텍스트 내에서 작동하며, 종종 해당하는 CLI 명령보다 더 많은 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="6c385-117">예를 들어, 콘솔을 통해 패키지를 설치하면 프로젝트에 대한 참조가 추가되지만 CLI 명령을 사용할 때는 이러한 참조가 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="6c385-118">이러한 이유로 Visual Studio에서 작업하는 개발자는 일반적으로 CLI보다 콘솔을 사용하는 것을 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="6c385-119">많은 콘솔 작업에서는 Visual Studio에서 알려진 경로 이름의 솔루션이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="6c385-120">저장되지 않은 솔루션이 있거나 솔루션이 없는 경우 "솔루션이 열려 있지 않거나 저장되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="6c385-121">열려 있고 저장된 솔루션이 있는지 확인하세요." 오류가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="6c385-122">이 오류는 콘솔에서 솔루션 폴더를 확인할 수 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="6c385-123">저장되지 않은 솔루션을 저장하거나, 열려 있는 솔루션이 없을 때 솔루션을 만든 후 저장하면 이 오류가 수정됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="6c385-124">콘솔 및 콘솔 컨트롤 열기</span><span class="sxs-lookup"><span data-stu-id="6c385-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="6c385-125">Visual Studio에서 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 명령을 사용하여 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="6c385-126">콘솔은 원하는 대로 정렬 및 배치할 수 있는 Visual Studio 창입니다([Visual Studio에서 창 레이아웃 사용자 지정](/visualstudio/ide/customizing-window-layouts-in-visual-studio) 참조).</span><span class="sxs-lookup"><span data-stu-id="6c385-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="6c385-127">기본적으로 콘솔 명령은 창의 맨 위에 있는 컨트롤에 설정된 대로 특정 패키지 원본 및 프로젝트에 대해 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![패키지 원본 및 프로젝트에 대한 패키지 관리자 콘솔 컨트롤](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="6c385-129">다른 패키지 원본 및/또는 프로젝트를 선택하면 후속 명령의 해당 기본값이 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="6c385-130">기본값을 변경하 않고 이러한 설정을 재정의하기 위해 대부분의 명령은 `-Source` 및 `-ProjectName` 옵션을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="6c385-131">패키지 원본을 관리하려면 기어 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="6c385-132">이 아이콘은 [패키지 관리자 UI](install-use-packages-visual-studio.md#package-sources) 페이지에 설명된 대로 **도구 > 옵션 > NuGet 패키지 관리자 > 패키지 원본** 대화 상자에 대한 바로 가기입니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](install-use-packages-visual-studio.md#package-sources) page.</span></span> <span data-ttu-id="6c385-133">또한 다음과 같은 프로젝트 선택기 오른쪽에 있는 컨트롤은 콘솔의 내용을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![패키지 관리자 콘솔 설정 및 지우기 컨트롤](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="6c385-135">오른쪽 단추는 장기 실행 명령을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="6c385-136">예를 들어 `Get-Package -ListAvailable -PageSize 500`을 실행하면 기본 원본(예: nuget.org)의 상위 500개 패키지가 표시되며, 실행하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![패키지 관리자 콘솔의 중지 컨트롤](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a><span data-ttu-id="6c385-138">패키지 설치</span><span class="sxs-lookup"><span data-stu-id="6c385-138">Install a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="6c385-139">[Install-Package](../reference/ps-reference/ps-ref-install-package.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c385-139">See [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span></span>

<span data-ttu-id="6c385-140">콘솔에 패키지를 설치하면 [패키지를 설치하면 어떻게 되나요?](../concepts/package-installation-process.md)에 설명된 것과 동일한 단계와 다음의 추가 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="6c385-141">콘솔 창에 해당 사용 조건과 묵시적 계약이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="6c385-142">조건에 동의하지 않는 경우 패키지를 즉시 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="6c385-143">또한 패키지에 대한 참조가 프로젝트 파일에 추가되고 **참조** 노드 아래의 **솔루션 탐색기**에 표시됩니다. 프로젝트 파일의 변경 내용을 직접 확인하려면 프로젝트를 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="6c385-144">패키지 제거</span><span class="sxs-lookup"><span data-stu-id="6c385-144">Uninstall a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="6c385-145">[Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c385-145">See [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="6c385-146">식별자를 찾아야 하는 경우에는 [Get-Package](../reference/ps-reference/ps-ref-get-package.md)를 사용하여 현재 기본 프로젝트에 설치된 모든 패키지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-146">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="6c385-147">패키지를 제거하면 다음 작업이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="6c385-148">프로젝트에서 패키지에 대한 참조(및 사용 중인 관리 형식)를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="6c385-149">참조가 더 이상 **솔루션 탐색기**에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="6c385-150">**Bin** 폴더에서 제거되었음을 확인하기 위해 프로젝트를 다시 빌드해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="6c385-151">패키지가 설치될 때 `app.config` 또는 `web.config`에 대해 수행된 변경 내용이 복귀됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="6c385-152">나머지 패키지에서 해당 종속성을 사용하지 않는 경우 이전에 설치된 종속성을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="6c385-153">패키지 업데이트</span><span class="sxs-lookup"><span data-stu-id="6c385-153">Update a package</span></span>

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

<span data-ttu-id="6c385-154">[Get-Package](../reference/ps-reference/ps-ref-get-package.md) 및 [Update-Package](../reference/ps-reference/ps-ref-update-package.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c385-154">See [Get-Package](../reference/ps-reference/ps-ref-get-package.md) and [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span></span>

## <a name="find-a-package"></a><span data-ttu-id="6c385-155">패키지 찾기</span><span class="sxs-lookup"><span data-stu-id="6c385-155">Find a package</span></span>

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

<span data-ttu-id="6c385-156">[Find-Package](../reference/ps-reference/ps-ref-find-package.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c385-156">See [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span></span> <span data-ttu-id="6c385-157">Visual Studio 2013 이전에는 [Get-Package](../reference/ps-reference/ps-ref-get-package.md)를 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-157">In Visual Studio 2013 and earlier, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="6c385-158">콘솔의 가용성</span><span class="sxs-lookup"><span data-stu-id="6c385-158">Availability of the console</span></span>

<span data-ttu-id="6c385-159">Visual Studio 2017부터 .NET 관련 워크로드를 선택하면 NuGet 및 NuGet 패키지 관리자가 자동으로 설치됩니다. Visual Studio 설치 관리자에서 **개별 구성 요소 > 코드 도구 > NuGet 패키지 관리자** 옵션을 선택하여 개별적으로 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="6c385-160">또한 Visual Studio 2015 이전 버전에서 NuGet 패키지 관리자가 누락된 경우 **도구 > 확장 및 업데이트...** 를 선택하고 NuGet 패키지 관리자 확장을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="6c385-161">Visual Studio에서 확장 설치 관리자를 사용할 수 없는 경우 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)에서 직접 확장을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="6c385-162">현재, Mac용 Visual Studio에서는 패키지 관리자 콘솔을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="6c385-163">그러나 [NuGet CLI](../reference/nuget-exe-CLI-reference.md)를 통해 동일한 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-163">The equivalent commands, however, are available through the [NuGet CLI](../reference/nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="6c385-164">Mac용 Visual Studio에는 NuGet 패키지를 관리하기 위한 UI가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="6c385-165">[프로젝트에 NuGet 패키지 포함](/visualstudio/mac/nuget-walkthrough)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c385-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="6c385-166">패키지 관리자 콘솔은 Visual Studio Code에 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extend-the-package-manager-console"></a><span data-ttu-id="6c385-167">패키지 관리자 콘솔 확장</span><span class="sxs-lookup"><span data-stu-id="6c385-167">Extend the Package Manager Console</span></span>

<span data-ttu-id="6c385-168">일부 패키지는 콘솔에 대한 새 명령을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="6c385-169">예를 들어 `MvcScaffolding`는 아래에 표시된 것처럼 ASP.NET MVC 컨트롤러 및 뷰를 생성하는 `Scaffold`와 같은 명령을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![MvcScaffold 설치 및 사용](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a><span data-ttu-id="6c385-171">NuGet PowerShell 프로필 설정</span><span class="sxs-lookup"><span data-stu-id="6c385-171">Set up a NuGet PowerShell profile</span></span>

<span data-ttu-id="6c385-172">Powershell 프로필을 사용하면 PowerShell을 사용할 때마다 일반적으로 사용되는 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="6c385-173">NuGet은 일반적으로 다음 위치에 있는 NuGet 특정 프로필을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="6c385-174">프로필을 찾으려면 콘솔에 `$profile`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="6c385-175">자세한 내용은 [Windows PowerShell 프로필 ](https://technet.microsoft.com/library/bb613488.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6c385-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="use-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="6c385-176">콘솔에서 nuget.exe CLI 사용</span><span class="sxs-lookup"><span data-stu-id="6c385-176">Use the nuget.exe CLI in the console</span></span>

<span data-ttu-id="6c385-177">[`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md)를 패키지 관리자 콘솔에서 사용할 수 있게 하려면 콘솔에서 [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6c385-177">To make the [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
