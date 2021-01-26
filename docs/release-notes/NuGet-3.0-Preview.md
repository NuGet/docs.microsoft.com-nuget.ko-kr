---
title: NuGet 3.0 Preview 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 포함 하는 NuGet 3.0 미리 보기에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ecaed21c5e689a488e033404f8042cd1f17eed0d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780329"
---
# <a name="nuget-30-preview-release-notes"></a><span data-ttu-id="75a8e-103">NuGet 3.0 Preview 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="75a8e-103">NuGet 3.0 Preview Release Notes</span></span>

<span data-ttu-id="75a8e-104">[NuGet 2.9 RC 릴리스 정보](../release-notes/nuget-2.9-rc.md)  |  [NuGet 3.0 베타 릴리스 정보](../release-notes/nuget-3.0-beta.md)</span><span class="sxs-lookup"><span data-stu-id="75a8e-104">[NuGet 2.9 RC Release Notes](../release-notes/nuget-2.9-rc.md) | [NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md)</span></span>

<span data-ttu-id="75a8e-105">NuGet 3.0 미리 보기는 Visual Studio 2015 Preview 릴리스의 일부로 2014 년 11 월 12 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-105">NuGet 3.0 Preview was released on November 12, 2014 as part of the Visual Studio 2015 Preview release.</span></span> <span data-ttu-id="75a8e-106">NuGet 3.0 미리 보기가 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-106">We released NuGet 3.0 Preview.</span></span> <span data-ttu-id="75a8e-107">이 릴리스는 미리 보기를 소개 하는 대규모 릴리스 이며 변경 내용에 대 한 피드백을 제공 하기 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-107">This is a big release for us (albeit a preview), and we're excited to start getting feedback on our changes.</span></span>

## <a name="visual-studio-2012"></a><span data-ttu-id="75a8e-108">Visual Studio 2012 +</span><span class="sxs-lookup"><span data-stu-id="75a8e-108">Visual Studio 2012+</span></span>

<span data-ttu-id="75a8e-109">이 NuGet 3.0 미리 보기는 Visual Studio 2015 Preview에 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-109">This NuGet 3.0 Preview is included in Visual Studio 2015 Preview.</span></span> <span data-ttu-id="75a8e-110">Visual Studio 2012 및 Visual Studio 2013에 대 한 미리 보기를 제공 하기 위해 노력 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-110">We are working to get preview drops out for Visual Studio 2012 and Visual Studio 2013 very soon.</span></span> <span data-ttu-id="75a8e-111">이전에는 [Visual Studio 2010에 대 한 업데이트를 중단](http://blog.nuget.org/20141002/visual-studio-2010.html)하는 것을 이전에 공유 했으며,이는 어려운 결정을 내리는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-111">We previously shared our intent to [discontinue updates for Visual Studio 2010](http://blog.nuget.org/20141002/visual-studio-2010.html), and we did make that difficult decision.</span></span>

## <a name="brand-new-ui"></a><span data-ttu-id="75a8e-112">브랜드 새 UI</span><span class="sxs-lookup"><span data-stu-id="75a8e-112">Brand New UI</span></span>

<span data-ttu-id="75a8e-113">NuGet 3.0 Preview에 대 한 첫 번째 사항은 새로운 UI입니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-113">The first thing you notice about NuGet 3.0 Preview is our brand new UI.</span></span> <span data-ttu-id="75a8e-114">더 이상 모달 대화 상자가 아닙니다. 이제 전체 Visual Studio 문서 창입니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-114">It's no longer a modal dialog; it's now a full Visual Studio document window.</span></span> <span data-ttu-id="75a8e-115">이를 통해 여러 프로젝트 (및/또는 솔루션)에 대 한 UI를 한 번에 열 수 있으며, 창을 다른 모니터로 분리 하 여 원하는 방식으로 도킹할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-115">This allows you to open the UI for multiple projects (and/or the solution) at once, tear the window off to another monitor, dock it however you'd like, etc.</span></span>

![새 NuGet UI](./media/NuGet-3.0-Preview/new-ui.png)

<span data-ttu-id="75a8e-117">모달 대화 상자를 포기 하는 것으로 인 한 유용성 차이 외에도 새 UI에 새로운 기능이 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-117">Beyond the usability differences because of abandoning the modal dialog, we also have lots of new features in the new UI.</span></span>

### <a name="version-selection"></a><span data-ttu-id="75a8e-118">버전 선택</span><span class="sxs-lookup"><span data-stu-id="75a8e-118">Version Selection</span></span>

<span data-ttu-id="75a8e-119">가장 많이 요청 되는 UI 기능은 패키지 설치 및 업데이트에 대 한 버전 선택을 허용 하는 것입니다. 이제 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-119">Perhaps the most requested UI feature is to allow version selection for package installation and update--this is now available.</span></span>

![패키지 버전 선택](./media/NuGet-3.0-Preview/version-selection.png)

<span data-ttu-id="75a8e-121">패키지를 설치 하거나 업데이트 하는 경우 버전 드롭다운을 사용 하 여 패키지에 사용할 수 있는 모든 버전을 확인할 수 있습니다 .이를 통해 쉽게 선택할 수 있도록 목록 맨 위에 몇 가지 주목할 만한 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-121">Whether you are installing or updating a package, the version dropdown allows you to see all of the versions available for the package, with some notable versions promoted to the top of the list for easy selection.</span></span> <span data-ttu-id="75a8e-122">더 이상 PowerShell 콘솔을 사용 하 여 최신 버전이 아닌 특정 버전을 가져올 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-122">You no longer need to use the PowerShell Console to get specific versions that are not the latest.</span></span>

### <a name="combined-installedonlineupdates-workflows"></a><span data-ttu-id="75a8e-123">통합 설치/온라인/업데이트 워크플로</span><span class="sxs-lookup"><span data-stu-id="75a8e-123">Combined Installed/Online/Updates Workflows</span></span>

<span data-ttu-id="75a8e-124">이전 UI에는 설치, 온라인 및 업데이트를 위한 3 개의 탭이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-124">Our previous UI had 3 tabs for Installed, Online, and Updates.</span></span> <span data-ttu-id="75a8e-125">나열 된 패키지는 해당 워크플로와 관련 된 것 이며 사용 가능한 작업은 워크플로와 관련 된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-125">The packages listed were specific to those workflows and the actions available were specific to the workflows as well.</span></span> <span data-ttu-id="75a8e-126">이는 논리적인 것으로 생각 되는 경우가 많기 때문에 대부분의 경우 이러한 구분으로 인해 발생 하는 경우가 많았습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-126">While that seemed logical, we heard that many of you would often get tripped up by this separation.</span></span>

<span data-ttu-id="75a8e-127">이제 패키지를 선택 하는 방법에 관계 없이 패키지를 설치, 업데이트 또는 제거할 수 있는 결합 된 환경이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-127">We now have a combined experience, where you can install, update, or uninstall a package regardless of how you got the package selected.</span></span> <span data-ttu-id="75a8e-128">특정 워크플로를 지원 하기 위해 이제 표시 되는 패키지를 필터링 할 수 있는 필터 드롭다운이 있지만 패키지에 사용할 수 있는 작업은 일관 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-128">To assist with the specific workflows, we now have a Filter dropdown that lets you filter the packages visible, but then the actions available for the package are consistent.</span></span>

![패키지 제거](./media/NuGet-3.0-Preview/uninstall-package.png)

<span data-ttu-id="75a8e-130">"설치 됨" 필터를 사용 하면 업데이트를 사용할 수 있는 패키지를 쉽게 볼 수 있으며, 버전 선택을 변경 하 여 사용 가능한 작업 변경을 확인 하 여 패키지를 제거 하거나 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-130">By using the "Installed" filter, you can then easily see your installed packages, which ones have updates available, and then you can either uninstall or update the package by changing the version selection to see change the action available.</span></span>

![패키지 업데이트](./media/NuGet-3.0-Preview/update-package.png)

### <a name="version-consolidation"></a><span data-ttu-id="75a8e-132">버전 통합</span><span class="sxs-lookup"><span data-stu-id="75a8e-132">Version Consolidation</span></span>

<span data-ttu-id="75a8e-133">솔루션 내에서 여러 프로젝트에 동일한 패키지를 설치 하는 것이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-133">It's common to have the same package installed into multiple projects within your solution.</span></span> <span data-ttu-id="75a8e-134">경우에 따라 각 프로젝트에 설치 되는 버전이 늘어날 수 있으며 사용 중인 버전을 통합 하는 데 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-134">Sometimes the versions installed into each project can drift apart and it's necessary to consolidate the versions in use.</span></span> <span data-ttu-id="75a8e-135">NuGet 3.0 Preview에는이 시나리오에 대 한 새로운 기능이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-135">NuGet 3.0 Preview introduces a new feature for just this scenario.</span></span>

<span data-ttu-id="75a8e-136">솔루션을 마우스 오른쪽 단추로 클릭 하 고 솔루션용 NuGet 패키지 관리를 선택 하 여 솔루션 수준 패키지 관리 창에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-136">The solution-level package management window can be accessed by right-clicking on the solution and choosing Manage NuGet Packages for Solution.</span></span> <span data-ttu-id="75a8e-137">여기에서 여러 프로젝트에 설치 된 패키지를 선택 하 고 다른 버전을 사용 하는 경우 새로운 "통합" 작업을 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-137">From there, if you select a package that is installed into multiple projects, but with different versions in use, a new "Consolidate" action becomes available.</span></span> <span data-ttu-id="75a8e-138">아래 스크린샷에서는를 사용 하 여에 `Newtonsoft.Json` 설치 되 `SamplesClassLibrary` `6.0.4` 고 버전의에 설치 되었습니다 `SamplesConsoleApp` `5.0.4` .</span><span class="sxs-lookup"><span data-stu-id="75a8e-138">In the screen shot below, `Newtonsoft.Json` was installed into the `SamplesClassLibrary` with version `6.0.4` and installed into `SamplesConsoleApp` with version `5.0.4`.</span></span>

![버전 통합](./media/NuGet-3.0-Preview/consolidate.png)

<span data-ttu-id="75a8e-140">단일 버전으로 통합 하기 위한 워크플로는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-140">Here's the workflow for consolidating onto a single version.</span></span>

1. <span data-ttu-id="75a8e-141">목록에서 패키지를 선택 합니다. `Newtonsoft.Json`</span><span class="sxs-lookup"><span data-stu-id="75a8e-141">Select the `Newtonsoft.Json` package in the list</span></span>
1. <span data-ttu-id="75a8e-142">`Consolidate` `Action` 드롭다운에서 선택</span><span class="sxs-lookup"><span data-stu-id="75a8e-142">Choose `Consolidate` from the `Action` dropdown</span></span>
1. <span data-ttu-id="75a8e-143">드롭다운을 사용 `Version` 하 여 통합할 버전을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-143">Use the `Version` dropdown to select the version to be consolidated onto</span></span>
1. <span data-ttu-id="75a8e-144">해당 버전에 통합 해야 하는 프로젝트의 확인란을 선택 합니다. 선택한 버전에 이미 있는 프로젝트는 회색으로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-144">Check the boxes for the projects that should be consolidated onto that version (note that projects already on the selected version will be greyed out)</span></span>
1. <span data-ttu-id="75a8e-145">단추를 클릭 `Consolidate` 하 여 통합을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-145">Click the `Consolidate` button to perform the consolidation</span></span>

### <a name="operation-previews"></a><span data-ttu-id="75a8e-146">작업 미리 보기</span><span class="sxs-lookup"><span data-stu-id="75a8e-146">Operation Previews</span></span>

<span data-ttu-id="75a8e-147">수행 중인 작업 (설치/업데이트/제거)에 관계 없이 이제 새 UI는 프로젝트에 적용 되는 변경 내용을 미리 볼 수 있는 방법을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-147">Regardless of which operation you're performing--install/update/uninstall--the new UI now offers a way to preview the changes that will be made to your project.</span></span> <span data-ttu-id="75a8e-148">이 미리 보기에는 설치 되는 새 패키지, 업데이트 되는 패키지 및 제거 될 패키지와 함께 작업 중에 변경 되지 않을 패키지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-148">This preview will show any new packages that will be installed, packages that will be updated, and packages that will be uninstalled, along with packages that will be unchanged during the operation.</span></span>

<span data-ttu-id="75a8e-149">아래 예제에서는 SignalR를 설치 하면 프로젝트가 크게 변경 되는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-149">In the example below, we can see that installing Microsoft.AspNet.SignalR will result in quite a few changes to the project.</span></span>

![SignalR 설치 미리 보기](./media/NuGet-3.0-Preview/preview.png)

### <a name="installation-options"></a><span data-ttu-id="75a8e-151">설치 옵션</span><span class="sxs-lookup"><span data-stu-id="75a8e-151">Installation Options</span></span>

<span data-ttu-id="75a8e-152">PowerShell 콘솔을 사용 하 여 몇 가지 주목할 만한 설치 옵션을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-152">Using the PowerShell Console, you've had control over a couple of notable installation options.</span></span> <span data-ttu-id="75a8e-153">이제 이러한 기능을 UI로 가져왔습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-153">We've now brought those features into the UI as well.</span></span> <span data-ttu-id="75a8e-154">이제 종속성의 버전을 선택 하는 방법에 대 한 종속성 확인 동작을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-154">You can now control the dependency resolution behavior for how versions of the dependencies are selected.</span></span>

![종속성 동작](./media/NuGet-3.0-Preview/dependency-behavior.png)

<span data-ttu-id="75a8e-156">패키지의 콘텐츠 파일이 이미 프로젝트에 있는 파일과 충돌 하는 경우 수행할 작업을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-156">You can also specify the action to take when content files from packages conflict with files already in your project.</span></span>

![파일 충돌 동작](./media/NuGet-3.0-Preview/file-conflict-action.png)

### <a name="infinite-scrolling"></a><span data-ttu-id="75a8e-158">무한 스크롤</span><span class="sxs-lookup"><span data-stu-id="75a8e-158">Infinite Scrolling</span></span>

<span data-ttu-id="75a8e-159">패키지를 나열할 때 스크롤 및 페이징 패러다임을 모두 포함 하는 UI에 대 한 피드백을 상당히 조금 활용 하는 데 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-159">We used to get quite a bit of feedback on our UI having both the scrolling and paging paradigms when listing packages.</span></span> <span data-ttu-id="75a8e-160">짧은 목록의 맨 아래로 스크롤하고 다음 페이지 번호를 클릭 한 다음 다시 스크롤해야 하는 것이 매우 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-160">It was pretty common to have to scroll to the bottom of the short list, click the next page number, and then scroll again.</span></span> <span data-ttu-id="75a8e-161">새 UI를 사용 하면 페이지를 스크롤 하지 않아도 되도록 패키지 목록에서 무한 스크롤을 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-161">With the new UI, we've implemented infinite scrolling in the package list so that you only need to scroll--no more paging.</span></span>

![무한 스크롤](./media/NuGet-3.0-Preview/infinite-scrolling.png)

### <a name="make-it-work-make-it-fast-make-it-pretty"></a><span data-ttu-id="75a8e-163">작업을 수행 하 고 신속 하 게 만들어 편리 하 게 만드세요.</span><span class="sxs-lookup"><span data-stu-id="75a8e-163">Make it Work, Make it Fast, Make it Pretty</span></span>

<span data-ttu-id="75a8e-164">이 새로운 UI를 사용해 볼 수 있습니다. 이 미리 보기 마일스 톤 중에 "it를 작동 하 고, 신속 하 게 만들어 보세요." 라는 좋은 이전 말라.</span><span class="sxs-lookup"><span data-stu-id="75a8e-164">We are excited to get this new UI out for you to try out. During this Preview milestone, we've been following the good old adage of "Make it work, make it fast, make it pretty."</span></span> <span data-ttu-id="75a8e-165">이 미리 보기에서는 가장 먼저 목표를 달성 했습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-165">In this preview, we've accomplished most of that first goal--it works.</span></span> <span data-ttu-id="75a8e-166">아직 빠르지는 않지만 아직 확실 하지 않은 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-166">We know it's not quite fast yet, and we know it's not quite pretty yet.</span></span> <span data-ttu-id="75a8e-167">현재와 RC 릴리스 간에 해당 목표에 대 한 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-167">Trust that we'll be working on those goals between now and the RC release.</span></span> <span data-ttu-id="75a8e-168">그 동안에는 새로운 UI의 *유용성* (워크플로, 작업 및 새 ui를 *사용 하는* 방법)에 대 한 의견을 보내 주시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-168">In the meantime, we would love to hear your feedback about the *usability* of the new UI--the workflows, operations, and how it *feels* to use the new UI.</span></span>

<span data-ttu-id="75a8e-169">이전 UI와 비교할 때 제거 된 두 가지 함수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-169">There are a couple of functions that we've removed when compared to the old UI.</span></span> <span data-ttu-id="75a8e-170">이러한 항목 중 하나는 의도적인 것이 고 다른 하나는 제때에 수행 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-170">One of these was intentional, and the other one just didn't get done in time.</span></span>

#### <a name="searching-all-package-sources"></a><span data-ttu-id="75a8e-171">"모든" 패키지 원본 검색</span><span class="sxs-lookup"><span data-stu-id="75a8e-171">Searching "All" Package Sources</span></span>

<span data-ttu-id="75a8e-172">이전 UI를 통해 모든 패키지 원본에 대해 패키지 검색을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-172">The old UI allowed you to perform a package search against all of your package sources.</span></span> <span data-ttu-id="75a8e-173">UI에서 해당 기능을 제거 하 고 다시 가져오는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-173">We've removed that feature in the UI and we won't be bringing it back.</span></span> <span data-ttu-id="75a8e-174">이 기능은 모든 패키지 소스에 대해 검색 작업을 수행 하 고 결과를 함께 직물 하 고 정렬 선택에 따라 결과를 정렬 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-174">This feature used to perform search operations against all of your package sources, weave the results together, and attempt to order the results based on your sorting selection.</span></span>

<span data-ttu-id="75a8e-175">검색 관련성은 정말 함께 직물를 형성 하기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-175">We found that search relevance is really hard to weave together.</span></span> <span data-ttu-id="75a8e-176">Google 및 Bing에 대해 검색을 수행 하 고 결과를 함께 weaving 할 수 있나요?</span><span class="sxs-lookup"><span data-stu-id="75a8e-176">Could you imagine performing a search against Google and Bing and weaving the results together?</span></span> <span data-ttu-id="75a8e-177">또한이 기능은 느리고 *실수로* 사용 하기 쉬우며 실제로는 거의 유용 하지 않다고 생각 합니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-177">Additionally, this feature was slow, easy to *accidentally* use, and we believe it was rarely actually useful.</span></span> <span data-ttu-id="75a8e-178">기능이 도입 된 문제로 인해 수정 되지 않았을 수 있는 많은 버그 보고서를 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-178">Because of the problems the feature introduced, we received a number of bug reports on it that could never have been fixed.</span></span>

#### <a name="update-all"></a><span data-ttu-id="75a8e-179">모두 업데이트</span><span class="sxs-lookup"><span data-stu-id="75a8e-179">Update All</span></span>

<span data-ttu-id="75a8e-180">이전 UI에서 아직 새 UI에 없는 "모두 업데이트" 단추를 사용 했습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-180">We used to have an "Update All" button in the old UI that isn't there in the new UI yet.</span></span> <span data-ttu-id="75a8e-181">RC 릴리스에 대해이 기능을 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-181">We will resurrect this feature for our RC release.</span></span>

## <a name="new-clientserver-api"></a><span data-ttu-id="75a8e-182">새 클라이언트/서버 API</span><span class="sxs-lookup"><span data-stu-id="75a8e-182">New Client/Server API</span></span>

<span data-ttu-id="75a8e-183">새 패키지 관리 UI의 모든 새로운 기능 외에도 NuGet의 클라이언트/서버 프로토콜에 대 한 몇 가지 구현 정보를 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-183">In addition to all of the new features in our new package management UI, we've also been working on some implementation details for NuGet's client/server protocol.</span></span> <span data-ttu-id="75a8e-184">수행한 작업은 패키지 복원 및 패키지 설치와 같은 중요 한 시나리오에 대 한 고가용성을 중심으로 작성 된 NuGet에 대해 "API v3"을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-184">The work we've done is to create "API v3" for NuGet, which is designed around high availability for critical scenarios such as package restore and installing packages.</span></span> <span data-ttu-id="75a8e-185">새 API는 REST 및 하이퍼 미디어를 기반으로 하며, [JSON-LD](http://json-ld.org) 를 리소스 형식으로 선택 했습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-185">The new API is based on REST and Hypermedia and we've selected [JSON-LD](http://json-ld.org) as our resource format.</span></span>

<span data-ttu-id="75a8e-186">NuGet 3.0 미리 보기 비트에는 패키지 원본 드롭다운에서 "preview.nuget.org" 라는 새 패키지 원본이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-186">In the NuGet 3.0 Preview bits, you see a new package source called "preview.nuget.org" in the package source dropdown.</span></span> <span data-ttu-id="75a8e-187">해당 패키지 원본을 선택 하는 경우 nuget.org에 연결 하는 대신 새 API를 사용 합니다. 새 API를 계속 테스트 하 고 수정 하 고 개선 하는 동안 UI에서 미리 보기 원본을 사용할 수 있게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-187">If you select that package source, we'll use our new API rather to connect to nuget.org. We've made the preview source available in the UI while we continue to test, revise, and improve the new API.</span></span> <span data-ttu-id="75a8e-188">NuGet 3.0 RC에서이 새 API v3 기반 패키지 원본은 v2 기반 "nuget.org" 패키지 원본을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-188">In NuGet 3.0 RC, this new API v3-based package source will replace the v2-based "nuget.org" package source.</span></span>

<span data-ttu-id="75a8e-189">API v3에 배치 하는 투자에도 불구 하 고 기존 API v2 프로토콜을 사용 하 여 이러한 새로운 기능을 모두 사용할 수 있습니다. 즉, nuget.org 이외의 기존 패키지 원본 에서도 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-189">Despite the investment we're putting into API v3, we've made all of these new features also work with our existing API v2 protocol, which means they will work with existing package sources other than nuget.org as well.</span></span>

## <a name="new-features-coming"></a><span data-ttu-id="75a8e-190">새 기능 출시</span><span class="sxs-lookup"><span data-stu-id="75a8e-190">New Features Coming</span></span>

<span data-ttu-id="75a8e-191">현재와 3.0 RTM 사이에서 UI에 표시 되는 것 외에도 몇 가지 기본적인 새로운 NuGet 기능을 작업 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-191">Between now and 3.0 RTM, we are also working on some fundamental new NuGet features, beyond what you see in the UI.</span></span> <span data-ttu-id="75a8e-192">다음은 두드러진 몇 가지 투자 영역에 대 한 간단한 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-192">Here's a short list of salient investment areas:</span></span>

1. <span data-ttu-id="75a8e-193">Microsoft는 Visual Studio 및 MSBuild 팀과 협력 하 여 [플랫폼에 더 심층적](http://blog.nuget.org/20141014/in-the-platform.html)으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-193">We're partnering with the Visual Studio and MSBuild teams to get [NuGet deeper into the platform](http://blog.nuget.org/20141014/in-the-platform.html).</span></span>
1. <span data-ttu-id="75a8e-194">설치 시간 패키지 규칙을 중단 하 고 대신 새 "신뢰할 수 있는" [패키지 매니페스트](http://blog.nuget.org/20141023/package-manifests.html)를 도입 하 여 패키징 시간에 이러한 규칙을 적용 하기 위해 노력 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-194">We're working to abandon installation-time package conventions and instead apply those conventions at packaging time by introducing a new "authoritative" [package manifest](http://blog.nuget.org/20141023/package-manifests.html).</span></span>
1. <span data-ttu-id="75a8e-195">NuGet 코드 베이스를 리팩터링하여 클라이언트 및 서버 구성 요소를 Visual Studio의 패키지 관리를 통해 다른 도메인에서 다시 사용할 수 있도록 하기 위해 노력 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-195">We're working to refactor the NuGet codebase to make the client and server components reusable in different domains beyond package management in Visual Studio.</span></span>
1. <span data-ttu-id="75a8e-196">패키지에서 구현 세부 정보에 대해서만 다른 패키지에 대 한 종속성이 있음을 나타낼 수 있고 이러한 종속성을 최상위 종속성으로 표시 하지 않는 "개인 종속성"의 개념을 조사 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75a8e-196">We're investigating the notion of "private dependencies" where a package can indicate that it has dependencies on other packages for implementation details only, and those dependencies shouldn't be surfaced as top-level dependencies.</span></span>

## <a name="stay-tuned"></a><span data-ttu-id="75a8e-197">계속 조정</span><span class="sxs-lookup"><span data-stu-id="75a8e-197">Stay Tuned</span></span>

<span data-ttu-id="75a8e-198">NuGet 3.0에 대 한 자세한 진행률과 공지 사항은 [블로그](http://blog.nuget.org) 를 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="75a8e-198">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>