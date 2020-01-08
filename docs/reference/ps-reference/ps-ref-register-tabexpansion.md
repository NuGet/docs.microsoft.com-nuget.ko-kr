---
title: NuGet 레지스터-TabExpansion PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 Register-TabExpansion PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 37aed96760e642b03c02bf31fe47a54f0e3cb74a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384456"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="e15c7-103">레지스터-TabExpansion (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="e15c7-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="e15c7-104">*Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내 에서만 사용할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="e15c7-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="e15c7-105">지정 된 명령의 매개 변수에 대 한 탭 확장을 등록 합니다. 예를 들어 명령을 입력할 때 Tab 키를 사용 하는 경우 확장 된 값이 해당 매개 변수에 사용할 수 있는 옵션으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e15c7-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="e15c7-106">명령에 대 한 모든 이전 확장을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="e15c7-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="e15c7-107">구문</span><span class="sxs-lookup"><span data-stu-id="e15c7-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="e15c7-108">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e15c7-108">Parameters</span></span>

| <span data-ttu-id="e15c7-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e15c7-109">Parameter</span></span> | <span data-ttu-id="e15c7-110">설명</span><span class="sxs-lookup"><span data-stu-id="e15c7-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e15c7-111">이름</span><span class="sxs-lookup"><span data-stu-id="e15c7-111">Name</span></span> | <span data-ttu-id="e15c7-112">하다 확장을 등록할 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="e15c7-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="e15c7-113">-Name 스위치 자체는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="e15c7-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="e15c7-114">정의</span><span class="sxs-lookup"><span data-stu-id="e15c7-114">Definition</span></span> | <span data-ttu-id="e15c7-115">하다 구문에서 인수를 설명 하는 개체 `@{'<parameter>' = {'<value1>', '<value2>', ...}}` `<parameter>`는 수정할 매개 변수의 이름이 고 각 `<value>`는 특정 확장을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15c7-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="e15c7-116">작은따옴표와 큰따옴표가 모두 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e15c7-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="e15c7-117">이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e15c7-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="e15c7-118">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="e15c7-118">Common Parameters</span></span>

<span data-ttu-id="e15c7-119">`Register-TabExpansion`는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](https://go.microsoft.com/fwlink/?LinkID=113216)를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15c7-119">`Register-TabExpansion` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="e15c7-120">예</span><span class="sxs-lookup"><span data-stu-id="e15c7-120">Examples</span></span>

<span data-ttu-id="e15c7-121">EventManager, 유틸리티 및 SpecialParser의 세 가지 프로젝트 이름을 포함 하는 솔루션을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15c7-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="e15c7-122">개발자는 이러한 각 프로젝트와 함께 다양 한 시간에 `Update-Package` 명령을 사용 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="e15c7-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="e15c7-123">`Update-Package` 명령이 `-ProjectName` 인수에 대 한 자동 완성 확장 기능을 제공 하 여 매번 프로젝트 이름을 입력할 필요가 없도록 하는 것이 편리 하다는 것을 알게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e15c7-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="e15c7-124">다음 명령에서는 이러한 세 개의 프로젝트 이름을 `-ProjectName` 매개 변수에 대 한 확장으로 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e15c7-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="e15c7-125">그러면 개발자는 `Update-Package -ProjectName `를 입력 하 고 Tab 키를 눌러 자동 완성 옵션으로 제공 된 확장을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e15c7-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![레지스터 탭 확장 사용 예](media/Register-TabExpansion-Example.png)
