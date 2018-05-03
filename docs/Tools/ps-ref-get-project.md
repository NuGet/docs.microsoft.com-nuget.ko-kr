---
title: NuGet Get 프로젝트 PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 GetProject PowerShell 명령에 대 한 참조입니다.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a7b66cbf36095e31b5929596300018239749cb15
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="589ba-103">Get-프로젝트 (Visual Studio에서 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="589ba-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="589ba-104">*내 에서만 사용할 수는 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows에서 Visual Studio에서 합니다.*</span><span class="sxs-lookup"><span data-stu-id="589ba-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="589ba-105">기본 또는 지정 된 프로젝트에 대 한 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="589ba-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="589ba-106">`Get-Project` 특히 프로젝트에 대 한 Visual Studio DTE (개발 도구 환경) 개체에 참조를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="589ba-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="589ba-107">구문</span><span class="sxs-lookup"><span data-stu-id="589ba-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="589ba-108">매개 변수</span><span class="sxs-lookup"><span data-stu-id="589ba-108">Parameters</span></span>

| <span data-ttu-id="589ba-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="589ba-109">Parameter</span></span> | <span data-ttu-id="589ba-110">설명</span><span class="sxs-lookup"><span data-stu-id="589ba-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="589ba-111">이름</span><span class="sxs-lookup"><span data-stu-id="589ba-111">Name</span></span> | <span data-ttu-id="589ba-112">패키지 관리자 콘솔에서 선택 된 기본 프로젝트 기본값으로 표시 하려면 프로젝트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="589ba-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="589ba-113">-Name 스위치는 선택 사항 자체입니다.</span><span class="sxs-lookup"><span data-stu-id="589ba-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="589ba-114">모두</span><span class="sxs-lookup"><span data-stu-id="589ba-114">All</span></span> | <span data-ttu-id="589ba-115">솔루션;의 모든 프로젝트에 대 한 정보를 표시합니다. 프로젝트의 순서는 결정적입니다.</span><span class="sxs-lookup"><span data-stu-id="589ba-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="589ba-116">매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="589ba-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="589ba-117">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="589ba-117">Common Parameters</span></span>

<span data-ttu-id="589ba-118">`Get-Project` 다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.</span><span class="sxs-lookup"><span data-stu-id="589ba-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="589ba-119">예제</span><span class="sxs-lookup"><span data-stu-id="589ba-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```