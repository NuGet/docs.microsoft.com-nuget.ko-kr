---
title: NuGet 4.0 RC 릴리스 정보
description: NuGet 4.0 RC에 대한 릴리스 정보(알려진 문제, 버그 수정, 추가된 기능 및 DCR 포함)
author: JonDouglas
ms.author: jodou
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 44f15e2fc33cca8a3d88af17bf76f1dcc16ca860
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780189"
---
# <a name="nuget-40-rc-release-notes"></a><span data-ttu-id="ba1ab-103">NuGet 4.0 RC 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="ba1ab-103">NuGet 4.0 RC Release Notes</span></span>

[<span data-ttu-id="ba1ab-104">NuGet 3.5 RTM 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="ba1ab-104">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="ba1ab-105">[Visual Studio 2017용 NuGet 4.0 RC](http://blog.nuget.org/20161121/introducing-nuget4.0)는 .NET Core 시나리오에 대한 지원 추가, 주요 고객 의견 처리 및 다양한 시나리오의 성능 향상에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ab-105">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="ba1ab-106">이 릴리스에는 PackageReference 지원, MSBuild 대상 NuGet 명령, 백그라운드 패키지 복원 등과 같이 향상된 몇 가지 기능이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ab-106">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="ba1ab-107">버그 수정</span><span class="sxs-lookup"><span data-stu-id="ba1ab-107">Bug Fixes</span></span>

- <span data-ttu-id="ba1ab-108">`dotnet pack --version-suffix foo` 동작 변경 - [#3838](https://github.com/NuGet/Home/issues/3838)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-108">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

- <span data-ttu-id="ba1ab-109">VS "15" 컴퓨터에서만 nuget.exe restore가 실패합니다. - [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-109">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

- <span data-ttu-id="ba1ab-110">.NETCore 파일 - 새 프로젝트를 복원하는 동안 빌드를 차단해야 합니다. - [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-110">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

- <span data-ttu-id="ba1ab-111">VS2015에서 VS "15"로 마이그레이션된 ASP.NET Core 웹앱을 복원할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ab-111">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="ba1ab-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

- <span data-ttu-id="ba1ab-113">[테스트 실패] PM UI에서 'jQuery 유효성 검사' 패키지를 제거할 수 없습니다. - [#3755](https://github.com/NuGet/Home/issues/3755)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-113">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

- <span data-ttu-id="ba1ab-114">패키지가 UWP `project.json`에 설치되면 부모 프로젝트도 복원해야 합니다. - [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-114">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

- <span data-ttu-id="ba1ab-115">NuGet 대상을 수정하여 패키지 원본을 보통 대신 높은 수준의 세부 정보 표시로 기록합니다. - [#3719](https://github.com/NuGet/Home/issues/3719)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-115">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

- <span data-ttu-id="ba1ab-116">dotnet</span><span class="sxs-lookup"><span data-stu-id="ba1ab-116">dotnet</span></span>
  - <span data-ttu-id="ba1ab-117">dotnetcore pack3에는 기본적으로 XML 문서가 포함되어야 합니다. - [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-117">dotnetcore pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

- <span data-ttu-id="ba1ab-118">패키지가 없는 원본이 처음이고 모든 원본이 선택되면 UI에서 일괄 업데이트가 실패합니다. - [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

- <span data-ttu-id="ba1ab-119">Nuget pack 명령에 모든 파일이 포함되지 않습니다. - [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

- <span data-ttu-id="ba1ab-120">OOM 문제 - [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

- <span data-ttu-id="ba1ab-121">자산 파일의 ProjectFileDependencyGroups 섹션에는 프로젝트의 라이브러리 이름을 사용해야 합니다. - [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

- <span data-ttu-id="ba1ab-122">"dotnet restore" 및 디렉터리 재귀 - [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

- <span data-ttu-id="ba1ab-123">Restore3 실패는 오류 대신 경고로 기록됩니다. - [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

- <span data-ttu-id="ba1ab-124">TFS 문제: 작업 영역에서 [file] 항목을 찾을 수 없거나 사용자에게 해당 항목에 액세스할 수 있는 권한이 없습니다. - [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

- <span data-ttu-id="ba1ab-125">VS 빠른 시작 검색 상자에 "nuget <packagename>"을 입력하면 "nuget " 접두사가 유지됩니다. - [#2719](https://github.com/NuGet/Home/issues/2719)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

- <span data-ttu-id="ba1ab-126">System.Xml.XmlException: Core Properties 파트에 인식할 수 없는 루트 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ab-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="ba1ab-127">줄 2, 위치 2</span><span class="sxs-lookup"><span data-stu-id="ba1ab-127">Line 2, position 2.</span></span><span data-ttu-id="ba1ab-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

- <span data-ttu-id="ba1ab-129">텍스트 필드에 이스케이프된 &lt; 또는 &gt;가 있는 `.nuspec`은 더 이상 빌드되지 않습니다. - [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

- <span data-ttu-id="ba1ab-130">nuget.exe delete는 자격 증명을 묻지 않습니다(비대화형 모드입니다) - [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

- <span data-ttu-id="ba1ab-131">nuget.exe delete는 의미가 없더라도 로컬 원본에 대한 API 키에 대해 경고합니다. - [#2625](https://github.com/NuGet/Home/issues/2625)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

- <span data-ttu-id="ba1ab-132">EF -pre 패키지를 설치할 때 오류 경험이 부족합니다. - [#2566](https://github.com/NuGet/Home/issues/2566)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

- <span data-ttu-id="ba1ab-133">패키지 관리자에서 선택 항목을 변경한 후 시도하면 Visual Studio에서 작동이 중단됩니다. - [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

- <span data-ttu-id="ba1ab-134">dotnet</span><span class="sxs-lookup"><span data-stu-id="ba1ab-134">dotnet</span></span>
  - <span data-ttu-id="ba1ab-135">유동적인 버전이 사용되는 경우 dotnetcore restore에서 단순 목록 로컬 리포지토리에 대해 대/소문자를 구분하는 ID 조회를 수행합니다. - [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-135">dotnetcore restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

- <span data-ttu-id="ba1ab-136">V2 피드에 대한 nuget.exe delete가 중단됩니다. - [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-136">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

- <span data-ttu-id="ba1ab-137">nuget.exe push 시간 제한에 더 나은 오류 메시지가 필요합니다. - [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-137">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

- <span data-ttu-id="ba1ab-138">적절한 가져오기가 없는 도구 복원이 자동으로 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ab-138">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="ba1ab-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

- <span data-ttu-id="ba1ab-140">nuget.org에서 설치하는 경우에도 개인 피드가 있을 때 NuGet에서 자격 증명을 입력하라는 메시지가 표시됩니다. - [#2346](https://github.com/NuGet/Home/issues/2346)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-140">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

- <span data-ttu-id="ba1ab-141">ApplicationInsights 2.0 패키지가 나열되었지만 아직 존재하지 않습니다. - [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-141">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

- <span data-ttu-id="ba1ab-142">VS "15" 미리 보기 5 분기의 UIDelay - [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-142">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

- <span data-ttu-id="ba1ab-143">UWP 빌드 시 복원에 대한 첫 번째 OnBuild 이벤트가 누락되어 있습니다. - [#3489](https://github.com/NuGet/Home/issues/3489)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-143">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

- <span data-ttu-id="ba1ab-144">PowerShell5에서 EntityFramework 설치가 중단됩니까?</span><span class="sxs-lookup"><span data-stu-id="ba1ab-144">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="ba1ab-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

- <span data-ttu-id="ba1ab-146">자세한 로깅에 원본을 추가합니다(3.5에 대한 고려 사항) - [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-146">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

- <span data-ttu-id="ba1ab-147">NoCache 매개 변수가 NuGet 클라이언트 버전 3.4 이상에서 적용되지 않습니다. - [#3074](https://github.com/NuGet/Home/issues/3074)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-147">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

- <span data-ttu-id="ba1ab-148">자격 증명 공급자가 VS에서 로드하지 못하는 경우 NuGet을 중단하면 안됩니다. - [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-148">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>

## <a name="features"></a><span data-ttu-id="ba1ab-149">기능</span><span class="sxs-lookup"><span data-stu-id="ba1ab-149">Features</span></span>

- <span data-ttu-id="ba1ab-150">x86을 실행하도록 CI를 설정합니다. - [#3868](https://github.com/NuGet/Home/issues/3868)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-150">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

- <span data-ttu-id="ba1ab-151">자동 복구 3/3: UI를 차단하지 않습니다. - [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-151">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

- <span data-ttu-id="ba1ab-152">자동 복원 2/3: 지정에 대한 백그라운드 복원을 수행합니다. - [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-152">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

- <span data-ttu-id="ba1ab-153">빌드 동작과 일치하도록 프로젝트 참조를 복원합니다(recurse). - [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-153">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

- <span data-ttu-id="ba1ab-154">VS "15"에서 DPL - minbar를 지원합니다. - [#3614](https://github.com/NuGet/Home/issues/3614)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-154">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

- <span data-ttu-id="ba1ab-155">설정 파일을 Program Files 폴더로 이동합니다. - [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-155">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

- <span data-ttu-id="ba1ab-156">생성된 props 및 targets 복원에는 대상 간 참가 지원이 필요합니다. - [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-156">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

- <span data-ttu-id="ba1ab-157">PackageTargetFallback에 대해 NuGet 복원(종종 imports라고 함)을 지원합니다. - [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-157">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

- <span data-ttu-id="ba1ab-158">ToolsRef 구현 - [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-158">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

- <span data-ttu-id="ba1ab-159">RID에 대한 restore3 - [#3465](https://github.com/NuGet/Home/issues/3465)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-159">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

- <span data-ttu-id="ba1ab-160">PackageRefs 추가/제거/업데이트를 지원하는 NuGet UI - [#3457](https://github.com/NuGet/Home/issues/3457)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-160">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

- <span data-ttu-id="ba1ab-161">자동 복원 1/3: 프로젝트 복원 캐싱 정보를 통해 지정 API를 구현합니다. - [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-161">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

- <span data-ttu-id="ba1ab-162">[0] NuGet restore 작업 및 대상 - [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-162">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

- <span data-ttu-id="ba1ab-163">[1] MSBuild에서 솔루션 수준 복원 사용 - [#2993](https://github.com/NuGet/Home/issues/2993)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-163">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

- <span data-ttu-id="ba1ab-164">Visual Studio에서 자격 증명 공급자 공용 확장성 지원 - [#2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-164">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

- <span data-ttu-id="ba1ab-165">재귀적 nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-165">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

- <span data-ttu-id="ba1ab-166">dev15에서 Microsoft.TeamFoundation.Client를 로드할 수 없습니다. VS "15" 미리 보기에서 Microsoft.TeamFoundation.Client 버전을 15.0으로 업데이트해야 합니다. - [#2392](https://github.com/NuGet/Home/issues/2392)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-166">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

- <span data-ttu-id="ba1ab-167">VS "15" 미리 보기에서 C++ UWP 프로젝트에 C++ 패키지를 설치할 수 없습니다. - [#2369](https://github.com/NuGet/Home/issues/2369)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-167">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

- <span data-ttu-id="ba1ab-168">Nupkg에서 \buildCrossTargeting\ 폴더를 지원하고 "대상으로 교차 지정된(crosstargeting)" MSBuild 범위에 대한 `.targets` / `.props`를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ab-168">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="ba1ab-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

- <span data-ttu-id="ba1ab-170">ToolsReference 디자인 - [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

- <span data-ttu-id="ba1ab-171">`.csproj`에서 PackageReferences를 통한 복원을 지원하도록 NuGet UI를 수정합니다. - [#3455](https://github.com/NuGet/Home/issues/3455)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-171">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

- <span data-ttu-id="ba1ab-172">VS 패키지 관리자 설정에 캐시 지우기 단추를 추가합니다. - [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-172">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="ba1ab-173">DCR</span><span class="sxs-lookup"><span data-stu-id="ba1ab-173">DCRs</span></span>

- <span data-ttu-id="ba1ab-174">자동 복원이 수행되는 동안 솔루션 복원이 차단되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ab-174">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="ba1ab-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

- <span data-ttu-id="ba1ab-176">NuGet 패키지 관리자 UI에서 설치한 NetCore는 패키지에서 지원하는 UI 대신 모든 TFM에 설치됩니다. - [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-176">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

- <span data-ttu-id="ba1ab-177">복원 지정자 API도 DotNetCliToolsReferences를 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ab-177">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="ba1ab-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

- <span data-ttu-id="ba1ab-179">VS "15" vsix를 SystemComponent로 표시합니다. - [#3700](https://github.com/NuGet/Home/issues/3700)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-179">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

- <span data-ttu-id="ba1ab-180">참조하는 MS.VS.Services.Client에서 MS.VS.Services.Client.Interactive로 마이그레이션합니다. - [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-180">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

- <span data-ttu-id="ba1ab-181">$(RestoreLegacyPackagesDirectory)는 복원을 통해 프로젝트 수준에서 적용되어야 합니다. - [#3618](https://github.com/NuGet/Home/issues/3618)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-181">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

- <span data-ttu-id="ba1ab-182">단일 TargetFramework를 사용하여 프로젝트를 복원하는 경우 props 조건이 되어서는 안됩니다. - [#3588](https://github.com/NuGet/Home/issues/3588)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-182">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

- <span data-ttu-id="ba1ab-183">dotnet</span><span class="sxs-lookup"><span data-stu-id="ba1ab-183">dotnet</span></span>
  - <span data-ttu-id="ba1ab-184">dotnetcore restore3 foo.csproj는 projectref 종속성을 따르고 이를 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ab-184">dotnetcore restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="ba1ab-185">빌드하는 경우도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="ba1ab-185">Like build.</span></span><span data-ttu-id="ba1ab-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

- <span data-ttu-id="ba1ab-187">"type": "platform" 종속성이 잠금 파일에서 "type":"package"로 표시됩니다. - [#2695](https://github.com/NuGet/Home/issues/2695)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-187">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

- <span data-ttu-id="ba1ab-188">nuget.exe 자세한 정보 표시 모드에 다운로드 URL이 표시되어야 합니다. - [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-188">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

- <span data-ttu-id="ba1ab-189">NuGet xplat을 Microsoft.NetCore.App 및 netcoreapp1.0으로 이동합니다. - [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-189">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

- <span data-ttu-id="ba1ab-190">push - 명령줄에서 푸시할 때 기호 서버를 재정의할 수 있어야 합니다. - [#2348](https://github.com/NuGet/Home/issues/2348)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-190">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

- <span data-ttu-id="ba1ab-191">전역 패키지 경로를 찾는 코드를 통합합니다. - [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-191">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

- <span data-ttu-id="ba1ab-192">suppressParent보다 더 나은 이름이 필요합니다. - [#2196](https://github.com/NuGet/Home/issues/2196)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-192">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

- <span data-ttu-id="ba1ab-193">MSBuild 프로젝트에 사용할 `project.json` 종속성 이름을 결정합니다. - [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-193">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

- <span data-ttu-id="ba1ab-194">NuGet.Core에 SemVer 2.0.0 지원을 추가합니다. - [#3383](https://github.com/NuGet/Home/issues/3383)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-194">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

- <span data-ttu-id="ba1ab-195">`.targets`가 있는 NuPkg 전이적 종속성을 MSBuild에서 사용할 수 있도록 허용합니다. - [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-195">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

- <span data-ttu-id="ba1ab-196">명령줄의 NuGet restore는 VS보다 훨씬 느립니다. - [#3330](https://github.com/NuGet/Home/issues/3330)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-196">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

- <span data-ttu-id="ba1ab-197">패키지 ID 및 버전 비교에서 대/소문자를 구분하지 않습니다. - [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-197">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

- <span data-ttu-id="ba1ab-198">NoCache 옵션이 `packages.config` 기반 복원/설치(GlobalPackagesFolder)에서 작동하지 않습니다. - [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-198">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

- <span data-ttu-id="ba1ab-199">FindPackageByIdResource 리소스에는 기본 캐시 컨텍스트와 로거가 필요합니다. - [#1357](https://github.com/NuGet/Home/issues/1357)</span><span class="sxs-lookup"><span data-stu-id="ba1ab-199">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
