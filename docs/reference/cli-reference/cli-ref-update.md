---
title: NuGet CLI 업데이트 명령
description: Nuget.exe update 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327510"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="69f1b-103">update 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="69f1b-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="69f1b-104">**적용 대상:** 패키지 &bullet; 사용 **지원 버전:** 모두</span><span class="sxs-lookup"><span data-stu-id="69f1b-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="69f1b-105">프로젝트의 모든 패키지(`packages.config` 사용)를 사용 가능한 최신 버전으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="69f1b-106">을`update`실행 하기 전에 [' 복원 '](cli-ref-restore.md) 을 실행 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="69f1b-107">개별 패키지를 업데이트 하려면 버전 번호를 [`nuget install`](cli-ref-install.md) 지정 하지 않고를 사용 합니다 .이 경우 NuGet은 최신 버전을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="69f1b-108">참고: `update` 는 Mono (Mac OSX 또는 Linux)에서 실행 되는 CLI 또는 PackageReference 형식을 사용 하는 경우에는 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="69f1b-109">이러한 참조가 이미 있는 경우이 명령은프로젝트파일의어셈블리참조도업데이트합니다.`update`</span><span class="sxs-lookup"><span data-stu-id="69f1b-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="69f1b-110">업데이트 된 패키지에 추가 된 어셈블리가 있으면 새 참조가 추가 *되지 않습니다* .</span><span class="sxs-lookup"><span data-stu-id="69f1b-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="69f1b-111">새 패키지 종속성에도 해당 어셈블리 참조가 추가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="69f1b-112">이러한 작업을 업데이트의 일부로 포함 하려면 패키지 관리자 UI 또는 패키지 관리자 콘솔을 사용 하 여 Visual Studio에서 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="69f1b-113">이 명령은 *-self* 플래그를 사용 하 여 nuget.exe 자체를 업데이트 하는 데도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="69f1b-114">사용법</span><span class="sxs-lookup"><span data-stu-id="69f1b-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="69f1b-115">여기서 `<configPath>` 는 프로젝트의 `packages.config` 종속성을 나열 하는 또는 솔루션 파일을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="69f1b-116">변수</span><span class="sxs-lookup"><span data-stu-id="69f1b-116">Options</span></span>

| <span data-ttu-id="69f1b-117">옵션</span><span class="sxs-lookup"><span data-stu-id="69f1b-117">Option</span></span> | <span data-ttu-id="69f1b-118">설명</span><span class="sxs-lookup"><span data-stu-id="69f1b-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="69f1b-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="69f1b-119">ConfigFile</span></span> | <span data-ttu-id="69f1b-120">적용할 NuGet 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="69f1b-121">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="69f1b-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="69f1b-122">FileConflictAction</span></span> | <span data-ttu-id="69f1b-123">프로젝트에서 참조 하는 기존 파일을 덮어쓰거나 무시 하도록 요청 된 경우 수행할 동작을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="69f1b-124">값은 *overwrite, ignore, none*입니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="69f1b-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="69f1b-125">ForceEnglishOutput</span></span> | <span data-ttu-id="69f1b-126">*(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="69f1b-127">Help</span><span class="sxs-lookup"><span data-stu-id="69f1b-127">Help</span></span> | <span data-ttu-id="69f1b-128">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="69f1b-129">ID</span><span class="sxs-lookup"><span data-stu-id="69f1b-129">Id</span></span> | <span data-ttu-id="69f1b-130">업데이트할 패키지 Id의 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="69f1b-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="69f1b-131">MSBuildPath</span></span> | <span data-ttu-id="69f1b-132">*(4.0 이상)* 명령에 사용할 MSBuild의 경로를 지정 합니다 `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="69f1b-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="69f1b-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="69f1b-133">MSBuildVersion</span></span> | <span data-ttu-id="69f1b-134">*(3.2 이상)* 이 명령에 사용할 MSBuild의 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="69f1b-135">지원 되는 값은 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9입니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="69f1b-136">기본적으로 경로에 MSBuild가 선택 되어 있으며, 그렇지 않은 경우 기본적으로 설치 되어 있는 MSBuild의 가장 높은 버전으로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="69f1b-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="69f1b-137">NonInteractive</span></span> | <span data-ttu-id="69f1b-138">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="69f1b-139">PreRelease</span><span class="sxs-lookup"><span data-stu-id="69f1b-139">PreRelease</span></span> | <span data-ttu-id="69f1b-140">시험판 버전으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="69f1b-141">이미 설치 된 시험판 패키지를 업데이트 하는 경우에는이 플래그가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="69f1b-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="69f1b-142">RepositoryPath</span></span> | <span data-ttu-id="69f1b-143">패키지가 설치 되는 로컬 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="69f1b-144">색상</span><span class="sxs-lookup"><span data-stu-id="69f1b-144">Safe</span></span> | <span data-ttu-id="69f1b-145">설치 된 패키지와 동일한 주 버전 및 부 버전 내에서 가장 높은 버전의 업데이트만 사용할 수 있도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="69f1b-146">자체</span><span class="sxs-lookup"><span data-stu-id="69f1b-146">Self</span></span> | <span data-ttu-id="69f1b-147">Nuget.exe를 최신 버전으로 업데이트 합니다. 다른 모든 인수는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="69f1b-148">Source</span><span class="sxs-lookup"><span data-stu-id="69f1b-148">Source</span></span> | <span data-ttu-id="69f1b-149">업데이트에 사용할 패키지 원본 (Url) 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="69f1b-150">생략 하는 경우 명령은 구성 파일에 제공 된 소스를 사용 합니다. [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="69f1b-150">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="69f1b-151">Verbosity</span><span class="sxs-lookup"><span data-stu-id="69f1b-151">Verbosity</span></span> | <span data-ttu-id="69f1b-152">출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="69f1b-153">버전</span><span class="sxs-lookup"><span data-stu-id="69f1b-153">Version</span></span> | <span data-ttu-id="69f1b-154">하나의 패키지 ID와 함께 사용 하는 경우 업데이트할 패키지의 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="69f1b-155">또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69f1b-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="69f1b-156">예제</span><span class="sxs-lookup"><span data-stu-id="69f1b-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
