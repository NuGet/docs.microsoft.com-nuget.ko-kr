---
title: NuGet CLI 복원 명령을 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe 복원 명령에 대 한 참조
keywords: nuget 복원 참조, 패키지 명령 복원
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 64f12fdedc8fbfcee15c1dcddc445148f458c030
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="b5f77-104">restore 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b5f77-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="b5f77-105">**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="b5f77-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="b5f77-106">다운로드 하 고 모든 패키지에서 누락 된 설치는 `packages` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-106">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="b5f77-107">NuGet 4.0 이상 및 PackageReference 형식으로 사용 하는 경우 생성 된 `<project>.nuget.props` 파일에 필요한 경우는 `obj` 폴더.</span><span class="sxs-lookup"><span data-stu-id="b5f77-107">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="b5f77-108">(소스 제어에서 파일을 생략할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="b5f77-108">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="b5f77-109">Mac OSX 및 모노에 CLI와 Linux에서 패키지를 복원 지원 되지 않습니다 PackageReference 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-109">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="b5f77-110">사용법</span><span class="sxs-lookup"><span data-stu-id="b5f77-110">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="b5f77-111">여기서 `<projectPath>` 솔루션의 위치를 지정 또는 `packages.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-111">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="b5f77-112">참조 [주의](#remarks) 아래 동작 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-112">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="b5f77-113">옵션</span><span class="sxs-lookup"><span data-stu-id="b5f77-113">Options</span></span>

| <span data-ttu-id="b5f77-114">옵션</span><span class="sxs-lookup"><span data-stu-id="b5f77-114">Option</span></span> | <span data-ttu-id="b5f77-115">설명</span><span class="sxs-lookup"><span data-stu-id="b5f77-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b5f77-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b5f77-116">ConfigFile</span></span> | <span data-ttu-id="b5f77-117">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b5f77-118">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b5f77-119">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="b5f77-119">DirectDownload</span></span> | <span data-ttu-id="b5f77-120">*(4.0 이상)*  이진 파일 및 메타 데이터에 대해 캐시를 채우지 않고 직접 패키지를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-120">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="b5f77-121">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="b5f77-121">DisableParallelProcessing</span></span> | <span data-ttu-id="b5f77-122">동시에 여러 패키지를 복원 하는 데 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-122">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="b5f77-123">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="b5f77-123">FallbackSource</span></span> | <span data-ttu-id="b5f77-124">*(3.2 +)*  패키지 주에서 찾을 수 없는 경우 대체도 사용할 패키지 소스 목록 또는 기본 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-124">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="b5f77-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b5f77-125">ForceEnglishOutput</span></span> | <span data-ttu-id="b5f77-126">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b5f77-127">도움말</span><span class="sxs-lookup"><span data-stu-id="b5f77-127">Help</span></span> | <span data-ttu-id="b5f77-128">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="b5f77-129">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="b5f77-129">MSBuildPath</span></span> | <span data-ttu-id="b5f77-130">*(4.0 이상)*  우선 순위를 차지 명령으로 사용 하는 MSBuild의 경로 지정 `-MSBuildVersion`합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-130">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="b5f77-131">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="b5f77-131">MSBuildVersion</span></span> | <span data-ttu-id="b5f77-132">*(3.2 +)*  이 명령과 함께 사용할 MSBuild의 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-132">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="b5f77-133">지원 되는 값은 4, 12, 14, 15입니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-133">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="b5f77-134">경로에 MSBuild 선택은 기본적으로 그렇지 않은 경우 기본값이 가장 높은 설치 된 버전의 MSBuild 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-134">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="b5f77-135">NoCache</span><span class="sxs-lookup"><span data-stu-id="b5f77-135">NoCache</span></span> | <span data-ttu-id="b5f77-136">캐시 된 패키지를 사용 하 여 NuGet을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-136">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="b5f77-137">참조 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-137">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="b5f77-138">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b5f77-138">NonInteractive</span></span> | <span data-ttu-id="b5f77-139">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-139">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b5f77-140">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="b5f77-140">OutputDirectory</span></span> | <span data-ttu-id="b5f77-141">패키지 설치 되는 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-141">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="b5f77-142">없는 폴더를 지정 하는 경우 현재 폴더가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-142">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="b5f77-143">복구 하는 경우 필수는 `packages.config` 하지 않는 한 파일 `PackagesDirectory` 또는 `SolutionDirectory` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-143">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>|
| <span data-ttu-id="b5f77-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="b5f77-144">PackageSaveMode</span></span> | <span data-ttu-id="b5f77-145">패키지 설치 후 저장할 파일의 형식을 지정 합니다: 중 `nuspec`, `nupkg`, 또는 `nuspec;nupkg`합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="b5f77-146">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="b5f77-146">PackagesDirectory</span></span> | <span data-ttu-id="b5f77-147">`OutputDirectory`와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-147">Same as `OutputDirectory`.</span></span> <span data-ttu-id="b5f77-148">복구 하는 경우 필수는 `packages.config` 하지 않는 한 파일 `OutputDirectory` 또는 `SolutionDirectory` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-148">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span> |
| <span data-ttu-id="b5f77-149">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="b5f77-149">Project2ProjectTimeOut</span></span> | <span data-ttu-id="b5f77-150">프로젝트 간 참조를 확인 하기 위한 시간 (초)의 시간이 초과 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-150">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="b5f77-151">재귀</span><span class="sxs-lookup"><span data-stu-id="b5f77-151">Recursive</span></span> | <span data-ttu-id="b5f77-152">*(4.0 이상)*  UWP 및.NET Core 프로젝트에 대 한 모든 참조 프로젝트를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-152">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="b5f77-153">사용 하 여 프로젝트에 적용 되지 않습니다 `packages.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-153">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="b5f77-154">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="b5f77-154">RequireConsent</span></span> | <span data-ttu-id="b5f77-155">다운로드 하 고 패키지를 설치 하기 전에 패키지를 복원 활성화 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-155">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="b5f77-156">자세한 내용은 참조 [패키지 복원](../consume-packages/package-restore.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-156">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="b5f77-157">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="b5f77-157">SolutionDirectory</span></span> | <span data-ttu-id="b5f77-158">솔루션 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-158">Specifies the solution folder.</span></span> <span data-ttu-id="b5f77-159">솔루션에 대 한 패키지를 복원 하는 경우 유효 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-159">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="b5f77-160">복구 하는 경우 필수는 `packages.config` 하지 않는 한 파일 `PackagesDirectory` 또는 `OutputDirectory` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-160">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span> |
| <span data-ttu-id="b5f77-161">소스</span><span class="sxs-lookup"><span data-stu-id="b5f77-161">Source</span></span> | <span data-ttu-id="b5f77-162">복원에 사용할 하도록 (Url)로 패키지 소스 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-162">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="b5f77-163">구성 파일에 제공 된 원본을 사용 하 여 생략 된 경우, 참조 [NuGet 구성 동작](../consume-packages/configuring-nuget-behavior.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-163">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="b5f77-164">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="b5f77-164">Verbosity</span></span> |<span data-ttu-id="b5f77-165">>-출력에 표시 되는 하위 크기를 지정 하는 중: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-165">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b5f77-166">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b5f77-166">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="b5f77-167">설명</span><span class="sxs-lookup"><span data-stu-id="b5f77-167">Remarks</span></span>

<span data-ttu-id="b5f77-168">Restore 명령에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-168">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="b5f77-169">Restore 명령 작업 모드를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-169">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="b5f77-170">projectPath 파일 형식</span><span class="sxs-lookup"><span data-stu-id="b5f77-170">projectPath file type</span></span> | <span data-ttu-id="b5f77-171">동작</span><span class="sxs-lookup"><span data-stu-id="b5f77-171">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="b5f77-172">솔루션 (폴더)</span><span class="sxs-lookup"><span data-stu-id="b5f77-172">Solution (folder)</span></span> | <span data-ttu-id="b5f77-173">NuGet를 찾습니다는 `.sln` 검색 되지 않으면 오류가 발생 하는 사용 하 여 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-173">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="b5f77-174">`(SolutionDir)\.nuget` 시작 폴더도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-174">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="b5f77-175">`.sln` 파일</span><span class="sxs-lookup"><span data-stu-id="b5f77-175">`.sln` file</span></span> | <span data-ttu-id="b5f77-176">솔루션;로 식별 되는 패키지를 복원 하면 오류가 발생 `-SolutionDirectory` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-176">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="b5f77-177">`$(SolutionDir)\.nuget` 시작 폴더도 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-177">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="b5f77-178">`packages.config` 또는 프로젝트 파일</span><span class="sxs-lookup"><span data-stu-id="b5f77-178">`packages.config` or project file</span></span> | <span data-ttu-id="b5f77-179">해결 및 종속성 설치 파일에 나열 된 패키지를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-179">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="b5f77-180">다른 파일 형식</span><span class="sxs-lookup"><span data-stu-id="b5f77-180">Other file type</span></span> | <span data-ttu-id="b5f77-181">파일 것으로 간주 되는 `.sln` 오류 NuGet은 솔루션을 없으면 위와; 같은 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-181">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="b5f77-182">(projectPath 지정 되지 않은)</span><span class="sxs-lookup"><span data-stu-id="b5f77-182">(projectPath not specified)</span></span> | <span data-ttu-id="b5f77-183">-NuGet 현재 폴더에서 솔루션 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-183">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="b5f77-184">하나; 패키지를 복원 하는 데 사용 단일 파일이 발견 된 경우 NuGet 여러 솔루션 발견 되 면 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-184">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="b5f77-185">-NuGet에 대 한 검색 솔루션 파일이 없는 경우는 `packages.config` 및이 사용 하 여 패키지를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-185">- If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span>
    |<span data-ttu-id="b5f77-186">-솔루션이 없는 경우 또는 `packages.config` 파일이, NuGet 오류가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-186">- If no solution or `packages.config` file is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="b5f77-187">다음과 같은 우선 순위 (NuGet 이러한 폴더의 발견 되지 않으면 오류가 제공)를 사용 하 여 패키지 폴더를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-187">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="b5f77-188">지정 된 폴더 `-PackagesDirectory`합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-188">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="b5f77-189">`repositoryPath` 베일에서 `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="b5f77-189">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="b5f77-190">지정 된 폴더 `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="b5f77-190">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="b5f77-191">솔루션에 대 한 패키지를 복원할 때 NuGet는 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-191">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="b5f77-192">솔루션 파일을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-192">Loads the solution file.</span></span>
    - <span data-ttu-id="b5f77-193">솔루션 수준 패키지에 나열 된 복원 `$(SolutionDir)\.nuget\packages.config` 에 `packages` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-193">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="b5f77-194">에 나열 된 패키지를 복원 `$(ProjectDir)\packages.config` 에 `packages` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-194">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="b5f77-195">지정 된 각 패키지에 대해 병렬로 패키지 않으면 복원이 `-DisableParallelProcessing` 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5f77-195">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="b5f77-196">예제</span><span class="sxs-lookup"><span data-stu-id="b5f77-196">Examples</span></span>

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
