---
title: NuGet 2.2.1 릴리스 정보
description: NuGet 2.2.1 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fddeb4e8c9fb2d85ba1876360862461e8ef025af
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819295"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="5ca13-103">NuGet 2.2.1 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="5ca13-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="5ca13-104">[NuGet 2.2 릴리스 정보](../release-notes/nuget-2.2.md) | [NuGet 2.5 릴리스 정보](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="5ca13-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="5ca13-105">NuGet 2.2.1는 2013 년 2 월 15 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca13-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="5ca13-106">VS 확장 버전 번호가 2.2.40116.9051입니다.</span><span class="sxs-lookup"><span data-stu-id="5ca13-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="5ca13-107">지역화 새로 고침</span><span class="sxs-lookup"><span data-stu-id="5ca13-107">Localization Refresh</span></span>
<span data-ttu-id="5ca13-108">NuGet은 Visual Studio 2012의 일부로 제공, 완벽 하 게 영어 + 13 다른 언어에 지역화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca13-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="5ca13-109">그 이후에 NuGet 2.1 및 2.2 제공 되지만 지역화가 새로 고쳐지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca13-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="5ca13-110">NuGet 2.2.1 릴리스 지역화를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="5ca13-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="5ca13-111">NuGet의 UI와 PowerShell 콘솔은 다음과 같은 언어로 지역화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca13-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="5ca13-112">및</span><span class="sxs-lookup"><span data-stu-id="5ca13-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="5ca13-113">옵션 대신,</span><span class="sxs-lookup"><span data-stu-id="5ca13-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="5ca13-114">체코어</span><span class="sxs-lookup"><span data-stu-id="5ca13-114">Czech</span></span>
1. <span data-ttu-id="5ca13-115">영어</span><span class="sxs-lookup"><span data-stu-id="5ca13-115">English</span></span>
1. <span data-ttu-id="5ca13-116">프랑스어</span><span class="sxs-lookup"><span data-stu-id="5ca13-116">French</span></span>
1. <span data-ttu-id="5ca13-117">독일어</span><span class="sxs-lookup"><span data-stu-id="5ca13-117">German</span></span>
1. <span data-ttu-id="5ca13-118">이탈리아어</span><span class="sxs-lookup"><span data-stu-id="5ca13-118">Italian</span></span>
1. <span data-ttu-id="5ca13-119">일본어</span><span class="sxs-lookup"><span data-stu-id="5ca13-119">Japanese</span></span>
1. <span data-ttu-id="5ca13-120">한국어</span><span class="sxs-lookup"><span data-stu-id="5ca13-120">Korean</span></span>
1. <span data-ttu-id="5ca13-121">폴란드어</span><span class="sxs-lookup"><span data-stu-id="5ca13-121">Polish</span></span>
1. <span data-ttu-id="5ca13-122">포르투갈어(브라질)</span><span class="sxs-lookup"><span data-stu-id="5ca13-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="5ca13-123">러시아어</span><span class="sxs-lookup"><span data-stu-id="5ca13-123">Russian</span></span>
1. <span data-ttu-id="5ca13-124">스페인어</span><span class="sxs-lookup"><span data-stu-id="5ca13-124">Spanish</span></span>
1. <span data-ttu-id="5ca13-125">터키어</span><span class="sxs-lookup"><span data-stu-id="5ca13-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="5ca13-126">Visual Studio 템플릿 여러 사전 설치 된 패키지 저장소를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca13-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="5ca13-127">Visual Studio 서식 파일을 생성 하는 경우에 NuGet을 사용할 수 있습니다 [패키지를 사전 설치](../visual-studio-extensibility/visual-studio-templates.md) 서식 파일의 일부로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca13-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="5ca13-128">지금까지이 기능에는 제한 사항이 동일한 원본에서 제공 하는 데 필요한 모든 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca13-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="5ca13-129">그러나 2.2.1 NuGet이 포함 된 서식 파일, 한 VSIX 또는 레지스트리에 정의 된 디스크의 폴더) (내 여러 저장소에서 설치 된 패키지 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca13-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="5ca13-130">이 기능에 대 한 주요 시나리오 ASP.NET 프로젝트 템플릿 사용자 지정입니다.</span><span class="sxs-lookup"><span data-stu-id="5ca13-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="5ca13-131">기본 제공 ASP.NET 템플릿 로컬 디스크에서 패키지를 풀링 하는 사전 설치 된 패키지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca13-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="5ca13-132">이제 ASP.NET에서 설치 된 기존 패키지를 사용 하는 사용자 지정 ASP.NET 프로젝트 템플릿을 만들 수 있지만 서식 파일에 추가 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca13-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="5ca13-133">버그 수정</span><span class="sxs-lookup"><span data-stu-id="5ca13-133">Bug Fixes</span></span>
<span data-ttu-id="5ca13-134">NuGet 2.2.1 대상으로 지정 된 몇 가지 버그 수정 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ca13-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="5ca13-135">작업 목록에 대 한 항목에서에서 수정 된 NuGet 2.2.1 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)합니다.</span><span class="sxs-lookup"><span data-stu-id="5ca13-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="5ca13-136">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="5ca13-136">Known Issues</span></span>

<span data-ttu-id="5ca13-137">모든 사전 설치 된 패키지 저장소에 대 한 동일한 값을 사용 해야 ASP.NET 프로젝트 템플릿을 확장 하는 경우는 `isPreunzipped` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="5ca13-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
