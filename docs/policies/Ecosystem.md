---
title: NuGet 에코시스템 개요
description: NuGet 소스, 비 Microsoft NuGet 프로젝트, 유틸리티 및 교육 자료를 포함하여 NuGet 에코시스템에 있는 포괄적인 리소스입니다.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 31243076f36f6ff274c4377c1773ea59dda8c834
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64495497"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a><span data-ttu-id="f5e27-103">NuGet 에코시스템 개요</span><span class="sxs-lookup"><span data-stu-id="f5e27-103">An overview of the NuGet ecosystem</span></span>

<span data-ttu-id="f5e27-104">2010을 소개하므로 NuGet에서는 개발 프로세스의 다양한 측면을 개선하고 자동화하는 좋은 기회를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-104">Since it's introduction in 2010, NuGet has presented a great opportunity to improve and automate different aspects of the development processes.</span></span>

<span data-ttu-id="f5e27-105">NuGet이 허용 [Apache v2 라이선스](http://choosealicense.com/licenses/apache/) 하의 오픈 소스이기 때문에 다른 프로젝트에서는 NuGet를 활용할 수 있고 회사는 해당 제품에서 지원을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-105">Because NuGet is open source under a permissive [Apache v2 license](http://choosealicense.com/licenses/apache/), other projects can leverage NuGet and companies can build support for it in their products.</span></span> <span data-ttu-id="f5e27-106">오픈 소스 프로젝트나 엔터프라이즈 애플리케이션 개발에서 NuGet 및 NuGet 주위에 빌드되는 다른 애플리케이션은 소프트웨어 개발 프로세스를 향상시키기 위한 도구의 광범위한 에코시스템을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-106">Whether for open-source projects or enterprise application development, NuGet and other applications built on and around NuGet provide a broad ecosystem of tools for improving your software development process.</span></span>

<span data-ttu-id="f5e27-107">이러한 프로젝트는 모두 개발자 기여로 인해 혁신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-107">All of these projects are able to innovate because of developer contributions.</span></span> <span data-ttu-id="f5e27-108">NuGet 자체에 기여한 것처럼 가능한 경우 오류 및 새로운 기능 아이디어를 보고하고, 피드백을 제공하고, 설명서를 작성하고, 코드에 기여하여 이러한 프로젝트에 참여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-108">Just as you contribute to NuGet itself, also make contribution to these projects by reporting defects and new feature ideas, providing feedback, writing documentation, and contributing code where possible.</span></span>

## <a name="net-foundation-projects"></a><span data-ttu-id="f5e27-109">.NET Foundation 프로젝트</span><span class="sxs-lookup"><span data-stu-id="f5e27-109">.NET Foundation projects</span></span>

<span data-ttu-id="f5e27-110">NuGet은 Microsoft 개발 플랫폼에 대한 체험용 오픈 소스 패키지 관리 시스템을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-110">NuGet provides a free, open source package management system for the Microsoft development platform.</span></span> <span data-ttu-id="f5e27-111">[공식 NuGet 갤러리](http://www.nuget.org)를 구성하는 서비스 집합뿐만 아니라 몇 가지 클라이언트 도구로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-111">It consists of a few client tools as well as the set of services that comprise the [official NuGet Gallery](http://www.nuget.org).</span></span> <span data-ttu-id="f5e27-112">이 항목이 결합되어 [.NET Foundation](http://www.dotnetfoundation.org/)에 의해 제어되는 NuGet 프로젝트를 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-112">Combined, these form the NuGet project which is governed by the [.NET Foundation](http://www.dotnetfoundation.org/).</span></span>

<span data-ttu-id="f5e27-113">NuGet 조직에는 GitHub에 대한 다양한 저장소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-113">The NuGet Organization contains various repositories on GitHub.</span></span> <span data-ttu-id="f5e27-114">[https://github.com/Nuget/Home](https://github.com/Nuget/Home)에서는 모든 리포지토리에 대한 개요 및 다양한 NuGet 구성 요소를 찾을 수 있는 위치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-114">[https://github.com/Nuget/Home](https://github.com/Nuget/Home) gives an overview of all the repositories and where to find the various NuGet components.</span></span>

## <a name="microsoft-projects"></a><span data-ttu-id="f5e27-115">Microsoft 프로젝트</span><span class="sxs-lookup"><span data-stu-id="f5e27-115">Microsoft projects</span></span>

<span data-ttu-id="f5e27-116">Microsoft에서는 NuGet을 개발하는 데 광범위하게 기여했습니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-116">Microsoft has contributed extensively to the development of NuGet.</span></span> <span data-ttu-id="f5e27-117">Microsoft 직원들이 수행한 모든 노력은 오픈 소스이며 .NET Foundation에 제공됩니다(저작권 포함).</span><span class="sxs-lookup"><span data-stu-id="f5e27-117">All contributions made by Microsoft employees are also open source and are donated (including copyrights) to the .NET Foundation.</span></span>

## <a name="non-microsoft-projects"></a><span data-ttu-id="f5e27-118">타사 프로젝트</span><span class="sxs-lookup"><span data-stu-id="f5e27-118">Non-Microsoft projects</span></span>

<span data-ttu-id="f5e27-119">다른 개인 및 회사에서도 NuGet 에코시스템에 상당히 기여했습니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-119">Many other individuals and companies have made significant contributions to the NuGet ecosystem.</span></span> <span data-ttu-id="f5e27-120">여기에 나열된 각 프로젝트에서는 주요 NuGet 구성 요소와 다른 라이선스를 사용할 수 있습니다. 따라서 사용하기 전에 사용 약관을 허용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-120">Each project listed here may have a different license than the core NuGet components, so confirm that the license terms are acceptable prior to use:</span></span>

- [<span data-ttu-id="f5e27-121">AppVeyor CI</span><span class="sxs-lookup"><span data-stu-id="f5e27-121">AppVeyor CI</span></span>](https://www.appveyor.com/)
- [<span data-ttu-id="f5e27-122">Artifactory</span><span class="sxs-lookup"><span data-stu-id="f5e27-122">Artifactory</span></span>](https://www.jfrog.com/artifactory/)
- [<span data-ttu-id="f5e27-123">BoxStarter</span><span class="sxs-lookup"><span data-stu-id="f5e27-123">BoxStarter</span></span>](http://boxstarter.org/)
- [<span data-ttu-id="f5e27-124">Chocolatey</span><span class="sxs-lookup"><span data-stu-id="f5e27-124">Chocolatey</span></span>](https://chocolatey.org/)
- [<span data-ttu-id="f5e27-125">CoApp</span><span class="sxs-lookup"><span data-stu-id="f5e27-125">CoApp</span></span>](http://coapp.org/)
- [<span data-ttu-id="f5e27-126">JetBrains ReSharper</span><span class="sxs-lookup"><span data-stu-id="f5e27-126">JetBrains ReSharper</span></span>](https://resharper-plugins.jetbrains.com/)
- [<span data-ttu-id="f5e27-127">JetBrains TeamCity</span><span class="sxs-lookup"><span data-stu-id="f5e27-127">JetBrains TeamCity</span></span>](https://www.jetbrains.com/teamcity/)
- [<span data-ttu-id="f5e27-128">Klondike</span><span class="sxs-lookup"><span data-stu-id="f5e27-128">Klondike</span></span>](https://github.com/themotleyfool/Klondike)
- [<span data-ttu-id="f5e27-129">MinimalNugetServer</span><span class="sxs-lookup"><span data-stu-id="f5e27-129">MinimalNugetServer</span></span>](https://github.com/TanukiSharp/MinimalNugetServer)
- [<span data-ttu-id="f5e27-130">MyGet(또는 NuGet-as-a-service)</span><span class="sxs-lookup"><span data-stu-id="f5e27-130">MyGet (or NuGet-as-a-service)</span></span>](http://www.myget.org/)
- [<span data-ttu-id="f5e27-131">NuGet 패키지 탐색기</span><span class="sxs-lookup"><span data-stu-id="f5e27-131">NuGet Package Explorer</span></span>](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [<span data-ttu-id="f5e27-132">NuGet 서버</span><span class="sxs-lookup"><span data-stu-id="f5e27-132">NuGet Server</span></span>](http://nugetserver.net/)
- [<span data-ttu-id="f5e27-133">OctopusDeploy</span><span class="sxs-lookup"><span data-stu-id="f5e27-133">OctopusDeploy</span></span>](https://octopus.com/)
- [<span data-ttu-id="f5e27-134">Paket</span><span class="sxs-lookup"><span data-stu-id="f5e27-134">Paket</span></span>](https://fsprojects.github.io/Paket/)
- [<span data-ttu-id="f5e27-135">ProGet(Inedo)</span><span class="sxs-lookup"><span data-stu-id="f5e27-135">ProGet (Inedo)</span></span>](http://inedo.com/proget)
- [<span data-ttu-id="f5e27-136">scriptcs</span><span class="sxs-lookup"><span data-stu-id="f5e27-136">scriptcs</span></span>](http://scriptcs.net/)
- [<span data-ttu-id="f5e27-137">SharpDevelop</span><span class="sxs-lookup"><span data-stu-id="f5e27-137">SharpDevelop</span></span>](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [<span data-ttu-id="f5e27-138">Sonatype Nexus</span><span class="sxs-lookup"><span data-stu-id="f5e27-138">Sonatype Nexus</span></span>](http://www.sonatype.com/nexus-repository-sonatype)
- [<span data-ttu-id="f5e27-139">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="f5e27-139">SymbolSource</span></span>](http://www.symbolsource.org/Public)
- [<span data-ttu-id="f5e27-140">Xamarin 및 MonoDevelop</span><span class="sxs-lookup"><span data-stu-id="f5e27-140">Xamarin and MonoDevelop</span></span>](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a><span data-ttu-id="f5e27-141">기타 NuGet 기반 유틸리티</span><span class="sxs-lookup"><span data-stu-id="f5e27-141">Other NuGet-based utilities</span></span>

<span data-ttu-id="f5e27-142">NuGet에 기반한 도구 및 유틸리티는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-142">These are tools and utilities built on NuGet:</span></span>

- <span data-ttu-id="f5e27-143">[슬라이드 확장](http://getglimpse.com/Packages)(플러그 인이 패키지)</span><span class="sxs-lookup"><span data-stu-id="f5e27-143">[Glimpse Extensions](http://getglimpse.com/Packages) (plug-ins are packages)</span></span>
- [<span data-ttu-id="f5e27-144">NuGetMustHaves.com</span><span class="sxs-lookup"><span data-stu-id="f5e27-144">NuGetMustHaves.com</span></span>](http://nugetmusthaves.com/)
- <span data-ttu-id="f5e27-145">[Orchard](http://www.orchardproject.net/)(Orchard 갤러리에서 호스트되는 v1 NuGet 피드에서 CMS 모듈을 가져옴)</span><span class="sxs-lookup"><span data-stu-id="f5e27-145">[Orchard](http://www.orchardproject.net/) (CMS modules are fetched from a v1 NuGet feed hosted in the Orchard Gallery)</span></span>
- [<span data-ttu-id="f5e27-146">NuGet 서버의 Java 구현</span><span class="sxs-lookup"><span data-stu-id="f5e27-146">Java implementation of NuGet Server</span></span>](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- <span data-ttu-id="f5e27-147">[NuGetLatest](https://twitter.com/NuGetLatest)(새 패키지 게시를 트윗하는 Twitter 봇)</span><span class="sxs-lookup"><span data-stu-id="f5e27-147">[NuGetLatest](https://twitter.com/NuGetLatest) (Twitter bot tweeting new package publications)</span></span>
- <span data-ttu-id="f5e27-148">[DefinitelyTyped](http://definitelytyped.org/)([자동](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript 형식 [NuGet에 게시된 정의](http://www.nuget.org/packages?q=DefinitelyTyped))</span><span class="sxs-lookup"><span data-stu-id="f5e27-148">[DefinitelyTyped](http://definitelytyped.org/) ([Automatic](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript Type [Definitions published to NuGet](http://www.nuget.org/packages?q=DefinitelyTyped))</span></span>

## <a name="training-materials-and-references"></a><span data-ttu-id="f5e27-149">교육 자료 및 참조</span><span class="sxs-lookup"><span data-stu-id="f5e27-149">Training materials and references</span></span>

<span data-ttu-id="f5e27-150">일반적으로 새로운 도구 또는 기술을 사용하면 학습 곡선이 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-150">Using a new tool or technology usually comes with a learning curve.</span></span> <span data-ttu-id="f5e27-151">다행히 NuGet의 학습 곡선은 가파르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-151">Luckily for you, NuGet has no steep learning curve it all!</span></span> <span data-ttu-id="f5e27-152">실제로 신속하게 [패키지를 사용하기 시작](../quickstart/use-a-package.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-152">In fact, anyone can [get started consuming packages](../quickstart/use-a-package.md) quickly.</span></span>

<span data-ttu-id="f5e27-153">즉, 자동화된 빌드 및 배포 프로세스에서 NuGet과 함께 패키지를 작성하려면(특히 양호한 패키지) 다음 리소스에 좀 더 많은 시간을 들여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-153">That said, authoring packages–and especially good packages–along with  embracing NuGet in automated build and deployment processes, requires spending a little more time with the following resources:</span></span>

- [<span data-ttu-id="f5e27-154">NuGet 블로그</span><span class="sxs-lookup"><span data-stu-id="f5e27-154">NuGet Blog</span></span>](http://blog.nuget.org/)
- [<span data-ttu-id="f5e27-155">Twitter의 NuGet 팀@nuget</span><span class="sxs-lookup"><span data-stu-id="f5e27-155">NuGet team on Twitter, @nuget</span></span>](http://twitter.com/nuget)
- <span data-ttu-id="f5e27-156">서적:</span><span class="sxs-lookup"><span data-stu-id="f5e27-156">Books:</span></span>
  - [<span data-ttu-id="f5e27-157">Apress Pro NuGet</span><span class="sxs-lookup"><span data-stu-id="f5e27-157">Apress Pro NuGet</span></span>](http://bit.ly/ProNuGet)
  - [<span data-ttu-id="f5e27-158">NuGet 2 Essentials</span><span class="sxs-lookup"><span data-stu-id="f5e27-158">NuGet 2 Essentials</span></span>](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a><span data-ttu-id="f5e27-159">개별 패키지에 대한 설명서</span><span class="sxs-lookup"><span data-stu-id="f5e27-159">Documentation for individual packages</span></span>

<span data-ttu-id="f5e27-160">[NuDoq](http://nudoq.org)은 NuGet 패키지에 대한 액세스와 업데이트 및 설명서를 간단하게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-160">[NuDoq](http://nudoq.org) provides straightforward access and updates and documentation for NuGet packages.</span></span>

<span data-ttu-id="f5e27-161">NuDoq는 정기적으로 최신 패키지 업데이트에 nuget.org 갤러리 서버를 폴링하고, 라이브러리 설명서 파일을 처리하고, 그에 따라 사이트를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="f5e27-161">NuDoq regularly polls the nuget.org gallery server for the latest package updates, unpacks and processes the library documentation files, and updates the site accordingly.</span></span>

## <a name="adding-your-project"></a><span data-ttu-id="f5e27-162">프로젝트 추가</span><span class="sxs-lookup"><span data-stu-id="f5e27-162">Adding your project</span></span>

<span data-ttu-id="f5e27-163">이 페이지에 추가되는 NuGet 에코시스템 프로젝트가 있는 경우 이 페이지를 편집하는 끌어오기 요청을 제출하세요.</span><span class="sxs-lookup"><span data-stu-id="f5e27-163">If you have a NuGet ecosystem project that would be a valuable addition to this page, please  submit a pull request with an edit to this page.</span></span>
