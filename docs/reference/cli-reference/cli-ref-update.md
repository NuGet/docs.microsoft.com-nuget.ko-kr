---
title: NuGet CLI 업데이트 명령
description: nuget.exe update 명령에 대 한 참조
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: cfa7fdcc6af46fd5f4030ba424754291f697bc43
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779135"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="14e15-103">update 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="14e15-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="14e15-104">**적용 대상:** 패키지 사용 &bullet; **지원 버전:** 모두</span><span class="sxs-lookup"><span data-stu-id="14e15-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="14e15-105">프로젝트의 모든 패키지(`packages.config` 사용)를 사용 가능한 최신 버전으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="14e15-106">을 실행 하기 전에 [' 복원 '](cli-ref-restore.md) 을 실행 하는 것이 좋습니다 `update` .</span><span class="sxs-lookup"><span data-stu-id="14e15-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="14e15-107">개별 패키지를 업데이트 하려면 [`nuget install`](cli-ref-install.md) 버전 번호를 지정 하지 않고를 사용 합니다 .이 경우 NuGet은 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="14e15-108">참고: `update` 는 Mono (MAC OSX 또는 Linux)에서 실행 되는 CLI 또는 PackageReference 형식을 사용 하는 경우에는 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="14e15-109">`update`이러한 참조가 이미 있는 경우이 명령은 프로젝트 파일의 어셈블리 참조도 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="14e15-110">업데이트 된 패키지에 추가 된 어셈블리가 있으면 새 참조가 추가 *되지 않습니다* .</span><span class="sxs-lookup"><span data-stu-id="14e15-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="14e15-111">새 패키지 종속성에도 해당 어셈블리 참조가 추가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="14e15-112">이러한 작업을 업데이트의 일부로 포함 하려면 패키지 관리자 UI 또는 패키지 관리자 콘솔을 사용 하 여 Visual Studio에서 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="14e15-113">이 명령은 *-self* 플래그를 사용 하 여 nuget.exe 자체를 업데이트 하는 데도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="14e15-114">사용량</span><span class="sxs-lookup"><span data-stu-id="14e15-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="14e15-115">여기서는 `<configPath>` `packages.config` 프로젝트의 종속성을 나열 하는 또는 솔루션 파일을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="14e15-116">옵션</span><span class="sxs-lookup"><span data-stu-id="14e15-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="14e15-117">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="14e15-118">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  <span data-ttu-id="14e15-119">사용할 종속성 패키지의 버전을 지정 합니다. 다음 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-119">Specifies the version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="14e15-120">*가장 낮음* (기본값): 가장 낮은 버전</span><span class="sxs-lookup"><span data-stu-id="14e15-120">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="14e15-121">*HighestPatch*: 최하위 주, 최저 부, 최고 패치가 있는 버전</span><span class="sxs-lookup"><span data-stu-id="14e15-121">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="14e15-122">*HighestMinor*: 최하위 주, 가장 높은 부, 최고 패치가 있는 버전</span><span class="sxs-lookup"><span data-stu-id="14e15-122">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="14e15-123">*최고*: 최고 버전</span><span class="sxs-lookup"><span data-stu-id="14e15-123">*Highest*: the highest version</span></span></li><li><span data-ttu-id="14e15-124">*무시*: 종속성 패키지가 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-124">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="14e15-125">패키지의 파일이 대상 프로젝트에 이미 있는 경우의 기본 동작을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-125">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="14e15-126">`Overwrite`항상 파일을 덮어쓰려면로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-126">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="14e15-127">파일을 `Ignore` 건너뛰려면로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-127">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="14e15-128">`PromptUser`기본값은 또는가 제공 되지 않은 경우 충돌 하는 각 파일에 대해 메시지를 표시 `OverwriteAll` `IgnoreAll` 하며 나머지 모든 파일에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-128">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="14e15-129">*(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-129">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="14e15-130">명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-130">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="14e15-131">업데이트할 패키지 Id의 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-131">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="14e15-132">*(4.0 이상)* 명령에 사용할 MSBuild의 경로를 지정 합니다 `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="14e15-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="14e15-133">*(3.2 이상)* 이 명령에 사용할 MSBuild의 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-133">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="14e15-134">지원 되는 값은 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9입니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-134">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="14e15-135">기본적으로 경로에 MSBuild가 선택 되어 있으며, 그렇지 않은 경우 기본적으로 설치 되어 있는 MSBuild의 가장 높은 버전으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-135">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="14e15-136">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-136">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="14e15-137">시험판 버전으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-137">Allows updating to prerelease versions.</span></span> <span data-ttu-id="14e15-138">이미 설치 된 시험판 패키지를 업데이트 하는 경우에는이 플래그가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-138">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="14e15-139">패키지가 설치 되는 로컬 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-139">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="14e15-140">설치 된 패키지와 동일한 주 버전 및 부 버전 내에서 가장 높은 버전의 업데이트만 사용할 수 있도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-140">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="14e15-141">최신 버전으로 nuget.exe 업데이트 다른 모든 인수는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-141">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span>

- **`-Source`**

  <span data-ttu-id="14e15-142">업데이트에 사용할 패키지 원본 (Url) 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-142">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="14e15-143">생략 하는 경우 명령은 구성 파일에 제공 된 소스를 사용 합니다. [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="14e15-143">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="14e15-144">출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-144">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="14e15-145">하나의 패키지 ID와 함께 사용 하는 경우 업데이트할 패키지의 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="14e15-145">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="14e15-146">[환경 변수](cli-ref-environment-variables.md) 참조</span><span class="sxs-lookup"><span data-stu-id="14e15-146">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="14e15-147">예</span><span class="sxs-lookup"><span data-stu-id="14e15-147">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
