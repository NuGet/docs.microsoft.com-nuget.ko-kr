---
title: NuGet CLI 복원 명령
description: nuget.exe 복원 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 108317aba2107948180ab0149c0c5ba5150cf9b8
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622832"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="b5df3-103">restore 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b5df3-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="b5df3-104">**적용 대상:** 패키지 사용 &bullet; **지원 버전:** 2.7 이상</span><span class="sxs-lookup"><span data-stu-id="b5df3-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="b5df3-105">폴더에서 누락 된 패키지를 다운로드 하 여 설치 `packages` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="b5df3-106">NuGet 4.0 + 및 PackageReference 형식과 함께 사용 하는 경우 `<project>.nuget.props` 필요한 경우 폴더에 파일을 생성 `obj` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="b5df3-107">파일은 소스 제어에서 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="b5df3-108">Mac에서 CLI를 사용 하는 Mac OSX 및 Linux에서 패키지 복원은 PackageReference에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="b5df3-109">사용량</span><span class="sxs-lookup"><span data-stu-id="b5df3-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="b5df3-110">여기서는 `<projectPath>` 솔루션 또는 파일의 위치를 지정 합니다 `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="b5df3-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="b5df3-111">동작 세부 정보는 아래 [설명 부분](#remarks) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b5df3-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="b5df3-112">옵션</span><span class="sxs-lookup"><span data-stu-id="b5df3-112">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="b5df3-113">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b5df3-114">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DirectDownload`**

  <span data-ttu-id="b5df3-115">*(4.0 이상)* 는 이진 또는 메타 데이터로 캐시를 채우지 않고 패키지를 직접 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-115">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span>

- **`-DisableParallelProcessing`**

   <span data-ttu-id="b5df3-116">여러 패키지를 동시에 복원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-116">Disables restoring multiple packages in parallel.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="b5df3-117">*(3.2 이상)* 주 또는 기본 원본에서 패키지를 찾을 수 없는 경우 대체로 사용할 패키지 원본 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-117">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> <span data-ttu-id="b5df3-118">세미콜론을 사용 하 여 목록 항목을 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-118">Use a semicolon to separate list entries.</span></span>

- **`-Force`**

  <span data-ttu-id="b5df3-119">PackageReference 기반 프로젝트에서 마지막 복원이 성공한 경우에도 모든 종속성이 확인 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-119">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="b5df3-120">이 플래그를 지정 하는 것은 파일을 삭제 하는 것과 비슷합니다 `project.assets.json` .</span><span class="sxs-lookup"><span data-stu-id="b5df3-120">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="b5df3-121">이는 http 캐시를 우회 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-121">This does not bypass the http-cache.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="b5df3-122">*(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-ForceEvaluate`**

  <span data-ttu-id="b5df3-123">잠금 파일이 이미 존재하는 경우에도 모든 종속성을 다시 평가하기 위해 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-123">Forces restore to reevaluate all dependencies even if a lock file already exists.</span></span>

- **`-?|-help`**

  <span data-ttu-id="b5df3-124">명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-124">Displays help information for the command.</span></span>

- **`-LockFilePath`**

  <span data-ttu-id="b5df3-125">프로젝트 잠금 파일이 작성되는 출력 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-125">Output location where project lock file is written.</span></span> <span data-ttu-id="b5df3-126">기본적으로 이 값은 `PROJECT_ROOT\packages.lock.json`입니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-126">By default, this is `PROJECT_ROOT\packages.lock.json`.</span></span>

- **`-LockedMode`**

  <span data-ttu-id="b5df3-127">프로젝트 잠금 파일 업데이트를 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-127">Don't allow updating project lock file.</span></span>

- **`-MSBuildPath`**

   <span data-ttu-id="b5df3-128">*(4.0 이상)* 명령에 사용할 MSBuild의 경로를 지정 합니다 `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="b5df3-128">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="b5df3-129">*(3.2 이상)* 이 명령에 사용할 MSBuild의 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-129">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="b5df3-130">지원 되는 값은 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9입니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-130">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="b5df3-131">기본적으로 경로에 MSBuild가 선택 되어 있으며, 그렇지 않은 경우 기본적으로 설치 되어 있는 MSBuild의 가장 높은 버전으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-131">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoCache`**

  <span data-ttu-id="b5df3-132">NuGet이 캐시 된 패키지를 사용 하지 못하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="b5df3-133">[전역 패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b5df3-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="b5df3-134">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="b5df3-135">패키지가 설치 되는 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="b5df3-136">폴더를 지정 하지 않으면 현재 폴더가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-136">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="b5df3-137">`packages.config`또는를 사용 하지 않는 한 파일을 사용 하 여 복원할 때 필요 `PackagesDirectory` `SolutionDirectory` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-137">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="b5df3-138">패키지 설치 후 저장할 파일 유형을 지정 합니다., 또는 중 하나 `nuspec` 입니다 `nupkg` `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="b5df3-138">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="b5df3-139">`OutputDirectory`와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-139">Same as `OutputDirectory`.</span></span> <span data-ttu-id="b5df3-140">`packages.config`또는를 사용 하지 않는 한 파일을 사용 하 여 복원할 때 필요 `OutputDirectory` `SolutionDirectory` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-140">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span>

- **`-Project2ProjectTimeOut`**

  <span data-ttu-id="b5df3-141">프로젝트 간 참조를 확인 하는 제한 시간 (초)입니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-141">Timeout in seconds for resolving project-to-project references.</span></span>

- **`-Recursive`**

  <span data-ttu-id="b5df3-142">*(4.0 이상)* UWP 및 .NET Core 프로젝트에 대 한 모든 참조 프로젝트를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-142">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="b5df3-143">을 사용 하는 프로젝트에는 적용 되지 않습니다 `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="b5df3-143">Does not apply to projects using `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="b5df3-144">패키지를 다운로드 하 고 설치 하기 전에 패키지 복원이 사용 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-144">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="b5df3-145">자세한 내용은 [패키지 복원](../../consume-packages/package-restore.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b5df3-145">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="b5df3-146">솔루션 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-146">Specifies the solution folder.</span></span> <span data-ttu-id="b5df3-147">솔루션에 대 한 패키지를 복원 하는 경우 유효 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-147">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="b5df3-148">`packages.config`또는를 사용 하지 않는 한 파일을 사용 하 여 복원할 때 필요 `PackagesDirectory` `OutputDirectory` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-148">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span>

- **`-Source`**

  <span data-ttu-id="b5df3-149">복원에 사용할 패키지 원본 (Url)의 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-149">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="b5df3-150">생략 하는 경우 명령은 구성 파일에 제공 된 소스를 사용 합니다. [NuGet 동작 구성](../../consume-packages/configuring-nuget-behavior.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b5df3-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="b5df3-151">세미콜론을 사용 하 여 목록 항목을 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-151">Use a semicolon to separate list entries.</span></span>

- **`-UseLockFile`**

  <span data-ttu-id="b5df3-152">복원에 사용되고 생성될 프로젝트 잠금 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-152">Enables project lock file to be generated and used with restore.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="b5df3-153">출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-153">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="b5df3-154">[환경 변수](cli-ref-environment-variables.md) 참조</span><span class="sxs-lookup"><span data-stu-id="b5df3-154">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="b5df3-155">설명</span><span class="sxs-lookup"><span data-stu-id="b5df3-155">Remarks</span></span>

<span data-ttu-id="b5df3-156">Restore 명령은 다음 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-156">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="b5df3-157">복원 명령의 작업 모드를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-157">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="b5df3-158">projectPath 파일 형식</span><span class="sxs-lookup"><span data-stu-id="b5df3-158">projectPath file type</span></span> | <span data-ttu-id="b5df3-159">동작</span><span class="sxs-lookup"><span data-stu-id="b5df3-159">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="b5df3-160">솔루션 (폴더)</span><span class="sxs-lookup"><span data-stu-id="b5df3-160">Solution (folder)</span></span> | <span data-ttu-id="b5df3-161">NuGet은 파일을 `.sln` 찾은 후 해당 파일을 사용 하 고, 그렇지 않으면 오류를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-161">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="b5df3-162">`(SolutionDir)\.nuget` 는 시작 폴더로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-162">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="b5df3-163">`.sln` 파일:</span><span class="sxs-lookup"><span data-stu-id="b5df3-163">`.sln` file</span></span> | <span data-ttu-id="b5df3-164">솔루션에 의해 식별 되는 패키지를 복원 합니다. 을 사용 하는 경우 오류를 제공 `-SolutionDirectory` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-164">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="b5df3-165">`$(SolutionDir)\.nuget` 는 시작 폴더로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-165">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="b5df3-166">`packages.config` 또는 프로젝트 파일</span><span class="sxs-lookup"><span data-stu-id="b5df3-166">`packages.config` or project file</span></span> | <span data-ttu-id="b5df3-167">파일에 나열 된 패키지를 복원 하 여 종속성을 확인 하 고 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-167">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="b5df3-168">기타 파일 형식</span><span class="sxs-lookup"><span data-stu-id="b5df3-168">Other file type</span></span> | <span data-ttu-id="b5df3-169">파일이 `.sln` 위와 같이 파일 이라고 가정 합니다. 솔루션이 아닌 경우 NuGet에서 오류를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-169">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="b5df3-170">(projectPath를 지정 하지 않음)</span><span class="sxs-lookup"><span data-stu-id="b5df3-170">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="b5df3-171">NuGet은 현재 폴더에 있는 솔루션 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-171">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="b5df3-172">단일 파일이 있는 경우 해당 파일은 패키지를 복원 하는 데 사용 됩니다. 여러 솔루션을 찾은 경우 NuGet은 오류를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-172">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="b5df3-173">솔루션 파일이 없는 경우 NuGet은를 찾고이를 사용 하 여 `packages.config` 패키지를 복원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-173">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="b5df3-174">솔루션이 나 파일이 없으면 `packages.config` NuGet에서 오류를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-174">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="b5df3-175">다음 우선 순위 순서를 사용 하 여 패키지 폴더를 결정 합니다. 이러한 폴더를 찾을 수 없는 경우 NuGet에서 오류를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-175">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="b5df3-176">로 지정 된 폴더 `-PackagesDirectory` 입니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-176">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="b5df3-177">`repositoryPath`의 값입니다.`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="b5df3-177">The `repositoryPath` value in `Nuget.Config`</span></span>
    - <span data-ttu-id="b5df3-178">지정 된 폴더 `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="b5df3-178">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="b5df3-179">솔루션에 대 한 패키지를 복원할 때 NuGet은 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-179">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="b5df3-180">솔루션 파일을 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-180">Loads the solution file.</span></span>
    - <span data-ttu-id="b5df3-181">에 나열 된 솔루션 수준 패키지를 폴더에 복원 `$(SolutionDir)\.nuget\packages.config` `packages` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-181">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="b5df3-182">에 나열 된 패키지를 폴더에 복원 `$(ProjectDir)\packages.config` `packages` 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5df3-182">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="b5df3-183">지정 된 각 패키지에 대해를 지정 하지 않으면 패키지를 병렬로 복원 합니다 `-DisableParallelProcessing` .</span><span class="sxs-lookup"><span data-stu-id="b5df3-183">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="b5df3-184">예</span><span class="sxs-lookup"><span data-stu-id="b5df3-184">Examples</span></span>

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
