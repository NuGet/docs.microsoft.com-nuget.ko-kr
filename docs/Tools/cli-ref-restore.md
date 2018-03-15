---
title: "NuGet CLI 복원 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 복원 명령에 대 한 참조"
keywords: "nuget 복원 참조, 패키지 명령 복원"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2416ad652244e0ea60651147ad74a1513cdb75ff
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="38a5b-104">restore 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="38a5b-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="38a5b-105">**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="38a5b-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="38a5b-106">다운로드 하 고 모든 패키지에서 누락 된 설치는 `packages` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-106">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="38a5b-107">NuGet 4.0 이상 및 PackageReference 형식으로 사용 하는 경우 생성 된 `<project>.nuget.props` 파일에 필요한 경우는 `obj` 폴더.</span><span class="sxs-lookup"><span data-stu-id="38a5b-107">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="38a5b-108">(소스 제어에서 파일을 생략할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="38a5b-108">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="38a5b-109">Mac OSX 및 모노에 CLI와 Linux에서 패키지를 복원 지원 되지 않습니다 PackageReference 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-109">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="38a5b-110">사용법</span><span class="sxs-lookup"><span data-stu-id="38a5b-110">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="38a5b-111">여기서 `<projectPath>` 솔루션의 위치를 지정 또는 `packages.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-111">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="38a5b-112">참조 [주의](#remarks) 아래 동작 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-112">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="38a5b-113">옵션</span><span class="sxs-lookup"><span data-stu-id="38a5b-113">Options</span></span>

| <span data-ttu-id="38a5b-114">옵션</span><span class="sxs-lookup"><span data-stu-id="38a5b-114">Option</span></span> | <span data-ttu-id="38a5b-115">설명</span><span class="sxs-lookup"><span data-stu-id="38a5b-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="38a5b-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="38a5b-116">ConfigFile</span></span> | <span data-ttu-id="38a5b-117">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="38a5b-118">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="38a5b-119">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="38a5b-119">DirectDownload</span></span> | <span data-ttu-id="38a5b-120">*(4.0 이상)*  이진 파일 및 메타 데이터에 대해 캐시를 채우지 않고 직접 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-120">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="38a5b-121">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="38a5b-121">DisableParallelProcessing</span></span> | <span data-ttu-id="38a5b-122">동시에 여러 패키지를 복원 하는 데 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-122">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="38a5b-123">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="38a5b-123">FallbackSource</span></span> | <span data-ttu-id="38a5b-124">*(3.2 +)*  패키지 주에서 찾을 수 없는 경우 대체도 사용할 패키지 소스 목록 또는 기본 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-124">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="38a5b-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="38a5b-125">ForceEnglishOutput</span></span> | <span data-ttu-id="38a5b-126">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="38a5b-127">도움말</span><span class="sxs-lookup"><span data-stu-id="38a5b-127">Help</span></span> | <span data-ttu-id="38a5b-128">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="38a5b-129">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="38a5b-129">MSBuildPath</span></span> | <span data-ttu-id="38a5b-130">*(4.0 이상)*  우선 순위를 차지 명령으로 사용 하는 MSBuild의 경로 지정 `-MSBuildVersion`합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-130">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="38a5b-131">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="38a5b-131">MSBuildVersion</span></span> | <span data-ttu-id="38a5b-132">*(3.2 +)*  이 명령과 함께 사용할 MSBuild의 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-132">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="38a5b-133">지원 되는 값은 4, 12, 14, 15입니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-133">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="38a5b-134">경로에 MSBuild 선택은 기본적으로 그렇지 않은 경우 기본값이 가장 높은 설치 된 버전의 MSBuild 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-134">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="38a5b-135">NoCache</span><span class="sxs-lookup"><span data-stu-id="38a5b-135">NoCache</span></span> | <span data-ttu-id="38a5b-136">NuGet 패키지를 사용 하 여 로컬 컴퓨터 캐시에서 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-136">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="38a5b-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="38a5b-137">NonInteractive</span></span> | <span data-ttu-id="38a5b-138">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="38a5b-139">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="38a5b-139">OutputDirectory</span></span> | <span data-ttu-id="38a5b-140">패키지 설치 되는 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-140">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="38a5b-141">없는 폴더를 지정 하는 경우 현재 폴더가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-141">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="38a5b-142">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="38a5b-142">PackageSaveMode</span></span> | <span data-ttu-id="38a5b-143">패키지 설치 후 저장할 파일의 형식을 지정 합니다: 중 `nuspec`, `nupkg`, 또는 `nuspec;nupkg`합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-143">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="38a5b-144">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="38a5b-144">PackagesDirectory</span></span> | <span data-ttu-id="38a5b-145">`OutputDirectory`와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-145">Same as `OutputDirectory`.</span></span> |
| <span data-ttu-id="38a5b-146">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="38a5b-146">Project2ProjectTimeOut</span></span> | <span data-ttu-id="38a5b-147">프로젝트 간 참조를 확인 하기 위한 시간 (초)의 시간이 초과 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-147">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="38a5b-148">재귀</span><span class="sxs-lookup"><span data-stu-id="38a5b-148">Recursive</span></span> | <span data-ttu-id="38a5b-149">*(4.0 이상)*  UWP 및.NET Core 프로젝트에 대 한 모든 참조 프로젝트를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-149">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="38a5b-150">사용 하 여 프로젝트에 적용 되지 않습니다 `packages.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-150">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="38a5b-151">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="38a5b-151">RequireConsent</span></span> | <span data-ttu-id="38a5b-152">다운로드 하 고 패키지를 설치 하기 전에 패키지를 복원 활성화 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-152">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="38a5b-153">자세한 내용은 참조 [패키지 복원](../consume-packages/package-restore.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-153">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="38a5b-154">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="38a5b-154">SolutionDirectory</span></span> | <span data-ttu-id="38a5b-155">솔루션 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-155">Specifies the solution folder.</span></span> <span data-ttu-id="38a5b-156">솔루션에 대 한 패키지를 복원 하는 경우 유효 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-156">Not valid when restoring packages for a solution.</span></span> |
| <span data-ttu-id="38a5b-157">소스</span><span class="sxs-lookup"><span data-stu-id="38a5b-157">Source</span></span> | <span data-ttu-id="38a5b-158">복원에 사용할 하도록 (Url)로 패키지 소스 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-158">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="38a5b-159">구성 파일에 제공 된 원본을 사용 하 여 생략 된 경우, 참조 [NuGet 구성 동작](../consume-packages/configuring-nuget-behavior.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-159">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="38a5b-160">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="38a5b-160">Verbosity</span></span> |<span data-ttu-id="38a5b-161">>-출력에 표시 되는 하위 크기를 지정 하는 중: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-161">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="38a5b-162">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="38a5b-162">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="38a5b-163">설명</span><span class="sxs-lookup"><span data-stu-id="38a5b-163">Remarks</span></span>

<span data-ttu-id="38a5b-164">Restore 명령에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-164">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="38a5b-165">Restore 명령 작업 모드를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-165">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="38a5b-166">projectPath 파일 형식</span><span class="sxs-lookup"><span data-stu-id="38a5b-166">projectPath file type</span></span> | <span data-ttu-id="38a5b-167">동작</span><span class="sxs-lookup"><span data-stu-id="38a5b-167">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="38a5b-168">솔루션 (폴더)</span><span class="sxs-lookup"><span data-stu-id="38a5b-168">Solution (folder)</span></span> | <span data-ttu-id="38a5b-169">NuGet를 찾습니다는 `.sln` 검색 되지 않으면 오류가 발생 하는 사용 하 여 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-169">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="38a5b-170">`(SolutionDir)\.nuget` 시작 폴더도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-170">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="38a5b-171">`.sln` 파일</span><span class="sxs-lookup"><span data-stu-id="38a5b-171">`.sln` file</span></span> | <span data-ttu-id="38a5b-172">솔루션;로 식별 되는 패키지를 복원 하면 오류가 발생 `-SolutionDirectory` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-172">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="38a5b-173">`$(SolutionDir)\.nuget` 시작 폴더도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-173">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="38a5b-174">`packages.config` 또는 프로젝트 파일</span><span class="sxs-lookup"><span data-stu-id="38a5b-174">`packages.config` or project file</span></span> | <span data-ttu-id="38a5b-175">해결 및 종속성 설치 파일에 나열 된 패키지를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-175">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="38a5b-176">다른 파일 형식</span><span class="sxs-lookup"><span data-stu-id="38a5b-176">Other file type</span></span> | <span data-ttu-id="38a5b-177">파일 것으로 간주 되는 `.sln` 오류 NuGet은 솔루션을 없으면 위와; 같은 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-177">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="38a5b-178">(projectPath 지정 되지 않은)</span><span class="sxs-lookup"><span data-stu-id="38a5b-178">(projectPath not specified)</span></span> | <span data-ttu-id="38a5b-179">-NuGet 현재 폴더에서 솔루션 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-179">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="38a5b-180">하나; 패키지를 복원 하는 데 사용 단일 파일이 발견 된 경우 NuGet 여러 솔루션 발견 되 면 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-180">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="38a5b-181">-NuGet에 대 한 검색 솔루션 파일이 없는 경우는 `packages.config` 및이 사용 하 여 패키지를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-181">- If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span>
    |<span data-ttu-id="38a5b-182">-솔루션이 없는 경우 또는 `packages.config` 파일이, NuGet 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-182">- If no solution or `packages.config` file is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="38a5b-183">다음과 같은 우선 순위 (NuGet 이러한 폴더의 발견 되지 않으면 오류가 제공)를 사용 하 여 패키지 폴더를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-183">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="38a5b-184">지정 된 폴더 `-PackagesDirectory`합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-184">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="38a5b-185">`repositoryPath` 베일에서 `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="38a5b-185">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="38a5b-186">지정 된 폴더 `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="38a5b-186">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="38a5b-187">솔루션에 대 한 패키지를 복원할 때 NuGet는 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-187">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="38a5b-188">솔루션 파일을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-188">Loads the solution file.</span></span>
    - <span data-ttu-id="38a5b-189">솔루션 수준 패키지에 나열 된 복원 `$(SolutionDir)\.nuget\packages.config` 에 `packages` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-189">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="38a5b-190">에 나열 된 패키지를 복원 `$(ProjectDir)\packages.config` 에 `packages` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-190">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="38a5b-191">지정 된 각 패키지에 대해 병렬로 패키지 않으면 복원이 `-DisableParallelProcessing` 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38a5b-191">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="38a5b-192">예제</span><span class="sxs-lookup"><span data-stu-id="38a5b-192">Examples</span></span>

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
