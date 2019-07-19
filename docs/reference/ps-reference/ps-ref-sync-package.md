---
title: NuGet 동기화-패키지 PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 동기화 패키지 PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a48a09a27b6db9b774e59b9a10652067179e2c27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327310"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="fcef3-103">Sync-Package (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="fcef3-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="fcef3-104">*버전 3.0 이상; Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내 에서만 사용할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="fcef3-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="fcef3-105">지정 된 (또는 기본) 프로젝트에서 설치 된 패키지의 버전을 가져오고 솔루션의 나머지 프로젝트와 버전을 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcef3-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="fcef3-106">구문</span><span class="sxs-lookup"><span data-stu-id="fcef3-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="fcef3-107">매개 변수</span><span class="sxs-lookup"><span data-stu-id="fcef3-107">Parameters</span></span>

| <span data-ttu-id="fcef3-108">매개 변수</span><span class="sxs-lookup"><span data-stu-id="fcef3-108">Parameter</span></span> | <span data-ttu-id="fcef3-109">Description</span><span class="sxs-lookup"><span data-stu-id="fcef3-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fcef3-110">ID</span><span class="sxs-lookup"><span data-stu-id="fcef3-110">Id</span></span> | <span data-ttu-id="fcef3-111">하다 동기화 할 패키지의 식별자입니다. -Id 스위치 자체는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="fcef3-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="fcef3-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="fcef3-112">IgnoreDependencies</span></span> | <span data-ttu-id="fcef3-113">해당 종속성이 아닌이 패키지만 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcef3-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="fcef3-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="fcef3-114">ProjectName</span></span> | <span data-ttu-id="fcef3-115">패키지를 동기화 할 프로젝트입니다. 기본값은 기본 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="fcef3-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="fcef3-116">버전</span><span class="sxs-lookup"><span data-stu-id="fcef3-116">Version</span></span> | <span data-ttu-id="fcef3-117">동기화 할 패키지의 버전으로, 현재 설치 된 버전을 기본값으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcef3-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="fcef3-118">Source</span><span class="sxs-lookup"><span data-stu-id="fcef3-118">Source</span></span> | <span data-ttu-id="fcef3-119">검색할 패키지 원본에 대 한 URL 또는 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="fcef3-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="fcef3-120">로컬 폴더 경로는 절대 경로 이거나 현재 폴더에 대 한 상대 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcef3-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="fcef3-121">생략 하면 현재 `Sync-Package` 선택 된 패키지 소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcef3-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="fcef3-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="fcef3-122">IncludePrerelease</span></span> | <span data-ttu-id="fcef3-123">동기화에 시험판 패키지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="fcef3-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="fcef3-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="fcef3-124">FileConflictAction</span></span> | <span data-ttu-id="fcef3-125">프로젝트에서 참조 하는 기존 파일을 덮어쓰거나 무시 하도록 요청 된 경우 수행할 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="fcef3-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="fcef3-126">가능한 값은 *Overwrite, Ignore, None, OverwriteAll*및 *(3.0 +)* *ignoreall*입니다.</span><span class="sxs-lookup"><span data-stu-id="fcef3-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="fcef3-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="fcef3-127">DependencyVersion</span></span> | <span data-ttu-id="fcef3-128">사용할 종속성 패키지의 버전은 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fcef3-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="fcef3-129">*최저* (기본값): 가장 낮은 버전</span><span class="sxs-lookup"><span data-stu-id="fcef3-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="fcef3-130">*HighestPatch*: 최하위 주, 최저 부, 최고 패치가 있는 버전</span><span class="sxs-lookup"><span data-stu-id="fcef3-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="fcef3-131">*HighestMinor*: 최하위 주, 가장 높은 부, 최고 패치가 있는 버전</span><span class="sxs-lookup"><span data-stu-id="fcef3-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="fcef3-132">*가장 높음* (매개 변수가 없는 업데이트-패키지의 기본값): 가장 높은 버전</span><span class="sxs-lookup"><span data-stu-id="fcef3-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="fcef3-133">파일의 [설정을`dependencyVersion`](../nuget-config-file.md#config-section) 사용 하 여 기본값을 설정할 수 있습니다. `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="fcef3-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="fcef3-134">Whatif</span><span class="sxs-lookup"><span data-stu-id="fcef3-134">WhatIf</span></span> | <span data-ttu-id="fcef3-135">실제로 동기화를 수행 하지 않고 명령을 실행할 때 발생 하는 상황을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fcef3-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="fcef3-136">이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="fcef3-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="fcef3-137">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="fcef3-137">Common Parameters</span></span>

<span data-ttu-id="fcef3-138">`Sync-Package`는 다음과 같은 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216)를 지원 합니다. 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable입니다.</span><span class="sxs-lookup"><span data-stu-id="fcef3-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="fcef3-139">예</span><span class="sxs-lookup"><span data-stu-id="fcef3-139">Examples</span></span>

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
