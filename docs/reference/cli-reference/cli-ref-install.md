---
title: NuGet CLI 설치 명령
description: Nuget.exe 설치 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f39bcc67c5f659f05ef02f2579bcf07b4481bb27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327790"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="74364-103">install 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="74364-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="74364-104">**적용 대상:** 패키지 &bullet; 사용 **지원 버전:** 모두</span><span class="sxs-lookup"><span data-stu-id="74364-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="74364-105">패키지를 다운로드 하 여 프로젝트에 설치 합니다. 기본적으로 현재 폴더는 지정 된 패키지 소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="74364-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="74364-106">프로젝트의 컨텍스트 외부에서 직접 패키지를 다운로드 하려면 [nuget.org](https://www.nuget.org) 의 패키지 페이지를 방문 하 여 **다운로드** 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="74364-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="74364-107">지정 된 원본이 없으면 전역 구성 파일 `%appdata%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)에 나열 된 소스가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74364-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="74364-108">자세한 내용은 [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="74364-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="74364-109">특정 패키지를 지정 하지 않으면는 `install` 프로젝트의 `packages.config` 파일에 나열 된 모든 패키지를 설치 하 여와 유사 [`restore`](cli-ref-restore.md)하 게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="74364-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="74364-110">이 명령은 프로젝트 `packages.config`파일을 수정 하지 않습니다 .이 `restore` 방법에서는 패키지를 디스크에만 추가 하지만 프로젝트의 종속성은 변경 하지 않는다는 점에서와 비슷합니다. `install`</span><span class="sxs-lookup"><span data-stu-id="74364-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="74364-111">종속성을 추가 하려면 Visual Studio에서 패키지 관리자 UI 또는 콘솔을 통해 패키지를 추가 하거나를 수정 `packages.config` 하 고 `install` 또는 `restore`를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="74364-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="74364-112">사용법</span><span class="sxs-lookup"><span data-stu-id="74364-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="74364-113">여기서 `<packageID>` 는 최신 버전을 사용 하 여 설치할 패키지의 이름을, 또는 `<configFilePath>` 설치할 패키지 `packages.config` 를 나열 하는 파일을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="74364-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="74364-114">`-Version` 옵션을 사용 하 여 특정 버전을 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74364-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="74364-115">변수</span><span class="sxs-lookup"><span data-stu-id="74364-115">Options</span></span>

| <span data-ttu-id="74364-116">옵션</span><span class="sxs-lookup"><span data-stu-id="74364-116">Option</span></span> | <span data-ttu-id="74364-117">설명</span><span class="sxs-lookup"><span data-stu-id="74364-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="74364-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="74364-118">ConfigFile</span></span> | <span data-ttu-id="74364-119">적용할 NuGet 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="74364-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="74364-120">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="74364-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="74364-121">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="74364-121">DependencyVersion</span></span> | <span data-ttu-id="74364-122">*(4.4 +)* 사용할 종속성 패키지의 버전은 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74364-122">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="74364-123">*최저* (기본값): 가장 낮은 버전</span><span class="sxs-lookup"><span data-stu-id="74364-123">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="74364-124">*HighestPatch*: 최하위 주, 최저 부, 최고 패치가 있는 버전</span><span class="sxs-lookup"><span data-stu-id="74364-124">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="74364-125">*HighestMinor*: 최하위 주, 가장 높은 부, 최고 패치가 있는 버전</span><span class="sxs-lookup"><span data-stu-id="74364-125">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="74364-126">*최고*: 최고 버전</span><span class="sxs-lookup"><span data-stu-id="74364-126">*Highest*: the highest version</span></span></li></ul> |
| <span data-ttu-id="74364-127">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="74364-127">DisableParallelProcessing</span></span> | <span data-ttu-id="74364-128">여러 패키지를 동시에 설치할 수 없도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="74364-128">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="74364-129">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="74364-129">ExcludeVersion</span></span> | <span data-ttu-id="74364-130">패키지 이름만 사용 하 고 버전 번호를 사용 하 여 라는 이름의 폴더에 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="74364-130">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="74364-131">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="74364-131">FallbackSource</span></span> | <span data-ttu-id="74364-132">*(3.2 이상)* 주 또는 기본 원본에서 패키지를 찾을 수 없는 경우 대체로 사용할 패키지 원본 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="74364-132">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="74364-133">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="74364-133">ForceEnglishOutput</span></span> | <span data-ttu-id="74364-134">*(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="74364-134">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="74364-135">프레임워크</span><span class="sxs-lookup"><span data-stu-id="74364-135">Framework</span></span> | <span data-ttu-id="74364-136">*(4.4 +)* 종속성을 선택 하는 데 사용 되는 대상 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="74364-136">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="74364-137">지정 하지 않으면 기본값은 ' a l l '입니다.</span><span class="sxs-lookup"><span data-stu-id="74364-137">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="74364-138">Help</span><span class="sxs-lookup"><span data-stu-id="74364-138">Help</span></span> | <span data-ttu-id="74364-139">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="74364-139">Displays help information for the command.</span></span> |
| <span data-ttu-id="74364-140">NoCache</span><span class="sxs-lookup"><span data-stu-id="74364-140">NoCache</span></span> | <span data-ttu-id="74364-141">NuGet이 캐시 된 패키지를 사용 하지 못하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="74364-141">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="74364-142">[전역 패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="74364-142">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="74364-143">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="74364-143">NonInteractive</span></span> | <span data-ttu-id="74364-144">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74364-144">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="74364-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="74364-145">OutputDirectory</span></span> | <span data-ttu-id="74364-146">패키지가 설치 되는 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="74364-146">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="74364-147">폴더를 지정 하지 않으면 현재 폴더가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="74364-147">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="74364-148">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="74364-148">PackageSaveMode</span></span> | <span data-ttu-id="74364-149">패키지 설치 후 저장할 파일 유형을 지정 합니다. `nuspec`, `nupkg`또는 `nuspec;nupkg`중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="74364-149">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="74364-150">PreRelease</span><span class="sxs-lookup"><span data-stu-id="74364-150">PreRelease</span></span> | <span data-ttu-id="74364-151">시험판 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74364-151">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="74364-152">이 플래그는를 사용 하 여 패키지를 `packages.config`복원 하는 경우에는 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="74364-152">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="74364-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="74364-153">RequireConsent</span></span> | <span data-ttu-id="74364-154">패키지를 다운로드 하 고 설치 하기 전에 패키지 복원이 사용 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="74364-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="74364-155">자세한 내용은 [패키지 복원](../../consume-packages/package-restore.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="74364-155">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="74364-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="74364-156">SolutionDirectory</span></span> | <span data-ttu-id="74364-157">패키지를 복원할 솔루션의 루트 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="74364-157">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="74364-158">Source</span><span class="sxs-lookup"><span data-stu-id="74364-158">Source</span></span> | <span data-ttu-id="74364-159">사용할 패키지 원본 (Url) 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="74364-159">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="74364-160">생략 하는 경우 명령은 구성 파일에 제공 된 소스를 사용 합니다. [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="74364-160">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="74364-161">Verbosity</span><span class="sxs-lookup"><span data-stu-id="74364-161">Verbosity</span></span> | <span data-ttu-id="74364-162">출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="74364-162">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="74364-163">버전</span><span class="sxs-lookup"><span data-stu-id="74364-163">Version</span></span> | <span data-ttu-id="74364-164">설치할 패키지의 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="74364-164">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="74364-165">또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="74364-165">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="74364-166">예제</span><span class="sxs-lookup"><span data-stu-id="74364-166">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
