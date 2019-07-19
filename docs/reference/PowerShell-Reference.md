---
title: NuGet PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 사용할 수 있는 PowerShell 명령에 대 한 전체 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 142af9c4f7d25c3b0d986524313851cceb1e4c60
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327930"
---
# <a name="powershell-reference"></a><span data-ttu-id="4cc5d-103">PowerShell 참조</span><span class="sxs-lookup"><span data-stu-id="4cc5d-103">PowerShell reference</span></span>

<span data-ttu-id="4cc5d-104">패키지 관리자 콘솔은 Windows의 Visual Studio 내 PowerShell 인터페이스를 제공 하 여 아래 나열 된 특정 명령을 통해 NuGet과 상호 작용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-104">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="4cc5d-105">콘솔은 현재 Mac용 Visual Studio에서 사용할 수 없습니다. 콘솔 사용에 대 한 가이드는 [패키지 관리자 콘솔을 사용 하 여 패키지 설치 및 관리](../consume-packages/install-use-packages-powershell.md) 항목을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-105">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="4cc5d-106">모든 PowerShell 명령은 패키지 사용량과만 관련 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-106">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="4cc5d-107">패키지를 만들고 게시 하는 것과 관련 된 PowerShell 명령은 없습니다. 단, 패키지가 다른 패키지의 소비자 일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-107">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="4cc5d-108">여기에 나열 된 명령은 Visual Studio의 패키지 관리자 콘솔과 다르며 일반 PowerShell 환경에서 사용할 수 있는 [패키지 관리 모듈 명령과](/powershell/module/packagemanagement/?view=powershell-6) 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-108">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/?view=powershell-6) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="4cc5d-109">특히, 각 환경에는 사용할 수 없는 명령이 있으며 동일한 이름의 명령은 특정 인수에서 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-109">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="4cc5d-110">Visual Studio에서 패키지 관리 콘솔을 사용 하는 경우이 현재 항목에 설명 된 명령 및 인수를 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-110">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="4cc5d-111">일반 명령</span><span class="sxs-lookup"><span data-stu-id="4cc5d-111">Common Commands</span></span> | <span data-ttu-id="4cc5d-112">설명</span><span class="sxs-lookup"><span data-stu-id="4cc5d-112">Description</span></span> | <span data-ttu-id="4cc5d-113">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="4cc5d-113">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="4cc5d-114">Install-Package</span><span class="sxs-lookup"><span data-stu-id="4cc5d-114">Install-Package</span></span>](ps-reference/ps-ref-install-package.md) | <span data-ttu-id="4cc5d-115">패키지와 해당 종속성을 프로젝트에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-115">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="4cc5d-116">모두</span><span class="sxs-lookup"><span data-stu-id="4cc5d-116">All</span></span> |
| [<span data-ttu-id="4cc5d-117">Update-Package</span><span class="sxs-lookup"><span data-stu-id="4cc5d-117">Update-Package</span></span>](ps-reference/ps-ref-update-package.md) | <span data-ttu-id="4cc5d-118">패키지와 해당 종속성 또는 프로젝트의 모든 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-118">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="4cc5d-119">모두</span><span class="sxs-lookup"><span data-stu-id="4cc5d-119">All</span></span> |
| [<span data-ttu-id="4cc5d-120">Find-Package</span><span class="sxs-lookup"><span data-stu-id="4cc5d-120">Find-Package</span></span>](ps-reference/ps-ref-find-package.md) | <span data-ttu-id="4cc5d-121">패키지 ID 또는 키워드를 사용 하 여 패키지 소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-121">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="4cc5d-122">3.0+</span><span class="sxs-lookup"><span data-stu-id="4cc5d-122">3.0+</span></span> |
| [<span data-ttu-id="4cc5d-123">Get-Package</span><span class="sxs-lookup"><span data-stu-id="4cc5d-123">Get-Package</span></span>](ps-reference/ps-ref-get-package.md) | <span data-ttu-id="4cc5d-124">로컬 리포지토리에 설치 된 패키지 목록을 검색 하거나 패키지 원본에서 사용할 수 있는 패키지를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-124">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="4cc5d-125">모두</span><span class="sxs-lookup"><span data-stu-id="4cc5d-125">All</span></span> |

| <span data-ttu-id="4cc5d-126">보조 명령</span><span class="sxs-lookup"><span data-stu-id="4cc5d-126">Secondary Commands</span></span> | <span data-ttu-id="4cc5d-127">설명</span><span class="sxs-lookup"><span data-stu-id="4cc5d-127">Description</span></span> | <span data-ttu-id="4cc5d-128">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="4cc5d-128">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="4cc5d-129">Add-BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="4cc5d-129">Add-BindingRedirect</span></span>](ps-reference/ps-ref-add-bindingredirect.md) | <span data-ttu-id="4cc5d-130">프로젝트의 출력 경로에 있는 모든 어셈블리를 검사 하 고 필요에 따라 `app.config` 또는 `web.config` 에 바인딩 리디렉션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-130">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="4cc5d-131">모두</span><span class="sxs-lookup"><span data-stu-id="4cc5d-131">All</span></span> |
| [<span data-ttu-id="4cc5d-132">Get-Project</span><span class="sxs-lookup"><span data-stu-id="4cc5d-132">Get-Project</span></span>](ps-reference/ps-ref-get-project.md) | <span data-ttu-id="4cc5d-133">기본 또는 지정 된 프로젝트에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-133">Displays information about the default or specified project.</span></span> | <span data-ttu-id="4cc5d-134">3.0+</span><span class="sxs-lookup"><span data-stu-id="4cc5d-134">3.0+</span></span> |
| [<span data-ttu-id="4cc5d-135">Open-PackagePage</span><span class="sxs-lookup"><span data-stu-id="4cc5d-135">Open-PackagePage</span></span>](ps-reference/ps-ref-open-packagepage.md) | <span data-ttu-id="4cc5d-136">지정 된 패키지에 대 한 프로젝트, 라이선스 또는 신고 URL을 사용 하 여 기본 브라우저를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-136">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="4cc5d-137">3\.0 이상에서 사용 되지 않음</span><span class="sxs-lookup"><span data-stu-id="4cc5d-137">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="4cc5d-138">Register-TabExpansion</span><span class="sxs-lookup"><span data-stu-id="4cc5d-138">Register-TabExpansion</span></span>](ps-reference/ps-ref-register-tabexpansion.md) | <span data-ttu-id="4cc5d-139">명령 매개 변수에 대 한 탭 확장을 등록 하 여 일반적으로 사용 되는 매개 변수 값에 대 한 사용자 지정 확장을 만들 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-139">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="4cc5d-140">모두</span><span class="sxs-lookup"><span data-stu-id="4cc5d-140">All</span></span> |
| [<span data-ttu-id="4cc5d-141">Sync-Package</span><span class="sxs-lookup"><span data-stu-id="4cc5d-141">Sync-Package</span></span>](ps-reference/ps-ref-sync-package.md) | <span data-ttu-id="4cc5d-142">지정 된 프로젝트에서 설치 된 패키지 버전을 가져오고 솔루션의 나머지 프로젝트에 버전을 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-142">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="4cc5d-143">3.0+</span><span class="sxs-lookup"><span data-stu-id="4cc5d-143">3.0+</span></span> |
| [<span data-ttu-id="4cc5d-144">Uninstall-Package</span><span class="sxs-lookup"><span data-stu-id="4cc5d-144">Uninstall-Package</span></span>](ps-reference/ps-ref-uninstall-package.md) | <span data-ttu-id="4cc5d-145">프로젝트에서 패키지를 제거 하 고 필요에 따라 해당 종속성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-145">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="4cc5d-146">모두</span><span class="sxs-lookup"><span data-stu-id="4cc5d-146">All</span></span> |

<span data-ttu-id="4cc5d-147">콘솔 내에서 이러한 명령에 대 한 자세한 도움말을 보려면 명령 이름으로 다음을 실행 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-147">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="4cc5d-148">모든 패키지 관리자 콘솔 명령은 다음과 같은 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216)를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-148">All Package Manager Console commands support the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216):</span></span>

- <span data-ttu-id="4cc5d-149">디버그</span><span class="sxs-lookup"><span data-stu-id="4cc5d-149">Debug</span></span>
- <span data-ttu-id="4cc5d-150">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="4cc5d-150">ErrorAction</span></span>
- <span data-ttu-id="4cc5d-151">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="4cc5d-151">ErrorVariable</span></span>
- <span data-ttu-id="4cc5d-152">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="4cc5d-152">OutBuffer</span></span>
- <span data-ttu-id="4cc5d-153">OutVariable</span><span class="sxs-lookup"><span data-stu-id="4cc5d-153">OutVariable</span></span>
- <span data-ttu-id="4cc5d-154">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="4cc5d-154">PipelineVariable</span></span>
- <span data-ttu-id="4cc5d-155">자세히</span><span class="sxs-lookup"><span data-stu-id="4cc5d-155">Verbose</span></span>
- <span data-ttu-id="4cc5d-156">WarningAction</span><span class="sxs-lookup"><span data-stu-id="4cc5d-156">WarningAction</span></span>
- <span data-ttu-id="4cc5d-157">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="4cc5d-157">WarningVariable</span></span>

<span data-ttu-id="4cc5d-158">자세한 내용은 PowerShell 설명서의 [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="4cc5d-158">For details, refer to [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in the PowerShell documentation.</span></span>
