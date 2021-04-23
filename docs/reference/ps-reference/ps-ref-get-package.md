---
title: NuGet Get-Package PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 Get-Package PowerShell 명령에 대 한 참조입니다.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7c91faecaac2967c7a01dd81e72b9097e7bd6cae
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901735"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f40b9-103">Get-Package (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="f40b9-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f40b9-104">*이 항목에서는 Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내의 명령을 설명 합니다. 일반 PowerShell Get-Package 명령의 경우 [Powershell PackageManagement 참조](/powershell/module/packagemanagement)를 참조 하세요.*</span><span class="sxs-lookup"><span data-stu-id="f40b9-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="f40b9-105">로컬 리포지토리에 설치 된 패키지 목록을 검색 하 고-ListAvailable 스위치와 함께 사용 하는 경우 패키지 원본에서 사용할 수 있는 패키지를 나열 하거나-Update 스위치와 함께 사용 하는 경우 사용 가능한 업데이트를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="f40b9-106">구문</span><span class="sxs-lookup"><span data-stu-id="f40b9-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="f40b9-107">매개 변수를 사용 하지 않으면 `Get-Package` 기본 프로젝트에 설치 된 패키지의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="f40b9-108">매개 변수</span><span class="sxs-lookup"><span data-stu-id="f40b9-108">Parameters</span></span>

| <span data-ttu-id="f40b9-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="f40b9-109">Parameter</span></span> | <span data-ttu-id="f40b9-110">Description</span><span class="sxs-lookup"><span data-stu-id="f40b9-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f40b9-111">원본</span><span class="sxs-lookup"><span data-stu-id="f40b9-111">Source</span></span> | <span data-ttu-id="f40b9-112">패키지에 대 한 URL 또는 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-112">The URL or folder path for the package .</span></span> <span data-ttu-id="f40b9-113">로컬 폴더 경로는 절대 경로 이거나 현재 폴더에 대 한 상대 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="f40b9-114">생략 하면 `Get-Package` 현재 선택 된 패키지 소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="f40b9-115">-ListAvailable와 함께 사용 하는 경우 기본값은 nuget.org입니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="f40b9-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="f40b9-116">ListAvailable</span></span> | <span data-ttu-id="f40b9-117">패키지 원본에서 사용할 수 있는 패키지를 나열 하 고 기본적으로 nuget.org를 사용 합니다. -PageSize 및/또는-First가 지정 되지 않은 경우 50 패키지의 기본값을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="f40b9-118">업데이트</span><span class="sxs-lookup"><span data-stu-id="f40b9-118">Updates</span></span> | <span data-ttu-id="f40b9-119">패키지 원본에서 업데이트를 사용할 수 있는 패키지를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="f40b9-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="f40b9-120">ProjectName</span></span> | <span data-ttu-id="f40b9-121">설치 된 패키지를 가져올 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-121">The project from which to get installed packages.</span></span> <span data-ttu-id="f40b9-122">생략 하는 경우 전체 솔루션에 대해 설치 된 프로젝트를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="f40b9-123">Assert</span><span class="sxs-lookup"><span data-stu-id="f40b9-123">Filter</span></span> | <span data-ttu-id="f40b9-124">패키지 ID, 설명 및 태그에 필터를 적용 하 여 패키지 목록의 범위를 좁히는 데 사용 되는 필터 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="f40b9-125">첫째</span><span class="sxs-lookup"><span data-stu-id="f40b9-125">First</span></span> | <span data-ttu-id="f40b9-126">목록의 처음부터 반환할 패키지 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="f40b9-127">지정 하지 않으면 기본값은 50입니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="f40b9-128">건너뛰기</span><span class="sxs-lookup"><span data-stu-id="f40b9-128">Skip</span></span> | <span data-ttu-id="f40b9-129">&lt; &gt; 표시 된 목록에서 첫 번째 int 패키지를 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="f40b9-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="f40b9-130">AllVersions</span></span> | <span data-ttu-id="f40b9-131">최신 버전 뿐 아니라 각 패키지의 사용 가능한 모든 버전을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="f40b9-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="f40b9-132">IncludePrerelease</span></span> | <span data-ttu-id="f40b9-133">결과에 시험판 패키지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="f40b9-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="f40b9-134">PageSize</span></span> | <span data-ttu-id="f40b9-135">*(3.0 이상)* -ListAvailable (필수)와 함께 사용 하는 경우 계속 하 라는 프롬프트를 제공 하기 전에 나열할 패키지의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="f40b9-136">이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f40b9-137">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="f40b9-137">Common Parameters</span></span>

<span data-ttu-id="f40b9-138">`Get-Package` 에서는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](/powershell/module/microsoft.powershell.core/about/about_commonparameters)를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f40b9-138">`Get-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f40b9-139">예</span><span class="sxs-lookup"><span data-stu-id="f40b9-139">Examples</span></span>

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