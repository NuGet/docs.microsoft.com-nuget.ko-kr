---
title: NuGet Get-프로젝트 PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 GetProject PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 2ceb1557eafd213c148d3ab870925ef5bbbee145
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842277"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="97725-103">Get-Project (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="97725-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="97725-104">*내 에서만 사용 가능 합니다 [패키지 관리자 콘솔](package-manager-console.md) Windows의 Visual Studio에서 합니다.*</span><span class="sxs-lookup"><span data-stu-id="97725-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="97725-105">기본 또는 지정 된 프로젝트에 대 한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="97725-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="97725-106">`Get-Project` 특히 프로젝트에 대 한 Visual Studio DTE (Development Tools Environment) 개체 참조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="97725-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="97725-107">구문</span><span class="sxs-lookup"><span data-stu-id="97725-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="97725-108">매개 변수</span><span class="sxs-lookup"><span data-stu-id="97725-108">Parameters</span></span>

| <span data-ttu-id="97725-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="97725-109">Parameter</span></span> | <span data-ttu-id="97725-110">Description</span><span class="sxs-lookup"><span data-stu-id="97725-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="97725-111">이름</span><span class="sxs-lookup"><span data-stu-id="97725-111">Name</span></span> | <span data-ttu-id="97725-112">패키지 관리자 콘솔에서 선택 된 기본 프로젝트가 기본적으로 표시할 프로젝트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="97725-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="97725-113">-Name 자체 선택적 스위치입니다.</span><span class="sxs-lookup"><span data-stu-id="97725-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="97725-114">모두</span><span class="sxs-lookup"><span data-stu-id="97725-114">All</span></span> | <span data-ttu-id="97725-115">모든 프로젝트를 솔루션에 대 한 정보를 표시 프로젝트의 순서가 결정적입니다.</span><span class="sxs-lookup"><span data-stu-id="97725-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="97725-116">이러한 매개 변수 중 파이프라인 입력 하거나 와일드 카드 문자 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="97725-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="97725-117">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="97725-117">Common Parameters</span></span>

<span data-ttu-id="97725-118">`Get-Project` 다음을 지원 합니다 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="97725-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="97725-119">예</span><span class="sxs-lookup"><span data-stu-id="97725-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```