---
title: NuGet CLI 목록 명령
description: nuget.exe list 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a6a4ee434c43ad4865dba12f039b5d545a90d3c4
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238168"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="44f77-103">list 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="44f77-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="44f77-104">**적용 대상:** 패키지 사용, &bullet; **지원 되는 버전 게시:** 모두</span><span class="sxs-lookup"><span data-stu-id="44f77-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="44f77-105">지정 된 원본의 패키지 목록을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="44f77-106">소스를 지정 하지 않으면 전역 구성 파일 (Windows) 또는에 정의 된 모든 소스가 `%AppData%\NuGet\NuGet.Config` `~/.nuget/NuGet/NuGet.Config` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="44f77-107">`NuGet.Config`에서 소스를 지정 하지 않는 경우는 `list` 기본 피드 (nuget.org)를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="44f77-108">사용량</span><span class="sxs-lookup"><span data-stu-id="44f77-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="44f77-109">여기서 선택적 검색 용어는 표시 된 목록을 필터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="44f77-110">[검색 용어](../../consume-packages/finding-and-choosing-packages.md#search-syntax) 는 nuget.org에서 사용 하는 경우와 마찬가지로 패키지, 태그 및 패키지 설명의 이름에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-110">[Search terms](../../consume-packages/finding-and-choosing-packages.md#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="44f77-111">옵션</span><span class="sxs-lookup"><span data-stu-id="44f77-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="44f77-112">패키지의 모든 버전을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-112">List all versions of a package.</span></span> <span data-ttu-id="44f77-113">기본적으로 최신 패키지 버전만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="44f77-114">적용할 NuGet 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="44f77-115">지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="44f77-116">*(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="44f77-117">명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="44f77-118">*(3.2 이상)* 나열 되지 않은 패키지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="44f77-119">사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="44f77-120">목록에 시험판 패키지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="44f77-121">검색할 패키지 원본 목록을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-121">Specifies a list of packages sources to search.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="44f77-122">출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-122">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="44f77-123">[환경 변수](cli-ref-environment-variables.md) 참조</span><span class="sxs-lookup"><span data-stu-id="44f77-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="44f77-124">예제</span><span class="sxs-lookup"><span data-stu-id="44f77-124">Examples</span></span>

<span data-ttu-id="44f77-125">구성 된 피드의 모든 패키지 나열:</span><span class="sxs-lookup"><span data-stu-id="44f77-125">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="44f77-126">자세한 자세한 정보 표시를 포함 하는 Azure 관련 패키지를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-126">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="44f77-127">구성 된 피드의 모든 버전의 Azure 관련 패키지를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-127">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="44f77-128">지정 된 원본/피드에서 JSON 관련 패키지의 모든 버전을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="44f77-128">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="44f77-129">여러 원본/피드에서 JSON 관련 패키지 나열:</span><span class="sxs-lookup"><span data-stu-id="44f77-129">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```