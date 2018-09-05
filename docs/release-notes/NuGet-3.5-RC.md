---
title: 3.5 RC 릴리스 정보
description: NuGet 3.5 RC 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548540"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="1cfe5-103">NuGet 3.5 RC 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="1cfe5-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="1cfe5-104">[NuGet 3.5 베타 2 릴리스 정보](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM 릴리스 정보](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="1cfe5-105">3.5 릴리스는 NuGet 클라이언트의 품질 및 성능을 개선 중점 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cfe5-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="1cfe5-106">에 대 한 지원과 같은 몇 가지 기능이 함께 있는 뿐만 [대체 (fallback) 폴더](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) 지원 `.nuspec` 등입니다.</span><span class="sxs-lookup"><span data-stu-id="1cfe5-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="1cfe5-107">문제 목록</span><span class="sxs-lookup"><span data-stu-id="1cfe5-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="1cfe5-108">버그 수정</span><span class="sxs-lookup"><span data-stu-id="1cfe5-108">Bug Fixes</span></span>

* <span data-ttu-id="1cfe5-109">패키지의 설치/복원 실패 "패키지에 여러 개 포함 된 `.nuspec` 파일입니다."</span><span class="sxs-lookup"><span data-stu-id="1cfe5-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="1cfe5-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="1cfe5-111">nuget pack 강제적으로 추가 됩니다 `.tt` 어떤-콘텐츠 폴더에 파일 [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="1cfe5-112">nuget 팩 csproj (사용 하 여 `project.json`) packOptions 및 JSON 파일의 소유자 없는 경우 충돌 [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="1cfe5-113">에 대 한 nuget 팩 `project.json` 요약, 작성자, 소유자 등-packOptions 태그를 무시 [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="1cfe5-114">출력의 종속성을 무시 하는 nuget 팩 `.nuspec` 에 대 한 `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="1cfe5-115">손상된 된 상태로-프로젝트 유지 rollback을 사용 하 여 여러 패키지를 업데이트 [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="1cfe5-116">Netstandard 프로젝트-에 대 한 ContentFiles에서 추가 되지 않습니다 [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="1cfe5-117">.NET을 대상으로 하는 라이브러리를 패키지할 수 없습니다 표준 제대로 [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="1cfe5-118">파일-> 새 프로젝트-Dev15 VS2015에서 클래스 라이브러리 (이식 가능) 프로젝트 실패-> [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="1cfe5-119">nuGet 오류-1.0.0-\* 문자열이 아닙니다. 유효한 버전- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="1cfe5-120">Find-package 실패를 표시 하지만 Install-package 작동- [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="1cfe5-121">오류 때-dev15에서 "Install-package jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="1cfe5-122">설치 된 VS 2015 업데이트 3 버전 3.5.0 오류 발생-NuGet을 사용 하는 VS에서 [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="1cfe5-123">패키지 관리자 UI: 패키지를 업데이트 한 후 새 버전이 표시 되지 않습니다- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="1cfe5-124">-ApiKey 삭제 명령줄에서 읽기/에서 전송 되지 않습니다 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="1cfe5-125">잘못 된 문자열: 패키지의 안정적인 릴리스 시험판 종속성에 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cfe5-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="1cfe5-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="1cfe5-127">PCL (net46 및 windows 10) 프로젝트 get NullRef 예외를 만드는 중입니다.</span><span class="sxs-lookup"><span data-stu-id="1cfe5-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="1cfe5-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="1cfe5-129">더 높은 버전 allowedVersions 제약 조건으로 제한 되 면 Nuget 업데이트 알림 메시지를 제공 해야 [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="1cfe5-130">오류-1 사용 하 여 자격 증명 플러그 인 종료 / 여러 소스를 사용 하 여 자격 증명 공급자를 사용 하는 경우 패키지 다운로드 중 오류 발생 [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="1cfe5-131">nuget 패키지 종속성 누락 Newtonsoft.Json-팩 [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="1cfe5-132">Linux/MacOS + Mono-ExecuteSynchronizedCore 버그 [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="1cfe5-133">VS repositoryPath에서 환경 변수를 지원 하지 않습니다 (nuget.exe 않습니다)- [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="1cfe5-134">액세스 가능성 문제를 해결 [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="1cfe5-135">하이픈으로 연결 된 프로필을 사용 하 여 이식 가능한 프레임 워크 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1cfe5-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="1cfe5-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="1cfe5-137">NuGet 패키지 관리자를 사용 해야 패키지 세부 정보에 적용 되지 않는 옵션 목록 명확히 `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="1cfe5-138">NuGet 3.3.0 업데이트 실패 '...는 추가 제약 조건에 정의 된 packages.config이이 작업을 방지 합니다.'</span><span class="sxs-lookup"><span data-stu-id="1cfe5-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="1cfe5-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="1cfe5-140">잘못 된 메시지-throw 존재 하지 않는 로컬 원본에서 패키지를 설치 [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="1cfe5-141">"사용 가능한 업그레이드" 필터 버전 제약 조건 위반 하는 업그레이드를 보여 줍니다. [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="1cfe5-142">성능 향상</span><span class="sxs-lookup"><span data-stu-id="1cfe5-142">Performance Improvements</span></span>

* <span data-ttu-id="1cfe5-143">성능: 개선 contentmodel은 대상 프레임 워크를 구문 분석- [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="1cfe5-144">성능: 읽기를 방지 `runtime.json` Rid 되지 않은 복원에 대 한 파일 [#3150](https://github.com/NuGet/Home/issues/3150)합니다.</span><span class="sxs-lookup"><span data-stu-id="1cfe5-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="1cfe5-145">CI 컴퓨터에서 ASP.NET 웹 응용 프로그램 3 초를 15 초 바탕으로 감소 하는 샘플을 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cfe5-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="1cfe5-146">성능: 패키지 관리자 콘솔 init.ps1 로드 시간 [#2956](https://github.com/NuGet/Home/issues/2956)합니다.</span><span class="sxs-lookup"><span data-stu-id="1cfe5-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="1cfe5-147">132s에서 10 사이의 경우도 PackageManagerConsole를 여는 데 시간이 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1cfe5-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="1cfe5-148">NuGet 업데이트-ReSharper 성능 문제 해결 [#3044](https://github.com/NuGet/Home/issues/3044): 샘플 프로젝트에서 패키지를 설치 하는 데 걸린 시간에서에서 감소 140s 68s 합니다.</span><span class="sxs-lookup"><span data-stu-id="1cfe5-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="1cfe5-149">DCR</span><span class="sxs-lookup"><span data-stu-id="1cfe5-149">DCRs</span></span>

* <span data-ttu-id="1cfe5-150">사용자를 기반으로 하는 dotnet tfm에서 업그레이드/설치 PCL 문제가 발생할 수 있습니다-알 수 있도록 필요한 NuGet [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="1cfe5-151">Tfm (포함)는 프로젝트에 대 한 잘못 된 설치/업그레이드 경고 = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="1cfe5-152">Netcoreapp11 및 netstandard17 지원-추가 [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="1cfe5-153">NuGet 경고 헤더 내용을 nuget.exe-콘솔에 인쇄 [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="1cfe5-154">AssemblyMetadata 특성 활용 `.nuspec` 대체-토큰 [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="1cfe5-155">잠금 파일에서 잠긴된 속성을 제거 [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="1cfe5-156">기호 패키지는 이전 설치에서 사용할 수 없습니다 또는 #2807 업데이트</span><span class="sxs-lookup"><span data-stu-id="1cfe5-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="1cfe5-157">기능</span><span class="sxs-lookup"><span data-stu-id="1cfe5-157">Features</span></span>

* <span data-ttu-id="1cfe5-158">-대체 패키지 폴더에 대 한 지원을 [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="1cfe5-159">디자인 및 구현-도구 패키지를 지원 하기 위해 패키지 형식의 개념 [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="1cfe5-160">전역 패키지 폴더 경로 이동 하려면 API [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="1cfe5-161">네이티브 패키지 업데이트 지원- [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="1cfe5-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
