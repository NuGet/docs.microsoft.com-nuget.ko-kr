---
title: NuGet Install-package PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 Install-package PowerShell 명령에 대 한 참조입니다.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5adfbcae0affcaa402f7981c12e108490d546511
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="8a005-103">Install-Package (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="8a005-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="8a005-104">*이 항목에서는 내에서 명령을 설명에서 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows에서 Visual Studio에서 합니다. 일반 PowerShell Install-package 명령에 대 한 참조는 [PowerShell PackageManagement 참조](/powershell/module/packagemanagement/?view=powershell-6)합니다.*</span><span class="sxs-lookup"><span data-stu-id="8a005-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="8a005-105">프로젝트에 패키지 및 해당 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="8a005-106">구문</span><span class="sxs-lookup"><span data-stu-id="8a005-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="8a005-107">NuGet 2.8 +에서 `Install-Package` 프로젝트에서 기존 패키지를 다운 그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="8a005-108">예를 들어 Microsoft.AspNet.MVC 5.1.0-rc1 설치 되어 있는 경우 다음 명령을에 다운 그레이드 5.0.0에:</span><span class="sxs-lookup"><span data-stu-id="8a005-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="8a005-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8a005-109">Parameters</span></span>

| <span data-ttu-id="8a005-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="8a005-110">Parameter</span></span> | <span data-ttu-id="8a005-111">설명</span><span class="sxs-lookup"><span data-stu-id="8a005-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8a005-112">ID</span><span class="sxs-lookup"><span data-stu-id="8a005-112">Id</span></span> | <span data-ttu-id="8a005-113">(필수) 설치할 패키지의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="8a005-114">(*3.0 +*) 식별자 경로 또는 URL 일 수 있습니다는 `packages.config` 파일 또는 `.nupkg` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="8a005-115">-Id 스위치 자체는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="8a005-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="8a005-116">IgnoreDependencies</span></span> | <span data-ttu-id="8a005-117">이 패키지만 및 해당 종속성을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="8a005-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="8a005-118">ProjectName</span></span> | <span data-ttu-id="8a005-119">기본 프로젝트를 패키지를 설치 하는 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="8a005-120">소스</span><span class="sxs-lookup"><span data-stu-id="8a005-120">Source</span></span> | <span data-ttu-id="8a005-121">검색 하기 위해 패키지 원본에 대 한 URL 또는 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="8a005-122">로컬 폴더 경로는 현재 폴더에 상대적 이거나 절대 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="8a005-123">생략 하면 `Install-Package` 현재 선택된 된 패키지 소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="8a005-124">버전</span><span class="sxs-lookup"><span data-stu-id="8a005-124">Version</span></span> | <span data-ttu-id="8a005-125">를 설치 하려면 패키지의 버전을 최신 버전을 기본값으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="8a005-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="8a005-126">IncludePrerelease</span></span> | <span data-ttu-id="8a005-127">설치에 시험판 패키지를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="8a005-128">생략 하면 패키지만 고려 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="8a005-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="8a005-129">FileConflictAction</span></span> | <span data-ttu-id="8a005-130">덮어쓰거나 프로젝트에서 참조 하는 기존 파일을 무시 하도록 요청 시 수행할 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="8a005-131">가능한 값은 *덮어쓰기, 건너뛰기, None, OverwriteAll*, 및 *(3.0 이상)* *IgnoreAll*합니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="8a005-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="8a005-132">DependencyVersion</span></span> | <span data-ttu-id="8a005-133">를 사용 하려면 다음 중 하나일 수 있는 종속성 패키지의 버전:</span><span class="sxs-lookup"><span data-stu-id="8a005-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="8a005-134">*가장 낮은* (기본값): 최하 버전</span><span class="sxs-lookup"><span data-stu-id="8a005-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="8a005-135">*HighestPatch*: 주요 가장 낮은 가장 낮은 부, 최고의 패치가 포함 된 버전</span><span class="sxs-lookup"><span data-stu-id="8a005-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="8a005-136">*HighestMinor*: 가장 낮은 주 버전과, 가장 높은 보조, 최고의 패치</span><span class="sxs-lookup"><span data-stu-id="8a005-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="8a005-137">*가장 높은* (매개 변수 없이 업데이트 패키지에 대 한 기본값): 가장 높은 버전</span><span class="sxs-lookup"><span data-stu-id="8a005-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="8a005-138">사용 하 여 기본 값을 설정할 수 있습니다는 [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) 에서 설정 된 `Nuget.Config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-138">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="8a005-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="8a005-139">WhatIf</span></span> | <span data-ttu-id="8a005-140">실제로 설치를 수행 하지 않고 명령을 실행할 때 어떻게 되는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="8a005-141">매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="8a005-142">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="8a005-142">Common Parameters</span></span>

<span data-ttu-id="8a005-143">`Install-Package` 다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.</span><span class="sxs-lookup"><span data-stu-id="8a005-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="8a005-144">예제</span><span class="sxs-lookup"><span data-stu-id="8a005-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
