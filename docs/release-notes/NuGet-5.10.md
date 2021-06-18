---
title: NuGet 5.10 릴리스 정보
description: 새로운 기능, 버그 수정 및 DCR을 포함한 NuGet 5.10 릴리스 정보입니다.
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356502"
---
# <a name="nuget-510-release-notes"></a><span data-ttu-id="0de38-103">NuGet 5.10 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="0de38-103">NuGet 5.10 Release Notes</span></span>

<span data-ttu-id="0de38-104">NuGet 배포 차량:</span><span class="sxs-lookup"><span data-stu-id="0de38-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="0de38-105">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="0de38-105">NuGet version</span></span> | <span data-ttu-id="0de38-106">Visual Studio 버전에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="0de38-106">Available in Visual Studio version</span></span> | <span data-ttu-id="0de38-107">.NET SDK에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="0de38-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="0de38-108">**5.10.0**</span><span class="sxs-lookup"><span data-stu-id="0de38-108">**5.10.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="0de38-109">Visual Studio 2019 버전 16.10</span><span class="sxs-lookup"><span data-stu-id="0de38-109">Visual Studio 2019 version 16.10</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="0de38-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="0de38-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |

<span data-ttu-id="0de38-111"><sup>1</sup> .NET Core 워크로드를 Visual Studio 2019와 함께 설치</span><span class="sxs-lookup"><span data-stu-id="0de38-111"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="0de38-112">Visual Studio 16.10, MSBuild 16.10 및 .NET 5.0.300 이상에는 NuGet.exe 5.10이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0de38-112">Visual Studio 16.10, MSBuild 16.10, and .NET 5.0.300+ requires NuGet.exe 5.10 or later.</span></span>

## <a name="summary-whats-new-in-510"></a><span data-ttu-id="0de38-113">요약: 5.10의 새로운 내용</span><span class="sxs-lookup"><span data-stu-id="0de38-113">Summary: What's New in 5.10</span></span>

* <span data-ttu-id="0de38-114">서명: dotnet trusted-signers 명령 구현 - [#8053](https://github.com/NuGet/Home/issues/8053)</span><span class="sxs-lookup"><span data-stu-id="0de38-114">Signing: implement dotnet trusted-signers command - [#8053](https://github.com/NuGet/Home/issues/8053)</span></span>

* <span data-ttu-id="0de38-115">Linux에서 기본 유효성 검사를 사용하지 않도록 설정하지만 Windows에서 기본적으로 사용하도록 설정 - [#10713](https://github.com/NuGet/Home/issues/10713)</span><span class="sxs-lookup"><span data-stu-id="0de38-115">Make default validation disabled on Linux, but enabled by default on Windows - [#10713](https://github.com/NuGet/Home/issues/10713)</span></span>

* <span data-ttu-id="0de38-116">.NET 5+ Linux/MAC에서 패키지 서명 확인을 위한 ENV 변수 추가 - [#10742](https://github.com/NuGet/Home/issues/10742)</span><span class="sxs-lookup"><span data-stu-id="0de38-116">Add an ENV Variable for Package Signing Verification on .NET 5+ Linux/MAC - [#10742](https://github.com/NuGet/Home/issues/10742)</span></span>

* <span data-ttu-id="0de38-117">대규모 솔루션에 대한 새 패키지 설치 성능 향상 - [#10166](https://github.com/NuGet/Home/issues/10166)</span><span class="sxs-lookup"><span data-stu-id="0de38-117">Improve install new package performance for large solutions - [#10166](https://github.com/NuGet/Home/issues/10166)</span></span>

* <span data-ttu-id="0de38-118">`nfproj`프로젝트 형식을 Nuget CLI용 supportedProjectExtensions 목록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0de38-118">Add the project type `nfproj` to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="0de38-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="0de38-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="0de38-120">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="0de38-120">Issues fixed in this release</span></span>

* <span data-ttu-id="0de38-121">프로젝트를 <requireLicenseAcceptance> 패킹할 때 요소 표시 안 함 - [#5133](https://github.com/NuGet/Home/issues/5133)</span><span class="sxs-lookup"><span data-stu-id="0de38-121">Suppress the <requireLicenseAcceptance> element when packing a project - [#5133](https://github.com/NuGet/Home/issues/5133)</span></span>

* <span data-ttu-id="0de38-122">[CPVM] 미리 보기 경고가 dotnet cli에 표시되어야 합니다. - [#10226](https://github.com/NuGet/Home/issues/10226)</span><span class="sxs-lookup"><span data-stu-id="0de38-122">[CPVM] preview warning should be shown on dotnet cli - [#10226](https://github.com/NuGet/Home/issues/10226)</span></span>

* <span data-ttu-id="0de38-123">PMUI의 배경색 및 전경색 토큰을 CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)</span><span class="sxs-lookup"><span data-stu-id="0de38-123">Update the background and foreground color tokens of the PMUI to CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)</span></span>

* <span data-ttu-id="0de38-124">[버그 Bash] PM UI에서 탭 간을 빠르게 전환할 때 오류 목록 창에 "사용자가 취소한 작업" 오류 표시 - [#10671](https://github.com/NuGet/Home/issues/10671)</span><span class="sxs-lookup"><span data-stu-id="0de38-124">[Bug Bash] Error “operation canceled by user” show in Error List window when switching between tabs quickly in PM UI - [#10671](https://github.com/NuGet/Home/issues/10671)</span></span>

* <span data-ttu-id="0de38-125">PM UI: 솔루션 수준에서 패키지 설치 성능 향상 - [#10210](https://github.com/NuGet/Home/issues/10210)</span><span class="sxs-lookup"><span data-stu-id="0de38-125">PM UI:  Improve package installation performance on the solution level - [#10210](https://github.com/NuGet/Home/issues/10210)</span></span>

* <span data-ttu-id="0de38-126">GetService를 NuGet.Clients의 모든 위치에서 GetServiceAsync로 바꿉니다. - [#3784](https://github.com/NuGet/Home/issues/3784)</span><span class="sxs-lookup"><span data-stu-id="0de38-126">Replace GetService with GetServiceAsync everywhere in NuGet.Clients - [#3784](https://github.com/NuGet/Home/issues/3784)</span></span>

* <span data-ttu-id="0de38-127">상대 경로의 NuGet.exe 팩 성능 문제 `..` - [#5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="0de38-127">NuGet.exe pack performance problem with `..` relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>

* <span data-ttu-id="0de38-128">원본 경로의 수준이 증가함에 따라 "nuget pack"의 성능이 저하됩니다. [#5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="0de38-128">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>

* <span data-ttu-id="0de38-129">NuGet은 중복 파일로 nuspec을 패키징할 때 오류가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0de38-129">NuGet doesn't error when packaging nuspec with duplicate files.</span></span><span data-ttu-id="0de38-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span><span class="sxs-lookup"><span data-stu-id="0de38-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span></span>

* <span data-ttu-id="0de38-131">NuGet 팩 "지정된 DateTimeOffset을 Zip 파일 타임스탬프로 변환할 수 없습니다." - [#7001](https://github.com/NuGet/Home/issues/7001)</span><span class="sxs-lookup"><span data-stu-id="0de38-131">NuGet pack "The DateTimeOffset specified cannot be converted into a Zip file timestamp" - [#7001](https://github.com/NuGet/Home/issues/7001)</span></span>

* <span data-ttu-id="0de38-132">포장된 패키지 파일의 타임스탬프가 시간대로 이동됩니다- [#7395](https://github.com/NuGet/Home/issues/7395)</span><span class="sxs-lookup"><span data-stu-id="0de38-132">Timestamps of file of packed package is shifted by the timezone - [#7395](https://github.com/NuGet/Home/issues/7395)</span></span>

* <span data-ttu-id="0de38-133">NU1004에는 더 많은 실행 가능한 정보가 포함되어야 합니다. [#7696](https://github.com/NuGet/Home/issues/7696)</span><span class="sxs-lookup"><span data-stu-id="0de38-133">NU1004 should contain more actionable information  - [#7696](https://github.com/NuGet/Home/issues/7696)</span></span>

* <span data-ttu-id="0de38-134">[버그 Bash] [테스트 실패] 'dotnet restore --use-lock-file --locked-mode'를 실행할 때는 비어 있거나 형식이 잘못된 잠금 파일을 업데이트하면 안 [됩니다.](https://github.com/NuGet/Home/issues/8640) - #8640</span><span class="sxs-lookup"><span data-stu-id="0de38-134">[Bug Bash][Test Failure] The empty/malformed lock file should not be updated when running ‘dotnet restore --use-lock-file --locked-mode’ - [#8640](https://github.com/NuGet/Home/issues/8640)</span></span>

* <span data-ttu-id="0de38-135">NuGetVersionRange를 사용하면 논리적으로 잘못된 범위를 구문 분석할 수 [있습니다. #9145](https://github.com/NuGet/Home/issues/9145)</span><span class="sxs-lookup"><span data-stu-id="0de38-135">NuGetVersionRange allows logically incorrect ranges to be parsed - [#9145](https://github.com/NuGet/Home/issues/9145)</span></span>

* <span data-ttu-id="0de38-136">PM UI는 선택한 패키지 원본과 마우스로 가리킨 패키지 원본 간에 구별 가능한 배경색을 표시할 수 없습니다. [- #9538](https://github.com/NuGet/Home/issues/9538)</span><span class="sxs-lookup"><span data-stu-id="0de38-136">PM UI can’t show distinguishable background color between selected and hovered package sources - [#9538](https://github.com/NuGet/Home/issues/9538)</span></span>

* <span data-ttu-id="0de38-137">설치할 프로젝트를 선택하기 위한 확인란이 화면 판독기에서 읽혀지지 않음 - [#9578](https://github.com/NuGet/Home/issues/9578)</span><span class="sxs-lookup"><span data-stu-id="0de38-137">Checkbox for selecting projects to install to isn't being read by screen reader - [#9578](https://github.com/NuGet/Home/issues/9578)</span></span>

* <span data-ttu-id="0de38-138">세부 정보 창 버전 드롭다운 기본 선택은 설치/업데이트 탭에서 설치/최신성이어야 합니다. - [#9887](https://github.com/NuGet/Home/issues/9887)</span><span class="sxs-lookup"><span data-stu-id="0de38-138">Details Pane Versions Dropdown default selection should be Installed/LatestStable on Installed/Updates tabs - [#9887](https://github.com/NuGet/Home/issues/9887)</span></span>

* <span data-ttu-id="0de38-139">일부 .NET 5 SDK 보고서 TargetPlatformMoniker에 대한 해결 방법 계정을 ` ,Version= `  -  [제거합니다#9913](https://github.com/NuGet/Home/issues/9913)</span><span class="sxs-lookup"><span data-stu-id="0de38-139">Remove workaround account for some .NET 5 SDKs report TargetPlatformMoniker of ` ,Version= ` - [#9913](https://github.com/NuGet/Home/issues/9913)</span></span>

* <span data-ttu-id="0de38-140">dotnet nuget verify가 너무 작음 - [#10316](https://github.com/NuGet/Home/issues/10316)</span><span class="sxs-lookup"><span data-stu-id="0de38-140">dotnet nuget verify is too quiet - [#10316](https://github.com/NuGet/Home/issues/10316)</span></span>

* <span data-ttu-id="0de38-141">VersionRange는 한 자리 범위를 구문 분석할 수 없습니다. [- #10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="0de38-141">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>

* <span data-ttu-id="0de38-142">VS 솔루션 관리자가 디버깅 중에 에 대해 null 예외를 throw합니다. [- #10352](https://github.com/NuGet/Home/issues/10352)</span><span class="sxs-lookup"><span data-stu-id="0de38-142">VS Solution manager throws null exception for during debugging - [#10352](https://github.com/NuGet/Home/issues/10352)</span></span>

* <span data-ttu-id="0de38-143">CLI 예외 메시지를 문자열 리소스 파일로 이동 - [#10392](https://github.com/NuGet/Home/issues/10392)</span><span class="sxs-lookup"><span data-stu-id="0de38-143">Move CLI exception messages to String Resource files - [#10392](https://github.com/NuGet/Home/issues/10392)</span></span>

* <span data-ttu-id="0de38-144">데드 코드 제거(TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)</span><span class="sxs-lookup"><span data-stu-id="0de38-144">Remove dead code (TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)</span></span>

* <span data-ttu-id="0de38-145">업데이트 상황에 맞는 메뉴가 첫 번째 선택한 항목으로 스크롤되어야 합니다. [- #10498](https://github.com/NuGet/Home/issues/10498)</span><span class="sxs-lookup"><span data-stu-id="0de38-145">Update context menu should scroll to first selected item - [#10498](https://github.com/NuGet/Home/issues/10498)</span></span>

* <span data-ttu-id="0de38-146">솔루션 PMUI 세부 정보에서 가로 막대가 겹칩니다. [- #10533](https://github.com/NuGet/Home/issues/10533)</span><span class="sxs-lookup"><span data-stu-id="0de38-146">Solution PMUI Details has overlapping horizontal bar - [#10533](https://github.com/NuGet/Home/issues/10533)</span></span>

* <span data-ttu-id="0de38-147">서명: 인증서가 만료되고 타임스탬프가 신뢰할 수 없는 경우 기본 서명 세부 정보가 표시되지 않음 - [#10535](https://github.com/NuGet/Home/issues/10535)</span><span class="sxs-lookup"><span data-stu-id="0de38-147">Signing:  primary signature details not displayed when certificate expired and timestamp untrusted - [#10535](https://github.com/NuGet/Home/issues/10535)</span></span>

* <span data-ttu-id="0de38-148">사용하도록 설정된 원본이 없을 경우 PM UI가 표시되지 않습니다. [#10541](https://github.com/NuGet/Home/issues/10541)</span><span class="sxs-lookup"><span data-stu-id="0de38-148">Having no enabled sources prevents the PM UI from showing - [#10541](https://github.com/NuGet/Home/issues/10541)</span></span>

* <span data-ttu-id="0de38-149">패키지 메타데이터(세부 정보, 사용 중단)가 CodeSpaces의 nuget.org 끌어오지 않는 경우가 있습니다. - [#10549](https://github.com/NuGet/Home/issues/10549)</span><span class="sxs-lookup"><span data-stu-id="0de38-149">Package Metadata (details, deprecation) are sometimes not pulled from nuget.org in CodeSpaces - [#10549](https://github.com/NuGet/Home/issues/10549)</span></span>

* <span data-ttu-id="0de38-150">디버그 세션 중 예외로 PMUI 초기화 실패 - [#10559](https://github.com/NuGet/Home/issues/10559)</span><span class="sxs-lookup"><span data-stu-id="0de38-150">PMUI initialization fails with exception during debug session - [#10559](https://github.com/NuGet/Home/issues/10559)</span></span>

* <span data-ttu-id="0de38-151">nuget 복원으로 big endian 시스템에서 패키지 무결성 검사 실패 - [#10567](https://github.com/NuGet/Home/issues/10567)</span><span class="sxs-lookup"><span data-stu-id="0de38-151">nuget restore results in a package integrity check failure on big endian system - [#10567](https://github.com/NuGet/Home/issues/10567)</span></span>

* <span data-ttu-id="0de38-152">PackagingException 대신 FormatException이 throw됩니다. [- #10595](https://github.com/NuGet/Home/issues/10595)</span><span class="sxs-lookup"><span data-stu-id="0de38-152">FormatException is thrown instead of PackagingException - [#10595](https://github.com/NuGet/Home/issues/10595)</span></span>

* <span data-ttu-id="0de38-153">CPVM - 그래프 보행 알고리즘의 동시성 문제 - [#10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="0de38-153">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>

* <span data-ttu-id="0de38-154">PMC powershell 버전 원격 분석 추가 - [#10609](https://github.com/NuGet/Home/issues/10609)</span><span class="sxs-lookup"><span data-stu-id="0de38-154">Add PMC powershell version telemetry - [#10609](https://github.com/NuGet/Home/issues/10609)</span></span>

* <span data-ttu-id="0de38-155">NuGetVersion 정렬 성능 향상 - [#10611](https://github.com/NuGet/Home/issues/10611)</span><span class="sxs-lookup"><span data-stu-id="0de38-155">Improve NuGetVersion sort performance - [#10611](https://github.com/NuGet/Home/issues/10611)</span></span>

* <span data-ttu-id="0de38-156">신뢰할 수 있는 서명자 추가에 일치하지 않는 인수가 [있습니다. - #10647](https://github.com/NuGet/Home/issues/10647)</span><span class="sxs-lookup"><span data-stu-id="0de38-156">Trusted-signers Add has inconsistent arguments - [#10647](https://github.com/NuGet/Home/issues/10647)</span></span>

* <span data-ttu-id="0de38-157">Vs2019 v16.9.0: NuGet 패키지 관리자 탭을 "업데이트"에서 "설치"로 전환해도 프레임이 업데이트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0de38-157">Vs2019 v16.9.0: Switching tabs in NuGet Package Manager from "Updates" to "Installed" doesn't update the frame.</span></span><span data-ttu-id="0de38-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span><span class="sxs-lookup"><span data-stu-id="0de38-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span></span>

* <span data-ttu-id="0de38-159">PMUI의 버전 번호에서 "v"를 제거합니다. [- #10677](https://github.com/NuGet/Home/issues/10677)</span><span class="sxs-lookup"><span data-stu-id="0de38-159">Remove the "v" from the version number in PMUI - [#10677](https://github.com/NuGet/Home/issues/10677)</span></span>

* <span data-ttu-id="0de38-160">INuGetProjectService.GetInstalledPackagesAsync가 CPS 프로젝트 시스템 추천을 받기 전에 throw함 - [#10681](https://github.com/NuGet/Home/issues/10681)</span><span class="sxs-lookup"><span data-stu-id="0de38-160">INuGetProjectService.GetInstalledPackagesAsync throws before receiving CPS project system nomination - [#10681](https://github.com/NuGet/Home/issues/10681)</span></span>

* <span data-ttu-id="0de38-161">포함된 아이콘으로 인해 찾아보기 탭의 원본 "Microsoft Visual Studio 오프라인 패키지"에서 액세스가 거부됩니다. - [#10687](https://github.com/NuGet/Home/issues/10687)</span><span class="sxs-lookup"><span data-stu-id="0de38-161">Embedded Icons cause Access Denied from source "Microsoft Visual Studio Offline Packages" on Browse tab - [#10687](https://github.com/NuGet/Home/issues/10687)</span></span>

* <span data-ttu-id="0de38-162">MSBuildProjectExtensionsPath가 설정되지 않은 경우 INuGetProjectService.GetInstalledPackagesAsync가 throw됩니다. [- #10739](https://github.com/NuGet/Home/issues/10739)</span><span class="sxs-lookup"><span data-stu-id="0de38-162">INuGetProjectService.GetInstalledPackagesAsync throws when MSBuildProjectExtensionsPath is not set - [#10739](https://github.com/NuGet/Home/issues/10739)</span></span>

* <span data-ttu-id="0de38-163">"dotnet nuget remove source nuget.org"가 처음으로 작동하지 않습니다. [#10745](https://github.com/NuGet/Home/issues/10745)</span><span class="sxs-lookup"><span data-stu-id="0de38-163">"dotnet nuget remove source nuget.org" doesn't work the first time - [#10745](https://github.com/NuGet/Home/issues/10745)</span></span>

* <span data-ttu-id="0de38-164">Nuget은 UI 스레드에 대한 동기 호출을 만드는 비동기 메서드에서 스레드 풀 스레드를 [차단합니다. #10775](https://github.com/NuGet/Home/issues/10775)</span><span class="sxs-lookup"><span data-stu-id="0de38-164">Nuget blocks a threadpool thread in an async method making a synchronous call to the UI thread - [#10775](https://github.com/NuGet/Home/issues/10775)</span></span>

* <span data-ttu-id="0de38-165">도구 -> 옵션 -> NuGet 패키지 관리자 문자열이 잘립니다. - [#10779](https://github.com/NuGet/Home/issues/10779)</span><span class="sxs-lookup"><span data-stu-id="0de38-165">Tools -> Options -> NuGet Package Manager string is truncated - [#10779](https://github.com/NuGet/Home/issues/10779)</span></span>

* <span data-ttu-id="0de38-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` 는 데드 코드이고 성능이 저하됩니다. [- #10790](https://github.com/NuGet/Home/issues/10790)</span><span class="sxs-lookup"><span data-stu-id="0de38-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` is dead code and hurting performance - [#10790](https://github.com/NuGet/Home/issues/10790)</span></span>

* <span data-ttu-id="0de38-167">NuGet SDK 패키지에서 포함 아이콘 사용 - [#10795](https://github.com/NuGet/Home/issues/10795)</span><span class="sxs-lookup"><span data-stu-id="0de38-167">Use embedded icon in NuGet SDK packages - [#10795](https://github.com/NuGet/Home/issues/10795)</span></span>

* <span data-ttu-id="0de38-168">SPDX 라이선스 목록 업데이트 - [#10806](https://github.com/NuGet/Home/issues/10806)</span><span class="sxs-lookup"><span data-stu-id="0de38-168">Update the SPDX license list - [#10806](https://github.com/NuGet/Home/issues/10806)</span></span>

<span data-ttu-id="0de38-169">**[이 릴리스에서 해결된 모든 문제 목록 - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span><span class="sxs-lookup"><span data-stu-id="0de38-169">**[List of all issues fixed in this release - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span></span>
  
<span data-ttu-id="0de38-170">**[이 릴리스의 커밋 목록 - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span><span class="sxs-lookup"><span data-stu-id="0de38-170">**[List of commits in this release - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span></span>
  
### <a name="community-contributions"></a><span data-ttu-id="0de38-171">커뮤니티 기여</span><span class="sxs-lookup"><span data-stu-id="0de38-171">Community contributions</span></span>

<span data-ttu-id="0de38-172">이 NuGet 릴리스를 만드는 데 도움을 주신 모든 기여자에게 감사드립니다.</span><span class="sxs-lookup"><span data-stu-id="0de38-172">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="0de38-173">대상</span><span class="sxs-lookup"><span data-stu-id="0de38-173">Who</span></span>|<span data-ttu-id="0de38-174">Prs</span><span class="sxs-lookup"><span data-stu-id="0de38-174">PRs</span></span>|<span data-ttu-id="0de38-175">문제</span><span class="sxs-lookup"><span data-stu-id="0de38-175">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="0de38-176">2018년 10월</span><span class="sxs-lookup"><span data-stu-id="0de38-176">louis-z</span></span>](https://github.com/louis-z) | [<span data-ttu-id="0de38-177">3991</span><span class="sxs-lookup"><span data-stu-id="0de38-177">3991</span></span>](https://github.com/NuGet/NuGet.Client/pull/3991) | <span data-ttu-id="0de38-178">VersionRange는 한 자리 범위를 구문 분석할 수 없습니다. [- #10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="0de38-178">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>
[<span data-ttu-id="0de38-179">omajid</span><span class="sxs-lookup"><span data-stu-id="0de38-179">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="0de38-180">3860</span><span class="sxs-lookup"><span data-stu-id="0de38-180">3860</span></span>](https://github.com/NuGet/NuGet.Client/pull/3860) | <span data-ttu-id="0de38-181">NuGet.Client build.sh 손상되었습니다. - [#10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="0de38-181">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="0de38-182">Nirmal4G</span><span class="sxs-lookup"><span data-stu-id="0de38-182">Nirmal4G</span></span>](https://github.com/Nirmal4G) | [<span data-ttu-id="0de38-183">3623</span><span class="sxs-lookup"><span data-stu-id="0de38-183">3623</span></span>](https://github.com/NuGet/NuGet.Client/pull/3623) | <span data-ttu-id="0de38-184">NuGet.Client build.sh 손상되었습니다. - [#10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="0de38-184">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="0de38-185">BlackGad</span><span class="sxs-lookup"><span data-stu-id="0de38-185">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="0de38-186">3953</span><span class="sxs-lookup"><span data-stu-id="0de38-186">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="0de38-187">원본 경로의 수준이 증가함에 따라 "nuget pack"의 성능이 저하됩니다. [#5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="0de38-187">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>
[<span data-ttu-id="0de38-188">BlackGad</span><span class="sxs-lookup"><span data-stu-id="0de38-188">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="0de38-189">3953</span><span class="sxs-lookup"><span data-stu-id="0de38-189">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="0de38-190">NuGet.exe 팩 성능 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de38-190">NuGet.exe pack performance problem with ..</span></span> <span data-ttu-id="0de38-191">상대 경로 - [#5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="0de38-191">relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>
[<span data-ttu-id="0de38-192">일치어 krystianc</span><span class="sxs-lookup"><span data-stu-id="0de38-192">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="0de38-193">3940</span><span class="sxs-lookup"><span data-stu-id="0de38-193">3940</span></span>](https://github.com/NuGet/NuGet.Client/pull/3940) | <span data-ttu-id="0de38-194">CPVM - 그래프 보행 알고리즘의 동시성 문제 - [#10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="0de38-194">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>
[<span data-ttu-id="0de38-195">josesimoes</span><span class="sxs-lookup"><span data-stu-id="0de38-195">josesimoes</span></span>](https://github.com/josesimoes) | [<span data-ttu-id="0de38-196">3943</span><span class="sxs-lookup"><span data-stu-id="0de38-196">3943</span></span>](https://github.com/NuGet/NuGet.Client/pull/3943) | <span data-ttu-id="0de38-197">nuget CLI용 supportedProjectExtensions 목록에 nfproj 프로젝트 형식을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0de38-197">Add the project type nfproj to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="0de38-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="0de38-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

## <a name="feedback-welcome"></a><span data-ttu-id="0de38-199">피드백 환영</span><span class="sxs-lookup"><span data-stu-id="0de38-199">Feedback welcome</span></span>

<span data-ttu-id="0de38-200">Microsoft는 사용자의 의견을 소중하게 생각합니다.</span><span class="sxs-lookup"><span data-stu-id="0de38-200">Your feedback is important to us.</span></span>  <span data-ttu-id="0de38-201">이 릴리스에 문제가 있는 경우 [GitHub 문제](https://github.com/NuGet/Home/issues) 및 기존 문제에 대한 [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="0de38-201">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="0de38-202">NuGet 내의 새로운 문제는 [GitHub 문제](https://github.com/NuGet/Home/issues/new)를 보고하세요.</span><span class="sxs-lookup"><span data-stu-id="0de38-202">For new issues within NuGet, please report a [GitHub Issue](https://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="0de38-203">일반적인 NuGet 환경 문제의 경우 도움말 > [문제 보고에서](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) 즐겨 찾는 IDE에 있는 **문제 보고** 옵션을 통해 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="0de38-203">For general NuGet experience issues, let us know via the [Report a Problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>
