---
title: NuGet 5.0 RTM 릴리스 정보
description: 알려진 문제, 버그 수정, 새로운 기능 및 Ecrs를 비롯 한 NuGet 5.0에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: e4a6be7fb26e3cc4bd297eaf02999f6ac1389b77
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236804"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="87627-103">NuGet 5.0 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="87627-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="87627-104">NuGet 배포 차량:</span><span class="sxs-lookup"><span data-stu-id="87627-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="87627-105">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="87627-105">NuGet version</span></span> | <span data-ttu-id="87627-106">Visual Studio 버전에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="87627-106">Available in Visual Studio version</span></span>| <span data-ttu-id="87627-107">.NET SDK에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="87627-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="87627-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="87627-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="87627-109">Visual Studio 2019 버전 16.0</span><span class="sxs-lookup"><span data-stu-id="87627-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="87627-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="87627-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="87627-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="87627-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="87627-112">Visual Studio 2019 버전 16.0.4</span><span class="sxs-lookup"><span data-stu-id="87627-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="87627-113">[2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="87627-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="87627-114"><sup>1</sup> .NET Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨</span><span class="sxs-lookup"><span data-stu-id="87627-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="87627-115"><sup>2</sup> .NET Core 워크 로드와 함께 Visual Studio 2019을 사용 하 여 선택적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87627-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="87627-116">요약: 5.0의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="87627-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="87627-117">Visual Studio 2019에서 [필터링 된 솔루션](/visualstudio/ide/filtered-solutions?view=vs-2019) 복원 지원- [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="87627-117">Support for restoring [filtered solutions](/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="87627-118">`BuildTransitive` 폴더를 사용 하면 패키지에서 대상/props을 호스트 프로젝트에 전이적으로 적용할 수 있습니다.- [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="87627-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="87627-119">NuGet Iv Api [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493) 에서 PackageReference 시나리오에 대 한 지원 향상</span><span class="sxs-lookup"><span data-stu-id="87627-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="87627-120">`nuget.exe pack project.json` 사용 되지 않음- [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="87627-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="87627-121">Gen 1 자격 증명 공급자 플러그 인이 [gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) 로 대체 되었으며 곧 사용 되지 않을 예정입니다. [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="87627-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="87627-122">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="87627-122">Issues fixed in this release</span></span>

<span data-ttu-id="87627-123">**버그**</span><span class="sxs-lookup"><span data-stu-id="87627-123">**Bugs**</span></span>

* <span data-ttu-id="87627-124">NoOp 복원 작업을 수행 하는 경우에는 .dgspec.js[#7854](https://github.com/NuGet/Home/issues/7854) obj 디렉터리에 쓸 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="87627-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="87627-125">~/.Era 내에서 만든 파일에 대 한 사용 권한이 너무 열려 [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="87627-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="87627-126">`dotnet list package --outdated` 인증이 필요한 원본에서 작동 하지 않음- [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="87627-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="87627-127">VisualStudio는 PackageReference로 설정 된 경우에도 항상 packages.config를 사용 하 여 패키지 참조가 없는 프로젝트에서 호출 [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="87627-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="87627-128">PMC: 목록에 없는 패키지에서 Update-Package 다시 설치에 실패 합니다 ("패키지를 찾을 수 없음").</span><span class="sxs-lookup"><span data-stu-id="87627-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="87627-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="87627-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="87627-130">리포지토리 및 VSIX에서 타사 공지를 추가 합니다. [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="87627-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="87627-131">VisualStudio. InstallPackage는 지정 [#7493](https://github.com/NuGet/Home/issues/7493) 된 버전이 없는 경우 최신 버전을 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87627-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="87627-132">--dotnet nuget 푸시 [#7519](https://github.com/NuGet/Home/issues/7519) 에 대 한 대화형 지원</span><span class="sxs-lookup"><span data-stu-id="87627-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="87627-133">잠금 파일을 사용 하 여 복원할 때 NU1603 경고가 발생 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87627-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="87627-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="87627-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="87627-135">NuGet은 최소한의 로깅으로 복원 하는 동안 프로젝트 경로를 인쇄할 수 없습니다.- [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="87627-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="87627-136">--dotnet 제거 패키지에 대 한 대화형 지원- [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="87627-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="87627-137">TypeForwardedTo [#7768](https://github.com/NuGet/Home/issues/7768) attrs를 사용 하 여 다시 NuGet을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="87627-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="87627-138">잘 작동 하려면 더 짧은 경로가 필요 plugins_cache [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="87627-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="87627-139">사용자가 특정 msbuild 버전을 요청 하지 않은 경우 msbuild 검색 경로를 선호 합니다. [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="87627-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="87627-140">`nuget.exe /?` 올바른 msbuild 버전을 나열 해야 합니다.- [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="87627-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="87627-141">Nuget.exe (498, 5): 오류: ' [#7793](https://github.com/NuGet/Home/issues/7793) /tmp/NuGetScratch '의 경로 부분을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="87627-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="87627-142">복원 불필요 한 모든 버전의 참조 된 패키지의 내용을 컴퓨터 캐시에 열거- [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="87627-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="87627-143">MSBuild 자동 검색은 VS 2019 Preview- [#7621](https://github.com/NuGet/Home/issues/7621) 를 설치한 후 항상 16.0을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="87627-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="87627-144">솔루션의 dotnet list 패키지는 프레임 워크에 대 한 중복 항목을 출력 합니다.- [#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="87627-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="87627-145">InstallPackage 이전 프로젝트 및 패키지 폴더에 대해 IVsPackageInstaller를 호출할 때 "빈 경로 이름이 잘못 되었습니다." 예외가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="87627-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="87627-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="87627-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="87627-147">msbuild/t: 최소한의 자세한 정도 복원의 경우는 최소 [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="87627-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="87627-148">VS 16.0의 NuGet UI에 색 문제로 인 한 읽을 수 없는 탭이 있습니다.- [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="87627-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="87627-149">Nuget. 클라이언트는 & License.txt 대 한 설명은 [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="87627-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="87627-150">복원 불필요 하 게 전역 패키지 폴더를 열거 하 여 형식 [#7596](https://github.com/NuGet/Home/issues/7596) 를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="87627-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="87627-151">파일 잠금 적용 오류는 오류 목록 창에 표시 됩니다 [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="87627-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="87627-152">NuGet.Configuration 문제 해결- [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="87627-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="87627-153">설치 위치를 업데이트 하는 MSBuild에 맞게 조정- [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="87627-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="87627-154">Nuget.exe. 작업 팩은 개발 종속성 이어야 합니다. [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="87627-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="87627-155">디버그 기호를 포함 하는 팩 확장 지점 추가- [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="87627-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="87627-156">`dotnet pack` 만든 nupkg에서 종속성 버전 범위를 유지 해야 함 (부동 버전이 사용 되는 경우에도)- [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="87627-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="87627-157">`dotnet restore`사용자 수준 구성에 소스- [#7209](https://github.com/NuGet/Home/issues/7209) 있는 경우 인증 된 원본에서 실패</span><span class="sxs-lookup"><span data-stu-id="87627-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="87627-158">Pack은 콘텐츠 파일에 대 한 BuildActions 집합을 제한 하지 않아야 합니다. [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="87627-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="87627-159">AssetTargetFallback가 성공 해야 하는 ProjectReference를 사용 하면 경고가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="87627-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="87627-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="87627-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="87627-161">CPS (CommonProjectSystem)로 호출할 때 스레딩 문제로 인 한 교착 상태- [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="87627-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="87627-162">`dotnet add package` 로컬 구성에 지정 된 원본에 대 한 전역 구성의 자격 증명을 사용 하지 않습니다- [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="87627-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="87627-163">비동기 코드 경로에서 호출 되는 MEF의 스레딩 문제- [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="87627-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="87627-164">서명: 오류는 호출 스택 없이 두 번 보고 됩니다. [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="87627-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="87627-165">신뢰할 수 없는 서명 인증서를 사용 하 여 서명 된 패키지를 설치 하면 오류 [#6318](https://github.com/NuGet/Home/issues/6318) 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="87627-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="87627-166">두 프로젝트가 obj 디렉터리를 공유 하는 경우 NuGet 복원에 부적절 한 NoOps- [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="87627-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="87627-167">`dotnet restore`인증 된 피드의 패키지와 함께 Linux에서 PAT를 사용할 수 없음- [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="87627-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="87627-168">사용 하지 않도록 설정 된 컴퓨터 전체 피드로 인해 dotnet restore 실패 함- [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="87627-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="87627-169">**DCR**</span><span class="sxs-lookup"><span data-stu-id="87627-169">**DCRs**</span></span>

* <span data-ttu-id="87627-170">나중에 "dotnet pack project.json"- [#7928](https://github.com/NuGet/Home/issues/7928) 제거에 대 한 경고</span><span class="sxs-lookup"><span data-stu-id="87627-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="87627-171">Gen1 자격 증명 플러그 인에 대 한 사용 중단 경고 추가- [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="87627-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="87627-172">서명: 리포지토리가 RepositorySignatures/5.0.0 리소스- [#7759](https://github.com/NuGet/Home/issues/7759) 를 통해 서명 된 모든 패키지의 클라이언트 확인을 요구 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="87627-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="87627-173">NuGet.Config- [#4538](https://github.com/NuGet/Home/issues/4538) 를 통해 원본 당 http 요청 수를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="87627-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="87627-174">NuGet은 Net472 (VSIX의 16.0 빌드를 정리 하기 위해)를 대상으로 해야 합니다.- [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="87627-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="87627-175">PMC: OpenPackagePage 명령 제거- [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="87627-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="87627-176">Netcoreapp1.0 3.0 map을 NetStandard 2.1로 설정- [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="87627-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="87627-177">NuGet. \* 패키지에 netstandard 2.0 지원 추가- [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="87627-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="87627-178">패키지 작성자가 빌드 자산 전이적 동작을 정의할 수 있도록 허용- [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="87627-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="87627-179">VS 2019 솔루션 필터 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="87627-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="87627-180">는 프로젝트가 솔루션에 없음 또는 언로드된 프로젝트도 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="87627-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="87627-181">전체 솔루션을 복원 해야 합니다 (CLI 또는 VS를 통해). 먼저 [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="87627-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="87627-182">TFM change를 통해 .NET 4.7.2을 요구 하는 NuGet 5.0 어셈블리- [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="87627-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="87627-183">NuGetLicenseData에서 패키징은 공용 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87627-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="87627-184">Spdx에서 라이선스 메타 데이터 수집를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="87627-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="87627-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="87627-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="87627-186">사용 되지 않는 설정 Api 제거- [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="87627-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="87627-187">1 개 cpu를 사용 하는 시스템의 복원 시간 제한 해결- [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="87627-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="87627-188">NuGet은 자격 증명에 대 한 인증 유형을 필터링 하기 위해 NuGet.config-config 추가 옵션에 자격 증명이 있는 경우에도 NTLM 인증을 선호 [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="87627-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="87627-189">PackageReference (Packages.Config 기능 일치)에 대해 EmbedInteropTypes 사용- [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="87627-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="87627-190">**[이 릴리스에서 해결 된 모든 문제 목록-5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="87627-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="87627-191">요약: 5.0.2의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="87627-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="87627-192">보안 (dotnet.exe 또는 mono.exe를 통해 실행)-올바른 권한을 사용 하 여 obj 폴더를 만들어야 [#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="87627-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="87627-193">사용자 지정 nuget.config 및 #8011에서 mono/MacOS에 대 한 nuget.exe 복원이 실패 함 `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span><span class="sxs-lookup"><span data-stu-id="87627-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="87627-194">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="87627-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="87627-195">.NET Core SDK로 설치된 FallbackFolders의 패키지는 사용자 지정 설치되며 서명 유효성 검사에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="87627-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="87627-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="87627-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="87627-197">문제</span><span class="sxs-lookup"><span data-stu-id="87627-197">Issue</span></span>
<span data-ttu-id="87627-198">netcoreapp 1.x 및 netcoreapp 2.x 다중 대상을 지정하는 프로젝트를 복원하기 위해 dotnet.exe 2.x를 사용하면 대체 폴더가 파일 피드로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="87627-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="87627-199">즉 복원할 때 NuGet이 대체 폴더에서 패키지를 선택하고 전역 패키지 폴더에 설치하려고 하며 일반적인 서명 유효성 검사를 수행하지만 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="87627-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="87627-200">해결 방법</span><span class="sxs-lookup"><span data-stu-id="87627-200">Workaround</span></span>
<span data-ttu-id="87627-201">을 nothing으로 설정 하 여 대체 폴더를 사용 하지 않도록 설정 합니다 `RestoreAdditionalProjectSources` .</span><span class="sxs-lookup"><span data-stu-id="87627-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="87627-202">대체 폴더에서 복원 되는 패키지가 이제 NuGet.org에서 다운로드 되기 때문에이를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="87627-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>