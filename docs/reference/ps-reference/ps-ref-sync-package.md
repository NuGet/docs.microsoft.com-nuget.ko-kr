---
title: NuGet 동기화-패키지 PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 동기화 패키지 PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 12a3d5f32056539a75da9e17b15d67e72a8a42c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384905"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="84f2c-103">Sync-Package (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="84f2c-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="84f2c-104">*버전 3.0 이상; Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내 에서만 사용할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="84f2c-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="84f2c-105">지정 된 (또는 기본) 프로젝트에서 설치 된 패키지의 버전을 가져오고 솔루션의 나머지 프로젝트와 버전을 동기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="84f2c-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="84f2c-106">구문</span><span class="sxs-lookup"><span data-stu-id="84f2c-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="84f2c-107">매개 변수</span><span class="sxs-lookup"><span data-stu-id="84f2c-107">Parameters</span></span>

| <span data-ttu-id="84f2c-108">매개 변수</span><span class="sxs-lookup"><span data-stu-id="84f2c-108">Parameter</span></span> | <span data-ttu-id="84f2c-109">설명</span><span class="sxs-lookup"><span data-stu-id="84f2c-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="84f2c-110">ID</span><span class="sxs-lookup"><span data-stu-id="84f2c-110">Id</span></span> | <span data-ttu-id="84f2c-111">하다 동기화 할 패키지의 식별자입니다. -Id 스위치 자체는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="84f2c-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="84f2c-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="84f2c-112">IgnoreDependencies</span></span> | <span data-ttu-id="84f2c-113">해당 종속성이 아닌이 패키지만 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="84f2c-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="84f2c-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="84f2c-114">ProjectName</span></span> | <span data-ttu-id="84f2c-115">패키지를 동기화 할 프로젝트입니다. 기본값은 기본 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="84f2c-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="84f2c-116">Version</span><span class="sxs-lookup"><span data-stu-id="84f2c-116">Version</span></span> | <span data-ttu-id="84f2c-117">동기화 할 패키지의 버전으로, 현재 설치 된 버전을 기본값으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="84f2c-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="84f2c-118">소스</span><span class="sxs-lookup"><span data-stu-id="84f2c-118">Source</span></span> | <span data-ttu-id="84f2c-119">검색할 패키지 원본에 대 한 URL 또는 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="84f2c-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="84f2c-120">로컬 폴더 경로는 절대 경로 이거나 현재 폴더에 대 한 상대 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84f2c-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="84f2c-121">생략 하는 경우 `Sync-Package`는 현재 선택 된 패키지 소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="84f2c-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="84f2c-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="84f2c-122">IncludePrerelease</span></span> | <span data-ttu-id="84f2c-123">동기화에 시험판 패키지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="84f2c-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="84f2c-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="84f2c-124">FileConflictAction</span></span> | <span data-ttu-id="84f2c-125">프로젝트에서 참조 하는 기존 파일을 덮어쓰거나 무시 하도록 요청 된 경우 수행할 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="84f2c-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="84f2c-126">가능한 값은 *Overwrite, Ignore, None, OverwriteAll*및 *(3.0 +)* *ignoreall*입니다.</span><span class="sxs-lookup"><span data-stu-id="84f2c-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="84f2c-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="84f2c-127">DependencyVersion</span></span> | <span data-ttu-id="84f2c-128">사용할 종속성 패키지의 버전은 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84f2c-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="84f2c-129">*가장 낮음* (기본값): 가장 낮은 버전</span><span class="sxs-lookup"><span data-stu-id="84f2c-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="84f2c-130">*HighestPatch*: 최하위 주, 최저 부, 최고 패치가 있는 버전</span><span class="sxs-lookup"><span data-stu-id="84f2c-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="84f2c-131">*HighestMinor*: 최하위 주, 가장 높은 부, 최고 패치가 있는 버전</span><span class="sxs-lookup"><span data-stu-id="84f2c-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="84f2c-132">*최상* (매개 변수가 없는 업데이트-패키지의 기본값): 가장 높은 버전</span><span class="sxs-lookup"><span data-stu-id="84f2c-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="84f2c-133">`Nuget.Config` 파일의 [`dependencyVersion`](../nuget-config-file.md#config-section) 설정을 사용 하 여 기본값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84f2c-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="84f2c-134">Whatif</span><span class="sxs-lookup"><span data-stu-id="84f2c-134">WhatIf</span></span> | <span data-ttu-id="84f2c-135">실제로 동기화를 수행 하지 않고 명령을 실행할 때 발생 하는 상황을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="84f2c-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="84f2c-136">이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="84f2c-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="84f2c-137">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="84f2c-137">Common Parameters</span></span>

<span data-ttu-id="84f2c-138">`Sync-Package`는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](https://go.microsoft.com/fwlink/?LinkID=113216)를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="84f2c-138">`Sync-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="84f2c-139">예</span><span class="sxs-lookup"><span data-stu-id="84f2c-139">Examples</span></span>

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
