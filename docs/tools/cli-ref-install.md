---
title: NuGet CLI 설치 명령
description: Nuget.exe 설치 명령에 대 한 참조
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e609b01bc14083ce212f6d4d4c6d3412f0ee316b
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508324"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="b1670-103">install 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b1670-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="b1670-104">**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 모든</span><span class="sxs-lookup"><span data-stu-id="b1670-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b1670-105">다운로드 하 고 지정 된 패키지 소스를 사용 하 여 현재 폴더를 기본값으로 프로젝트에 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="b1670-106">프로젝트의 컨텍스트 외부 직접 패키지를 다운로드 하려면에 패키지의 페이지를 방문 [nuget.org](https://www.nuget.org) 선택 합니다 **다운로드** 링크.</span><span class="sxs-lookup"><span data-stu-id="b1670-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="b1670-107">전역 구성 파일에 없는 소스를 지정 하는 경우 나열한 `%appdata%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="b1670-108">참조 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md) 추가 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-108">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="b1670-109">없는 특정 패키지를 지정 하는 경우 `install` 프로젝트의 나열 된 모든 패키지를 설치 `packages.config` 파일을 유사 하므로 [ `restore` ](cli-ref-restore.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="b1670-110">합니다 `install` 명령은 프로젝트 파일을 수정 하지 않습니다 또는 `packages.config`; 비슷합니다 이런 `restore` 것만 디스크에 패키지를 추가 하지만 프로젝트의 종속성을 변경 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="b1670-111">종속성을 추가 하려면 Visual Studio에서 패키지 관리자 UI 또는 콘솔을 통해 패키지를 추가 또는 수정 `packages.config` 하나를 실행할 `install` 또는 `restore`합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="b1670-112">사용법</span><span class="sxs-lookup"><span data-stu-id="b1670-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="b1670-113">여기서 `<packageID>` (최신 버전 사용) 설치를 위해 패키지 이름 또는 `<configFilePath>` 하 게 식별 하는 `packages.config` 나열 패키지를 설치 하는 파일.</span><span class="sxs-lookup"><span data-stu-id="b1670-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="b1670-114">사용 하 여 특정 버전을 지정할 수 있습니다는 `-Version` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="b1670-115">옵션</span><span class="sxs-lookup"><span data-stu-id="b1670-115">Options</span></span>

| <span data-ttu-id="b1670-116">옵션</span><span class="sxs-lookup"><span data-stu-id="b1670-116">Option</span></span> | <span data-ttu-id="b1670-117">설명</span><span class="sxs-lookup"><span data-stu-id="b1670-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b1670-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b1670-118">ConfigFile</span></span> | <span data-ttu-id="b1670-119">NuGet 구성 파일을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b1670-120">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b1670-121">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="b1670-121">DependencyVersion</span></span> | <span data-ttu-id="b1670-122">*(4.4 이상)*  다음 중 하나일 수 있습니다를 사용 하려면 종속성 패키지의 버전:</span><span class="sxs-lookup"><span data-stu-id="b1670-122">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="b1670-123">*가장 낮은* (기본값): 가장 낮은 버전</span><span class="sxs-lookup"><span data-stu-id="b1670-123">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="b1670-124">*HighestPatch*: 가장 낮은 주요, 가장 낮은 부 최고 패치 버전</span><span class="sxs-lookup"><span data-stu-id="b1670-124">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="b1670-125">*HighestMinor*: 가장 낮은 주 버전, 가장 높은 보조, 최고의 패치</span><span class="sxs-lookup"><span data-stu-id="b1670-125">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="b1670-126">*가장 높은*: 가장 높은 버전</span><span class="sxs-lookup"><span data-stu-id="b1670-126">*Highest*: the highest version</span></span></li></ul> |
| <span data-ttu-id="b1670-127">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="b1670-127">DisableParallelProcessing</span></span> | <span data-ttu-id="b1670-128">병렬로 여러 패키지를 설치 하는 사용 하지 않도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-128">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="b1670-129">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="b1670-129">ExcludeVersion</span></span> | <span data-ttu-id="b1670-130">패키지 이름과 버전 번호가 없습니다 사용 하 여 폴더에 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-130">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="b1670-131">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="b1670-131">FallbackSource</span></span> | <span data-ttu-id="b1670-132">*(3.2 이상)*  패키지 주 서버에 없는 경우 대체도 사용할 패키지 원본의 목록 또는 기본 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-132">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="b1670-133">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b1670-133">ForceEnglishOutput</span></span> | <span data-ttu-id="b1670-134">*(3.5 이상)*  고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-134">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b1670-135">프레임워크</span><span class="sxs-lookup"><span data-stu-id="b1670-135">Framework</span></span> | <span data-ttu-id="b1670-136">*(4.4 이상)*  대상 프레임 워크 종속성을 선택 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-136">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="b1670-137">기본값은 'Any' 지정 되지 않은 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-137">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="b1670-138">도움말</span><span class="sxs-lookup"><span data-stu-id="b1670-138">Help</span></span> | <span data-ttu-id="b1670-139">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-139">Displays help information for the command.</span></span> |
| <span data-ttu-id="b1670-140">NoCache</span><span class="sxs-lookup"><span data-stu-id="b1670-140">NoCache</span></span> | <span data-ttu-id="b1670-141">캐시 된 패키지를 사용 하 여 NuGet을 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-141">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="b1670-142">참조 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-142">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="b1670-143">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b1670-143">NonInteractive</span></span> | <span data-ttu-id="b1670-144">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-144">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b1670-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="b1670-145">OutputDirectory</span></span> | <span data-ttu-id="b1670-146">패키지 설치 되는 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-146">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="b1670-147">폴더는 지정 하지 않으면 현재 폴더가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-147">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="b1670-148">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="b1670-148">PackageSaveMode</span></span> | <span data-ttu-id="b1670-149">패키지를 설치한 후 파일의 형식을 지정 합니다: 중 하나 `nuspec`, `nupkg`, 또는 `nuspec;nupkg`합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-149">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="b1670-150">PreRelease</span><span class="sxs-lookup"><span data-stu-id="b1670-150">PreRelease</span></span> | <span data-ttu-id="b1670-151">시험판 패키지를를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-151">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="b1670-152">사용 하 여 패키지를 복원 하는 경우이 플래그는 필요 하지 `packages.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-152">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="b1670-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="b1670-153">RequireConsent</span></span> | <span data-ttu-id="b1670-154">다운로드 하 고 패키지를 설치 하기 전에 패키지 복원 활성화 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="b1670-155">자세한 내용은 참조 하세요 [패키지 복원](../consume-packages/package-restore.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-155">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="b1670-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="b1670-156">SolutionDirectory</span></span> | <span data-ttu-id="b1670-157">패키지를 복원 하는 솔루션의 루트 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-157">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="b1670-158">소스</span><span class="sxs-lookup"><span data-stu-id="b1670-158">Source</span></span> | <span data-ttu-id="b1670-159">사용 하도록 (Url)로 패키지 소스 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-159">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="b1670-160">생략 하면 사용 하 여 구성 파일에서 제공 하는 소스를 참조 하십시오 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-160">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="b1670-161">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="b1670-161">Verbosity</span></span> | <span data-ttu-id="b1670-162">출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-162">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="b1670-163">버전</span><span class="sxs-lookup"><span data-stu-id="b1670-163">Version</span></span> | <span data-ttu-id="b1670-164">설치 패키지의 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1670-164">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="b1670-165">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b1670-165">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b1670-166">예제</span><span class="sxs-lookup"><span data-stu-id="b1670-166">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
