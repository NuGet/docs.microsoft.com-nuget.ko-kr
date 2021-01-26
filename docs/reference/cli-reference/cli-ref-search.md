---
title: NuGet CLI 검색 명령
description: nuget.exe 검색 명령에 대 한 참조
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 6f4adcdf3981e5ec0e5e88337a8c3bcdd9158ca3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779162"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="e7cbe-103">검색 명령 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="e7cbe-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="e7cbe-104">**적용 대상:** 패키지 사용 &bullet; **지원 버전:** 5.8 +</span><span class="sxs-lookup"><span data-stu-id="e7cbe-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="e7cbe-105">제공 된 쿼리 문자열을 사용 하 여 지정 된 소스를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7cbe-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="e7cbe-106">원본을 지정 하지 않으면% AppData% \NuGet\NuGet.config에 정의 된 모든 원본이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7cbe-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="e7cbe-107">사용량</span><span class="sxs-lookup"><span data-stu-id="e7cbe-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="e7cbe-108">여기서 검색 용어는 nuget.org에서 사용 하는 경우와 마찬가지로 패키지, 태그 및 패키지 설명의 이름에 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7cbe-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="e7cbe-109">옵션</span><span class="sxs-lookup"><span data-stu-id="e7cbe-109">Options</span></span>

| <span data-ttu-id="e7cbe-110">이름</span><span class="sxs-lookup"><span data-stu-id="e7cbe-110">Name</span></span> | <span data-ttu-id="e7cbe-111">Description</span><span class="sxs-lookup"><span data-stu-id="e7cbe-111">Description</span></span> | <span data-ttu-id="e7cbe-112">사용량</span><span class="sxs-lookup"><span data-stu-id="e7cbe-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="e7cbe-113">시험판</span><span class="sxs-lookup"><span data-stu-id="e7cbe-113">PreRelease</span></span> | <span data-ttu-id="e7cbe-114">시험판 패키지는 기본적으로 포함 되어 있지 않지만이 인수를 사용 하 여 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7cbe-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="e7cbe-115">-시험판</span><span class="sxs-lookup"><span data-stu-id="e7cbe-115">-PreRelease</span></span> |
| <span data-ttu-id="e7cbe-116">원본</span><span class="sxs-lookup"><span data-stu-id="e7cbe-116">Source</span></span> | <span data-ttu-id="e7cbe-117">__nuget.config__ 에서 기본 소스를 쿼리 하는 대신 검색할 특정 패키지 원본</span><span class="sxs-lookup"><span data-stu-id="e7cbe-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="e7cbe-118">-원본 `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="e7cbe-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="e7cbe-119">Take</span><span class="sxs-lookup"><span data-stu-id="e7cbe-119">Take</span></span> | <span data-ttu-id="e7cbe-120">반환할 결과의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="e7cbe-120">The number of results to return.</span></span> <span data-ttu-id="e7cbe-121">기본값은 20입니다.</span><span class="sxs-lookup"><span data-stu-id="e7cbe-121">The default value is 20.</span></span> | <span data-ttu-id="e7cbe-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="e7cbe-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="e7cbe-123">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="e7cbe-123">Verbosity</span></span> | <span data-ttu-id="e7cbe-124">출력에 표시할 세부 정보 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="e7cbe-124">The level of detail to display in the output.</span></span> <span data-ttu-id="e7cbe-125">기본값은 _normal_ 입니다.</span><span class="sxs-lookup"><span data-stu-id="e7cbe-125">The default is _normal_.</span></span> <span data-ttu-id="e7cbe-126">(아래 참고 참조)</span><span class="sxs-lookup"><span data-stu-id="e7cbe-126">(See the note below)</span></span>  | <span data-ttu-id="e7cbe-127">-자세한 정도 `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="e7cbe-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="e7cbe-128">도움말</span><span class="sxs-lookup"><span data-stu-id="e7cbe-128">Help</span></span> | <span data-ttu-id="e7cbe-129">명령에 대 한 도움말 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7cbe-129">Displays help information for the command</span></span> | <span data-ttu-id="e7cbe-130">-Help</span><span class="sxs-lookup"><span data-stu-id="e7cbe-130">-Help</span></span> |

<span data-ttu-id="e7cbe-131">[환경 변수](cli-ref-environment-variables.md) 참조</span><span class="sxs-lookup"><span data-stu-id="e7cbe-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="e7cbe-132">자세한 표시 수준:</span><span class="sxs-lookup"><span data-stu-id="e7cbe-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="e7cbe-133">_자동_ 패키지 ID, 버전</span><span class="sxs-lookup"><span data-stu-id="e7cbe-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="e7cbe-134">_일반_ -패키지 ID, 버전, 다운로드, 설명 미리 보기</span><span class="sxs-lookup"><span data-stu-id="e7cbe-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="e7cbe-135">_세부_ 정보-패키지 ID, 버전, 다운로드, 전체 설명, 쿼리 URL과 같은 기타 정보</span><span class="sxs-lookup"><span data-stu-id="e7cbe-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="e7cbe-136">예제</span><span class="sxs-lookup"><span data-stu-id="e7cbe-136">Examples</span></span>

<span data-ttu-id="e7cbe-137">기본 원본에서 *로깅* 관련 패키지 검색:</span><span class="sxs-lookup"><span data-stu-id="e7cbe-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="e7cbe-138">자세한 자세한 정보 표시를 사용 하 여 *로깅* 관련 패키지를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7cbe-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="e7cbe-139">*로깅* 관련 패키지를 검색 하 고 상위 5 개 결과만 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7cbe-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="e7cbe-140">지정 된 원본/피드의 시험판 버전을 포함 하 여 *JSON* 관련 패키지를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7cbe-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="e7cbe-141">여러 원본/피드에서 *JSON* 관련 패키지 검색:</span><span class="sxs-lookup"><span data-stu-id="e7cbe-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
