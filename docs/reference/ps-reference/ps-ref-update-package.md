---
title: NuGet Update-Package PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 Update-Package PowerShell 명령에 대 한 참조입니다.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 159817e56d978d6432e989d2027907c0d2445222
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777374"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="8272f-103">Update-Package (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="8272f-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="8272f-104">*Windows의 Visual Studio에서 [NuGet 패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내 에서만 사용할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="8272f-104">*Available only within the [NuGet Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="8272f-105">패키지와 해당 종속성 또는 프로젝트의 모든 패키지를 최신 버전으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="8272f-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="8272f-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="8272f-107">NuGet 2.8 +에서를 `Update-Package` 사용 하 여 프로젝트의 기존 패키지를 다운 그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="8272f-108">예를 들어 5.1.0이 설치 되어 있는 경우 다음 명령을 5.0.0로 다운 그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="8272f-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8272f-109">Parameters</span></span>

|  <span data-ttu-id="8272f-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8272f-110">Parameter</span></span> | <span data-ttu-id="8272f-111">Description</span><span class="sxs-lookup"><span data-stu-id="8272f-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8272f-112">Id</span><span class="sxs-lookup"><span data-stu-id="8272f-112">Id</span></span> | <span data-ttu-id="8272f-113">업데이트할 패키지의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-113">The identifier of the package to update.</span></span> <span data-ttu-id="8272f-114">생략 하면 모든 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-114">If omitted, updates all packages.</span></span> <span data-ttu-id="8272f-115">-Id 스위치 자체는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="8272f-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="8272f-116">IgnoreDependencies</span></span> | <span data-ttu-id="8272f-117">패키지 종속성 업데이트를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="8272f-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="8272f-118">ProjectName</span></span> | <span data-ttu-id="8272f-119">업데이트할 패키지를 포함 하는 프로젝트의 이름입니다. 모든 프로젝트를 기본값으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="8272f-120">버전</span><span class="sxs-lookup"><span data-stu-id="8272f-120">Version</span></span> | <span data-ttu-id="8272f-121">업그레이드에 사용할 버전입니다. 기본적으로 최신 버전이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="8272f-122">NuGet 3.0 이상에서 버전 값은 *최하위, 최고, HighestMinor* 또는 *HighestPatch* 중 하나 여야 합니다 (-Safe와 동일).</span><span class="sxs-lookup"><span data-stu-id="8272f-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="8272f-123">Safe</span><span class="sxs-lookup"><span data-stu-id="8272f-123">Safe</span></span> | <span data-ttu-id="8272f-124">현재 설치 된 패키지와 주 버전과 부 버전이 동일한 버전 으로만 업그레이드를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="8272f-125">원본</span><span class="sxs-lookup"><span data-stu-id="8272f-125">Source</span></span> | <span data-ttu-id="8272f-126">검색할 패키지 원본에 대 한 URL 또는 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="8272f-127">로컬 폴더 경로는 절대 경로 이거나 현재 폴더에 대 한 상대 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="8272f-128">생략 하면 `Update-Package` 현재 선택 된 패키지 소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="8272f-129">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="8272f-129">IncludePrerelease</span></span> | <span data-ttu-id="8272f-130">업데이트를 위한 시험판 패키지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="8272f-131">다시 설치</span><span class="sxs-lookup"><span data-stu-id="8272f-131">Reinstall</span></span> | <span data-ttu-id="8272f-132">현재 설치 된 버전을 사용 하 여 패키지를 Resintalls 합니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="8272f-133">[패키지 다시 설치 및 업데이트를](../../consume-packages/reinstalling-and-updating-packages.md)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="8272f-133">See [Reinstalling and updating packages](../../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="8272f-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="8272f-134">FileConflictAction</span></span> | <span data-ttu-id="8272f-135">프로젝트에서 참조 하는 기존 파일을 덮어쓰거나 무시 하도록 요청 된 경우 수행할 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="8272f-136">가능한 값은 *Overwrite, Ignore, None, OverwriteAll* 및 *ignoreall* (3.0 +)입니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="8272f-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="8272f-137">DependencyVersion</span></span> | <span data-ttu-id="8272f-138">사용할 종속성 패키지의 버전은 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="8272f-139">*가장 낮음* (기본값): 가장 낮은 버전</span><span class="sxs-lookup"><span data-stu-id="8272f-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="8272f-140">*HighestPatch*: 최하위 주, 최저 부, 최고 패치가 있는 버전</span><span class="sxs-lookup"><span data-stu-id="8272f-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="8272f-141">*HighestMinor*: 최하위 주, 가장 높은 부, 최고 패치가 있는 버전</span><span class="sxs-lookup"><span data-stu-id="8272f-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="8272f-142">*가장 높음* (매개 변수가 없는 Update-Package에 대 한 기본값): 가장 높은 버전</span><span class="sxs-lookup"><span data-stu-id="8272f-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="8272f-143">파일의 설정을 사용 하 여 기본값을 설정할 수 있습니다 [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="8272f-143">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="8272f-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="8272f-144">ToHighestPatch</span></span> | <span data-ttu-id="8272f-145">-Safe와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="8272f-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="8272f-146">ToHighestMinor</span></span> | <span data-ttu-id="8272f-147">업그레이드를 현재 설치 된 패키지와 동일한 주 버전의 버전 으로만 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="8272f-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="8272f-148">WhatIf</span></span> | <span data-ttu-id="8272f-149">실제로 업데이트를 수행 하지 않고 명령을 실행할 때 발생 하는 상황을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="8272f-150">이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="8272f-151">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="8272f-151">Common Parameters</span></span>

<span data-ttu-id="8272f-152">`Update-Package` 에서는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](/powershell/module/microsoft.powershell.core/about/about_commonparameters)를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="8272f-152">`Update-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="8272f-153">예</span><span class="sxs-lookup"><span data-stu-id="8272f-153">Examples</span></span>

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
Update-Package Elmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package Elmah –reinstall -ignoreDependencies
```
