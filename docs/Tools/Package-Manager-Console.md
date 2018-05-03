---
title: NuGet 패키지 관리자 콘솔 가이드
description: 패키지 작업에 대 한 Visual Studio에서 NuGet 패키지 관리자 콘솔을 사용 하기 위한 지침입니다.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 64912f0dc32a492d9c23a02f45b4303c69faf340
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="package-manager-console"></a><span data-ttu-id="becb7-103">패키지 관리자 콘솔</span><span class="sxs-lookup"><span data-stu-id="becb7-103">Package Manager Console</span></span>

<span data-ttu-id="becb7-104">NuGet 패키지 관리자 콘솔이 Windows 2012 이상 버전에서 Visual Studio에 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-104">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="becb7-105">(이 Visual Studio Code 또는 Mac에 대 한 Visual Studio에 포함 합니다.)</span><span class="sxs-lookup"><span data-stu-id="becb7-105">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="becb7-106">콘솔을 통해 사용할 수 있습니다 [NuGet PowerShell 명령을](../tools/powershell-reference.md) 를 찾으려면 설치, 제거 및 NuGet 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-106">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="becb7-107">콘솔을 사용 하는 패키지 관리자 UI 작업을 수행 하는 방법을 제공 하지 않는 경우에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-107">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="becb7-108">사용 하도록 `nuget.exe` 콘솔에서 명령을 참조 [콘솔에서 nuget.exe CLI를 사용 하 여](#using-the-nugetexe-cli-in-the-console)합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-108">To use `nuget.exe` commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="becb7-109">예를 들어, 찾기 및 설치 패키지는 3 개의 쉬운 단계를 통해 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-109">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="becb7-110">Visual Studio에서 프로젝트/솔루션을 열고 사용 하 여 콘솔을 열고는 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-110">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="becb7-111">설치 하려는 패키지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-111">Find the package you want to install.</span></span> <span data-ttu-id="becb7-112">이 이미 알고 있는 경우에 3 단계로 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-112">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="becb7-113">설치 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-113">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="becb7-114">콘솔에서 사용할 수 있는 모든 작업으로 수행할 수 있습니다는 [NuGet CLI](../tools/nuget-exe-cli-reference.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-114">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="becb7-115">그러나 콘솔 명령 Visual Studio 및 저장 된 프로젝트/솔루션의 컨텍스트 내에서 작동 하 고 종종의 상응 하는 CLI 명령 이상 수행.</span><span class="sxs-lookup"><span data-stu-id="becb7-115">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="becb7-116">예를 들어 콘솔을 통해 패키지를 설치 하는 CLI 명령에는 없는 반면 프로젝트에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-116">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="becb7-117">이러한 이유로 Visual Studio에서 일반적으로 작업 하는 개발자가 CLI에 콘솔을 사용 하 여 선호 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-117">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="becb7-118">많은 콘솔 작업 알려진된 경로 이름으로 연 Visual Studio에서 솔루션을 갖추는 것에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-118">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="becb7-119">저장 되지 않은 솔루션 또는 솔루션이 없는 경우 오류를 볼 수 있습니다, "솔루션이 열려 있지 않거나 저장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-119">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="becb7-120">있는지 확인 하십시오 열려 있고 저장 된 솔루션입니다. "</span><span class="sxs-lookup"><span data-stu-id="becb7-120">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="becb7-121">이 콘솔은 솔루션 폴더를 확인할 수 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-121">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="becb7-122">저장 되지 않은 솔루션을 저장 하거나 만들고 없는 경우 솔루션을 저장를 열고 오류를 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-122">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="becb7-123">콘솔 및 콘솔 컨트롤 열기</span><span class="sxs-lookup"><span data-stu-id="becb7-123">Opening the console and console controls</span></span>

1. <span data-ttu-id="becb7-124">Visual Studio를 사용 하 여 콘솔을 열고는 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-124">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="becb7-125">그러나 콘솔은 정렬 하 고 원하는 배치 수 있는 Visual Studio 창 (참조 [Visual Studio에서 창 레이아웃 사용자 지정](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="becb7-125">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="becb7-126">기본적으로 콘솔 명령 특정 패키지 소스 및 프로젝트에 대해 창의 위쪽에 있는 컨트롤에 설정 된 대로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-126">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![프로젝트 및 패키지 원본에 대 한 패키지 관리자 콘솔을 제어합니다.](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="becb7-128">다른 패키지 소스 및/또는 프로젝트를 선택 하면 이후 명령에 대 한 이러한 기본 설정을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-128">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="becb7-129">기본값을 변경 하지 않고 이러한 설정을 overrride 하려면 대부분의 명령은 지원 `-Source` 및 `-ProjectName` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-129">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="becb7-130">패키지 소스를 관리 하려면 기어 아이콘을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-130">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="becb7-131">이 바로 가기는 **도구 > 옵션 > NuGet 패키지 관리자 > 패키지 소스** 대화 상자에 설명 된 대로 [패키지 관리자 UI](package-manager-ui.md#package-sources) 페이지.</span><span class="sxs-lookup"><span data-stu-id="becb7-131">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="becb7-132">또한 프로젝트 선택기의 오른쪽에 컨트롤 콘솔의 내용을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-132">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![패키지 관리자 콘솔 설정과 일반 제어](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="becb7-134">오른쪽에 있는 단추는 장기 실행 명령을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-134">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="becb7-135">예를 들면 `Get-Package -ListAvailable -PageSize 500` 최상위 500 패키지를 실행 하는 데 몇 분 정도 소요 될 수 있습니다 (예: nuget.org), 기본 원본에 대해 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-135">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![패키지 관리자 콘솔 중지 제어](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="becb7-137">패키지 설치</span><span class="sxs-lookup"><span data-stu-id="becb7-137">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="becb7-138">참조 [Install-package](../tools/ps-ref-install-package.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-138">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="becb7-139">에 설명 된 대로 동일한 단계를 수행 하는 콘솔에서 패키지를 설치 [패키지 설치 될 때 어떤 일이 생기](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), 다음 사항이 추가:</span><span class="sxs-lookup"><span data-stu-id="becb7-139">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), with the following additions:</span></span>

- <span data-ttu-id="becb7-140">암시 된 계약의 창에서 해당 사용 조건 콘솔에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-140">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="becb7-141">약관에 동의 하지 않는 경우 패키지를 즉시 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-141">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="becb7-142">또한 패키지에 대 한 참조를 프로젝트 파일에 추가 되 고 표시 **솔루션 탐색기** 아래는 **참조** 직접 프로젝트 파일에서 변경 내용을 보려면 프로젝트를 저장 해야 하는 노드를 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-142">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="becb7-143">패키지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-143">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="becb7-144">참조 [Uninstall-package](../tools/ps-ref-uninstall-package.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-144">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="becb7-145">사용 하 여 [패키지 가져오기](../tools/ps-ref-get-package.md) 현재 식별자를 찾을 해야 할 경우 기본 프로젝트에 설치 된 모든 패키지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-145">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="becb7-146">패키지를 제거 합니다. 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-146">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="becb7-147">프로젝트 (및 사용 되 고 모든 관리 형식)에서 패키지에 대 한 참조를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-147">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="becb7-148">에 표시 되지 않는 참조 **솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-148">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="becb7-149">(프로젝트 참조에서 제거를 다시 작성 해야 할 수도 있습니다는 **Bin** 폴더입니다.)</span><span class="sxs-lookup"><span data-stu-id="becb7-149">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="becb7-150">변경 내용이 취소 `app.config` 또는 `web.config` 패키지가 설치 된 경우.</span><span class="sxs-lookup"><span data-stu-id="becb7-150">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="becb7-151">나머지 패키지 해당 종속성을 사용 하는 경우 종속성을 제거 이전에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-151">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="becb7-152">패키지를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-152">Updating a package</span></span>

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

<span data-ttu-id="becb7-153">참조 [패키지 가져오기](../tools/ps-ref-get-package.md) 및 [업데이트 패키지](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="becb7-153">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="becb7-154">패키지 찾기</span><span class="sxs-lookup"><span data-stu-id="becb7-154">Finding a package</span></span>

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

<span data-ttu-id="becb7-155">참조 [Find-package](../tools/ps-ref-find-package.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-155">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="becb7-156">Visual Studio 2013 및 이전 버전에서 사용 하 여 [패키지 가져오기](../tools/ps-ref-get-package.md) 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-156">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="becb7-157">콘솔의 가용성</span><span class="sxs-lookup"><span data-stu-id="becb7-157">Availability of the console</span></span>

<span data-ttu-id="becb7-158">Visual Studio 2017 NuGet 및 NuGet 패키지 관리자는 자동으로 설치 어떤를 선택 합니다. NET 관련 작업; 설치할 수 있습니다도 개별적으로 확인 하 여는 **개별 구성 요소 > 코드 도구 > NuGet 패키지 관리자** Visual Studio 2017 설치 관리자에 대 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-158">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="becb7-159">NuGet 패키지 관리자 및 이전 버전 Visual Studio 2015에서 누락 된 하는 경우 확인 **도구 > 확장 및 업데이트 중...**  NuGet 패키지 관리자 확장에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-159">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="becb7-160">Visual studio에서 확장명 설치 관리자를 사용 하는 경우에에서 직접 확장을 다운로드할 수 있습니다 [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-160">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="becb7-161">패키지 관리자 콘솔을 현재 Mac.에 대 한 Visual Studio와 함께 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-161">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="becb7-162">해당 명령 사항은 통해 사용할 수는 [NuGet CLI](nuget-exe-CLI-reference.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-162">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="becb7-163">Mac 용 visual Studio NuGet 패키지 관리를 위한 UI가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-163">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="becb7-164">참조 [프로젝트에 포함 하는 NuGet 패키지](/visualstudio/mac/nuget-walkthrough)합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-164">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="becb7-165">패키지 관리자 콘솔을 Visual Studio 코드 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-165">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="becb7-166">패키지 관리자 콘솔을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-166">Extending the Package Manager Console</span></span>

<span data-ttu-id="becb7-167">일부 패키지는 콘솔에 대 한 새 명령을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-167">Some packages install new commands for the console.</span></span> <span data-ttu-id="becb7-168">예를 들어 `MvcScaffolding` 과 같은 명령을 만듭니다 `Scaffold` ASP.NET MVC 컨트롤러와 뷰 생성 아래에 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-168">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![설치 및 MvcScaffold 사용](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="becb7-170">NuGet PowerShell 프로 파일 설정</span><span class="sxs-lookup"><span data-stu-id="becb7-170">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="becb7-171">PowerShell 프로필에는 PowerShell을 사용 하 여 때마다 일반적으로 사용 되는 명령을 사용할 수 있도록 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-171">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="becb7-172">NuGet에서는 일반적으로 다음 위치에서 발견 하는 NuGet 특정 프로필을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-172">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="becb7-173">프로필을 찾으려면 입력 `$profile` 콘솔에서:</span><span class="sxs-lookup"><span data-stu-id="becb7-173">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="becb7-174">자세한 내용은 참조 [Windows PowerShell 프로필](https://technet.microsoft.com/library/bb613488.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="becb7-174">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="becb7-175">콘솔에서 nuget.exe CLI를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="becb7-175">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="becb7-176">확인 하는 [ `nuget.exe` CLI](nuget-exe-cli-reference.md) 패키지 관리자 콘솔에서 사용할 수 있는 설치는 [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) 콘솔에서 패키지:</span><span class="sxs-lookup"><span data-stu-id="becb7-176">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
