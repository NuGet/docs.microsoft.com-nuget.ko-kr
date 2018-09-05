---
title: NuGet Uninstall-package PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 Uninstall-package PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ae60473fbb716b23f40b0605be8aaa8515802315
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551645"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="bc40f-103">Uninstall-Package (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="bc40f-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="bc40f-104">*내에서 명령에 설명 합니다 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows의 Visual Studio에서 합니다. 일반 PowerShell Uninstall-package 명령에 대 한 참조를 [PowerShell PackageManagement 참조](/powershell/module/packagemanagement/?view=powershell-6)합니다.*</span><span class="sxs-lookup"><span data-stu-id="bc40f-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="bc40f-105">필요에 따라 해당 종속성을 제거 하는 프로젝트에서 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc40f-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="bc40f-106">하지 않는 한 다른 패키지에이 패키지에 의존 하는 경우 명령이 실패 – Force 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc40f-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="bc40f-107">구문</span><span class="sxs-lookup"><span data-stu-id="bc40f-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="bc40f-108">하지 않는 한 다른 패키지에이 패키지에 의존 하는 경우 명령이 실패 – Force 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc40f-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="bc40f-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="bc40f-109">Parameters</span></span>

| <span data-ttu-id="bc40f-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="bc40f-110">Parameter</span></span> | <span data-ttu-id="bc40f-111">설명</span><span class="sxs-lookup"><span data-stu-id="bc40f-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bc40f-112">ID</span><span class="sxs-lookup"><span data-stu-id="bc40f-112">Id</span></span> | <span data-ttu-id="bc40f-113">(필수) 제거할 패키지의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="bc40f-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="bc40f-114">-Id 자체 스위치는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="bc40f-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="bc40f-115">버전</span><span class="sxs-lookup"><span data-stu-id="bc40f-115">Version</span></span> | <span data-ttu-id="bc40f-116">를 제거 하려면 패키지 버전을 현재 설치 된 버전을 기본값으로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc40f-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="bc40f-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="bc40f-117">RemoveDependencies</span></span> | <span data-ttu-id="bc40f-118">패키지 및 해당 사용 되지 않는 종속성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc40f-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="bc40f-119">즉, 모든 종속성에 종속 된 다른 패키지에 있으면이 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="bc40f-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="bc40f-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="bc40f-120">ProjectName</span></span> | <span data-ttu-id="bc40f-121">기본 프로젝트에 기본적으로 패키지를 제거 하는 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="bc40f-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="bc40f-122">Force</span><span class="sxs-lookup"><span data-stu-id="bc40f-122">Force</span></span> | <span data-ttu-id="bc40f-123">다른 패키지에 의존 하는 경우에 제거할 패키지를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc40f-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="bc40f-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="bc40f-124">WhatIf</span></span> | <span data-ttu-id="bc40f-125">실제로 제거를 수행 하지 않고 명령을 실행할 때 발생할 상황을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bc40f-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="bc40f-126">이러한 매개 변수 중 파이프라인 입력 하거나 와일드 카드 문자 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc40f-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="bc40f-127">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="bc40f-127">Common Parameters</span></span>

<span data-ttu-id="bc40f-128">`Uninstall-Package` 다음을 지원 합니다 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, 자세한 정보 표시, WarningAction, WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="bc40f-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="bc40f-129">예제</span><span class="sxs-lookup"><span data-stu-id="bc40f-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
