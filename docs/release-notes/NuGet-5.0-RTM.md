---
title: NuGet 5.0 RTM 릴리스 정보
description: 알려진된 문제, 버그 수정, 새로운 기능 및 Dcr 포함 하 여 NuGet 5.0에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 5e48ff19ea5c4908d7eb0a3cb19a31b738e348eb
ms.sourcegitcommit: 8793f528a11bd8e8fb229cd12e9abba50d61e104
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2019
ms.locfileid: "58921587"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="9ce94-103">NuGet 5.0 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="9ce94-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="9ce94-104">NuGet 배포 차량:</span><span class="sxs-lookup"><span data-stu-id="9ce94-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="9ce94-105">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="9ce94-105">NuGet version</span></span> | <span data-ttu-id="9ce94-106">Visual Studio 버전에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="9ce94-106">Available in Visual Studio version</span></span>| <span data-ttu-id="9ce94-107">.NET SDK에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="9ce94-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [**<span data-ttu-id="9ce94-108">5.0.0</span><span class="sxs-lookup"><span data-stu-id="9ce94-108">5.0.0</span></span>**](https://nuget.org/downloads) | [<span data-ttu-id="9ce94-109">Visual Studio 2019 버전 16.0</span><span class="sxs-lookup"><span data-stu-id="9ce94-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="9ce94-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="9ce94-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="9ce94-111"><sup>1</sup>.NET Core 워크 로드를 사용 하 여 Visual Studio 2019와 함께 설치</span><span class="sxs-lookup"><span data-stu-id="9ce94-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="9ce94-112"><sup>2</sup>.NET Core 워크 로드를 사용 하 여 Visual Studio 2019를 사용 하 여 설치를 선택적으로 사용 가능</span><span class="sxs-lookup"><span data-stu-id="9ce94-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="9ce94-113">요약: 5.0의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="9ce94-113">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="9ce94-114">복원에 대 한 지원을 [솔루션을 필터링](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) 에서 Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="9ce94-114">Support for restoring [filtered solutions](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* `BuildTransitive` <span data-ttu-id="9ce94-115">폴더에 패키지를 호스트 프로젝트에 대상/props를 전이적으로 적용할 수 있도록 [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="9ce94-115">folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="9ce94-116">NuGet Iv api-PackageReference 시나리오에 대 한 지원 향상 [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="9ce94-116">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* `nuget.exe pack project.json` <span data-ttu-id="9ce94-117">has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="9ce94-117">has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="9ce94-118">Gen 1 자격 증명 공급자 플러그 인으로 대체 되었습니다 [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) 되며 곧 사용 되지 않음- [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="9ce94-118">Gen 1 Credential Provider plugin has been superseded by [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="9ce94-119">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="9ce94-119">Issues fixed in this release</span></span>

**<span data-ttu-id="9ce94-120">버그</span><span class="sxs-lookup"><span data-stu-id="9ce94-120">Bugs</span></span>**

* <span data-ttu-id="9ce94-121">방지 NoOp 복원 작업을 수행 하는 경우 \*. obj 디렉터리-dgspec.json 쓰기 [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="9ce94-121">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="9ce94-122">~/.Nuget 내에서 생성 된 파일에 대 한 권한이 너무 열려- [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="9ce94-122">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* `dotnet list package --outdated` <span data-ttu-id="9ce94-123">인증-는 소스를 사용 하 여 작동 하지 않습니다 [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="9ce94-123">doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="9ce94-124">NuGet.VisualStudio.IVsPackageInstaller-없는 패키지를 사용 하 여 프로젝트에 대 한 호출 참조 항상 사용 하 여 packages.config를 PackageReference-기본값은 설정 하는 경우에 [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="9ce94-124">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="9ce94-125">PMC: 업데이트 패키지 목록 패키지에 실패 하면 ("패키지를 찾을 수 없음")를 다시 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ce94-125">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="9ce94-126"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="9ce94-126"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="9ce94-127">리포지토리 및-VSIX에 제 3 자 통지 추가 [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="9ce94-127">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="9ce94-128">-지정 된 버전이 없는 경우 최신 버전을 설치 해야 하는 NuGet.VisualStudio.IVsPackageInstaller.InstallPackage [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="9ce94-128">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="9ce94-129">-dotnet nuget push 대화형 지원- [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="9ce94-129">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="9ce94-130">잠금 파일을 사용 하 여 복원 NU1603 경고 발생 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ce94-130">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="9ce94-131"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="9ce94-131"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="9ce94-132">NuGet은 최소 로깅으로-복원 하는 동안 프로젝트 경로 인쇄 하지 [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="9ce94-132">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="9ce94-133">-dotnet 용 대화형 지원 패키지를 제거 하는 데 사용- [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="9ce94-133">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="9ce94-134">추가 NuGet.Packaging.Core TypeForwardedTo 기록 속성-를 사용 하 여 다시 [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="9ce94-134">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="9ce94-135">plugins_cache 해야도 작동 하려면 더 짧은 경로 [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="9ce94-135">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="9ce94-136">사용자 특정 msbuild 버전-요청 하지 않은 경우 msbuild 검색에 대 한 경로 선호 [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="9ce94-136">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* `nuget.exe /?` <span data-ttu-id="9ce94-137">올바른 msbuild 버전을 나열 해야 [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="9ce94-137">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="9ce94-138">NuGet.targets(498,5): 오류: 경로의 일부를 찾을 수 없습니다 ' / tmp/NuGetScratch--mono에서 [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="9ce94-138">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="9ce94-139">복원에는 불필요 하 게 컴퓨터 캐시-참조 되는 패키지의 모든 버전의 내용을 열거 [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="9ce94-139">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="9ce94-140">설치 및 2019 미리 보기로 제공 후 항상 MSBuild 자동 검색 16.0 선택 [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="9ce94-140">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="9ce94-141">솔루션에서 dotnet 목록 패키지 프레임 워크-에 대 한 중복 항목을 출력 [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="9ce94-141">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="9ce94-142">예외 "빈 경로 이름이 잘못 되었습니다." 이전에 호출 IVsPackageInstaller.InstallPackage 프로젝트 및 패키지 폴더 때 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ce94-142">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="9ce94-143"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="9ce94-143"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="9ce94-144">msbuild /t: restore가 최소 자세한 정도-최소화 해야 [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="9ce94-144">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="9ce94-145">VS 16.0의 NuGet UI에 읽을 수 없는 탭 색-문제로 [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="9ce94-145">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="9ce94-146">NuGet.Core 및 NuGet.Clients License.txt 설명이- [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="9ce94-146">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="9ce94-147">복원 유형-확인 하려고 시도할 때 전역 패키지 폴더를 불필요 하 게 열거 [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="9ce94-147">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="9ce94-148">잠금 파일 적용에서 오류-오류 목록 창에 표시 해야 [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="9ce94-148">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="9ce94-149">NuGet.Configuration 문제 해결 [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="9ce94-149">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="9ce94-150">MSBuild 해당 설치 업데이트를 적용할 위치- [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="9ce94-150">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="9ce94-151">NuGet.Build.Tasks.Pack 개발 종속성-해야 [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="9ce94-151">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="9ce94-152">포함에 대 한 팩 확장 지점을 추가할 디버그 기호- [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="9ce94-152">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* `dotnet pack` <span data-ttu-id="9ce94-153">(짝수 부동 버전을 사용 하는 경우)-nupkg 생성된에서 종속성 버전 범위를 유지 해야 [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="9ce94-153">should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* `dotnet restore` <span data-ttu-id="9ce94-154">인증된 원본 소스-역시 사용자 수준 구성 하는 경우에 실패 [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="9ce94-154">fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="9ce94-155">팩 콘텐츠 파일에 대 한 BuildActions 집합이 제한 하지 [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="9ce94-155">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="9ce94-156">되려면 AssetTargetFallback 해야 하는 ProjectReference를 사용 하 게 경고 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ce94-156">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="9ce94-157"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="9ce94-157"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="9ce94-158">CPS (CommonProjectSystem-)를 호출 하는 경우 스레딩 문제로 인해 교착 상태가 [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="9ce94-158">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* `dotnet add package` <span data-ttu-id="9ce94-159">로컬 구성-에 지정 된 원본에 대 한 전역 구성에서 자격 증명을 사용 하지 않습니다 [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="9ce94-159">doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="9ce94-160">비동기에서 호출 되는 MEF 사용 하 여 스레딩 문제 코드 경로- [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="9ce94-160">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="9ce94-161">서명: 오류가 보고 되는 두 번 및 호출 스택을-없이 [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="9ce94-161">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="9ce94-162">신뢰할 수 없는 서명 인증서를 사용 하 여 서명된 된 패키지를 설치 오류-표시할지 [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="9ce94-162">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="9ce94-163">2 프로젝트 obj 디렉터리를 공유 하는 경우 NuGet 복원 괜찮음 부적절 하 게 [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="9ce94-163">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="9ce94-164">사용 하 여 PAT를 사용할 수 없습니다 `dotnet restore` -인증 된 피드의 패키지를 사용 하 여 Linux에서 [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="9ce94-164">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="9ce94-165">사용할 수 없는 컴퓨터 와이드 피드-인해 dotnet restore가 실패 [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="9ce94-165">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

**<span data-ttu-id="9ce94-166">DCR</span><span class="sxs-lookup"><span data-stu-id="9ce94-166">DCRs</span></span>**

* <span data-ttu-id="9ce94-167">"Dotnet 팩 project.json"-향후 제거의 경고 [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="9ce94-167">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="9ce94-168">Gen1 자격 증명 플러그 인-에 대 한 사용 중단 경고가 추가 [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="9ce94-168">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="9ce94-169">서명: RepositorySignatures/5.0.0 리소스를 통해 모든 패키지의 리포지토리로 클라이언트 인증을 요구 하는 사용된 리포지토리 서명 [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="9ce94-169">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="9ce94-170">원본당 NuGet.Config-를 통해 http 요청 수를 제한 [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="9ce94-170">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="9ce94-171">NuGet (하는 데 VSIX의 16.0 빌드 정리) Net472-대상으로 지정 해야 [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="9ce94-171">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="9ce94-172">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="9ce94-172">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="9ce94-173">확인 NetCoreApp 3.0 매핑할 NetStandard 2.1- [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="9ce94-173">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="9ce94-174">NuGet.\* 패키지-netstandard2.0 지원을 추가할 [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="9ce94-174">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="9ce94-175">빌드 자산 전이적 동작을 정의 하는 패키지 작성자 허용 [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="9ce94-175">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="9ce94-176">VS 2019 솔루션 필터 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ce94-176">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="9ce94-177">또한 솔루션에 없는 프로젝트 또는 언로드된 프로젝트를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9ce94-177">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="9ce94-178">(CLI 또는 VS)를 통해 완전 한 솔루션을 먼저 복원 해야 [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="9ce94-178">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="9ce94-179">.NET 4.7.2 (TFM 변경)-를 통해 할 NuGet 5.0 어셈블리 [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="9ce94-179">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="9ce94-180">NuGetLicenseData NuGet.Packaging에서 공용 유형 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ce94-180">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="9ce94-181">Spdx에서 수집 하는 라이선스 메타 데이터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ce94-181">Update license metadata ingested from spdx.</span></span><span data-ttu-id="9ce94-182"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="9ce94-182"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="9ce94-183">사용 되지 않는 설정을 Api-제거 [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="9ce94-183">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="9ce94-184">해결 방법 복원 시간 제한이 1 사용 하 여 시스템에서 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="9ce94-184">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="9ce94-185">NuGet.config에서 자격 증명이 있는 경우에 NuGet에서 NTLM 인증-자격 증명에 대 한 인증 유형을 필터링 하기 구성 옵션을 추가 [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="9ce94-185">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="9ce94-186">Packagereference (일치 하는 Packages.Config 기능)-EmbedInteropTypes 사용 [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="9ce94-186">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

**[<span data-ttu-id="9ce94-187">이 릴리스-5.0 RTM에서에서 수정 된 모든 문제 목록</span><span class="sxs-lookup"><span data-stu-id="9ce94-187">List of all issues fixed in this release - 5.0 RTM</span></span>](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="known-issues"></a><span data-ttu-id="9ce94-188">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="9ce94-188">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="9ce94-189">.NET Core SDK로 설치된 FallbackFolders의 패키지는 사용자 지정 설치되며 서명 유효성 검사에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="9ce94-189">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="9ce94-190"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="9ce94-190"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="9ce94-191">문제</span><span class="sxs-lookup"><span data-stu-id="9ce94-191">Issue</span></span>
<span data-ttu-id="9ce94-192">netcoreapp 1.x 및 netcoreapp 2.x 다중 대상을 지정하는 프로젝트를 복원하기 위해 dotnet.exe 2.x를 사용하면 대체 폴더가 파일 피드로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ce94-192">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="9ce94-193">즉 복원할 때 NuGet이 대체 폴더에서 패키지를 선택하고 전역 패키지 폴더에 설치하려고 하며 일반적인 서명 유효성 검사를 수행하지만 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="9ce94-193">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="9ce94-194">해결 방법</span><span class="sxs-lookup"><span data-stu-id="9ce94-194">Workaround</span></span>
<span data-ttu-id="9ce94-195">대체 폴더의 사용을 설정 하 여 비활성화 된 `RestoreAdditionalProjectSources` nothing으로:</span><span class="sxs-lookup"><span data-stu-id="9ce94-195">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="9ce94-196">대체 (fallback) 폴더에서 복원할 수는 패키지는 NuGet.org에서 다운로드 하는 대로 주의 해 서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ce94-196">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>
