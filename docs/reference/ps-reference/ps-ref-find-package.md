---
title: NuGet Find-Package PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 Find-Package PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 267dd3eb501cae6e419386a5ca5e0c1ab659f807
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238090"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="20778-103">Find-Package (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="20778-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="20778-104">*버전 3.0 이상; 이 항목에서는 Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내의 명령을 설명 합니다. 일반 PowerShell Find-Package 명령의 경우 [Powershell PackageManagement 참조](/powershell/module/packagemanagement/?view=powershell-6)를 참조 하세요.*</span><span class="sxs-lookup"><span data-stu-id="20778-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="20778-105">패키지 원본에서 지정 된 ID 또는 키워드를 사용 하 여 원격 패키지 집합을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="20778-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="20778-106">구문</span><span class="sxs-lookup"><span data-stu-id="20778-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="20778-107">매개 변수</span><span class="sxs-lookup"><span data-stu-id="20778-107">Parameters</span></span>

| <span data-ttu-id="20778-108">매개 변수</span><span class="sxs-lookup"><span data-stu-id="20778-108">Parameter</span></span> | <span data-ttu-id="20778-109">Description</span><span class="sxs-lookup"><span data-stu-id="20778-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="20778-110">Id &lt; 키워드&gt;</span><span class="sxs-lookup"><span data-stu-id="20778-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="20778-111">하다 패키지 소스를 검색할 때 사용할 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="20778-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="20778-112">패키지 ID가 키워드와 일치 하는 패키지만 반환 하려면-ExactMatch을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="20778-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="20778-113">키워드를 지정 하지 않으면에서 `Find-Package` 다운로드 하 여 상위 20 개 패키지의 목록을 반환 하거나,-First로 지정 된 숫자를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="20778-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="20778-114">-Id는 선택 사항이 며 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="20778-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="20778-115">원본</span><span class="sxs-lookup"><span data-stu-id="20778-115">Source</span></span> | <span data-ttu-id="20778-116">검색할 패키지 원본에 대 한 URL 또는 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="20778-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="20778-117">로컬 폴더 경로는 절대 경로 이거나 현재 폴더에 대 한 상대 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20778-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="20778-118">생략 하면 `Find-Package` 현재 선택 된 패키지 소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="20778-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="20778-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="20778-119">AllVersions</span></span> | <span data-ttu-id="20778-120">최신 버전 뿐 아니라 각 패키지의 사용 가능한 모든 버전을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="20778-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="20778-121">첫째</span><span class="sxs-lookup"><span data-stu-id="20778-121">First</span></span> | <span data-ttu-id="20778-122">목록의 처음부터 반환할 패키지 수입니다. 기본값은 20입니다.</span><span class="sxs-lookup"><span data-stu-id="20778-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="20778-123">건너뛰기</span><span class="sxs-lookup"><span data-stu-id="20778-123">Skip</span></span> | <span data-ttu-id="20778-124">&lt; &gt; 표시 된 목록에서 첫 번째 int 패키지를 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="20778-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="20778-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="20778-125">IncludePrerelease</span></span> | <span data-ttu-id="20778-126">결과에 시험판 패키지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="20778-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="20778-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="20778-127">ExactMatch</span></span> | <span data-ttu-id="20778-128">&lt; &gt; 대/소문자를 구분 하는 패키지 ID로 키워드를 사용 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="20778-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="20778-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="20778-129">StartWith</span></span> | <span data-ttu-id="20778-130">패키지 ID가 키워드로 시작 하는 패키지를 반환 &lt; &gt; 합니다.</span><span class="sxs-lookup"><span data-stu-id="20778-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="20778-131">이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="20778-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="20778-132">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="20778-132">Common Parameters</span></span>

<span data-ttu-id="20778-133">`Find-Package` 에서는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](/powershell/module/microsoft.powershell.core/about/about_commonparameters)를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="20778-133">`Find-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="20778-134">예</span><span class="sxs-lookup"><span data-stu-id="20778-134">Examples</span></span>

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