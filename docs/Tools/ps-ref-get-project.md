---
title: "NuGet Get 프로젝트 PowerShell 참조 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio에서 NuGet 패키지 관리자 콘솔에서 GetProject PowerShell 명령에 대 한 참조입니다."
keywords: "NuGet 패키지 관리자 콘솔, NuGet Powershell 명령 가져오기 프로젝트 NuGet Powershell 참조"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c347a6104d89bb29626ad7c2f33bec150eb38cd2
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="e8925-104">Get-프로젝트 (Visual Studio에서 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="e8925-104">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e8925-105">*내 에서만 사용할 수는 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows에서 Visual Studio에서 합니다.*</span><span class="sxs-lookup"><span data-stu-id="e8925-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e8925-106">기본 또는 지정 된 프로젝트에 대 한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e8925-106">Displays information about the default or specified project.</span></span> <span data-ttu-id="e8925-107">`Get-Project` 특히 프로젝트에 대 한 Visual Studio DTE (개발 도구 환경) 개체에 참조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e8925-107">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="e8925-108">구문</span><span class="sxs-lookup"><span data-stu-id="e8925-108">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="e8925-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e8925-109">Parameters</span></span>

| <span data-ttu-id="e8925-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e8925-110">Parameter</span></span> | <span data-ttu-id="e8925-111">설명</span><span class="sxs-lookup"><span data-stu-id="e8925-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e8925-112">name</span><span class="sxs-lookup"><span data-stu-id="e8925-112">Name</span></span> | <span data-ttu-id="e8925-113">패키지 관리자 콘솔에서 선택 된 기본 프로젝트 기본값으로 표시 하려면 프로젝트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8925-113">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="e8925-114">-Name 스위치는 선택 사항 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="e8925-114">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="e8925-115">모두</span><span class="sxs-lookup"><span data-stu-id="e8925-115">All</span></span> | <span data-ttu-id="e8925-116">솔루션;의 모든 프로젝트에 대 한 정보를 표시합니다. 프로젝트의 순서는 결정적입니다.</span><span class="sxs-lookup"><span data-stu-id="e8925-116">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="e8925-117">매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8925-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e8925-118">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="e8925-118">Common Parameters</span></span>

<span data-ttu-id="e8925-119">`Get-Project` 다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8925-119">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e8925-120">예제</span><span class="sxs-lookup"><span data-stu-id="e8925-120">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```