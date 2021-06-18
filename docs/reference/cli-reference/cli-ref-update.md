---
title: NuGet CLI 업데이트 명령
description: nuget.exe 업데이트 명령에 대한 참조
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323650"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="8bb39-103">update 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8bb39-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="8bb39-104">**적용 대상:** 패키지 사용 &bullet; **지원 버전:** 모두</span><span class="sxs-lookup"><span data-stu-id="8bb39-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8bb39-105">프로젝트의 모든 패키지(`packages.config` 사용)를 사용 가능한 최신 버전으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="8bb39-106">를 실행하기 전에 ['restore'를](cli-ref-restore.md) 실행하는 것이 `update` 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="8bb39-107">(개별 패키지를 업데이트하려면 버전 번호를 지정하지 않고 를 사용합니다. [`nuget install`](cli-ref-install.md) 이 경우 NuGet은 최신 버전을 설치합니다.)</span><span class="sxs-lookup"><span data-stu-id="8bb39-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="8bb39-108">참고: `update` 는 Mono(Mac OSX 또는 Linux)에서 실행되거나 PackageReference 형식을 사용하는 경우 CLI에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="8bb39-109">또한 이 `update` 명령은 해당 참조가 이미 있는 경우 프로젝트 파일에서 어셈블리 참조를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="8bb39-110">업데이트된 패키지에 어셈블리가 추가된 경우 새 참조가 *추가되지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="8bb39-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="8bb39-111">새 패키지 의존성에도 어셈블리 참조가 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="8bb39-112">이러한 작업을 업데이트의 일부로 포함하려면 패키지 관리자 UI 또는 패키지 관리자 콘솔을 사용하여 Visual Studio 패키지를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="8bb39-113">이 명령은 *-self* 플래그를 사용하여 nuget.exe 업데이트하는 데도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="8bb39-114">사용</span><span class="sxs-lookup"><span data-stu-id="8bb39-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="8bb39-115">여기서 `<configPath>` 는 `packages.config` 프로젝트의 dependencies를 나열하는 또는 솔루션 파일을 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="8bb39-116">옵션</span><span class="sxs-lookup"><span data-stu-id="8bb39-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="8bb39-117">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="8bb39-118">지정하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  <span data-ttu-id="8bb39-119">사용할 종속성 패키지의 버전을 지정합니다. 이 버전은 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-119">Specifies the version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="8bb39-120">*가장 낮게(기본값):* 가장 낮은 버전</span><span class="sxs-lookup"><span data-stu-id="8bb39-120">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="8bb39-121">*HighestPatch:* 주 패치가 가장 낮고, 부 버전이 가장 낮고, 패치가 가장 높은 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-121">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="8bb39-122">*HighestMinor*: 주, 가장 높은 부 버전, 가장 높은 패치가 있는 버전</span><span class="sxs-lookup"><span data-stu-id="8bb39-122">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="8bb39-123">*Highest:* 가장 높은 버전</span><span class="sxs-lookup"><span data-stu-id="8bb39-123">*Highest*: the highest version</span></span></li><li><span data-ttu-id="8bb39-124">*무시:* 종속성 패키지가 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-124">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="8bb39-125">패키지의 파일이 대상 프로젝트에 이미 있는 경우 기본 동작을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-125">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="8bb39-126">항상 `Overwrite` 파일을 덮어쓰려면 로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-126">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="8bb39-127">파일을 `Ignore` 건너뛰려면 로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-127">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="8bb39-128">`PromptUser`작업( 기본값)은 또는 가 제공되지 않는 한 충돌하는 각 파일에 대한 메시지를 `OverwriteAll` `IgnoreAll` 표시하며, 이는 나머지 모든 파일에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-128">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="8bb39-129">*(3.5 이상)* 고정 영어 기반 문화권으로 nuget.exe 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-129">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="8bb39-130">명령에 대한 도움말 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-130">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="8bb39-131">업데이트할 패키지 ID 목록을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-131">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="8bb39-132">*(4.0 이상)* 보다 우선적으로 명령에 사용할 MSBuild의 경로를 `-MSBuildVersion` 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="8bb39-133">*(3.2 이상)* 이 명령과 함께 사용할 MSBuild의 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-133">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="8bb39-134">지원되는 값은 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9입니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-134">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="8bb39-135">기본적으로 경로의 MSBuild가 선택되며, 그렇지 않으면 기본적으로 설치된 가장 높은 버전의 MSBuild로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-135">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="8bb39-136">사용자 입력 또는 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-136">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="8bb39-137">사전 버전으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-137">Allows updating to prerelease versions.</span></span> <span data-ttu-id="8bb39-138">이 플래그는 이미 설치된 prerelease 패키지를 업데이트할 때 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-138">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="8bb39-139">패키지가 설치되는 로컬 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-139">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="8bb39-140">설치된 패키지와 동일한 주 버전 및 부 버전 내에서 사용할 수 있는 가장 높은 버전의 업데이트만 설치할 것을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-140">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="8bb39-141">최신 `nuget.exe` 버전으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-141">Updates `nuget.exe` to the latest version.</span></span> <span data-ttu-id="8bb39-142">`-Source` 를 사용할 수 있습니다. 그러나 다른 모든 인수는 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-142">`-Source` can be used however all other arguments are ignored.</span></span> <span data-ttu-id="8bb39-143">소스가 제공되지 않으면 `nuget.org` 설정에 관계없이 에서 업데이트를 확인합니다. `NuGet.Config`</span><span class="sxs-lookup"><span data-stu-id="8bb39-143">If no source is provided, checks `nuget.org` for updates regardless of `NuGet.Config` settings.</span></span>

- **`-Source`**

  <span data-ttu-id="8bb39-144">업데이트에 사용할 패키지 원본 목록을 URL로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-144">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="8bb39-145">생략하면 명령은 구성 파일에 제공된 소스를 사용합니다. 일반적인 [NuGet 구성을 참조하세요.](../../consume-packages/configuring-nuget-behavior.md)</span><span class="sxs-lookup"><span data-stu-id="8bb39-145">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="8bb39-146">(기본값), 또는 출력에 표시되는 세부 정보의 양을 `normal` `quiet` `detailed` 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-146">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="8bb39-147">하나의 패키지 ID와 함께 사용할 경우 업데이트할 패키지의 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8bb39-147">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="8bb39-148">환경 [변수도 참조하세요.](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8bb39-148">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8bb39-149">예</span><span class="sxs-lookup"><span data-stu-id="8bb39-149">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
