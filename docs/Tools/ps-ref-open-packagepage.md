---
title: "NuGet 오픈 PackagePage PowerShell 참조 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio에서 NuGet 패키지 관리자 콘솔에서 오픈 PackagePage PowerShell 명령에 대 한 참조입니다."
keywords: "NuGet 패키지 관리자 콘솔, NuGet Powershell 명령, 오픈 PackagePage NuGet Powershell 참조"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 389bad37940f05dd864adfc06080bf746464365d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="a695a-104">열기-PackagePage (Visual Studio에서 패키지 관리자 콘솔)</span><span class="sxs-lookup"><span data-stu-id="a695a-104">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a695a-105">*3.0 +;에서 사용 되지 않습니다. 내 에서만 사용할 수는 [NuGet 패키지 관리자 콘솔](Package-Manager-Console.md) Windows에서 Visual Studio에서 합니다.*</span><span class="sxs-lookup"><span data-stu-id="a695a-105">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="a695a-106">프로젝트, 라이선스 또는 지정된 된 패키지에 대 한 보고서 남용 URL을 사용 하 여 기본 브라우저를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a695a-106">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="a695a-107">구문</span><span class="sxs-lookup"><span data-stu-id="a695a-107">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a695a-108">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a695a-108">Parameters</span></span>

| <span data-ttu-id="a695a-109">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a695a-109">Parameter</span></span> | <span data-ttu-id="a695a-110">설명</span><span class="sxs-lookup"><span data-stu-id="a695a-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a695a-111">ID</span><span class="sxs-lookup"><span data-stu-id="a695a-111">Id</span></span> | <span data-ttu-id="a695a-112">원하는 패키지의 패키지 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="a695a-112">The package ID of the desired package.</span></span> <span data-ttu-id="a695a-113">-Id 스위치 자체는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="a695a-113">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="a695a-114">버전</span><span class="sxs-lookup"><span data-stu-id="a695a-114">Version</span></span> | <span data-ttu-id="a695a-115">최신 버전을 기본값으로 패키지의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="a695a-115">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="a695a-116">소스</span><span class="sxs-lookup"><span data-stu-id="a695a-116">Source</span></span> | <span data-ttu-id="a695a-117">원본 드롭다운 목록에서에서 선택 된 소스를 패키지 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="a695a-117">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="a695a-118">라이선스</span><span class="sxs-lookup"><span data-stu-id="a695a-118">License</span></span> | <span data-ttu-id="a695a-119">패키지의 라이선스 URL로 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a695a-119">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="a695a-120">-라이선스 아니고-ReportAbuse를 지정 하는 경우 패키지의 프로젝트 URL 브라우저에 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a695a-120">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="a695a-121">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="a695a-121">ReportAbuse</span></span> | <span data-ttu-id="a695a-122">패키지의 보고서 남용 URL로 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a695a-122">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="a695a-123">-라이선스 아니고-ReportAbuse를 지정 하는 경우 패키지의 프로젝트 URL 브라우저에 열립니다.</span><span class="sxs-lookup"><span data-stu-id="a695a-123">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="a695a-124">PassThru</span><span class="sxs-lookup"><span data-stu-id="a695a-124">PassThru</span></span> | <span data-ttu-id="a695a-125">표시 됩니다. 브라우저를 열지 않으려면-whatif를 지원함을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a695a-125">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="a695a-126">매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a695a-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a695a-127">일반 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a695a-127">Common Parameters</span></span>

<span data-ttu-id="a695a-128">`Open-PackagePage`다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.</span><span class="sxs-lookup"><span data-stu-id="a695a-128">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a695a-129">예제</span><span class="sxs-lookup"><span data-stu-id="a695a-129">Examples</span></span>

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