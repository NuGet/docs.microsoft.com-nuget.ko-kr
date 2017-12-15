---
title: "NuGet CLI 명령 업데이트 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 61fde945-6983-46a5-8636-da0fada4e641
description: "Nuget.exe update 명령에 대 한 참조"
keywords: "nuget 업데이트 참조에 업데이트 패키지 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 654144e93a99a4a4f8d79c0db5660cfb7c6c308e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="abe61-104">업데이트 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="abe61-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="abe61-105">**적용 대상:** 소비 패키지 &bullet; **지원 되는 버전:** 모든</span><span class="sxs-lookup"><span data-stu-id="abe61-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="abe61-106">프로젝트의 모든 패키지를 업데이트 (사용 하 여 `packages.config`)를 사용할 수 있는 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="abe61-107">실행 하는 것이 좋습니다. ['restore'](#restore) 실행 하기 전에 `update`합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-107">It is recommended to run ['restore'](#restore) before running the `update`.</span></span> <span data-ttu-id="abe61-108">(사용 하 여 개별 패키지를 업데이트 하려면 [ `nuget install` ](cli-ref-install.md) 사례 NuGet 최신 버전을 설치 하는 버전 번호를 지정 하지 않고.)</span><span class="sxs-lookup"><span data-stu-id="abe61-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="abe61-109">참고: `update` 모노 (Mac OSX 또는 Linux)에서 실행 되는 CLI 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux).</span></span> <span data-ttu-id="abe61-110">이 명령은 또한를 사용 하 여 프로젝트와 함께 작동 하지 않습니다 `project.json` 또는 PackageReference 관리 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-110">The command also does not work with projects using `project.json` or PackageReference management formats.</span></span>

<span data-ttu-id="abe61-111">`update` 명령은 또한 프로젝트 파일에서 어셈블리 참조를 업데이트, 이미 참조 하는 것 제공 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-111">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="abe61-112">업데이트 된 패키지에 추가 된 어셈블리를 새 참조는 *하지* 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-112">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="abe61-113">또한 새 패키지 종속 파일의 어셈블리 참조 추가 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-113">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="abe61-114">이러한 작업에 대 한 업데이트의 일부로 포함 하려면 패키지 관리자 UI 또는 패키지 관리자 콘솔을 사용 하 여 Visual Studio에서 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-114">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="abe61-115">Nuget.exe 자체를 업데이트 하려면이 명령을 사용할 수도 있습니다를 사용 하는 *-자체* 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-115">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="abe61-116">용도</span><span class="sxs-lookup"><span data-stu-id="abe61-116">Usage</span></span>

```
nuget update <configPath> [options]
```

<span data-ttu-id="abe61-117">여기서 `<configPath>` 중 하나를 식별 하는 `packages.config` 또는 솔루션 파일을 프로젝트의 종속성을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-117">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="abe61-118">옵션</span><span class="sxs-lookup"><span data-stu-id="abe61-118">Options</span></span>

| <span data-ttu-id="abe61-119">옵션</span><span class="sxs-lookup"><span data-stu-id="abe61-119">Option</span></span> | <span data-ttu-id="abe61-120">설명</span><span class="sxs-lookup"><span data-stu-id="abe61-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="abe61-121">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="abe61-121">ConfigFile</span></span> | <span data-ttu-id="abe61-122">*(2.5 +)*  NuGet 구성 파일을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="abe61-123">지정 하지 않으면 *%AppData%\NuGet\NuGet.Config* 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="abe61-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="abe61-124">FileConflictAction</span></span> | <span data-ttu-id="abe61-125">*(2.5 +)*  덮어쓰거나 프로젝트에서 참조 하는 기존 파일을 무시 하도록 요청 될 때 수행할 동작을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-125">*(2.5+)* Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="abe61-126">값은 *덮어쓰기, none 무시*합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-126">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="abe61-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="abe61-127">ForceEnglishOutput</span></span> | <span data-ttu-id="abe61-128">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="abe61-129">도움말</span><span class="sxs-lookup"><span data-stu-id="abe61-129">Help</span></span> | <span data-ttu-id="abe61-130">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="abe61-131">ID</span><span class="sxs-lookup"><span data-stu-id="abe61-131">Id</span></span> | <span data-ttu-id="abe61-132">패키지를 업데이트 하는 Id의 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-132">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="abe61-133">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="abe61-133">MSBuildPath</span></span> | <span data-ttu-id="abe61-134">*(4.0 이상)*  우선 순위를 차지 명령으로 사용 하는 MSBuild의 경로 지정 `-MSBuildVersion`합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-134">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="abe61-135">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="abe61-135">MSBuildVersion</span></span> | <span data-ttu-id="abe61-136">*(3.2 +)*  이 명령과 함께 사용할 MSBuild의 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-136">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="abe61-137">지원 되는 값은 4, 12, 14, 15입니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-137">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="abe61-138">경로에 MSBuild 선택은 기본적으로 그렇지 않은 경우 기본값이 가장 높은 설치 된 버전의 MSBuild 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-138">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="abe61-139">비 대화형</span><span class="sxs-lookup"><span data-stu-id="abe61-139">NonInteractive</span></span> | <span data-ttu-id="abe61-140">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="abe61-141">시험판</span><span class="sxs-lookup"><span data-stu-id="abe61-141">PreRelease</span></span> | <span data-ttu-id="abe61-142">시험판 버전에 업데이트를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-142">Allows updating to prerelease versions.</span></span> <span data-ttu-id="abe61-143">이미 설치 되어 있는 시험판 패키지를 업데이트 하는 경우에이 플래그가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-143">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="abe61-144">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="abe61-144">RepositoryPath</span></span> | <span data-ttu-id="abe61-145">패키지 설치 된 로컬 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-145">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="abe61-146">안전</span><span class="sxs-lookup"><span data-stu-id="abe61-146">Safe</span></span> | <span data-ttu-id="abe61-147">업데이트 하는 동일한 주 및 부 버전에서 사용할 수 있는 가장 높은 버전으로 설치 된 패키지가 설치를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-147">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="abe61-148">자체</span><span class="sxs-lookup"><span data-stu-id="abe61-148">Self</span></span> | <span data-ttu-id="abe61-149">*(1.4 +)*  Nuget.exe; 최신 버전으로 업데이트 다른 모든 인수는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-149">*(1.4+)* Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="abe61-150">소스</span><span class="sxs-lookup"><span data-stu-id="abe61-150">Source</span></span> | <span data-ttu-id="abe61-151">업데이트를 사용 하도록 (Url)로 패키지 소스 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-151">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="abe61-152">구성 파일에 제공 된 원본을 사용 하 여 생략 된 경우, 참조 [NuGet 구성 동작](../Consume-Packages/Configuring-NuGet-Behavior.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-152">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="abe61-153">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="abe61-153">Verbosity</span></span> | <span data-ttu-id="abe61-154">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *세부 (2.5 이상)*합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-154">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="abe61-155">버전</span><span class="sxs-lookup"><span data-stu-id="abe61-155">Version</span></span> | <span data-ttu-id="abe61-156">하나의 패키지 ID를 사용할 때는 업데이트할 패키지의 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="abe61-156">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="abe61-157">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="abe61-157">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="abe61-158">예제</span><span class="sxs-lookup"><span data-stu-id="abe61-158">Examples</span></span>

```
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
