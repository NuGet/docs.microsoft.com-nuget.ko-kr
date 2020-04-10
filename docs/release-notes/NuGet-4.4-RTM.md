---
title: NuGet 4.4 RTM 릴리스 정보
description: NuGet 4.3 RTM에 대한 릴리스 정보(알려진 문제, 버그 수정, 추가된 기능 및 DCR 포함).
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3be24a86cc92c4e6d07fcae1dc625a150f28d7b4
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498692"
---
# <a name="nuget-44-release-notes"></a><span data-ttu-id="3f8c0-103">NuGet 4.4 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="3f8c0-103">NuGet 4.4 Release Notes</span></span>

<span data-ttu-id="3f8c0-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes)는 NuGet 4.4 RTM과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f8c0-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="summary-whats-new-in-440"></a><span data-ttu-id="3f8c0-105">요약: 4.4.0의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="3f8c0-105">Summary: What's New in 4.4.0</span></span>

## <a name="summary-whats-new-in-442"></a><span data-ttu-id="3f8c0-106">요약: 4.4.2의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="3f8c0-106">Summary: What's New in 4.4.2</span></span>

* <span data-ttu-id="3f8c0-107">보안 수정: ~/.nuget 내에서 만든 파일에 대한 권한이 열려 있습니다. [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-107">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-443"></a><span data-ttu-id="3f8c0-108">요약: 4.4.3의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="3f8c0-108">Summary: What's New in 4.4.3</span></span>

* <span data-ttu-id="3f8c0-109">보안 수정: NUPKG 내부에 있는 파일에는 NUPKG 디렉터리 위의 상대 경로가 포함될 수 있습니다. [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="3f8c0-110">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="3f8c0-110">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="3f8c0-111">.NET Framework 및 NuGet이 포함된 .NET Standard 2.0 관련 문제</span><span class="sxs-lookup"><span data-stu-id="3f8c0-111">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="3f8c0-112">.NET Standard 및 해당 도구는 .NET Framework 4.6.1을 대상으로 하는 프로젝트에서 .NET Standard 2.0 또는 이전 버전을 대상으로 하는 NuGet 패키지 및 프로젝트를 사용할 수 있도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8c0-112">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="3f8c0-113">[이 문서](https://github.com/dotnet/standard/issues/481)에서는 해당 시나리오와 관련된 문제, 문제를 해결하기 위한 계획 및 현재의 도구 상태로 배포할 수 있는 해결 방법을 요약하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8c0-113">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="3f8c0-114">패키지 관리자 콘솔을 사용하는 동안 'Enter' 키가 작동하지 않을 수 있음</span><span class="sxs-lookup"><span data-stu-id="3f8c0-114">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="3f8c0-115">문제점</span><span class="sxs-lookup"><span data-stu-id="3f8c0-115">Issue</span></span>

<span data-ttu-id="3f8c0-116">경우에 따라 패키지 관리자 콘솔에서 Enter 키가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8c0-116">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="3f8c0-117">이런 경우 수정 진행 상황을 확인하고 재현 단계에 대해 도움이 되는 추가 정보를 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="3f8c0-117">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="3f8c0-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-118">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="3f8c0-119">해결 방법</span><span class="sxs-lookup"><span data-stu-id="3f8c0-119">Workaround</span></span>

<span data-ttu-id="3f8c0-120">Visual Studio를 다시 시작하고 솔루션을 열기 전에 PMC를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="3f8c0-120">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="3f8c0-121">또는 `project.lock.json`을 삭제하고 다시 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8c0-121">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="3f8c0-122">NuGet 패키지 관리자를 사용하여 DotNetCLITools를 보거나 추가 또는 업데이트할 수 없음</span><span class="sxs-lookup"><span data-stu-id="3f8c0-122">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="3f8c0-123">문제점</span><span class="sxs-lookup"><span data-stu-id="3f8c0-123">Issue</span></span>

<span data-ttu-id="3f8c0-124">NuGet 패키지 관리자는 DotNetCLITools 추가/업데이트를 표시하지 않으며 허용하지도 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8c0-124">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="3f8c0-125">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="3f8c0-125">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="3f8c0-126">해결 방법</span><span class="sxs-lookup"><span data-stu-id="3f8c0-126">Workaround</span></span>

<span data-ttu-id="3f8c0-127">프로젝트 파일에서 DotNetCLIToolReferences를 수동으로 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8c0-127">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="3f8c0-128">대상 프레임워크 버전의 대상을 변경하면 불완전한 IntelliSense가 발생할 수 있음</span><span class="sxs-lookup"><span data-stu-id="3f8c0-128">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="3f8c0-129">문제점</span><span class="sxs-lookup"><span data-stu-id="3f8c0-129">Issue</span></span>

<span data-ttu-id="3f8c0-130">Visual Studio에서 대상 프레임워크 버전의 대상을 변경하면 불완전한 IntelliSense가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8c0-130">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="3f8c0-131">이 문제는 PackageReferences를 패키지 관리자 형식으로 사용하는 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8c0-131">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="3f8c0-132">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="3f8c0-132">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="3f8c0-133">해결 방법</span><span class="sxs-lookup"><span data-stu-id="3f8c0-133">Workaround</span></span>

<span data-ttu-id="3f8c0-134">수동 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8c0-134">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="3f8c0-135">잘못된 시그니처와 함께 어셈블리가 포함된 .NET Core 프로젝트의 패키지는 무한 복원 루프를 트리거할 수 있음</span><span class="sxs-lookup"><span data-stu-id="3f8c0-135">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="3f8c0-136">문제점</span><span class="sxs-lookup"><span data-stu-id="3f8c0-136">Issue</span></span>

<span data-ttu-id="3f8c0-137">경우에 따라 잘못된 시그니처와 함께 어셈블리가 포함된 패키지를 사용하거나 패키지 버전이 'DateTime' 표시기로 설정된 경우 패키지 자동 복원이 무한 루프로 실행됩니다(dotnet/project-system#1457).</span><span class="sxs-lookup"><span data-stu-id="3f8c0-137">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="3f8c0-138">해결 방법</span><span class="sxs-lookup"><span data-stu-id="3f8c0-138">Workaround</span></span>

<span data-ttu-id="3f8c0-139">지금은 해결 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8c0-139">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="3f8c0-140">NuGet 4.4 RTM 기간에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="3f8c0-140">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="3f8c0-141">[NuGet 4.3 RTM 릴리스 정보](../release-notes/nuget-4.3-RTM.md) - NuGet 4.3 RTM에서 수정된 모든 문제를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8c0-141">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="3f8c0-142">기능</span><span class="sxs-lookup"><span data-stu-id="3f8c0-142">Features</span></span>

- <span data-ttu-id="3f8c0-143">PMC 및 NuGet PM UI 시나리오에서 경량 솔루션 로드를 지원합니다. - [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-143">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="3f8c0-144">msbuild pack 대상에는 자체적으로 사용자 대상을 실행하기 위한 공용 후크가 있어야 합니다. - [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-144">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="3f8c0-145">기능: nuget install에 dependencyVersion 스위치를 추가할 수 있습니다. - [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-145">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="3f8c0-146">uap10.0.TODO.0은 NuGet용 .NET Standard 2.0에 매핑되어야 합니다. - [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-146">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="3f8c0-147">msbuild /t:restore에서 Visual Studio Build Tools SKU를 지원합니다. - [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-147">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="3f8c0-148">복원 중에 .NET Standard 2.0에 대한 .NET 4.6.1 지원이 필요하지만 설치되지 않은 경우 오류를 생성합니다. - [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-148">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="3f8c0-149">패키지 ID 접두사 예약 클라이언트 UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-149">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="3f8c0-150">지역화된 NuGet 구성 요소를 제공하여 dotnet.exe 지역화를 지원합니다. - [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-150">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="3f8c0-151">버그</span><span class="sxs-lookup"><span data-stu-id="3f8c0-151">Bugs</span></span>

- <span data-ttu-id="3f8c0-152">다른 프로젝트 경로 대/소문자 구분 기능으로 인해 복원 시 PackageReferences가 손실될 수 있습니다. - [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-152">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="3f8c0-153">경고 번호가 있는 오류 코드를 오류 범위로 이동해야 합니다. - [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-153">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="3f8c0-154">.NET Standard 버전이 대상 프레임워크와 호환되지 않는 것으로 인식되는 경우 잘못 해석된 오류가 발생합니다. - [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-154">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="3f8c0-155">혼동스러운 라이선스가 있는 테스트 파일 - [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-155">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="3f8c0-156">라이선스 헤더가 누락된 EndToEnd 테스트 템플릿 - [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-156">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="3f8c0-157">packages.config restore에서 NU1000 오류를 표시합니다. - [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-157">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="3f8c0-158">nuget.exe install에는 Mono에서 DisableParallelProcessing이 있어야 합니다. - [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-158">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="3f8c0-159">nuget.exe install에서 캐싱을 사용하지 않도록 잘못 설정합니다. - [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-159">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="3f8c0-160">VS 옵션에서 복원을 사용하지 않도록 설정되어 있을 때 packages.config에 대한 restore 명령을 실행하면 잘못된 메시지가 표시됩니다. - [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-160">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="3f8c0-161">VS 옵션에서 복원을 사용하지 않도록 설정되어 있을 때 restore 명령을 실행하면 혼동스러운 메시지가 표시됩니다. - [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-161">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="3f8c0-162">버전 메타데이터가 누락되면 GetRestoreDotnetCliToolsTask가 실패합니다. - [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-162">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="3f8c0-163">dotnet</span><span class="sxs-lookup"><span data-stu-id="3f8c0-163">dotnet</span></span>
  - <span data-ttu-id="3f8c0-164">dotnetcore add package가 csproj에서 빈 줄을 지울 수 있습니다. - [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-164">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="3f8c0-165">NuGet.Config의 자격 증명 설정의 원본 이름은 대/소문자를 구분합니다. - [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-165">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="3f8c0-166">GeneratePackageOnBuild를 사용하면 패키지의 전체 기록이 삭제되었습니다. - [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-166">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="3f8c0-167">복원은 mono.cecil 또는 semver 패키지를 복원하지 않지만 다른 모든 패키지는 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f8c0-167">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="3f8c0-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-168"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="3f8c0-169">오류 및 경고 - 원본을 사용할 수 없는 경우 잘못된 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3f8c0-169">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="3f8c0-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-170">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="3f8c0-171">[DesignConsistency] NuGet 설치 상태 텍스트가 현재 어두운 테마에서 올바르게 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f8c0-171">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="3f8c0-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-172"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="3f8c0-173">모든 프로젝트에 대한 솔루션 업데이트/설치 시의 패키지 업데이트 - [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-173">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="3f8c0-174">dotnet</span><span class="sxs-lookup"><span data-stu-id="3f8c0-174">dotnet</span></span>
  - <span data-ttu-id="3f8c0-175">dotnetcore pack은 TargetFramework와 TargetFrameworks에 따라 다르게 동작합니다. - [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-175">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="3f8c0-176">Tools 폴더에 포함된 DLL에서 경고를 throw합니다. - [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-176">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="3f8c0-177">NuGet.ContentModel은 문자열 연산에 너무 많은 메모리를 사용합니다. - [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-177">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="3f8c0-178">RuntimeEnvironmentHelper.IsLinux에서 OSX에 대해 true를 반환합니다. - [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-178">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="3f8c0-179">'dotnet pack'은 nuspec을 obj\Debug 대신 obj에 넣습니다. - [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-179">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="3f8c0-180">매우 느린 NuGet 패키지 업그레이드 - [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-180">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="3f8c0-181">CPS가 복원에서 LSL(경량 솔루션 복원)이 설정되지 않은 큰 솔루션과 동기화되지 않습니다. - [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-181">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="3f8c0-182">SemVer 2.0 - 제공된 버전(3.5.0-rtm-1938)의 nuget pack에서 메타데이터를 무시합니다. - [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-182">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="3f8c0-183">버전 번호 및 ExcludeVersion 플래그가 포함된 nuget.exe(3.0 이상) 설치 패키지에서 패키지를 최신 버전으로 업데이트하지 않습니다. - [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-183">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="3f8c0-184">최상위 패키지가 제약 조건을 위반할 때 Project.json 복원에서 경고해야 합니다. - [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-184">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="3f8c0-185">install 명령의 -ConfigFile에서 사용자 지정 구성을 설정하지 않습니다. - [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-185">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="3f8c0-186">nuget.exe install에서 '-DisableParallelProcessing' 스위치가 적용되지 않습니다. - [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-186">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="3f8c0-187">DotNet.exe 또는 msbuild.exe에서 사용하도록 설정되지 않은 원본을 계속 사용합니다. - [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-187">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="3f8c0-188">LSL 시나리오에서 중단을 수정합니다. - [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-188">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="3f8c0-189">DCR</span><span class="sxs-lookup"><span data-stu-id="3f8c0-189">DCRs</span></span>

- <span data-ttu-id="3f8c0-190">nuget.exe install에서 TargetFramework를 지원합니다. - [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-190">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="3f8c0-191">서로 다른 msbuild task UserAgent 문자열(netcore 및 desktop msbuild)을 추가합니다. - [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-191">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="3f8c0-192">PackagePathResolver.GetPackageDirectoryName은 virtual이어야 합니다. - [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-192">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="3f8c0-193">[DesignConsistency] NuGet 패키지 추가 시 혼동스러운 메시지가 표시됩니다. - [#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-193">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="3f8c0-194">[경고 및 오류] NoWarn이 P2P 참조를 통해 과도하게 이동하지 않습니다. - [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-194">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="3f8c0-195">경량 솔루션 로드: PM UI, PMC 및 IV에 대한 공통 핵심 - - [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-195">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="3f8c0-196">경량 솔루션 로드: 지원 - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-196">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="3f8c0-197">Visual Studio에서 트리거하는 사전 복원 MSBuild 대상에 대한 지원을 추가합니다. - [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-197">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="3f8c0-198">BeforeTargets를 사용하여 참조할 수 있는 공용 대상을 NuGet.targets에 추가합니다. - [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-198">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="3f8c0-199">팩 대상은 빌드 작업으로 contentFiles를 올바르게 만들 수 없습니다. - [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-199">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="3f8c0-200">RestoreOperationLogger.Do에서 스레드 풀 스레드를 차단합니다. - [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-200">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="3f8c0-201">Docs</span><span class="sxs-lookup"><span data-stu-id="3f8c0-201">Docs</span></span>

- <span data-ttu-id="3f8c0-202">Install 명령의 DependencyVersion 및 Framework 플래그에 대한 문서 - [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-202">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="3f8c0-203">NuGet 경고 및 오류 관련 문서에 대한 업데이트 - [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="3f8c0-203">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="3f8c0-204">4\.4 RTM에서 수정된 GitHub 문제에 대한 링크</span><span class="sxs-lookup"><span data-stu-id="3f8c0-204">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="3f8c0-205">문제 목록 1</span><span class="sxs-lookup"><span data-stu-id="3f8c0-205">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="3f8c0-206">문제 목록 2</span><span class="sxs-lookup"><span data-stu-id="3f8c0-206">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="3f8c0-207">문제 목록 3</span><span class="sxs-lookup"><span data-stu-id="3f8c0-207">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
