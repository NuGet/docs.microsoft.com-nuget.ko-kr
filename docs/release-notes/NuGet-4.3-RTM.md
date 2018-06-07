---
title: NuGet 4.3 RTM 릴리스 정보
description: NuGet 4.3 RTM에 대한 릴리스 정보(알려진 문제, 버그 수정, 추가된 기능 및 DCR 포함).
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: cb44f47ef0b3bd086f0a681cb2fedc7c5afc42fa
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-43-rtm-release-notes"></a><span data-ttu-id="4eaec-103">NuGet 4.3 RTM 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="4eaec-103">NuGet 4.3 RTM Release Notes</span></span>

<span data-ttu-id="4eaec-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes)는 .NET Standard 2.0/.NET Core 2.0과 같은 새로운 시나리오에 대한 지원을 추가하고, 많은 품질 수정을 포함하며, 성능을 향상시키는 NuGet 4.3 RTM과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eaec-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="4eaec-105">또한 이 릴리스에는 유의적 버전 2.0.0 지원, NuGet 경고/오류의 MSBuild 통합 등과 같이 향상된 몇 가지 기능도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="4eaec-105">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="4eaec-106">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="4eaec-106">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="4eaec-107">일부 경우에 NuGet 복원이 사용하지 않도록 설정된 패키지 소스를 사용 설정된 것으로 처리할 수 있음</span><span class="sxs-lookup"><span data-stu-id="4eaec-107">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="4eaec-108">문제</span><span class="sxs-lookup"><span data-stu-id="4eaec-108">Issue</span></span>

<span data-ttu-id="4eaec-109">다음 restore 명령줄 기술은 사용하지 않도록 설정된 패키지 원본을 사용 가능한 것으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaec-109">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="4eaec-110">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="4eaec-110">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="4eaec-111">`dotnet restore`(VS와 함께 제공되는 dotnet.exe 또는 NetCore SDK 2.0.0과 함께 제공되는 dotnet.exe 사용)</span><span class="sxs-lookup"><span data-stu-id="4eaec-111">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="4eaec-112">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4eaec-112">Workaround</span></span>

1. <span data-ttu-id="4eaec-113">Visual Studio(2017 15.3 이상) 또는 NuGet.exe(v4.3.0 이상) 사용</span><span class="sxs-lookup"><span data-stu-id="4eaec-113">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="4eaec-114">사용할 수 없는 소스를 삭제하고 msbuild 또는 dotnet.exe를 계속 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaec-114">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="4eaec-115">솔루션에 대해 NuGet.config에서 “Clear”를 사용한 다음, 해당 솔루션에 필요한 소스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eaec-115">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="4eaec-116">패키지 관리자 콘솔을 사용하는 동안 'Enter' 키가 작동하지 않을 수 있음</span><span class="sxs-lookup"><span data-stu-id="4eaec-116">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="4eaec-117">문제</span><span class="sxs-lookup"><span data-stu-id="4eaec-117">Issue</span></span>

<span data-ttu-id="4eaec-118">경우에 따라 패키지 관리자 콘솔에서 Enter 키가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4eaec-118">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="4eaec-119">이런 경우 수정 진행 상황을 확인하고 재현 단계에 대해 도움이 되는 추가 정보를 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="4eaec-119">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="4eaec-120">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="4eaec-120">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="4eaec-121">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4eaec-121">Workaround</span></span>

<span data-ttu-id="4eaec-122">Visual Studio를 다시 시작하고 솔루션을 열기 전에 PMC를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="4eaec-122">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="4eaec-123">또는 `project.lock.json`을 삭제하고 다시 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaec-123">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="4eaec-124">NuGet 패키지 관리자를 사용하여 DotNetCLITools를 보거나 추가 또는 업데이트할 수 없음</span><span class="sxs-lookup"><span data-stu-id="4eaec-124">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="4eaec-125">문제</span><span class="sxs-lookup"><span data-stu-id="4eaec-125">Issue</span></span>

<span data-ttu-id="4eaec-126">NuGet 패키지 관리자는 DotNetCLITools 추가/업데이트를 표시하지 않으며 허용하지도 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4eaec-126">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="4eaec-127">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="4eaec-127">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="4eaec-128">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4eaec-128">Workaround</span></span>

<span data-ttu-id="4eaec-129">프로젝트 파일에서 DotNetCLIToolReferences를 수동으로 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaec-129">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="4eaec-130">대상 프레임워크 버전의 대상을 변경하면 불완전한 IntelliSense가 발생할 수 있음</span><span class="sxs-lookup"><span data-stu-id="4eaec-130">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="4eaec-131">문제</span><span class="sxs-lookup"><span data-stu-id="4eaec-131">Issue</span></span>

<span data-ttu-id="4eaec-132">Visual Studio에서 대상 프레임워크 버전의 대상을 변경하면 불완전한 IntelliSense가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eaec-132">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="4eaec-133">이 문제는 PackageReferences를 패키지 관리자 형식으로 사용하는 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaec-133">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="4eaec-134">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="4eaec-134">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="4eaec-135">해결 방법</span><span class="sxs-lookup"><span data-stu-id="4eaec-135">Workaround</span></span>

<span data-ttu-id="4eaec-136">수동 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaec-136">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="4eaec-137">NuGet 4.3 RTM 기간에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="4eaec-137">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="4eaec-138">[NuGet 4.0 RTM 릴리스 정보](../release-notes/nuget-4.0-RTM.md) - NuGet 4.0 RTM에서 수정된 모든 문제를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaec-138">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="4eaec-139">기능</span><span class="sxs-lookup"><span data-stu-id="4eaec-139">Features</span></span>

- <span data-ttu-id="4eaec-140">NuGet 복원 성능 향상 - 명령줄 복원 및 VS에 대해 더 효율적인 NoOp을 구현했습니다. - [#5080](https://github.com/NuGet/Home/issues/5080)</span><span class="sxs-lookup"><span data-stu-id="4eaec-140">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="4eaec-141">.NET Core 2.0: VS/Dotnet CLI는 기존 NuGet 기능(FallBack 폴더)을 사용하여 시작해야 합니다. - [#4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="4eaec-141">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="4eaec-142">.NET Core 2.0: 사용자가 특정 복원 경고를 무시(또는 오류로 상승)하도록 설정할 수 있습니다. - [#4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="4eaec-142">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="4eaec-143">.NET Core 2.0: CLI 지역화된 어셈블리 - [#4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="4eaec-143">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="4eaec-144">.NET Core 2.0: 모든 경고/오류(PackageTargetFallback 포함)를 자산 파일에 등록할 수 있습니다. - [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="4eaec-144">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="4eaec-145">TFM 지원 사용: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="4eaec-145">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="4eaec-146">NuGet.Core 및 NuGet.Client 프로젝트(이에 따라 DLL) 수를 줄입니다. - [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="4eaec-146">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="4eaec-147">NuGet 경고를 오류로 표시하는 기능을 추가합니다. - [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="4eaec-147">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="4eaec-148">버그</span><span class="sxs-lookup"><span data-stu-id="4eaec-148">Bugs</span></span>

- <span data-ttu-id="4eaec-149">"PackTask" 작업에서 지원되지 않는 "DevelopmentDependency" 매개 변수로 인해 msbuild /t:pack이 실패합니다. - [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="4eaec-149">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="4eaec-150">PackagePath의 끝에 Windows 디렉터리 구분 기호를 추가하지 않으면 콘텐츠 파일에 대한 디렉터리 구조가 평면화되지 않습니다. - [#4795](https://github.com/NuGet/Home/issues/4795)</span><span class="sxs-lookup"><span data-stu-id="4eaec-150">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="4eaec-151">.NET Core 프로젝트는 설정을 developmentDependency로 지원하지 않습니다. - [#4694](https://github.com/NuGet/Home/issues/4694)</span><span class="sxs-lookup"><span data-stu-id="4eaec-151">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="4eaec-152">동기식으로 로드되는 RestoreManagerPackage에서 VS 교착 상태가 발생한 UI 스레드를 차단합니다. - [#4679](https://github.com/NuGet/Home/issues/4679)</span><span class="sxs-lookup"><span data-stu-id="4eaec-152">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="4eaec-153">dotnet</span><span class="sxs-lookup"><span data-stu-id="4eaec-153">dotnet</span></span>
  - <span data-ttu-id="4eaec-154">dotnetcore Restore(따라서 msbuild /t:restore)는 명시적 솔루션 프로젝트 종속성이 있는 프로젝트를 건너뜁니다. - [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="4eaec-154">dotnetcore Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="4eaec-155">솔루션에 다른 대/소문자 구분 기능으로 동일한 프로젝트를 참조하는 projectreferences가 있는 경우 복원이 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4eaec-155">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="4eaec-156">또한 이는 대/소문자 구분 기능에 차이가 없는 다른 상대 경로에도 영향을 미칩니다. - [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="4eaec-156">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="4eaec-157">NuGet 패키지에서 복원된 실행 파일은 .NET Core 2.0에서 더 이상 실행되지 않습니다. - [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="4eaec-157">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="4eaec-158">NuGet.exe에서 솔루션 파일을 구문 분석할 때 예외에 대한 세부 정보를 숨깁니다. - [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="4eaec-158">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="4eaec-159">Windows에서 '/'로 끝나는 경로가 ContentTargetFolders에 포함된 경우 콘텐츠 파일을 잘못된 위치에 넣습니다. - [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="4eaec-159">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="4eaec-160">netcoreapp1.1을 대상으로 하는 도구 패키지에 대한 DotNetCliToolReference를 복원할 수 없습니다. - [#4396](https://github.com/NuGet/Home/issues/4396)</span><span class="sxs-lookup"><span data-stu-id="4eaec-160">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="4eaec-161">NuGet 업데이트 CLI가 프로젝트 파일(C++)에서 이전 패키지 버전 조건을 유지합니다. - [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="4eaec-161">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="4eaec-162">DCR</span><span class="sxs-lookup"><span data-stu-id="4eaec-162">DCRs</span></span>

- <span data-ttu-id="4eaec-163">CPS 지정에서 DotnetCliToolTargetFramework를 읽습니다. - [#5397](https://github.com/NuGet/Home/issues/5397)</span><span class="sxs-lookup"><span data-stu-id="4eaec-163">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="4eaec-164">프로젝트 스타일 UWP에서 TPMinV 검사가 작동해야 합니다. - [#4763](https://github.com/NuGet/Home/issues/4763)</span><span class="sxs-lookup"><span data-stu-id="4eaec-164">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="4eaec-165">AutoReferenced 패키지에 대한 UI 설명이 향상되었습니다. - [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="4eaec-165">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="4eaec-166">NuGet 복원은 런타임 섹션에서 자산을 컴파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4eaec-166">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="4eaec-167"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="4eaec-167"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="4eaec-168">잠금 파일에 종속성 진단을 넣습니다. - [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="4eaec-168">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="4eaec-169">4.3 RTM에서 수정된 GitHub 문제에 대한 링크</span><span class="sxs-lookup"><span data-stu-id="4eaec-169">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="4eaec-170">문제 목록</span><span class="sxs-lookup"><span data-stu-id="4eaec-170">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")