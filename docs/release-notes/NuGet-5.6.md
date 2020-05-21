---
title: NuGet 5.6 릴리스 정보
description: 새 기능, 버그 수정 및 Ecrs를 비롯 한 NuGet 5.6에 대 한 릴리스 정보입니다.
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727808"
---
# <a name="nuget-56-release-notes"></a><span data-ttu-id="f94d8-103">NuGet 5.6 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="f94d8-103">NuGet 5.6 Release Notes</span></span>

<span data-ttu-id="f94d8-104">NuGet 배포 차량:</span><span class="sxs-lookup"><span data-stu-id="f94d8-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="f94d8-105">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="f94d8-105">NuGet version</span></span> | <span data-ttu-id="f94d8-106">Visual Studio 버전에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="f94d8-106">Available in Visual Studio version</span></span>| <span data-ttu-id="f94d8-107">.NET SDK에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="f94d8-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="f94d8-108">**5.6.0**</span><span class="sxs-lookup"><span data-stu-id="f94d8-108">**5.6.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="f94d8-109">Visual Studio 2019 버전 16.6</span><span class="sxs-lookup"><span data-stu-id="f94d8-109">Visual Studio 2019 version 16.6</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="f94d8-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="f94d8-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="f94d8-111"><sup>1</sup> .NET Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨</span><span class="sxs-lookup"><span data-stu-id="f94d8-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-56"></a><span data-ttu-id="f94d8-112">요약: 5.6의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="f94d8-112">Summary: What's New in 5.6</span></span>

* <span data-ttu-id="f94d8-113">부동 버전이 포함 된 시험판 패키지를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f94d8-113">Support prerelease packages with floating versions.</span></span> <span data-ttu-id="f94d8-114">`Version="*-*"``Version="1.*-*"`지정 된 범위 내에서 시험판 버전을 포함 하 여, 및 유사한 float를 최신 버전으로 [#912](https://github.com/NuGet/Home/issues/912)</span><span class="sxs-lookup"><span data-stu-id="f94d8-114">`Version="*-*"`, `Version="1.*-*"`, and similar float to latest versions, including prerelease versions, within specified range  - [#912](https://github.com/NuGet/Home/issues/912)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="f94d8-115">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="f94d8-115">Issues fixed in this release</span></span>

<span data-ttu-id="f94d8-116">**미**</span><span class="sxs-lookup"><span data-stu-id="f94d8-116">**Bugs:**</span></span>

* <span data-ttu-id="f94d8-117">`nuget push *.nupkg`snupkg가 없는 경우 실패- [#8148](https://github.com/NuGet/Home/issues/8148)</span><span class="sxs-lookup"><span data-stu-id="f94d8-117">`nuget push *.nupkg` fails when snupkg does not exist - [#8148](https://github.com/NuGet/Home/issues/8148)</span></span>

* <span data-ttu-id="f94d8-118">Pack 및 기타 일부 코드 경로는 로캘에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f94d8-118">Pack, and several other code paths, fail dependent on locale.</span></span> <span data-ttu-id="f94d8-119">System.text.regularexpressions.regexoptions 사용 Regexoptions.cultureinvariant- [#8246](https://github.com/NuGet/Home/issues/8246)</span><span class="sxs-lookup"><span data-stu-id="f94d8-119">Use RegexOptions.CultureInvariant - [#8246](https://github.com/NuGet/Home/issues/8246)</span></span>

* <span data-ttu-id="f94d8-120">성능: 언로드된 프로젝트 시나리오에 대 한 DG 사양은 미리 보기 복원으로 작성할 수 없습니다.- [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="f94d8-120">Perf: DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="f94d8-121">복원: 솔루션 종속성을 캐싱하여 성능을 향상 시킵니다. [#9201](https://github.com/NuGet/Home/issues/9201)</span><span class="sxs-lookup"><span data-stu-id="f94d8-121">Restore: Improve performance by caching solution dependency graph spec - [#9201](https://github.com/NuGet/Home/issues/9201)</span></span>

* <span data-ttu-id="f94d8-122">Pm 콘솔을 사용 하 여 패키지를 설치한 후에는 PM UI가 SDK 스타일 프로젝트에서 작동 하지 않음- [#9203](https://github.com/NuGet/Home/issues/9203)</span><span class="sxs-lookup"><span data-stu-id="f94d8-122">PM UI doesn't work for SDK style projects after installing a package with PM Console - [#9203](https://github.com/NuGet/Home/issues/9203)</span></span>

* <span data-ttu-id="f94d8-123">/Vs에 따라 로컬 패키지 피드가 포함 된 PM UI에 포함 아이콘을 표시할 수 없습니다. [#9225](https://github.com/NuGet/Home/issues/9225)</span><span class="sxs-lookup"><span data-stu-id="f94d8-123">Embedded icon can’t be shown in PM UI with local package feed - depending on / vs \ - [#9225](https://github.com/NuGet/Home/issues/9225)</span></span>

* <span data-ttu-id="f94d8-124">NuGetVersion. TryParseStrict ()는 구문 분석에 실패 하는 경우 false를 반환 합니다. [#9255](https://github.com/NuGet/Home/issues/9255)</span><span class="sxs-lookup"><span data-stu-id="f94d8-124">NuGetVersion.TryParseStrict() should return false if it fails to parse - [#9255](https://github.com/NuGet/Home/issues/9255)</span></span>

* <span data-ttu-id="f94d8-125">`nuget.exe push`에 대 한 도움말 `-source` 은 원본 URL이 아닌 원본 이름 사용을 제안 해야 합니다. [#9265](https://github.com/NuGet/Home/issues/9265)</span><span class="sxs-lookup"><span data-stu-id="f94d8-125">`nuget.exe push` help for `-source`, should suggest usage of source name, not source URL - [#9265](https://github.com/NuGet/Home/issues/9265)</span></span>

* <span data-ttu-id="f94d8-126">`dotnet nuget add package SourceUri`잘못 된 기본 패키지 원본 이름을 만듭니다. [#9277](https://github.com/NuGet/Home/issues/9277)</span><span class="sxs-lookup"><span data-stu-id="f94d8-126">`dotnet nuget add package SourceUri`  creates bad default package source name - [#9277](https://github.com/NuGet/Home/issues/9277)</span></span>

* <span data-ttu-id="f94d8-127">화면 읽기 프로그램에서 "검색 중 ..."을 알리지 않습니다. 탭 전환 시 메시지- [#9307](https://github.com/NuGet/Home/issues/9307)</span><span class="sxs-lookup"><span data-stu-id="f94d8-127">Screen reader doesn't announce "Searching..." message when switching tabs - [#9307](https://github.com/NuGet/Home/issues/9307)</span></span>

* <span data-ttu-id="f94d8-128">접근성: 포커스 사각형 색은 진한 테마의 PM UI 탭에 액세스할 수 없습니다.- [#9336](https://github.com/NuGet/Home/issues/9336)</span><span class="sxs-lookup"><span data-stu-id="f94d8-128">Accessibility: Focus-rectangle color is not accessible PM UI tabs in dark theme - [#9336](https://github.com/NuGet/Home/issues/9336)</span></span>

* <span data-ttu-id="f94d8-129">nuget .exe 5.5이 MSBuild 14 또는 아래 [#9458](https://github.com/NuGet/Home/issues/9458) 으로 복원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f94d8-129">nuget.exe 5.5 fails to restore with MSBuild 14 or below - [#9458](https://github.com/NuGet/Home/issues/9458)</span></span>

* <span data-ttu-id="f94d8-130">복원 메시지에서 밀리초 번 기록 안 함- [#8977](https://github.com/NuGet/Home/issues/8977)</span><span class="sxs-lookup"><span data-stu-id="f94d8-130">Don't log millisecond times in restore messages - [#8977](https://github.com/NuGet/Home/issues/8977)</span></span>

* <span data-ttu-id="f94d8-131">IOutputConsole 비동기 작업 [#9268](https://github.com/NuGet/Home/issues/9268)</span><span class="sxs-lookup"><span data-stu-id="f94d8-131">Make IOutputConsole async - [#9268](https://github.com/NuGet/Home/issues/9268)</span></span>

* <span data-ttu-id="f94d8-132">MSBuild 버전 선택은 일부 영어가 아닌 문화권에서 제대로 작동 하지 않습니다. [#9322](https://github.com/NuGet/Home/issues/9322)</span><span class="sxs-lookup"><span data-stu-id="f94d8-132">MSBuild version picking works poorly on some non-english cultures - [#9322](https://github.com/NuGet/Home/issues/9322)</span></span>

* <span data-ttu-id="f94d8-133">#9337에 대 한 누락 된 서식 기본값 `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)</span><span class="sxs-lookup"><span data-stu-id="f94d8-133">Missing format default on `dotnet nuget list source` - [#9337](https://github.com/NuGet/Home/issues/9337)</span></span>

* <span data-ttu-id="f94d8-134">Perf: RestoreOperationLogger에 불필요 한 스레드 선호도가 있습니다. [#9288](https://github.com/NuGet/Home/issues/9288)</span><span class="sxs-lookup"><span data-stu-id="f94d8-134">Perf: RestoreOperationLogger has unnecessary thread affinity - [#9288](https://github.com/NuGet/Home/issues/9288)</span></span>

* <span data-ttu-id="f94d8-135">명령에 대 한 docs 자동 생성 `dotnet nuget` - [#9146](https://github.com/NuGet/Home/issues/9146)</span><span class="sxs-lookup"><span data-stu-id="f94d8-135">Automated creation of docs for `dotnet nuget` commands - [#9146](https://github.com/NuGet/Home/issues/9146)</span></span>

* <span data-ttu-id="f94d8-136">기본 자세한 정도는 각 프로젝트의 noop 복원 [#8792](https://github.com/NuGet/Home/issues/8792) 보고 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f94d8-136">Default verbosity should not report each project's noop restore - [#8792](https://github.com/NuGet/Home/issues/8792)</span></span>

* <span data-ttu-id="f94d8-137">`-DependencyVersion` `NuGet.exe update` 설치 명령- [#7694](https://github.com/NuGet/Home/issues/7694) 와 유사한의 지원 매개 변수</span><span class="sxs-lookup"><span data-stu-id="f94d8-137">Support `-DependencyVersion` parameter for `NuGet.exe update`, similar to install command - [#7694](https://github.com/NuGet/Home/issues/7694)</span></span>


<span data-ttu-id="f94d8-138">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="f94d8-138">**DCRs:**</span></span>

* <span data-ttu-id="f94d8-139">Net 5.0 대상 프레임 워크에 대 한 초기 지원 추가- [#9584](https://github.com/NuGet/Home/issues/9584)</span><span class="sxs-lookup"><span data-stu-id="f94d8-139">Add initial support for net5.0 target framework - [#9584](https://github.com/NuGet/Home/issues/9584)</span></span>

* <span data-ttu-id="f94d8-140">PM UI의 업데이트 탭에서 ID 별로 패키지 정렬- [#9278](https://github.com/NuGet/Home/issues/9278)</span><span class="sxs-lookup"><span data-stu-id="f94d8-140">Sort packages by ID in the Updates tab of the PM UI - [#9278](https://github.com/NuGet/Home/issues/9278)</span></span>


<span data-ttu-id="f94d8-141">**[이 릴리스에서 해결 된 모든 문제 목록-5.6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span><span class="sxs-lookup"><span data-stu-id="f94d8-141">**[List of all issues fixed in this release - 5.6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span></span>
