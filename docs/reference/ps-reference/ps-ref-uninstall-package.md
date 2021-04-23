---
title: NuGet Uninstall-Package PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 Uninstall-Package PowerShell 명령에 대 한 참조입니다.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 371e95c341efbce1c4a15facefc15cd51b266141
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901787"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="95cab-103">Uninstall-Package (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="95cab-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="95cab-104">*이 항목에서는 Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내의 명령을 설명 합니다. 일반 PowerShell Uninstall-Package 명령의 경우 [Powershell PackageManagement 참조](/powershell/module/packagemanagement)를 참조 하세요.*</span><span class="sxs-lookup"><span data-stu-id="95cab-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="95cab-105">프로젝트에서 패키지를 제거 하 고 필요에 따라 해당 종속성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="95cab-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="95cab-106">이 패키지에 다른 패키지가 종속된 경우 –Force 옵션을 지정하지 않으면 명령이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="95cab-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="95cab-107">구문</span><span class="sxs-lookup"><span data-stu-id="95cab-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="95cab-108">이 패키지에 다른 패키지가 종속된 경우 –Force 옵션을 지정하지 않으면 명령이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="95cab-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="95cab-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="95cab-109">Parameters</span></span>

| <span data-ttu-id="95cab-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="95cab-110">Parameter</span></span> | <span data-ttu-id="95cab-111">설명</span><span class="sxs-lookup"><span data-stu-id="95cab-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="95cab-112">Id</span><span class="sxs-lookup"><span data-stu-id="95cab-112">Id</span></span> | <span data-ttu-id="95cab-113">하다 제거할 패키지의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="95cab-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="95cab-114">-Id 스위치 자체는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="95cab-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="95cab-115">Version</span><span class="sxs-lookup"><span data-stu-id="95cab-115">Version</span></span> | <span data-ttu-id="95cab-116">제거할 패키지의 버전입니다. 기본값은 현재 설치 된 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="95cab-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="95cab-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="95cab-117">RemoveDependencies</span></span> | <span data-ttu-id="95cab-118">패키지와 사용 되지 않는 종속성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="95cab-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="95cab-119">즉, 종속성에 종속 된 다른 패키지가 있는 경우이를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="95cab-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="95cab-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="95cab-120">ProjectName</span></span> | <span data-ttu-id="95cab-121">패키지를 제거할 프로젝트 이며 기본 프로젝트를 기본값으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="95cab-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="95cab-122">Force</span><span class="sxs-lookup"><span data-stu-id="95cab-122">Force</span></span> | <span data-ttu-id="95cab-123">다른 패키지에 종속 된 경우에도 패키지를 강제로 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="95cab-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="95cab-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="95cab-124">WhatIf</span></span> | <span data-ttu-id="95cab-125">실제로 제거를 수행 하지 않고 명령을 실행할 때 발생 하는 상황을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="95cab-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="95cab-126">이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95cab-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="95cab-127">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="95cab-127">Common Parameters</span></span>

<span data-ttu-id="95cab-128">`Uninstall-Package` 에서는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](/powershell/module/microsoft.powershell.core/about/about_commonparameters)를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="95cab-128">`Uninstall-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="95cab-129">예</span><span class="sxs-lookup"><span data-stu-id="95cab-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```