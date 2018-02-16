---
title: "NuGet 동기화 패키지 PowerShell 참조 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio에서 NuGet 패키지 관리자 콘솔에서 동기화 패키지 PowerShell 명령에 대 한 참조입니다."
keywords: "NuGet 패키지 관리자 콘솔, NuGet Powershell 명령, Sync 패키지 NuGet Powershell 참조"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8e4b627cff01a353440c47883b98cd93f9edd6cb
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="61993-104">Sync 패키지 (Visual Studio에서 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="61993-104">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="61993-105">*버전 3.0 +; 내 에서만 사용할 수는 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows에서 Visual Studio에서 합니다.*</span><span class="sxs-lookup"><span data-stu-id="61993-105">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="61993-106">프로젝트 하 고 버전을 솔루션의 프로젝트의 나머지를 동기화 하는 지정 된 (또는 기본값)에서 설치 된 패키지의 버전을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="61993-106">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="61993-107">구문</span><span class="sxs-lookup"><span data-stu-id="61993-107">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="61993-108">매개 변수</span><span class="sxs-lookup"><span data-stu-id="61993-108">Parameters</span></span>

| <span data-ttu-id="61993-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="61993-109">Parameter</span></span> | <span data-ttu-id="61993-110">설명</span><span class="sxs-lookup"><span data-stu-id="61993-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="61993-111">ID</span><span class="sxs-lookup"><span data-stu-id="61993-111">Id</span></span> | <span data-ttu-id="61993-112">(필수) 동기화 할 패키지의 식별자입니다. -Id 스위치 자체는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="61993-112">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="61993-113">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="61993-113">IgnoreDependencies</span></span> | <span data-ttu-id="61993-114">이 패키지만 및 해당 종속성을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="61993-114">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="61993-115">ProjectName</span><span class="sxs-lookup"><span data-stu-id="61993-115">ProjectName</span></span> | <span data-ttu-id="61993-116">기본 프로젝트에 기본 설정에서 패키지를 동기화 하는 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="61993-116">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="61993-117">버전</span><span class="sxs-lookup"><span data-stu-id="61993-117">Version</span></span> | <span data-ttu-id="61993-118">동기화 되는 데 패키지의 버전은 현재 설치 된 버전을 기본값으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="61993-118">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="61993-119">소스</span><span class="sxs-lookup"><span data-stu-id="61993-119">Source</span></span> | <span data-ttu-id="61993-120">검색 하기 위해 패키지 원본에 대 한 URL 또는 폴더 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="61993-120">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="61993-121">로컬 폴더 경로는 현재 폴더에 상대적 이거나 절대 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61993-121">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="61993-122">생략 하면 `Sync-Package` 현재 선택된 된 패키지 소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="61993-122">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="61993-123">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="61993-123">IncludePrerelease</span></span> | <span data-ttu-id="61993-124">Sync에 시험판 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="61993-124">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="61993-125">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="61993-125">FileConflictAction</span></span> | <span data-ttu-id="61993-126">덮어쓰거나 프로젝트에서 참조 하는 기존 파일을 무시 하도록 요청 시 수행할 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="61993-126">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="61993-127">가능한 값은 *덮어쓰기, 건너뛰기, None, OverwriteAll*, 및 *(3.0 이상)* *IgnoreAll*합니다.</span><span class="sxs-lookup"><span data-stu-id="61993-127">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="61993-128">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="61993-128">DependencyVersion</span></span> | <span data-ttu-id="61993-129">를 사용 하려면 다음 중 하나일 수 있는 종속성 패키지의 버전:</span><span class="sxs-lookup"><span data-stu-id="61993-129">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="61993-130">*가장 낮은* (기본값): 최하 버전</span><span class="sxs-lookup"><span data-stu-id="61993-130">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="61993-131">*HighestPatch*: 주요 가장 낮은 가장 낮은 부, 최고의 패치가 포함 된 버전</span><span class="sxs-lookup"><span data-stu-id="61993-131">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="61993-132">*HighestMinor*: 가장 낮은 주 버전과, 가장 높은 보조, 최고의 패치</span><span class="sxs-lookup"><span data-stu-id="61993-132">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="61993-133">*가장 높은* (매개 변수 없이 업데이트 패키지에 대 한 기본값): 가장 높은 버전</span><span class="sxs-lookup"><span data-stu-id="61993-133">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="61993-134">사용 하 여 기본 값을 설정할 수 있습니다는 [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) 에서 설정 된 `Nuget.Config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="61993-134">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="61993-135">WhatIf</span><span class="sxs-lookup"><span data-stu-id="61993-135">WhatIf</span></span> | <span data-ttu-id="61993-136">실제로 동기화를 수행 하지 않고 명령을 실행할 때 어떻게 되는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="61993-136">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="61993-137">매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="61993-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="61993-138">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="61993-138">Common Parameters</span></span>

<span data-ttu-id="61993-139">`Sync-Package` 다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.</span><span class="sxs-lookup"><span data-stu-id="61993-139">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="61993-140">예제</span><span class="sxs-lookup"><span data-stu-id="61993-140">Examples</span></span>

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
