---
title: NuGet Open-PackagePage PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 Open-PackagePage PowerShell 명령에 대 한 참조입니다.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d34a91007197f8004e4923deedb1cdb26d662d53
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780409"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="410fe-103">Open-PackagePage (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="410fe-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="410fe-104">*3.0 이상에서 사용 되지 않음 Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내 에서만 사용할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="410fe-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="410fe-105">지정 된 패키지에 대 한 프로젝트, 라이선스 또는 신고 URL을 사용 하 여 기본 브라우저를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="410fe-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="410fe-106">구문</span><span class="sxs-lookup"><span data-stu-id="410fe-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="410fe-107">매개 변수</span><span class="sxs-lookup"><span data-stu-id="410fe-107">Parameters</span></span>

| <span data-ttu-id="410fe-108">매개 변수</span><span class="sxs-lookup"><span data-stu-id="410fe-108">Parameter</span></span> | <span data-ttu-id="410fe-109">Description</span><span class="sxs-lookup"><span data-stu-id="410fe-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="410fe-110">Id</span><span class="sxs-lookup"><span data-stu-id="410fe-110">Id</span></span> | <span data-ttu-id="410fe-111">원하는 패키지의 패키지 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="410fe-111">The package ID of the desired package.</span></span> <span data-ttu-id="410fe-112">-Id 스위치 자체는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="410fe-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="410fe-113">버전</span><span class="sxs-lookup"><span data-stu-id="410fe-113">Version</span></span> | <span data-ttu-id="410fe-114">패키지의 버전은 기본적으로 최신 버전을 기본값으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="410fe-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="410fe-115">원본</span><span class="sxs-lookup"><span data-stu-id="410fe-115">Source</span></span> | <span data-ttu-id="410fe-116">원본 드롭다운에서 선택 된 소스를 기본값으로 하는 패키지 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="410fe-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="410fe-117">라이선스</span><span class="sxs-lookup"><span data-stu-id="410fe-117">License</span></span> | <span data-ttu-id="410fe-118">패키지의 라이선스 URL에 대 한 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="410fe-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="410fe-119">라이선스와-ReportAbuse 모두 지정 하지 않으면 브라우저에서 패키지의 프로젝트 URL을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="410fe-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="410fe-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="410fe-120">ReportAbuse</span></span> | <span data-ttu-id="410fe-121">패키지의 신고 URL에 대 한 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="410fe-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="410fe-122">라이선스와-ReportAbuse 모두 지정 하지 않으면 브라우저에서 패키지의 프로젝트 URL을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="410fe-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="410fe-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="410fe-123">PassThru</span></span> | <span data-ttu-id="410fe-124">URL을 표시 합니다. 브라우저를 열지 않으려면-WhatIf를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="410fe-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="410fe-125">이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="410fe-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="410fe-126">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="410fe-126">Common Parameters</span></span>

<span data-ttu-id="410fe-127">`Open-PackagePage` 에서는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](/powershell/module/microsoft.powershell.core/about/about_commonparameters)를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="410fe-127">`Open-PackagePage` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="410fe-128">예</span><span class="sxs-lookup"><span data-stu-id="410fe-128">Examples</span></span>

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```