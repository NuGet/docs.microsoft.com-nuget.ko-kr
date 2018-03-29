---
title: NuGet CLI 목록 표시 명령 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe 목록 명령에 대 한 참조
keywords: nuget 목록 참조 패키지 목록 표시 명령
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 61ad02eb99d6c56968c38841498df8aa9f74159d
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="5333a-104">목록 표시 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5333a-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="5333a-105">**적용 대상:** 패키지 소비, 게시 &bullet; **지원 되는 버전:** 모든</span><span class="sxs-lookup"><span data-stu-id="5333a-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5333a-106">지정된 된 원본에서 패키지의 목록이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5333a-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="5333a-107">모든 소스에서 글로벌 구성 파일에 정의 된 원본이 지정 된 경우 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config`, 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5333a-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="5333a-108">경우 `NuGet.Config` 다음 원본이 없습니다 지정 `list` 기본 피드 (nuget.org)를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="5333a-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="5333a-109">사용법</span><span class="sxs-lookup"><span data-stu-id="5333a-109">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="5333a-110">여기서 선택적 검색 단어에 표시 된 목록을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="5333a-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="5333a-111">검색어는 nuget.org 방화벽을 사용 하는 경우와 마찬가지로 패키지, 태그 및 패키지 설명의 이름에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5333a-111">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="5333a-112">옵션</span><span class="sxs-lookup"><span data-stu-id="5333a-112">Options</span></span>

| <span data-ttu-id="5333a-113">옵션</span><span class="sxs-lookup"><span data-stu-id="5333a-113">Option</span></span> | <span data-ttu-id="5333a-114">설명</span><span class="sxs-lookup"><span data-stu-id="5333a-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5333a-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="5333a-115">AllVersions</span></span> | <span data-ttu-id="5333a-116">패키지의 모든 버전을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="5333a-116">List all versions of a package.</span></span> <span data-ttu-id="5333a-117">기본적으로는 최신 패키지 버전에만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5333a-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="5333a-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5333a-118">ConfigFile</span></span> | <span data-ttu-id="5333a-119">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5333a-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5333a-120">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5333a-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5333a-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5333a-121">ForceEnglishOutput</span></span> | <span data-ttu-id="5333a-122">*(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="5333a-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5333a-123">도움말</span><span class="sxs-lookup"><span data-stu-id="5333a-123">Help</span></span> | <span data-ttu-id="5333a-124">도움말의 명령에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5333a-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="5333a-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="5333a-125">IncludeDelisted</span></span> | <span data-ttu-id="5333a-126">*(3.2 +)*  목록에 없는 패키지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="5333a-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="5333a-127">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="5333a-127">NonInteractive</span></span> | <span data-ttu-id="5333a-128">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5333a-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5333a-129">시험판</span><span class="sxs-lookup"><span data-stu-id="5333a-129">PreRelease</span></span> | <span data-ttu-id="5333a-130">목록에 시험판 패키지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5333a-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="5333a-131">소스</span><span class="sxs-lookup"><span data-stu-id="5333a-131">Source</span></span> | <span data-ttu-id="5333a-132">검색할 패키지 소스 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5333a-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="5333a-133">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="5333a-133">Verbosity</span></span> | <span data-ttu-id="5333a-134">출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다.</span><span class="sxs-lookup"><span data-stu-id="5333a-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5333a-135">또한 참조 [환경 변수](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5333a-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5333a-136">예제</span><span class="sxs-lookup"><span data-stu-id="5333a-136">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
