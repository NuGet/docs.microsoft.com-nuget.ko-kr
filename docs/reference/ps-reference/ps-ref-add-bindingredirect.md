---
title: NuGet Add-BindingRedirect PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 Add-BindingRedirect PowerShell 명령에 대 한 참조입니다.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 62edf1bf8995a4e1ffb83acc7a7621a786cc53e4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777618"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="f6ba5-103">Add-BindingRedirect (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="f6ba5-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f6ba5-104">*Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내 에서만 사용할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="f6ba5-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f6ba5-105">프로젝트의 출력 경로에 있는 모든 어셈블리를 검사 하 고 필요한 경우 응용 프로그램이 나 웹 구성 파일에 바인딩 리디렉션을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="f6ba5-106">이 명령은 패키지를 설치할 때 자동으로 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-106">This command is run automatically when installing a package.</span></span>

> [!NOTE]
> <span data-ttu-id="f6ba5-107">이는 packages.config 파일을 사용 하는 시나리오에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-107">This only applies to scenarios using a packages.config file.</span></span> <span data-ttu-id="f6ba5-108">자세한 내용은 [NuGet packages.config 파일 참조](~/reference/packages-config.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-108">For more information, see [NuGet packages.config file reference](~/reference/packages-config.md).</span></span>

<span data-ttu-id="f6ba5-109">바인딩 리디렉션 및 사용 이유에 대 한 자세한 내용은 .NET 설명서의 [어셈블리 버전 리디렉션](/dotnet/framework/configure-apps/redirect-assembly-versions) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-109">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="f6ba5-110">구문</span><span class="sxs-lookup"><span data-stu-id="f6ba5-110">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f6ba5-111">매개 변수</span><span class="sxs-lookup"><span data-stu-id="f6ba5-111">Parameters</span></span>

| <span data-ttu-id="f6ba5-112">매개 변수</span><span class="sxs-lookup"><span data-stu-id="f6ba5-112">Parameter</span></span> | <span data-ttu-id="f6ba5-113">Description</span><span class="sxs-lookup"><span data-stu-id="f6ba5-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f6ba5-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="f6ba5-114">ProjectName</span></span> | <span data-ttu-id="f6ba5-115">하다 바인딩 리디렉션을 추가할 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-115">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="f6ba5-116">-ProjectName 스위치 자체는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-116">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="f6ba5-117">이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f6ba5-118">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="f6ba5-118">Common Parameters</span></span>

<span data-ttu-id="f6ba5-119">`Add-BindingRedirect` 에서는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](/powershell/module/microsoft.powershell.core/about/about_commonparameters)를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6ba5-119">`Add-BindingRedirect` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f6ba5-120">예</span><span class="sxs-lookup"><span data-stu-id="f6ba5-120">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```