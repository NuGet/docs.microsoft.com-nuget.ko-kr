---
title: NuGet CLI 업데이트 명령
description: Nuget.exe 업데이트 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ded9b571324d810c2f0e1a46ea76375a28940406
ms.sourcegitcommit: d5a35a097e6b461ae791d9f66b3a85d5219d7305
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56145607"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="75df6-103">update 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="75df6-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="75df6-104">**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 모든</span><span class="sxs-lookup"><span data-stu-id="75df6-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="75df6-105">프로젝트의 모든 패키지 업데이트 (사용 하 여 `packages.config`) 사용 가능한 최신 버전으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="75df6-106">실행 하는 것이 좋습니다 ['restore'](cli-ref-restore.md) 실행 하기 전에 `update`합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="75df6-107">(사용 하 여 개별 패키지를 업데이트 하려면 [ `nuget install` ](cli-ref-install.md) 사례 NuGet 최신 버전을 설치 하는 버전 번호를 지정 하지 않고.)</span><span class="sxs-lookup"><span data-stu-id="75df6-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="75df6-108">참고: `update` PackageReference 형식을 사용 하는 경우 Mono (Mac OSX 또는 Linux)에서 또는 실행 하는 CLI를 사용 하 여 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="75df6-109">`update` 명령은 프로젝트 파일에서 어셈블리 참조를 업데이트도, 이미 참조 된 제공 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="75df6-110">새 참조는 업데이트 된 패키지에 어셈블리를 추가 하는 경우 *되지* 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="75df6-111">또한 새 패키지 종속성 추가 어셈블리 참조는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="75df6-112">이러한 작업에는 업데이트의 일부로 포함 하려면 패키지 관리자 UI 또는 패키지 관리자 콘솔을 사용 하 여 Visual Studio에서 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="75df6-113">Nuget.exe 자체를 업데이트 하려면이 명령을 사용할 수도 있습니다를 사용 하는 *-자체* 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="75df6-114">사용법</span><span class="sxs-lookup"><span data-stu-id="75df6-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="75df6-115">여기서 `<configPath>` 중 하나를 식별 하는 `packages.config` 또는 프로젝트의 종속성을 나열 하는 솔루션 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="75df6-116">옵션</span><span class="sxs-lookup"><span data-stu-id="75df6-116">Options</span></span>

| <span data-ttu-id="75df6-117">옵션</span><span class="sxs-lookup"><span data-stu-id="75df6-117">Option</span></span> | <span data-ttu-id="75df6-118">설명</span><span class="sxs-lookup"><span data-stu-id="75df6-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="75df6-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="75df6-119">ConfigFile</span></span> | <span data-ttu-id="75df6-120">수정할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="75df6-121">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="75df6-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="75df6-122">FileConflictAction</span></span> | <span data-ttu-id="75df6-123">덮어쓰거나 프로젝트에서 참조 하는 기존 파일을 무시 하 라는 메시지가 표시 되는 경우 수행할 동작을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="75df6-124">값은 *덮어쓰기, none 무시*합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="75df6-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="75df6-125">ForceEnglishOutput</span></span> | <span data-ttu-id="75df6-126">*(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="75df6-127">도움말</span><span class="sxs-lookup"><span data-stu-id="75df6-127">Help</span></span> | <span data-ttu-id="75df6-128">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="75df6-129">ID</span><span class="sxs-lookup"><span data-stu-id="75df6-129">Id</span></span> | <span data-ttu-id="75df6-130">패키지를 업데이트 하는 Id의 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="75df6-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="75df6-131">MSBuildPath</span></span> | <span data-ttu-id="75df6-132">*(4.0 이상)*  보다 우선함 명령으로 사용 하는 MSBuild의 경로 지정 `-MSBuildVersion`합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="75df6-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="75df6-133">MSBuildVersion</span></span> | <span data-ttu-id="75df6-134">*(3.2 이상)*  이 명령을 사용 하 여 사용할 MSBuild의 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="75df6-135">지원 되는 값은 4, 12, 14, 15.1, 15.3, 15.4에서 15.5, 15.6, 15.7, 15.8, 15.9.</span><span class="sxs-lookup"><span data-stu-id="75df6-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="75df6-136">경로에 MSBuild 선택은 기본적으로 그렇지 않은 경우 기본값은 MSBuild의 설치 된 가장 높은 버전으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="75df6-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="75df6-137">NonInteractive</span></span> | <span data-ttu-id="75df6-138">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="75df6-139">PreRelease</span><span class="sxs-lookup"><span data-stu-id="75df6-139">PreRelease</span></span> | <span data-ttu-id="75df6-140">시험판 버전으로 업데이트를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="75df6-141">이미 설치 되어 있는 시험판 패키지를 업데이트 하는 경우이 플래그는 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="75df6-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="75df6-142">RepositoryPath</span></span> | <span data-ttu-id="75df6-143">패키지 설치 되어 있는 로컬 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="75df6-144">안전 하 게 보호</span><span class="sxs-lookup"><span data-stu-id="75df6-144">Safe</span></span> | <span data-ttu-id="75df6-145">만 업데이트 하는 동일한 주 및 부 버전에서 사용할 수 있는 가장 높은 버전을 사용 하 여 설치 된 패키지를 설치할 때 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="75df6-146">자체</span><span class="sxs-lookup"><span data-stu-id="75df6-146">Self</span></span> | <span data-ttu-id="75df6-147">Nuget.exe를 최신 버전; 업데이트 다른 모든 인수는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="75df6-148">소스</span><span class="sxs-lookup"><span data-stu-id="75df6-148">Source</span></span> | <span data-ttu-id="75df6-149">업데이트에 사용할 (Url)로 패키지 소스 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="75df6-150">생략 하면 사용 하 여 구성 파일에서 제공 하는 소스를 참조 하십시오 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="75df6-151">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="75df6-151">Verbosity</span></span> | <span data-ttu-id="75df6-152">출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="75df6-153">버전</span><span class="sxs-lookup"><span data-stu-id="75df6-153">Version</span></span> | <span data-ttu-id="75df6-154">하나의 패키지 ID를 사용 하면 업데이트할 패키지의 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="75df6-155">또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75df6-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="75df6-156">예제</span><span class="sxs-lookup"><span data-stu-id="75df6-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
