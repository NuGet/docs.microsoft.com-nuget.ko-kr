---
title: NuGet Find-package PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 Find-package PowerShell 명령에 대 한 참조입니다.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 0faf5c5cf9ae99105e3d76a4f5e37f164c4f4ff3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="3fe4b-103">Find-Package (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="3fe4b-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="3fe4b-104">*버전 3.0 +; 이 항목에서는 내에서 명령을 설명에서 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows에서 Visual Studio에서 합니다. 일반 PowerShell Find-package 명령에 대 한 참조는 [PowerShell PackageManagement 참조](/powershell/module/packagemanagement/?view=powershell-6)합니다.*</span><span class="sxs-lookup"><span data-stu-id="3fe4b-104">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="3fe4b-105">패키지 소스에서 지정 된 ID 또는 키워드를 사용 하 여 원격 패키지 세트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="3fe4b-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="3fe4b-106">구문</span><span class="sxs-lookup"><span data-stu-id="3fe4b-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="3fe4b-107">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3fe4b-107">Parameters</span></span>

| <span data-ttu-id="3fe4b-108">매개 변수</span><span class="sxs-lookup"><span data-stu-id="3fe4b-108">Parameter</span></span> | <span data-ttu-id="3fe4b-109">설명</span><span class="sxs-lookup"><span data-stu-id="3fe4b-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3fe4b-110">Id &lt;키워드&gt;</span><span class="sxs-lookup"><span data-stu-id="3fe4b-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="3fe4b-111">(필수) 패키지 소스를 검색할 때 사용 하는 키워드입니다.</span><span class="sxs-lookup"><span data-stu-id="3fe4b-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="3fe4b-112">ExactMatch-를 사용 하 여 패키지 ID를 가진 키워드와 일치 하는 패키지에만 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fe4b-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="3fe4b-113">키워드가 없습니다 제공 `Find-Package` 먼저-지정한 수 또는 다운로드 하 여 상위 20 패키지 목록을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fe4b-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="3fe4b-114">Id는 선택 사항입니다-및 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3fe4b-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="3fe4b-115">소스</span><span class="sxs-lookup"><span data-stu-id="3fe4b-115">Source</span></span> | <span data-ttu-id="3fe4b-116">검색 하기 위해 패키지 원본에 대 한 URL 또는 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="3fe4b-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="3fe4b-117">로컬 폴더 경로는 현재 폴더에 상대적 이거나 절대 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fe4b-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="3fe4b-118">생략 하면 `Find-Package` 현재 선택된 된 패키지 소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fe4b-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="3fe4b-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="3fe4b-119">AllVersions</span></span> | <span data-ttu-id="3fe4b-120">최신 버전만 대신 각 패키지의 사용 가능한 모든 버전을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3fe4b-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="3fe4b-121">First</span><span class="sxs-lookup"><span data-stu-id="3fe4b-121">First</span></span> | <span data-ttu-id="3fe4b-122">목록 시작 부분부터 반환할 패키지 수 기본값은 20입니다.</span><span class="sxs-lookup"><span data-stu-id="3fe4b-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="3fe4b-123">Skip</span><span class="sxs-lookup"><span data-stu-id="3fe4b-123">Skip</span></span> | <span data-ttu-id="3fe4b-124">첫 번째 생략 &lt;int&gt; 표시 된 목록에서 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fe4b-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="3fe4b-125">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="3fe4b-125">IncludePrerelease</span></span> | <span data-ttu-id="3fe4b-126">결과에 시험판 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3fe4b-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="3fe4b-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="3fe4b-127">ExactMatch</span></span> | <span data-ttu-id="3fe4b-128">사용 하도록 지정한 &lt;키워드&gt; 으로 대/소문자 구분 패키지 id입니다.</span><span class="sxs-lookup"><span data-stu-id="3fe4b-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="3fe4b-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="3fe4b-129">StartWith</span></span> | <span data-ttu-id="3fe4b-130">반환 된 패키지 ID로 시작 패키지 &lt;키워드&gt;합니다.</span><span class="sxs-lookup"><span data-stu-id="3fe4b-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="3fe4b-131">매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3fe4b-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="3fe4b-132">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="3fe4b-132">Common Parameters</span></span>

<span data-ttu-id="3fe4b-133">`Find-Package` 다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.</span><span class="sxs-lookup"><span data-stu-id="3fe4b-133">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="3fe4b-134">예제</span><span class="sxs-lookup"><span data-stu-id="3fe4b-134">Examples</span></span>

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
