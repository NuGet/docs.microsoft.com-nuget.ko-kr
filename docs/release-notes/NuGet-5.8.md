---
title: NuGet 5.8 릴리스 정보
description: 새 기능, 버그 수정 및 Ecrs를 비롯 한 NuGet 5.8에 대 한 릴리스 정보입니다.
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: 550971d77ed4b15129fdc58fef95e0cceda8d8d1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776171"
---
# <a name="nuget-58-release-notes"></a><span data-ttu-id="acd5d-103">NuGet 5.8 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="acd5d-103">NuGet 5.8 Release Notes</span></span>

<span data-ttu-id="acd5d-104">NuGet 배포 차량:</span><span class="sxs-lookup"><span data-stu-id="acd5d-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="acd5d-105">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="acd5d-105">NuGet version</span></span> | <span data-ttu-id="acd5d-106">Visual Studio 버전에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="acd5d-106">Available in Visual Studio version</span></span> | <span data-ttu-id="acd5d-107">.NET SDK에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="acd5d-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="acd5d-108">**5.8**</span><span class="sxs-lookup"><span data-stu-id="acd5d-108">**5.8**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="acd5d-109">Visual Studio 2019 버전 16.8</span><span class="sxs-lookup"><span data-stu-id="acd5d-109">Visual Studio 2019 version 16.8</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="acd5d-110">[5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="acd5d-110">[5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |
| [<span data-ttu-id="acd5d-111">**5.8.1**</span><span class="sxs-lookup"><span data-stu-id="acd5d-111">**5.8.1**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="acd5d-112">Visual Studio 2019 버전 16.8.4</span><span class="sxs-lookup"><span data-stu-id="acd5d-112">Visual Studio 2019 version 16.8.4</span></span>](https://visualstudio.microsoft.com/downloads/) | |

<span data-ttu-id="acd5d-113"><sup>1</sup> .net Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨</span><span class="sxs-lookup"><span data-stu-id="acd5d-113"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="acd5d-114">Visual Studio 16.8, MSBuild 16.8 및 .NET 5.0에는 NuGet.exe 5.8 이상이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd5d-114">Visual Studio 16.8, MSBuild 16.8, and .NET 5.0 require NuGet.exe 5.8 or later.</span></span>


## <a name="summary-whats-new-in-58"></a><span data-ttu-id="acd5d-115">요약: 5.8의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="acd5d-115">Summary: What's New in 5.8</span></span>
<span data-ttu-id="acd5d-116">🎉 **.net 5.0를 대상으로 하는 NuGet 패키지에 대 한 전체 작성 및 복원 지원을 제공 하기 위한 첫 번째 릴리스입니다** 🎉</span><span class="sxs-lookup"><span data-stu-id="acd5d-116">🎉 **This is the first release to offer full authoring and restoring support for NuGet packages targeting .NET 5.0** 🎉</span></span>

* <span data-ttu-id="acd5d-117">Mmap/Createfilemapping에서 [#9807](https://github.com/NuGet/Home/issues/9807) 를 사용 하 여 nupkg 추출 가속화</span><span class="sxs-lookup"><span data-stu-id="acd5d-117">Speed up nupkg extraction using mmap/CreateFileMapping - [#9807](https://github.com/NuGet/Home/issues/9807)</span></span>

* <span data-ttu-id="acd5d-118">패키지 관리자 UI 패키지 정보 창에서 패키지 취약성 세부 정보 표시- [#9850](https://github.com/NuGet/Home/issues/9850)</span><span class="sxs-lookup"><span data-stu-id="acd5d-118">Display package vulnerability details in the Package Manager UI package details pane - [#9850](https://github.com/NuGet/Home/issues/9850)</span></span>

* <span data-ttu-id="acd5d-119">새 명령으로 서명 된 NuGet 패키지 확인 [`dotnet nuget verify`](/dotnet/core/tools/dotnet-nuget-verify) - [#8051](https://github.com/NuGet/Home/issues/8051)</span><span class="sxs-lookup"><span data-stu-id="acd5d-119">Verify signed NuGet packages with the new [`dotnet nuget verify`](/dotnet/core/tools/dotnet-nuget-verify) command - [#8051](https://github.com/NuGet/Home/issues/8051)</span></span>

* <span data-ttu-id="acd5d-120">[`dotnet add package`](/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples)`--prerelease`시험판 버전을 포함 하 여 최신 버전의 패키지를 추가 하는 옵션을 지원 [#4699](https://github.com/NuGet/Home/issues/4699)</span><span class="sxs-lookup"><span data-stu-id="acd5d-120">[`dotnet add package`](/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) supports `--prerelease` option to add the latest version of a package, including prerelease versions - [#4699](https://github.com/NuGet/Home/issues/4699)</span></span>

* <span data-ttu-id="acd5d-121">CLI에서 명령을 사용 하 여 패키지 검색 [`nuget.exe search`](../reference/cli-reference/cli-ref-search.md) [#9704](https://github.com/NuGet/Home/issues/9704)</span><span class="sxs-lookup"><span data-stu-id="acd5d-121">Search for packages in the CLI with [`nuget.exe search`](../reference/cli-reference/cli-ref-search.md) command - [#9704](https://github.com/NuGet/Home/issues/9704)</span></span>

* <span data-ttu-id="acd5d-122">[`dotnet list package`](/dotnet/core/tools/dotnet-list-package) 명령에서 `--verbosity` 옵션을 지원 [#9600](https://github.com/NuGet/Home/issues/9600)</span><span class="sxs-lookup"><span data-stu-id="acd5d-122">[`dotnet list package`](/dotnet/core/tools/dotnet-list-package) command supports `--verbosity` option - [#9600](https://github.com/NuGet/Home/issues/9600)</span></span>

* <span data-ttu-id="acd5d-123">Visual Studio에서 .csproj 스타일의 PackageReference 기반 프로젝트에 대 한 빠른 No-Op 복원 최적화를 사용 합니다.- [#9565](https://github.com/NuGet/Home/issues/9565)</span><span class="sxs-lookup"><span data-stu-id="acd5d-123">Enable fast No-Op restore optimization for csproj-style, PackageReference-based projects in Visual Studio - [#9565](https://github.com/NuGet/Home/issues/9565)</span></span>

* <span data-ttu-id="acd5d-124">패키지 설치 및 업데이트와 같은 솔루션 수준 패키지 관리자 UI 작업은 더 빠르게 10 배 수 있습니다 [#6010](https://github.com/NuGet/Home/issues/6010)</span><span class="sxs-lookup"><span data-stu-id="acd5d-124">Solution level Package Manager UI operations such as package installs and updates are up to 10x faster - [#6010](https://github.com/NuGet/Home/issues/6010)</span></span>

* <span data-ttu-id="acd5d-125">Visual Studio- [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984), [#10052](https://github.com/NuGet/Home/issues/10052), [#9903](https://github.com/NuGet/Home/issues/9903) 의 여러 NuGet 성능 향상</span><span class="sxs-lookup"><span data-stu-id="acd5d-125">Several other NuGet performance improvements in Visual Studio - [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984), [#10052](https://github.com/NuGet/Home/issues/10052), [#9903](https://github.com/NuGet/Home/issues/9903)</span></span>


### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="acd5d-126">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="acd5d-126">Issues fixed in this release</span></span>

<span data-ttu-id="acd5d-127">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="acd5d-127">**DCRs:**</span></span>

* <span data-ttu-id="acd5d-128">.NET 5.0 TFM: 프레임 워크 선행 규칙- [#9436](https://github.com/NuGet/Home/issues/9436)</span><span class="sxs-lookup"><span data-stu-id="acd5d-128">.NET 5.0 TFM: Framework Precedence Rules - [#9436](https://github.com/NuGet/Home/issues/9436)</span></span>

* <span data-ttu-id="acd5d-129">TargetFramework를 구문 분석할 때 NuGet에서 도트 플랫폼 버전을 유추할 수 없습니다. [#9842](https://github.com/NuGet/Home/issues/9842)</span><span class="sxs-lookup"><span data-stu-id="acd5d-129">NuGet should not infer dots platform version when parsing TargetFramework - [#9842](https://github.com/NuGet/Home/issues/9842)</span></span>

* <span data-ttu-id="acd5d-130">개별 TFI, TFV, TFI, TFI 속성을 사용 하는 대신 TargetFrameworkMoniker & TargetPlatformMoniker를 사용 하 여 프레임 워크를 유추 합니다. [#9895](https://github.com/NuGet/Home/issues/9895)</span><span class="sxs-lookup"><span data-stu-id="acd5d-130">Use TargetFrameworkMoniker & TargetPlatformMoniker to infer the frameworks instead of using individual TFI, TFV, TPI, TPV properties - [#9895](https://github.com/NuGet/Home/issues/9895)</span></span>

* <span data-ttu-id="acd5d-131">`GetReferenceNearestTargetFrameworkTask()`플랫폼을 사용 하 여 대상 프레임 워크를 지원 하도록 업데이트 (예: net 5.0-windows)- [#9894](https://github.com/NuGet/Home/issues/9894)</span><span class="sxs-lookup"><span data-stu-id="acd5d-131">Update `GetReferenceNearestTargetFrameworkTask()` to support target frameworks with platforms (such as net5.0-windows) - [#9894](https://github.com/NuGet/Home/issues/9894)</span></span>

* <span data-ttu-id="acd5d-132">.NET 5.0 Visual Studio Api- [#9650](https://github.com/NuGet/Home/issues/9650)</span><span class="sxs-lookup"><span data-stu-id="acd5d-132">.NET 5.0 Visual Studio APIs - [#9650](https://github.com/NuGet/Home/issues/9650)</span></span>

* <span data-ttu-id="acd5d-133">패키지 관리자 UI: 패키지 통합 또는 업데이트 작업은 오류 (패키지 다운 그레이드 등)로 인해 차단 되지 않아야 합니다.- [#9224](https://github.com/NuGet/Home/issues/9224)</span><span class="sxs-lookup"><span data-stu-id="acd5d-133">Package Manager UI: Consolidate or Update packages operations should not be blocked due to errors (Package Downgrade, etc.) - [#9224](https://github.com/NuGet/Home/issues/9224)</span></span>

* <span data-ttu-id="acd5d-134">기능이 있는 프로젝트에 대해 NuGet 기능이 강화 되어야 합니다. "PackageReferences"- [#9957](https://github.com/NuGet/Home/issues/9957)</span><span class="sxs-lookup"><span data-stu-id="acd5d-134">NuGet features should light up for projects that have the capability; "PackageReferences" - [#9957](https://github.com/NuGet/Home/issues/9957)</span></span>

* <span data-ttu-id="acd5d-135">Visual Studio에서 No-Op 복원 메시지 표시 안 함- [#6384](https://github.com/NuGet/Home/issues/6384)</span><span class="sxs-lookup"><span data-stu-id="acd5d-135">Suppress No-Op Restore messages in Visual Studio - [#6384](https://github.com/NuGet/Home/issues/6384)</span></span>

<span data-ttu-id="acd5d-136">**미**</span><span class="sxs-lookup"><span data-stu-id="acd5d-136">**Bugs:**</span></span>

* <span data-ttu-id="acd5d-137">OutputWindowTextWriter 생성자는 백그라운드 스레드에서 호출 되지 않아야 합니다. [#9764](https://github.com/NuGet/Home/issues/9764)</span><span class="sxs-lookup"><span data-stu-id="acd5d-137">OutputWindowTextWriter constructor should not be called on background thread - [#9764](https://github.com/NuGet/Home/issues/9764)</span></span>

* <span data-ttu-id="acd5d-138">빅 Endian Cpu에서 서명 된 패키지 복원- [#9547](https://github.com/NuGet/Home/issues/9547)</span><span class="sxs-lookup"><span data-stu-id="acd5d-138">Restore signed packages on Big Endian CPUs - [#9547](https://github.com/NuGet/Home/issues/9547)</span></span>

* <span data-ttu-id="acd5d-139">OutputConsoleLogger는 MEF 생성자에서 선호도가 설정 메서드를 호출 하면 안 됩니다.- [#9591](https://github.com/NuGet/Home/issues/9591)</span><span class="sxs-lookup"><span data-stu-id="acd5d-139">OutputConsoleLogger should not call affinitized methods in MEF constructors - [#9591](https://github.com/NuGet/Home/issues/9591)</span></span>

* <span data-ttu-id="acd5d-140">Nuget.exe의 버그. 콘솔 `PrintJustified()` 메서드- [#9737](https://github.com/NuGet/Home/issues/9737)</span><span class="sxs-lookup"><span data-stu-id="acd5d-140">Bug in NuGet.CommandLine.Console `PrintJustified()` method - [#9737](https://github.com/NuGet/Home/issues/9737)</span></span>

* <span data-ttu-id="acd5d-141">잘못 된 바인딩으로 인해 패키지 메타 데이터가 가비지 수집 되는 경우 패키지 관리자 UI 메모리가 누수 [#9757](https://github.com/NuGet/Home/issues/9757)</span><span class="sxs-lookup"><span data-stu-id="acd5d-141">Package Manager UI memory leak when package metadata is garbage collected due to a bad binding - [#9757](https://github.com/NuGet/Home/issues/9757)</span></span>

* <span data-ttu-id="acd5d-142">서명 패키지 관리자 UI에서 packages.config 형식의 서명 된 패키지를 설치 하는 경우 오류 목록에 경고가 표시 되지 않습니다. [#9798](https://github.com/NuGet/Home/issues/9798)</span><span class="sxs-lookup"><span data-stu-id="acd5d-142">[Signing] No warning is showed in Error List when installing a signed package with packages.config format in Package Manager UI - [#9798](https://github.com/NuGet/Home/issues/9798)</span></span>

* <span data-ttu-id="acd5d-143">XPlat에는 공용 Api를 사용할 수 없습니다.- [#9821](https://github.com/NuGet/Home/issues/9821)</span><span class="sxs-lookup"><span data-stu-id="acd5d-143">NuGet.CommandLine.XPlat should not have public APIs - [#9821](https://github.com/NuGet/Home/issues/9821)</span></span>

* <span data-ttu-id="acd5d-144">#9822로 스레드 풀 스레드를 차단 하 여 발생 하는 솔루션 로드 시간에 리소스 경합을 줄입니다. `BlockingCollection.Take()`  -  [](https://github.com/NuGet/Home/issues/9822)</span><span class="sxs-lookup"><span data-stu-id="acd5d-144">Reduce resource contention at Solution Load time caused by blocking a threaded-pool thread with `BlockingCollection.Take()` - [#9822](https://github.com/NuGet/Home/issues/9822)</span></span>

* <span data-ttu-id="acd5d-145">다중 대상 프로젝트를 사용 하는 명령줄 복원에서는 NuGet이 내부 빌드에서 대상 프레임 워크 관련 정보를 읽어야 [#9869](https://github.com/NuGet/Home/issues/9869)</span><span class="sxs-lookup"><span data-stu-id="acd5d-145">In command line restore, with multi targeted projects, NuGet should read the target framework related information from the inner build - [#9869](https://github.com/NuGet/Home/issues/9869)</span></span>

* <span data-ttu-id="acd5d-146">TargetFrameworkInformation 항목을 통해 런타임 식별자 그래프 읽기- [#9874](https://github.com/NuGet/Home/issues/9874)</span><span class="sxs-lookup"><span data-stu-id="acd5d-146">Read Runtime Identifier graph through TargetFrameworkInformation item - [#9874](https://github.com/NuGet/Home/issues/9874)</span></span>

* <span data-ttu-id="acd5d-147">Visual Studio 및 일반 MSBuild evaluation 복원과 비교할 때 CrossTargeting 속성과 관련 하 여 정적 그래프 복원은 일관 되지 않습니다. [#9881](https://github.com/NuGet/Home/issues/9881)</span><span class="sxs-lookup"><span data-stu-id="acd5d-147">Static graph restore is inconsistent with regards to CrossTargeting property in compared to Visual Studio and regular MSBuild evaluation restore - [#9881](https://github.com/NuGet/Home/issues/9881)</span></span>

* <span data-ttu-id="acd5d-148">정적 그래프 복원에서 다중 대상 프로젝트를 사용 하는 경우 NuGet은 내부 빌드에서 대상 프레임 워크 관련 정보를 읽어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd5d-148">In static graph restore, with multi targeted projects, NuGet should read the target framework related information from the inner build.</span></span><span data-ttu-id="acd5d-149"> - [#9870](https://github.com/NuGet/Home/issues/9870)</span><span class="sxs-lookup"><span data-stu-id="acd5d-149"> - [#9870](https://github.com/NuGet/Home/issues/9870)</span></span>

* <span data-ttu-id="acd5d-150">`net5.0-platform`Visual Studio에서 프로젝트를 로드 하 고 복원할 수 있도록 허용- [#9863](https://github.com/NuGet/Home/issues/9863)</span><span class="sxs-lookup"><span data-stu-id="acd5d-150">Allow `net5.0-platform` projects to be loaded and restored in Visual Studio - [#9863](https://github.com/NuGet/Home/issues/9863)</span></span>

* <span data-ttu-id="acd5d-151">패키지 관리자 UI에서 확인 된 버전 표시- [#9826](https://github.com/NuGet/Home/issues/9826)</span><span class="sxs-lookup"><span data-stu-id="acd5d-151">Display the resolved version in the Package Manager UI - [#9826](https://github.com/NuGet/Home/issues/9826)</span></span>

* <span data-ttu-id="acd5d-152">패키지 관리자 UI: 솔루션 탐색기에 모든 NuGet 패키지 종속성이 표시 되지 않습니다. [#9898](https://github.com/NuGet/Home/issues/9898)</span><span class="sxs-lookup"><span data-stu-id="acd5d-152">Package Manager UI: Solution Explorer is not showing all NuGet package dependencies - [#9898](https://github.com/NuGet/Home/issues/9898)</span></span>

* <span data-ttu-id="acd5d-153">SPDX 라이선스 목록 업데이트- [#9946](https://github.com/NuGet/Home/issues/9946)</span><span class="sxs-lookup"><span data-stu-id="acd5d-153">Update the SPDX license list - [#9946](https://github.com/NuGet/Home/issues/9946)</span></span>

* <span data-ttu-id="acd5d-154">NuGet 패키지 관리를 연 후 VS 2019 충돌이 발생 함: 아이콘이 이미지 conversio에서 처리 되지 않은 예외를 발생 시킵니다 [#9696](https://github.com/NuGet/Home/issues/9696)</span><span class="sxs-lookup"><span data-stu-id="acd5d-154">VS 2019 crashes after opening Manage NuGet Packages: icon causes unhandled exception in image conversio - [#9696](https://github.com/NuGet/Home/issues/9696)</span></span>

* <span data-ttu-id="acd5d-155">Ilmerge는 온- [#9966](https://github.com/NuGet/Home/issues/9966) Newtonsoft.Js제외 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd5d-155">NuGet.Packaging.Extraction needs ilmerge to exclude Newtonsoft.Json - [#9966](https://github.com/NuGet/Home/issues/9966)</span></span>

* <span data-ttu-id="acd5d-156">오류가 없으면 ContinuePackingAfterGeneratingNuspec = false로 압축 하지 않아야 합니다.- [#9786](https://github.com/NuGet/Home/issues/9786)</span><span class="sxs-lookup"><span data-stu-id="acd5d-156">Packing with ContinuePackingAfterGeneratingNuspec=false should not fail when there are no errors - [#9786](https://github.com/NuGet/Home/issues/9786)</span></span>

* <span data-ttu-id="acd5d-157">패키지 관리자 UI: 아이콘이 색을 제대로 반전 하지 않음- [#10017](https://github.com/NuGet/Home/issues/10017)</span><span class="sxs-lookup"><span data-stu-id="acd5d-157">Package Manager UI: Icons aren't inverting colors properly - [#10017](https://github.com/NuGet/Home/issues/10017)</span></span>

* <span data-ttu-id="acd5d-158">복원 시 최신 및 No-Op 프로젝트에 대 한 프로젝트 수가 잘못 되었습니다. [#10026](https://github.com/NuGet/Home/issues/10026)</span><span class="sxs-lookup"><span data-stu-id="acd5d-158">Incorrect project counts for Up-To-Date and No-Op projects at Restore - [#10026](https://github.com/NuGet/Home/issues/10026)</span></span>

* <span data-ttu-id="acd5d-159">`/p:RestoreUseStaticGraphEvaluation=true`값에 결과를 사용 하는 것은 Null 일 수 없습니다 [#9280](https://github.com/NuGet/Home/issues/9280)</span><span class="sxs-lookup"><span data-stu-id="acd5d-159">Using `/p:RestoreUseStaticGraphEvaluation=true` Results in Value Cannot Be Null - [#9280](https://github.com/NuGet/Home/issues/9280)</span></span>

* <span data-ttu-id="acd5d-160">`dotnet pack` WPF 라이브러리 프로젝트에 대 한 별칭을 잘못 사용 합니다.- [#10020](https://github.com/NuGet/Home/issues/10020)</span><span class="sxs-lookup"><span data-stu-id="acd5d-160">`dotnet pack` mistakenly uses alias for WPF Library projects - [#10020](https://github.com/NuGet/Home/issues/10020)</span></span>

* <span data-ttu-id="acd5d-161">패키지 관리자 UI: 서명 유효성 검사에 실패 하면 NullReferenceException- [#10042](https://github.com/NuGet/Home/issues/10042)</span><span class="sxs-lookup"><span data-stu-id="acd5d-161">Package Manager UI: NullReferenceException when signature validation fails - [#10042](https://github.com/NuGet/Home/issues/10042)</span></span>

* <span data-ttu-id="acd5d-162">Codespaces: `object` 프로젝트 메타 데이터 값에 형식을 사용 하지 않습니다.- [#10055](https://github.com/NuGet/Home/issues/10055)</span><span class="sxs-lookup"><span data-stu-id="acd5d-162">Codespaces: do not use `object` type for project metadata values  - [#10055](https://github.com/NuGet/Home/issues/10055)</span></span>

* <span data-ttu-id="acd5d-163">Codespaces: 도구 옵션에 패키지 원본을 저장 하면 자격 증명을 덮어씁니다. [#9711](https://github.com/NuGet/Home/issues/9711)</span><span class="sxs-lookup"><span data-stu-id="acd5d-163">Codespaces: saving package sources in tools options will overwrite credentials - [#9711](https://github.com/NuGet/Home/issues/9711)</span></span>


<span data-ttu-id="acd5d-164">**[이 릴리스에서 해결 된 모든 문제 목록-5.8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**</span><span class="sxs-lookup"><span data-stu-id="acd5d-164">**[List of all issues fixed in this release - 5.8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**</span></span>

<span data-ttu-id="acd5d-165">**[이 릴리스의 문제 목록-5.8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**</span><span class="sxs-lookup"><span data-stu-id="acd5d-165">**[List of issues in this release - 5.8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**</span></span>

### <a name="community-contributions"></a><span data-ttu-id="acd5d-166">커뮤니티 기여</span><span class="sxs-lookup"><span data-stu-id="acd5d-166">Community contributions</span></span>

<span data-ttu-id="acd5d-167">이 NuGet 릴리스를 위해 도움을 주는 모든 참가자에 게 감사 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd5d-167">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="acd5d-168">대상</span><span class="sxs-lookup"><span data-stu-id="acd5d-168">Who</span></span>|<span data-ttu-id="acd5d-169">Pr</span><span class="sxs-lookup"><span data-stu-id="acd5d-169">PRs</span></span>|<span data-ttu-id="acd5d-170">문제</span><span class="sxs-lookup"><span data-stu-id="acd5d-170">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="acd5d-171">omajid</span><span class="sxs-lookup"><span data-stu-id="acd5d-171">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="acd5d-172">3437</span><span class="sxs-lookup"><span data-stu-id="acd5d-172">3437</span></span>](https://github.com/NuGet/NuGet.Client/pull/3437) | <span data-ttu-id="acd5d-173">오류 메시지에 오타가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="acd5d-173">Typo in error message.</span></span> <span data-ttu-id="acd5d-174">"administrator" 대신 "관리자로"- [#9662](https://github.com/NuGet/Home/issues/9662)</span><span class="sxs-lookup"><span data-stu-id="acd5d-174">"administator" instead of "administrator" - [#9662](https://github.com/NuGet/Home/issues/9662)</span></span>
[<span data-ttu-id="acd5d-175">odalet</span><span class="sxs-lookup"><span data-stu-id="acd5d-175">odalet</span></span>](https://github.com/odalet) | [<span data-ttu-id="acd5d-176">3341</span><span class="sxs-lookup"><span data-stu-id="acd5d-176">3341</span></span>](https://github.com/NuGet/NuGet.Client/pull/3341) | <span data-ttu-id="acd5d-177">AssemblyInformationalVersion 보고서가 잘못 된 NuGet 팩이 "설명이 필요 합니다."- [#5548](https://github.com/NuGet/Home/issues/5548)</span><span class="sxs-lookup"><span data-stu-id="acd5d-177">NuGet Pack with invalid AssemblyInformationalVersion reports "description is required" - [#5548](https://github.com/NuGet/Home/issues/5548)</span></span>
[<span data-ttu-id="acd5d-178">campersau</span><span class="sxs-lookup"><span data-stu-id="acd5d-178">campersau</span></span>](https://github.com/campersau) | [<span data-ttu-id="acd5d-179">3501</span><span class="sxs-lookup"><span data-stu-id="acd5d-179">3501</span></span>](https://github.com/NuGet/NuGet.Client/pull/3501) | <span data-ttu-id="acd5d-180">`RepositoryMetadata.Equals()` 분기 및 커밋 속성을 고려 하지 않습니다.- [#9613](https://github.com/NuGet/Home/issues/9613)</span><span class="sxs-lookup"><span data-stu-id="acd5d-180">`RepositoryMetadata.Equals()` does not account for Branch and Commit properties - [#9613](https://github.com/NuGet/Home/issues/9613)</span></span>
[<span data-ttu-id="acd5d-181">Youssef1313</span><span class="sxs-lookup"><span data-stu-id="acd5d-181">Youssef1313</span></span>](https://github.com/Youssef1313) | [<span data-ttu-id="acd5d-182">3599</span><span class="sxs-lookup"><span data-stu-id="acd5d-182">3599</span></span>](https://github.com/NuGet/NuGet.Client/pull/3599) | <span data-ttu-id="acd5d-183">Visual Studio 오류 목록 창에서 뉴 코드를 클릭 하면로 이동 해야 https://docs.microsoft.com/nuget/reference/errors-and-warnings/  -  [#9934](https://github.com/NuGet/Home/issues/9934)</span><span class="sxs-lookup"><span data-stu-id="acd5d-183">Clicking NU code in Visual Studio Error List window should go to https://docs.microsoft.com/nuget/reference/errors-and-warnings/ - [#9934](https://github.com/NuGet/Home/issues/9934)</span></span>
[<span data-ttu-id="acd5d-184">ChrisMaddock</span><span class="sxs-lookup"><span data-stu-id="acd5d-184">ChrisMaddock</span></span>](https://github.com/ChrisMaddock) | [<span data-ttu-id="acd5d-185">3624</span><span class="sxs-lookup"><span data-stu-id="acd5d-185">3624</span></span>](https://github.com/NuGet/NuGet.Client/pull/3624) | <span data-ttu-id="acd5d-186">Visual Studio 옵션을 통해 새 패키지 소스를 추가할 때 ' https://'를 사용 합니다.- [#9974](https://github.com/NuGet/Home/issues/9974)</span><span class="sxs-lookup"><span data-stu-id="acd5d-186">Use 'https://' when adding new package source through Visual Studio options - [#9974](https://github.com/NuGet/Home/issues/9974)</span></span>
[<span data-ttu-id="acd5d-187">Zzok</span><span class="sxs-lookup"><span data-stu-id="acd5d-187">Therzok</span></span>](https://github.com/Therzok) | [<span data-ttu-id="acd5d-188">3636</span><span class="sxs-lookup"><span data-stu-id="acd5d-188">3636</span></span>](https://github.com/NuGet/NuGet.Client/pull/3636) | <span data-ttu-id="acd5d-189">`RuntimeEnvironmentHelper.IsRunningOnVisualStudio`Mono- [#9989](https://github.com/NuGet/Home/issues/9989) 의 성능 문제</span><span class="sxs-lookup"><span data-stu-id="acd5d-189">`RuntimeEnvironmentHelper.IsRunningOnVisualStudio` performance issue on Mono - [#9989](https://github.com/NuGet/Home/issues/9989)</span></span>
[<span data-ttu-id="acd5d-190">thomaslevesque</span><span class="sxs-lookup"><span data-stu-id="acd5d-190">thomaslevesque</span></span>](https://github.com/thomaslevesque) | [<span data-ttu-id="acd5d-191">3442</span><span class="sxs-lookup"><span data-stu-id="acd5d-191">3442</span></span>](https://github.com/NuGet/NuGet.Client/pull/3442) | <span data-ttu-id="acd5d-192">SemanticVersion 클래스에 대 한 TypeConverter 추가- [#9125](https://github.com/NuGet/Home/issues/9125)</span><span class="sxs-lookup"><span data-stu-id="acd5d-192">Add a TypeConverter for the SemanticVersion class - [#9125](https://github.com/NuGet/Home/issues/9125)</span></span>

## <a name="summary-whats-new-in-581"></a><span data-ttu-id="acd5d-193">요약: 5.8.1의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="acd5d-193">Summary: What's New in 5.8.1</span></span>

* <span data-ttu-id="acd5d-194">package.lock.jspackages.config 5.8- [#10257](https://github.com/NuGet/Home/issues/10257) 에서 잘못 된 대상 프레임 워크를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="acd5d-194">packages.config package.lock.json uses an incorrect target framework in 5.8 - [#10257](https://github.com/NuGet/Home/issues/10257)</span></span>

* <span data-ttu-id="acd5d-195">5.8 + 16.8 PackageReference 및 packages.config를 혼합할 때 전이적 프로젝트 종속성을 확인할 수 없습니다 [#10326](https://github.com/NuGet/Home/issues/10326)</span><span class="sxs-lookup"><span data-stu-id="acd5d-195">5.8 + 16.8 Cannot resolve transitive project dependencies when mixing PackageReference and packages.config - [#10326](https://github.com/NuGet/Home/issues/10326)</span></span>

<span data-ttu-id="acd5d-196">**[이 릴리스에서 수정 된 모든 문제 목록-5.8.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**</span><span class="sxs-lookup"><span data-stu-id="acd5d-196">**[List of all issues fixed in this release - 5.8.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**</span></span>

<span data-ttu-id="acd5d-197">**[이 릴리스의 커밋 목록-5.8.1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**</span><span class="sxs-lookup"><span data-stu-id="acd5d-197">**[List of commits in this release - 5.8.1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**</span></span>

## <a name="feedback-welcome"></a><span data-ttu-id="acd5d-198">사용자 의견 환영</span><span class="sxs-lookup"><span data-stu-id="acd5d-198">Feedback welcome</span></span>

<span data-ttu-id="acd5d-199">Microsoft는 사용자의 의견을 소중하게 생각합니다.</span><span class="sxs-lookup"><span data-stu-id="acd5d-199">Your feedback is important to us.</span></span>  <span data-ttu-id="acd5d-200">이 릴리스에 문제가 있는 경우 [GitHub 문제](https://github.com/NuGet/Home/issues) 및 [Visual Studio 개발자 커뮤니티](https://developercommunity.visualstudio.com/) 에서 기존 문제를 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="acd5d-200">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="acd5d-201">NuGet 내의 새로운 문제에 대 한 자세한 내용은 [GitHub 문제](https://github.com/NuGet/Home/issues/new)를 보고 하세요.</span><span class="sxs-lookup"><span data-stu-id="acd5d-201">For new issues within NuGet, please report a [GitHub Issue](https://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="acd5d-202">일반적인 NuGet 환경 문제에 대 한 자세한 내용은 **문제 보고 > 도움말** 에서 즐겨 사용 하는 IDE의 [문제 보고](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) 옵션을 통해 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="acd5d-202">For general NuGet experience issues, let us know via the [Report a Problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>