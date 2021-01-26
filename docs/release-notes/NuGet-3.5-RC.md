---
title: 3.5 RC 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 포함 하는 NuGet 3.5 RC에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780205"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="9650d-103">NuGet 3.5 RC 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="9650d-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="9650d-104">[NuGet 3.5-Beta2 릴리스 정보](../release-notes/nuget-3.5-Beta2.md)  |  [NuGet 3.5-RTM 릴리스 정보](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="9650d-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="9650d-105">3.5 릴리스는 NuGet 클라이언트의 품질 및 성능을 개선 하는 데 중점을 두었습니다.</span><span class="sxs-lookup"><span data-stu-id="9650d-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="9650d-106">또한 [대체 폴더](https://github.com/NuGet/Home/issues/2899)지원, [PackageType](https://github.com/NuGet/Home/issues/2476) 지원 등의 몇 가지 기능을 제공 `.nuspec` 합니다.</span><span class="sxs-lookup"><span data-stu-id="9650d-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="9650d-107">문제 목록</span><span class="sxs-lookup"><span data-stu-id="9650d-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="9650d-108">버그 픽스</span><span class="sxs-lookup"><span data-stu-id="9650d-108">Bug Fixes</span></span>

* <span data-ttu-id="9650d-109">"패키지에 여러 파일이 포함 되어 있습니다." 라는 오류와 함께 패키지의 설치/복원이 실패 `.nuspec` 합니다.</span><span class="sxs-lookup"><span data-stu-id="9650d-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="9650d-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="9650d-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="9650d-111">nuget 팩 `.tt` 은 [#3203](https://github.com/NuGet/Home/issues/3203) 에 관계 없이 파일을 콘텐츠 폴더에 강제로 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="9650d-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="9650d-112">JSON 파일에 pack 옵션과 소유자가 없는 경우 nuget pack .csproj (with `project.json` )이 충돌 합니다. [#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="9650d-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="9650d-113">용 nuget 팩은 `project.json` 요약, 저자, 소유자 등의 패키지 옵션 태그를 무시 [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="9650d-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="9650d-114">nuget 팩은 #3145 출력에서 종속성을 무시 `.nuspec` 합니다. `project.json`  -  [](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="9650d-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="9650d-115">Rollback을 사용 하 여 여러 패키지를 업데이트 하면 프로젝트가 중단 된 상태로 남게 됩니다 [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="9650d-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="9650d-116">모든 아래 ContentFiles는 netstandard.library 프로젝트에 추가 되지 않습니다. [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="9650d-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="9650d-117">.Net Standard를 올바르게 대상으로 하는 라이브러리를 패키지할 수 없습니다. [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="9650d-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="9650d-118">VS2015 및 Dev15에서 파일 > 새 프로젝트-> 클래스 라이브러리 (이식 가능) 프로젝트가 실패 [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="9650d-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="9650d-119">NuGet 오류-1.0.0-\*은 올바른 버전 문자열이 아닙니다. [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="9650d-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="9650d-120">Find-Package 표시 되지 않지만 Install-Package 작동 [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="9650d-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="9650d-121">Dev15- [#3061](https://github.com/NuGet/Home/issues/3061) 에서 "Install-Package jquery. validation" 오류가 발생 하는 경우 오류</span><span class="sxs-lookup"><span data-stu-id="9650d-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="9650d-122">NuGet 버전을 사용 하는 VS 2015 업데이트 3이 설치 된 경우 3.5.0 오류 발생- [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="9650d-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="9650d-123">패키지 관리자 UI: 패키지를 업데이트 한 후 새 버전을 표시 하지 않습니다.- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="9650d-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="9650d-124">-3.5.0에서 명령줄의 ApiKey를 읽고 보내지 않습니다.-beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="9650d-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="9650d-125">잘못 된 문자열: 안정적인 패키지 릴리스가 시험판 종속성에 포함 되어서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9650d-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="9650d-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="9650d-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="9650d-127">PCL (고 net46 및 windows 10) 프로젝트 만들기 NullRef 예외</span><span class="sxs-lookup"><span data-stu-id="9650d-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="9650d-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="9650d-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="9650d-129">상위 버전이 allowedVersions 제약 조건에 의해 제한 되는 경우 Nuget 업데이트는 정보 메시지를 제공 해야 [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="9650d-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="9650d-130">여러 소스가 포함 된 자격 증명 공급자를 사용 하는 경우 자격 증명 플러그 인이 종료 되었습니다. 오류 1/패키지 다운로드 오류- [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="9650d-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="9650d-131">nuget 팩-패키지 종속성에 Newtonsoft.Js누락- [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="9650d-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="9650d-132">Linux/MacOS + Mono에서 ExecuteSynchronizedCore의 버그- [#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="9650d-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="9650d-133">VS는 repositoryPath (nuget.exe)에서 환경 변수를 지원 하지 않습니다 [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="9650d-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="9650d-134">내게 필요한 옵션 문제 해결- [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="9650d-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="9650d-135">하이픈이 있는 이식 가능한 프레임 워크는 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9650d-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="9650d-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="9650d-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="9650d-137">NuGet 패키지 관리자는 패키지 세부 정보의 옵션 목록이에 적용 되지 않는다는 것을 명확 하 게 지정 해야 `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="9650d-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="9650d-138">' 추가 제약 조건을 사용 하 여 NuGet 3.3.0 업데이트가 실패 합니다. packages.config에 정의 되어 있으므로이 작업을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9650d-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="9650d-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="9650d-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="9650d-140">존재 하지 않는 로컬 원본에서 패키지를 설치 하면 가짜 메시지가 throw 됩니다. [#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="9650d-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="9650d-141">"Upgrade v)" 필터는 버전 제약 조건을 위반 하는 업그레이드를 표시 합니다.- [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="9650d-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="9650d-142">성능 향상</span><span class="sxs-lookup"><span data-stu-id="9650d-142">Performance Improvements</span></span>

* <span data-ttu-id="9650d-143">성능: ContentModel 대상 프레임 워크 구문 분석 개선- [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="9650d-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="9650d-144">성능: `runtime.json` rid [#3150](https://github.com/NuGet/Home/issues/3150)없는 복원에 대 한 파일을 읽지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9650d-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="9650d-145">CI 컴퓨터에서 샘플 ASP.NET 웹 응용 프로그램 복원이 15 초에서 3 초까지 줄었습니다.</span><span class="sxs-lookup"><span data-stu-id="9650d-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="9650d-146">성능: 패키지 관리자 콘솔 init.ps1 로드 시간이 [#2956](https://github.com/NuGet/Home/issues/2956).</span><span class="sxs-lookup"><span data-stu-id="9650d-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="9650d-147">132s에서 10 초까지 PackageManagerConsole을 여는 데 걸리는 시간이 개선 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9650d-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="9650d-148">NuGet 업데이트 ReSharper의 성능 문제 해결- [#3044](https://github.com/NuGet/Home/issues/3044): 샘플 프로젝트에서 140s에서 68s로 축소 된 패키지를 설치 하는 데 걸린 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="9650d-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="9650d-149">DCR</span><span class="sxs-lookup"><span data-stu-id="9650d-149">DCRs</span></span>

* <span data-ttu-id="9650d-150">NuGet은 dotnet tfm 기반 PCL에서 업그레이드/설치 하는 데 [#3138](https://github.com/NuGet/Home/issues/3138) 문제가 발생할 수 있음을 사용자에 게 알릴 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9650d-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="9650d-151">Project w/tfm = "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137) 에 대 한 잘못 된 설치/업그레이드 경고</span><span class="sxs-lookup"><span data-stu-id="9650d-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="9650d-152">Netcoreapp11 및 netstandard17 지원 추가- [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="9650d-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="9650d-153">nuget.exe의 콘솔에 NuGet-Warning 머리글 콘텐츠 인쇄- [#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="9650d-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="9650d-154">토큰 교체에 AssemblyMetadata 특성 활용 `.nuspec` - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="9650d-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="9650d-155">잠금 파일에서 잠긴 속성을 제거 합니다.- [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="9650d-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="9650d-156">기호 패키지는 설치 또는 업데이트에 사용 하면 안 됩니다 #2807</span><span class="sxs-lookup"><span data-stu-id="9650d-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="9650d-157">기능</span><span class="sxs-lookup"><span data-stu-id="9650d-157">Features</span></span>

* <span data-ttu-id="9650d-158">대체 패키지 폴더에 대 한 지원- [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="9650d-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="9650d-159">도구 패키지를 지원 하기 위한 패키지 형식의 개념 디자인 및 구현- [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="9650d-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="9650d-160">전역 패키지 폴더에 대 한 경로를 가져오는 API- [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="9650d-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="9650d-161">네이티브 패키지 업데이트 지원- [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="9650d-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
