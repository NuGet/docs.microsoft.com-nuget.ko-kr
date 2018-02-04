---
title: "3.5 베타 2 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 3.5 베타 2에 대 한 릴리스 정보입니다."
keywords: "NuGet 3.5 베타 2, 릴리스 정보 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4073b669c19f9e96ebd35ba269919b5f42313e7c
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="f5273-104">NuGet 3.5 베타 2 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="f5273-104">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="f5273-105">[NuGet 3.5 베타 릴리스 정보](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC 릴리스 정보](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="f5273-105">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="f5273-106">2016 년 6 월 27 일에 Visual Studio 2013 및 nuget.exe 릴리스 되었습니다 NuGet 3.5 베타 2 RTM</span><span class="sxs-lookup"><span data-stu-id="f5273-106">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="f5273-107">전체 변경 로그</span><span class="sxs-lookup"><span data-stu-id="f5273-107">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="f5273-108">문제 목록</span><span class="sxs-lookup"><span data-stu-id="f5273-108">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="f5273-109">버그 수정</span><span class="sxs-lookup"><span data-stu-id="f5273-109">Bug Fixes</span></span>

* <span data-ttu-id="f5273-110">업데이트 된 오류 메시지를 인증 된 피드-에 대 한.NET Core에서는 암호 decrpytion에 대 한 지원 부족 [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="f5273-110">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="f5273-111">패키지 가져오기 패키지 관리자 콘솔에는.NET Core 프로젝트-열려 있으면 실패 [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="f5273-111">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="f5273-112">NuGet 푸시 명령에서 403의 잘못 된 처리를 수정 [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="f5273-112">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="f5273-113">DisableSourceControlIntegration 설정 된 경우 TFS 소스 제어에 바인딩할 솔루션에서 패키지를 제거할 때에 문제 해결-true로 [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="f5273-113">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="f5273-114">패키지 업데이트 계정-대상 패키지-상황이 해결 [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="f5273-114">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="f5273-115">MSBuild의 자세한 정도 수준을 사용 하 여 UI 작업-Nuget 패키지 관리자에 대 한로 거 수준을 설정 [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="f5273-115">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="f5273-116">NuGet 구성이 수정 프로그램은-VS 2015 VSIX (v3.4.3)-웹 사이트 프로젝트에서 잘못 된 오류 [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="f5273-116">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="f5273-117">팩 문제를 해결 `.csproj` 콘텐츠 파일은 포함-때 [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="f5273-117">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="f5273-118">DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) 작동 하지 않는- [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="f5273-118">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="f5273-119">-값은 패키지 만들기에는 null 일 수 없습니다-Nuget 3.4.3 릴리스에서 문제를 해결 [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="f5273-119">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="f5273-120">복원은 Nuget.Config에서 저장 된 자격 증명을 사용 하 여 VSTS 피드에- [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="f5273-120">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="f5273-121">성능-버전 비교 코드의 과도 한 할당 수정- [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="f5273-121">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="f5273-122">Nuget.exe 여러 개 병렬로-같은 패키지를 설치 하려고 할 때 문제를 해결 [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="f5273-122">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="f5273-123">-다중 프로젝트 작업에 대 한 종속성 정보 캐시-성능 [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="f5273-123">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="f5273-124">문제를 해결할 때 소스 목록이 비어 있는-패키지 소스 없습니다 설정에서 추가할 수 [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="f5273-124">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="f5273-125">디자인 타임 외관-에 의존 하는 패키지를 설치 하려고 할 때 Misleading 오류를 해결 [#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="f5273-125">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="f5273-126">첫 번째 소스-시도 PackageManager "All"을 설정 하는 콘솔에서 패키지를 설치 [#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="f5273-126">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="f5273-127">(모노)-나중에 한 번 쓰기를 사용 하 여 파일에 있는 패키지의 문제를 해결 [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="f5273-127">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="f5273-128">에 있을 때 오류 찾기 프로젝트 update 명령-예외 표시 [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="f5273-128">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="f5273-129">패키지 콘텐츠 인수와 함께 피드 nuget v3.3 +에서 패키지를 설치할 때 제대로 복원 되지-NoCache 패키지에 포함 된 경우 `.nupkg` 파일- [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="f5273-129">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="f5273-130">패키지와 문제 해결-1 원본의 패키지 누락 된 경우 (모든 원본의 경우)를 설치 [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="f5273-130">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="f5273-131">단일 소스 권한 부여-에 실패 하는 경우 블록 설치 [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="f5273-131">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="f5273-132">`.nuspec`범위는-IncludeReferencedProjects 버전-를 재정의 해야 하는 버전 [#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="f5273-132">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="f5273-133">NuGet 3.3.0 업데이트와 함께 실패 '... 추가 제약 조건에 정의 된 packages.config이이 작업을 방지 합니다.'</span><span class="sxs-lookup"><span data-stu-id="f5273-133">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="f5273-134"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="f5273-134"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="f5273-135">nuget.exe 업데이트 어셈블리의 강력한 이름 및 개인 특성을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f5273-135">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="f5273-136"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="f5273-136"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="f5273-137">"DefaultPushSource"-에 대 한 상대 파일 경로 문제 해결 [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="f5273-137">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="f5273-138">업데이트 확인자 실패 메시지-개선 [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="f5273-138">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="f5273-139">기능 및 동작 변경 내용</span><span class="sxs-lookup"><span data-stu-id="f5273-139">Features and Behavior Changes</span></span>

* <span data-ttu-id="f5273-140">nuget.exe 푸시-timeout 매개 변수 작동 하지 않는- [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="f5273-140">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="f5273-141">nuget.exe 복원을 생성 하지 않는다는 `.props` 및 `.targets` 파일에 대 한 `.nuproj` 프로젝트 (v3.4.3.855 회귀)- [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="f5273-141">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="f5273-142">확장성 API 가져오기-프레임 워크를 비교할 필요 [#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="f5273-142">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="f5273-143">종속성 옵션을 사용 하는 경우 숨기기 `project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="f5273-143">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="f5273-144">인쇄 결과물에 자세한 출력-버전 헤더 nuget.exe [#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="f5273-144">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="f5273-145">NuGet {rid} /runtimes/ /nativeassets/ {txm}에 대 한 지원을 추가 해야 /- [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="f5273-145">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>