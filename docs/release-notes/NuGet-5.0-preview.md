---
title: NuGet 5.0 preview 릴리스 정보
description: 알려진된 문제, 버그 수정, 새로운 기능 및 Dcr 포함 하는 NuGet 5.0 미리 보기에 대 한 릴리스 정보입니다.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 5889ea52f993fa8fe841f8eb83b6da659cdede93
ms.sourcegitcommit: 1ab750ff17e55c763d646c50e7630138804ce8b8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247661"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="52714-103">NuGet 5.0 미리 보기 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="52714-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="52714-104">NuGet 5.0 미리 보기 릴리스</span><span class="sxs-lookup"><span data-stu-id="52714-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="52714-105">2019 년 2 월 13- [NuGet 5.0 미리 보기 3](#summary-whats-new-in-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="52714-105">February 13, 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span></span>
* <span data-ttu-id="52714-106">2019 년 1 월 23- [NuGet 5.0 미리 보기 2](#summary-whats-new-in-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="52714-106">January 23, 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span></span>

## <a name="summary-whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="52714-107">요약: NuGet 5.0 미리 보기 3의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="52714-107">Summary: What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="52714-108">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="52714-108">Issues fixed in this release</span></span> 

<span data-ttu-id="52714-109">**버그:**</span><span class="sxs-lookup"><span data-stu-id="52714-109">**Bugs:**</span></span>

* <span data-ttu-id="52714-110">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="52714-110">nuget.exe /?</span></span> <span data-ttu-id="52714-111">올바른 msbuild 버전을 나열 해야 [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="52714-111">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="52714-112">NuGet.targets(498,5): 오류: 경로의 일부를 찾을 수 없습니다 ' / tmp/NuGetScratch--mono에서 [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="52714-112">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="52714-113">복원에는 불필요 하 게 컴퓨터 캐시-참조 되는 패키지의 모든 버전의 내용을 열거 [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="52714-113">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="52714-114">설치 및 2019 미리 보기로 제공 후 항상 MSBuild 자동 검색 16.0 선택 [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="52714-114">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="52714-115">솔루션에서 dotnet 목록 패키지 프레임 워크-에 대 한 중복 항목을 출력 [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="52714-115">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="52714-116">예외 "빈 경로 이름이 잘못 되었습니다." 이전에 호출 IVsPackageInstaller.InstallPackage 프로젝트 및 패키지 폴더 때 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="52714-116">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="52714-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="52714-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="52714-118">msbuild /t: restore가 최소 자세한 정도-최소화 해야 [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="52714-118">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="52714-119">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="52714-119">**DCRs**</span></span>

* <span data-ttu-id="52714-120">빌드 자산 전이적 동작을 정의 하는 패키지 작성자 허용 [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="52714-120">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="52714-121">프로젝트를 솔루션의 일부가 아닌 또는 로드 되지 않지만 이전에 복원한-경우에 성공 하도록 VS에서 복원을 사용 하도록 설정 [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="52714-121">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="52714-122">요약: 5.0 미리 보기 2의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="52714-122">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="52714-123">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="52714-123">Issues fixed in this release</span></span>

<span data-ttu-id="52714-124">**버그:**</span><span class="sxs-lookup"><span data-stu-id="52714-124">**Bugs:**</span></span>

* <span data-ttu-id="52714-125">VS 16.0의 NuGet UI에 읽을 수 없는 탭 색-문제로 [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="52714-125">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="52714-126">NuGet.Core 및 NuGet.Clients License.txt 설명이- [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="52714-126">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="52714-127">복원 유형-확인 하려고 시도할 때 전역 패키지 폴더를 불필요 하 게 열거 [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="52714-127">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="52714-128">잠금 파일 적용에서 오류-오류 목록 창에 표시 해야 [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="52714-128">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="52714-129">NuGet.Configuration 문제 해결 [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="52714-129">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="52714-130">MSBuild 업데이트에 맞게의 설치 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="52714-130">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="52714-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="52714-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="52714-132">NuGet.Build.Tasks.Pack 개발 종속성-해야 [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="52714-132">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="52714-133">포함에 대 한 팩 확장 지점을 추가할 디버그 기호- [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="52714-133">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="52714-134">dotnet pack에서 만든된 nupkg 종속성 버전 범위를 보존 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52714-134">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="52714-135">(짝수 부동 버전을 사용 하는 경우)- [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="52714-135">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="52714-136">사용자 수준 구성도 원본이-하는 경우 인증 된 원본에서 dotnet restore가 실패 [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="52714-136">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="52714-137">팩 콘텐츠 파일에 대 한 BuildActions 집합이 제한 하지 [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="52714-137">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="52714-138">되려면 AssetTargetFallback 해야 하는 projectreference를 사용 하 게 경고 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52714-138">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="52714-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="52714-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="52714-140">CPS (CommonProjectSystem-)를 호출 하는 경우 스레딩 문제로 인해 교착 상태가 [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="52714-140">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="52714-141">dotnet 패키지 로컬 config-에 지정 된 원본에 대 한 전역 구성에서 자격 증명을 사용 하지 않습니다 추가 [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="52714-141">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="52714-142">스레딩 문제 MEF는 비동기 없게-호출 [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="52714-142">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="52714-143">서명: 오류가 보고 되는 두 번 및 호출 스택을-없이 [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="52714-143">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="52714-144">신뢰할 수 없는 서명 인증서를 사용 하 여 서명된 된 패키지를 설치 오류-표시할지 [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="52714-144">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="52714-145">2 프로젝트 obj 디렉터리를 공유 하는 경우 NuGet 복원 괜찮음 부적절 하 게 [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="52714-145">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="52714-146">PAT-인증 된 피드의 패키지를 사용 하 여 Linux에서 dotnet restore를 사용 하 여 사용할 수 없습니다 [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="52714-146">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="52714-147">사용할 수 없는 컴퓨터 와이드 피드-인해 dotnet restore가 실패 [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="52714-147">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="52714-148">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="52714-148">**DCRs**</span></span>

* <span data-ttu-id="52714-149">.NET 4.7.2 (TFM 변경)-를 통해 할 NuGet 5.0 어셈블리 [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="52714-149">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="52714-150">NuGetLicenseData NuGet.Packaging에서 공용 유형 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="52714-150">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="52714-151">Spdx에서 수집 하는 라이선스 메타 데이터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="52714-151">Update license metadata ingested from spdx.</span></span><span data-ttu-id="52714-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="52714-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="52714-153">사용 되지 않는 설정을 Api-제거 [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="52714-153">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="52714-154">해결 방법 복원 시간 제한이 1 사용 하 여 시스템에서 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="52714-154">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="52714-155">NuGet.config에서 자격 증명이 있는 경우에 NuGet에서 NTLM 인증-자격 증명에 대 한 인증 유형을 필터링 하기 구성 옵션을 추가 [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="52714-155">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="52714-156">Packagereference (일치 하는 Packages.Config 기능)-EmbedInteropTypes 사용 [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="52714-156">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="52714-157">이 릴리스 5.0.0-preview2에서 해결 된 모든 문제 목록</span><span class="sxs-lookup"><span data-stu-id="52714-157">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="52714-158">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="52714-158">Known issues</span></span>

#### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="52714-159">dotnet nuget 푸시 --interactive로 인해 Mac에서 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="52714-159">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="52714-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="52714-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>
<span data-ttu-id="52714-161">**문제** 는 `--interactive` 인수는 dotnet cli를 통해 전달 되지 않습니다 및 오류 발생 `error: Missing value for option 'interactive'` 
 **해결** 같은대화형옵션을사용하여다른dotnet명령실행`dotnet restore --interactive` 하 고 인증 합니다.</span><span class="sxs-lookup"><span data-stu-id="52714-161">**Issue** The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`
**Workaround** Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="52714-162">인증은 자격 증명 공급자에 의해 캐시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="52714-162">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="52714-163">그런 다음, `dotnet nuget push`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="52714-163">Then run `dotnet nuget push`.</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="52714-164">.NET Core SDK로 설치된 FallbackFolders의 패키지는 사용자 지정 설치되며 서명 유효성 검사에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="52714-164">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="52714-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="52714-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="52714-166">**문제** dotnet.exe를 사용 하는 경우 해당 다중 대상 netcoreapp 프로젝트를 복원 하려면 2.x 1.x 및 netcoreapp 2.x, 대체 폴더 피드 파일로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="52714-166">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="52714-167">즉 복원할 때 NuGet이 대체 폴더에서 패키지를 선택하고 전역 패키지 폴더에 설치하려고 하며 일반적인 서명 유효성 검사를 수행하지만 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="52714-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="52714-168">**해결 방법** 대체 폴더의 사용을 설정 하 여 비활성화 된 `RestoreAdditionalProjectSources` nothing으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="52714-168">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="52714-169">`<RestoreAdditionalProjectSources/>` NuGet.org에서 많은 패키지가 다운로드되도록 하므로 주의하여 사용하세요. 그렇지 않으면 대체 폴더에서 복원될 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="52714-169">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
