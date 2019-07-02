---
title: NuGet Update-package PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 Update-package PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5b5a11ee11d9e2cf6a90d56ac63b1f7bad750ea
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496488"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="8eaea-103">Update-Package (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="8eaea-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="8eaea-104">*내 에서만 사용 가능 합니다 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows의 Visual Studio에서 합니다.*</span><span class="sxs-lookup"><span data-stu-id="8eaea-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="8eaea-105">최신 버전으로 프로젝트의 모든 패키지 및 해당 종속성 또는 패키지를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="8eaea-106">구문</span><span class="sxs-lookup"><span data-stu-id="8eaea-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="8eaea-107">Nuget 2.8 + `Update-Package` 프로젝트에서 기존 패키지를 다운 그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="8eaea-108">예를 들어 Microsoft.AspNet.MVC 5.1.0-rc1 설치 된 경우 다음 명령을 다운 그레이드 하 고 5.0.0에:</span><span class="sxs-lookup"><span data-stu-id="8eaea-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="8eaea-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8eaea-109">Parameters</span></span>

|  <span data-ttu-id="8eaea-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8eaea-110">Parameter</span></span> | <span data-ttu-id="8eaea-111">설명</span><span class="sxs-lookup"><span data-stu-id="8eaea-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8eaea-112">ID</span><span class="sxs-lookup"><span data-stu-id="8eaea-112">Id</span></span> | <span data-ttu-id="8eaea-113">업데이트 패키지의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-113">The identifier of the package to update.</span></span> <span data-ttu-id="8eaea-114">생략 하면 모든 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-114">If omitted, updates all packages.</span></span> <span data-ttu-id="8eaea-115">-Id 자체 스위치는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="8eaea-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="8eaea-116">IgnoreDependencies</span></span> | <span data-ttu-id="8eaea-117">패키지의 종속성을 업데이트 하는 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="8eaea-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="8eaea-118">ProjectName</span></span> | <span data-ttu-id="8eaea-119">업데이트할 패키지가 포함 된, 모든 프로젝트에 기본적으로 프로젝트의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="8eaea-120">버전</span><span class="sxs-lookup"><span data-stu-id="8eaea-120">Version</span></span> | <span data-ttu-id="8eaea-121">버전 업그레이드를 최신 버전을 기본값으로 사용입니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="8eaea-122">Nuget 3.0 이상에서 버전 값 중 하나 여야 *Lowest, 최고 HighestMinor*, 또는 *HighestPatch* (안전한 간와 같음).</span><span class="sxs-lookup"><span data-stu-id="8eaea-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="8eaea-123">안전 하 게 보호</span><span class="sxs-lookup"><span data-stu-id="8eaea-123">Safe</span></span> | <span data-ttu-id="8eaea-124">현재 설치 된 패키지와 동일한 주 버전과 부 버전을 사용 하 여 전용 버전에 대 한 업그레이드를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="8eaea-125">Source</span><span class="sxs-lookup"><span data-stu-id="8eaea-125">Source</span></span> | <span data-ttu-id="8eaea-126">검색할 패키지 원본에 대 한 URL 또는 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="8eaea-127">로컬 폴더 경로 현재 폴더에 상대적 이거나 절대 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="8eaea-128">생략 하면 `Update-Package` 현재 선택된 된 패키지 소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="8eaea-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="8eaea-129">IncludePrerelease</span></span> | <span data-ttu-id="8eaea-130">업데이트에 대 한 시험판 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="8eaea-131">다시 설치</span><span class="sxs-lookup"><span data-stu-id="8eaea-131">Reinstall</span></span> | <span data-ttu-id="8eaea-132">현재 설치 된 버전을 사용 하 여 Resintalls 패키지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="8eaea-133">[패키지 다시 설치 및 업데이트](../consume-packages/reinstalling-and-updating-packages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8eaea-133">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="8eaea-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="8eaea-134">FileConflictAction</span></span> | <span data-ttu-id="8eaea-135">덮어쓰거나 프로젝트에서 참조 하는 기존 파일을 무시 하 라는 메시지가 표시 되는 경우 수행할 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="8eaea-136">가능한 값은 *덮어쓰기, Ignore, None, OverwriteAll*, 및 *IgnoreAll* (3.0 이상).</span><span class="sxs-lookup"><span data-stu-id="8eaea-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="8eaea-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="8eaea-137">DependencyVersion</span></span> | <span data-ttu-id="8eaea-138">다음 중 하나일 수 있습니다를 사용 하려면 종속성 패키지의 버전:</span><span class="sxs-lookup"><span data-stu-id="8eaea-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="8eaea-139">*가장 낮은* (기본값): 가장 낮은 버전</span><span class="sxs-lookup"><span data-stu-id="8eaea-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="8eaea-140">*HighestPatch*: 가장 낮은 주요, 가장 낮은 부 최고 패치 버전</span><span class="sxs-lookup"><span data-stu-id="8eaea-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="8eaea-141">*HighestMinor*: 가장 낮은 주 버전, 가장 높은 보조, 최고의 패치</span><span class="sxs-lookup"><span data-stu-id="8eaea-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="8eaea-142">*가장 높은* (매개 변수 없이 사용 하 여 업데이트 패키지에 대 한 기본값): 가장 높은 버전</span><span class="sxs-lookup"><span data-stu-id="8eaea-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="8eaea-143">사용 하 여 기본 값을 설정할 수 있습니다 합니다 [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) 에서 설정 된 `Nuget.Config` 파일.</span><span class="sxs-lookup"><span data-stu-id="8eaea-143">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="8eaea-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="8eaea-144">ToHighestPatch</span></span> | <span data-ttu-id="8eaea-145">-안전에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="8eaea-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="8eaea-146">ToHighestMinor</span></span> | <span data-ttu-id="8eaea-147">현재 설치 된 패키지와 동일한 주 버전을 사용 하 여 버전에 업그레이드를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="8eaea-148">Whatif</span><span class="sxs-lookup"><span data-stu-id="8eaea-148">WhatIf</span></span> | <span data-ttu-id="8eaea-149">실제로 업데이트를 수행 하지 않고 명령을 실행할 때 발생할 상황을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="8eaea-150">이러한 매개 변수 중 파이프라인 입력 하거나 와일드 카드 문자 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8eaea-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="8eaea-151">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="8eaea-151">Common Parameters</span></span>

<span data-ttu-id="8eaea-152">`Update-Package` 다음을 지원 합니다 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="8eaea-152">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="8eaea-153">예제</span><span class="sxs-lookup"><span data-stu-id="8eaea-153">Examples</span></span>

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
