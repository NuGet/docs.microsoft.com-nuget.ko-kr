---
title: NuGet 4.6 RTM 릴리스 정보
description: NuGet 4.6.0에 대한 릴리스 정보(알려진 문제, 버그 수정, 추가된 기능 및 DCR 포함)
author: anangaur
ms.author: anangaur
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: eacd29d4c9340a0f015fcdf6c5b9dd41bf781419
ms.sourcegitcommit: 74bf831e013470da8b0c1f43193df10bfb1f4fe6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2019
ms.locfileid: "58432558"
---
# <a name="nuget-46-release-notes"></a><span data-ttu-id="779e5-103">NuGet 4.6 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="779e5-103">NuGet 4.6 Release Notes</span></span>

<span data-ttu-id="779e5-104">[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes)는 [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe)과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="779e5-104">[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-460"></a><span data-ttu-id="779e5-105">요약: 4.6.0의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="779e5-105">Summary: What's New in 4.6.0</span></span>

* <span data-ttu-id="779e5-106">[패키지 서명](../create-packages/sign-a-package.md)에 대한 지원을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="779e5-106">We have added support for [signing packages](../create-packages/sign-a-package.md).</span></span>
* <span data-ttu-id="779e5-107">Visual Studio 2017 및 nuget.exe는 이제 [서명된 패키지](../reference/signed-packages-reference.md)의 패키지 설치, 복원 전에 패키지 무결성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="779e5-107">Visual Studio 2017 and nuget.exe now verifies package integrity before installing, restoring packages for [signed packages](../reference/signed-packages-reference.md).</span></span>
* <span data-ttu-id="779e5-108">연속 복원의 성능을 개선했습니다.</span><span class="sxs-lookup"><span data-stu-id="779e5-108">We have improved performance of successive restores.</span></span>

## <a name="summary-whats-new-in-463"></a><span data-ttu-id="779e5-109">요약: 4.6.3의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="779e5-109">Summary: What's New in 4.6.3</span></span>

* <span data-ttu-id="779e5-110">보안 수정: ~/.nuget 내에서 만든 파일에 대한 사용 권한이 열려 있습니다. [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="779e5-110">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-464"></a><span data-ttu-id="779e5-111">요약: 4.6.4의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="779e5-111">Summary: What's New in 4.6.4</span></span>

* <span data-ttu-id="779e5-112">보안 수정: NUPKG 내부에 있는 파일에는 NUPKG 디렉터리 위의 상대 경로가 포함될 수 있습니다. [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="779e5-112">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="779e5-113">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="779e5-113">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="779e5-114">.NET Framework 및 NuGet이 포함된 .NET Standard 2.0 관련 문제</span><span class="sxs-lookup"><span data-stu-id="779e5-114">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="779e5-115">.NET Standard 및 해당 도구는 .NET Framework 4.6.1을 대상으로 하는 프로젝트에서 .NET Standard 2.0 또는 이전 버전을 대상으로 하는 NuGet 패키지 및 프로젝트를 사용할 수 있도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="779e5-115">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="779e5-116">[이 문서](https://github.com/dotnet/standard/issues/481)에서는 해당 시나리오와 관련된 문제, 문제를 해결하기 위한 계획 및 현재의 도구 상태로 배포할 수 있는 해결 방법을 요약하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="779e5-116">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

## <a name="top-issues-fixed-in-this-release"></a><span data-ttu-id="779e5-117">이번 릴리스에서 해결된 주요 문제</span><span class="sxs-lookup"><span data-stu-id="779e5-117">Top issues fixed in this release</span></span>

<span data-ttu-id="779e5-118">**성능 개선**</span><span class="sxs-lookup"><span data-stu-id="779e5-118">**Performance fixes**</span></span>

* <span data-ttu-id="779e5-119">변경 내용이 없는 경우 자산 파일을 기록하지 않음 - [#6491](https://github.com/NuGet/Home/issues/6491)</span><span class="sxs-lookup"><span data-stu-id="779e5-119">Don't write asset files when there is no change - [#6491](https://github.com/NuGet/Home/issues/6491)</span></span>
* <span data-ttu-id="779e5-120">자식 프로젝트의 TFM이 부모 프로젝트와 일치하지 않는 경우 복원 시 추가 MSBuild 평가가 수행됨 - [#6311](https://github.com/NuGet/Home/issues/6311)</span><span class="sxs-lookup"><span data-stu-id="779e5-120">Restore causes extra MSBuild evaluations when child projects' TFM do not match with the parent project's - [#6311](https://github.com/NuGet/Home/issues/6311)</span></span>
* <span data-ttu-id="779e5-121">종속성 그래프 사양 생성을 최적화하여 NoOp 복원 성능 개선 - [#6252](https://github.com/NuGet/Home/issues/6252)</span><span class="sxs-lookup"><span data-stu-id="779e5-121">Improve NoOp restore perf by optimizing dependency graph spec creation - [#6252](https://github.com/NuGet/Home/issues/6252)</span></span>

<span data-ttu-id="779e5-122">**버그**</span><span class="sxs-lookup"><span data-stu-id="779e5-122">**Bugs**</span></span>

* <span data-ttu-id="779e5-123">로컬 폴더로 푸시하면 nupkg가 잠김 - [#6325](https://github.com/NuGet/Home/issues/6325)</span><span class="sxs-lookup"><span data-stu-id="779e5-123">Push to local folder leaves nupkg locked - [#6325](https://github.com/NuGet/Home/issues/6325)</span></span>
* <span data-ttu-id="779e5-124">NuGet 플러그인 구현: 여러 문제 - [#6149](https://github.com/NuGet/Home/issues/6149)</span><span class="sxs-lookup"><span data-stu-id="779e5-124">NuGet Plugin implementation:  multiple issues - [#6149](https://github.com/NuGet/Home/issues/6149)</span></span>
* <span data-ttu-id="779e5-125">UIHang - VSSolutionManager에서 MEF 초기화의 쿼리 서비스 호출 제거 - [#6110](https://github.com/NuGet/Home/issues/6110)</span><span class="sxs-lookup"><span data-stu-id="779e5-125">UIHang - Remove query service call from MEF initialization in VSSolutionManager - [#6110](https://github.com/NuGet/Home/issues/6110)</span></span>
* <span data-ttu-id="779e5-126">취소된 패키지 다운로드 작업의 오류 보고 예외 - [#6096](https://github.com/NuGet/Home/issues/6096)</span><span class="sxs-lookup"><span data-stu-id="779e5-126">Error reporting exception for cancelled package download task - [#6096](https://github.com/NuGet/Home/issues/6096)</span></span>
* <span data-ttu-id="779e5-127">NuGet.exe가 어셈블리 이름의 '+'를 '%2B'로 바꿈 - [#5956](https://github.com/NuGet/Home/issues/5956)</span><span class="sxs-lookup"><span data-stu-id="779e5-127">NuGet.exe replaces '+' with '%2B' in assembly name - [#5956](https://github.com/NuGet/Home/issues/5956)</span></span>
* <span data-ttu-id="779e5-128">Fn+F1을 눌러도 PM UI 및 콘솔의 올바른 도움말 페이지로 이동되지 않음 - [#5912](https://github.com/NuGet/Home/issues/5912)</span><span class="sxs-lookup"><span data-stu-id="779e5-128">Fn+F1 does not take to the right help page for PM UI and Console - [#5912](https://github.com/NuGet/Home/issues/5912)</span></span>
* <span data-ttu-id="779e5-129">VS NuGet가 특정 상황에서 프로젝트 파일에 절대 경로를 기록함 - [#5888](https://github.com/NuGet/Home/issues/5888)</span><span class="sxs-lookup"><span data-stu-id="779e5-129">VS NuGet writes absolute paths into project files under specific circumstances - [#5888](https://github.com/NuGet/Home/issues/5888)</span></span>
* <span data-ttu-id="779e5-130">4.3 재발 해결 - 콘텐츠 파일에서 자리 표시자 $product$ 및 $AssemblyGuid$가 변환을 통해 대체되지 않음 - [#5880](https://github.com/NuGet/Home/issues/5880)</span><span class="sxs-lookup"><span data-stu-id="779e5-130">Fix 4.3 regression - Placeholders $product$ and $AssemblyGuid$ not replaced in contentfile through transformation - [#5880](https://github.com/NuGet/Home/issues/5880)</span></span>
* <span data-ttu-id="779e5-131">여러 소스를 사용하는 dotnet restore가 충돌함 - [#5817](https://github.com/NuGet/Home/issues/5817)</span><span class="sxs-lookup"><span data-stu-id="779e5-131">dotnet restore with multiple sources crashes - [#5817](https://github.com/NuGet/Home/issues/5817)</span></span>
* <span data-ttu-id="779e5-132">팩이 프로젝트 버전을 다시 계산해야 git 버전 관리가 가능함 - [#4790](https://github.com/NuGet/Home/issues/4790)</span><span class="sxs-lookup"><span data-stu-id="779e5-132">Pack should re-evaluate project versions to allow git versioning - [#4790](https://github.com/NuGet/Home/issues/4790)</span></span>
* <span data-ttu-id="779e5-133">호환되지 않는 패키지를 설치할 때 이해하기 어려운 오류 개선 - [#4555](https://github.com/NuGet/Home/issues/4555)</span><span class="sxs-lookup"><span data-stu-id="779e5-133">Improve hard to understand errors when you install an incompatible package - [#4555](https://github.com/NuGet/Home/issues/4555)</span></span>
* <span data-ttu-id="779e5-134">TemplateWizard에서 패키지를 PackageReference로 설치하는 옵션이 필요함 - [#4549](https://github.com/NuGet/Home/issues/4549)</span><span class="sxs-lookup"><span data-stu-id="779e5-134">TemplateWizard needs option to install packages as PackageReferences - [#4549](https://github.com/NuGet/Home/issues/4549)</span></span>
* <span data-ttu-id="779e5-135">개발자 명령 프롬프트 외부에서 MSBuild.exe를 실행할 때 패키지에서 제공한 props 파일이 무시됨 - [#4530](https://github.com/NuGet/Home/issues/4530)</span><span class="sxs-lookup"><span data-stu-id="779e5-135">Package-delivered props files ignored when MSBuild.exe is run from outside a Developer Command Prompt - [#4530](https://github.com/NuGet/Home/issues/4530)</span></span>
* <span data-ttu-id="779e5-136">프로젝트에 적용할 수 없는 .NET Standard 라이브러리를 참조할 때 나쁨 오류 메시지 해결 - [#4423](https://github.com/NuGet/Home/issues/4423)</span><span class="sxs-lookup"><span data-stu-id="779e5-136">Fix poor error message when referencing .NET Standard Library that is not applicable to project - [#4423](https://github.com/NuGet/Home/issues/4423)</span></span>
* <span data-ttu-id="779e5-137">약간의 지침이 포함된 이식 가능한 프로필을 대상으로 하는 패키지의 경우 dotnet add package가 실패함 - [#4349](https://github.com/NuGet/Home/issues/4349)</span><span class="sxs-lookup"><span data-stu-id="779e5-137">dotnet add package fails for package targeting portable profile with little guidance - [#4349](https://github.com/NuGet/Home/issues/4349)</span></span>
* <span data-ttu-id="779e5-138">dotnet pack - ProjectReference에 버전 접미사가 없음 - [#4337](https://github.com/NuGet/Home/issues/4337)</span><span class="sxs-lookup"><span data-stu-id="779e5-138">dotnet pack - version suffix missing from ProjectReference - [#4337](https://github.com/NuGet/Home/issues/4337)</span></span>
* <span data-ttu-id="779e5-139">.NET Core 템플릿 관련 빌드 오류 및 VS 충돌 - [#3973](https://github.com/NuGet/Home/issues/3973)</span><span class="sxs-lookup"><span data-stu-id="779e5-139">Build errors and VS crash with .NET Core template - [#3973](https://github.com/NuGet/Home/issues/3973)</span></span>
* <span data-ttu-id="779e5-140">소스 https:\*의 서비스 인덱스를 로드할 수 없음 - [#3681](https://github.com/NuGet/Home/issues/3681)</span><span class="sxs-lookup"><span data-stu-id="779e5-140">Unable to load the service index for source https:\* - [#3681](https://github.com/NuGet/Home/issues/3681)</span></span>
* <span data-ttu-id="779e5-141">nuget.exe 목록 -allversion이 작동하지 않음 - [#3441](https://github.com/NuGet/Home/issues/3441)</span><span class="sxs-lookup"><span data-stu-id="779e5-141">nuget.exe list -allversions doesn't work - [#3441](https://github.com/NuGet/Home/issues/3441)</span></span>
* <span data-ttu-id="779e5-142">잘못된 종속성 해결 오류 메시지 - [#2984](https://github.com/NuGet/Home/issues/2984)</span><span class="sxs-lookup"><span data-stu-id="779e5-142">Misleading dependency resolution error message - [#2984](https://github.com/NuGet/Home/issues/2984)</span></span>
* <span data-ttu-id="779e5-143">nuget.exe restore가 .msbuildproj에 대한 .props 및 .targets 파일을 생성하지 않음(v3.3.0-3.4.4 업그레이드에서 재발) - [#2921](https://github.com/NuGet/Home/issues/2921)</span><span class="sxs-lookup"><span data-stu-id="779e5-143">nuget.exe restore doesn't produce .props and .targets files for .msbuildproj (regression in v3.3.0-3.4.4 upgrade) - [#2921](https://github.com/NuGet/Home/issues/2921)</span></span>
* <span data-ttu-id="779e5-144">XAML 파일을 연 상태에서 NuGet 패키지를 업데이트할 때 UI 지연 - [#2878](https://github.com/NuGet/Home/issues/2878)</span><span class="sxs-lookup"><span data-stu-id="779e5-144">UI delay when updating a NuGet package with XAML file open - [#2878](https://github.com/NuGet/Home/issues/2878)</span></span>
* <span data-ttu-id="779e5-145">경로에 잘못된 문자가 있을 경우 IIS의 WebSite 프로젝트가 실패함 - [#2798](https://github.com/NuGet/Home/issues/2798)</span><span class="sxs-lookup"><span data-stu-id="779e5-145">WebSite project from IIS fails with illegal characters in path - [#2798](https://github.com/NuGet/Home/issues/2798)</span></span>
* <span data-ttu-id="779e5-146">CentOS에서 Nuget add가 중지됨 - [#2708](https://github.com/NuGet/Home/issues/2708)</span><span class="sxs-lookup"><span data-stu-id="779e5-146">Nuget add hangs on CentOS - [#2708](https://github.com/NuGet/Home/issues/2708)</span></span>
* <span data-ttu-id="779e5-147">json.net의 경우 packagesavemode -nupkg를 사용한 복원이 실패함 - [#2706](https://github.com/NuGet/Home/issues/2706)</span><span class="sxs-lookup"><span data-stu-id="779e5-147">Restore with packagesavemode -nupkg fails for json.net - [#2706](https://github.com/NuGet/Home/issues/2706)</span></span>
* <span data-ttu-id="779e5-148">복원 명령의 vs 출력 창에서 패키지 관리자 필터를 사용할 수 없음 - [#2704](https://github.com/NuGet/Home/issues/2704)</span><span class="sxs-lookup"><span data-stu-id="779e5-148">Package Manager filter not available in vs output window for restore command - [#2704](https://github.com/NuGet/Home/issues/2704)</span></span>

[<span data-ttu-id="779e5-149">이번 릴리스에서 수정된 모든 문제 목록</span><span class="sxs-lookup"><span data-stu-id="779e5-149">List of all issues fixed in this release</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
