---
title: NuGet CLI 목록 표시 명령
description: Nuget.exe 목록 명령에 대 한 참조
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4a44c70937e7cb49e472c53e9857e9f44d269f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="1c622-103">목록 표시 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1c622-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="1c622-104">**적용 대상:** 패키지 소비, 게시 &bullet; **지원 되는 버전:** 모든</span><span class="sxs-lookup"><span data-stu-id="1c622-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="1c622-105">지정된 된 원본에서 패키지의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c622-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="1c622-106">모든 소스에서 글로벌 구성 파일에 정의 된 원본이 지정 된 경우 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config`, 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c622-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="1c622-107">경우 `NuGet.Config` 다음 원본이 없습니다 지정 `list` 기본 피드 (nuget.org)를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c622-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="1c622-108">사용법</span><span class="sxs-lookup"><span data-stu-id="1c622-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="1c622-109">여기서 선택적 검색 단어에 표시 된 목록을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c622-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="1c622-110">검색어는 nuget.org 방화벽을 사용 하는 경우와 마찬가지로 패키지, 태그 및 패키지 설명의 이름에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c622-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="1c622-111">옵션</span><span class="sxs-lookup"><span data-stu-id="1c622-111">Options</span></span>

| <span data-ttu-id="1c622-112">옵션</span><span class="sxs-lookup"><span data-stu-id="1c622-112">Option</span></span> | <span data-ttu-id="1c622-113">설명</span><span class="sxs-lookup"><span data-stu-id="1c622-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1c622-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="1c622-114">AllVersions</span></span> | <span data-ttu-id="1c622-115">패키지의 모든 버전을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c622-115">List all versions of a package.</span></span> <span data-ttu-id="1c622-116">기본적으로는 최신 패키지 버전에만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c622-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="1c622-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1c622-117">ConfigFile</span></span> | <span data-ttu-id="1c622-118">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="1c622-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1c622-119">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c622-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1c622-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1c622-120">ForceEnglishOutput</span></span> | <span data-ttu-id="1c622-121">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c622-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1c622-122">도움말</span><span class="sxs-lookup"><span data-stu-id="1c622-122">Help</span></span> | <span data-ttu-id="1c622-123">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c622-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="1c622-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="1c622-124">IncludeDelisted</span></span> | <span data-ttu-id="1c622-125">*(3.2 +)*  목록에 없는 패키지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c622-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="1c622-126">비 대화형</span><span class="sxs-lookup"><span data-stu-id="1c622-126">NonInteractive</span></span> | <span data-ttu-id="1c622-127">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c622-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1c622-128">시험판</span><span class="sxs-lookup"><span data-stu-id="1c622-128">PreRelease</span></span> | <span data-ttu-id="1c622-129">목록에 시험판 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="1c622-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="1c622-130">소스</span><span class="sxs-lookup"><span data-stu-id="1c622-130">Source</span></span> | <span data-ttu-id="1c622-131">검색할 패키지 소스 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c622-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="1c622-132">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="1c622-132">Verbosity</span></span> | <span data-ttu-id="1c622-133">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="1c622-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="1c622-134">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1c622-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1c622-135">예제</span><span class="sxs-lookup"><span data-stu-id="1c622-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
