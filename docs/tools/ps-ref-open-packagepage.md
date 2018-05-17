---
title: NuGet 오픈 PackagePage PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 오픈 PackagePage PowerShell 명령에 대 한 참조입니다.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: df4bea390105a7e3fc5d2abd476f2908d92bbcf8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="5f31a-103">Open-PackagePage (Visual Studio의 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="5f31a-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="5f31a-104">*3.0 +;에서 사용 되지 않습니다. 내 에서만 사용할 수는 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows에서 Visual Studio에서 합니다.*</span><span class="sxs-lookup"><span data-stu-id="5f31a-104">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="5f31a-105">프로젝트, 라이선스 또는 지정된 된 패키지에 대 한 보고서 남용 URL을 사용 하 여 기본 브라우저를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="5f31a-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="5f31a-106">구문</span><span class="sxs-lookup"><span data-stu-id="5f31a-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="5f31a-107">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5f31a-107">Parameters</span></span>

| <span data-ttu-id="5f31a-108">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5f31a-108">Parameter</span></span> | <span data-ttu-id="5f31a-109">설명</span><span class="sxs-lookup"><span data-stu-id="5f31a-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5f31a-110">ID</span><span class="sxs-lookup"><span data-stu-id="5f31a-110">Id</span></span> | <span data-ttu-id="5f31a-111">원하는 패키지의 패키지 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="5f31a-111">The package ID of the desired package.</span></span> <span data-ttu-id="5f31a-112">-Id 스위치 자체는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="5f31a-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="5f31a-113">버전</span><span class="sxs-lookup"><span data-stu-id="5f31a-113">Version</span></span> | <span data-ttu-id="5f31a-114">최신 버전을 기본값으로 패키지의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="5f31a-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="5f31a-115">소스</span><span class="sxs-lookup"><span data-stu-id="5f31a-115">Source</span></span> | <span data-ttu-id="5f31a-116">원본 드롭다운 목록에서에서 선택 된 소스를 패키지 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="5f31a-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="5f31a-117">라이선스</span><span class="sxs-lookup"><span data-stu-id="5f31a-117">License</span></span> | <span data-ttu-id="5f31a-118">패키지의 라이선스 URL로 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5f31a-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="5f31a-119">-라이선스 아니고-ReportAbuse를 지정 하는 경우 패키지의 프로젝트 URL 브라우저에 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5f31a-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="5f31a-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="5f31a-120">ReportAbuse</span></span> | <span data-ttu-id="5f31a-121">패키지의 보고서 남용 URL로 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5f31a-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="5f31a-122">-라이선스 아니고-ReportAbuse를 지정 하는 경우 패키지의 프로젝트 URL 브라우저에 열립니다.</span><span class="sxs-lookup"><span data-stu-id="5f31a-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="5f31a-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="5f31a-123">PassThru</span></span> | <span data-ttu-id="5f31a-124">표시 됩니다. 브라우저를 열지 않으려면-whatif를 지원함을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f31a-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="5f31a-125">매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f31a-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="5f31a-126">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="5f31a-126">Common Parameters</span></span>

<span data-ttu-id="5f31a-127">`Open-PackagePage` 다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f31a-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="5f31a-128">예제</span><span class="sxs-lookup"><span data-stu-id="5f31a-128">Examples</span></span>

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