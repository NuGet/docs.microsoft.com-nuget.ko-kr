---
title: NuGet 오픈 PackagePage PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 오픈 PackagePage PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0325aa4ddd718a901dd6a09cdf86cae260e326ab
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547170"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="5de93-103">Open-PackagePage (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="5de93-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="5de93-104">*3.0 이상;에서 사용 되지 않음 내 에서만 사용 가능 합니다 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows의 Visual Studio에서 합니다.*</span><span class="sxs-lookup"><span data-stu-id="5de93-104">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="5de93-105">프로젝트, 라이선스 또는 지정된 된 패키지에 대 한 URL 신고를 사용 하 여 기본 브라우저를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5de93-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="5de93-106">구문</span><span class="sxs-lookup"><span data-stu-id="5de93-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="5de93-107">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5de93-107">Parameters</span></span>

| <span data-ttu-id="5de93-108">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5de93-108">Parameter</span></span> | <span data-ttu-id="5de93-109">설명</span><span class="sxs-lookup"><span data-stu-id="5de93-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5de93-110">ID</span><span class="sxs-lookup"><span data-stu-id="5de93-110">Id</span></span> | <span data-ttu-id="5de93-111">원하는 패키지의 패키지 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="5de93-111">The package ID of the desired package.</span></span> <span data-ttu-id="5de93-112">-Id 자체 스위치는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5de93-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="5de93-113">버전</span><span class="sxs-lookup"><span data-stu-id="5de93-113">Version</span></span> | <span data-ttu-id="5de93-114">최신 버전을 기본값으로 패키지의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="5de93-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="5de93-115">소스</span><span class="sxs-lookup"><span data-stu-id="5de93-115">Source</span></span> | <span data-ttu-id="5de93-116">원본 드롭다운 목록에서에서 선택된 된 소스가 기본적으로 패키지 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="5de93-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="5de93-117">라이선스</span><span class="sxs-lookup"><span data-stu-id="5de93-117">License</span></span> | <span data-ttu-id="5de93-118">패키지의 라이선스 URL로 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5de93-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="5de93-119">-라이선스 아니고-ReportAbuse 지정 된 경우 브라우저는 패키지의 프로젝트 URL을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5de93-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="5de93-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="5de93-120">ReportAbuse</span></span> | <span data-ttu-id="5de93-121">패키지의 악성 URL 신고 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5de93-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="5de93-122">-라이선스 아니고-ReportAbuse 지정 된 경우 브라우저는 패키지의 프로젝트 URL을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5de93-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="5de93-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="5de93-123">PassThru</span></span> | <span data-ttu-id="5de93-124">URL 표시 브라우저를 열고 표시 하지 않으려면-WhatIf를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5de93-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="5de93-125">이러한 매개 변수 중 파이프라인 입력 하거나 와일드 카드 문자 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5de93-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="5de93-126">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="5de93-126">Common Parameters</span></span>

<span data-ttu-id="5de93-127">`Open-PackagePage` 다음을 지원 합니다 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, 자세한 정보 표시, WarningAction, WarningVariable.</span><span class="sxs-lookup"><span data-stu-id="5de93-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="5de93-128">예제</span><span class="sxs-lookup"><span data-stu-id="5de93-128">Examples</span></span>

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