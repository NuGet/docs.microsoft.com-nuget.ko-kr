---
title: NuGet 4.7 RTM 릴리스 정보
description: NuGet 4.7.0에 대한 릴리스 정보(알려진 문제, 버그 수정, 추가된 기능 및 DCR 포함)
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: f23cc2973fa6370d9b7513d415fd8151b822c104
ms.sourcegitcommit: 8f0bb8bb9cb91d27d660963ed9b0f32642f420fe
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34225972"
---
# <a name="nuget-47-rtm-release-notes"></a><span data-ttu-id="0aa54-103">NuGet 4.7 RTM 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="0aa54-103">NuGet 4.7 RTM Release Notes</span></span>

<span data-ttu-id="0aa54-104">[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes)는 [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe)과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0aa54-104">[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-this-release"></a><span data-ttu-id="0aa54-105">요약: 이번 릴리스의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="0aa54-105">Summary: What's New in this Release</span></span>

* <span data-ttu-id="0aa54-106">[리포지토리 서명 패키지](https://github.com/NuGet/Home/wiki/Repository-Signatures)를 사용하도록 패키지 서명을 확대했습니다.</span><span class="sxs-lookup"><span data-stu-id="0aa54-106">We have augemented package signing to enable [Repository Signed packages](https://github.com/NuGet/Home/wiki/Repository-Signatures)</span></span>

* <span data-ttu-id="0aa54-107">Visual Studio 버전 15.7에서는 [PackageReference를 사용하기 위해 packages.config 형식을 사용하는 기존 프로젝트를 마이그레이션하는 ](https://docs.microsoft.com/en-us/nuget/reference/migrate-packages-config-to-package-reference) 기능을 대신 도입했습니다.</span><span class="sxs-lookup"><span data-stu-id="0aa54-107">With Visual Studio Version 15.7, we have introduced the capability to [migrate existing projects that use the packages.config format to use PackageReference](https://docs.microsoft.com/en-us/nuget/reference/migrate-packages-config-to-package-reference) instead.</span></span>

## <a name="known-issues"></a><span data-ttu-id="0aa54-108">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="0aa54-108">Known issues</span></span>

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a><span data-ttu-id="0aa54-109">`Migrate packages.config to PackageReference...` 옵션을 오른쪽 클릭 상황에 맞는 메뉴에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0aa54-109">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span>

#### <a name="issue"></a><span data-ttu-id="0aa54-110">문제</span><span class="sxs-lookup"><span data-stu-id="0aa54-110">Issue</span></span>

<span data-ttu-id="0aa54-111">프로젝트를 처음 열면 NuGet 작업이 수행될 때까지 NuGet을 초기화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0aa54-111">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="0aa54-112">이로 인해 마이그레이션 옵션이 `packages.config` 또는 `References`의 오른쪽 클릭 상황에 맞는 메뉴에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0aa54-112">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span>

#### <a name="workaround"></a><span data-ttu-id="0aa54-113">해결 방법</span><span class="sxs-lookup"><span data-stu-id="0aa54-113">Workaround</span></span>

<span data-ttu-id="0aa54-114">다음 NuGet 작업 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="0aa54-114">Peform any one of the following NuGet actions:</span></span>
* <span data-ttu-id="0aa54-115">패키지 관리자 UI 열기 - `References`를 마우스 오른쪽 단추로 클릭하고 `Manage NuGet Packages...`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0aa54-115">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span>
* <span data-ttu-id="0aa54-116">패키지 관리자 콘솔 열기 - `Tools > NuGet Package Manager`에서 `Package Manager Console`을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0aa54-116">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span>
* <span data-ttu-id="0aa54-117">NuGet 복원 실행 - 솔루션 탐색기에서 솔루션 노드를 마우스 오른쪽 단추로 클릭하고 `Restore NuGet Packages`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0aa54-117">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span>
* <span data-ttu-id="0aa54-118">NuGet 복원을 트리거하는 프로젝트 빌드</span><span class="sxs-lookup"><span data-stu-id="0aa54-118">Build the project which also triggers NuGet restore</span></span>

<span data-ttu-id="0aa54-119">이제 마이그레이션 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0aa54-119">You should now be able to see the migration option.</span></span> <span data-ttu-id="0aa54-120">이 옵션은 지원되지 않으며 ASP.NET 및 C++ 프로젝트 형식에 대해 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0aa54-120">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="0aa54-121">.NET Framework 및 NuGet이 포함된 .NET Standard 2.0 관련 문제</span><span class="sxs-lookup"><span data-stu-id="0aa54-121">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span>

<span data-ttu-id="0aa54-122">.NET Standard 및 해당 도구는 .NET Framework 4.6.1을 대상으로 하는 프로젝트에서 .NET Standard 2.0 또는 이전 버전을 대상으로 하는 NuGet 패키지 및 프로젝트를 사용할 수 있도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0aa54-122">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="0aa54-123">[이 문서](https://github.com/dotnet/standard/issues/481)에서는 해당 시나리오와 관련된 문제, 문제를 해결하기 위한 계획 및 현재의 도구 상태로 배포할 수 있는 해결 방법을 요약하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0aa54-123">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

## <a name="top-issues-fixed-in-this-release"></a><span data-ttu-id="0aa54-124">이번 릴리스에서 해결된 주요 문제</span><span class="sxs-lookup"><span data-stu-id="0aa54-124">Top issues fixed in this release</span></span>

### <a name="bugs"></a><span data-ttu-id="0aa54-125">버그</span><span class="sxs-lookup"><span data-stu-id="0aa54-125">Bugs</span></span>

* <span data-ttu-id="0aa54-126">NuGet이 .NET Core 프로젝트 시스템(새 회귀)에서 교착 상태로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="0aa54-126">NuGet runs into a deadlock in .Net Core project system (new regression).</span></span><span data-ttu-id="0aa54-127"> - [#6733](https://github.com/NuGet/Home/issues/6733)</span><span class="sxs-lookup"><span data-stu-id="0aa54-127"> - [#6733](https://github.com/NuGet/Home/issues/6733)</span></span>
* <span data-ttu-id="0aa54-128">팩: TfmSpecificPackageFile이 와일드카드 사용 경로와 함께 사용되는 경우 PackagePath가 잘못 구성됨 - [#6726](https://github.com/NuGet/Home/issues/6726)</span><span class="sxs-lookup"><span data-stu-id="0aa54-128">Pack: PackagePath is constructed incorrectly if TfmSpecificPackageFile is used with globbing paths - [#6726](https://github.com/NuGet/Home/issues/6726)</span></span>
* <span data-ttu-id="0aa54-129">팩: ispackable이 명시적으로 설정되지 않으면 Web API 프로젝트에서 패키지를 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0aa54-129">Pack: web api project cannot create package unless ispackable is explicitly set.</span></span><span data-ttu-id="0aa54-130"> - [#6156](https://github.com/NuGet/Home/issues/6156)</span><span class="sxs-lookup"><span data-stu-id="0aa54-130"> - [#6156](https://github.com/NuGet/Home/issues/6156)</span></span>
* <span data-ttu-id="0aa54-131">VS UI 및 PMC에서 새 패키지를 표시하는 데 30분이 걸림(nuget.exe는 바로 표시됨) - [#6657](https://github.com/NuGet/Home/issues/6657)</span><span class="sxs-lookup"><span data-stu-id="0aa54-131">VS UI and PMC take 30min to see new package (nuget.exe sees it right away) - [#6657](https://github.com/NuGet/Home/issues/6657)</span></span>
* <span data-ttu-id="0aa54-132">서명: SignatureUtility.GetCertificateChain(...)이 모든 체인 상태를 확인하지 않음 - [#6565](https://github.com/NuGet/Home/issues/6565)</span><span class="sxs-lookup"><span data-stu-id="0aa54-132">Signing:  SignatureUtility.GetCertificateChain(...) does not check all chain statuses - [#6565](https://github.com/NuGet/Home/issues/6565)</span></span>
* <span data-ttu-id="0aa54-133">서명: DER GeneralizedTime 처리 개선 - [#6564](https://github.com/NuGet/Home/issues/6564)</span><span class="sxs-lookup"><span data-stu-id="0aa54-133">Signing:  improve DER GeneralizedTime handling - [#6564](https://github.com/NuGet/Home/issues/6564)</span></span>
* <span data-ttu-id="0aa54-134">서명: 변경된 패키지를 설치할 때 VS가 NU3002 오류를 표시하지 않음 - [#6337](https://github.com/NuGet/Home/issues/6337)</span><span class="sxs-lookup"><span data-stu-id="0aa54-134">Signing: VS does not show a NU3002 error when installing a tampered package - [#6337](https://github.com/NuGet/Home/issues/6337)</span></span>
* <span data-ttu-id="0aa54-135">lockFile.GetLibrary가 대소문자를 구분함 - [#6500](https://github.com/NuGet/Home/issues/6500)</span><span class="sxs-lookup"><span data-stu-id="0aa54-135">lockFile.GetLibrary is case sensitive - [#6500](https://github.com/NuGet/Home/issues/6500)</span></span>
* <span data-ttu-id="0aa54-136">설치/업데이트 복원 코드 및 복원 코드 경로가 일치하지 않음 - [#3471](https://github.com/NuGet/Home/issues/3471)</span><span class="sxs-lookup"><span data-stu-id="0aa54-136">Install/update restore code and Restore code paths are not consistent - [#3471](https://github.com/NuGet/Home/issues/3471)</span></span>
* <span data-ttu-id="0aa54-137">솔루션 패키지 관리자 버전 콤보 상자가 키보드를 통해 구분 기호를 선택할 수 있음 - [#2606](https://github.com/NuGet/Home/issues/2606)</span><span class="sxs-lookup"><span data-stu-id="0aa54-137">Solution PackageManager Version ComboBox can select separator via keyboard - [#2606](https://github.com/NuGet/Home/issues/2606)</span></span>
* <span data-ttu-id="0aa54-138">소스에 대해 서비스 인덱스를 로드할 수 없음 `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException: 응답 상태 코드가 성공을 나타내지 않음: 403(사용할 수 없음) - [#2530](https://github.com/NuGet/Home/issues/2530)</span><span class="sxs-lookup"><span data-stu-id="0aa54-138">Unable to load the service index for source `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException: Response status code does not indicate success: 403 (Forbidden) - [#2530](https://github.com/NuGet/Home/issues/2530)</span></span>

### <a name="dcrs"></a><span data-ttu-id="0aa54-139">DCR</span><span class="sxs-lookup"><span data-stu-id="0aa54-139">DCRs</span></span>

* <span data-ttu-id="0aa54-140">요청 간 상관 관계를 지정하기 위해 X-NuGet-Session-Id 헤더를 내보냄 [기능 제안] - [#5330](https://github.com/NuGet/Home/issues/5330)</span><span class="sxs-lookup"><span data-stu-id="0aa54-140">Emit X-NuGet-Session-Id header to correlate across requests [feature proposal] - [#5330](https://github.com/NuGet/Home/issues/5330)</span></span>
* <span data-ttu-id="0aa54-141">IV API를 통해 Visual Studio에서 실행 중인 복원 작업 실행을 대기하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="0aa54-141">Expose a way to wait on running restore operation running in Visual Studio via IVs apis.</span></span><span data-ttu-id="0aa54-142"> - [#6029](https://github.com/NuGet/Home/issues/6029)</span><span class="sxs-lookup"><span data-stu-id="0aa54-142"> - [#6029](https://github.com/NuGet/Home/issues/6029)</span></span>
* <span data-ttu-id="0aa54-143">NuGet.exe -NoServiceEndpoint가 서비스 URL 접미사를 추가하지 못하게 함 - [#6586](https://github.com/NuGet/Home/issues/6586)</span><span class="sxs-lookup"><span data-stu-id="0aa54-143">NuGet.exe -NoServiceEndpoint will avoid appending service url suffix - [#6586](https://github.com/NuGet/Home/issues/6586)</span></span>
* <span data-ttu-id="0aa54-144">정보 버전에 커밋 해시 추가 - [#6492](https://github.com/NuGet/Home/issues/6492)</span><span class="sxs-lookup"><span data-stu-id="0aa54-144">add commit hash to informational version - [#6492](https://github.com/NuGet/Home/issues/6492)</span></span>
* <span data-ttu-id="0aa54-145">서명: 리포지토리 서명/연대 서명 제거 사용 - [#6646](https://github.com/NuGet/Home/issues/6646)</span><span class="sxs-lookup"><span data-stu-id="0aa54-145">Signing:  enable removal of repository signature/countersignature - [#6646](https://github.com/NuGet/Home/issues/6646)</span></span>
* <span data-ttu-id="0aa54-146">서명: 리포지토리 서명/연대 서명 제거용 API - [#6589](https://github.com/NuGet/Home/issues/6589)</span><span class="sxs-lookup"><span data-stu-id="0aa54-146">Signing:  API for stripping repository signature/countersignature - [#6589](https://github.com/NuGet/Home/issues/6589)</span></span>
* <span data-ttu-id="0aa54-147">VS에서 소스 정보 로그 - [#6527](https://github.com/NuGet/Home/issues/6527)</span><span class="sxs-lookup"><span data-stu-id="0aa54-147">Log source information in VS - [#6527](https://github.com/NuGet/Home/issues/6527)</span></span>
* <span data-ttu-id="0aa54-148">TFM 및 RID에서만 /tools를 필터링하여 설정 XML을 /tools 폴더에 넣을 수 있음 - [#6197](https://github.com/NuGet/Home/issues/6197)</span><span class="sxs-lookup"><span data-stu-id="0aa54-148">Filter /tools on only TFM and RID, so the settings XML can be put in /tools folder - [#6197](https://github.com/NuGet/Home/issues/6197)</span></span>
* <span data-ttu-id="0aa54-149">팩 명령이 .로 시작하는 파일을 제외할 때 경고함</span><span class="sxs-lookup"><span data-stu-id="0aa54-149">Warn when Pack command excludes a file that starts with .</span></span><span data-ttu-id="0aa54-150">  - [#3308](https://github.com/NuGet/Home/issues/3308)</span><span class="sxs-lookup"><span data-stu-id="0aa54-150">  - [#3308](https://github.com/NuGet/Home/issues/3308)</span></span>

[<span data-ttu-id="0aa54-151">이번 릴리스에서 수정된 모든 문제 목록</span><span class="sxs-lookup"><span data-stu-id="0aa54-151">List of all issues fixed in this release</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
