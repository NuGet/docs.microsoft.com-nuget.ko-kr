---
title: "NuGet 4.5 RTM 릴리스 정보 | Microsoft Docs"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 12/4/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 4.5 RTM에 대한 릴리스 정보(알려진 문제, 버그 수정, 추가된 기능 및 DCR 포함)"
keywords: "NuGet 4.5 RTM 릴리스 정보, 버그 수정, 알려진 문제, 추가된 기능, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: e4727d46812cbfeb2e7094ddf28bf4e738e8aeea
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2018
---
# <a name="nuget-45-rtm-release-notes"></a><span data-ttu-id="f83e2-104">NuGet 4.5 RTM 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="f83e2-104">NuGet 4.5 RTM Release Notes</span></span>

<span data-ttu-id="f83e2-105">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes)는 [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe)과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f83e2-105">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="known-issues"></a><span data-ttu-id="f83e2-106">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="f83e2-106">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="f83e2-107">.NET Framework 및 NuGet이 포함된 .NET Standard 2.0 관련 문제</span><span class="sxs-lookup"><span data-stu-id="f83e2-107">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="f83e2-108">.NET Standard 및 해당 도구는 .NET Framework 4.6.1을 대상으로 하는 프로젝트에서 .NET Standard 2.0 또는 이전 버전을 대상으로 하는 NuGet 패키지 및 프로젝트를 사용할 수 있도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f83e2-108">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="f83e2-109">[이 문서](https://github.com/dotnet/standard/issues/481)에서는 해당 시나리오와 관련된 문제, 문제를 해결하기 위한 계획 및 현재의 도구 상태로 배포할 수 있는 해결 방법을 요약하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f83e2-109">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="f83e2-110">NuGet 패키지 관리자를 사용하여 DotNetCLITools를 보거나 추가 또는 업데이트할 수 없음</span><span class="sxs-lookup"><span data-stu-id="f83e2-110">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="f83e2-111">문제</span><span class="sxs-lookup"><span data-stu-id="f83e2-111">Issue</span></span>

<span data-ttu-id="f83e2-112">NuGet 패키지 관리자는 DotNetCLITools 추가/업데이트를 표시하지 않으며 허용하지도 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f83e2-112">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="f83e2-113">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="f83e2-113">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="f83e2-114">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f83e2-114">Workaround</span></span>

<span data-ttu-id="f83e2-115">프로젝트 파일에서 DotNetCLIToolReferences를 수동으로 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f83e2-115">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="f83e2-116">대상 프레임워크 버전의 대상을 변경하면 불완전한 IntelliSense가 발생할 수 있음</span><span class="sxs-lookup"><span data-stu-id="f83e2-116">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="f83e2-117">문제</span><span class="sxs-lookup"><span data-stu-id="f83e2-117">Issue</span></span>

<span data-ttu-id="f83e2-118">Visual Studio에서 대상 프레임워크 버전의 대상을 변경하면 불완전한 IntelliSense가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f83e2-118">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="f83e2-119">이 문제는 PackageReferences를 패키지 관리자 형식으로 사용하는 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f83e2-119">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="f83e2-120">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="f83e2-120">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="f83e2-121">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f83e2-121">Workaround</span></span>

<span data-ttu-id="f83e2-122">수동 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f83e2-122">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="f83e2-123">잘못된 시그니처와 함께 어셈블리가 포함된 .NET Core 프로젝트의 패키지는 무한 복원 루프를 트리거할 수 있음</span><span class="sxs-lookup"><span data-stu-id="f83e2-123">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="f83e2-124">문제</span><span class="sxs-lookup"><span data-stu-id="f83e2-124">Issue</span></span>

<span data-ttu-id="f83e2-125">경우에 따라 잘못된 시그니처와 함께 어셈블리가 포함된 패키지를 사용하거나 패키지 버전이 'DateTime' 표시기로 설정된 경우 패키지 자동 복원이 무한 루프로 실행됩니다([dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457)).</span><span class="sxs-lookup"><span data-stu-id="f83e2-125">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="f83e2-126">해결 방법</span><span class="sxs-lookup"><span data-stu-id="f83e2-126">Workaround</span></span>

<span data-ttu-id="f83e2-127">지금은 해결 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f83e2-127">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="f83e2-128">NuGet 4.5 RTM 기간에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="f83e2-128">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="f83e2-129">NuGet 4.4 RTM에서 수정된 문제는 [NuGet 4.4 RTM 릴리스 정보](../release-notes/nuget-4.4-RTM.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f83e2-129">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="f83e2-130">기능</span><span class="sxs-lookup"><span data-stu-id="f83e2-130">Features</span></span>

- <span data-ttu-id="f83e2-131">기호 패키지 자동 푸시 사용 안 함 - [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="f83e2-131">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="f83e2-132">버그</span><span class="sxs-lookup"><span data-stu-id="f83e2-132">Bugs</span></span>

- <span data-ttu-id="f83e2-133">15.5p1에서 [재귀]: Portable0.0은 건너뜁니다. - [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="f83e2-133">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="f83e2-134">복원 후 패키지의 자산이 누락되었습니다. - [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="f83e2-134">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="f83e2-135">공백이 포함된 URI를 사용하는 경우 플러그 인 자격 증명 공급자가 작동하지 않습니다. - [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="f83e2-135">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="f83e2-136">패키지를 복원하지 못하면 최소 세부 정보 표시를 ON으로 설정해도 출력에 오류가 출력됩니다. - [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="f83e2-136">If package failed to restore, error should be printed i the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="f83e2-137">솔루션 수준의 dotnet restore에서 ReferenceOutputAssembly가 false인 ProjectReference를 따르지 않아 임의 빌드가 실패합니다. - [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="f83e2-137">dotnet restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="f83e2-138">PMC의 자동 완성이 개체 메서드에서 제대로 작동하지 않습니다. - [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="f83e2-138">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="f83e2-139">Visual Studio 2015 도구 집합으로 인해 nuget.exe restore가 실패합니다. - [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="f83e2-139">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="f83e2-140">perf - pmc는 VS2017에서 인스턴스화하는 데 비용이 많이 듭니다. - [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="f83e2-140">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="f83e2-141">저속 연결에서 종속성 정보를 가져오는 데 시간이 많이 걸립니다. - [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="f83e2-141">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="f83e2-142">여러 패키지에서 일반적인 종속성을 공유하면 uninstall-package w/ -RemoveDependencies가 실패합니다. - [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="f83e2-142">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="f83e2-143">게시를 위해 NuGet.Core.nupkg를 완료합니다. - [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="f83e2-143">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="f83e2-144">csproj + project.json에 -IncludeProjectReferences를 사용하면 NuGet 팩에서 디렉터리 이름의 종속성 ID를 확인합니다. - [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="f83e2-144">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="f83e2-145">'NuGet.ProxyCache'에 대한 형식 이니셜라이저에서 예외를 throw했습니다. - [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="f83e2-145">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="f83e2-146">Kudu를 사용한 nuget restore 성능이 저하되는 문제가 있습니다. - [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="f83e2-146">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="f83e2-147">검색이 Blob 등록보다 먼저 수행되면 UI 클라이언트에서 오류 또는 경고를 표시하지 못합니다. - [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="f83e2-147">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="f83e2-148">Get-Packages - 업데이트에서 잘못된 쿼리를 생성합니다. - [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="f83e2-148">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="f83e2-149">4.5 RTM에서 수정된 GitHub 문제에 대한 링크</span><span class="sxs-lookup"><span data-stu-id="f83e2-149">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="f83e2-150">문제 목록</span><span class="sxs-lookup"><span data-stu-id="f83e2-150">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
