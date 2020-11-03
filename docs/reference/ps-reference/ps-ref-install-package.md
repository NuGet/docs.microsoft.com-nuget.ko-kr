---
title: NuGet Install-Package PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 Install-Package PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5bda888e0fb526faca79e88da93b0ceb9aff5348
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237207"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="40e58-103">Install-Package (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="40e58-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="40e58-104">*이 항목에서는 Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내의 명령을 설명 합니다. 일반 PowerShell Install-Package 명령의 경우 [Powershell PackageManagement 참조](/powershell/module/packagemanagement/?view=powershell-6)를 참조 하세요.*</span><span class="sxs-lookup"><span data-stu-id="40e58-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="40e58-105">패키지와 해당 종속성을 프로젝트에 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="40e58-106">구문</span><span class="sxs-lookup"><span data-stu-id="40e58-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="40e58-107">NuGet 2.8 +에서는 `Install-Package` 프로젝트의 기존 패키지를 다운 그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="40e58-108">예를 들어 5.1.0이 설치 되어 있는 경우 다음 명령을 5.0.0로 다운 그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="40e58-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="40e58-109">Parameters</span></span>

| <span data-ttu-id="40e58-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="40e58-110">Parameter</span></span> | <span data-ttu-id="40e58-111">Description</span><span class="sxs-lookup"><span data-stu-id="40e58-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="40e58-112">Id</span><span class="sxs-lookup"><span data-stu-id="40e58-112">Id</span></span> | <span data-ttu-id="40e58-113">하다 설치할 패키지의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="40e58-114">( *3.0 이상* ) 식별자는 파일이 나 파일의 경로 또는 URL이 될 수 있습니다 `packages.config` `.nupkg` .</span><span class="sxs-lookup"><span data-stu-id="40e58-114">( *3.0+* ) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="40e58-115">-Id 스위치 자체는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="40e58-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="40e58-116">IgnoreDependencies</span></span> | <span data-ttu-id="40e58-117">해당 종속성이 아닌이 패키지만 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="40e58-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="40e58-118">ProjectName</span></span> | <span data-ttu-id="40e58-119">패키지를 설치할 프로젝트 이며 기본 프로젝트를 기본값으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="40e58-120">원본</span><span class="sxs-lookup"><span data-stu-id="40e58-120">Source</span></span> | <span data-ttu-id="40e58-121">검색할 패키지 원본에 대 한 URL 또는 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="40e58-122">로컬 폴더 경로는 절대 경로 이거나 현재 폴더에 대 한 상대 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="40e58-123">생략 하면 `Install-Package` 현재 선택 된 패키지 소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="40e58-124">버전</span><span class="sxs-lookup"><span data-stu-id="40e58-124">Version</span></span> | <span data-ttu-id="40e58-125">설치할 패키지의 버전입니다. 기본값은 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="40e58-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="40e58-126">IncludePrerelease</span></span> | <span data-ttu-id="40e58-127">설치를 위한 시험판 패키지를 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="40e58-128">이 매개 변수가 생략되면 정식 버전의 패키지만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="40e58-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="40e58-129">FileConflictAction</span></span> | <span data-ttu-id="40e58-130">프로젝트에서 참조 하는 기존 파일을 덮어쓰거나 무시 하도록 요청 된 경우 수행할 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="40e58-131">가능한 값은 *Overwrite, Ignore, None, OverwriteAll* 및 *(3.0 +)* *ignoreall* 입니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-131">Possible values are *Overwrite, Ignore, None, OverwriteAll* , and *(3.0+)* *IgnoreAll* .</span></span> |
| <span data-ttu-id="40e58-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="40e58-132">DependencyVersion</span></span> | <span data-ttu-id="40e58-133">사용할 종속성 패키지의 버전은 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="40e58-134">*가장 낮음* (기본값): 가장 낮은 버전</span><span class="sxs-lookup"><span data-stu-id="40e58-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="40e58-135">*HighestPatch* : 최하위 주, 최저 부, 최고 패치가 있는 버전</span><span class="sxs-lookup"><span data-stu-id="40e58-135">*HighestPatch* : the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="40e58-136">*HighestMinor* : 최하위 주, 가장 높은 부, 최고 패치가 있는 버전</span><span class="sxs-lookup"><span data-stu-id="40e58-136">*HighestMinor* : the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="40e58-137">*가장 높음* (매개 변수가 없는 Update-Package에 대 한 기본값): 가장 높은 버전</span><span class="sxs-lookup"><span data-stu-id="40e58-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="40e58-138">파일의 설정을 사용 하 여 기본값을 설정할 수 있습니다 [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` .</span><span class="sxs-lookup"><span data-stu-id="40e58-138">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="40e58-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="40e58-139">WhatIf</span></span> | <span data-ttu-id="40e58-140">실제로 설치를 수행 하지 않고 명령을 실행할 때 발생 하는 상황을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="40e58-141">이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="40e58-142">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="40e58-142">Common Parameters</span></span>

<span data-ttu-id="40e58-143">`Install-Package` 에서는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](/powershell/module/microsoft.powershell.core/about/about_commonparameters)를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="40e58-143">`Install-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="40e58-144">예</span><span class="sxs-lookup"><span data-stu-id="40e58-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```