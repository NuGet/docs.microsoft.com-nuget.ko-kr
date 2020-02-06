---
title: NuGet CLI 설치 명령
description: Nuget.exe 설치 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6c49b2406462eae6ce45c65dfd8b3a9eb1077e73
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036944"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="1a931-103">install 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1a931-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="1a931-104">**적용 대상:** 패키지 사용 &bullet; **지원 되는 버전:** 모두</span><span class="sxs-lookup"><span data-stu-id="1a931-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="1a931-105">패키지를 다운로드 하 여 프로젝트에 설치 합니다. 기본적으로 현재 폴더는 지정 된 패키지 소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="1a931-106">프로젝트의 컨텍스트 외부에서 직접 패키지를 다운로드 하려면 [nuget.org](https://www.nuget.org) 의 패키지 페이지를 방문 하 여 **다운로드** 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="1a931-107">지정 된 소스가 없으면 전역 구성 파일 `%appdata%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)에 나열 된 소스가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="1a931-108">자세한 내용은 [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1a931-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="1a931-109">특정 패키지를 지정 하지 않으면 `install` 프로젝트의 `packages.config` 파일에 나열 된 모든 패키지를 설치 하 여 [`restore`](cli-ref-restore.md)와 유사 하 게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="1a931-110">`install` 명령은 프로젝트 파일이 나 `packages.config`를 수정 하지 않습니다. 이러한 방식으로 패키지를 디스크에 추가 하 고 프로젝트의 종속성을 변경 하지 않는다는 점에서 `restore`와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="1a931-111">종속성을 추가 하려면 Visual Studio에서 패키지 관리자 UI 또는 콘솔을 통해 패키지를 추가 하거나 `packages.config` 수정한 후 `install` 또는 `restore`를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="1a931-112">사용</span><span class="sxs-lookup"><span data-stu-id="1a931-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="1a931-113">(최신 버전을 사용 하 여 설치할 패키지의 이름을 `<packageID>` 하거나 설치할 패키지를 나열 하는 `packages.config` 파일을 `<configFilePath>` 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="1a931-114">`-Version` 옵션을 사용 하 여 특정 버전을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="1a931-115">옵션</span><span class="sxs-lookup"><span data-stu-id="1a931-115">Options</span></span>

| <span data-ttu-id="1a931-116">옵션</span><span class="sxs-lookup"><span data-stu-id="1a931-116">Option</span></span> | <span data-ttu-id="1a931-117">Description</span><span class="sxs-lookup"><span data-stu-id="1a931-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1a931-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1a931-118">ConfigFile</span></span> | <span data-ttu-id="1a931-119">수정할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1a931-120">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1a931-121">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="1a931-121">DependencyVersion</span></span> | <span data-ttu-id="1a931-122">*(4.4 +)* 사용할 종속성 패키지의 버전은 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-122">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="1a931-123">*가장 낮음* (기본값): 가장 낮은 버전</span><span class="sxs-lookup"><span data-stu-id="1a931-123">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="1a931-124">*HighestPatch*: 최하위 주, 최저 부, 최고 패치가 있는 버전</span><span class="sxs-lookup"><span data-stu-id="1a931-124">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="1a931-125">*HighestMinor*: 최하위 주, 가장 높은 부, 최고 패치가 있는 버전</span><span class="sxs-lookup"><span data-stu-id="1a931-125">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="1a931-126">*최고*: 최고 버전</span><span class="sxs-lookup"><span data-stu-id="1a931-126">*Highest*: the highest version</span></span></li><li><span data-ttu-id="1a931-127">*무시*: 종속성 패키지가 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-127">*Ignore*: No dependency packages will be used</span></span></li></ul> |
| <span data-ttu-id="1a931-128">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="1a931-128">DisableParallelProcessing</span></span> | <span data-ttu-id="1a931-129">여러 패키지를 동시에 설치할 수 없도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-129">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="1a931-130">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="1a931-130">ExcludeVersion</span></span> | <span data-ttu-id="1a931-131">패키지 이름만 사용 하 고 버전 번호를 사용 하 여 라는 이름의 폴더에 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-131">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="1a931-132">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="1a931-132">FallbackSource</span></span> | <span data-ttu-id="1a931-133">*(3.2 이상)* 주 또는 기본 원본에서 패키지를 찾을 수 없는 경우 대체로 사용할 패키지 원본 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-133">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="1a931-134">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1a931-134">ForceEnglishOutput</span></span> | <span data-ttu-id="1a931-135">*(3.5 +)* 고정 영어 기반 문화권을 사용 하 여 nuget.exe를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-135">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1a931-136">프레임워크</span><span class="sxs-lookup"><span data-stu-id="1a931-136">Framework</span></span> | <span data-ttu-id="1a931-137">*(4.4 +)* 종속성을 선택 하는 데 사용 되는 대상 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-137">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="1a931-138">지정 하지 않으면 기본값은 ' a l l '입니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-138">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="1a931-139">도움말</span><span class="sxs-lookup"><span data-stu-id="1a931-139">Help</span></span> | <span data-ttu-id="1a931-140">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-140">Displays help information for the command.</span></span> |
| <span data-ttu-id="1a931-141">NoCache</span><span class="sxs-lookup"><span data-stu-id="1a931-141">NoCache</span></span> | <span data-ttu-id="1a931-142">NuGet이 캐시 된 패키지를 사용 하지 못하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-142">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="1a931-143">[전역 패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1a931-143">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="1a931-144">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1a931-144">NonInteractive</span></span> | <span data-ttu-id="1a931-145">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-145">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1a931-146">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="1a931-146">OutputDirectory</span></span> | <span data-ttu-id="1a931-147">패키지가 설치 되는 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-147">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="1a931-148">폴더를 지정 하지 않으면 현재 폴더가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-148">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="1a931-149">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="1a931-149">PackageSaveMode</span></span> | <span data-ttu-id="1a931-150">패키지 설치 후 저장할 파일 유형을 지정 합니다. `nuspec`, `nupkg`또는 `nuspec;nupkg`중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-150">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="1a931-151">PreRelease</span><span class="sxs-lookup"><span data-stu-id="1a931-151">PreRelease</span></span> | <span data-ttu-id="1a931-152">시험판 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-152">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="1a931-153">`packages.config`를 사용 하 여 패키지를 복원 하는 경우이 플래그는 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-153">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="1a931-154">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="1a931-154">RequireConsent</span></span> | <span data-ttu-id="1a931-155">패키지를 다운로드 하 고 설치 하기 전에 패키지 복원이 사용 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-155">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="1a931-156">자세한 내용은 [패키지 복원](../../consume-packages/package-restore.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1a931-156">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="1a931-157">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="1a931-157">SolutionDirectory</span></span> | <span data-ttu-id="1a931-158">패키지를 복원할 솔루션의 루트 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-158">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="1a931-159">원본</span><span class="sxs-lookup"><span data-stu-id="1a931-159">Source</span></span> | <span data-ttu-id="1a931-160">사용할 패키지 원본 (Url) 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-160">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="1a931-161">생략 하는 경우 명령은 구성 파일에 제공 된 소스를 사용 합니다. [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="1a931-161">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="1a931-162">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="1a931-162">Verbosity</span></span> | <span data-ttu-id="1a931-163">출력에 표시 되는 세부 정보의 양을 지정 합니다. *보통*, *자동*, *자세히*입니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-163">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="1a931-164">버전</span><span class="sxs-lookup"><span data-stu-id="1a931-164">Version</span></span> | <span data-ttu-id="1a931-165">설치할 패키지의 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1a931-165">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="1a931-166">[환경 변수](cli-ref-environment-variables.md) 참조</span><span class="sxs-lookup"><span data-stu-id="1a931-166">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1a931-167">예</span><span class="sxs-lookup"><span data-stu-id="1a931-167">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
