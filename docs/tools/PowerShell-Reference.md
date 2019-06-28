---
title: NuGet PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 사용할 수 있는 PowerShell 명령에 대 한 전체 참조 합니다.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 977e06d36962366abd69f1c7f21ef33eca4e5029
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426120"
---
# <a name="powershell-reference"></a><span data-ttu-id="9ffc3-103">PowerShell 참조</span><span class="sxs-lookup"><span data-stu-id="9ffc3-103">PowerShell reference</span></span>

<span data-ttu-id="9ffc3-104">패키지 관리자 콘솔에는 아래에 나열 된 특정 명령을 통해 NuGet을 사용 하 여 상호 작용 하는 Windows에서 Visual Studio 내에서 PowerShell 인터페이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc3-104">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="9ffc3-105">(콘솔은 현재 mac 용 Visual Studio에서 사용할 수 있습니다.) 콘솔을 사용 하 여 지침을 참조 하세요 [설치 하 고 PowerShell을 사용 하 여 패키지를 관리할](../tools/package-manager-console.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc3-105">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see [Install and manage packages using PowerShell](../tools/package-manager-console.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="9ffc3-106">모든 PowerShell 명령 패키지 소비만 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc3-106">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="9ffc3-107">PowerShell 명령을 패키지 만들기 및 게시 제외 하는 패키지는 다른 패키지의 소비자를 수도 있습니다와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc3-107">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="9ffc3-108">여기에 나열 된 명령을 Visual Studio에서 패키지 관리자 콘솔에 관련이 있으며 다 합니다 [패키지 관리 모듈 명령을](/powershell/module/packagemanagement/?view=powershell-6) 일반 PowerShell 환경에서 사용할 수 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc3-108">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/?view=powershell-6) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="9ffc3-109">특히 각 환경에 다른 사용할 수 없는 명령 및 동일한 이름 사용 하 여 명령을 해당 특정 인수에도 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc3-109">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="9ffc3-110">Visual Studio에서 패키지 관리 콘솔을 사용 하는 경우 명령과이 있는 항목에 설명 된 인수를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc3-110">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="9ffc3-111">일반적인 명령</span><span class="sxs-lookup"><span data-stu-id="9ffc3-111">Common Commands</span></span> | <span data-ttu-id="9ffc3-112">설명</span><span class="sxs-lookup"><span data-stu-id="9ffc3-112">Description</span></span> | <span data-ttu-id="9ffc3-113">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="9ffc3-113">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="9ffc3-114">Install-Package</span><span class="sxs-lookup"><span data-stu-id="9ffc3-114">Install-Package</span></span>](ps-ref-install-package.md) | <span data-ttu-id="9ffc3-115">프로젝트에 패키지 및 해당 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc3-115">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="9ffc3-116">모두</span><span class="sxs-lookup"><span data-stu-id="9ffc3-116">All</span></span> |
| [<span data-ttu-id="9ffc3-117">Update-Package</span><span class="sxs-lookup"><span data-stu-id="9ffc3-117">Update-Package</span></span>](ps-ref-update-package.md) | <span data-ttu-id="9ffc3-118">프로젝트의 모든 패키지 및 해당 종속성 또는 패키지를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc3-118">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="9ffc3-119">모두</span><span class="sxs-lookup"><span data-stu-id="9ffc3-119">All</span></span> |
| [<span data-ttu-id="9ffc3-120">Find-Package</span><span class="sxs-lookup"><span data-stu-id="9ffc3-120">Find-Package</span></span>](ps-ref-find-package.md) | <span data-ttu-id="9ffc3-121">패키지 ID 또는 키워드를 사용 하 여 패키지 소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc3-121">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="9ffc3-122">3.0+</span><span class="sxs-lookup"><span data-stu-id="9ffc3-122">3.0+</span></span> |
| [<span data-ttu-id="9ffc3-123">Get-Package</span><span class="sxs-lookup"><span data-stu-id="9ffc3-123">Get-Package</span></span>](ps-ref-get-package.md) | <span data-ttu-id="9ffc3-124">로컬 저장소에 설치 된 패키지 목록을 검색 하거나 패키지 원본에서 사용할 수 있는 패키지를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc3-124">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="9ffc3-125">모두</span><span class="sxs-lookup"><span data-stu-id="9ffc3-125">All</span></span> |

| <span data-ttu-id="9ffc3-126">보조 명령</span><span class="sxs-lookup"><span data-stu-id="9ffc3-126">Secondary Commands</span></span> | <span data-ttu-id="9ffc3-127">설명</span><span class="sxs-lookup"><span data-stu-id="9ffc3-127">Description</span></span> | <span data-ttu-id="9ffc3-128">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="9ffc3-128">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="9ffc3-129">Add-BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="9ffc3-129">Add-BindingRedirect</span></span>](ps-ref-add-bindingredirect.md) | <span data-ttu-id="9ffc3-130">프로젝트의 출력 경로 내의 모든 어셈블리를 검사 하 고에 바인딩 리디렉션을 추가 합니다 `app.config` 또는 `web.config` 필요한 경우.</span><span class="sxs-lookup"><span data-stu-id="9ffc3-130">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="9ffc3-131">모두</span><span class="sxs-lookup"><span data-stu-id="9ffc3-131">All</span></span> |
| [<span data-ttu-id="9ffc3-132">Get-Project</span><span class="sxs-lookup"><span data-stu-id="9ffc3-132">Get-Project</span></span>](ps-ref-get-project.md) | <span data-ttu-id="9ffc3-133">기본 또는 지정 된 프로젝트에 대 한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc3-133">Displays information about the default or specified project.</span></span> | <span data-ttu-id="9ffc3-134">3.0+</span><span class="sxs-lookup"><span data-stu-id="9ffc3-134">3.0+</span></span> |
| [<span data-ttu-id="9ffc3-135">Open-PackagePage</span><span class="sxs-lookup"><span data-stu-id="9ffc3-135">Open-PackagePage</span></span>](ps-ref-open-packagepage.md) | <span data-ttu-id="9ffc3-136">프로젝트, 라이선스 또는 지정된 된 패키지에 대 한 URL 신고를 사용 하 여 기본 브라우저를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc3-136">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="9ffc3-137">3\.0 이상에서 사용 되지 않음</span><span class="sxs-lookup"><span data-stu-id="9ffc3-137">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="9ffc3-138">Register-TabExpansion</span><span class="sxs-lookup"><span data-stu-id="9ffc3-138">Register-TabExpansion</span></span>](ps-ref-register-tabexpansion.md) | <span data-ttu-id="9ffc3-139">일반적으로 사용 되는 매개 변수 값에 대 한 사용자 지정된 확장을 만들 수 있도록 명령의 매개 변수에 대해 탭 확장을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc3-139">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="9ffc3-140">모두</span><span class="sxs-lookup"><span data-stu-id="9ffc3-140">All</span></span> |
| [<span data-ttu-id="9ffc3-141">Sync-Package</span><span class="sxs-lookup"><span data-stu-id="9ffc3-141">Sync-Package</span></span>](ps-ref-sync-package.md) | <span data-ttu-id="9ffc3-142">패키지를 설치 하는 버전은 가져오기 프로젝트를 지정 하 고 솔루션에서 프로젝트의 나머지 부분에는 버전 동기화.</span><span class="sxs-lookup"><span data-stu-id="9ffc3-142">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="9ffc3-143">3.0+</span><span class="sxs-lookup"><span data-stu-id="9ffc3-143">3.0+</span></span> |
| [<span data-ttu-id="9ffc3-144">Uninstall-Package</span><span class="sxs-lookup"><span data-stu-id="9ffc3-144">Uninstall-Package</span></span>](ps-ref-uninstall-package.md) | <span data-ttu-id="9ffc3-145">필요에 따라 해당 종속성을 제거 하는 프로젝트에서 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc3-145">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="9ffc3-146">모두</span><span class="sxs-lookup"><span data-stu-id="9ffc3-146">All</span></span> |

<span data-ttu-id="9ffc3-147">콘솔 내에서 이러한 명령 중 하나에서 완전 하 고 자세한 도움이 필요 하면 해당 명령 이름을 사용 하 여 다음 실행:</span><span class="sxs-lookup"><span data-stu-id="9ffc3-147">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="9ffc3-148">모든 패키지 관리자 콘솔 명령은 다음을 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216):</span><span class="sxs-lookup"><span data-stu-id="9ffc3-148">All Package Manager Console commands support the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216):</span></span>

- <span data-ttu-id="9ffc3-149">디버그</span><span class="sxs-lookup"><span data-stu-id="9ffc3-149">Debug</span></span>
- <span data-ttu-id="9ffc3-150">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="9ffc3-150">ErrorAction</span></span>
- <span data-ttu-id="9ffc3-151">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="9ffc3-151">ErrorVariable</span></span>
- <span data-ttu-id="9ffc3-152">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="9ffc3-152">OutBuffer</span></span>
- <span data-ttu-id="9ffc3-153">OutVariable</span><span class="sxs-lookup"><span data-stu-id="9ffc3-153">OutVariable</span></span>
- <span data-ttu-id="9ffc3-154">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="9ffc3-154">PipelineVariable</span></span>
- <span data-ttu-id="9ffc3-155">자세히</span><span class="sxs-lookup"><span data-stu-id="9ffc3-155">Verbose</span></span>
- <span data-ttu-id="9ffc3-156">WarningAction</span><span class="sxs-lookup"><span data-stu-id="9ffc3-156">WarningAction</span></span>
- <span data-ttu-id="9ffc3-157">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="9ffc3-157">WarningVariable</span></span>

<span data-ttu-id="9ffc3-158">자세한 내용은를 참조 [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) PowerShell 설명서에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc3-158">For details, refer to [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in the PowerShell documentation.</span></span>
