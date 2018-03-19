---
title: "NuGet 패키지 찾기 및 선택 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 8886f899-797b-4704-9d16-820b55b71186
description: "NuGet 검색 구문에 대한 세부 정보를 포함하여 프로젝트에 가장 적합한 NuGet 패키지를 찾아 선택하는 방법을 간략히 설명합니다."
keywords: "NuGet 패키지 사용, NuGet 패키지 검색, 가장 적합한 NuGet 패키지, 패키지 결정, 패키지 사용, 패키지 평가, NuGet 검색 구문"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0c52fa237a663fcf227e8336534d344e432523b4
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a><span data-ttu-id="dc3d8-104">프로젝트에 대한 NuGet 패키지 찾기 및 평가</span><span class="sxs-lookup"><span data-stu-id="dc3d8-104">Finding and evaluating NuGet packages for your project</span></span>

<span data-ttu-id="dc3d8-105">모든 .NET 프로젝트를 시작하거나 앱 또는 서비스에 대한 기능적 요구 사항을 확인할 때마다 해당 요구 사항을 충족하는 기존 NuGet 패키지를 사용하여 많은 시간과 노력을 많이 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-105">When starting any .NET project, or whenever you identify a functional need for your app or service, you can save yourself lots of time and trouble by using existing NuGet packages that fulfill that need.</span></span> <span data-ttu-id="dc3d8-106">이러한 패키지는 [nuget.org](http://www.nuget.org/packages/)의 공용 컬렉션 또는 조직이나 다른 제3자가 제공한 전용 원본에서 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-106">These packages can come from the public collection on [nuget.org](http://www.nuget.org/packages/), or a private source that's provided by your organization or another third party.</span></span>

## <a name="finding-packages"></a><span data-ttu-id="dc3d8-107">패키지 찾기</span><span class="sxs-lookup"><span data-stu-id="dc3d8-107">Finding packages</span></span>

<span data-ttu-id="dc3d8-108">nuget.org를 방문하거나 Visual Studio에서 패키지 관리자 UI를 열면 총 다운로드 수를 기준으로 정렬된 패키지 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-108">When you visit nuget.org or open the Package Manager UI in Visual Studio, you see a list of packages sorted by total downloads.</span></span> <span data-ttu-id="dc3d8-109">이렇게 하면 수백만 개의 .NET 프로젝트에서 가장 널리 사용되는 패키지가 바로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-109">This immediately shows you the most widely-used packages across the millions of .NET projects.</span></span> <span data-ttu-id="dc3d8-110">최소한 처음 몇 페이지에 나열된 패키지 중 일부는 프로젝트에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-110">There's a good chance, then, that at least some of the packages listed on the first few pages will be useful in your projects.</span></span>

![가장 인기 있는 패키지를 보여 주는 nuget.org/packages의 기본 보기](media/Finding-01-Popularity.png)

<span data-ttu-id="dc3d8-112">페이지의 오른쪽 위에 **시험판 포함** 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-112">Notice the **Include prerelease** option on the upper right of the page.</span></span> <span data-ttu-id="dc3d8-113">이 옵션을 선택하면 nuget.org에서 베타 및 기타 초기 릴리스를 포함한 모든 패키지 버전을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-113">When selected, nuget.org shows all versions of packages including beta and other early releases.</span></span> <span data-ttu-id="dc3d8-114">안정적인 릴리스만 표시하려면 이 옵션을 선택 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-114">To show only stable released, clear the option.</span></span>

<span data-ttu-id="dc3d8-115">특정 요구 사항에 대한 태그 기준 검색(Visual Studio의 패키지 관리자 또는 nuget.org와 같은 포털에서)이 가장 적합한 패키지 검색 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-115">For specific needs, searching by tags (within Visual Studio's Package Manager or on a portal like nuget.org) is the most common means of discovering a suitable package.</span></span> <span data-ttu-id="dc3d8-116">예를 들어 "json"을 검색하면 해당 키워드로 태그가 지정된 모든 NuGet 패키지를 나열하며, 이에 따라 JSON 데이터 형식과 어떤 관계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-116">For example, searching on "json" lists all NuGet packages that are tagged with that keyword and thus have some relationship to the JSON data format.</span></span>

![nuget.org의 'json'에 대한 검색 결과](media/Finding-02-SearchResults.png)

<span data-ttu-id="dc3d8-118">패키지 ID를 알고 있는 경우 이를 사용하여 검색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-118">You can also search using the package ID, if you know it.</span></span> <span data-ttu-id="dc3d8-119">아래의 [검색 구문](#search-syntax)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-119">See [Search Syntax](#search-syntax) below.</span></span>

<span data-ttu-id="dc3d8-120">현재 검색 결과는 관련성에 따라 정렬되므로 일반적으로 사용자의 요구 사항에 맞는 패키지에 대한 결과의 처음 몇 페이지를 최소한으로 살펴보거나 검색 용어를 더 구체적으로 조정하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-120">At this time, search results are sorted only by relevance, so you generally want to look through at least the first few pages of results for packages that suit your needs, or refine your search terms to be more specific.</span></span>

### <a name="does-the-package-support-my-projects-target-framework"></a><span data-ttu-id="dc3d8-121">패키지에서 내 프로젝트의 대상 프레임워크를 지원합니까?</span><span class="sxs-lookup"><span data-stu-id="dc3d8-121">Does the package support my project's target framework?</span></span>

<span data-ttu-id="dc3d8-122">패키지에서 지원되는 프레임워크에 프로젝트의 대상 프레임워크가 포함되어 있는 경우에만 NuGet에서 해당 패키지를 프로젝트에 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-122">NuGet installs a package into a project only if that package's supported frameworks include the project's target framework.</span></span> <span data-ttu-id="dc3d8-123">(패키지를 만들 때 이 작업이 수행되는 방식은 [여러 대상 프레임워크 지원](../create-packages/supporting-multiple-target-frameworks.md)을 참조하세요.) 패키지가 호환되지 않으면 NuGet에서 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-123">(See [Supporting multiple target frameworks](../create-packages/supporting-multiple-target-frameworks.md) for how this is done when creating a package.) If the package is not compatible, NuGet issues an error.</span></span>

<span data-ttu-id="dc3d8-124">일부 패키지는 지원되는 프레임워크를 nuget.org 갤러리에 직접 나열하지만, 이러한 데이터가 필요하지 않으므로 많은 패키지에는 해당 목록이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-124">Some packages list their supported frameworks directly in the nuget.org gallery, but because such data is not required, many packages do not include that list.</span></span> <span data-ttu-id="dc3d8-125">현재 특정 대상 프레임워크를 지원하는 패키지를 nuget.org에서 검색할 수 있는 방법은 없습니다([NuGet 문제 2936](https://github.com/NuGet/NuGetGallery/issues/2936)에서 고려 중인 기능 참조).</span><span class="sxs-lookup"><span data-stu-id="dc3d8-125">At present there is no means to search nuget.org for packages that support a specific target framework (the feature is under consideration, see [NuGet Issue 2936](https://github.com/NuGet/NuGetGallery/issues/2936)).</span></span>

<span data-ttu-id="dc3d8-126">다행히도 두 가지 다른 방법을 통해 지원되는 프레임워크를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-126">Fortunately, you can determine supported frameworks through two other means:</span></span>

1. <span data-ttu-id="dc3d8-127">NuGet 패키지 관리자 콘솔에서 [`Install-Package`](../tools/ps-ref-install-package.md) 명령을 사용하여 프로젝트에 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-127">Attempt to install a package into a project using the [`Install-Package`](../tools/ps-ref-install-package.md) command in the NuGet Package Manager Console.</span></span> <span data-ttu-id="dc3d8-128">패키지가 호환되지 않으면 이 명령은 패키지에서 지원하는 프레임워크를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-128">If the package is incompatible, this command shows you the package's supported frameworks.</span></span>

1. <span data-ttu-id="dc3d8-129">**정보** 아래의 **수동 다운로드** 링크를 사용하여 nuget.org의 해당 페이지에서 패키지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-129">Download the package from its page on nuget.org using the **Manual download** link under **Info**.</span></span> <span data-ttu-id="dc3d8-130">확장명을 `.nupkg`에서 `.zip`으로 변경하고 해당 파일을 열어 `lib` 폴더의 내용을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-130">Change the extension from `.nupkg` to `.zip`, and open the file to examine the content of its `lib` folder.</span></span> <span data-ttu-id="dc3d8-131">각 하위 폴더에는 TFM(대상 프레임워크 모니커, [대상 프레임워크](../reference/target-frameworks.md) 참조)으로 명명된 지원되는 각 프레임워크의 하위 폴더가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-131">There you see subfolders for each of the supported frameworks, where each subfolder is named with a target framework moniker (TFM; see [Target Frameworks](../reference/target-frameworks.md)).</span></span> <span data-ttu-id="dc3d8-132">`lib`에 하위 폴더가 없고 단일 DLL만 표시되면 프로젝트에 패키지를 설치하여 해당 호환성을 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-132">If you see no subfolders under `lib` and only a single DLL, then you must attempt to install the package in your project to discover its compatibility.</span></span>

## <a name="pre-release-packages"></a><span data-ttu-id="dc3d8-133">시험판 패키지</span><span class="sxs-lookup"><span data-stu-id="dc3d8-133">Pre-release packages</span></span>

<span data-ttu-id="dc3d8-134">대부분의 패키지 작성자는 미리 보기 및 베타 릴리스를 제공하여 지속적으로 개선하고 최신 수정 버전에 대한 피드백을 얻고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-134">Many package authors make preview and beta releases available as they continue to make improvements and seek feedback on their latest revisions.</span></span>

<span data-ttu-id="dc3d8-135">기본적으로 nuget.org에서는 시험판 패키지를 검색 결과에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-135">By default, nuget.org shows pre-release packages in search results.</span></span> <span data-ttu-id="dc3d8-136">안정적인 릴리스만 검색하려면 페이지 오른쪽 위의 **시험판 포함** 옵션을 선택 취소합니다</span><span class="sxs-lookup"><span data-stu-id="dc3d8-136">To search only stable releases, clear the **Include prerelease** option on the upper right of the page</span></span>

![nuget.org의 시험판 포함 확인란](media/Finding-06-include-prerelease.png)

<span data-ttu-id="dc3d8-138">Visual Studio 및 NuGet CLI를 사용하는 경우 NuGet에는 기본적으로 시험판 버전이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-138">In Visual Studio and when using the NuGet CLI, NuGet does not include pre-release versions by default.</span></span> <span data-ttu-id="dc3d8-139">이 동작을 변경하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-139">To change this behavior, do the following steps:</span></span>

- <span data-ttu-id="dc3d8-140">**Visual Studio의 패키지 관리자 UI**: **NuGet 패키지 관리** UI에서 **시험판 포함** 확인란을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-140">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, set the **Include prerelease** box.</span></span> <span data-ttu-id="dc3d8-141">이 확인란을 설정 또는 해제하면 패키지 관리자 UI 및 설치할 수 있는 사용 가능한 버전 목록을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-141">Setting or clearing this box refreshes the Package Manager UI and the list of available versions you can install.</span></span>

    ![Visual Studio의 시험판 포함 확인란](media/Prerelease_02-CheckPrerelease.png)

- <span data-ttu-id="dc3d8-143">**패키지 관리자 콘솔**: `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` 및 `Update-Package` 명령과 함께 `-IncludePrerelease` 스위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-143">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="dc3d8-144">[PowerShell 참조](../tools/powershell-reference.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-144">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="dc3d8-145">**NuGet CLI**: `install`, `update`, `delete` 및 `mirror` 명령과 함께 `-prerelease` 스위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-145">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="dc3d8-146">[NuGet CLI 참조](../tools/nuget-exe-cli-reference.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-146">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a><span data-ttu-id="dc3d8-147">네이티브 C++ 패키지</span><span class="sxs-lookup"><span data-stu-id="dc3d8-147">Native C++ packages</span></span>

<span data-ttu-id="dc3d8-148">NuGet은 Visual Studio의 C++ 프로젝트에서 사용할 수 있는 네이티브 C++ 패키지 캔을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-148">NuGet supports native C++ packages can that can be used in C++ projects in Visual Studio.</span></span> <span data-ttu-id="dc3d8-149">이를 통해 프로젝트의 **NuGet 패키지 관리** 상황에 맞는 메뉴 명령을 사용할 수 있고, `native` 대상 프레임워크를 소개하고, MSBuild 통합을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-149">This enables the **Manage NuGet Packages** context-menu command for projects, introduces a `native` target framework, and provides MSBuild integration.</span></span>

<span data-ttu-id="dc3d8-150">[nuget.org](https://www.nuget.org/packages)에서 네이티브 패키지를 찾으려면 `tag:native`를 사용하여 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-150">To find native packages on [nuget.org](https://www.nuget.org/packages), search using `tag:native`.</span></span> <span data-ttu-id="dc3d8-151">이러한 패키지는 일반적으로 패키지가 프로젝트에 추가될 때 NuGet에서 자동으로 가져오는 `.targets` 및 `.props` 파일을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-151">Such packages typically provide `.targets` and `.props` files, which NuGet imports automatically when the package is added to a project.</span></span>

## <a name="evaluating-packages"></a><span data-ttu-id="dc3d8-152">패키지 평가</span><span class="sxs-lookup"><span data-stu-id="dc3d8-152">Evaluating packages</span></span>

<span data-ttu-id="dc3d8-153">패키지의 유용성을 평가하는 가장 좋은 방법은 패키지를 다운로드하여 코드에서 시험해 보는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-153">The best way to evaluate the usefulness of a package is to download it and try it out in your code.</span></span> <span data-ttu-id="dc3d8-154">즉 인기 있는 모든 패키지는 소수의 개발자만 사용하여 시작되었으며, 사용자는 얼리어답터 중 한 명일 수 있습니다!</span><span class="sxs-lookup"><span data-stu-id="dc3d8-154">After all, every highly popular package got started with only a few developers using it, and you might be one of the early adopters!</span></span> <span data-ttu-id="dc3d8-155">(nuget.org의 모든 패키지는 바이러스에 대해 정기적으로 검사됩니다.)</span><span class="sxs-lookup"><span data-stu-id="dc3d8-155">(Note that all packages on nuget.org are routinely scanned for viruses.)</span></span>

<span data-ttu-id="dc3d8-156">한편 NuGet 패키지를 사용한다는 것은 패키지에 의존하고 있다는 것을 의미하므로 패키지가 강력하고 신뢰할 수 있는지 확인하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-156">At the same time, using a NuGet package means taking a dependency on it, so you want to make sure it's robust and reliable.</span></span> <span data-ttu-id="dc3d8-157">패키지 설치 및 직접 테스트는 시간이 오래 걸리므로 패키지의 목록 페이지에 있는 정보를 사용하여 패키지의 품질에 대해 많이 알아볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-157">Because installing and directly testing a package is time-consuming, you can also learn a lot about a package's quality by using the information on a package's listing page:</span></span>

- <span data-ttu-id="dc3d8-158">*통계 다운로드*: nuget.org의 패키지 페이지에서 **통계** 섹션에는 총 다운로드 수, 최근 버전 다운로드 수 및 일일 평균 다운로드 수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-158">*Downloads statistics*: on the package page on nuget.org, the **Statistics** section shows total downloads, downloads of the most recent version, and average downloads per day.</span></span> <span data-ttu-id="dc3d8-159">숫자가 클수록 다른 많은 개발자가 패키지에 의존하고 있음을 나타내며, 이는 패키지가 그 자체를 입증했다는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-159">Larger numbers indicate that many other developers have taken a dependency on the package, which means that it has proven itself.</span></span>

    ![패키지의 목록 페이지에 대한 다운로드 통계](media/Finding-03-Downloads.png)

- <span data-ttu-id="dc3d8-161">*버전 기록*: 패키지 페이지의 **정보** 아래에서 최신 업데이트 날짜를 확인하고 **버전 기록**을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-161">*Version history*: on the package page, look under **Info** for the date of the most recent update and examine the **Version History**.</span></span> <span data-ttu-id="dc3d8-162">잘 유지 관리된 패키지에는 최신 업데이트와 풍부한 버전 기록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-162">A well-maintained package has recent updates and a rich version history.</span></span> <span data-ttu-id="dc3d8-163">방치한 패키지에는 업데이트가 거의 없으며, 일정 기간 동안 업데이트되지 않은 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-163">Neglected packages have few updates and often haven't been updated in some time.</span></span>

    ![패키지 목록 페이지의 버전 기록](media/Finding-04-VersionHistory.png)

- <span data-ttu-id="dc3d8-165">*최근 설치*: 패키지 페이지의 **통계** 아래에서 **전체 통계 보기**를 선택합니다. 전체 통계 페이지에서는 지난 6주 동안 버전 번호별로 설치된 패키지를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-165">*Recent installs*: on the package page under **Statistics**, select **View full stats**. The full stats page shows the package installs over the last six weeks by version number.</span></span> <span data-ttu-id="dc3d8-166">일반적으로 다른 개발자가 적극적으로 사용하는 패키지는 그렇지 않은 패키지보다 더 나은 선택입니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-166">A package that other developers are actively using is typically a better choice than one that's not.</span></span>

- <span data-ttu-id="dc3d8-167">*지원*: 패키지 페이지의 **정보** 아래에서 **프로젝트 사이트**(사용 가능한 경우)를 선택하여 사용 가능한 지원 옵션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-167">*Support*: on the package page under **Info**, select **Project Site** (if available) to see what support options are available.</span></span> <span data-ttu-id="dc3d8-168">일반적으로 전용 사이트가 있는 프로젝트가 더 잘 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-168">A project with a dedicated site is generally better supported.</span></span>

- <span data-ttu-id="dc3d8-169">*개발자 기록*: 패키지 페이지의 **소유자** 아래에서 소유자를 선택하여 게시한 다른 패키지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-169">*Developer history*: on the package page under **Owners**, select an owner to see what other packages they've published.</span></span> <span data-ttu-id="dc3d8-170">여러 패키지가 있는 사람들은 앞으로도 계속 지원할 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-170">Those with multiple packages are more likely to continue supporting their work in the future.</span></span>

- <span data-ttu-id="dc3d8-171">*오픈 소스 기여*: 많은 패키지가 오픈 소스 리포지토리에서 유지 관리되므로 개발자가 버그 수정 및 기능 향상에 직접 기여할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-171">*Open source contributions*: many packages are maintained in open-source repositories, making it possible for developers depending on them to directly contribute bug fixes and feature improvements.</span></span> <span data-ttu-id="dc3d8-172">지정된 패키지의 기여 기록은 얼마나 많은 개발자가 적극적으로 참여했는지를 나타내는 좋은 지표이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-172">The contribution history of any given package is also a good indicator of how many developers are actively involved.</span></span>

- <span data-ttu-id="dc3d8-173">*소유자 인터뷰*: 사용자가 사용할 수 있는 훌륭한 패키지를 만드는 데 새 개발자도 동등하게 헌신할 수 있으며, NuGet 생태계에 새로운 것을 가져올 수 있는 기회를 제공하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-173">*Interview the owners*: new developers can certainly be equally committed to producing great packages for you to use, and it's good to give them a chance to bring something new to the NuGet ecosystem.</span></span> <span data-ttu-id="dc3d8-174">이를 고려하여, 목록 페이지의 **정보** 아래에 있는 **연락처 소유자** 옵션을 통해 패키지 개발자에게 직접 문의해 보세요.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-174">With this in mind, reach out directly to the package developers through the **Contact Owners** option under **Info** on the listing page.</span></span> <span data-ttu-id="dc3d8-175">아마, 이들은 여러분의 요구에 부응하기 위해 여러분과 함께 기꺼이 협력할 것입니다!</span><span class="sxs-lookup"><span data-stu-id="dc3d8-175">Chances are, they'll be happy to work with you to serve your needs!</span></span>

> [!Note]
> <span data-ttu-id="dc3d8-176">nuget.org의 패키지 목록 페이지에서 **라이선스 정보**를 선택하면 볼 수 있는 패키지의 사용 조건에 항상 유의해야 합니다. 패키지에서 사용 조건을 지정하지 않은 경우 패키지 페이지의 **연락처 소유자** 링크를 사용하여 패키지 소유자에게 직접 문의해 보세요.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-176">Always be mindful of a package's license terms, which you can see by selecting **License Info** on a package's listing page on nuget.org. If a package does not specify license terms, contact the package owner directly using the **Contact owners** link on the package page.</span></span> <span data-ttu-id="dc3d8-177">Microsoft는 타사 패키지 공급자로부터 사용자에게 지적 재산권을 부여하지 않으며 타사에서 제공한 정보에 대해 책임을 지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-177">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

## <a name="search-syntax"></a><span data-ttu-id="dc3d8-178">검색 구문</span><span class="sxs-lookup"><span data-stu-id="dc3d8-178">Search Syntax</span></span>

<span data-ttu-id="dc3d8-179">NuGet 패키지 검색은 nuget.org, NuGet CLI 및 Visual Studio의 NuGet 패키지 관리자 확장에서 동일하게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-179">NuGet package search works the same on nuget.org, from the NuGet CLI, and within the NuGet Package Manager extension in Visual Studio.</span></span> <span data-ttu-id="dc3d8-180">일반적으로 검색은 패키지 설명뿐만 아니라 키워드에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-180">In general, search is applied to keywords as well as package descriptions.</span></span>

- <span data-ttu-id="dc3d8-181">**키워드**: 제공된 모든 키워드를 포함하는 관련 패키지를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-181">**Keywords**: Search looks for relevant packages that contain all the provided keywords.</span></span> <span data-ttu-id="dc3d8-182">예제:</span><span class="sxs-lookup"><span data-stu-id="dc3d8-182">Example:</span></span>

    ```
    modern UI javascript
    ```

- <span data-ttu-id="dc3d8-183">**구**: 인용 부호 안에 검색어를 입력하면 해당 용어와 대/소문자를 구분하지 않는 정확한 일치를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-183">**Phrases**: Entering terms within quotation marks looks for exact case-insensitive matches to those terms.</span></span> <span data-ttu-id="dc3d8-184">예제:</span><span class="sxs-lookup"><span data-stu-id="dc3d8-184">Example:</span></span>

    ```
    "modern UI" package
    ```

- <span data-ttu-id="dc3d8-185">**필터링**: `<property>:<term>` 구문을 사용하여 특정 속성에 검색어를 적용할 수 있습니다. 여기서 `<property>`(대/소문자 구분 안 함)은 `id`, `packageid`, `version`, `title`, `tags`, `author`, `description`, `summary` 및 `owner`일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-185">**Filtering**: You can apply a search term to a specific property by using the syntax `<property>:<term>` where `<property>` (case-insensitive) can be `id`, `packageid`, `version`, `title`, `tags`, `author`, `description`, `summary`, and `owner`.</span></span> <span data-ttu-id="dc3d8-186">필요에 따라 용어를 따옴표로 묶어 여러 속성을 동시에 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-186">Terms can be contained in quotes if needed, and you can search for multiple properties at the same time.</span></span> <span data-ttu-id="dc3d8-187">또한 `id` 속성에 대한 검색은 부분 문자열 일치이지만, `packageid`는 정확히 일치 항목을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-187">Also, searches on the `id` property are substring matches, whereas `packageid` uses an exact match.</span></span> <span data-ttu-id="dc3d8-188">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dc3d8-188">Examples:</span></span>

    ```
    id:NuGet.Core                //Match any part of the id property
    Id:"Nuget.Core"
    ID:jQuery
    title:jquery                 //Searches title as shown on the package listing
    PackageId:jquery             //Match the package id exactly
    id:jquery id:ui              //Search for multiple terms in the id
    id:jquery tags:validation    //Search multiple properties
    id:"jquery.ui"               //Phrase search
    invalid:jquery ui            //Unsupported properties are ignored, so this
                                 //is the same as searching on jquery ui
    ```