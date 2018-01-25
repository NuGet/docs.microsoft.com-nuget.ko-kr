---
title: "NuGet 3.0 미리 보기 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 3.0 미리 보기에 대 한 릴리스 정보입니다."
keywords: "NuGet 3.0 미리 보기 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e07bcad2bf713deee0add72663c84b9979f8c5c4
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-30-preview-release-notes"></a><span data-ttu-id="443e0-104">NuGet 3.0 미리 보기 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="443e0-104">NuGet 3.0 Preview Release Notes</span></span>

<span data-ttu-id="443e0-105">[NuGet 2.9 RC 릴리스 정보](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 베타 릴리스 정보](../release-notes/nuget-3.0-beta.md)</span><span class="sxs-lookup"><span data-stu-id="443e0-105">[NuGet 2.9 RC Release Notes](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md)</span></span>

<span data-ttu-id="443e0-106">NuGet 3.0 미리 보기는 Visual Studio 2015 Preview 릴리스의 일부로 서 2014 년 11 월 12 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-106">NuGet 3.0 Preview was released on November 12, 2014 as part of the Visual Studio 2015 Preview release.</span></span> <span data-ttu-id="443e0-107">NuGet 3.0 미리 보기를 발표 했습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-107">We released NuGet 3.0 Preview.</span></span> <span data-ttu-id="443e0-108">이 us에 대 한 큰 릴리스 (하지만 미리 보기), 기능 변경 내용이에 피드백 시작 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-108">This is a big release for us (albeit a preview), and we're excited to start getting feedback on our changes.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="443e0-109">Visual Studio 2012+</span><span class="sxs-lookup"><span data-stu-id="443e0-109">Visual Studio 2012+</span></span>

<span data-ttu-id="443e0-110">이 NuGet 3.0 미리 보기는 Visual Studio 2015 Preview에 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-110">This NuGet 3.0 Preview is included in Visual Studio 2015 Preview.</span></span> <span data-ttu-id="443e0-111">가져오려는 미리 보기 삭제 Visual Studio 2012 및 Visual Studio 2013에 대 한 가능한 한 빨리 노력 하 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-111">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="443e0-112">에서는 이전에 공유 우리의 의도 [Visual Studio 2010에 대 한 업데이트를 중단](http://blog.nuget.org/20141002/visual-studio-2010.html), 해당 어려운 결정 하도록 않았습니다 고 합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-112">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="brand-new-ui"></a><span data-ttu-id="443e0-113">새 브랜드 UI</span><span class="sxs-lookup"><span data-stu-id="443e0-113">Brand New UI</span></span>

<span data-ttu-id="443e0-114">가장 먼저 NuGet 3.0 미리 보기에 대 한 알 수 있습니다 하 새로운 UI입니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-114">The first thing you'll notice about NuGet 3.0 Preview is our brand new UI.</span></span> <span data-ttu-id="443e0-115">더 이상; 모달 대화 상자 이제 전체 Visual Studio 문서 창입니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-115">It's no longer a modal dialog; it's now a full Visual Studio document window.</span></span> <span data-ttu-id="443e0-116">이 옵션을 사용 하면 한 번에 여러 프로젝트 (및 솔루션)에 대 한 UI를 열고, 다른 모니터에 창을 분리, 있지만 좋아요 등은 고정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-116">This allows you to open the UI for multiple projects (and/or the solution) at once, tear the window off to another monitor, dock it however you'd like, etc.</span></span>

![새 NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

<span data-ttu-id="443e0-118">모달 대화 상자를 중단으로 인해 유용성 차이 외도 다양 한 새로운 기능에에서 있는 새 UI입니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-118">Beyond the usability differences because of abandoning the modal dialog, we also have lots of new features in the new UI.</span></span>

### <a name="version-selection"></a><span data-ttu-id="443e0-119">버전 선택</span><span class="sxs-lookup"><span data-stu-id="443e0-119">Version Selection</span></span>

<span data-ttu-id="443e0-120">아마도 가장 요청한 UI 기능은 패키지를 설치 및 업데이트-에 대 한 버전 선택을 허용 하는 것이 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-120">Perhaps the most requested UI feature is to allow version selection for package installation and update--this is now available.</span></span>

![패키지 버전 선택](./media/NuGet-3.0-Preview/version-selection.png)

<span data-ttu-id="443e0-122">설치 하거나 패키지를 업데이트 하는 지 여부를 버전 드롭다운을 사용 하는 모든 사용자가 쉽게 선택할 목록의 처음으로 승격 하는 몇 가지 주목할 만한 버전 패키지에 사용할 수 있는 버전을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-122">Whether you are installing or updating a package, the version dropdown allows you to see all of the versions available for the package, with some notable versions promoted to the top of the list for easy selection.</span></span> <span data-ttu-id="443e0-123">PowerShell 콘솔을 사용 하 여 최신 하지 않은 특정 버전 가져오기 더 이상 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-123">You no longer need to use the PowerShell Console to get specific versions that are not the latest.</span></span>

### <a name="combined-installedonlineupdates-workflows"></a><span data-ttu-id="443e0-124">설치 된/온라인/업데이트 워크플로 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-124">Combined Installed/Online/Updates Workflows</span></span>

<span data-ttu-id="443e0-125">이전 UI 설치 됨, 온라인 및 업데이트 3 개의 탭 수 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-125">Our previous UI had 3 tabs for Installed, Online, and Updates.</span></span> <span data-ttu-id="443e0-126">나열 된 패키지 워크플로의 관련 값과 수행할 수 있는 않은 워크플로에 특정 합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-126">The packages listed were specific to those workflows and the actions available were specific to the workflows as well.</span></span> <span data-ttu-id="443e0-127">논리 소식이, 종종는 여러분의 의견은 동안이 분리 하 여 중단점이 가져오기.</span><span class="sxs-lookup"><span data-stu-id="443e0-127">While that seemed logical, we heard that many of you would often get tripped up by this separation.</span></span>

<span data-ttu-id="443e0-128">결합 된 경험을 하거나 수 있는 설치, 업데이트, 선택한 패키지를 가져온 방법에 관계 없이 패키지를 제거 했습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-128">We now have a combined experience, where you can install, update, or uninstall a package regardless of how you got the package selected.</span></span> <span data-ttu-id="443e0-129">을 지원 하기 위해 특정 워크플로 사용 하 여 이제 있다고 표시 되는 패키지를 필터링 할 수 있는 필터 드롭다운 하지만 패키지에 대해 사용할 수 있는 작업에 일관성이 다음 합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-129">To assist with the specific workflows, we now have a Filter dropdown that lets you filter the packages visible, but then the actions available for the package are consistent.</span></span>

![패키지를 제거 합니다.](./media/NuGet-3.0-Preview/uninstall-package.png)

<span data-ttu-id="443e0-131">"설치 됨" 필터를 사용 하 여 확인할 수 있습니다 쉽게 사항이 사용 가능한 업데이트를 설치 된 패키지에서 및 다음를 제거 하거나 보려면 버전 선택 변경 하 여 패키지를 업데이트할 사용 가능한 동작을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-131">By using the "Installed" filter, you can then easily see your installed packages, which ones have updates available, and then you can either uninstall or update the package by changing the version selection to see change the action available.</span></span>

![패키지 업데이트](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a><span data-ttu-id="443e0-133">버전 통합</span><span class="sxs-lookup"><span data-stu-id="443e0-133">Version Consolidation</span></span>

<span data-ttu-id="443e0-134">일반적으로 동일한 솔루션 내에서 여러 프로젝트에 설치 된 패키지는 이며</span><span class="sxs-lookup"><span data-stu-id="443e0-134">It's common to have the same package installed into multiple projects within your solution.</span></span> <span data-ttu-id="443e0-135">경우에 따라 각 프로젝트에 설치 된 버전 떨어져 있는 드리프트 수 및 사용 중인 버전을 통합 해야 하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-135">Sometimes the versions installed into each project can drift apart and it's necessary to consolidate the versions in use.</span></span> <span data-ttu-id="443e0-136">NuGet 3.0 미리 보기에는이 시나리오에 새 기능이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-136">NuGet 3.0 Preview introduces a new feature for just this scenario.</span></span>

<span data-ttu-id="443e0-137">솔루션 수준의 패키지 관리 창에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 솔루션에 대 한 NuGet 패키지 관리를 선택 하 여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-137">The solution-level package management window can be accessed by right-clicking on the solution and choosing Manage NuGet Packages for Solution.</span></span> <span data-ttu-id="443e0-138">여기에서 서로 다른 버전 사용에서 하면서도 여러 프로젝트에 설치 되어 있는 패키지를 선택 하는 경우 새 "통합" 동작을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-138">From there, if you select a package that is installed into multiple projects, but with different versions in use, a new "Consolidate" action becomes available.</span></span> <span data-ttu-id="443e0-139">화면 아래에 `Newtonsoft.Json` 에 설치 된는 `SamplesClassLibrary` 버전과 `6.0.4` 하 고에 설치 된 `SamplesConsoleApp` 버전과 `5.0.4`합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-139">In the screen shot below, `Newtonsoft.Json` was installed into the `SamplesClassLibrary` with version `6.0.4` and installed into `SamplesConsoleApp` with version `5.0.4`.</span></span>

![버전 통합](./media/NuGet-3.0-Preview/consolidate.png)

<span data-ttu-id="443e0-141">다음은 단일 버전으로 통합을 위한 워크플로입니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-141">Here's the workflow for consolidating onto a single version.</span></span>

1. <span data-ttu-id="443e0-142">선택 된 `Newtonsoft.Json` 목록에는 패키지</span><span class="sxs-lookup"><span data-stu-id="443e0-142">Select the `Newtonsoft.Json` package in the list</span></span>
1. <span data-ttu-id="443e0-143">선택 `Consolidate` 에서 `Action` 드롭다운</span><span class="sxs-lookup"><span data-stu-id="443e0-143">Choose `Consolidate` from the `Action` dropdown</span></span>
1. <span data-ttu-id="443e0-144">사용 하 여 `Version` 버전으로 통합할 수을 선택 하는 드롭다운</span><span class="sxs-lookup"><span data-stu-id="443e0-144">Use the `Version` dropdown to select the version to be consolidated onto</span></span>
1. <span data-ttu-id="443e0-145">해당 버전 (이미 선택된 된 버전의 프로젝트를 사용할 수 있는 참고)에 통합 해야 하는 프로젝트에 대 한 확인란을 선택</span><span class="sxs-lookup"><span data-stu-id="443e0-145">Check the boxes for the projects that should be consolidated onto that version (note that projects already on the selected version will be greyed out)</span></span>
1. <span data-ttu-id="443e0-146">클릭는 `Consolidate` 통합을 수행 하는 단추</span><span class="sxs-lookup"><span data-stu-id="443e0-146">Click the `Consolidate` button to perform the consolidation</span></span>

### <a name="operation-previews"></a><span data-ttu-id="443e0-147">작업 미리 보기</span><span class="sxs-lookup"><span data-stu-id="443e0-147">Operation Previews</span></span>

<span data-ttu-id="443e0-148">-수행 하는 작업에 관계 없이 설치/업데이트/제거-새 UI 이제 제공 프로젝트에 적용 될 변경 내용을 미리 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-148">Regardless of which operation you're performing--install/update/uninstall--the new UI now offers a way to preview the changes that will be made to your project.</span></span> <span data-ttu-id="443e0-149">이 미리 보기에는 모든 새 패키지는이 설치 되지 않는 변경 작업을 하는 동안 패키지와 함께 제거 되며 패키지를 패키지 하 고 업데이트 됩니다 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-149">This preview will show any new packages that will be installed, packages that will be updated, and packages that will be uninstalled, along with packages that will be unchanged during the operation.</span></span>

<span data-ttu-id="443e0-150">아래 예제에서는 Microsoft.AspNet.SignalR 설치 프로젝트에 많은 변경 내용이 발생 합니다 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-150">In the example below, we can see that installing Microsoft.AspNet.SignalR will result in quite a few changes to the project.</span></span>

![SignalR을 설치 하는 미리 보기](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a><span data-ttu-id="443e0-152">설치 옵션</span><span class="sxs-lookup"><span data-stu-id="443e0-152">Installation Options</span></span>

<span data-ttu-id="443e0-153">PowerShell 콘솔을 사용 하는 데는 두 가지 주목할 만한 설치 옵션에 대 한 제어 합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-153">Using the PowerShell Console, you've had control over a couple of notable installation options.</span></span> <span data-ttu-id="443e0-154">이제 UI도에 이러한 기능을 옮겼습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-154">We've now brought those features into the UI as well.</span></span> <span data-ttu-id="443e0-155">이제 종속성의 버전 선택 방법에 대 한 종속성 확인 하는 동작을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-155">You can now control the dependency resolution behavior for how versions of the dependencies are selected.</span></span>

![종속성 동작](./media/NuGet-3.0-Preview/dependency-behavior.png)

<span data-ttu-id="443e0-157">또한 패키지의 콘텐츠 파일이 프로젝트에 이미 있는 파일 충돌 하는 경우 수행할 동작을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-157">You can also specify the action to take when content files from packages conflict with files already in your project.</span></span>

![파일 충돌 작업](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a><span data-ttu-id="443e0-159">무한 스크롤</span><span class="sxs-lookup"><span data-stu-id="443e0-159">Infinite Scrolling</span></span>

<span data-ttu-id="443e0-160">UI에 대 한 피드백의 두 스크롤 필요 상당한 가져오고 패키지를 나열할 때 패러다임을 페이징 하 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-160">We used to get quite a bit of feedback on our UI having both the scrolling and paging paradigms when listing packages.</span></span> <span data-ttu-id="443e0-161">매우 일반적으로 짧은 목록 아래쪽으로 스크롤하여, 다음 페이지 번호를 클릭 한 다음 다시를 스크롤하여는 했습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-161">It was pretty common to have to scroll to the bottom of the short list, click the next page number, and then scroll again.</span></span> <span data-ttu-id="443e0-162">새 UI로 스크롤하여-더 이상 페이징 하기만 하면 되도록 패키지 목록에 무한 스크롤 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-162">With the new UI, we've implemented infinite scrolling in the package list so that you only need to scroll--no more paging.</span></span>

![무한 스크롤](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a><span data-ttu-id="443e0-164">작업을 확인, 빠른, 예쁘게 확인 확인</span><span class="sxs-lookup"><span data-stu-id="443e0-164">Make it Work, Make it Fast, Make it Pretty</span></span>

<span data-ttu-id="443e0-165">이 새 UI를 사용해 볼 수에 대 한 가져올 수 있습니다. 이 미리 보기 마일스 톤 중 지금 까지는의 좋은 이전 속담 다음 "만들기" 작업, 빠른 확인, 멋지게 만들기.</span><span class="sxs-lookup"><span data-stu-id="443e0-165">We are excited to get this new UI out for you to try out. During this Preview milestone, we've been following the good old adage of "Make it work, make it fast, make it pretty."</span></span> <span data-ttu-id="443e0-166">이 미리 보기에서는 대부분 완료 한 첫 번째 그 목표에 해당-의 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-166">In this preview, we've accomplished most of that first goal--it works.</span></span> <span data-ttu-id="443e0-167">매우 빠른를 아직 및 회원님의 매우 꽤 아직 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-167">We know it's not quite fast yet, and we know it's not quite pretty yet.</span></span> <span data-ttu-id="443e0-168">지금은 RC 릴리스 사이의 이러한 목표에서 작업 하는 신뢰 됩니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-168">Trust that we'll be working on those goals between now and the RC release.</span></span> <span data-ttu-id="443e0-169">에 대 한 사용자 의견을 보내 가입 그 동안에 *유용성* 새로운 ui-워크플로, 작업, 및 방법을 것 *느낌* 새 UI를 사용 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-169">In the meantime, we would love to hear your feedback about the *usability* of the new UI--the workflows, operations, and how it *feels* to use the new UI.</span></span>

<span data-ttu-id="443e0-170">이전 UI에 비해 없어졌습니다 함수는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-170">There are a couple of functions that we've removed when compared to the old UI.</span></span> <span data-ttu-id="443e0-171">다음 중 하나를 의도 한 것, 다른 하나 방금 하지 않은 가져오기에 시간.</span><span class="sxs-lookup"><span data-stu-id="443e0-171">One of these was intentional, and the other one just didn't get done in time.</span></span>

#### <a name="searching-all-package-sources"></a><span data-ttu-id="443e0-172">"All" 패키지 소스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-172">Searching "All" Package Sources</span></span>

<span data-ttu-id="443e0-173">이전 UI 모든 패키지 소스에 대해 패키지 검색을 수행 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-173">The old UI allowed you to perform a package search against all of your package sources.</span></span> <span data-ttu-id="443e0-174">UI의 기능을 제거 했습니다 고 म 않습니다 수 상태로 전환 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-174">We've removed that feature in the UI and we won't be bringing it back.</span></span> <span data-ttu-id="443e0-175">모든 패키지 소스에 대 한 검색 작업을 수행 하는 데이 기능은 묶는 결과 하 고 정렬 선택에 따라 결과 정렬 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-175">This feature used to perform search operations against all of your package sources, weave the results together, and attempt to order the results based on your sorting selection.</span></span>

<span data-ttu-id="443e0-176">검색 관련성은 묶는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-176">We found that search relevance is really hard to weave together.</span></span> <span data-ttu-id="443e0-177">Google / Bing에 대 한 검색 결과 함께 구성 하 고 가정 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="443e0-177">Could you imagine performing a search against Google and Bing and weaving the results together?</span></span> <span data-ttu-id="443e0-178">느린, 하기가이 기능을 하는 또한 *실수로* 사용 및 우리 생각 경량 풀링이 실제로 유용한 거의 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-178">Additionally, this feature was slow, easy to *accidentally* use, and we believe it was rarely actually useful.</span></span> <span data-ttu-id="443e0-179">문제로 인해 도입 하는 기능을 수신 했습니다. 수 되지 수정 된 버그 보고서를 다양 합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-179">Because of the problems the feature introduced, we received a number of bug reports on it that could never have been fixed.</span></span>

#### <a name="update-all"></a><span data-ttu-id="443e0-180">모두 업데이트</span><span class="sxs-lookup"><span data-stu-id="443e0-180">Update All</span></span>

<span data-ttu-id="443e0-181">아직 새 ui에서 없는 이전 UI에 "업데이트 모두" 단추를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-181">We used to have an "Update All" button in the old UI that isn't there in the new UI yet.</span></span> <span data-ttu-id="443e0-182">이 RC 버전에 대 한이 기능을 부활 됩니다 했습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-182">We will resurrect this feature for our RC release.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="443e0-183">새 클라이언트/서버 API</span><span class="sxs-lookup"><span data-stu-id="443e0-183">New Client/Server API</span></span>

<span data-ttu-id="443e0-184">모든 새 패키지 관리 UI의에서 새로운 기능 외에도 지금도 작업에 NuGet의 클라이언트/서버 프로토콜에 대 한 일부 구현 세부 정보.</span><span class="sxs-lookup"><span data-stu-id="443e0-184">In addition to all of the new features in our new package management UI, we've also been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="443e0-185">수행한 작업에 대 한 NuGet 패키지를 복원 하 고 패키지를 설치 하는 등의 중요 한 시나리오에 대 한 고가용성 요구에 맞게 설계을 "API v3"를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-185">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="443e0-186">새로운 API REST 기반으로 하며 하이퍼미디어 되 고, 선택한 [JSON LD](http://json-ld.org) 우리의 리소스 형식으로.</span><span class="sxs-lookup"><span data-stu-id="443e0-186">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="443e0-187">NuGet 3.0 미리 보기 비트에서 패키지 소스 드롭다운에 "preview.nuget.org" 라는 새 패키지 소스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-187">In the NuGet 3.0 Preview bits, you'll see a new package source called "preview.nuget.org" in the package source dropdown.</span></span> <span data-ttu-id="443e0-188">해당 패키지 소스를 선택 하는 경우 새 API nuget.org에 연결 하는 대신 사용 합니다. 만들었고 원본 미리 보기 UI에서 사용할 수 있는 동안 테스트, 수정 및 향상 된 새로운 API를 계속 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-188">If you select that package source, we'll use our new API rather to connect to nuget.org. We've made the preview source available in the UI while we continue to test, revise, and improve the new API.</span></span> <span data-ttu-id="443e0-189">NuGet 3.0 RC에서이 새 API v3 기반 패키지 소스를 v2 기반 "nuget.org" 패키지 소스를 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-189">In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>

<span data-ttu-id="443e0-190">API v 3로 올리는 म 투자를 불구 하 고 만들었고의 새로운 기능 모두 우리의 기존 API v2 프로토콜도 nuget.org 이외의 기존 패키지 소스 작업할 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-190">Despite the investment we're putting into API v3, we've made all of these new features also work with our existing API v2 protocol, which means they will work with existing package sources other than nuget.org as well.</span></span>

## <a name="new-features-coming"></a><span data-ttu-id="443e0-191">발생 하는 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="443e0-191">New Features Coming</span></span>

<span data-ttu-id="443e0-192">지금은 사이의 3.0 RTM 제작 하는 또한 몇 가지 기본적인 이외에 새 NuGet 기능, UI에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-192">Between now and 3.0 RTM, we are also working on some fundamental new NuGet features, beyond what you'll see in the UI.</span></span> <span data-ttu-id="443e0-193">측면에 관련 된 특정 투자의 짧은 목록을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-193">Here's a short list of salient investment areas:</span></span>

1. <span data-ttu-id="443e0-194">MSBuild를 가져오려는 팀이 고 Visual Studio와 협력 하는 것 [NuGet 플랫폼으로 깊은](http://blog.nuget.org/20141014/in-the-platform.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-194">We're partnering with the Visual Studio and MSBuild teams to get [NuGet deeper into the platform](http://blog.nuget.org/20141014/in-the-platform.html).</span></span>
1. <span data-ttu-id="443e0-195">설치 시 패키지 규칙 취소 하 고 대신 새 도입 하 여 패키징 시 이러한 규칙을 적용 하기 위해 노력 하 고 "권한 있는" [패키지 매니페스트](http://blog.nuget.org/20141023/package-manifests.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-195">We're working to abandon installation-time package conventions and instead apply those conventions at packaging time by introducing a new "authoritative" [package manifest](http://blog.nuget.org/20141023/package-manifests.html).</span></span>
1. <span data-ttu-id="443e0-196">Visual Studio에서 패키지 관리 이상의 서로 다른 도메인에 클라이언트 및 서버 구성 요소를 다시 사용할 수 있도록 하려면 코드 베이스 NuGet 리팩터링 위해 노력 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-196">We're working to refactor the NuGet codebase to make the client and server components reusable in different domains beyond package management in Visual Studio.</span></span>
1. <span data-ttu-id="443e0-197">패키지 한다는 나타낼 수 있습니다 "개인 종속성"의 개념을 조사 중에, 구현 세부 정보에 대 한 다른 패키지에 종속 있으며 이러한 종속성 최상위 종속성으로 표시 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="443e0-197">We're investigating the notion of "private dependencies" where a package can indicate that it has dependencies on other packages for implementation details only, and those dependencies shouldn't be surfaced as top-level dependencies.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="443e0-198">기대</span><span class="sxs-lookup"><span data-stu-id="443e0-198">Stay Tuned</span></span>

<span data-ttu-id="443e0-199">에 유의 하십시오 [블로그에서](http://blog.nuget.org) 자세한 진행률 및 NuGet 3.0에 대 한 공지 사항!</span><span class="sxs-lookup"><span data-stu-id="443e0-199">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>