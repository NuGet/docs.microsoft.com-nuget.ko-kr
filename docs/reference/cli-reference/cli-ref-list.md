---
title: NuGet CLI 목록 명령
description: Nuget.exe 목록 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327740"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="b0d25-103">list 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b0d25-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="b0d25-104">**적용 대상:** 패키지 사용, &bullet; **지원 되는 버전 게시:** 모두</span><span class="sxs-lookup"><span data-stu-id="b0d25-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b0d25-105">지정 된 원본의 패키지 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d25-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="b0d25-106">소스를 지정 하지 않으면 전역 구성 파일 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config`에 정의 된 모든 소스가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0d25-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="b0d25-107">에서 소스를 지정 하지 않는 경우 `NuGet.Config` 는 기본 피드 (nuget.org)를 사용합니다.`list`</span><span class="sxs-lookup"><span data-stu-id="b0d25-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="b0d25-108">사용법</span><span class="sxs-lookup"><span data-stu-id="b0d25-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="b0d25-109">여기서 선택적 검색 용어는 표시 된 목록을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d25-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="b0d25-110">검색 용어는 nuget.org에서 사용 하는 경우와 마찬가지로 패키지, 태그 및 패키지 설명의 이름에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0d25-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="b0d25-111">변수</span><span class="sxs-lookup"><span data-stu-id="b0d25-111">Options</span></span>

| <span data-ttu-id="b0d25-112">옵션</span><span class="sxs-lookup"><span data-stu-id="b0d25-112">Option</span></span> | <span data-ttu-id="b0d25-113">Description</span><span class="sxs-lookup"><span data-stu-id="b0d25-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b0d25-114">Allversions)</span><span class="sxs-lookup"><span data-stu-id="b0d25-114">AllVersions</span></span> | <span data-ttu-id="b0d25-115">패키지의 모든 버전을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d25-115">List all versions of a package.</span></span> <span data-ttu-id="b0d25-116">기본적으로 최신 패키지 버전만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0d25-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="b0d25-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b0d25-117">ConfigFile</span></span> | <span data-ttu-id="b0d25-118">적용할 NuGet 설정 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b0d25-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b0d25-119">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b0d25-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b0d25-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b0d25-120">ForceEnglishOutput</span></span> | <span data-ttu-id="b0d25-121">*(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d25-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b0d25-122">Help</span><span class="sxs-lookup"><span data-stu-id="b0d25-122">Help</span></span> | <span data-ttu-id="b0d25-123">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d25-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="b0d25-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="b0d25-124">IncludeDelisted</span></span> | <span data-ttu-id="b0d25-125">*(3.2 이상)* 나열 되지 않은 패키지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d25-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="b0d25-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b0d25-126">NonInteractive</span></span> | <span data-ttu-id="b0d25-127">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d25-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b0d25-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="b0d25-128">PreRelease</span></span> | <span data-ttu-id="b0d25-129">목록에 시험판 패키지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d25-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="b0d25-130">Source</span><span class="sxs-lookup"><span data-stu-id="b0d25-130">Source</span></span> | <span data-ttu-id="b0d25-131">검색할 패키지 원본 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d25-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="b0d25-132">Verbosity</span><span class="sxs-lookup"><span data-stu-id="b0d25-132">Verbosity</span></span> | <span data-ttu-id="b0d25-133">출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="b0d25-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b0d25-134">또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0d25-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b0d25-135">예제</span><span class="sxs-lookup"><span data-stu-id="b0d25-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
