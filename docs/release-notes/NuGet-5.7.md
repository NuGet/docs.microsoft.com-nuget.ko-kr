---
title: NuGet 5.7 릴리스 정보
description: 새 기능, 버그 수정 및 Ecrs를 비롯 한 NuGet 5.7에 대 한 릴리스 정보입니다.
author: chgill-msft
ms.author: chgill
ms.date: 8/14/2020
ms.topic: conceptual
ms.openlocfilehash: 58ab481f0c6a6cb5549c269788170b8c3ff6002f
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508789"
---
# <a name="nuget-57-release-notes"></a><span data-ttu-id="6fb0e-103">NuGet 5.7 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="6fb0e-103">NuGet 5.7 Release Notes</span></span>

<span data-ttu-id="6fb0e-104">NuGet 배포 차량:</span><span class="sxs-lookup"><span data-stu-id="6fb0e-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="6fb0e-105">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="6fb0e-105">NuGet version</span></span> | <span data-ttu-id="6fb0e-106">Visual Studio 버전에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="6fb0e-106">Available in Visual Studio version</span></span> | <span data-ttu-id="6fb0e-107">.NET SDK에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="6fb0e-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="6fb0e-108">**5.7.0 이상이 필요**</span><span class="sxs-lookup"><span data-stu-id="6fb0e-108">**5.7.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="6fb0e-109">Visual Studio 2019 버전 16.7</span><span class="sxs-lookup"><span data-stu-id="6fb0e-109">Visual Studio 2019 version 16.7</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="6fb0e-110">[3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="6fb0e-110">[3.1.401](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |
| [<span data-ttu-id="6fb0e-111">**5.7.1**</span><span class="sxs-lookup"><span data-stu-id="6fb0e-111">**5.7.1**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="6fb0e-112">Visual Studio 2019 버전 16.7</span><span class="sxs-lookup"><span data-stu-id="6fb0e-112">Visual Studio 2019 version 16.7</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="6fb0e-113">[3.1.408](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="6fb0e-113">[3.1.408](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="6fb0e-114"><sup>1</sup> .net Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨</span><span class="sxs-lookup"><span data-stu-id="6fb0e-114"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-57"></a><span data-ttu-id="6fb0e-115">요약: 5.7의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="6fb0e-115">Summary: What's New in 5.7</span></span>

### <a name="features-added-in-this-release"></a><span data-ttu-id="6fb0e-116">이 릴리스에 추가 된 기능</span><span class="sxs-lookup"><span data-stu-id="6fb0e-116">Features added in this release</span></span>

* <span data-ttu-id="6fb0e-117">NuGet 패키지 참조에 대 한 extern 별칭 지원이 추가 됨- [#4989](https://github.com/NuGet/Home/issues/4989)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-117">Added extern alias support for NuGet package references - [#4989](https://github.com/NuGet/Home/issues/4989)</span></span>

* <span data-ttu-id="6fb0e-118">데이터 원본을 공유 하 고 resfreshing를 줄이는 것을 허용 하 여 설치 된 탭과 업데이트 탭 간의 전환을 더 빠르게 수행 했습니다. [#8294](https://github.com/NuGet/Home/issues/8294)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-118">Made switching between Installed and Updates tabs faster by allowing them to share a data source and reducing resfreshing - [#8294](https://github.com/NuGet/Home/issues/8294)</span></span>

* <span data-ttu-id="6fb0e-119">MSBuild 정적 그래프 api (dotnet.exe [#9644](https://github.com/NuGet/Home/issues/9644) )를 호출 하 여 신속한 복원 속도 평가</span><span class="sxs-lookup"><span data-stu-id="6fb0e-119">Make restore faster - speed up evaluations by calling MSBuild Static Graph apis (dotnet.exe) - [#9644](https://github.com/NuGet/Home/issues/9644)</span></span>

* <span data-ttu-id="6fb0e-120">PackageReference 프로젝트에 대 한 Visual Studio 부분 복원 추가 (op + +)- [#9513](https://github.com/NuGet/Home/issues/9513)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-120">Added Visual Studio partial restore for PackageReference projects (no-op++) - [#9513](https://github.com/NuGet/Home/issues/9513)</span></span>

* <span data-ttu-id="6fb0e-121">Visual Studio 패키지 관리자 UI는 HTTP 요청당 요청 된 수를 초과 하 여 반환 되는 오동작 패키지 원본을 검색할 때 자주 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fb0e-121">Visual Studio Package Manager UI will crash less often when searching misbehaving package sources that return more than the requested number of results per HTTP request.</span></span><span data-ttu-id="6fb0e-122"> - [#8478](https://github.com/NuGet/Home/issues/8478)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-122"> - [#8478](https://github.com/NuGet/Home/issues/8478)</span></span>

* <span data-ttu-id="6fb0e-123">VS 복원에서 비 SDK 스타일 프로젝트에 대 한 PackageVersion 정보 통합이 추가 됨- [#9236](https://github.com/NuGet/Home/issues/9236)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-123">Added integration of PackageVersion information for non-SDK style projects in VS restore  - [#9236](https://github.com/NuGet/Home/issues/9236)</span></span>

* <span data-ttu-id="6fb0e-124">nuget.exe 업데이트에 대 한 지원이 추가 되었습니다 `-self -Source` https://feed  -  [#1783](https://github.com/NuGet/Home/issues/1783)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-124">Added support for nuget.exe update `-self -Source` https://feed - [#1783](https://github.com/NuGet/Home/issues/1783)</span></span>

* <span data-ttu-id="6fb0e-125">%APPDATA%\NuGet 디렉터리- [#9394](https://github.com/NuGet/Home/issues/9394) 에 여러 구성 파일에 대 한 지원이 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6fb0e-125">Added support for multiple config files in %APPDATA%\NuGet directory - [#9394](https://github.com/NuGet/Home/issues/9394)</span></span>

* <span data-ttu-id="6fb0e-126">DeterministicSourcePaths는 이제 NuGet 원본 패키지를 계정으로 사용 합니다. [#9431](https://github.com/NuGet/Home/issues/9431)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-126">DeterministicSourcePaths now takes NuGet source packages into account - [#9431](https://github.com/NuGet/Home/issues/9431)</span></span>

* <span data-ttu-id="6fb0e-127">INuGetProjectService를 추가 했습니다. GetInstalledPackagesAsync 확장성 API- [#9702](https://github.com/NuGet/Home/issues/9702)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-127">Added INuGetProjectService.GetInstalledPackagesAsync extensibility API - [#9702](https://github.com/NuGet/Home/issues/9702)</span></span>

* <span data-ttu-id="6fb0e-128">솔루션/프로젝트를 요구 하지 않고 대체 폴더를 열거 하는 interop API를 추가 [#9395](https://github.com/NuGet/Home/issues/9395)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-128">Added interop API to enumerate fallback folders without requiring a solution/project - [#9395](https://github.com/NuGet/Home/issues/9395)</span></span>

* <span data-ttu-id="6fb0e-129">`latest`#8808에 대 한 옵션이 추가 됨 `-MSBuildVersion`  -  [](https://github.com/NuGet/Home/issues/8808)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-129">Added `latest` option for `-MSBuildVersion` - [#8808](https://github.com/NuGet/Home/issues/8808)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="6fb0e-130">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="6fb0e-130">Issues fixed in this release</span></span>

<span data-ttu-id="6fb0e-131">**미**</span><span class="sxs-lookup"><span data-stu-id="6fb0e-131">**Bugs:**</span></span>

* <span data-ttu-id="6fb0e-132">Dotnet CLI 복원에서 자격 증명 플러그 인을 시작 하는 경우 `DOTNET_HOST_PATH`  환경 변수가 정의 되어 있지 않으면 시스템 경로에서 DOTNET cli를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fb0e-132">In a dotnet CLI restore, when launching credential plugins, try the dotnet CLI on the system path if the `DOTNET_HOST_PATH`  environment variable is not defined.</span></span><span data-ttu-id="6fb0e-133"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-133"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span></span>

* <span data-ttu-id="6fb0e-134">nuget.exe spec은 #8696 대신 저작권 YYYY의 하드 코드 된 텍스트를 사용 하 여 저작권 태그를 생성 합니다. `$copyright$`  -  [](https://github.com/NuGet/Home/issues/8696)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-134">nuget.exe spec generates a copyright tag with hard-coded text of Copyright YYYY Instead of `$copyright$` - [#8696](https://github.com/NuGet/Home/issues/8696)</span></span>

* <span data-ttu-id="6fb0e-135">어셈블리 이름이 변경 된 경우에는 assemblyinfo 특성을 무시 하는 .csproj의 pack에서 ' 작성자 필요 ' 예외가 throw 됩니다.- [#4234](https://github.com/NuGet/Home/issues/4234) NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="6fb0e-135">NuGet.exe throws exception 'authors required' during pack of a csproj ignoring placeholders and assemblyinfo attributes if the assembly name is changed - [#4234](https://github.com/NuGet/Home/issues/4234)</span></span>

* <span data-ttu-id="6fb0e-136">HttpRequestMessage는 [#8661](https://github.com/NuGet/Home/issues/8661) SocketHttpHandler에서 지원 되지 않는 여러 번 다시 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fb0e-136">HttpRequestMessage gets reused multiple times which is not supported with the SocketHttpHandler - [#8661](https://github.com/NuGet/Home/issues/8661)</span></span>

* <span data-ttu-id="6fb0e-137">5.6.0 preview 3 이상 인덱싱에서 다른 공개 키 토큰을 사용 합니다. [#9481](https://github.com/NuGet/Home/issues/9481)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-137">NuGet.Indexing 5.6.0 preview 3 and later use a different public key token - [#9481](https://github.com/NuGet/Home/issues/9481)</span></span>

* <span data-ttu-id="6fb0e-138">NuGet 패키지를 만드는 동안 TreatWarningsAsErrors 준수- [#7404](https://github.com/NuGet/Home/issues/7404)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-138">Honor TreatWarningsAsErrors during NuGet Package creation - [#7404](https://github.com/NuGet/Home/issues/7404)</span></span>

* <span data-ttu-id="6fb0e-139">[CPVM] 여러 p2p 프로젝트에 대 한 의사 패키지 다운 그레이드- [#9549](https://github.com/NuGet/Home/issues/9549)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-139">[CPVM] Spurious package downgrades for multiple p2p projects  - [#9549](https://github.com/NuGet/Home/issues/9549)</span></span>

* <span data-ttu-id="6fb0e-140">"찾아보기" 탭은 검색 상자를 사용 하 여 왼쪽에 정렬 되지 않습니다. [#9559](https://github.com/NuGet/Home/issues/9559)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-140">The “Browse” tab is not aligned left with search box - [#9559](https://github.com/NuGet/Home/issues/9559)</span></span>

* <span data-ttu-id="6fb0e-141">설치 된 버전은 여러 버전이 설치 된 하나의 패키지 id에 대 한 솔루션 수준 PM UI의 포함 된 아이콘과 일치 하지 않습니다 [#9321](https://github.com/NuGet/Home/issues/9321)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-141">The installed version is inconsistent with the embedded icon in the solution level PM UI for one package id with multiple versions installed - [#9321](https://github.com/NuGet/Home/issues/9321)</span></span>

* <span data-ttu-id="6fb0e-142">누수: PartCreationPolicy (CreationPolicy) SolutionRestoreManager. RestoreOperationLogger- [#9595](https://github.com/NuGet/Home/issues/9595)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-142">Leak: PartCreationPolicy(CreationPolicy.NonShared) NuGet.SolutionRestoreManager.RestoreOperationLogger - [#9595](https://github.com/NuGet/Home/issues/9595)</span></span>

* <span data-ttu-id="6fb0e-143">Op 복원에서 자산 파일을 읽지 않습니다.- [#9693](https://github.com/NuGet/Home/issues/9693)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-143">Avoid reading the assets file in no-op restores - [#9693](https://github.com/NuGet/Home/issues/9693)</span></span>

* <span data-ttu-id="6fb0e-144">NuGet. 프로토콜은 검색에서 버전의 다운로드 횟수를 가져오는 기능을 지원 하지 않습니다 [#9086](https://github.com/NuGet/Home/issues/9086)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-144">NuGet.Protocol does not support getting a version's download count from search - [#9086](https://github.com/NuGet/Home/issues/9086)</span></span>

* <span data-ttu-id="6fb0e-145">JObject [#9719](https://github.com/NuGet/Home/issues/9719) 종속성을 줄여 PackageMetadataResourceV3의 메모리 성능을 향상 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="6fb0e-145">Improve memory performance of PackageMetadataResourceV3 by reducing the JObject dependencies - [#9719](https://github.com/NuGet/Home/issues/9719)</span></span>

<span data-ttu-id="6fb0e-146">**변경 요청 디자인:**</span><span class="sxs-lookup"><span data-stu-id="6fb0e-146">**Design change requests:**</span></span>

* <span data-ttu-id="6fb0e-147">`<owners>`중복 된 경우 요소를 표시 하지 않습니다 [#5134](https://github.com/NuGet/Home/issues/5134)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-147">Suppressed the `<owners>` element when it is redundant - [#5134](https://github.com/NuGet/Home/issues/5134)</span></span>

* <span data-ttu-id="6fb0e-148">ETW 이벤트로 Int추적기 기록- [#9593](https://github.com/NuGet/Home/issues/9593)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-148">Log IntervalTrackers as ETW events - [#9593](https://github.com/NuGet/Home/issues/9593)</span></span>

* <span data-ttu-id="6fb0e-149">CPVM 사용자에 게 기능이 미리 보기 상태 임을 알리기 위해 복원에 정보 메시지를 추가 했습니다 [#9340](https://github.com/NuGet/Home/issues/9340)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-149">Added an informational message on restore to inform CPVM users that the feature is in preview - [#9340](https://github.com/NuGet/Home/issues/9340)</span></span>

* <span data-ttu-id="6fb0e-150">자산 파일에서 솔루션 탐색기 패키지/프로젝트 전이적 종속성 채우기- [#9580](https://github.com/NuGet/Home/issues/9580)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-150">Populate Solution Explorer package/project transitive dependencies from assets file - [#9580](https://github.com/NuGet/Home/issues/9580)</span></span>

* <span data-ttu-id="6fb0e-151">설치 된 패키지 탭에서 패키지 목록의 키를 매길 필요가 없습니다. [#6995](https://github.com/NuGet/Home/issues/6995)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-151">Installed packages tab shouldn't paginate the packages list - [#6995](https://github.com/NuGet/Home/issues/6995)</span></span>

<span data-ttu-id="6fb0e-152">**[이 릴리스에서 해결 된 모든 문제 목록-5.7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**</span><span class="sxs-lookup"><span data-stu-id="6fb0e-152">**[List of all issues fixed in this release - 5.7](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ea77f51ab1a972297db2e92)**</span></span>

### <a name="community-contributions"></a><span data-ttu-id="6fb0e-153">커뮤니티 기여</span><span class="sxs-lookup"><span data-stu-id="6fb0e-153">Community contributions</span></span>

<span data-ttu-id="6fb0e-154">이 NuGet 릴리스를 위해 도움을 주는 모든 참가자에 게 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fb0e-154">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="6fb0e-155">대상</span><span class="sxs-lookup"><span data-stu-id="6fb0e-155">Who</span></span>|<span data-ttu-id="6fb0e-156">Pr</span><span class="sxs-lookup"><span data-stu-id="6fb0e-156">PRs</span></span>|<span data-ttu-id="6fb0e-157">문제</span><span class="sxs-lookup"><span data-stu-id="6fb0e-157">Issues</span></span>|
|----|----|----|
|[<span data-ttu-id="6fb0e-158">campersau</span><span class="sxs-lookup"><span data-stu-id="6fb0e-158">campersau</span></span>](https://github.com/campersau)|<span data-ttu-id="6fb0e-159">[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-159">[3433](https://github.com/NuGet/NuGet.Client/pull/3433), [3120](https://github.com/NuGet/NuGet.Client/pull/3120)</span></span>|<span data-ttu-id="6fb0e-160">NuGet. 프로토콜은 검색에서 버전의 다운로드 횟수를 가져오는 기능을 지원 하지 않습니다 [#9086](https://github.com/NuGet/Home/issues/9086)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-160">NuGet.Protocol does not support getting a version's download count from search - [#9086](https://github.com/NuGet/Home/issues/9086)</span></span> </br><span data-ttu-id="6fb0e-161">HttpRequestMessage는 [#8661](https://github.com/NuGet/Home/issues/8661) SocketHttpHandler에서 지원 되지 않는 여러 번 다시 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6fb0e-161">HttpRequestMessage gets reused multiple times which is not supported with the SocketHttpHandler - [#8661](https://github.com/NuGet/Home/issues/8661)</span></span>|
|[<span data-ttu-id="6fb0e-162">Joseph Musser (jnm2)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-162">Joseph Musser (jnm2)</span></span>](https://github.com/jnm2)|[<span data-ttu-id="6fb0e-163">3241</span><span class="sxs-lookup"><span data-stu-id="6fb0e-163">3241</span></span>](https://github.com/NuGet/NuGet.Client/pull/3241)|<span data-ttu-id="6fb0e-164">`<owners>`중복 된 경우 요소를 표시 하지 않습니다 [#5134](https://github.com/NuGet/Home/issues/5134)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-164">Suppressed the `<owners>` element when it is redundant - [#5134](https://github.com/NuGet/Home/issues/5134)</span></span>|
|[<span data-ttu-id="6fb0e-165">Volodymyr Shkolka (블랙 Gad)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-165">Volodymyr Shkolka (BlackGad)</span></span>](https://github.com/BlackGad)|[<span data-ttu-id="6fb0e-166">3273</span><span class="sxs-lookup"><span data-stu-id="6fb0e-166">3273</span></span>](https://github.com/NuGet/NuGet.Client/pull/3273)|<span data-ttu-id="6fb0e-167">NuGet은 클라이언트 인증서가 필요한 HTTPS 원본에서 복원할 수 없습니다.- [#5773](https://github.com/NuGet/Home/issues/5773)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-167">NuGet cannot restore from HTTPS sources that require Client Certificates - [#5773](https://github.com/NuGet/Home/issues/5773)</span></span>|
|[<span data-ttu-id="6fb0e-168">Marius Unanu (Rezok)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-168">Marius Ungureanu (Therzok)</span></span>](https://github.com/Therzok)|[<span data-ttu-id="6fb0e-169">3357</span><span class="sxs-lookup"><span data-stu-id="6fb0e-169">3357</span></span>](https://github.com/NuGet/NuGet.Client/pull/3357)|<span data-ttu-id="6fb0e-170">HttpSourceAuthenticationHandler SemaphoreSlim 미래 교정- [#9463](https://github.com/NuGet/Home/issues/9463)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-170">HttpSourceAuthenticationHandler SemaphoreSlim future proofing - [#9463](https://github.com/NuGet/Home/issues/9463)</span></span>|
|[<span data-ttu-id="6fb0e-171">Sunner (SuNNjek)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-171">Sunner (SuNNjek)</span></span>](https://github.com/SuNNjek)|[<span data-ttu-id="6fb0e-172">3088</span><span class="sxs-lookup"><span data-stu-id="6fb0e-172">3088</span></span>](https://github.com/NuGet/NuGet.Client/pull/3088)|<span data-ttu-id="6fb0e-173">nuget.exe spec은 #8696 대신 저작권 YYYY의 하드 코드 된 텍스트를 사용 하 여 저작권 태그를 생성 합니다. `$copyright$`  -  [](https://github.com/NuGet/Home/issues/8696)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-173">nuget.exe spec generates a copyright tag with hard-coded text of Copyright YYYY Instead of `$copyright$` - [#8696](https://github.com/NuGet/Home/issues/8696)</span></span>|
|[<span data-ttu-id="6fb0e-174">Olivier Spinelli (olivier-spinelli)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-174">Olivier Spinelli (olivier-spinelli)</span></span>](https://github.com/olivier-spinelli)|[<span data-ttu-id="6fb0e-175">3335</span><span class="sxs-lookup"><span data-stu-id="6fb0e-175">3335</span></span>](https://github.com/NuGet/NuGet.Client/pull/3335)|<span data-ttu-id="6fb0e-176">Dotnet CLI 복원에서 자격 증명 플러그 인을 시작 하는 경우 `DOTNET_HOST_PATH`  환경 변수가 정의 되어 있지 않으면 시스템 경로에서 DOTNET cli를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="6fb0e-176">In a dotnet CLI restore, when launching credential plugins, try the dotnet CLI on the system path if the `DOTNET_HOST_PATH`  environment variable is not defined.</span></span><span data-ttu-id="6fb0e-177"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-177"> - [#7438](https://github.com/NuGet/Home/issues/7438)</span></span>|
|[<span data-ttu-id="6fb0e-178">goyzhang</span><span class="sxs-lookup"><span data-stu-id="6fb0e-178">goyzhang</span></span>](https://github.com/goyzhang)|[<span data-ttu-id="6fb0e-179">3370</span><span class="sxs-lookup"><span data-stu-id="6fb0e-179">3370</span></span>](https://github.com/NuGet/NuGet.Client/pull/3370)|<span data-ttu-id="6fb0e-180">`latest`#8808에 대 한 옵션이 추가 됨 `-MSBuildVersion`  -  [](https://github.com/NuGet/Home/issues/8808)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-180">Added `latest` option for `-MSBuildVersion` - [#8808](https://github.com/NuGet/Home/issues/8808)</span></span>|

## <a name="summary-whats-new-in-571"></a><span data-ttu-id="6fb0e-181">요약: 5.7.1의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="6fb0e-181">Summary: What's New in 5.7.1</span></span>

* <span data-ttu-id="6fb0e-182">Nupkg 파일을 확장 하 여 설치 소스를 포함 합니다.- [#10354](https://github.com/NuGet/Home/issues/10354)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-182">Extend the .nupkg.metadata file to include the installation source - [#10354](https://github.com/NuGet/Home/issues/10354)</span></span>

* <span data-ttu-id="6fb0e-183">복원 하는 동안 로그 패키지 contenthash (추출 중)- [#10384](https://github.com/NuGet/Home/issues/10384)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-183">Log package contenthash during restore logging (during extraction) - [#10384](https://github.com/NuGet/Home/issues/10384)</span></span>

* <span data-ttu-id="6fb0e-184">정상적으로 복원 하는 경우 패키지를 복원할 원본- [#10461](https://github.com/NuGet/Home/issues/10461)</span><span class="sxs-lookup"><span data-stu-id="6fb0e-184">When restoring at normal verbosity, log which source a package is being restored from - [#10461](https://github.com/NuGet/Home/issues/10461)</span></span>

<span data-ttu-id="6fb0e-185">**[이 릴리스에서 수정 된 모든 문제 목록-5.7.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f5724f84579cc29a79ee)**</span><span class="sxs-lookup"><span data-stu-id="6fb0e-185">**[List of all issues fixed in this release - 5.7.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=6075f5724f84579cc29a79ee)**</span></span>

<span data-ttu-id="6fb0e-186">**[이 릴리스의 커밋 목록-5.7.1](https://github.com/NuGet/NuGet.Client/compare/80512866a2c127e52ce3e86fd803fff77e9b9b52...5.7.1.4)**</span><span class="sxs-lookup"><span data-stu-id="6fb0e-186">**[List of commits in this release - 5.7.1](https://github.com/NuGet/NuGet.Client/compare/80512866a2c127e52ce3e86fd803fff77e9b9b52...5.7.1.4)**</span></span>
