---
title: NuGet 추가 BindingRedirect PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 추가 BindingRedirect PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5f318ddfb2bb8498ab3e608f8036be05dcb0706
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842535"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="84a7f-103">Add-BindingRedirect (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="84a7f-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="84a7f-104">*내 에서만 사용 가능 합니다 [패키지 관리자 콘솔](package-manager-console.md) Windows의 Visual Studio에서 합니다.*</span><span class="sxs-lookup"><span data-stu-id="84a7f-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="84a7f-105">프로젝트의 출력 경로 내의 모든 어셈블리를 검사 하 고 필요한 경우 응용 프로그램 또는 웹 구성 파일에 바인딩 리디렉션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="84a7f-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="84a7f-106">이 명령은 패키지를 설치할 때 자동으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="84a7f-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="84a7f-107">바인딩 리디렉션 및 사용 되는 이유에 대 한 내용은 참조 하세요 [어셈블리 버전 리디렉션](/dotnet/framework/configure-apps/redirect-assembly-versions) .NET 설명서에서.</span><span class="sxs-lookup"><span data-stu-id="84a7f-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="84a7f-108">구문</span><span class="sxs-lookup"><span data-stu-id="84a7f-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="84a7f-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="84a7f-109">Parameters</span></span>

| <span data-ttu-id="84a7f-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="84a7f-110">Parameter</span></span> | <span data-ttu-id="84a7f-111">설명</span><span class="sxs-lookup"><span data-stu-id="84a7f-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="84a7f-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="84a7f-112">ProjectName</span></span> | <span data-ttu-id="84a7f-113">(필수) 프로젝트를 바인딩 리디렉션을 추가할 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="84a7f-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="84a7f-114">-ProjectName 스위치 자체가 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="84a7f-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="84a7f-115">이러한 매개 변수 중 파이프라인 입력 하거나 와일드 카드 문자 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="84a7f-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="84a7f-116">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="84a7f-116">Common Parameters</span></span>

<span data-ttu-id="84a7f-117">`Add-BindingRedirect` 다음을 지원 합니다 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="84a7f-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="84a7f-118">예</span><span class="sxs-lookup"><span data-stu-id="84a7f-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```