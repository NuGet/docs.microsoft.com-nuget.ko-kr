---
title: NuGet CLI 설치 명령
description: nuget.exe install 명령에 대 한 참조
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 34b79bfa7a0dddf5da6b5c465293caec49129f6c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779261"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="4d718-103">install 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="4d718-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="4d718-104">**적용 대상:** 패키지 사용 &bullet; **지원 버전:** 모두</span><span class="sxs-lookup"><span data-stu-id="4d718-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="4d718-105">패키지를 다운로드 하 여 프로젝트에 설치 합니다. 기본적으로 현재 폴더는 지정 된 패키지 소스를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="4d718-106">프로젝트의 컨텍스트 외부에서 직접 패키지를 다운로드 하려면 [nuget.org](https://www.nuget.org) 의 패키지 페이지를 방문 하 여 **다운로드** 링크를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="4d718-107">지정 된 원본이 없으면 전역 구성 파일 `%appdata%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)에 나열 된 소스가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="4d718-108">자세한 내용은 [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md) 을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="4d718-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="4d718-109">특정 패키지를 지정 하지 않으면는 `install` 프로젝트의 파일에 나열 된 모든 패키지를 설치 하 `packages.config` 여와 유사 하 게 만듭니다 [`restore`](cli-ref-restore.md) .</span><span class="sxs-lookup"><span data-stu-id="4d718-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="4d718-110">`install`이 명령은 프로젝트 파일을 수정 하지 않습니다 `packages.config` .이 방법에서는 `restore` 패키지를 디스크에만 추가 하지만 프로젝트의 종속성은 변경 하지 않는다는 점에서와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="4d718-111">종속성을 추가 하려면 Visual Studio에서 패키지 관리자 UI 또는 콘솔을 통해 패키지를 추가 하거나를 수정 `packages.config` 하 고 또는를 실행 `install` `restore` 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="4d718-112">사용량</span><span class="sxs-lookup"><span data-stu-id="4d718-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="4d718-113">여기서는 `<packageID>` 최신 버전을 사용 하 여 설치할 패키지의 이름을, 또는 `<configFilePath>` `packages.config` 설치할 패키지를 나열 하는 파일을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="4d718-114">옵션을 사용 하 여 특정 버전을 나타낼 수 있습니다 `-Version` .</span><span class="sxs-lookup"><span data-stu-id="4d718-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="4d718-115">옵션</span><span class="sxs-lookup"><span data-stu-id="4d718-115">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="4d718-116">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="4d718-117">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DependencyVersion`**

  <span data-ttu-id="4d718-118">*(4.4 +)* 사용할 종속성 패키지의 버전은 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-118">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="4d718-119">*가장 낮음* (기본값): 가장 낮은 버전</span><span class="sxs-lookup"><span data-stu-id="4d718-119">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="4d718-120">*HighestPatch*: 최하위 주, 최저 부, 최고 패치가 있는 버전</span><span class="sxs-lookup"><span data-stu-id="4d718-120">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="4d718-121">*HighestMinor*: 최하위 주, 가장 높은 부, 최고 패치가 있는 버전</span><span class="sxs-lookup"><span data-stu-id="4d718-121">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="4d718-122">*최고*: 최고 버전</span><span class="sxs-lookup"><span data-stu-id="4d718-122">*Highest*: the highest version</span></span></li><li><span data-ttu-id="4d718-123">*무시*: 종속성 패키지가 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-123">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-DirectDownload`**

  <span data-ttu-id="4d718-124">메타 데이터 또는 이진 파일을 사용 하 여 캐시를 채우지 않고 직접 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-124">Download directly without populating any caches with metadata or binaries.</span></span>

- **`-DisableParallelProcessing`**

  <span data-ttu-id="4d718-125">여러 패키지를 동시에 설치할 수 없도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-125">Disables installing multiple packages in parallel.</span></span>

- **`-x|-ExcludeVersion`**

  <span data-ttu-id="4d718-126">패키지 이름만 사용 하 고 버전 번호를 사용 하 여 라는 이름의 폴더에 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-126">Installs the package to a folder named with only the package name and not the version number.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="4d718-127">*(3.2 이상)* 주 또는 기본 원본에서 패키지를 찾을 수 없는 경우 대체로 사용할 패키지 원본 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-127">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="4d718-128">*(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Framework`**

  <span data-ttu-id="4d718-129">*(4.4 +)* 종속성을 선택 하는 데 사용 되는 대상 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-129">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="4d718-130">지정 하지 않으면 기본값은 ' a l l '입니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-130">Defaults to 'Any' if not specified.</span></span>

- **`-?|-help`**

  <span data-ttu-id="4d718-131">명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-131">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="4d718-132">NuGet이 캐시 된 패키지를 사용 하지 못하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="4d718-133">[전역 패키지 및 캐시 폴더 관리](../../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="4d718-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="4d718-134">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="4d718-135">패키지가 설치 되는 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="4d718-136">폴더를 지정 하지 않으면 현재 폴더가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-136">If no folder is specified, the current folder is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="4d718-137">패키지 설치 후 저장할 파일 유형을 지정 합니다., 또는 중 하나 `nuspec` 입니다 `nupkg` `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="4d718-137">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="4d718-138">시험판 패키지를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-138">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="4d718-139">이 플래그는를 사용 하 여 패키지를 복원 하는 경우에는 필요 하지 않습니다 `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="4d718-139">This flag is not required when restoring packages with `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="4d718-140">패키지를 다운로드 하 고 설치 하기 전에 패키지 복원이 사용 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-140">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="4d718-141">자세한 내용은 [패키지 복원](../../consume-packages/package-restore.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="4d718-141">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="4d718-142">패키지를 복원할 솔루션의 루트 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-142">Specifies root folder of the solution for which to restore packages.</span></span>

- **`-Source`**

   <span data-ttu-id="4d718-143">사용할 패키지 원본 (Url) 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-143">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="4d718-144">생략 하는 경우 명령은 구성 파일에 제공 된 소스를 사용 합니다. [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="4d718-144">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="4d718-145">출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-145">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="4d718-146">설치할 패키지의 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4d718-146">Specifies the version of the package to install.</span></span>

<span data-ttu-id="4d718-147">[환경 변수](cli-ref-environment-variables.md) 참조</span><span class="sxs-lookup"><span data-stu-id="4d718-147">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="4d718-148">예</span><span class="sxs-lookup"><span data-stu-id="4d718-148">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
