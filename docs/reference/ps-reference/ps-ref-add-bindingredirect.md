---
title: NuGet BindingRedirect PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 BindingRedirect PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d3d156cf882229260e8cf55f8ece2804aec36dc9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384986"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="ed0e5-103">Add-BindingRedirect (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="ed0e5-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ed0e5-104">*Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내 에서만 사용할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="ed0e5-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="ed0e5-105">프로젝트의 출력 경로에 있는 모든 어셈블리를 검사 하 고 필요한 경우 응용 프로그램이 나 웹 구성 파일에 바인딩 리디렉션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0e5-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="ed0e5-106">이 명령은 패키지를 설치할 때 자동으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ed0e5-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="ed0e5-107">바인딩 리디렉션 및 사용 이유에 대 한 자세한 내용은 .NET 설명서의 [어셈블리 버전 리디렉션](/dotnet/framework/configure-apps/redirect-assembly-versions) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="ed0e5-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="ed0e5-108">구문</span><span class="sxs-lookup"><span data-stu-id="ed0e5-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="ed0e5-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ed0e5-109">Parameters</span></span>

| <span data-ttu-id="ed0e5-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="ed0e5-110">Parameter</span></span> | <span data-ttu-id="ed0e5-111">설명</span><span class="sxs-lookup"><span data-stu-id="ed0e5-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ed0e5-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="ed0e5-112">ProjectName</span></span> | <span data-ttu-id="ed0e5-113">하다 바인딩 리디렉션을 추가할 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="ed0e5-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="ed0e5-114">-ProjectName 스위치 자체는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="ed0e5-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="ed0e5-115">이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ed0e5-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ed0e5-116">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="ed0e5-116">Common Parameters</span></span>

<span data-ttu-id="ed0e5-117">`Add-BindingRedirect`는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](https://go.microsoft.com/fwlink/?LinkID=113216)를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="ed0e5-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ed0e5-118">예</span><span class="sxs-lookup"><span data-stu-id="ed0e5-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```