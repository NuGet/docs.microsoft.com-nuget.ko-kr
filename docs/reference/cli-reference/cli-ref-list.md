---
title: NuGet CLI 목록 명령
description: Nuget.exe 목록 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813340"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="a4ef5-103">list 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a4ef5-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="a4ef5-104">**적용 대상:** 패키지 사용, 게시 &bullet; **지원 되는 버전:** 모두</span><span class="sxs-lookup"><span data-stu-id="a4ef5-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a4ef5-105">지정 된 원본의 패키지 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="a4ef5-106">원본을 지정 하지 않으면 전역 구성 파일 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config`에 정의 된 모든 소스가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="a4ef5-107">`NuGet.Config`에서 소스를 지정 하지 않으면 `list` 기본 피드 (nuget.org)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="a4ef5-108">용도</span><span class="sxs-lookup"><span data-stu-id="a4ef5-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="a4ef5-109">여기서 선택적 검색 용어는 표시 된 목록을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="a4ef5-110">검색 용어는 nuget.org에서 사용 하는 경우와 마찬가지로 패키지, 태그 및 패키지 설명의 이름에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="a4ef5-111">Options</span><span class="sxs-lookup"><span data-stu-id="a4ef5-111">Options</span></span>

| <span data-ttu-id="a4ef5-112">옵션</span><span class="sxs-lookup"><span data-stu-id="a4ef5-112">Option</span></span> | <span data-ttu-id="a4ef5-113">설명</span><span class="sxs-lookup"><span data-stu-id="a4ef5-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a4ef5-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="a4ef5-114">AllVersions</span></span> | <span data-ttu-id="a4ef5-115">패키지의 모든 버전을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-115">List all versions of a package.</span></span> <span data-ttu-id="a4ef5-116">기본적으로 최신 패키지 버전만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="a4ef5-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a4ef5-117">ConfigFile</span></span> | <span data-ttu-id="a4ef5-118">수정할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a4ef5-119">지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a4ef5-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a4ef5-120">ForceEnglishOutput</span></span> | <span data-ttu-id="a4ef5-121">*(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a4ef5-122">도움말</span><span class="sxs-lookup"><span data-stu-id="a4ef5-122">Help</span></span> | <span data-ttu-id="a4ef5-123">명령어에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="a4ef5-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="a4ef5-124">IncludeDelisted</span></span> | <span data-ttu-id="a4ef5-125">*(3.2 이상)* 나열 되지 않은 패키지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="a4ef5-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a4ef5-126">NonInteractive</span></span> | <span data-ttu-id="a4ef5-127">사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a4ef5-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="a4ef5-128">PreRelease</span></span> | <span data-ttu-id="a4ef5-129">목록에 시험판 패키지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="a4ef5-130">소스</span><span class="sxs-lookup"><span data-stu-id="a4ef5-130">Source</span></span> | <span data-ttu-id="a4ef5-131">검색할 패키지 원본 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="a4ef5-132">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="a4ef5-132">Verbosity</span></span> | <span data-ttu-id="a4ef5-133">출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a4ef5-134">또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a4ef5-135">예</span><span class="sxs-lookup"><span data-stu-id="a4ef5-135">Examples</span></span>

<span data-ttu-id="a4ef5-136">구성 된 피드의 모든 패키지 나열:</span><span class="sxs-lookup"><span data-stu-id="a4ef5-136">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="a4ef5-137">자세한 자세한 정보 표시를 포함 하는 Azure 관련 패키지를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-137">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="a4ef5-138">구성 된 피드의 모든 버전의 Azure 관련 패키지를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-138">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="a4ef5-139">지정 된 원본/피드에서 JSON 관련 패키지의 모든 버전을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="a4ef5-139">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="a4ef5-140">여러 원본/피드에서 JSON 관련 패키지 나열:</span><span class="sxs-lookup"><span data-stu-id="a4ef5-140">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

