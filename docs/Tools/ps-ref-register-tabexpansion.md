---
title: NuGet 레지스터 TabExpansion PowerShell 참조 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 레지스터 TabExpansion PowerShell 명령에 대 한 참조입니다.
keywords: NuGet 패키지 관리자 콘솔, NuGet Powershell 명령, 레지스터 TabExpansion NuGet Powershell 참조
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: c7b95c46c55b95a8d743f9661ef9c63433b0192d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="18a75-104">등록 키를 누른 채 TabExpansion (Visual Studio에서 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="18a75-104">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="18a75-105">*내 에서만 사용할 수는 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows에서 Visual Studio에서 합니다.*</span><span class="sxs-lookup"><span data-stu-id="18a75-105">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="18a75-106">확장 된 값이 해당 매개 변수에 대해 사용할 수 있는 옵션으로 표시 탭 명령을 입력할 때 사용 되 면 되도록 지정 된 매개 변수에 대해 탭 확장을 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="18a75-106">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="18a75-107">명령에 대 한 모든 이전 확장을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="18a75-107">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="18a75-108">구문</span><span class="sxs-lookup"><span data-stu-id="18a75-108">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="18a75-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="18a75-109">Parameters</span></span>

| <span data-ttu-id="18a75-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="18a75-110">Parameter</span></span> | <span data-ttu-id="18a75-111">설명</span><span class="sxs-lookup"><span data-stu-id="18a75-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="18a75-112">이름</span><span class="sxs-lookup"><span data-stu-id="18a75-112">Name</span></span> | <span data-ttu-id="18a75-113">(필수) 확장을 등록할 수 있는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="18a75-113">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="18a75-114">-Name 자체 스위치는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="18a75-114">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="18a75-115">정의</span><span class="sxs-lookup"><span data-stu-id="18a75-115">Definition</span></span> | <span data-ttu-id="18a75-116">(필수) 구문에 대 한 인수를 설명 하는 개체 `@{'<parameter>' = {'<value1>', '<value2>', ...}}` 여기서 `<parameter>` 매개 변수를 수정 하 고 각각의 이름인 `<value>` 특정 확장을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="18a75-116">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="18a75-117">작은따옴표와 큰따옴표가 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="18a75-117">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="18a75-118">매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="18a75-118">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="18a75-119">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="18a75-119">Common Parameters</span></span>

<span data-ttu-id="18a75-120">`Register-TabExpansion` 다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.</span><span class="sxs-lookup"><span data-stu-id="18a75-120">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="18a75-121">예제</span><span class="sxs-lookup"><span data-stu-id="18a75-121">Examples</span></span>

<span data-ttu-id="18a75-122">프로젝트 이름 EventManager, 유틸리티 및 SpecialParser 3 개를 포함 하는 솔루션을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="18a75-122">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="18a75-123">개발자는 주로 사용은 `Update-Package` 각각의 해당 프로젝트와 다른 시간에 명령 합니다.</span><span class="sxs-lookup"><span data-stu-id="18a75-123">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="18a75-124">가 편리 하 게 찾습니다 그녀는 `Update-Package` 명령에 대 한 자동 완성 기능 확장을 제공는 `-ProjectName` 인수 하므로 매번 프로젝트 이름을 입력 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="18a75-124">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="18a75-125">다음 명령에 대 한 확장으로 이러한 세 개의 프로젝트 이름을 만든 다음,으로 등록 된 `-ProjectName` 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="18a75-125">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="18a75-126">개발자 입력할 수 `Update-Package -ProjectName `, tab 키를 및 자동 완성 옵션으로 제공 하는 확장을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="18a75-126">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![레지스터 TabExpansion 사용의 예](media/Register-TabExpansion-Example.png)
