---
title: "NuGet PowerShell 참조 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/2/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: cd08b869-44c6-480e-90f7-494a6d08e6d0
description: "Visual Studio에서 NuGet 패키지 관리자 콘솔에서 사용할 수 있는 PowerShell 명령에 대 한 전체 참조 합니다."
keywords: "NuGet 패키지 관리자 콘솔에서 NuGet Powershell 명령 NuGet Powershell 참조"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0da5c88447784fdd49d824bbd03b11f73c22ebc
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="powershell-reference"></a><span data-ttu-id="8513a-104">PowerShell 참조</span><span class="sxs-lookup"><span data-stu-id="8513a-104">PowerShell reference</span></span>

<span data-ttu-id="8513a-105">패키지 관리자 콘솔 아래에 나열 된 특정 명령을 통해 NuGet이 포함 된 상호 작용 하는 Windows에서 Visual Studio 내에서 PowerShell 인터페이스를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-105">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="8513a-106">(콘솔은 현재 Mac.에 대 한 Visual Studio에서 제공) 콘솔을 사용 하 여 지침을 참조 하십시오.는 [패키지 관리자 콘솔](../tools/package-manager-console.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-106">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see the [Package Manager Console](../tools/package-manager-console.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="8513a-107">모든 PowerShell 명령 패키지 소비와만 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-107">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="8513a-108">PowerShell 명령을 만들고 하는 패키지는 또한 다른 패키지의 소비자 수를 제외 하 고 패키지를 게시와 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-108">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="8513a-109">여기에 나열 된 명령을 Visual Studio에서 패키지 관리자 콘솔에 관련 된와 다른 지는 [패키지 관리 모듈 명령을](https://msdn.microsoft.com/powershell/reference/6/packagemanagement/packagemanagement) 일반 PowerShell 환경에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-109">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](https://msdn.microsoft.com/powershell/reference/6/packagemanagement/packagemanagement) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="8513a-110">특히 각 환경에는 다른에 사용할 수 없는 명령 및 동일한 이름 가진 명령을 해당 특정 인수에도 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-110">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="8513a-111">패키지 관리 콘솔을 사용 하 여 Visual Studio에서, 명령 및 인수가 있는 항목에 문서화 되어 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-111">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="8513a-112">일반적인 명령</span><span class="sxs-lookup"><span data-stu-id="8513a-112">Common Commands</span></span> | <span data-ttu-id="8513a-113">설명</span><span class="sxs-lookup"><span data-stu-id="8513a-113">Description</span></span> | <span data-ttu-id="8513a-114">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="8513a-114">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="8513a-115">설치 패키지</span><span class="sxs-lookup"><span data-stu-id="8513a-115">Install-Package</span></span>](ps-ref-install-package.md) | <span data-ttu-id="8513a-116">프로젝트에 패키지 및 해당 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-116">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="8513a-117">모두</span><span class="sxs-lookup"><span data-stu-id="8513a-117">All</span></span> |
| [<span data-ttu-id="8513a-118">업데이트 패키지</span><span class="sxs-lookup"><span data-stu-id="8513a-118">Update-Package</span></span>](ps-ref-update-package.md) | <span data-ttu-id="8513a-119">패키지 및 해당 종속 항목 또는 프로젝트의 모든 패키지를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-119">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="8513a-120">모두</span><span class="sxs-lookup"><span data-stu-id="8513a-120">All</span></span> |
| [<span data-ttu-id="8513a-121">패키지 찾기</span><span class="sxs-lookup"><span data-stu-id="8513a-121">Find-Package</span></span>](ps-ref-find-package.md) | <span data-ttu-id="8513a-122">패키지 ID 또는 키워드를 사용 하 여 패키지 소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-122">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="8513a-123">3.0+</span><span class="sxs-lookup"><span data-stu-id="8513a-123">3.0+</span></span> |
| [<span data-ttu-id="8513a-124">패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="8513a-124">Get-Package</span></span>](ps-ref-get-package.md) | <span data-ttu-id="8513a-125">로컬 저장소에 설치 된 패키지 목록을 검색 하거나 패키지 소스에서 사용할 수 있는 패키지를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-125">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="8513a-126">모두</span><span class="sxs-lookup"><span data-stu-id="8513a-126">All</span></span> |

| <span data-ttu-id="8513a-127">보조 명령</span><span class="sxs-lookup"><span data-stu-id="8513a-127">Secondary Commands</span></span> | <span data-ttu-id="8513a-128">설명</span><span class="sxs-lookup"><span data-stu-id="8513a-128">Description</span></span> | <span data-ttu-id="8513a-129">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="8513a-129">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="8513a-130">BindingRedirect 추가</span><span class="sxs-lookup"><span data-stu-id="8513a-130">Add-BindingRedirect</span></span>](ps-ref-add-bindingredirect.md) | <span data-ttu-id="8513a-131">프로젝트에 대 한 출력 경로 내의 모든 어셈블리를 확인 하 고 바인딩 리디렉션을 추가 `app.config` 또는 `web.config` 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-131">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="8513a-132">모두</span><span class="sxs-lookup"><span data-stu-id="8513a-132">All</span></span> |
| [<span data-ttu-id="8513a-133">프로젝트 가져오기</span><span class="sxs-lookup"><span data-stu-id="8513a-133">Get-Project</span></span>](ps-ref-get-project.md) | <span data-ttu-id="8513a-134">기본 또는 지정 된 프로젝트에 대 한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-134">Displays information about the default or specified project.</span></span> | <span data-ttu-id="8513a-135">3.0+</span><span class="sxs-lookup"><span data-stu-id="8513a-135">3.0+</span></span> |
| [<span data-ttu-id="8513a-136">PackagePage 열기</span><span class="sxs-lookup"><span data-stu-id="8513a-136">Open-PackagePage</span></span>](ps-ref-open-packagepage.md) | <span data-ttu-id="8513a-137">프로젝트, 라이선스 또는 지정된 된 패키지에 대 한 보고서 남용 URL을 사용 하 여 기본 브라우저를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-137">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="8513a-138">3.0 이상에서 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-138">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="8513a-139">레지스터 TabExpansion</span><span class="sxs-lookup"><span data-stu-id="8513a-139">Register-TabExpansion</span></span>](ps-ref-register-tabexpansion.md) | <span data-ttu-id="8513a-140">일반적으로 사용 되는 매개 변수 값에 대 한 사용자 지정된 확장을 만들 수 있도록, 명령의 매개 변수에 대해 탭 확장을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-140">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="8513a-141">모두</span><span class="sxs-lookup"><span data-stu-id="8513a-141">All</span></span> |
| [<span data-ttu-id="8513a-142">Sync 패키지</span><span class="sxs-lookup"><span data-stu-id="8513a-142">Sync-Package</span></span>](ps-ref-sync-package.md) | <span data-ttu-id="8513a-143">패키지를 설치 하는 버전은 get 프로젝트를 지정 하 고 버전을 솔루션의 프로젝트의 나머지를 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-143">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="8513a-144">3.0+</span><span class="sxs-lookup"><span data-stu-id="8513a-144">3.0+</span></span> |
| [<span data-ttu-id="8513a-145">패키지 제거</span><span class="sxs-lookup"><span data-stu-id="8513a-145">Uninstall-Package</span></span>](ps-ref-uninstall-package.md) | <span data-ttu-id="8513a-146">필요에 따라 해당 종속성을 제거 하는 프로젝트에서 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-146">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="8513a-147">모두</span><span class="sxs-lookup"><span data-stu-id="8513a-147">All</span></span> |

<span data-ttu-id="8513a-148">콘솔 내에서 이러한 명령 중 하나에서 완전 하 고 자세한 도움말을 방금 문제의 명령 이름으로 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-148">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="8513a-149">다음을 지원 하는 모든 패키지 관리자 콘솔 명령이 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216):</span><span class="sxs-lookup"><span data-stu-id="8513a-149">All Package Manager Console commands support the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216):</span></span>

- <span data-ttu-id="8513a-150">디버그</span><span class="sxs-lookup"><span data-stu-id="8513a-150">Debug</span></span>
- <span data-ttu-id="8513a-151">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="8513a-151">ErrorAction</span></span>
- <span data-ttu-id="8513a-152">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="8513a-152">ErrorVariable</span></span>
- <span data-ttu-id="8513a-153">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="8513a-153">OutBuffer</span></span>
- <span data-ttu-id="8513a-154">Outvariable을 지원</span><span class="sxs-lookup"><span data-stu-id="8513a-154">OutVariable</span></span>
- <span data-ttu-id="8513a-155">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="8513a-155">PipelineVariable</span></span>
- <span data-ttu-id="8513a-156">자세히</span><span class="sxs-lookup"><span data-stu-id="8513a-156">Verbose</span></span>
- <span data-ttu-id="8513a-157">WarningAction</span><span class="sxs-lookup"><span data-stu-id="8513a-157">WarningAction</span></span>
- <span data-ttu-id="8513a-158">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="8513a-158">WarningVariable</span></span>

<span data-ttu-id="8513a-159">자세한 내용은 참조 [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) PowerShell 설명서에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8513a-159">For details, refer to [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in the PowerShell documentation.</span></span>
