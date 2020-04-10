---
title: NuGet 4.3 RTM 릴리스 정보
description: NuGet 4.3 RTM에 대한 릴리스 정보(알려진 문제, 버그 수정, 추가된 기능 및 DCR 포함).
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 72d707cb9bacd8abbac873ee10b2fd00f233d3cc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496587"
---
# <a name="nuget-43-release-notes"></a><span data-ttu-id="69f11-103">NuGet 4.3 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="69f11-103">NuGet 4.3 Release Notes</span></span>

<span data-ttu-id="69f11-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes)는 .NET Standard 2.0/.NET Core 2.0과 같은 새로운 시나리오에 대한 지원을 추가하고, 많은 품질 수정을 포함하며, 성능을 향상시키는 NuGet 4.3 RTM과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="69f11-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="69f11-105">또한 이 릴리스에는 유의적 버전 2.0.0 지원, NuGet 경고/오류의 MSBuild 통합 등과 같이 향상된 몇 가지 기능도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="69f11-105">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="summary-whats-new-in-430"></a><span data-ttu-id="69f11-106">요약: 4.3.0의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="69f11-106">Summary: What's New in 4.3.0</span></span>

## <a name="summary-whats-new-in-431"></a><span data-ttu-id="69f11-107">요약: 4.3.1의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="69f11-107">Summary: What's New in 4.3.1</span></span>

* <span data-ttu-id="69f11-108">보안 수정: ~/.nuget 내에서 만든 파일에 대한 권한이 열려 있습니다. [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="69f11-108">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>
* <span data-ttu-id="69f11-109">보안 수정: NUPKG 내부에 있는 파일에는 NUPKG 디렉터리 위의 상대 경로가 포함될 수 있습니다. [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="69f11-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="69f11-110">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="69f11-110">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="69f11-111">일부 경우에 NuGet 복원이 사용하지 않도록 설정된 패키지 소스를 사용 설정된 것으로 처리할 수 있음</span><span class="sxs-lookup"><span data-stu-id="69f11-111">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="69f11-112">문제점</span><span class="sxs-lookup"><span data-stu-id="69f11-112">Issue</span></span>

<span data-ttu-id="69f11-113">다음 restore 명령줄 기술은 사용하지 않도록 설정된 패키지 원본을 사용 가능한 것으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="69f11-113">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="69f11-114">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="69f11-114">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="69f11-115">`dotnet restore`(VS와 함께 제공되는 dotnet.exe 또는 NetCore SDK 2.0.0과 함께 제공되는 dotnet.exe 사용)</span><span class="sxs-lookup"><span data-stu-id="69f11-115">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="69f11-116">해결 방법</span><span class="sxs-lookup"><span data-stu-id="69f11-116">Workaround</span></span>

1. <span data-ttu-id="69f11-117">Visual Studio(2017 15.3 이상) 또는 NuGet.exe(v4.3.0 이상) 사용</span><span class="sxs-lookup"><span data-stu-id="69f11-117">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="69f11-118">사용할 수 없는 소스를 삭제하고 msbuild 또는 dotnet.exe를 계속 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69f11-118">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="69f11-119">솔루션에 대해 NuGet.config에서 “Clear”를 사용한 다음, 해당 솔루션에 필요한 소스를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f11-119">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="69f11-120">패키지 관리자 콘솔을 사용하는 동안 'Enter' 키가 작동하지 않을 수 있음</span><span class="sxs-lookup"><span data-stu-id="69f11-120">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="69f11-121">문제점</span><span class="sxs-lookup"><span data-stu-id="69f11-121">Issue</span></span>

<span data-ttu-id="69f11-122">경우에 따라 패키지 관리자 콘솔에서 Enter 키가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69f11-122">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="69f11-123">이런 경우 수정 진행 상황을 확인하고 재현 단계에 대해 도움이 되는 추가 정보를 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="69f11-123">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="69f11-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="69f11-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="69f11-125">해결 방법</span><span class="sxs-lookup"><span data-stu-id="69f11-125">Workaround</span></span>

<span data-ttu-id="69f11-126">Visual Studio를 다시 시작하고 솔루션을 열기 전에 PMC를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="69f11-126">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="69f11-127">또는 `project.lock.json`을 삭제하고 다시 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="69f11-127">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="69f11-128">NuGet 패키지 관리자를 사용하여 DotNetCLITools를 보거나 추가 또는 업데이트할 수 없음</span><span class="sxs-lookup"><span data-stu-id="69f11-128">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="69f11-129">문제점</span><span class="sxs-lookup"><span data-stu-id="69f11-129">Issue</span></span>

<span data-ttu-id="69f11-130">NuGet 패키지 관리자는 DotNetCLITools 추가/업데이트를 표시하지 않으며 허용하지도 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69f11-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="69f11-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="69f11-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="69f11-132">해결 방법</span><span class="sxs-lookup"><span data-stu-id="69f11-132">Workaround</span></span>

<span data-ttu-id="69f11-133">프로젝트 파일에서 DotNetCLIToolReferences를 수동으로 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f11-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="69f11-134">대상 프레임워크 버전의 대상을 변경하면 불완전한 IntelliSense가 발생할 수 있음</span><span class="sxs-lookup"><span data-stu-id="69f11-134">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="69f11-135">문제점</span><span class="sxs-lookup"><span data-stu-id="69f11-135">Issue</span></span>

<span data-ttu-id="69f11-136">Visual Studio에서 대상 프레임워크 버전의 대상을 변경하면 불완전한 IntelliSense가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f11-136">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="69f11-137">이 문제는 PackageReferences를 패키지 관리자 형식으로 사용하는 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="69f11-137">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="69f11-138">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="69f11-138">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="69f11-139">해결 방법</span><span class="sxs-lookup"><span data-stu-id="69f11-139">Workaround</span></span>

<span data-ttu-id="69f11-140">수동 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="69f11-140">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="69f11-141">NuGet 4.3 RTM 기간에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="69f11-141">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="69f11-142">[NuGet 4.0 RTM 릴리스 정보](../release-notes/nuget-4.0-RTM.md) - NuGet 4.0 RTM에서 수정된 모든 문제를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="69f11-142">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="69f11-143">기능</span><span class="sxs-lookup"><span data-stu-id="69f11-143">Features</span></span>

- <span data-ttu-id="69f11-144">NuGet 복원 성능 향상 - 명령줄 복원 및 VS에 대해 더 효율적인 NoOp을 구현했습니다. - [#5080](https://github.com/NuGet/Home/issues/5080)</span><span class="sxs-lookup"><span data-stu-id="69f11-144">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="69f11-145">NET Core 2.0: VS/Dotnet CLI는 기존 NuGet 기능(대체 폴더)을 사용하여 시작해야 합니다. - [#4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="69f11-145">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="69f11-146">NET Core 2.0: 사용자가 특정 복원 경고를 무시(또는 오류로 상승)하도록 설정할 수 있습니다. - [#4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="69f11-146">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="69f11-147">NET Core 2.0: CLI 지역화된 어셈블리 - [#4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="69f11-147">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="69f11-148">.NET Core 2.0: 모든 경고/오류(PackageTargetFallback 포함)를 자산 파일에 등록할 수 있습니다. - [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="69f11-148">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="69f11-149">TFM 지원 사용: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="69f11-149">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="69f11-150">NuGet.Core 및 NuGet.Client 프로젝트(이에 따라 DLL) 수를 줄입니다. - [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="69f11-150">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="69f11-151">NuGet 경고를 오류로 표시하는 기능을 추가합니다. - [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="69f11-151">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="69f11-152">버그</span><span class="sxs-lookup"><span data-stu-id="69f11-152">Bugs</span></span>

- <span data-ttu-id="69f11-153">"PackTask" 작업에서 지원되지 않는 "DevelopmentDependency" 매개 변수로 인해 msbuild /t:pack이 실패합니다. - [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="69f11-153">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="69f11-154">PackagePath의 끝에 Windows 디렉터리 구분 기호를 추가하지 않으면 콘텐츠 파일에 대한 디렉터리 구조가 평면화되지 않습니다. - [#4795](https://github.com/NuGet/Home/issues/4795)</span><span class="sxs-lookup"><span data-stu-id="69f11-154">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="69f11-155">.NET Core 프로젝트는 설정을 developmentDependency로 지원하지 않습니다. - [#4694](https://github.com/NuGet/Home/issues/4694)</span><span class="sxs-lookup"><span data-stu-id="69f11-155">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="69f11-156">동기식으로 로드되는 RestoreManagerPackage에서 VS 교착 상태가 발생한 UI 스레드를 차단합니다. - [#4679](https://github.com/NuGet/Home/issues/4679)</span><span class="sxs-lookup"><span data-stu-id="69f11-156">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="69f11-157">dotnet</span><span class="sxs-lookup"><span data-stu-id="69f11-157">dotnet</span></span>
  - <span data-ttu-id="69f11-158">dotnetcore Restore(따라서 msbuild /t:restore)는 명시적 솔루션 프로젝트 종속성이 있는 프로젝트를 건너뜁니다. - [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="69f11-158">dotnetcore Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="69f11-159">솔루션에 다른 대/소문자 구분 기능으로 동일한 프로젝트를 참조하는 projectreferences가 있는 경우 복원이 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f11-159">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="69f11-160">또한 이는 대/소문자 구분 기능에 차이가 없는 다른 상대 경로에도 영향을 미칩니다. - [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="69f11-160">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="69f11-161">NuGet 패키지에서 복원된 실행 파일은 .NET Core 2.0에서 더 이상 실행되지 않습니다. - [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="69f11-161">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="69f11-162">NuGet.exe에서 솔루션 파일을 구문 분석할 때 예외에 대한 세부 정보를 숨깁니다. - [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="69f11-162">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="69f11-163">Windows에서 '/'로 끝나는 경로가 ContentTargetFolders에 포함된 경우 콘텐츠 파일을 잘못된 위치에 넣습니다. - [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="69f11-163">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="69f11-164">netcoreapp1.1을 대상으로 하는 도구 패키지에 대한 DotNetCliToolReference를 복원할 수 없습니다. - [#4396](https://github.com/NuGet/Home/issues/4396)</span><span class="sxs-lookup"><span data-stu-id="69f11-164">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="69f11-165">NuGet 업데이트 CLI가 프로젝트 파일(C++)에서 이전 패키지 버전 조건을 유지합니다. - [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="69f11-165">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="69f11-166">DCR</span><span class="sxs-lookup"><span data-stu-id="69f11-166">DCRs</span></span>

- <span data-ttu-id="69f11-167">CPS 지정에서 DotnetCliToolTargetFramework를 읽습니다. - [#5397](https://github.com/NuGet/Home/issues/5397)</span><span class="sxs-lookup"><span data-stu-id="69f11-167">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="69f11-168">프로젝트 스타일 UWP에서 TPMinV 검사가 작동해야 합니다. - [#4763](https://github.com/NuGet/Home/issues/4763)</span><span class="sxs-lookup"><span data-stu-id="69f11-168">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="69f11-169">AutoReferenced 패키지에 대한 UI 설명이 향상되었습니다. - [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="69f11-169">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="69f11-170">NuGet 복원은 런타임 섹션에서 자산을 컴파일을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="69f11-170">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="69f11-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="69f11-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="69f11-172">잠금 파일에 종속성 진단을 넣습니다. - [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="69f11-172">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="69f11-173">4\.3 RTM에서 수정된 GitHub 문제에 대한 링크</span><span class="sxs-lookup"><span data-stu-id="69f11-173">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="69f11-174">문제 목록</span><span class="sxs-lookup"><span data-stu-id="69f11-174">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
