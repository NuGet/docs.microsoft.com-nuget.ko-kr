---
title: "NuGet 패키지 가져오기 PowerShell 참조 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio에서 NuGet 패키지 관리자 콘솔에서 패키지 가져오기 PowerShell 명령에 대 한 참조입니다."
keywords: "NuGet 패키지 관리자 콘솔, NuGet Powershell 명령, NuGet Powershell 참조, 패키지 가져오기"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c38e0da2e98d2e5bf5b4fc165462e9abcfdd73c0
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="5ea1b-104">패키지 가져오기 (Visual Studio에서 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="5ea1b-104">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="5ea1b-105">*이 항목에서는 내에서 명령을 설명에서 [NuGet 패키지 관리자 콘솔](Package-Manager-Console.md) Windows에서 Visual Studio에서 합니다. 일반 PowerShell 패키지 가져오기 명령에 대 한 참조는 [PowerShell PackageManagement 참조](/powershell/module/packagemanagement/?view=powershell-6)합니다.*</span><span class="sxs-lookup"><span data-stu-id="5ea1b-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="5ea1b-106">로컬 저장소에 설치 된 패키지 목록을 검색 하 고,-ListAvailable 스위치와 함께 사용 하면 패키지 소스에서 사용할 수 있는 패키지를 나열 또는-업데이트 스위치와 함께 사용할 경우 사용 가능한 업데이트를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-106">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="5ea1b-107">구문</span><span class="sxs-lookup"><span data-stu-id="5ea1b-107">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="5ea1b-108">매개 변수 없이 `Get-Package` 기본 프로젝트에 설치 된 패키지의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-108">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="5ea1b-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5ea1b-109">Parameters</span></span>

| <span data-ttu-id="5ea1b-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5ea1b-110">Parameter</span></span> | <span data-ttu-id="5ea1b-111">설명</span><span class="sxs-lookup"><span data-stu-id="5ea1b-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5ea1b-112">소스</span><span class="sxs-lookup"><span data-stu-id="5ea1b-112">Source</span></span> | <span data-ttu-id="5ea1b-113">패키지에 대 한 URL 또는 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-113">The URL or folder path for the package .</span></span> <span data-ttu-id="5ea1b-114">로컬 폴더 경로는 현재 폴더에 상대적 이거나 절대 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-114">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="5ea1b-115">생략 하면 `Get-Package` 현재 선택된 된 패키지 소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-115">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="5ea1b-116">-ListAvailable를 함께 사용할 때 nuget.org의 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-116">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="5ea1b-117">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="5ea1b-117">ListAvailable</span></span> | <span data-ttu-id="5ea1b-118">Nuget.org를 패키지 소스에서 사용할 수 있는 패키지를 나열 합니다. -PageSize 및/또는-첫 번째는 지정 하지 않으면 기본값은 50 패키지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-118">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="5ea1b-119">Updates</span><span class="sxs-lookup"><span data-stu-id="5ea1b-119">Updates</span></span> | <span data-ttu-id="5ea1b-120">패키지 소스에서 사용 가능한 업데이트가 있는 패키지를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-120">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="5ea1b-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="5ea1b-121">ProjectName</span></span> | <span data-ttu-id="5ea1b-122">설치 된 패키지를 얻을 수 있는 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-122">The project from which to get installed packages.</span></span> <span data-ttu-id="5ea1b-123">생략 하면 전체 솔루션에 프로젝트를 설치 된를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-123">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="5ea1b-124">필터</span><span class="sxs-lookup"><span data-stu-id="5ea1b-124">Filter</span></span> | <span data-ttu-id="5ea1b-125">패키지 ID, 설명 및 태그에 적용 하 여 패키지 목록을 줄이는 데 사용 된 필터 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-125">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="5ea1b-126">First</span><span class="sxs-lookup"><span data-stu-id="5ea1b-126">First</span></span> | <span data-ttu-id="5ea1b-127">목록 시작 부분부터 반환할 패키지 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-127">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="5ea1b-128">지정 하지 않으면 기본값은 50입니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-128">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="5ea1b-129">Skip</span><span class="sxs-lookup"><span data-stu-id="5ea1b-129">Skip</span></span> | <span data-ttu-id="5ea1b-130">첫 번째 생략 &lt;int&gt; 표시 된 목록에서 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-130">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="5ea1b-131">AllVersions</span><span class="sxs-lookup"><span data-stu-id="5ea1b-131">AllVersions</span></span> | <span data-ttu-id="5ea1b-132">최신 버전만 대신 각 패키지의 사용 가능한 모든 버전을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-132">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="5ea1b-133">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="5ea1b-133">IncludePrerelease</span></span> | <span data-ttu-id="5ea1b-134">결과에 시험판 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-134">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="5ea1b-135">PageSize</span><span class="sxs-lookup"><span data-stu-id="5ea1b-135">PageSize</span></span> | <span data-ttu-id="5ea1b-136">*(3.0 +)*  계속할 것인지 묻는 제공 하기 전에 나열 하는 패키지 수가-ListAvailable (필수), 함께 사용 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-136">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="5ea1b-137">매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="5ea1b-138">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="5ea1b-138">Common Parameters</span></span>

<span data-ttu-id="5ea1b-139">`Get-Package`다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea1b-139">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="5ea1b-140">예제</span><span class="sxs-lookup"><span data-stu-id="5ea1b-140">Examples</span></span>

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```
