---
title: NuGet 5.5 릴리스 정보
description: 새 기능, 버그 수정 및 Ecrs를 비롯 한 NuGet 5.5에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0fde67dd03c31e986ed89f2f8627608e279ef908
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780115"
---
# <a name="nuget-55-release-notes"></a><span data-ttu-id="9e726-103">NuGet 5.5 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="9e726-103">NuGet 5.5 Release Notes</span></span>

<span data-ttu-id="9e726-104">NuGet 배포 차량:</span><span class="sxs-lookup"><span data-stu-id="9e726-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="9e726-105">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="9e726-105">NuGet version</span></span> | <span data-ttu-id="9e726-106">Visual Studio 버전에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="9e726-106">Available in Visual Studio version</span></span>| <span data-ttu-id="9e726-107">.NET SDK에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="9e726-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="9e726-108">**5.5.0**</span><span class="sxs-lookup"><span data-stu-id="9e726-108">**5.5.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="9e726-109">Visual Studio 2019 버전 16.5</span><span class="sxs-lookup"><span data-stu-id="9e726-109">Visual Studio 2019 version 16.5</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="9e726-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="9e726-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="9e726-111"><sup>1</sup> .NET Core 워크 로드와 함께 Visual Studio 2019와 함께 설치 됨</span><span class="sxs-lookup"><span data-stu-id="9e726-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-55"></a><span data-ttu-id="9e726-112">요약: 5.5의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="9e726-112">Summary: What's New in 5.5</span></span>

* <span data-ttu-id="9e726-113">Visual Studio의 NuGet 패키지 관리자 UI에 대 한 내게 필요한 옵션 및 화면 판독기 환경 개선</span><span class="sxs-lookup"><span data-stu-id="9e726-113">Improved accessibility and screen reader experience for the NuGet package manager UI in Visual Studio</span></span>
    * <span data-ttu-id="9e726-114">화면 판독기 환경에서의 접근성 문제, 누락 된 altText, 설치 된 텍스트 상자에 대 한 액세스 가능한 이름 등,- [#9059](https://github.com/NuGet/Home/issues/9059)</span><span class="sxs-lookup"><span data-stu-id="9e726-114">Accessibility issues in Screen Reader experiences, missing altText and accessible name for Installed textbox, etc., - [#9059](https://github.com/NuGet/Home/issues/9059)</span></span>
    * <span data-ttu-id="9e726-115">패키지 목록에서 화면 판독기 환경의 접근성 문제- [#9077](https://github.com/NuGet/Home/issues/9077)</span><span class="sxs-lookup"><span data-stu-id="9e726-115">Accessibility issues in Screen Reader experiences in Packages List - [#9077](https://github.com/NuGet/Home/issues/9077)</span></span>
    * <span data-ttu-id="9e726-116">"찾아보기", "설치", "업데이트" 탭과 관련 된 화면 판독기 환경에서 접근성 문제가 있습니다 [#9078](https://github.com/NuGet/Home/issues/9078)</span><span class="sxs-lookup"><span data-stu-id="9e726-116">Accessibility issues in Screen Reader experiences related to "browse","install","update" Tabs - [#9078](https://github.com/NuGet/Home/issues/9078)</span></span>
    * <span data-ttu-id="9e726-117">내레이터는 "Blank", "No Dependencies", "," MIT "링크 레이블을 발표 하지 않습니다 [#9157](https://github.com/NuGet/Home/issues/9157)</span><span class="sxs-lookup"><span data-stu-id="9e726-117">Narrator does not announce "Blank","No Dependencies","nuget.org","MIT" link label [#9157](https://github.com/NuGet/Home/issues/9157)</span></span>

* <span data-ttu-id="9e726-118">로컬 피드에 호스트 되는 패키지에 대 한 Visual Studio 패키지 관리자 UI의 자동 포함 아이콘에 대 한 지원- [#8189](https://github.com/NuGet/Home/issues/8189)</span><span class="sxs-lookup"><span data-stu-id="9e726-118">Support for surfacing self-contained icons in Visual Studio package manager UI for packages hosted on local feeds - [#8189](https://github.com/NuGet/Home/issues/8189)</span></span>

* <span data-ttu-id="9e726-119">`RestoreUseStaticGraphEvaluation`MSBuild 정적 Graph api- [8791](https://github.com/NuGet/Home/issues/8791) 를 호출 하 여 계산 속도를 높일 때 사용 하는 op 복원 성능이 크게 향상 됨</span><span class="sxs-lookup"><span data-stu-id="9e726-119">Significantly improved no-op restore performance using `RestoreUseStaticGraphEvaluation` which speeds up evaluations by calling MSBuild Static Graph APIs - [8791](https://github.com/NuGet/Home/issues/8791)</span></span>

* <span data-ttu-id="9e726-120">플랫폼 간 인증 플러그인을 사용 하 여 dotnet.exe 안정성이 향상 됨</span><span class="sxs-lookup"><span data-stu-id="9e726-120">Improved dotnet.exe reliability with cross-platform authentication plugins</span></span>
    * <span data-ttu-id="9e726-121">TaskCanceledException를 사용 하 여 dotnet restore 실패- [#7842](https://github.com/NuGet/Home/issues/7842)</span><span class="sxs-lookup"><span data-stu-id="9e726-121">dotnet restore failing with TaskCanceledException - [#7842](https://github.com/NuGet/Home/issues/7842)</span></span>
    * <span data-ttu-id="9e726-122">플러그 인: "작업이 취소 되었습니다."-이로 인해 ADO 인증에 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e726-122">Plugin:  "A task was cancelled" - problem with ADO authentication due to this.</span></span><span data-ttu-id="9e726-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span><span class="sxs-lookup"><span data-stu-id="9e726-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span></span>

* <span data-ttu-id="9e726-124">`dotnet nuget <add|remove|update|disable|enable|list> source`명령 추가- [#4126](https://github.com/NuGet/Home/issues/4126)</span><span class="sxs-lookup"><span data-stu-id="9e726-124">add `dotnet nuget <add|remove|update|disable|enable|list> source` command - [#4126](https://github.com/NuGet/Home/issues/4126)</span></span>

* <span data-ttu-id="9e726-125">`--skip-duplicate`Dotnet nuget 푸시 [#8778](https://github.com/NuGet/Home/issues/8778) 사용에 대 한 지원을</span><span class="sxs-lookup"><span data-stu-id="9e726-125">Suport for `--skip-duplicate`  using dotnet nuget push - [#8778](https://github.com/NuGet/Home/issues/8778)</span></span>

* <span data-ttu-id="9e726-126">`packages.config`Msbuild/restore- [#8506](https://github.com/NuGet/Home/issues/8506) 지원</span><span class="sxs-lookup"><span data-stu-id="9e726-126">Support `packages.config` with msbuild /restore - [#8506](https://github.com/NuGet/Home/issues/8506)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="9e726-127">이번 릴리스에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="9e726-127">Issues fixed in this release</span></span>

<span data-ttu-id="9e726-128">**버그**</span><span class="sxs-lookup"><span data-stu-id="9e726-128">**Bugs**</span></span>

* <span data-ttu-id="9e726-129">V3 Api를 사용 하 여 Self-Updater 재작업- [#4197](https://github.com/NuGet/Home/issues/4197)</span><span class="sxs-lookup"><span data-stu-id="9e726-129">Rework Self-Updater with V3 Apis - [#4197](https://github.com/NuGet/Home/issues/4197)</span></span>

* <span data-ttu-id="9e726-130">패키지 종속성 버전이 ' \* '로 설정 된 경우 패키지 종속성 버전이 잘못 되었습니다.- [#6697](https://github.com/NuGet/Home/issues/6697)</span><span class="sxs-lookup"><span data-stu-id="9e726-130">Wrong package dependency version If package dependency version is set to '\*' - [#6697](https://github.com/NuGet/Home/issues/6697)</span></span>

* <span data-ttu-id="9e726-131">ErrorUnsafePackageEntry 오류 메시지가 문제의 원인을 가리키지 않습니다.- [#7505](https://github.com/NuGet/Home/issues/7505)</span><span class="sxs-lookup"><span data-stu-id="9e726-131">ErrorUnsafePackageEntry error message is not pointing to source of problem - [#7505](https://github.com/NuGet/Home/issues/7505)</span></span>

* <span data-ttu-id="9e726-132">잠금 파일은 "\*" 시나리오에서 적용 되지 않습니다.- [#8073](https://github.com/NuGet/Home/issues/8073)</span><span class="sxs-lookup"><span data-stu-id="9e726-132">Lock file is not honored in "\*" scenarios  - [#8073](https://github.com/NuGet/Home/issues/8073)</span></span>

* <span data-ttu-id="9e726-133">PackageReference에서 \*를 사용 하는 경우 (MSBuild/Dotnet/VS restore do)에서 NuGet.exe는 최신 버전의 패키지로 확인 되지 않습니다 [#8432](https://github.com/NuGet/Home/issues/8432)</span><span class="sxs-lookup"><span data-stu-id="9e726-133">NuGet.exe does not resolve to the latest version of a package when using \* in PackageReference (MSBuild/Dotnet/VS restore do) - [#8432](https://github.com/NuGet/Home/issues/8432)</span></span>

* <span data-ttu-id="9e726-134">다중 대상 WPF 프로젝트를 사용 하는 dotnet list 패키지- [#8463](https://github.com/NuGet/Home/issues/8463)</span><span class="sxs-lookup"><span data-stu-id="9e726-134">dotnet list package with multi targeting WPF project - [#8463](https://github.com/NuGet/Home/issues/8463)</span></span>

* <span data-ttu-id="9e726-135">ConcurrencyUtilities 개선 (CPU 사용량 감소)- [#8653](https://github.com/NuGet/Home/issues/8653)</span><span class="sxs-lookup"><span data-stu-id="9e726-135">Improve ConcurrencyUtilities (reduce CPU usage) - [#8653](https://github.com/NuGet/Home/issues/8653)</span></span>

* <span data-ttu-id="9e726-136">언로드된 프로젝트 시나리오에 대 한 DG 사양은 미리 보기 복원으로 작성할 수 없습니다.- [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="9e726-136">DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="9e726-137">Visual Studio NuGet 패키지 (RestoreManagerPackage)는 솔루션 빌드 이벤트에서 자동으로 로드 해야 합니다. [#8796](https://github.com/NuGet/Home/issues/8796)</span><span class="sxs-lookup"><span data-stu-id="9e726-137">The Visual Studio NuGet packages (RestoreManagerPackage) needs to auto load on solution build events - [#8796](https://github.com/NuGet/Home/issues/8796)</span></span>

* <span data-ttu-id="9e726-138">.Vssettings init의 교착 상태- [#8842](https://github.com/NuGet/Home/issues/8842)</span><span class="sxs-lookup"><span data-stu-id="9e726-138">Deadlock in VSSettings init - [#8842](https://github.com/NuGet/Home/issues/8842)</span></span>

* <span data-ttu-id="9e726-139">VisualStudio 도구 상자는 프로젝트가 솔루션 폴더에 배치 되는 경우 NuGet 패키지에서 채워지지 않습니다.- [#8868](https://github.com/NuGet/Home/issues/8868)</span><span class="sxs-lookup"><span data-stu-id="9e726-139">VisualStudio ToolBox is not populated from a NuGet package if a project is placed in a solution folder - [#8868](https://github.com/NuGet/Home/issues/8868)</span></span>

* <span data-ttu-id="9e726-140">VS: 솔루션 복원 영구적으로 경합 조건으로 인해 실패 함- [#8881](https://github.com/NuGet/Home/issues/8881)</span><span class="sxs-lookup"><span data-stu-id="9e726-140">VS:  solution restore perpetually fails due to race condition - [#8881](https://github.com/NuGet/Home/issues/8881)</span></span>

* <span data-ttu-id="9e726-141">"로드 중 ..."이 설치 된 탭에서 "</span><span class="sxs-lookup"><span data-stu-id="9e726-141">Constant "loading.." on installed tab, and "searching</span></span> <term><span data-ttu-id="9e726-142">. "업데이트 탭- [#8890](https://github.com/NuGet/Home/issues/8890)</span><span class="sxs-lookup"><span data-stu-id="9e726-142">.." on updates tab - [#8890](https://github.com/NuGet/Home/issues/8890)</span></span>

* <span data-ttu-id="9e726-143">캐시 만료 후 VS PM UI에 포함 된 아이콘 누락- [#9069](https://github.com/NuGet/Home/issues/9069)</span><span class="sxs-lookup"><span data-stu-id="9e726-143">Missing Embedded Icons in VS PM UI after cache expires - [#9069](https://github.com/NuGet/Home/issues/9069)</span></span>

* <span data-ttu-id="9e726-144">FireAndForget PM UI 시작- [#9112](https://github.com/NuGet/Home/issues/9112)</span><span class="sxs-lookup"><span data-stu-id="9e726-144">FireAndForget PM UI startup - [#9112](https://github.com/NuGet/Home/issues/9112)</span></span>

* <span data-ttu-id="9e726-145">복원: IncludeExcludeFiles. Equals (...) 구현이 잘못 되었습니다. [#9167](https://github.com/NuGet/Home/issues/9167)</span><span class="sxs-lookup"><span data-stu-id="9e726-145">Restore: IncludeExcludeFiles.Equals(...) implementation is incorrect - [#9167](https://github.com/NuGet/Home/issues/9167)</span></span>

* <span data-ttu-id="9e726-146">복원: PackageSpec ()는 동일 하지 않은 클론을 만듭니다. [#9211](https://github.com/NuGet/Home/issues/9211)</span><span class="sxs-lookup"><span data-stu-id="9e726-146">Restore: PackageSpec.Clone() creates unequal clone - [#9211](https://github.com/NuGet/Home/issues/9211)</span></span>

* <span data-ttu-id="9e726-147">"빌드가 오류로 인해 완료 되는 경우 항상 오류 목록 표시"를 선택 하지 않은 경우에도 표시 되는 오류 목록 [#8190](https://github.com/NuGet/Home/issues/8190)</span><span class="sxs-lookup"><span data-stu-id="9e726-147">Error list shown although "Always show Error List if build finishes with errors" is not checked - [#8190](https://github.com/NuGet/Home/issues/8190)</span></span>

* <span data-ttu-id="9e726-148">정적 그래프 복원은 빈 솔루션 경로를 전달 하면 안 됩니다.- [#9061](https://github.com/NuGet/Home/issues/9061)</span><span class="sxs-lookup"><span data-stu-id="9e726-148">Static Graph restore should not pass empty SolutionPath - [#9061](https://github.com/NuGet/Home/issues/9061)</span></span>

* <span data-ttu-id="9e726-149">복원: 각 프로젝트에 대 한 클로저 계산 됨- [#9042](https://github.com/NuGet/Home/issues/9042)</span><span class="sxs-lookup"><span data-stu-id="9e726-149">Restore: closure computed for each project 4 times - [#9042](https://github.com/NuGet/Home/issues/9042)</span></span>

* <span data-ttu-id="9e726-150">Restore: DependencyGraphSpec (...)에는 JObject- [#9040](https://github.com/NuGet/Home/issues/9040) 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9e726-150">Restore: DependencyGraphSpec.Load(...) does not need JObject - [#9040](https://github.com/NuGet/Home/issues/9040)</span></span>

* <span data-ttu-id="9e726-151">복원: LOH (large object heap)에 생성 되는 긴 문자열 [#9031](https://github.com/NuGet/Home/issues/9031)</span><span class="sxs-lookup"><span data-stu-id="9e726-151">Restore: large strings created on large object heap (LOH) - [#9031](https://github.com/NuGet/Home/issues/9031)</span></span>

* <span data-ttu-id="9e726-152">MSBuild SDK 확인자- [8848](https://github.com/NuGet/Home/issues/8848) 로 인해 최신 mono의 사용자 지정 nuget.exe 중단 될 수 있음</span><span class="sxs-lookup"><span data-stu-id="9e726-152">Custom nuget.exe on newer mono might break due to the MSBuild SDK Resolver - [8848](https://github.com/NuGet/Home/issues/8848)</span></span>

* <span data-ttu-id="9e726-153">nuget.dgspec.js에서 "다른 프로세스에서 사용" 하는 경우 복원이 실패 합니다.- [8692](https://github.com/NuGet/Home/issues/8692)</span><span class="sxs-lookup"><span data-stu-id="9e726-153">restore fails when nuget.dgspec.json is "used by another process" - [8692](https://github.com/NuGet/Home/issues/8692)</span></span>

<span data-ttu-id="9e726-154">**DCR**</span><span class="sxs-lookup"><span data-stu-id="9e726-154">**DCRs**</span></span>

* <span data-ttu-id="9e726-155">_GetRestoreProjectStyle의 논리는 작업에 있어야 합니다. [#8804](https://github.com/NuGet/Home/issues/8804)</span><span class="sxs-lookup"><span data-stu-id="9e726-155">Logic in _GetRestoreProjectStyle should be in a task - [#8804](https://github.com/NuGet/Home/issues/8804)</span></span>

* <span data-ttu-id="9e726-156">설치 됨 탭에서 기본적으로 사용 중단 정보를 추가 [#8541](https://github.com/NuGet/Home/issues/8541)</span><span class="sxs-lookup"><span data-stu-id="9e726-156">Add deprecation information by default on the installed tab - [#8541](https://github.com/NuGet/Home/issues/8541)</span></span>

<span data-ttu-id="9e726-157">**[이 릴리스에서 해결 된 모든 문제 목록-5.5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span><span class="sxs-lookup"><span data-stu-id="9e726-157">**[List of all issues fixed in this release - 5.5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span></span>
