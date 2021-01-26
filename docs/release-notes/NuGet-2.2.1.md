---
title: NuGet 2.2.1 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 2.2.1를 포함 하는 NuGet에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776807"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="fa97b-103">NuGet 2.2.1 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="fa97b-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="fa97b-104">[NuGet 2.2 릴리스 정보](../release-notes/nuget-2.2.md)  |  [NuGet 2.5 릴리스 정보](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="fa97b-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="fa97b-105">NuGet 2.2.1는 2013 년 2 월 15 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fa97b-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="fa97b-106">VS 확장 버전 번호는 2.2.40116.9051입니다.</span><span class="sxs-lookup"><span data-stu-id="fa97b-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="fa97b-107">지역화 새로 고침</span><span class="sxs-lookup"><span data-stu-id="fa97b-107">Localization Refresh</span></span>
<span data-ttu-id="fa97b-108">NuGet은 Visual Studio 2012의 일부로 제공 될 때 영어 + 13 기타 언어로 완전히 지역화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fa97b-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="fa97b-109">그 이후에는 NuGet 2.1 및 2.2이 제공 되었지만 지역화를 새로 고치지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="fa97b-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="fa97b-110">NuGet 2.2.1 릴리스는 지역화를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="fa97b-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="fa97b-111">NuGet의 UI 및 PowerShell 콘솔은 다음 언어로 지역화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa97b-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="fa97b-112">중국어(간체)</span><span class="sxs-lookup"><span data-stu-id="fa97b-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="fa97b-113">중국어(번체)</span><span class="sxs-lookup"><span data-stu-id="fa97b-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="fa97b-114">체코어</span><span class="sxs-lookup"><span data-stu-id="fa97b-114">Czech</span></span>
1. <span data-ttu-id="fa97b-115">영어</span><span class="sxs-lookup"><span data-stu-id="fa97b-115">English</span></span>
1. <span data-ttu-id="fa97b-116">프랑스어</span><span class="sxs-lookup"><span data-stu-id="fa97b-116">French</span></span>
1. <span data-ttu-id="fa97b-117">독일어</span><span class="sxs-lookup"><span data-stu-id="fa97b-117">German</span></span>
1. <span data-ttu-id="fa97b-118">이탈리아어</span><span class="sxs-lookup"><span data-stu-id="fa97b-118">Italian</span></span>
1. <span data-ttu-id="fa97b-119">일본어</span><span class="sxs-lookup"><span data-stu-id="fa97b-119">Japanese</span></span>
1. <span data-ttu-id="fa97b-120">한국어</span><span class="sxs-lookup"><span data-stu-id="fa97b-120">Korean</span></span>
1. <span data-ttu-id="fa97b-121">폴란드어</span><span class="sxs-lookup"><span data-stu-id="fa97b-121">Polish</span></span>
1. <span data-ttu-id="fa97b-122">포르투갈어(브라질)</span><span class="sxs-lookup"><span data-stu-id="fa97b-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="fa97b-123">러시아어</span><span class="sxs-lookup"><span data-stu-id="fa97b-123">Russian</span></span>
1. <span data-ttu-id="fa97b-124">스페인어</span><span class="sxs-lookup"><span data-stu-id="fa97b-124">Spanish</span></span>
1. <span data-ttu-id="fa97b-125">터키어</span><span class="sxs-lookup"><span data-stu-id="fa97b-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="fa97b-126">Visual Studio 템플릿은 미리 설치 된 여러 패키지 리포지토리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa97b-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="fa97b-127">Visual Studio 템플릿을 생성 하는 경우 NuGet을 사용 하 여 템플릿의 일부로 [패키지를 사전 설치할](../visual-studio-extensibility/visual-studio-templates.md) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa97b-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="fa97b-128">지금 까지는이 기능에 모든 패키지가 동일한 소스에서 제공 되어야 한다는 제한이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="fa97b-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="fa97b-129">그러나 NuGet 2.2.1을 사용 하면 템플릿, VSIX 또는 레지스트리에 정의 된 디스크의 폴더에 있는 여러 리포지토리에서 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa97b-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="fa97b-130">이 기능의 주요 시나리오는 사용자 지정 ASP.NET 프로젝트 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="fa97b-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="fa97b-131">기본 제공 ASP.NET 템플릿은 미리 설치 된 패키지를 사용 하 여 로컬 디스크에서 패키지를 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="fa97b-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="fa97b-132">이제 ASP.NET에 의해 설치 된 기존 패키지를 사용 하지만 템플릿에 추가 NuGet 패키지를 추가 하는 사용자 지정 ASP.NET 프로젝트 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa97b-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="fa97b-133">버그 픽스</span><span class="sxs-lookup"><span data-stu-id="fa97b-133">Bug Fixes</span></span>
<span data-ttu-id="fa97b-134">NuGet 2.2.1에는 몇 가지 대상 버그 수정이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa97b-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="fa97b-135">NuGet 2.2.1에서 수정 된 작업 항목 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)를 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="fa97b-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="fa97b-136">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="fa97b-136">Known Issues</span></span>

<span data-ttu-id="fa97b-137">ASP.NET 프로젝트 템플릿을 확장 하는 경우 사전 설치 된 모든 패키지 리포지토리는 특성에 대해 동일한 값을 사용 해야 합니다 `isPreunzipped` .</span><span class="sxs-lookup"><span data-stu-id="fa97b-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
