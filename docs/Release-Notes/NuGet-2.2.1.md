---
title: "NuGet 2.2.1 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 2.2.1 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다."
keywords: "NuGet 2.2.1 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c3e912dcabeb3a26c880b42560a3cec6f7bf2db9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="4289a-104">NuGet 2.2.1 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="4289a-104">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="4289a-105">[NuGet 2.2 릴리스 정보](../release-notes/nuget-2.2.md) | [NuGet 2.5 릴리스 정보](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="4289a-105">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="4289a-106">NuGet 2.2.1는 2013 년 2 월 15 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4289a-106">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="4289a-107">VS 확장 버전 번호가 2.2.40116.9051입니다.</span><span class="sxs-lookup"><span data-stu-id="4289a-107">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="4289a-108">지역화 새로 고침</span><span class="sxs-lookup"><span data-stu-id="4289a-108">Localization Refresh</span></span>
<span data-ttu-id="4289a-109">NuGet은 Visual Studio 2012의 일부로 제공, 완벽 하 게 영어 + 13 다른 언어에 지역화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4289a-109">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="4289a-110">그 이후에 NuGet 2.1 및 2.2 제공 되지만 지역화가 새로 고쳐지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4289a-110">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="4289a-111">NuGet 2.2.1 릴리스 지역화를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="4289a-111">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="4289a-112">NuGet의 UI와 PowerShell 콘솔은 다음과 같은 언어로 지역화 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4289a-112">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="4289a-113">및</span><span class="sxs-lookup"><span data-stu-id="4289a-113">Chinese (Simplified)</span></span>
1. <span data-ttu-id="4289a-114">옵션 대신,</span><span class="sxs-lookup"><span data-stu-id="4289a-114">Chinese (Traditional)</span></span>
1. <span data-ttu-id="4289a-115">체코어</span><span class="sxs-lookup"><span data-stu-id="4289a-115">Czech</span></span>
1. <span data-ttu-id="4289a-116">영어</span><span class="sxs-lookup"><span data-stu-id="4289a-116">English</span></span>
1. <span data-ttu-id="4289a-117">프랑스어</span><span class="sxs-lookup"><span data-stu-id="4289a-117">French</span></span>
1. <span data-ttu-id="4289a-118">독일어</span><span class="sxs-lookup"><span data-stu-id="4289a-118">German</span></span>
1. <span data-ttu-id="4289a-119">이탈리아어</span><span class="sxs-lookup"><span data-stu-id="4289a-119">Italian</span></span>
1. <span data-ttu-id="4289a-120">일본어</span><span class="sxs-lookup"><span data-stu-id="4289a-120">Japanese</span></span>
1. <span data-ttu-id="4289a-121">한국어</span><span class="sxs-lookup"><span data-stu-id="4289a-121">Korean</span></span>
1. <span data-ttu-id="4289a-122">폴란드어</span><span class="sxs-lookup"><span data-stu-id="4289a-122">Polish</span></span>
1. <span data-ttu-id="4289a-123">포르투갈어(브라질)</span><span class="sxs-lookup"><span data-stu-id="4289a-123">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="4289a-124">러시아어</span><span class="sxs-lookup"><span data-stu-id="4289a-124">Russian</span></span>
1. <span data-ttu-id="4289a-125">스페인어</span><span class="sxs-lookup"><span data-stu-id="4289a-125">Spanish</span></span>
1. <span data-ttu-id="4289a-126">터키어</span><span class="sxs-lookup"><span data-stu-id="4289a-126">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="4289a-127">Visual Studio 템플릿 여러 사전 설치 된 패키지 저장소를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4289a-127">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="4289a-128">Visual Studio 서식 파일을 생성 하는 경우에 NuGet을 사용할 수 있습니다 [패키지를 사전 설치](../visual-studio-extensibility/visual-studio-templates.md) 서식 파일의 일부로 합니다.</span><span class="sxs-lookup"><span data-stu-id="4289a-128">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="4289a-129">지금까지이 기능에는 제한 사항이 동일한 원본에서 제공 하는 데 필요한 모든 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="4289a-129">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="4289a-130">그러나 2.2.1 NuGet이 포함 된 서식 파일, 한 VSIX 또는 레지스트리에 정의 된 디스크의 폴더) (내 여러 저장소에서 설치 된 패키지 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4289a-130">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="4289a-131">이 기능에 대 한 주요 시나리오 ASP.NET 프로젝트 템플릿 사용자 지정입니다.</span><span class="sxs-lookup"><span data-stu-id="4289a-131">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="4289a-132">기본 제공 ASP.NET 템플릿 로컬 디스크에서 패키지를 풀링 하는 사전 설치 된 패키지를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4289a-132">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="4289a-133">이제 ASP.NET에서 설치 된 기존 패키지를 사용 하는 사용자 지정 ASP.NET 프로젝트 템플릿을 만들 수 있지만 서식 파일에 추가 NuGet 패키지를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="4289a-133">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="4289a-134">버그 수정</span><span class="sxs-lookup"><span data-stu-id="4289a-134">Bug Fixes</span></span>
<span data-ttu-id="4289a-135">NuGet 2.2.1 대상으로 지정 된 몇 가지 버그 수정 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4289a-135">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="4289a-136">작업 목록에 대 한 항목에서에서 수정 된 NuGet 2.2.1 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)합니다.</span><span class="sxs-lookup"><span data-stu-id="4289a-136">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="4289a-137">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="4289a-137">Known Issues</span></span>

<span data-ttu-id="4289a-138">모든 사전 설치 된 패키지 저장소에 대 한 동일한 값을 사용 해야 ASP.NET 프로젝트 템플릿을 확장 하는 경우는 `isPreunzipped` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="4289a-138">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
