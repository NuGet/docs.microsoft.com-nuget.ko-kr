---
title: NuGet 등록 TabExpansion PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 등록 TabExpansion PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 98171c598bd4a3468bd23e2d6060e267c38021b4
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546607"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="83583-103">등록 키를 누른 채 TabExpansion (Visual Studio에서 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="83583-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="83583-104">*내 에서만 사용 가능 합니다 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows의 Visual Studio에서 합니다.*</span><span class="sxs-lookup"><span data-stu-id="83583-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="83583-105">명령을 입력 하는 경우 탭을 사용 하면 해당 매개 변수에 대해 사용 가능한 옵션으로 확장된 값이 표시 되도록 지정 된 명령의 매개 변수에 대해 탭 확장을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="83583-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="83583-106">명령에 대 한 모든 이전 확장을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="83583-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="83583-107">구문</span><span class="sxs-lookup"><span data-stu-id="83583-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="83583-108">매개 변수</span><span class="sxs-lookup"><span data-stu-id="83583-108">Parameters</span></span>

| <span data-ttu-id="83583-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="83583-109">Parameter</span></span> | <span data-ttu-id="83583-110">설명</span><span class="sxs-lookup"><span data-stu-id="83583-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="83583-111">이름</span><span class="sxs-lookup"><span data-stu-id="83583-111">Name</span></span> | <span data-ttu-id="83583-112">(필수) 확장을 등록 하는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="83583-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="83583-113">-Name 자체 스위치는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="83583-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="83583-114">정의</span><span class="sxs-lookup"><span data-stu-id="83583-114">Definition</span></span> | <span data-ttu-id="83583-115">(필수) 구문에서 인수를 설명 하는 개체 `@{'<parameter>' = {'<value1>', '<value2>', ...}}` 여기서 `<parameter>` 매개 변수를 수정 하 고 각각의 이름은 `<value>` 특정 확장을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="83583-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="83583-116">모두 작은따옴표와 큰따옴표 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="83583-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="83583-117">이러한 매개 변수 중 파이프라인 입력 하거나 와일드 카드 문자 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="83583-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="83583-118">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="83583-118">Common Parameters</span></span>

<span data-ttu-id="83583-119">`Register-TabExpansion` 다음을 지원 합니다 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, 자세한 정보 표시, WarningAction, WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="83583-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="83583-120">예제</span><span class="sxs-lookup"><span data-stu-id="83583-120">Examples</span></span>

<span data-ttu-id="83583-121">프로젝트 이름 EventManager, 유틸리티 및 SpecialParser 3 개를 포함 하는 솔루션을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="83583-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="83583-122">개발자가 자주 사용 하는 `Update-Package` 각 해당 프로젝트를 사용 하 여 서로 다른 시간에 명령 합니다.</span><span class="sxs-lookup"><span data-stu-id="83583-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="83583-123">있으면 편리 찾습니다 그녀는 `Update-Package` 명령에 대 한 자동 완성 확장을 제공 합니다 `-ProjectName` 인수 그녀 때마다 프로젝트 이름을 입력할 필요가 없도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="83583-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="83583-124">다음 명령을 그런 다음 이러한 세 가지 프로젝트 이름에 대 한 확장으로 등록 된 `-ProjectName` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="83583-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="83583-125">개발자 수 입력 `Update-Package -ProjectName `, tab 키를 누르고, 및 자동 완성 옵션으로 제공 되는 확장을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="83583-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![등록 TabExpansion를 사용 하는 예제](media/Register-TabExpansion-Example.png)
