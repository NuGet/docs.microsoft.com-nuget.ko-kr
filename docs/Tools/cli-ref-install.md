---
title: "NuGet CLI 설치 명령 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 59ac622f-837c-4545-bc93-a56330e02d71
description: "Nuget.exe 설치 명령에 대 한 참조"
keywords: "nuget 참조 패키지 명령을 설치,"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88c123a7f2a3d628713cefcc4b110fb0205093b4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="45594-104">명령 (NuGet CLI)를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="45594-105">**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 모든</span><span class="sxs-lookup"><span data-stu-id="45594-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="45594-106">다운로드 하 고 지정 된 패키지 소스를 사용 하 여 현재 폴더를 프로젝트에 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="45594-107">프로젝트의 컨텍스트 외부 직접 패키지를 다운로드 하려면 패키지의 페이지를 방문 하십시오 [nuget.org](https://www.nuget.org) 선택 하 고는 **다운로드** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span> 

<span data-ttu-id="45594-108">글로벌 구성 파일에 나열 된 원본이 지정 된 경우 `%APPDATA%\NuGet\NuGet.Config`, 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45594-108">If no sources are specified, those listed in the global configuration file, `%APPDATA%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="45594-109">참조 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md) 추가 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-109">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="45594-110">특정 패키지를 지정 하는 경우 `install` 프로젝트의에 나열 된 패키지를 모두 설치 `packages.config` 파일 그룹과 같이 [ `restore` ](#restore)합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](#restore).</span></span> <span data-ttu-id="45594-111">(의 `install` 명령이와 작동 하지 않는다 `project.json`.)</span><span class="sxs-lookup"><span data-stu-id="45594-111">(The `install` command does not work with `project.json`.)</span></span>

<span data-ttu-id="45594-112">`install` 프로젝트 파일 수정 되지 않도록 또는 `packages.config`; 비슷하지만 이런 방식에서 `restore` 한다는 점에서 것만 디스크에 패키지를 추가 하면 프로젝트의 종속성을 변경 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="45594-112">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="45594-113">종속성을 추가 하려면 Visual Studio에서 패키지 관리자 UI 또는 콘솔을 통해 프로젝트를 추가 하거나 수정 `packages.config` 하나를 실행 하 고 `install` 또는 `restore`합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-113">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span> <span data-ttu-id="45594-114">사용 하 여 프로젝트에 대 한 `project.json`, 해당 파일을 수정 하 고 다음 실행 `restore`합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-114">For projects using `project.json`, you can modify that file and then run `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="45594-115">용도</span><span class="sxs-lookup"><span data-stu-id="45594-115">Usage</span></span>

```
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="45594-116">여기서 `<packageID>` (최신 버전 사용)를 설치 하려면 패키지 이름을 지정 하거나 `<configFilePath>` 식별는 `packages.config` 설치할 패키지를 나열 하는 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="45594-116">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="45594-117">특정 버전을 나타낼 수 있습니다는 `-Version` 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="45594-117">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="45594-118">옵션</span><span class="sxs-lookup"><span data-stu-id="45594-118">Options</span></span>

| <span data-ttu-id="45594-119">옵션</span><span class="sxs-lookup"><span data-stu-id="45594-119">Option</span></span> | <span data-ttu-id="45594-120">설명</span><span class="sxs-lookup"><span data-stu-id="45594-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="45594-121">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="45594-121">ConfigFile</span></span> | <span data-ttu-id="45594-122">*(2.5 +)*  NuGet 구성 파일을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="45594-123">지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45594-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="45594-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="45594-124">DisableParallelProcessing</span></span> | <span data-ttu-id="45594-125">동시에 여러 패키지를 설치 하는 데 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="45594-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="45594-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="45594-126">ExcludeVersion</span></span> | <span data-ttu-id="45594-127">패키지 이름과 버전 번호가 아닙니다 라는 폴더를 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="45594-128">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="45594-128">FallbackSource</span></span> | <span data-ttu-id="45594-129">*(3.2 +)*  패키지 주에서 찾을 수 없는 경우 대체도 사용할 패키지 소스 목록 또는 기본 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="45594-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="45594-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="45594-130">ForceEnglishOutput</span></span> | <span data-ttu-id="45594-131">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="45594-132">프레임워크</span><span class="sxs-lookup"><span data-stu-id="45594-132">Framework</span></span> | <span data-ttu-id="45594-133">*(4.4 +)*  대상 프레임 워크 종속성을 선택 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="45594-134">기본값은 'Any' 형식 지정 하지 않은 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="45594-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="45594-135">도움말</span><span class="sxs-lookup"><span data-stu-id="45594-135">Help</span></span> | <span data-ttu-id="45594-136">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="45594-137">캐시 없음</span><span class="sxs-lookup"><span data-stu-id="45594-137">NoCache</span></span> | <span data-ttu-id="45594-138">NuGet 패키지를 사용 하 여 로컬 컴퓨터 캐시에서 방지 합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="45594-139">비 대화형</span><span class="sxs-lookup"><span data-stu-id="45594-139">NonInteractive</span></span> | <span data-ttu-id="45594-140">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="45594-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="45594-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="45594-141">OutputDirectory</span></span> | <span data-ttu-id="45594-142">패키지 설치 되는 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="45594-143">없는 폴더를 지정 하는 경우 현재 폴더가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45594-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="45594-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="45594-144">PackageSaveMode</span></span> | <span data-ttu-id="45594-145">패키지 설치 후 저장할 파일의 형식을 지정 합니다: 중 `nuspec`, `nupkg`, 또는 `nuspec;nupkg`합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="45594-146">시험판</span><span class="sxs-lookup"><span data-stu-id="45594-146">PreRelease</span></span> | <span data-ttu-id="45594-147">시험판 패키지를를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45594-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="45594-148">사용 하 여 패키지를 복원 하는 경우이 플래그는 필요 하지 `packages.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="45594-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="45594-149">RequireConsent</span></span> | <span data-ttu-id="45594-150">다운로드 하 고 패키지를 설치 하기 전에 패키지를 복원 활성화 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="45594-151">자세한 내용은 참조 [패키지 복원](../consume-packages/package-restore.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="45594-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="45594-152">SolutionDirectory</span></span> | <span data-ttu-id="45594-153">패키지를 복원 하도록 솔루션의 루트 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="45594-154">소스</span><span class="sxs-lookup"><span data-stu-id="45594-154">Source</span></span> | <span data-ttu-id="45594-155">(Url)로 패키지 소스 목록의 사용 하도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="45594-156">구성 파일에 제공 된 원본을 사용 하 여 생략 된 경우, 참조 [NuGet 구성 동작](../Consume-Packages/Configuring-NuGet-Behavior.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="45594-157">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="45594-157">Verbosity</span></span> | <span data-ttu-id="45594-158">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *세부 (2.5 이상)*합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="45594-159">버전</span><span class="sxs-lookup"><span data-stu-id="45594-159">Version</span></span> | <span data-ttu-id="45594-160">설치할 패키지의 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="45594-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="45594-161">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="45594-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="45594-162">예제</span><span class="sxs-lookup"><span data-stu-id="45594-162">Examples</span></span>

```
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
