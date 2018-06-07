---
title: NuGet 업데이트 패키지 PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에 업데이트 패키지 PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: aa039f3ffcc0a7323178dae846733559c0f689b5
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817101"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="5720e-103">Update-Package (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="5720e-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="5720e-104">*내 에서만 사용할 수는 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows에서 Visual Studio에서 합니다.*</span><span class="sxs-lookup"><span data-stu-id="5720e-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="5720e-105">패키지 및 해당 종속 항목 또는 프로젝트에서 모든 패키지를 최신 버전으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="5720e-106">구문</span><span class="sxs-lookup"><span data-stu-id="5720e-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="5720e-107">NuGet 2.8 +에서 `Update-Package` 는 프로젝트에서 기존 패키지를 다운 그레이드 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="5720e-108">예를 들어 Microsoft.AspNet.MVC 5.1.0-rc1 설치 되어 있는 경우 다음 명령을에 다운 그레이드 5.0.0에:</span><span class="sxs-lookup"><span data-stu-id="5720e-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="5720e-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5720e-109">Parameters</span></span>

|  <span data-ttu-id="5720e-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5720e-110">Parameter</span></span> | <span data-ttu-id="5720e-111">설명</span><span class="sxs-lookup"><span data-stu-id="5720e-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5720e-112">ID</span><span class="sxs-lookup"><span data-stu-id="5720e-112">Id</span></span> | <span data-ttu-id="5720e-113">업데이트할 패키지의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-113">The identifier of the package to update.</span></span> <span data-ttu-id="5720e-114">생략 하면 모든 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-114">If omitted, updates all packages.</span></span> <span data-ttu-id="5720e-115">-Id 스위치 자체는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="5720e-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="5720e-116">IgnoreDependencies</span></span> | <span data-ttu-id="5720e-117">업데이트 패키지의 종속성을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="5720e-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="5720e-118">ProjectName</span></span> | <span data-ttu-id="5720e-119">업데이트할 패키지가 포함 된, 모든 프로젝트를 프로젝트의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="5720e-120">버전</span><span class="sxs-lookup"><span data-stu-id="5720e-120">Version</span></span> | <span data-ttu-id="5720e-121">를 업그레이드 하는 최신 버전으로 기본 설정에 사용할 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="5720e-122">NuGet 3.0 +에서 버전 값 중 하나 여야 합니다 *Lowest, 최고, HighestMinor*, 또는 *HighestPatch* (에서-Safe와 동일).</span><span class="sxs-lookup"><span data-stu-id="5720e-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="5720e-123">안전</span><span class="sxs-lookup"><span data-stu-id="5720e-123">Safe</span></span> | <span data-ttu-id="5720e-124">유일한 버전 현재 설치 된 패키지와 같은 주 / 부 버전으로 업그레이드를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="5720e-125">소스</span><span class="sxs-lookup"><span data-stu-id="5720e-125">Source</span></span> | <span data-ttu-id="5720e-126">검색 하기 위해 패키지 원본에 대 한 URL 또는 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="5720e-127">로컬 폴더 경로는 현재 폴더에 상대적 이거나 절대 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="5720e-128">생략 하면 `Update-Package` 현재 선택된 된 패키지 소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="5720e-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="5720e-129">IncludePrerelease</span></span> | <span data-ttu-id="5720e-130">업데이트에 대 한 시험판 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="5720e-131">다시 설치</span><span class="sxs-lookup"><span data-stu-id="5720e-131">Reinstall</span></span> | <span data-ttu-id="5720e-132">현재 설치 된 버전을 사용 하 여 Resintalls 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="5720e-133">[패키지 다시 설치 및 업데이트](../consume-packages/reinstalling-and-updating-packages.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5720e-133">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="5720e-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="5720e-134">FileConflictAction</span></span> | <span data-ttu-id="5720e-135">덮어쓰거나 프로젝트에서 참조 하는 기존 파일을 무시 하도록 요청 시 수행할 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="5720e-136">가능한 값은 *덮어쓰기, 건너뛰기, None, OverwriteAll*, 및 *IgnoreAll* (3.0 이상)입니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="5720e-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="5720e-137">DependencyVersion</span></span> | <span data-ttu-id="5720e-138">를 사용 하려면 다음 중 하나일 수 있는 종속성 패키지의 버전:</span><span class="sxs-lookup"><span data-stu-id="5720e-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="5720e-139">*가장 낮은* (기본값): 최하 버전</span><span class="sxs-lookup"><span data-stu-id="5720e-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="5720e-140">*HighestPatch*: 주요 가장 낮은 가장 낮은 부, 최고의 패치가 포함 된 버전</span><span class="sxs-lookup"><span data-stu-id="5720e-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="5720e-141">*HighestMinor*: 가장 낮은 주 버전과, 가장 높은 보조, 최고의 패치</span><span class="sxs-lookup"><span data-stu-id="5720e-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="5720e-142">*가장 높은* (매개 변수 없이 업데이트 패키지에 대 한 기본값): 가장 높은 버전</span><span class="sxs-lookup"><span data-stu-id="5720e-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="5720e-143">사용 하 여 기본 값을 설정할 수 있습니다는 [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) 에서 설정 된 `Nuget.Config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-143">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="5720e-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="5720e-144">ToHighestPatch</span></span> | <span data-ttu-id="5720e-145">현재 설치 된 패키지와 동일한 부 버전으로 버전에 업그레이드를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-145">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="5720e-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="5720e-146">ToHighestMinor</span></span> | <span data-ttu-id="5720e-147">만 버전 현재 설치 된 패키지와 같은 주 버전으로 업그레이드를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="5720e-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="5720e-148">WhatIf</span></span> | <span data-ttu-id="5720e-149">실제로 업데이트를 수행 하지 않고 명령을 실행할 때 어떻게 되는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="5720e-150">매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="5720e-151">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="5720e-151">Common Parameters</span></span>

<span data-ttu-id="5720e-152">`Update-Package` 다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.</span><span class="sxs-lookup"><span data-stu-id="5720e-152">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="5720e-153">예제</span><span class="sxs-lookup"><span data-stu-id="5720e-153">Examples</span></span>

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
