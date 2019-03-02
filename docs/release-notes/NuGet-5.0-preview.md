---
title: NuGet 5.0 preview 릴리스 정보
description: 알려진된 문제, 버그 수정, 새로운 기능 및 Dcr 포함 하는 NuGet 5.0 미리 보기에 대 한 릴리스 정보입니다.
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 4b05dcb9a2960c1e3231e81d4b4c122d3a518753
ms.sourcegitcommit: 571644118e3c5a2fd818891d305b4b8de8ef21de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2019
ms.locfileid: "57225890"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="94d21-103">NuGet 5.0 미리 보기 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="94d21-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="94d21-104">NuGet 5.0 미리 보기 릴리스</span><span class="sxs-lookup"><span data-stu-id="94d21-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="94d21-105">2019 년 2 월 27- [NuGet 5.0 Preview 4](#whats-new-in-nuget-50-preview-4)</span><span class="sxs-lookup"><span data-stu-id="94d21-105">February 27, 2019 - [NuGet 5.0 Preview 4](#whats-new-in-nuget-50-preview-4)</span></span>
* <span data-ttu-id="94d21-106">2019 년 2 월 13- [NuGet 5.0 미리 보기 3](#whats-new-in-nuget-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="94d21-106">February 13, 2019 - [NuGet 5.0 Preview 3](#whats-new-in-nuget-50-preview-3)</span></span>
* <span data-ttu-id="94d21-107">2019 년 1 월 23- [NuGet 5.0 미리 보기 2](#whats-new-in-nuget-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="94d21-107">January 23, 2019 - [NuGet 5.0 Preview 2](#whats-new-in-nuget-50-preview-2)</span></span>

## <a name="whats-new-in-nuget-50-preview-4"></a><span data-ttu-id="94d21-108">NuGet 5.0 Preview 4의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="94d21-108">What's New in NuGet 5.0 Preview 4</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="94d21-109">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="94d21-109">Issues fixed in this release</span></span>

<span data-ttu-id="94d21-110">**버그**</span><span class="sxs-lookup"><span data-stu-id="94d21-110">**Bugs**</span></span>

* <span data-ttu-id="94d21-111">NuGet.VisualStudio.IVsPackageInstaller-없는 패키지를 사용 하 여 프로젝트에 대 한 호출 참조 항상 사용 하 여 packages.config를 PackageReference-기본값은 설정 하는 경우에 [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="94d21-111">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="94d21-112">PMC: 업데이트 패키지 목록 패키지에 실패 하면 ("패키지를 찾을 수 없음")를 다시 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="94d21-112">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="94d21-113"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="94d21-113"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="94d21-114">리포지토리 및-VSIX에 제 3 자 통지 추가 [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="94d21-114">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="94d21-115">-지정 된 버전이 없는 경우 최신 버전을 설치 해야 하는 NuGet.VisualStudio.IVsPackageInstaller.InstallPackage [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="94d21-115">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="94d21-116">-dotnet nuget push 대화형 지원- [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="94d21-116">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="94d21-117">잠금 파일을 사용 하 여 복원 NU1603 경고 발생 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94d21-117">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="94d21-118"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="94d21-118"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="94d21-119">NuGet은 최소 로깅으로-복원 하는 동안 프로젝트 경로 인쇄 하지 [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="94d21-119">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="94d21-120">-dotnet 용 대화형 지원 패키지를 제거 하는 데 사용- [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="94d21-120">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="94d21-121">추가 NuGet.Packaging.Core TypeForwardedTo 기록 속성-를 사용 하 여 다시 [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="94d21-121">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="94d21-122">plugins_cache 해야도 작동 하려면 더 짧은 경로 [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="94d21-122">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="94d21-123">사용자 특정 msbuild 버전-요청 하지 않은 경우 msbuild 검색에 대 한 경로 선호 [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="94d21-123">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

<span data-ttu-id="94d21-124">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="94d21-124">**DCRs**</span></span>

* <span data-ttu-id="94d21-125">원본당 NuGet.Config-를 통해 http 요청 수를 제한 [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="94d21-125">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="94d21-126">NuGet (하는 데 VSIX의 16.0 빌드 정리) Net472-대상으로 지정 해야 [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="94d21-126">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="94d21-127">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="94d21-127">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="94d21-128">확인 NetCoreApp 3.0 매핑할 NetStandard 2.1- [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="94d21-128">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="94d21-129">NuGet.\* 패키지-netstandard2.0 지원을 추가할 [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="94d21-129">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>


## <a name="whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="94d21-130">NuGet 5.0 미리 보기 3의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="94d21-130">What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="94d21-131">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="94d21-131">Issues fixed in this release</span></span> 

<span data-ttu-id="94d21-132">**버그**</span><span class="sxs-lookup"><span data-stu-id="94d21-132">**Bugs**</span></span>

* <span data-ttu-id="94d21-133">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="94d21-133">nuget.exe /?</span></span> <span data-ttu-id="94d21-134">올바른 msbuild 버전을 나열 해야 [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="94d21-134">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="94d21-135">NuGet.targets(498,5): 오류: 경로의 일부를 찾을 수 없습니다 ' / tmp/NuGetScratch--mono에서 [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="94d21-135">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="94d21-136">복원에는 불필요 하 게 컴퓨터 캐시-참조 되는 패키지의 모든 버전의 내용을 열거 [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="94d21-136">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="94d21-137">설치 및 2019 미리 보기로 제공 후 항상 MSBuild 자동 검색 16.0 선택 [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="94d21-137">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="94d21-138">솔루션에서 dotnet 목록 패키지 프레임 워크-에 대 한 중복 항목을 출력 [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="94d21-138">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="94d21-139">예외 "빈 경로 이름이 잘못 되었습니다." 이전에 호출 IVsPackageInstaller.InstallPackage 프로젝트 및 패키지 폴더 때 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94d21-139">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="94d21-140"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="94d21-140"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="94d21-141">msbuild /t: restore가 최소 자세한 정도-최소화 해야 [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="94d21-141">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="94d21-142">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="94d21-142">**DCRs**</span></span>

* <span data-ttu-id="94d21-143">빌드 자산 전이적 동작을 정의 하는 패키지 작성자 허용 [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="94d21-143">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="94d21-144">프로젝트를 솔루션의 일부가 아닌 또는 로드 되지 않지만 이전에 복원한-경우에 성공 하도록 VS에서 복원을 사용 하도록 설정 [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="94d21-144">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="whats-new-in-nuget-50-preview-2"></a><span data-ttu-id="94d21-145">NuGet 5.0 미리 보기 2의에서 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="94d21-145">What's New in NuGet 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="94d21-146">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="94d21-146">Issues fixed in this release</span></span>

<span data-ttu-id="94d21-147">**버그**</span><span class="sxs-lookup"><span data-stu-id="94d21-147">**Bugs**</span></span>

* <span data-ttu-id="94d21-148">VS 16.0의 NuGet UI에 읽을 수 없는 탭 색-문제로 [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="94d21-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="94d21-149">NuGet.Core 및 NuGet.Clients License.txt 설명이- [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="94d21-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="94d21-150">복원 유형-확인 하려고 시도할 때 전역 패키지 폴더를 불필요 하 게 열거 [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="94d21-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="94d21-151">잠금 파일 적용에서 오류-오류 목록 창에 표시 해야 [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="94d21-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="94d21-152">NuGet.Configuration 문제 해결 [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="94d21-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="94d21-153">MSBuild 업데이트에 맞게의 설치 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="94d21-153">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="94d21-154">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="94d21-154">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="94d21-155">NuGet.Build.Tasks.Pack 개발 종속성-해야 [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="94d21-155">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="94d21-156">포함에 대 한 팩 확장 지점을 추가할 디버그 기호- [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="94d21-156">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="94d21-157">dotnet pack에서 만든된 nupkg 종속성 버전 범위를 보존 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94d21-157">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="94d21-158">(짝수 부동 버전을 사용 하는 경우)- [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="94d21-158">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="94d21-159">사용자 수준 구성도 원본이-하는 경우 인증 된 원본에서 dotnet restore가 실패 [#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="94d21-159">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="94d21-160">팩 콘텐츠 파일에 대 한 BuildActions 집합이 제한 하지 [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="94d21-160">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="94d21-161">되려면 AssetTargetFallback 해야 하는 projectreference를 사용 하 게 경고 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94d21-161">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="94d21-162"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="94d21-162"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="94d21-163">CPS (CommonProjectSystem-)를 호출 하는 경우 스레딩 문제로 인해 교착 상태가 [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="94d21-163">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="94d21-164">dotnet 패키지 로컬 config-에 지정 된 원본에 대 한 전역 구성에서 자격 증명을 사용 하지 않습니다 추가 [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="94d21-164">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="94d21-165">스레딩 문제 MEF는 비동기 없게-호출 [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="94d21-165">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="94d21-166">서명: 오류가 보고 되는 두 번 및 호출 스택을-없이 [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="94d21-166">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="94d21-167">신뢰할 수 없는 서명 인증서를 사용 하 여 서명된 된 패키지를 설치 오류-표시할지 [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="94d21-167">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="94d21-168">2 프로젝트 obj 디렉터리를 공유 하는 경우 NuGet 복원 괜찮음 부적절 하 게 [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="94d21-168">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="94d21-169">PAT-인증 된 피드의 패키지를 사용 하 여 Linux에서 dotnet restore를 사용 하 여 사용할 수 없습니다 [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="94d21-169">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="94d21-170">사용할 수 없는 컴퓨터 와이드 피드-인해 dotnet restore가 실패 [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="94d21-170">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="94d21-171">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="94d21-171">**DCRs**</span></span>

* <span data-ttu-id="94d21-172">.NET 4.7.2 (TFM 변경)-를 통해 할 NuGet 5.0 어셈블리 [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="94d21-172">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="94d21-173">NuGetLicenseData NuGet.Packaging에서 공용 유형 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="94d21-173">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="94d21-174">Spdx에서 수집 하는 라이선스 메타 데이터를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="94d21-174">Update license metadata ingested from spdx.</span></span><span data-ttu-id="94d21-175"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="94d21-175"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="94d21-176">사용 되지 않는 설정을 Api-제거 [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="94d21-176">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="94d21-177">해결 방법 복원 시간 제한이 1 사용 하 여 시스템에서 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="94d21-177">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="94d21-178">NuGet.config에서 자격 증명이 있는 경우에 NuGet에서 NTLM 인증-자격 증명에 대 한 인증 유형을 필터링 하기 구성 옵션을 추가 [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="94d21-178">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="94d21-179">Packagereference (일치 하는 Packages.Config 기능)-EmbedInteropTypes 사용 [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="94d21-179">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="94d21-180">이 릴리스 5.0.0-preview2에서 해결 된 모든 문제 목록</span><span class="sxs-lookup"><span data-stu-id="94d21-180">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="94d21-181">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="94d21-181">Known issues</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="94d21-182">.NET Core SDK로 설치된 FallbackFolders의 패키지는 사용자 지정 설치되며 서명 유효성 검사에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="94d21-182">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="94d21-183"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="94d21-183"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="94d21-184">**문제** dotnet.exe를 사용 하는 경우 해당 다중 대상 netcoreapp 프로젝트를 복원 하려면 2.x 1.x 및 netcoreapp 2.x, 대체 폴더 피드 파일로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="94d21-184">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="94d21-185">즉 복원할 때 NuGet이 대체 폴더에서 패키지를 선택하고 전역 패키지 폴더에 설치하려고 하며 일반적인 서명 유효성 검사를 수행하지만 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="94d21-185">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="94d21-186">**해결 방법** 대체 폴더의 사용을 설정 하 여 비활성화 된 `RestoreAdditionalProjectSources` nothing으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="94d21-186">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="94d21-187">`<RestoreAdditionalProjectSources/>` NuGet.org에서 많은 패키지가 다운로드되도록 하므로 주의하여 사용하세요. 그렇지 않으면 대체 폴더에서 복원될 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="94d21-187">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
