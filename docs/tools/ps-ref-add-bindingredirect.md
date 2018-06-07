---
title: NuGet 추가 BindingRedirect PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 추가 BindingRedirect PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: f3addd95b64d78eac201deeb2c64915ea935cd71
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817625"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="4849e-103">Add-BindingRedirect (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="4849e-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4849e-104">*내 에서만 사용할 수는 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows에서 Visual Studio에서 합니다.*</span><span class="sxs-lookup"><span data-stu-id="4849e-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="4849e-105">프로젝트에 대 한 출력 경로 내의 모든 어셈블리를 검사 하 고 요소가 필요한 경우 응용 프로그램 또는 웹 구성 파일에 바인딩 리디렉션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4849e-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="4849e-106">이 명령은 패키지를 설치할 때 자동으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4849e-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="4849e-107">바인딩 리디렉션 및 사용 하는 이유에 대 한 세부 정보를 참조 하십시오. [어셈블리 버전 리디렉션](/dotnet/framework/configure-apps/redirect-assembly-versions) .NET 설명서에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4849e-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="4849e-108">구문</span><span class="sxs-lookup"><span data-stu-id="4849e-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="4849e-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="4849e-109">Parameters</span></span>

| <span data-ttu-id="4849e-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="4849e-110">Parameter</span></span> | <span data-ttu-id="4849e-111">설명</span><span class="sxs-lookup"><span data-stu-id="4849e-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4849e-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="4849e-112">ProjectName</span></span> | <span data-ttu-id="4849e-113">(필수) 바인딩 리디렉션을 추가할 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="4849e-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="4849e-114">자체-p r o j 스위치는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="4849e-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="4849e-115">매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4849e-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4849e-116">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="4849e-116">Common Parameters</span></span>

<span data-ttu-id="4849e-117">`Add-BindingRedirect` 다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.</span><span class="sxs-lookup"><span data-stu-id="4849e-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4849e-118">예제</span><span class="sxs-lookup"><span data-stu-id="4849e-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```