---
title: NuGet Uninstall-package PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔의 제거 패키지 PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 860a58c359c9b723564a70f83aee4eee5cebf16d
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818869"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="781de-103">Uninstall-Package (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="781de-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="781de-104">*이 항목에서는 내에서 명령을 설명에서 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows에서 Visual Studio에서 합니다. 일반 PowerShell Uninstall-package 명령에 대 한 참조는 [PowerShell PackageManagement 참조](/powershell/module/packagemanagement/?view=powershell-6)합니다.*</span><span class="sxs-lookup"><span data-stu-id="781de-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="781de-105">필요에 따라 해당 종속성을 제거 하는 프로젝트에서 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="781de-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="781de-106">하지 않으면 명령이 실패 합니다 다른 패키지가이 패키지에 종속 되어, 하는 경우 – Force 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="781de-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="781de-107">구문</span><span class="sxs-lookup"><span data-stu-id="781de-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="781de-108">하지 않으면 명령이 실패 합니다 다른 패키지가이 패키지에 종속 되어, 하는 경우 – Force 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="781de-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="781de-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="781de-109">Parameters</span></span>

| <span data-ttu-id="781de-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="781de-110">Parameter</span></span> | <span data-ttu-id="781de-111">설명</span><span class="sxs-lookup"><span data-stu-id="781de-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="781de-112">ID</span><span class="sxs-lookup"><span data-stu-id="781de-112">Id</span></span> | <span data-ttu-id="781de-113">(필수) 제거할 패키지의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="781de-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="781de-114">-Id 스위치 자체는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="781de-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="781de-115">버전</span><span class="sxs-lookup"><span data-stu-id="781de-115">Version</span></span> | <span data-ttu-id="781de-116">버전을 제거 하려면 패키지의 현재 설치 된 버전을 기본값으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="781de-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="781de-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="781de-117">RemoveDependencies</span></span> | <span data-ttu-id="781de-118">패키지와 그 사용 하지 않는 종속성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="781de-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="781de-119">즉, 모든 종속성에 의존 하는 다른 패키지,이 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="781de-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="781de-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="781de-120">ProjectName</span></span> | <span data-ttu-id="781de-121">기본 프로젝트에 기본값으로 설정 하 고 패키지를 제거할 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="781de-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="781de-122">강제</span><span class="sxs-lookup"><span data-stu-id="781de-122">Force</span></span> | <span data-ttu-id="781de-123">다른 패키지가 종속 되어 있는 경우에를 제거 해야 패키지를 강제로 합니다.</span><span class="sxs-lookup"><span data-stu-id="781de-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="781de-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="781de-124">WhatIf</span></span> | <span data-ttu-id="781de-125">실제로 제거를 수행 하지 않고 명령을 실행할 때 어떻게 되는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="781de-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="781de-126">매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="781de-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="781de-127">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="781de-127">Common Parameters</span></span>

<span data-ttu-id="781de-128">`Uninstall-Package` 다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.</span><span class="sxs-lookup"><span data-stu-id="781de-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="781de-129">예제</span><span class="sxs-lookup"><span data-stu-id="781de-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
