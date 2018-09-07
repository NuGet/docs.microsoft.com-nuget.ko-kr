---
title: NuGet 4.0 RC 릴리스 정보
description: NuGet 4.0 RTM에 대한 릴리스 정보(알려진 문제, 버그 수정, 추가된 기능 및 DCR 포함)
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c27d0aa2e5c9af9cb15d2f487b93e93aca666214
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547763"
---
# <a name="nuget-40-rtm-release-notes"></a><span data-ttu-id="75602-103">NuGet 4.0 RTM 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="75602-103">NuGet 4.0 RTM Release Notes</span></span>

<span data-ttu-id="75602-104">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes)은 .NET Core에 대한 지원을 추가하고, 많은 품질 수정을 포함하며, 성능을 향상시키는 NuGet 4.0과 함께 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="75602-104">[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.0 which adds support for .NET Core, has a bunch of quality fixes and improves performance.</span></span> <span data-ttu-id="75602-105">또한 이 릴리스에는 PackageReference 지원, MSBuild 대상 NuGet 명령, 백그라운드 패키지 복원 등과 같이 향상된 몇 가지 기능도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="75602-105">This release also brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restores, and more.</span></span>

## <a name="known-issues"></a><span data-ttu-id="75602-106">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="75602-106">Known issues</span></span>

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a><span data-ttu-id="75602-107">솔루션에 다른 프로젝트를 참조하는 프로젝트가 여러 개 있는 경우 NuGet 복원이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75602-107">NuGet restore may fail when you have multiple projects referencing another project in a solution</span></span>

#### <a name="issue"></a><span data-ttu-id="75602-108">문제</span><span class="sxs-lookup"><span data-stu-id="75602-108">Issue</span></span>

<span data-ttu-id="75602-109">대/소문자나 상대 경로가 다른, 동일한 프로젝트에 대한 프로젝트 참조가 솔루션에 있는 경우 NuGet 복원이 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75602-109">NuGet restore may not work if, in a solution, you have project references to the same project with different casing or with different relative paths.</span></span> [<span data-ttu-id="75602-110">NuGet#4574</span><span class="sxs-lookup"><span data-stu-id="75602-110">NuGet#4574</span></span>](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a><span data-ttu-id="75602-111">해결 방법</span><span class="sxs-lookup"><span data-stu-id="75602-111">Workaround</span></span>

<span data-ttu-id="75602-112">모든 프로젝트 참조에 대해 대/소문자나 상대 경로를 동일하게 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="75602-112">Fix the casings or relative paths to be the same for all project references.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="75602-113">패키지 관리자 콘솔을 사용하는 동안 'Enter' 키가 작동하지 않을 수 있음</span><span class="sxs-lookup"><span data-stu-id="75602-113">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="75602-114">문제</span><span class="sxs-lookup"><span data-stu-id="75602-114">Issue</span></span>

<span data-ttu-id="75602-115">경우에 따라 패키지 관리자 콘솔에서 Enter 키가 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75602-115">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="75602-116">이런 경우 수정 진행 상황을 확인하고 재현 단계에 대해 도움이 되는 추가 정보를 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="75602-116">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="75602-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="75602-117">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="75602-118">해결 방법</span><span class="sxs-lookup"><span data-stu-id="75602-118">Workaround</span></span>

<span data-ttu-id="75602-119">Visual Studio를 다시 시작하고 솔루션을 열기 전에 PMC를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="75602-119">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="75602-120">또는 `project.lock.json`을 삭제하고 다시 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="75602-120">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a><span data-ttu-id="75602-121">.NET Core 프로젝트에서 잘못된 시그니처와 함께 어셈블리가 포함된 패키지를 사용할 때 무한 복원 루프가 발생할 수 있음</span><span class="sxs-lookup"><span data-stu-id="75602-121">In .NET Core projects, you may end up in infinite restore loop when you use a package containing an assembly with an invalid signature</span></span>

#### <a name="issue"></a><span data-ttu-id="75602-122">문제</span><span class="sxs-lookup"><span data-stu-id="75602-122">Issue</span></span>

<span data-ttu-id="75602-123">경우에 따라 잘못된 시그니처와 함께 어셈블리가 포함된 패키지를 사용하거나 패키지 버전이 'DateTime' 표시기로 설정되었을 때 패키지 자동 복원이 무한 루프로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="75602-123">Occassionally, when you use a package containing an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes package auto-restore to run in infinite loop.</span></span> [<span data-ttu-id="75602-124">NuGet#4542</span><span class="sxs-lookup"><span data-stu-id="75602-124">NuGet#4542</span></span>](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a><span data-ttu-id="75602-125">해결 방법</span><span class="sxs-lookup"><span data-stu-id="75602-125">Workaround</span></span>

<span data-ttu-id="75602-126">지금은 해결 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75602-126">There is no workaround at this time.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="75602-127">NuGet 패키지 관리자를 사용하여 DotNetCLITools를 보거나 추가 또는 업데이트할 수 없음</span><span class="sxs-lookup"><span data-stu-id="75602-127">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="75602-128">문제</span><span class="sxs-lookup"><span data-stu-id="75602-128">Issue</span></span>

<span data-ttu-id="75602-129">NuGet 패키지 관리자는 DotNetCLITools 추가/업데이트를 표시하지 않으며 허용하지도 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75602-129">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="75602-130">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="75602-130">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="75602-131">해결 방법</span><span class="sxs-lookup"><span data-stu-id="75602-131">Workaround</span></span>

<span data-ttu-id="75602-132">프로젝트 파일에서 DotNetCLIToolReferences를 수동으로 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75602-132">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a><span data-ttu-id="75602-133">프로젝트에 대해 PackageId 속성을 설정하면 NuGet 복원이 실패함</span><span class="sxs-lookup"><span data-stu-id="75602-133">NuGet restore will fail when you set PackageId property for projects</span></span>

#### <a name="issue"></a><span data-ttu-id="75602-134">문제</span><span class="sxs-lookup"><span data-stu-id="75602-134">Issue</span></span>

<span data-ttu-id="75602-135">.NET Core 프로젝트의 경우 Visual Studio의 NuGet 복원에 프로젝트의 PackageId 속성이 반영되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75602-135">For .NET Core projects, NuGet restore in Visual Studio does not respect PackageId property of projects.</span></span> [<span data-ttu-id="75602-136">NuGet#4586</span><span class="sxs-lookup"><span data-stu-id="75602-136">NuGet#4586</span></span>](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a><span data-ttu-id="75602-137">해결 방법</span><span class="sxs-lookup"><span data-stu-id="75602-137">Workaround</span></span>

<span data-ttu-id="75602-138">명령줄을 사용하여 복원을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="75602-138">Run restore using the command-line.</span></span>

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a><span data-ttu-id="75602-139">프로젝트에 'obj' 폴더가 없는 경우 패키지 복원에 실패할 수 있음</span><span class="sxs-lookup"><span data-stu-id="75602-139">When your project does not have 'obj' folder, package restore may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="75602-140">문제</span><span class="sxs-lookup"><span data-stu-id="75602-140">Issue</span></span>

<span data-ttu-id="75602-141">'obj' 폴더가 삭제된 경우 Visual Studio에서 PackageReferences를 복원하지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="75602-141">Visual Studio fails to restore PackageReferences when 'obj' folder has been deleted.</span></span> [<span data-ttu-id="75602-142">NuGet#4528</span><span class="sxs-lookup"><span data-stu-id="75602-142">NuGet#4528</span></span>](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a><span data-ttu-id="75602-143">해결 방법</span><span class="sxs-lookup"><span data-stu-id="75602-143">Workaround</span></span>

<span data-ttu-id="75602-144">수동으로 'obj' 폴더를 만들면 복원이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="75602-144">Create 'obj' folder manually and the restore should work.</span></span>

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a><span data-ttu-id="75602-145">콘솔에서 Update-Package를 사용하여 패키지를 수동으로 업데이트하면 실패할 수 있음</span><span class="sxs-lookup"><span data-stu-id="75602-145">Manually updating packages using Update-Package in console may fail</span></span>

#### <a name="issue"></a><span data-ttu-id="75602-146">문제</span><span class="sxs-lookup"><span data-stu-id="75602-146">Issue</span></span>

<span data-ttu-id="75602-147">방금 변환된 PackageReferences 프로젝트에 대해 한 번만 콘솔에서 Update-Package를 수동으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75602-147">Using Update-Package manually in the console only works once for PackageReferences projects that were just converted.</span></span> [<span data-ttu-id="75602-148">NuGet#4431</span><span class="sxs-lookup"><span data-stu-id="75602-148">NuGet#4431</span></span>](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a><span data-ttu-id="75602-149">해결 방법</span><span class="sxs-lookup"><span data-stu-id="75602-149">Workaround</span></span>

<span data-ttu-id="75602-150">지금은 해결 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75602-150">There is no workaround at this time.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="75602-151">대상 프레임워크 버전의 대상을 변경하면 불완전한 IntelliSense가 발생할 수 있음</span><span class="sxs-lookup"><span data-stu-id="75602-151">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="75602-152">문제</span><span class="sxs-lookup"><span data-stu-id="75602-152">Issue</span></span>

<span data-ttu-id="75602-153">Visual Studio에서 대상 프레임워크 버전의 대상을 변경하면 불완전한 IntelliSense가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75602-153">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="75602-154">이 문제는 PackageReferences를 패키지 관리자 형식으로 사용하는 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="75602-154">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="75602-155">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="75602-155">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="75602-156">해결 방법</span><span class="sxs-lookup"><span data-stu-id="75602-156">Workaround</span></span>

<span data-ttu-id="75602-157">수동 복원을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="75602-157">Do a manual restore.</span></span>

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a><span data-ttu-id="75602-158">.NET461을 대상으로 하는 프로젝트가 .NETStandard를 대상으로 하는 다른 프로젝트를 참조하는 경우 msbuild /t:restore가 실패함</span><span class="sxs-lookup"><span data-stu-id="75602-158">msbuild /t:restore fails when a project targeting .NET461 references another project targeting .NETStandard</span></span>

#### <a name="issue"></a><span data-ttu-id="75602-159">문제</span><span class="sxs-lookup"><span data-stu-id="75602-159">Issue</span></span>

<span data-ttu-id="75602-160">.NET461을 대상으로 하는 PackageReference 기반 프로젝트가 .NETStandard를 대상으로 하는 다른 PackageReference 기반 프로젝트를 참조하는 경우 msbuild /t:restore가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="75602-160">msbuild /t:restore fails when a PackageReferenece based project targeting .NET461 references another PackageReference based project targeting .NETStandard.</span></span>  [<span data-ttu-id="75602-161">NuGet#4532</span><span class="sxs-lookup"><span data-stu-id="75602-161">NuGet#4532</span></span>](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a><span data-ttu-id="75602-162">해결 방법</span><span class="sxs-lookup"><span data-stu-id="75602-162">Workaround</span></span>

<span data-ttu-id="75602-163">지금은 해결 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75602-163">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a><span data-ttu-id="75602-164">NuGet 4.0 RTM 기간에서 수정된 문제</span><span class="sxs-lookup"><span data-stu-id="75602-164">Issues fixed in NuGet 4.0 RTM timeframe</span></span>

<span data-ttu-id="75602-165">[NuGet 4.0 RC 릴리스 정보](../release-notes/nuget-4.0-RC.md) - NuGet 4.0 RC에서 수정된 모든 문제를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="75602-165">[NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md) - Lists all the issues fixed for NuGet 4.0 RC</span></span>

### <a name="features"></a><span data-ttu-id="75602-166">기능</span><span class="sxs-lookup"><span data-stu-id="75602-166">Features</span></span>

- <span data-ttu-id="75602-167">NuGet.Core.sln의 문자열을 지역화합니다. - [#2041](https://github.com/NuGet/Home/issues/2041)</span><span class="sxs-lookup"><span data-stu-id="75602-167">Localize strings in NuGet.Core.sln - [#2041](https://github.com/NuGet/Home/issues/2041)</span></span>

- <span data-ttu-id="75602-168">Nuget은 LSL 모드에서 웹 응용 프로그램 프로젝트를 강제로 로드합니다. - [#4258](https://github.com/NuGet/Home/issues/4258)</span><span class="sxs-lookup"><span data-stu-id="75602-168">Nuget forces to load web application projects in LSL mode - [#4258](https://github.com/NuGet/Home/issues/4258)</span></span>

- <span data-ttu-id="75602-169">UI에서 "SDK가 설치된" 패키지에 대한 버전 변경을 차단하기 위해 AutoReferenced PackageReference를 지원합니다. - [#4044](https://github.com/NuGet/Home/issues/4044)</span><span class="sxs-lookup"><span data-stu-id="75602-169">AutoReferenced PackageReference support to block version changes in UI for "sdk installed" packages - [#4044](https://github.com/NuGet/Home/issues/4044)</span></span>

- <span data-ttu-id="75602-170">모든 프로젝트 종속성에 대해 PackageSpec.Version을 올바르게 전달합니다(PackageRef). - [#3902](https://github.com/NuGet/Home/issues/3902)</span><span class="sxs-lookup"><span data-stu-id="75602-170">Correctly communicate PackageSpec.Version for any project dependencies (PackageRef) - [#3902](https://github.com/NuGet/Home/issues/3902)</span></span>

- <span data-ttu-id="75602-171">명령줄에서 `.csproj`로부터 참조를 제거하는 기능을 지원합니다. - [#4101](https://github.com/NuGet/Home/issues/4101)</span><span class="sxs-lookup"><span data-stu-id="75602-171">support for removing references into `.csproj` from commandline(s) - [#4101](https://github.com/NuGet/Home/issues/4101)</span></span>

- <span data-ttu-id="75602-172">PackageReference 프로젝트(일반 및 xplat) 및 경량 솔루션 로드에 대한 복원을 지원합니다. - [#4003](https://github.com/NuGet/Home/issues/4003)</span><span class="sxs-lookup"><span data-stu-id="75602-172">Support restore for PackageReference projects (normal and xplat) and Lightweight Solution Load - [#4003](https://github.com/NuGet/Home/issues/4003)</span></span>

- <span data-ttu-id="75602-173">명령줄에서 `.csproj`에 참조를 추가하는 기능을 지원합니다. - [#3751](https://github.com/NuGet/Home/issues/3751)</span><span class="sxs-lookup"><span data-stu-id="75602-173">support for adding references into `.csproj` from commandline(s) - [#3751](https://github.com/NuGet/Home/issues/3751)</span></span>

- <span data-ttu-id="75602-174">`packages.config` 또는 `project.json`의 경량 솔루션 로드에 대한 NuGet 복원을 지원합니다. - [#3711](https://github.com/NuGet/Home/issues/3711)</span><span class="sxs-lookup"><span data-stu-id="75602-174">Support NuGet restore for Lightweight Solution Load for `packages.config` or `project.json` - [#3711](https://github.com/NuGet/Home/issues/3711)</span></span>

- <span data-ttu-id="75602-175">nuget에서 생성된 targets 파일에서 contentFiles를 지원합니다. - [#3683](https://github.com/NuGet/Home/issues/3683)</span><span class="sxs-lookup"><span data-stu-id="75602-175">contentFiles support in nuget generated targets file - [#3683](https://github.com/NuGet/Home/issues/3683)</span></span>

- <span data-ttu-id="75602-176">MSBuild를 사용하여 Mac에서 nuget.exe 유효성 검사에 대한 Mono CI를 설정합니다. - [#3646](https://github.com/NuGet/Home/issues/3646)</span><span class="sxs-lookup"><span data-stu-id="75602-176">Establish a Mono CI for nuget.exe validation on Mac using MSBuild - [#3646](https://github.com/NuGet/Home/issues/3646)</span></span>

- <span data-ttu-id="75602-177">v2 NuGet.Core 종속성에서 NuGet을 이동합니다. - [#3645](https://github.com/NuGet/Home/issues/3645)</span><span class="sxs-lookup"><span data-stu-id="75602-177">Move NuGet off of v2 NuGet.Core dependencies - [#3645](https://github.com/NuGet/Home/issues/3645)</span></span>

### <a name="bugs"></a><span data-ttu-id="75602-178">버그</span><span class="sxs-lookup"><span data-stu-id="75602-178">Bugs</span></span>

- <span data-ttu-id="75602-179">Visual Studio의 NuGet restore에서 프로젝트의 PackageId 속성이 적용되지 않습니다. - [#4586](https://github.com/NuGet/Home/issues/4586)</span><span class="sxs-lookup"><span data-stu-id="75602-179">NuGet restore in Visual Studio does not respect PackageId property of projects - [#4586](https://github.com/NuGet/Home/issues/4586)</span></span>

- <span data-ttu-id="75602-180">vsix 패키지에 패키지를 추가하면 NuGet ProjectSystemCache 오류가 발생합니다. - [#4545](https://github.com/NuGet/Home/issues/4545)</span><span class="sxs-lookup"><span data-stu-id="75602-180">NuGet ProjectSystemCache error when adding package in vsix package - [#4545](https://github.com/NuGet/Home/issues/4545)</span></span>

- <span data-ttu-id="75602-181">IncludeSource가 여러 TFM이 있는 프로젝트에서 사용되는 경우 Pack에서 예외를 throw합니다. - [#4536](https://github.com/NuGet/Home/issues/4536)</span><span class="sxs-lookup"><span data-stu-id="75602-181">Pack throws exception if IncludeSource is used in a project with multiple TFMs - [#4536](https://github.com/NuGet/Home/issues/4536)</span></span>

- <span data-ttu-id="75602-182">솔루션 전체 패키지 관리에서 업데이트를 사용하면 VS 2017 RC3 작동이 중단됩니다. - [#4474](https://github.com/NuGet/Home/issues/4474)</span><span class="sxs-lookup"><span data-stu-id="75602-182">VS 2017 RC3 crashes on using update from Solution-wide package management - [#4474](https://github.com/NuGet/Home/issues/4474)</span></span>

- <span data-ttu-id="75602-183">새로 설치된 패키지를 제거할 수 없습니다. - [#4435](https://github.com/NuGet/Home/issues/4435)</span><span class="sxs-lookup"><span data-stu-id="75602-183">Cannot uninstall newly installed package  - [#4435](https://github.com/NuGet/Home/issues/4435)</span></span>

- <span data-ttu-id="75602-184">PackageRef로 마이그레이션하면 하이브리드 솔루션에 이상한 복원 동작이 발생합니다. - [#4433](https://github.com/NuGet/Home/issues/4433)</span><span class="sxs-lookup"><span data-stu-id="75602-184">When migrating to PackageRef, hybrid solutions have strange restore behavior - [#4433](https://github.com/NuGet/Home/issues/4433)</span></span>

- <span data-ttu-id="75602-185">NuGet 작업(install, update, restore)을 시작한 직후에 빌드하면 VS가 중단될 수 있습니다. - [#4420](https://github.com/NuGet/Home/issues/4420)</span><span class="sxs-lookup"><span data-stu-id="75602-185">Building soon after starting NuGet operation (install, update, restore), can cause VS to Hang - [#4420](https://github.com/NuGet/Home/issues/4420)</span></span>

- <span data-ttu-id="75602-186">UI 중단 - NuGet.SolutionRestoreManager.RestoreManagerPackage 초기화 시 교착 상태 - [#4371](https://github.com/NuGet/Home/issues/4371)</span><span class="sxs-lookup"><span data-stu-id="75602-186">UI Hang - Deadlock initializing NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)</span></span>

- <span data-ttu-id="75602-187">패키지 추가 명령은 요소 대신 버전을 특성으로 추가해야 합니다. - [#4325](https://github.com/NuGet/Home/issues/4325)</span><span class="sxs-lookup"><span data-stu-id="75602-187">add package command should add version as attribute instead of element - [#4325](https://github.com/NuGet/Home/issues/4325)</span></span>

- <span data-ttu-id="75602-188">dotnet</span><span class="sxs-lookup"><span data-stu-id="75602-188">dotnet</span></span>
  - <span data-ttu-id="75602-189">dotnetcore Restore foo.sln - SLN의 구성으로 인해 복원 그래프에서 중복(그러나 구성과 다름) 프로젝트가 발생하면 실패합니다. - [#4316](https://github.com/NuGet/Home/issues/4316)</span><span class="sxs-lookup"><span data-stu-id="75602-189">dotnetcore Restore foo.sln -- fails when configurations in SLN cause duplicate (but diff config) projects in restore graph - [#4316](https://github.com/NuGet/Home/issues/4316)</span></span>

- <span data-ttu-id="75602-190">콘텐츠 전용 패키지 - [#3668](https://github.com/NuGet/Home/issues/3668)</span><span class="sxs-lookup"><span data-stu-id="75602-190">Content only packages - [#3668](https://github.com/NuGet/Home/issues/3668)</span></span>

- <span data-ttu-id="75602-191">기본적으로 패키지 형식 선택기 옵션을 선택 취소합니다. - [#4468](https://github.com/NuGet/Home/issues/4468)</span><span class="sxs-lookup"><span data-stu-id="75602-191">By default opt out of package format selector option - [#4468](https://github.com/NuGet/Home/issues/4468)</span></span>

- <span data-ttu-id="75602-192">성능: CreateUAP_CSharp_VS.01.1.Create 프로젝트에서 Duration_TotalElapsedTime을 3,153.570ms(149.1%)만큼 재귀했습니다.</span><span class="sxs-lookup"><span data-stu-id="75602-192">Perf: CreateUAP_CSharp_VS.01.1.Create project regressed Duration_TotalElapsedTime by 3,153.570 ms (149.1%).</span></span> <span data-ttu-id="75602-193">기준 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span><span class="sxs-lookup"><span data-stu-id="75602-193">Baseline 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)</span></span>

- <span data-ttu-id="75602-194">성능: ManagedLangs_CS_DDRIT.0300.Rebuild 솔루션에서 Duration_TotalElapsedTime을 1.5초만큼 재귀했습니다.</span><span class="sxs-lookup"><span data-stu-id="75602-194">Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Solution regressed Duration_TotalElapsedTime by 1.5sec.</span></span> <span data-ttu-id="75602-195">기준 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span><span class="sxs-lookup"><span data-stu-id="75602-195">Baseline 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)</span></span>

- <span data-ttu-id="75602-196">다중 TFM 프로젝트에서 지정 유효성 검사가 실패합니다. - [#4419](https://github.com/NuGet/Home/issues/4419)</span><span class="sxs-lookup"><span data-stu-id="75602-196">Nomination fails in multi-TFM projects - [#4419](https://github.com/NuGet/Home/issues/4419)</span></span>

- <span data-ttu-id="75602-197">성능: WebForms_DDRIT.1200.Close 솔루션에서 VM_ImagesInMemory_Total_devenv를 3.000개(0.5%)만큼 재귀했습니다.</span><span class="sxs-lookup"><span data-stu-id="75602-197">Perf: WebForms_DDRIT.1200.Close Solution regressed VM_ImagesInMemory_Total_devenv by 3.000 Count (0.5%).</span></span> <span data-ttu-id="75602-198">기준 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span><span class="sxs-lookup"><span data-stu-id="75602-198">Baseline 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)</span></span>

- <span data-ttu-id="75602-199">vsfeedback - netcoreapp1.1을 대상으로 지정하면 경고가 표시됩니다. - [#4397](https://github.com/NuGet/Home/issues/4397)</span><span class="sxs-lookup"><span data-stu-id="75602-199">vsfeedback - Pack warnings when targeting netcoreapp1.1 - [#4397](https://github.com/NuGet/Home/issues/4397)</span></span>

- <span data-ttu-id="75602-200">빈 ASP.NET Core 웹 응용 프로그램에 NuGet 패키지를 추가하려고 하면 PathTooLongException이 발생합니다. - [#4391](https://github.com/NuGet/Home/issues/4391)</span><span class="sxs-lookup"><span data-stu-id="75602-200">PathTooLongException when trying to add a NuGet package to empty ASP.NET Core web application - [#4391](https://github.com/NuGet/Home/issues/4391)</span></span>

- <span data-ttu-id="75602-201">Pack이 너무 자주 실행됨 -- dotnet</span><span class="sxs-lookup"><span data-stu-id="75602-201">Pack runs too often -- dotnet</span></span>
  - <span data-ttu-id="75602-202">“Pack” 대상과 관련된 대상 종속성 그래프에 순환 종속성이 있으므로 dotnetcore pack이 실패합니다. - [#4381](https://github.com/NuGet/Home/issues/4381)</span><span class="sxs-lookup"><span data-stu-id="75602-202">dotnetcore pack fails with There is a circular dependency in the target dependency graph involving target "Pack"  - [#4381](https://github.com/NuGet/Home/issues/4381)</span></span>

- <span data-ttu-id="75602-203">Pack이 너무 자주 실행됨 - NuGet 패키지 생성에 모든 구성이 포함되지 않습니다. - [#4380](https://github.com/NuGet/Home/issues/4380)</span><span class="sxs-lookup"><span data-stu-id="75602-203">Pack runs too often -- Generate NuGet package doesn't include all the configurations  - [#4380](https://github.com/NuGet/Home/issues/4380)</span></span>

- <span data-ttu-id="75602-204">NullReferenceException - C++ 프로젝트에서 packageref가 포함된 nuget을 추가했습니다. - [#4378](https://github.com/NuGet/Home/issues/4378)</span><span class="sxs-lookup"><span data-stu-id="75602-204">NullReferenceException adding  nuget with packageref in  C++  project - [#4378](https://github.com/NuGet/Home/issues/4378)</span></span>

- <span data-ttu-id="75602-205">내게 필요한 옵션: 내레이터에서 패키지를 설치할 프로젝트를 선택하는 확인란을 설명하지 않습니다. - [#4366](https://github.com/NuGet/Home/issues/4366)</span><span class="sxs-lookup"><span data-stu-id="75602-205">Accessibility : Narrator does not narrate the checkbox to select the projects to install the package to - [#4366](https://github.com/NuGet/Home/issues/4366)</span></span>

- <span data-ttu-id="75602-206">NuGet VS17에서 VSO/VSTS 피드에 연결하는 데 산발적으로 실패합니다(VS 버그 365798). - [#4365](https://github.com/NuGet/Home/issues/4365)</span><span class="sxs-lookup"><span data-stu-id="75602-206">NuGet VS17 sporadically fails connecting to VSO/VSTS feeds - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)</span></span>

- <span data-ttu-id="75602-207">PackagePath에서 path를 "contentFiles"로 지정하면 contentFiles가 잘못된 위치로 출력됩니다. - [#4348](https://github.com/NuGet/Home/issues/4348)</span><span class="sxs-lookup"><span data-stu-id="75602-207">contentFiles get output to wrong location if PackagePath specifies path as "contentFiles" - [#4348](https://github.com/NuGet/Home/issues/4348)</span></span>

- <span data-ttu-id="75602-208">Pack 대상에서 VersionSuffix를 사용하여 PackageVersion 속성을 추가합니다. - [#4324](https://github.com/NuGet/Home/issues/4324)</span><span class="sxs-lookup"><span data-stu-id="75602-208">Pack target appends PackageVersion property with VersionSuffix - [#4324](https://github.com/NuGet/Home/issues/4324)</span></span>

- <span data-ttu-id="75602-209">dotnet pack에서 패키지 경로 지정이 작동하지 않습니다. - [#4321](https://github.com/NuGet/Home/issues/4321)</span><span class="sxs-lookup"><span data-stu-id="75602-209">Specifying package path doesn't work with dotnet pack - [#4321](https://github.com/NuGet/Home/issues/4321)</span></span>

- <span data-ttu-id="75602-210">NuGet에서 복원하는 동안 중복 가져오기에 대한 많은 경고를 출력합니다. - [#4304](https://github.com/NuGet/Home/issues/4304)</span><span class="sxs-lookup"><span data-stu-id="75602-210">NuGet outputs a bunch of warnings about duplicate imports during restore - [#4304](https://github.com/NuGet/Home/issues/4304)</span></span>

- <span data-ttu-id="75602-211">"NuGet 패키지 관리자 형식 선택" 대화 상자가 어두운 테마에서 제대로 표시되지 않습니다. - [#4300](https://github.com/NuGet/Home/issues/4300)</span><span class="sxs-lookup"><span data-stu-id="75602-211">Choose "NuGet Package Manager Format" dialog looks bad under dark theme - [#4300](https://github.com/NuGet/Home/issues/4300)</span></span>

- <span data-ttu-id="75602-212">빌드 복원 시 VS 작동이 중단됩니다. - [#4298](https://github.com/NuGet/Home/issues/4298)</span><span class="sxs-lookup"><span data-stu-id="75602-212">VS crash on build restore - [#4298](https://github.com/NuGet/Home/issues/4298)</span></span>

- <span data-ttu-id="75602-213">targetframeworks에 TFM을 추가하고 저장한 다음 빌드하면 Visual Studio 교착 상태가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="75602-213">Visual Studio deadlocks if you add TFM in targetframeworks, save, then build.</span></span> <span data-ttu-id="75602-214">시간의 10% - [#4295](https://github.com/NuGet/Home/issues/4295)</span><span class="sxs-lookup"><span data-stu-id="75602-214">10% of time - [#4295](https://github.com/NuGet/Home/issues/4295)</span></span>

- <span data-ttu-id="75602-215">nuget pack에서 프로젝트를 성공적으로 압축했지만 성공 메시지를 출력하지 않습니다. - [#4294](https://github.com/NuGet/Home/issues/4294)</span><span class="sxs-lookup"><span data-stu-id="75602-215">nuget pack does not output success message on packing a project successfully - [#4294](https://github.com/NuGet/Home/issues/4294)</span></span>

- <span data-ttu-id="75602-216">System.IO.Compression 4.1을 찾을 수 없어 PackTask가 실패합니다. - [#4290](https://github.com/NuGet/Home/issues/4290)</span><span class="sxs-lookup"><span data-stu-id="75602-216">PackTask fails due to System.IO.Compression 4.1 not being found - [#4290](https://github.com/NuGet/Home/issues/4290)</span></span>

- <span data-ttu-id="75602-217">Pack이 너무 자주 실행됨 - 파일 액세스 충돌로 인해 PackTask가 자주 실패합니다. - [#4289](https://github.com/NuGet/Home/issues/4289)</span><span class="sxs-lookup"><span data-stu-id="75602-217">Pack runs too often -- PackTask frequently fails with file access conflict - [#4289](https://github.com/NuGet/Home/issues/4289)</span></span>

- <span data-ttu-id="75602-218">NuGet에서 백그라운드 복원 중에 출력 창을 엽니다. - [#4274](https://github.com/NuGet/Home/issues/4274)</span><span class="sxs-lookup"><span data-stu-id="75602-218">NuGet opens the output window during background restore - [#4274](https://github.com/NuGet/Home/issues/4274)</span></span>

- <span data-ttu-id="75602-219">ServiceProvider를 위험한 코딩 패턴으로 제거합니다(중단이 발생할 수 있음). - [#4268](https://github.com/NuGet/Home/issues/4268)</span><span class="sxs-lookup"><span data-stu-id="75602-219">Eliminate ServiceProvider as dangerous coding pattern (which can cause hangs) - [#4268](https://github.com/NuGet/Home/issues/4268)</span></span>

- <span data-ttu-id="75602-220">성능/UI 중지 - DownloadTimeoutStream 읽기가 향상되었습니다. - [#4266](https://github.com/NuGet/Home/issues/4266)</span><span class="sxs-lookup"><span data-stu-id="75602-220">Perf/UIHang - Improve DownloadTimeoutStream reads - [#4266](https://github.com/NuGet/Home/issues/4266)</span></span>

- <span data-ttu-id="75602-221">nuget restore가 완료되기 전에 프로젝트를 닫으려고 하면 Visual Studio 교착 상태가 발생합니다. - [#4257](https://github.com/NuGet/Home/issues/4257)</span><span class="sxs-lookup"><span data-stu-id="75602-221">Visual Studio deadlocks if you attempt to close a project before NuGet restore has finished - [#4257](https://github.com/NuGet/Home/issues/4257)</span></span>

- <span data-ttu-id="75602-222">PackTask 및 `.nuspec` 압축 관련 문제 - [#4250](https://github.com/NuGet/Home/issues/4250)</span><span class="sxs-lookup"><span data-stu-id="75602-222">Issues with PackTask and packing `.nuspec` - [#4250](https://github.com/NuGet/Home/issues/4250)</span></span>

- <span data-ttu-id="75602-223">[vsfeedback] 새 프로젝트에서 NuGet 패키지를 확인할 수 없습니다(Visual Studio를 다시 시작해야 함). - [#4217](https://github.com/NuGet/Home/issues/4217)</span><span class="sxs-lookup"><span data-stu-id="75602-223">[vsfeedback] Cannot resolve nuget packages on new project (needs to restart visual studio) - [#4217](https://github.com/NuGet/Home/issues/4217)</span></span>

- <span data-ttu-id="75602-224">[vsfeedback] 사용 가능한 패키지 버전을 표시하는 "Version" 드롭다운에서 선택한 NuGet 패키지와 동기화 상태를 유지하기가 어렵습니다. - [#4198](https://github.com/NuGet/Home/issues/4198)</span><span class="sxs-lookup"><span data-stu-id="75602-224">[vsfeedback] The "Version" drop down that shows available package versions, struggles to stay in-sync with the selected nuGet package...  - [#4198](https://github.com/NuGet/Home/issues/4198)</span></span>

- <span data-ttu-id="75602-225">Nuget.Client에서 CPS와 상호 작용하여 교착 상태를 방지하는 경우 CPS JoinableTaskFactory를 사용해야 합니다. - [#4185](https://github.com/NuGet/Home/issues/4185)</span><span class="sxs-lookup"><span data-stu-id="75602-225">Nuget.Client should use CPS JoinableTaskFactory when interacting with CPS to prevent deadlocks - [#4185](https://github.com/NuGet/Home/issues/4185)</span></span>

- <span data-ttu-id="75602-226">NuGet 3.5.0에서 패키지의 `.targets`를 압축 해제하지 않습니다. - [#4171](https://github.com/NuGet/Home/issues/4171)</span><span class="sxs-lookup"><span data-stu-id="75602-226">NuGet 3.5.0 not unpacking `.targets` from package - [#4171](https://github.com/NuGet/Home/issues/4171)</span></span>

- <span data-ttu-id="75602-227">dotnet</span><span class="sxs-lookup"><span data-stu-id="75602-227">dotnet</span></span>
  - <span data-ttu-id="75602-228">dotnetcore pack에서 `.csproj`의 제목을 지원하지 않습니다. - [#4150](https://github.com/NuGet/Home/issues/4150)</span><span class="sxs-lookup"><span data-stu-id="75602-228">dotnetcore pack does not support title in `.csproj` - [#4150](https://github.com/NuGet/Home/issues/4150)</span></span>

- <span data-ttu-id="75602-229">VS2017 RC에서 Install-Package가 오류 대화 상자를 표시합니다. - [#4127](https://github.com/NuGet/Home/issues/4127)</span><span class="sxs-lookup"><span data-stu-id="75602-229">Install-Package results in error dialog in VS2017 RC - [#4127](https://github.com/NuGet/Home/issues/4127)</span></span>

- <span data-ttu-id="75602-230">UI에서 지정된 위치의 CPS 업데이트를 가져오지 않으므로 .NET Core 프로젝트에 대한 패키지 업데이트가 작동하지 않는 것으로 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="75602-230">Updating a package for .net core project appears to not work, as the UI doesn't get the CPS update from the nominate.</span></span><span data-ttu-id="75602-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span><span class="sxs-lookup"><span data-stu-id="75602-231"> - [#4035](https://github.com/NuGet/Home/issues/4035)</span></span>

- <span data-ttu-id="75602-232">확인되지 않은 참조 경고가 향상되었습니다. - [#3955](https://github.com/NuGet/Home/issues/3955)</span><span class="sxs-lookup"><span data-stu-id="75602-232">Improve unresolved reference warning - [#3955](https://github.com/NuGet/Home/issues/3955)</span></span>

- <span data-ttu-id="75602-233">dotnet</span><span class="sxs-lookup"><span data-stu-id="75602-233">dotnet</span></span>
  - <span data-ttu-id="75602-234">dotnetcore pack - ProjectReference에서 버전 정보가 손실됩니다. - [#3953](https://github.com/NuGet/Home/issues/3953)</span><span class="sxs-lookup"><span data-stu-id="75602-234">dotnetcore pack - ProjectReference loses version information - [#3953](https://github.com/NuGet/Home/issues/3953)</span></span>

- <span data-ttu-id="75602-235">UWP 앱 만들기 프로젝트 생성 및 총 경과 시간 재귀 다시 빌드 - [#3873](https://github.com/NuGet/Home/issues/3873)</span><span class="sxs-lookup"><span data-stu-id="75602-235">Create UWP app create project & rebuild total elapsed time regressions - [#3873](https://github.com/NuGet/Home/issues/3873)</span></span>

- <span data-ttu-id="75602-236">복원 중에 오류가 발생한 후에도 성공적인 복원 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="75602-236">Successful restore message is displayed even after error during restore.</span></span><span data-ttu-id="75602-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span><span class="sxs-lookup"><span data-stu-id="75602-237"> - [#3799](https://github.com/NuGet/Home/issues/3799)</span></span>

- <span data-ttu-id="75602-238">Nuget.CommandLine 3.4.4를 Nuget.org에 다시 게시합니다. - [#2931](https://github.com/NuGet/Home/issues/2931)</span><span class="sxs-lookup"><span data-stu-id="75602-238">re-Publish Nuget.CommandLine 3.4.4 to Nuget.org - [#2931](https://github.com/NuGet/Home/issues/2931)</span></span>

- <span data-ttu-id="75602-239">마이그레이션 시 프로젝트가 `project.json`에서 `.csproj`로 변경되면 복원이 실패합니다. - [#4297](https://github.com/NuGet/Home/issues/4297)</span><span class="sxs-lookup"><span data-stu-id="75602-239">On Migrate, projects change from `project.json` to `.csproj` --- restore fails - [#4297](https://github.com/NuGet/Home/issues/4297)</span></span>

- <span data-ttu-id="75602-240">새로 만든 xunit 테스트 프로젝트에서 복원이 실패합니다. - [#4296](https://github.com/NuGet/Home/issues/4296)</span><span class="sxs-lookup"><span data-stu-id="75602-240">Restore failing on newly created xunit Test project  - [#4296](https://github.com/NuGet/Home/issues/4296)</span></span>

- <span data-ttu-id="75602-241">Core 프로젝트가 중단되고 열린 상태에서 UI를 잠글 수 있습니다. - [#4269](https://github.com/NuGet/Home/issues/4269)</span><span class="sxs-lookup"><span data-stu-id="75602-241">Core projects can hang, lock up UI on open - [#4269](https://github.com/NuGet/Home/issues/4269)</span></span>

- <span data-ttu-id="75602-242">빌드 작업에 대한 대상 파일을 수정합니다. - [#4267](https://github.com/NuGet/Home/issues/4267)</span><span class="sxs-lookup"><span data-stu-id="75602-242">fix targets file for build tasks - [#4267](https://github.com/NuGet/Home/issues/4267)</span></span>

- <span data-ttu-id="75602-243">참조된 프로젝트를 언로드하는 솔루션을 빌드한 후에 오류 목록에 오류가 있습니다. - [#4208](https://github.com/NuGet/Home/issues/4208)</span><span class="sxs-lookup"><span data-stu-id="75602-243">Error list has error after build solution which unload the referenced project - [#4208](https://github.com/NuGet/Home/issues/4208)</span></span>

- <span data-ttu-id="75602-244">MSB4057: "_GenerateRestoreGraphProjectEntry" 대상이 프로젝트에 존재하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75602-244">MSB4057: The target "_GenerateRestoreGraphProjectEntry" does not exist in the project.</span></span><span data-ttu-id="75602-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span><span class="sxs-lookup"><span data-stu-id="75602-245"> - [#4194](https://github.com/NuGet/Home/issues/4194)</span></span>

- <span data-ttu-id="75602-246">vsfeedback: 모든 프로젝트를 선택하면 솔루션에 대한 NuGet 관리자 UI 작동이 중단됩니다. - [#4191](https://github.com/NuGet/Home/issues/4191)</span><span class="sxs-lookup"><span data-stu-id="75602-246">vsfeedback: nuget manager ui for solution crashes when you select all projects - [#4191](https://github.com/NuGet/Home/issues/4191)</span></span>

- <span data-ttu-id="75602-247">후행 슬래시가 있으면 nuget.exe msbuildpath가 실패합니다. - [#4180](https://github.com/NuGet/Home/issues/4180)</span><span class="sxs-lookup"><span data-stu-id="75602-247">nuget.exe msbuildpath fails when there is a trailing slash - [#4180](https://github.com/NuGet/Home/issues/4180)</span></span>

- <span data-ttu-id="75602-248">vsfeedback: nuget restore에서 LinqToTwitter 프로젝트에 대한 여러 프로젝트 참조 경고를 제공합니다 - [#4156](https://github.com/NuGet/Home/issues/4156)</span><span class="sxs-lookup"><span data-stu-id="75602-248">vsfeedback: NuGet restore give several project reference warnings for LinqToTwitter project - [#4156](https://github.com/NuGet/Home/issues/4156)</span></span>

- <span data-ttu-id="75602-249">`.csproj`의 pack에 minClientVersion 특성이 포함되지 않습니다. - [#4135](https://github.com/NuGet/Home/issues/4135)</span><span class="sxs-lookup"><span data-stu-id="75602-249">Pack from `.csproj` does not include the minClientVersion attribute  - [#4135](https://github.com/NuGet/Home/issues/4135)</span></span>

- <span data-ttu-id="75602-250">NuGet.Build.Tasks.Pack.dll이 VS2017(d15rel 26014.00)에서 지연된 서명으로 제공되었습니다. - [#4122](https://github.com/NuGet/Home/issues/4122)</span><span class="sxs-lookup"><span data-stu-id="75602-250">NuGet.Build.Tasks.Pack.dll shipped delay signed in VS2017 (d15rel 26014.00) - [#4122](https://github.com/NuGet/Home/issues/4122)</span></span>

- <span data-ttu-id="75602-251">VSFeedback: CMake 3.7.1을 사용하여 생성된 VS 2015 프로젝트에 대한 복원이 실패합니다. - [#4114](https://github.com/NuGet/Home/issues/4114)</span><span class="sxs-lookup"><span data-stu-id="75602-251">VSFeedback: Restore fails for a VS 2015 project generated with CMake 3.7.1 - [#4114](https://github.com/NuGet/Home/issues/4114)</span></span>

- <span data-ttu-id="75602-252">VSFeedback: 복원 오류로 인해 빌드에서 제공할 수 있는 완전한 오류 메시지가 손상될 수 있습니다. - [#4113](https://github.com/NuGet/Home/issues/4113)</span><span class="sxs-lookup"><span data-stu-id="75602-252">VSFeedback: Restore errors can obscure more complete error messages that build could give - [#4113](https://github.com/NuGet/Home/issues/4113)</span></span>

- <span data-ttu-id="75602-253">[VSFeedback] 웹 사이트 프로젝트에 대한 NuGet 패키지를 복원하는 동안 오류가 발생했습니다. 값은 null일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75602-253">[VSFeedback] Error occurred while restoring NuGet packages for website project: Value cannot be null.</span></span><span data-ttu-id="75602-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span><span class="sxs-lookup"><span data-stu-id="75602-254"> - [#4092](https://github.com/NuGet/Home/issues/4092)</span></span>

- <span data-ttu-id="75602-255">마이그레이션 중에 NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker에서 "개체 참조 예외"를 throw합니다. - [#4067](https://github.com/NuGet/Home/issues/4067)</span><span class="sxs-lookup"><span data-stu-id="75602-255">Migration Throws "Object reference Exception" in NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - [#4067](https://github.com/NuGet/Home/issues/4067)</span></span>

- <span data-ttu-id="75602-256">dotnet</span><span class="sxs-lookup"><span data-stu-id="75602-256">dotnet</span></span>
  - <span data-ttu-id="75602-257">dotnetcore pack에서 도구를 패키지가 빌드된 버전으로 압축해야 합니다. - [#4063](https://github.com/NuGet/Home/issues/4063)</span><span class="sxs-lookup"><span data-stu-id="75602-257">dotnetcore pack should pack tools with the versions that the package was built against - [#4063](https://github.com/NuGet/Home/issues/4063)</span></span>

- <span data-ttu-id="75602-258">복원하는 데 몇 초가 걸리는 경우 새 백그라운드 복원에서 상태 표시줄에 밀리초를 씁니다. - [#4036](https://github.com/NuGet/Home/issues/4036)</span><span class="sxs-lookup"><span data-stu-id="75602-258">New background restore writes milliseconds to status bar when it takes seconds to restore - [#4036](https://github.com/NuGet/Home/issues/4036)</span></span>

- <span data-ttu-id="75602-259">오타로 인해 모든 프로젝트 참조를 확인하지 못했습니다. - [#4018](https://github.com/NuGet/Home/issues/4018)</span><span class="sxs-lookup"><span data-stu-id="75602-259">Typo on failed to resolve all project references - [#4018](https://github.com/NuGet/Home/issues/4018)</span></span>

- <span data-ttu-id="75602-260">패키지 참조 시나리오에서 PCM 워크플로를 사용하도록 설정합니다. - [#4016](https://github.com/NuGet/Home/issues/4016)</span><span class="sxs-lookup"><span data-stu-id="75602-260">Enable PCM workflows in package reference scenarios - [#4016](https://github.com/NuGet/Home/issues/4016)</span></span>

- <span data-ttu-id="75602-261">패키지 관리자 UI에서 설치된 패키지를 찾을 수 없습니다. - [#4015](https://github.com/NuGet/Home/issues/4015)</span><span class="sxs-lookup"><span data-stu-id="75602-261">Can not find installed packages in package manager UI - [#4015](https://github.com/NuGet/Home/issues/4015)</span></span>

- <span data-ttu-id="75602-262">dotnet</span><span class="sxs-lookup"><span data-stu-id="75602-262">dotnet</span></span>
  - <span data-ttu-id="75602-263">PackagePath가 비어 있으면 dotnetcore pack이 실패합니다. - [#3993](https://github.com/NuGet/Home/issues/3993)</span><span class="sxs-lookup"><span data-stu-id="75602-263">dotnetcore pack fails when PackagePath is empty - [#3993](https://github.com/NuGet/Home/issues/3993)</span></span>

- <span data-ttu-id="75602-264">다중 사용자 시나리오에서 복원 작업이 실패합니다. - [#3897](https://github.com/NuGet/Home/issues/3897)</span><span class="sxs-lookup"><span data-stu-id="75602-264">Restore task fails in an multi user scenario - [#3897](https://github.com/NuGet/Home/issues/3897)</span></span>

- <span data-ttu-id="75602-265">NuGet Pack 작업을 사용하여 압축할 때 콘텐츠 형식을 변경할 수 없습니다. - [#3895](https://github.com/NuGet/Home/issues/3895)</span><span class="sxs-lookup"><span data-stu-id="75602-265">Cannot change Content type when packing using NuGet Pack Task - [#3895](https://github.com/NuGet/Home/issues/3895)</span></span>

- <span data-ttu-id="75602-266">MsBuild /t:pack에 대한 ContentFiles 기본 복사가 올바르지 않습니다. - [#3894](https://github.com/NuGet/Home/issues/3894)</span><span class="sxs-lookup"><span data-stu-id="75602-266">Default Copy of ContentFiles are incorrect for MsBuild /t:pack - [#3894](https://github.com/NuGet/Home/issues/3894)</span></span>

- <span data-ttu-id="75602-267">설치 패키지 복원에서 패키지 복원 메시지가 두 번 기록됩니다. - [#3785](https://github.com/NuGet/Home/issues/3785)</span><span class="sxs-lookup"><span data-stu-id="75602-267">Install package restore double logs the restoring packages message - [#3785](https://github.com/NuGet/Home/issues/3785)</span></span>

- <span data-ttu-id="75602-268">Guardrails 제거 - "runtimes" 섹션의 복원은 현재 프로젝트에만 적용해야 합니다. - [#3768](https://github.com/NuGet/Home/issues/3768)</span><span class="sxs-lookup"><span data-stu-id="75602-268">Remove Guardrails - Restore of "runtimes" section should only apply to the current project - [#3768](https://github.com/NuGet/Home/issues/3768)</span></span>

- <span data-ttu-id="75602-269">Pack 작업에서 'content/' 및 'contentFiles/' 모두에 콘텐츠 파일을 넣습니다. - [#3718](https://github.com/NuGet/Home/issues/3718)</span><span class="sxs-lookup"><span data-stu-id="75602-269">Pack task puts content files in both 'content/' and 'contentFiles/' - [#3718](https://github.com/NuGet/Home/issues/3718)</span></span>

- <span data-ttu-id="75602-270">dotnet</span><span class="sxs-lookup"><span data-stu-id="75602-270">dotnet</span></span>
  - <span data-ttu-id="75602-271">dotnetcore pack3에서 별도의 태그 분할을 수행합니다. - [#3701](https://github.com/NuGet/Home/issues/3701)</span><span class="sxs-lookup"><span data-stu-id="75602-271">dotnetcore pack3 does extra tag splitting - [#3701](https://github.com/NuGet/Home/issues/3701)</span></span>

- <span data-ttu-id="75602-272">dotnet</span><span class="sxs-lookup"><span data-stu-id="75602-272">dotnet</span></span>
  - <span data-ttu-id="75602-273">dotnetcore pack: 패키지 참조가 포함된 프로젝트를 압축하면 중복적인 가져오기 경고가 발생합니다. - [#3665](https://github.com/NuGet/Home/issues/3665)</span><span class="sxs-lookup"><span data-stu-id="75602-273">dotnetcore pack: packing projects with package references results in duplicate import warning - [#3665](https://github.com/NuGet/Home/issues/3665)</span></span>

- <span data-ttu-id="75602-274">VS에서 복원 로깅이 항상 표시되지 않습니다. - [#3633](https://github.com/NuGet/Home/issues/3633)</span><span class="sxs-lookup"><span data-stu-id="75602-274">Restore logging in VS doesn't always show - [#3633](https://github.com/NuGet/Home/issues/3633)</span></span>

- <span data-ttu-id="75602-275">nuget locals help 텍스트에서 여전히 패키지 캐시를 언급했습니다. - [#3592](https://github.com/NuGet/Home/issues/3592)</span><span class="sxs-lookup"><span data-stu-id="75602-275">nuget locals help text still mentioned packages cache - [#3592](https://github.com/NuGet/Home/issues/3592)</span></span>

- <span data-ttu-id="75602-276">Restore3에서 PackageReferences를 TargetFrameworks와 결합합니다.</span><span class="sxs-lookup"><span data-stu-id="75602-276">Restore3 couples PackageReferences with TargetFrameworks.</span></span><span data-ttu-id="75602-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span><span class="sxs-lookup"><span data-stu-id="75602-277"> - [#3504](https://github.com/NuGet/Home/issues/3504)</span></span>

- <span data-ttu-id="75602-278">Nuget이 VS "15" Preview 4 dev 명령 프롬프트에서 MSBuild의 예기치 않은</span><span class="sxs-lookup"><span data-stu-id="75602-278">Nuget picks unexpected version of MSBuild in VS "15" Preview 4 dev.</span></span> <span data-ttu-id="75602-279">버전을 선택합니다. - [#3408](https://github.com/NuGet/Home/issues/3408)</span><span class="sxs-lookup"><span data-stu-id="75602-279">command prompt - [#3408](https://github.com/NuGet/Home/issues/3408)</span></span>

- <span data-ttu-id="75602-280">실패한 복원에서 targets/props 파일을 작성합니다. - [#3399](https://github.com/NuGet/Home/issues/3399)</span><span class="sxs-lookup"><span data-stu-id="75602-280">Write out targets/props files on failed restore - [#3399](https://github.com/NuGet/Home/issues/3399)</span></span>

- <span data-ttu-id="75602-281">VS 15 명령 프롬프트에서 실행할 때 NuGet에서 복원하는 동안 MSBuild와 동일한 compat shim을 따르지 않습니다. - [#3387](https://github.com/NuGet/Home/issues/3387)</span><span class="sxs-lookup"><span data-stu-id="75602-281">NuGet during restore doesn't respect the same compat shims as MSBuild when running in VS 15 command prompt - [#3387](https://github.com/NuGet/Home/issues/3387)</span></span>

- <span data-ttu-id="75602-282">VS15에 대해 PackFromProjectWithDevelopmentDependencySet을 사용하도록 다시 설정합니다. - [#3272](https://github.com/NuGet/Home/issues/3272)</span><span class="sxs-lookup"><span data-stu-id="75602-282">Re-enable PackFromProjectWithDevelopmentDependencySet for VS15 - [#3272](https://github.com/NuGet/Home/issues/3272)</span></span>

- <span data-ttu-id="75602-283">NuGet과 관련된 Blend 문제 - [#4043](https://github.com/NuGet/Home/issues/4043)</span><span class="sxs-lookup"><span data-stu-id="75602-283">Blend problems with NuGet - [#4043](https://github.com/NuGet/Home/issues/4043)</span></span>

- <span data-ttu-id="75602-284">4.0.0.2067을 CLI 및 SDK 리포지토리에 통합하여 RC2와 함께 제공합니다. - [#4029](https://github.com/NuGet/Home/issues/4029)</span><span class="sxs-lookup"><span data-stu-id="75602-284">Integrate 4.0.0.2067 into CLI and SDK repos to ship with RC2 - [#4029](https://github.com/NuGet/Home/issues/4029)</span></span>

- <span data-ttu-id="75602-285">새 Core 콘솔 앱 만들기, 솔루션 닫기, 솔루션 열기 및 솔루션 닫기를 수행하면 VS가 중단됩니다. - [#4008](https://github.com/NuGet/Home/issues/4008)</span><span class="sxs-lookup"><span data-stu-id="75602-285">VS Hangs when you Create new Core Console App, Close Solution, Open Solution and Close Solution  - [#4008](https://github.com/NuGet/Home/issues/4008)</span></span>

- <span data-ttu-id="75602-286">d15prerel.25916.01에 대한 프로젝트 열기가 중단됩니다. - [#3982](https://github.com/NuGet/Home/issues/3982)</span><span class="sxs-lookup"><span data-stu-id="75602-286">Hitting hang opening project against d15prerel.25916.01 - [#3982](https://github.com/NuGet/Home/issues/3982)</span></span>

- <span data-ttu-id="75602-287">dotnet/nuget.exe locals doc/help 메시지를 수정합니다. - [#3919](https://github.com/NuGet/Home/issues/3919)</span><span class="sxs-lookup"><span data-stu-id="75602-287">Fix dotnet/nuget.exe locals doc/help message - [#3919](https://github.com/NuGet/Home/issues/3919)</span></span>

- <span data-ttu-id="75602-288">후행 또는 선행 공백 문제에 대한 PackTask를 검사합니다. - [#3906](https://github.com/NuGet/Home/issues/3906)</span><span class="sxs-lookup"><span data-stu-id="75602-288">Inspect PackTask for issues with trailing or leading whitespace - [#3906](https://github.com/NuGet/Home/issues/3906)</span></span>

- <span data-ttu-id="75602-289">dotnet</span><span class="sxs-lookup"><span data-stu-id="75602-289">dotnet</span></span>
  - <span data-ttu-id="75602-290">dotnetcore pack은 bin이 아닌 obj에서 압축합니다. - [#3880](https://github.com/NuGet/Home/issues/3880)</span><span class="sxs-lookup"><span data-stu-id="75602-290">dotnetcore pack is packing from obj not bin - [#3880](https://github.com/NuGet/Home/issues/3880)</span></span>

- <span data-ttu-id="75602-291">dotnet</span><span class="sxs-lookup"><span data-stu-id="75602-291">dotnet</span></span>
  - <span data-ttu-id="75602-292">dotnetcore pack에서 항상 ProjectReference 버전을 1.0.0으로 설정하는 것으로 보입니다. - [#3874](https://github.com/NuGet/Home/issues/3874)</span><span class="sxs-lookup"><span data-stu-id="75602-292">dotnetcore pack always seems to set ProjectReference version to 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)</span></span>

- <span data-ttu-id="75602-293">dotnet</span><span class="sxs-lookup"><span data-stu-id="75602-293">dotnet</span></span>
  - <span data-ttu-id="75602-294">프로젝트 참조 및 <TargetFramework>로 인해 dotnetcore pack이 실패합니다. - [#3865](https://github.com/NuGet/Home/issues/3865)</span><span class="sxs-lookup"><span data-stu-id="75602-294">dotnetcore pack fails with project references and <TargetFramework> - [#3865](https://github.com/NuGet/Home/issues/3865)</span></span>

- <span data-ttu-id="75602-295">ProjectSystemCache.TryGetProjectNameByShortName에서 LockRecursionException을 throw합니다. - [#3861](https://github.com/NuGet/Home/issues/3861)</span><span class="sxs-lookup"><span data-stu-id="75602-295">LockRecursionException in ProjectSystemCache.TryGetProjectNameByShortName - [#3861](https://github.com/NuGet/Home/issues/3861)</span></span>

- <span data-ttu-id="75602-296">MSBuild 속성에서 공백을 제거해야 합니다. - [#3819](https://github.com/NuGet/Home/issues/3819)</span><span class="sxs-lookup"><span data-stu-id="75602-296">Trim whitespace from MSBuild properties - [#3819](https://github.com/NuGet/Home/issues/3819)</span></span>

- <span data-ttu-id="75602-297">프로젝트 로드 시 발생한 두 프로젝트 이벤트를 통합합니다. - [#3759](https://github.com/NuGet/Home/issues/3759)</span><span class="sxs-lookup"><span data-stu-id="75602-297">Consolidate the two project events raised on project load - [#3759](https://github.com/NuGet/Home/issues/3759)</span></span>

- <span data-ttu-id="75602-298">`project.assets.json` 파일의 P2P 라이브러리에 잘못된 버전이 있습니다. - [#3748](https://github.com/NuGet/Home/issues/3748)</span><span class="sxs-lookup"><span data-stu-id="75602-298">P2P libraries in `project.assets.json` file have incorrect Version - [#3748](https://github.com/NuGet/Home/issues/3748)</span></span>

- <span data-ttu-id="75602-299">응답하지 않는 피드 및 사용할 수 없는 패키지로 인해 복원 작동이 중단됩니다. - [#3672](https://github.com/NuGet/Home/issues/3672)</span><span class="sxs-lookup"><span data-stu-id="75602-299">Restore crash due to unresponsive feed and unavailable package - [#3672](https://github.com/NuGet/Home/issues/3672)</span></span>

- <span data-ttu-id="75602-300">대량의 MSBuild 오류 출력에서 nuget.exe가 중단될 수 있습니다. - [#3572](https://github.com/NuGet/Home/issues/3572)</span><span class="sxs-lookup"><span data-stu-id="75602-300">nuget.exe could hang on a large amount of MSBuild error output - [#3572](https://github.com/NuGet/Home/issues/3572)</span></span>

- <span data-ttu-id="75602-301">Blend에 대한 빌드 시 복원(Restore-on-build)이 처음에는 실패하고 두 번째에 성공합니다(VS 시나리오가 수정됨). - [#2121](https://github.com/NuGet/Home/issues/2121)</span><span class="sxs-lookup"><span data-stu-id="75602-301">Restore-on-build for Blend fails first time, succeeds second time (VS scenario fixed) - [#2121](https://github.com/NuGet/Home/issues/2121)</span></span>

### <a name="dcrs"></a><span data-ttu-id="75602-302">DCR</span><span class="sxs-lookup"><span data-stu-id="75602-302">DCRs</span></span>

- <span data-ttu-id="75602-303">vsix를 v2 vsix에서 v3 vsix로 마이그레이션합니다. - [#4196](https://github.com/NuGet/Home/issues/4196)</span><span class="sxs-lookup"><span data-stu-id="75602-303">migrate vsix from v2 vsix to v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)</span></span>

- <span data-ttu-id="75602-304">MSBuild에서 잠금 파일의 경로를 가져오는 메커니즘이 NuGet에 있어야 합니다. - [#3351](https://github.com/NuGet/Home/issues/3351)</span><span class="sxs-lookup"><span data-stu-id="75602-304">NuGet should have a mechanism for getting the path to the lock file in MSBuild - [#3351](https://github.com/NuGet/Home/issues/3351)</span></span>

- <span data-ttu-id="75602-305">TFM 호환성 검사 및 자산 파일에 빌드 자산을 추가합니다. - [#3296](https://github.com/NuGet/Home/issues/3296)</span><span class="sxs-lookup"><span data-stu-id="75602-305">Add build assets to the TFM compatibility check and assets file - [#3296](https://github.com/NuGet/Home/issues/3296)</span></span>

- <span data-ttu-id="75602-306">Pack 대상에 새 ProjectCapability "Pack"을 정의하여 패키지 관련 기능을 사용하도록 설정합니다. - [#4146](https://github.com/NuGet/Home/issues/4146)</span><span class="sxs-lookup"><span data-stu-id="75602-306">Define a new ProjectCapability "Pack" in Pack targets for enabling Package related capabilities - [#4146](https://github.com/NuGet/Home/issues/4146)</span></span>

- <span data-ttu-id="75602-307">"GeneratePackageOnBuild" MSBuild 속성에 따른 빌드 후 대상으로 Pack을 실행합니다. - [#4145](https://github.com/NuGet/Home/issues/4145)</span><span class="sxs-lookup"><span data-stu-id="75602-307">Run Pack as a post build target conditioned on "GeneratePackageOnBuild" MSBuild property - [#4145](https://github.com/NuGet/Home/issues/4145)</span></span>

- <span data-ttu-id="75602-308">RestoreProjectStyle NuGet 속성을 사용하여 특정 NuGet 프로젝트를 만듭니다. - [#4134](https://github.com/NuGet/Home/issues/4134)</span><span class="sxs-lookup"><span data-stu-id="75602-308">Use NuGet property RestoreProjectStyle to create specific NuGet project - [#4134](https://github.com/NuGet/Home/issues/4134)</span></span>

- <span data-ttu-id="75602-309">전이적 프로젝트 참조 변경에 맞게 복원을 조정합니다. - [#4076](https://github.com/NuGet/Home/issues/4076)</span><span class="sxs-lookup"><span data-stu-id="75602-309">Adapt Restore for Transitive Project References change - [#4076](https://github.com/NuGet/Home/issues/4076)</span></span>

- <span data-ttu-id="75602-310">비UWP 프로젝트의 대상 파일에 NuGet 속성을 추가합니다. - [#4030](https://github.com/NuGet/Home/issues/4030)</span><span class="sxs-lookup"><span data-stu-id="75602-310">Add NuGet properties in target file for non-UWP projects - [#4030](https://github.com/NuGet/Home/issues/4030)</span></span>

- <span data-ttu-id="75602-311">UWP TargetPlatformVersion 지원 - [#3923](https://github.com/NuGet/Home/issues/3923)</span><span class="sxs-lookup"><span data-stu-id="75602-311">UWP TargetPlatformVersion support - [#3923](https://github.com/NuGet/Home/issues/3923)</span></span>

- <span data-ttu-id="75602-312">NuGet 프로젝트 시스템에 프로젝트 참조 메타데이터를 전달합니다. - [#3922](https://github.com/NuGet/Home/issues/3922)</span><span class="sxs-lookup"><span data-stu-id="75602-312">Communicate project reference metadata to NuGet project system - [#3922](https://github.com/NuGet/Home/issues/3922)</span></span>

- <span data-ttu-id="75602-313">패키징 모드에 대한 UI를 추가해야 합니다. - [#3921](https://github.com/NuGet/Home/issues/3921)</span><span class="sxs-lookup"><span data-stu-id="75602-313">Add UI for packaging mode - [#3921](https://github.com/NuGet/Home/issues/3921)</span></span>

- <span data-ttu-id="75602-314">레거시 `.csproj`에는 proj/targets에 설정된 NugetTargetMoniker 및 RuntimeIdentifiers가 있어야 합니다. - [#3854](https://github.com/NuGet/Home/issues/3854)</span><span class="sxs-lookup"><span data-stu-id="75602-314">Legacy `.csproj` needs NugetTargetMoniker and RuntimeIdentifiers set in proj/targets - [#3854](https://github.com/NuGet/Home/issues/3854)</span></span>

- <span data-ttu-id="75602-315">설치 패키지가 자동 복원과 겹칠 수 있습니다. - [#3836](https://github.com/NuGet/Home/issues/3836)</span><span class="sxs-lookup"><span data-stu-id="75602-315">Install package may overlap with auto-restore - [#3836](https://github.com/NuGet/Home/issues/3836)</span></span>

- <span data-ttu-id="75602-316">VSPackage가 로드되지 않은 경우 QueryStatus 상황에 맞는 메뉴가 발생하지 않습니다. - [#3835](https://github.com/NuGet/Home/issues/3835)</span><span class="sxs-lookup"><span data-stu-id="75602-316">Context menu QueryStatus doesn't happen when VSPackage is not loaded - [#3835](https://github.com/NuGet/Home/issues/3835)</span></span>

- <span data-ttu-id="75602-317">솔루션 복원 및 빌드 복원 대화 상자가 계속 표시됩니다. - [#3789](https://github.com/NuGet/Home/issues/3789)</span><span class="sxs-lookup"><span data-stu-id="75602-317">Solution Restore and Build Restore still show dialogs - [#3789](https://github.com/NuGet/Home/issues/3789)</span></span>

- <span data-ttu-id="75602-318">NuGet.Clients 솔루션 빌드에서 VSSDK 버전을 격리합니다. - [#3890](https://github.com/NuGet/Home/issues/3890)</span><span class="sxs-lookup"><span data-stu-id="75602-318">Isolate VSSDK version in NuGet.Clients solution build - [#3890](https://github.com/NuGet/Home/issues/3890)</span></span>

## <a name="links-to-github-issues-fixed-in-rtm"></a><span data-ttu-id="75602-319">RTM에서 수정된 GitHub 문제에 대한 링크</span><span class="sxs-lookup"><span data-stu-id="75602-319">Links to GitHub issues fixed in RTM</span></span>
[<span data-ttu-id="75602-320">문제 목록 1</span><span class="sxs-lookup"><span data-stu-id="75602-320">Issues list 1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[<span data-ttu-id="75602-321">문제 목록 2</span><span class="sxs-lookup"><span data-stu-id="75602-321">Issues list 2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[<span data-ttu-id="75602-322">문제 목록 3</span><span class="sxs-lookup"><span data-stu-id="75602-322">Issues list 3</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[<span data-ttu-id="75602-323">문제 목록 4</span><span class="sxs-lookup"><span data-stu-id="75602-323">Issues list 4</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[<span data-ttu-id="75602-324">문제 목록 5</span><span class="sxs-lookup"><span data-stu-id="75602-324">Issues list 5</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
