---
title: "NuGet Uninstall-package PowerShell 참조 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: f4f5dc79-8e8e-4012-8986-873a5d9283d9
description: "Visual Studio에서 NuGet 패키지 관리자 콘솔의 제거 패키지 PowerShell 명령에 대 한 참조입니다."
keywords: "NuGet 패키지 관리자 콘솔, NuGet Powershell 명령 제거 패키지 NuGet Powershell 참조"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 679e89e9cfb16dbe484f133b0b6431313b9d87ac
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="84018-104">(Visual Studio에서 패키지 관리자 콘솔) Uninstall-package</span><span class="sxs-lookup"><span data-stu-id="84018-104">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="84018-105">*이 항목에서는 내에서 명령을 설명에서 [NuGet 패키지 관리자 콘솔](Package-Manager-Console.md) Windows에서 Visual Studio에서 합니다. 일반 PowerShell Uninstall-package 명령에 대 한 참조는 [PowerShell PackageManagement 참조](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6)합니다.*</span><span class="sxs-lookup"><span data-stu-id="84018-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="84018-106">필요에 따라 해당 종속성을 제거 하는 프로젝트에서 패키지를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="84018-106">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="84018-107">하지 않으면 명령이 실패 합니다 다른 패키지가이 패키지에 종속 되어, 하는 경우 – Force 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="84018-107">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="84018-108">구문</span><span class="sxs-lookup"><span data-stu-id="84018-108">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="84018-109">하지 않으면 명령이 실패 합니다 다른 패키지가이 패키지에 종속 되어, 하는 경우 – Force 옵션을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="84018-109">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="84018-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="84018-110">Parameters</span></span>

| <span data-ttu-id="84018-111">매개 변수</span><span class="sxs-lookup"><span data-stu-id="84018-111">Parameter</span></span> | <span data-ttu-id="84018-112">설명</span><span class="sxs-lookup"><span data-stu-id="84018-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="84018-113">ID</span><span class="sxs-lookup"><span data-stu-id="84018-113">Id</span></span> | <span data-ttu-id="84018-114">(필수) 제거할 패키지의 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="84018-114">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="84018-115">-Id 스위치 자체는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="84018-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="84018-116">버전</span><span class="sxs-lookup"><span data-stu-id="84018-116">Version</span></span> | <span data-ttu-id="84018-117">버전을 제거 하려면 패키지의 현재 설치 된 버전을 기본값으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84018-117">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="84018-118">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="84018-118">RemoveDependencies</span></span> | <span data-ttu-id="84018-119">패키지와 그 사용 하지 않는 종속성을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="84018-119">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="84018-120">즉, 모든 종속성에 의존 하는 다른 패키지,이 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="84018-120">That is, if any dependency has another package that depends on it, it is skipped.</span></span> |
| <span data-ttu-id="84018-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="84018-121">ProjectName</span></span> | <span data-ttu-id="84018-122">기본 프로젝트에 기본값으로 설정 하 고 패키지를 제거할 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="84018-122">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="84018-123">강제</span><span class="sxs-lookup"><span data-stu-id="84018-123">Force</span></span> | <span data-ttu-id="84018-124">다른 패키지가 종속 되어 있는 경우에를 제거 해야 패키지를 강제로 합니다.</span><span class="sxs-lookup"><span data-stu-id="84018-124">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="84018-125">WhatIf</span><span class="sxs-lookup"><span data-stu-id="84018-125">WhatIf</span></span> | <span data-ttu-id="84018-126">실제로 제거를 수행 하지 않고 명령을 실행할 때 어떻게 되는지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="84018-126">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="84018-127">매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="84018-127">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="84018-128">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="84018-128">Common Parameters</span></span>

<span data-ttu-id="84018-129">`Uninstall-Package`다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.</span><span class="sxs-lookup"><span data-stu-id="84018-129">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="84018-130">예제</span><span class="sxs-lookup"><span data-stu-id="84018-130">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
