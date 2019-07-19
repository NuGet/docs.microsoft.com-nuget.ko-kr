---
title: NuGet 가져오기-프로젝트 PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에 있는 GetProject PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 830746f032bb4eb916508ef320c5b3d0486b89a4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327360"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="2b6eb-103">Get-Project (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="2b6eb-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="2b6eb-104">*Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내 에서만 사용할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="2b6eb-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="2b6eb-105">기본 또는 지정 된 프로젝트에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6eb-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="2b6eb-106">`Get-Project`는 특히 프로젝트에 대 한 Visual Studio DTE (개발 도구 환경) 개체에 대 한 referent를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6eb-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="2b6eb-107">구문</span><span class="sxs-lookup"><span data-stu-id="2b6eb-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="2b6eb-108">매개 변수</span><span class="sxs-lookup"><span data-stu-id="2b6eb-108">Parameters</span></span>

| <span data-ttu-id="2b6eb-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="2b6eb-109">Parameter</span></span> | <span data-ttu-id="2b6eb-110">Description</span><span class="sxs-lookup"><span data-stu-id="2b6eb-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2b6eb-111">이름</span><span class="sxs-lookup"><span data-stu-id="2b6eb-111">Name</span></span> | <span data-ttu-id="2b6eb-112">패키지 관리자 콘솔에서 선택 된 기본 프로젝트를 기본값으로 지정 하 여 표시할 프로젝트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b6eb-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="2b6eb-113">-Name 스위치는 자체 선택적입니다.</span><span class="sxs-lookup"><span data-stu-id="2b6eb-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="2b6eb-114">모두</span><span class="sxs-lookup"><span data-stu-id="2b6eb-114">All</span></span> | <span data-ttu-id="2b6eb-115">솔루션의 모든 프로젝트에 대 한 정보를 표시 합니다. 프로젝트의 순서는 결정적이 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b6eb-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="2b6eb-116">이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b6eb-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="2b6eb-117">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="2b6eb-117">Common Parameters</span></span>

<span data-ttu-id="2b6eb-118">`Get-Project`는 다음과 같은 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216)를 지원 합니다. 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable입니다.</span><span class="sxs-lookup"><span data-stu-id="2b6eb-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="2b6eb-119">예</span><span class="sxs-lookup"><span data-stu-id="2b6eb-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```