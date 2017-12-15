---
title: "NuGet CLI 복원 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee41020-e548-4e61-b8cd-c82b77ac6af7
description: "Nuget.exe 복원 명령에 대 한 참조"
keywords: "nuget 복원 참조, 패키지 명령 복원"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b435a3c2ffe08e3c2f8fc6a4dacb06cf674e4fb9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="e701c-104">restore 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e701c-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="e701c-105">**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="e701c-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="e701c-106">NuGet 2.7 +: 다운로드 하 고에서 누락 된 모든 패키지를 설치 하는 `packages` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-106">NuGet 2.7+: Downloads and installs any packages missing from the `packages` folder.</span></span>

<span data-ttu-id="e701c-107">NuGet 3.3 +를 사용 하 여 프로젝트와 함께 `project.json`: 생성 한 `project.lock.json` 파일 및 `<project>.nuget.props` 파일, 필요한 경우.</span><span class="sxs-lookup"><span data-stu-id="e701c-107">NuGet 3.3+ with projects using `project.json`: Generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="e701c-108">(소스 제어에서 두 파일을 생략할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="e701c-108">(Both files can be omitted from source control.)</span></span>

<span data-ttu-id="e701c-109">프로젝트는 패키지에 참조가 포함 되어 프로젝트 파일에 직접 NuGet 4.0 이상: 생성 한 `<project>.nuget.props` 파일에 필요한 경우는 `obj` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-109">NuGet 4.0+ with project in which package references are included in the project file directly: Generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="e701c-110">(소스 제어에서 파일을 생략할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="e701c-110">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="e701c-111">Mac OSX 및 모노에 CLI와 Linux에서 패키지를 복원 지원 되지 않습니다 PackageReference 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-111">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with the PackageReference format.</span></span>

## <a name="usage"></a><span data-ttu-id="e701c-112">용도</span><span class="sxs-lookup"><span data-stu-id="e701c-112">Usage</span></span>

```
nuget restore <projectPath> [options]
```

<span data-ttu-id="e701c-113">여기서 `<projectPath>` 는 솔루션의 위치를 지정는 `packages.config` 파일 또는 `project.json` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-113">where `<projectPath>` specifies the location of a solution, a `packages.config` file, or a `project.json` file.</span></span> <span data-ttu-id="e701c-114">참조 [주의](#remarks) 아래 동작 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-114">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="e701c-115">옵션</span><span class="sxs-lookup"><span data-stu-id="e701c-115">Options</span></span>

| <span data-ttu-id="e701c-116">옵션</span><span class="sxs-lookup"><span data-stu-id="e701c-116">Option</span></span> | <span data-ttu-id="e701c-117">설명</span><span class="sxs-lookup"><span data-stu-id="e701c-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e701c-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="e701c-118">ConfigFile</span></span> | <span data-ttu-id="e701c-119">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="e701c-120">지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="e701c-121">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="e701c-121">DirectDownload</span></span> | <span data-ttu-id="e701c-122">*(4.0 이상)*  이진 파일 및 메타 데이터에 대해 캐시를 채우지 않고 직접 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-122">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="e701c-123">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="e701c-123">DisableParallelProcessing</span></span> | <span data-ttu-id="e701c-124">동시에 여러 패키지를 복원 하는 데 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-124">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="e701c-125">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="e701c-125">FallbackSource</span></span> | <span data-ttu-id="e701c-126">*(3.2 +)*  패키지 주에서 찾을 수 없는 경우 대체도 사용할 패키지 소스 목록 또는 기본 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-126">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="e701c-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="e701c-127">ForceEnglishOutput</span></span> | <span data-ttu-id="e701c-128">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="e701c-129">도움말</span><span class="sxs-lookup"><span data-stu-id="e701c-129">Help</span></span> | <span data-ttu-id="e701c-130">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="e701c-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="e701c-131">MSBuildPath</span></span> | <span data-ttu-id="e701c-132">*(4.0 이상)*  우선 순위를 차지 명령으로 사용 하는 MSBuild의 경로 지정 `-MSBuildVersion`합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="e701c-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="e701c-133">MSBuildVersion</span></span> | <span data-ttu-id="e701c-134">*(3.2 +)*  이 명령과 함께 사용할 MSBuild의 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="e701c-135">지원 되는 값은 4, 12, 14, 15입니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-135">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="e701c-136">경로에 MSBuild 선택은 기본적으로 그렇지 않은 경우 기본값이 가장 높은 설치 된 버전의 MSBuild 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="e701c-137">캐시 없음</span><span class="sxs-lookup"><span data-stu-id="e701c-137">NoCache</span></span> | <span data-ttu-id="e701c-138">NuGet 패키지를 사용 하 여 로컬 컴퓨터 캐시에서 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="e701c-139">비 대화형</span><span class="sxs-lookup"><span data-stu-id="e701c-139">NonInteractive</span></span> | <span data-ttu-id="e701c-140">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="e701c-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="e701c-141">OutputDirectory</span></span> | <span data-ttu-id="e701c-142">패키지 설치 되는 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="e701c-143">없는 폴더를 지정 하는 경우 현재 폴더가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="e701c-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="e701c-144">PackageSaveMode</span></span> | <span data-ttu-id="e701c-145">패키지 설치 후 저장할 파일의 형식을 지정 합니다: 중 `nuspec`, `nupkg`, 또는 `nuspec;nupkg`합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="e701c-146">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="e701c-146">PackagesDirectory</span></span> | <span data-ttu-id="e701c-147">`OutputDirectory`와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-147">Same as `OutputDirectory`.</span></span> |
| <span data-ttu-id="e701c-148">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="e701c-148">Project2ProjectTimeOut</span></span> | <span data-ttu-id="e701c-149">프로젝트 간 참조를 확인 하기 위한 시간 (초)의 시간이 초과 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-149">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="e701c-150">재귀</span><span class="sxs-lookup"><span data-stu-id="e701c-150">Recursive</span></span> | <span data-ttu-id="e701c-151">*(4.0 이상)*  UWP 및.NET Core 프로젝트에 대 한 모든 참조 프로젝트를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-151">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="e701c-152">사용 하 여 프로젝트에 적용 되지 않습니다 `packages.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-152">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="e701c-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="e701c-153">RequireConsent</span></span> | <span data-ttu-id="e701c-154">다운로드 하 고 패키지를 설치 하기 전에 패키지를 복원 활성화 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="e701c-155">자세한 내용은 참조 [패키지 복원](../consume-packages/package-restore.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-155">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="e701c-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="e701c-156">SolutionDirectory</span></span> | <span data-ttu-id="e701c-157">솔루션 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-157">Specifies the solution folder.</span></span> <span data-ttu-id="e701c-158">솔루션에 대 한 패키지를 복원 하는 경우 유효 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-158">Not valid when restoring packages for a solution.</span></span> |
| <span data-ttu-id="e701c-159">소스</span><span class="sxs-lookup"><span data-stu-id="e701c-159">Source</span></span> | <span data-ttu-id="e701c-160">복원에 사용할 하도록 (Url)로 패키지 소스 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-160">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="e701c-161">구성 파일에 제공 된 원본을 사용 하 여 생략 된 경우, 참조 [NuGet 구성 동작](../Consume-Packages/Configuring-NuGet-Behavior.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-161">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="e701c-162">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="e701c-162">Verbosity</span></span> |<span data-ttu-id="e701c-163">>-출력에 표시 되는 하위 크기를 지정 하는 중: *일반*, *quiet*, *세부 (2.5 이상)*합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-163">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="e701c-164">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="e701c-164">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="e701c-165">설명</span><span class="sxs-lookup"><span data-stu-id="e701c-165">Remarks</span></span>

<span data-ttu-id="e701c-166">Restore 명령에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-166">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="e701c-167">Restore 명령 작업 모드를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-167">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="e701c-168">projectPath 파일 형식</span><span class="sxs-lookup"><span data-stu-id="e701c-168">projectPath file type</span></span> | <span data-ttu-id="e701c-169">동작</span><span class="sxs-lookup"><span data-stu-id="e701c-169">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="e701c-170">솔루션 (폴더)</span><span class="sxs-lookup"><span data-stu-id="e701c-170">Solution (folder)</span></span> | <span data-ttu-id="e701c-171">NuGet를 찾습니다는 `.sln` 검색 되지 않으면 오류가 발생 하는 사용 하 여 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-171">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="e701c-172">`(SolutionDir)\.nuget`시작 폴더도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-172">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="e701c-173">`.sln`파일</span><span class="sxs-lookup"><span data-stu-id="e701c-173">`.sln` file</span></span> | <span data-ttu-id="e701c-174">솔루션;로 식별 되는 패키지를 복원 하면 오류가 발생 `-SolutionDirectory` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-174">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="e701c-175">`$(SolutionDir)\.nuget`시작 폴더도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-175">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="e701c-176">`packages.config``project.json`, 또는 프로젝트 파일</span><span class="sxs-lookup"><span data-stu-id="e701c-176">`packages.config`, `project.json`, or project file</span></span> | <span data-ttu-id="e701c-177">해결 및 종속성 설치 파일에 나열 된 패키지를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-177">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="e701c-178">다른 파일 형식</span><span class="sxs-lookup"><span data-stu-id="e701c-178">Other file type</span></span> | <span data-ttu-id="e701c-179">파일 것으로 간주 되는 `.sln` 오류 NuGet은 솔루션을 없으면 위와; 같은 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-179">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="e701c-180">(projectPath 지정 되지 않은)</span><span class="sxs-lookup"><span data-stu-id="e701c-180">(projectPath not specified)</span></span> | <span data-ttu-id="e701c-181">-NuGet 현재 폴더에서 솔루션 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-181">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="e701c-182">하나; 패키지를 복원 하는 데 사용 단일 파일이 발견 된 경우 NuGet 여러 솔루션 발견 되 면 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-182">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="e701c-183">-NuGet에 대 한 검색 솔루션 파일이 없는 경우는 `packages.config` 또는 `project.json` 및이 사용 하 여 패키지를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-183">- If there are no solution files, NuGet looks for a `packages.config` or `project.json` and uses that to restore packages.</span></span>
    |<span data-ttu-id="e701c-184">-경우 솔루션 파일이 없거나 `packages.config`, 또는 `project.json` 발견 되 면 NuGet 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-184">- If no solution file, `packages.config`, or `project.json` is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="e701c-185">다음과 같은 우선 순위 (NuGet 이러한 폴더의 발견 되지 않으면 오류가 제공)를 사용 하 여 패키지 폴더를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-185">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="e701c-186">`%userprofile%\.nuget\packages` 값 `project.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-186">The `%userprofile%\.nuget\packages` value in `project.json`.</span></span>
    - <span data-ttu-id="e701c-187">지정 된 폴더 `-PackagesDirectory`합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-187">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="e701c-188">`repositoryPath` 베일에서`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="e701c-188">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="e701c-189">지정 된 폴더`-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="e701c-189">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="e701c-190">솔루션에 대 한 패키지를 복원할 때 NuGet는 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-190">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="e701c-191">솔루션 파일을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-191">Loads the solution file.</span></span>
    - <span data-ttu-id="e701c-192">솔루션 수준 패키지에 나열 된 복원 `$(SolutionDir)\.nuget\packages.config` 에 `packages` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-192">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="e701c-193">에 나열 된 패키지를 복원 `$(ProjectDir)\packages.config` 에 `packages` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-193">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="e701c-194">지정 된 각 패키지에 대해 병렬로 패키지 않으면 복원이 `-DisableParallelProcessing` 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e701c-194">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="e701c-195">예제</span><span class="sxs-lookup"><span data-stu-id="e701c-195">Examples</span></span>

```
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
