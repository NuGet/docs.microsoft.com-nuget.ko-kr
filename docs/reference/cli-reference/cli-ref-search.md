---
title: NuGet CLI 검색 명령
description: nuget.exe 검색 명령에 대한 참조
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323663"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="5b327-103">search 명령(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5b327-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="5b327-104">**적용 대상:** 패키지 사용 &bullet; **지원 버전:** 5.8 이상</span><span class="sxs-lookup"><span data-stu-id="5b327-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="5b327-105">제공된 쿼리 문자열을 사용하여 지정된 소스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5b327-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="5b327-106">지정된 소스가 없으면 %AppData%\NuGet\NuGet.Config 정의된 모든 원본이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b327-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.Config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="5b327-107">사용</span><span class="sxs-lookup"><span data-stu-id="5b327-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="5b327-108">여기서 검색 용어는 nuget.org 사용할 때와 마찬가지로 패키지, 태그 및 패키지 설명의 이름에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b327-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="5b327-109">옵션</span><span class="sxs-lookup"><span data-stu-id="5b327-109">Options</span></span>

| <span data-ttu-id="5b327-110">이름</span><span class="sxs-lookup"><span data-stu-id="5b327-110">Name</span></span> | <span data-ttu-id="5b327-111">Description</span><span class="sxs-lookup"><span data-stu-id="5b327-111">Description</span></span> | <span data-ttu-id="5b327-112">사용</span><span class="sxs-lookup"><span data-stu-id="5b327-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="5b327-113">시험판</span><span class="sxs-lookup"><span data-stu-id="5b327-113">PreRelease</span></span> | <span data-ttu-id="5b327-114">사전 릴리스 패키지는 기본적으로 포함되지 않지만 이 인수를 사용하여 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b327-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="5b327-115">-PreRelease</span><span class="sxs-lookup"><span data-stu-id="5b327-115">-PreRelease</span></span> |
| <span data-ttu-id="5b327-116">원본</span><span class="sxs-lookup"><span data-stu-id="5b327-116">Source</span></span> | <span data-ttu-id="5b327-117">에서 기본 원본을 쿼리하는 대신 검색할 특정 패키지 __원본nuget.config__</span><span class="sxs-lookup"><span data-stu-id="5b327-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="5b327-118">-Source `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="5b327-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="5b327-119">Take</span><span class="sxs-lookup"><span data-stu-id="5b327-119">Take</span></span> | <span data-ttu-id="5b327-120">반환할 결과 수입니다.</span><span class="sxs-lookup"><span data-stu-id="5b327-120">The number of results to return.</span></span> <span data-ttu-id="5b327-121">기본값은 20입니다.</span><span class="sxs-lookup"><span data-stu-id="5b327-121">The default value is 20.</span></span> | <span data-ttu-id="5b327-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="5b327-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="5b327-123">자세한 정도</span><span class="sxs-lookup"><span data-stu-id="5b327-123">Verbosity</span></span> | <span data-ttu-id="5b327-124">출력에 표시할 세부 정보 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="5b327-124">The level of detail to display in the output.</span></span> <span data-ttu-id="5b327-125">기본값은 _일반_ 입니다.</span><span class="sxs-lookup"><span data-stu-id="5b327-125">The default is _normal_.</span></span> <span data-ttu-id="5b327-126">(아래 참고 참조)</span><span class="sxs-lookup"><span data-stu-id="5b327-126">(See the note below)</span></span>  | <span data-ttu-id="5b327-127">-Verbosity `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="5b327-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="5b327-128">도움말</span><span class="sxs-lookup"><span data-stu-id="5b327-128">Help</span></span> | <span data-ttu-id="5b327-129">명령에 대한 도움말 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5b327-129">Displays help information for the command</span></span> | <span data-ttu-id="5b327-130">-Help</span><span class="sxs-lookup"><span data-stu-id="5b327-130">-Help</span></span> |

<span data-ttu-id="5b327-131">환경 [변수도 참조하세요.](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5b327-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="5b327-132">자세한 정도 수준:</span><span class="sxs-lookup"><span data-stu-id="5b327-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="5b327-133">_quiet_ - 패키지 ID, 버전</span><span class="sxs-lookup"><span data-stu-id="5b327-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="5b327-134">_normal_ - 패키지 ID, 버전, 다운로드, 설명 미리 보기</span><span class="sxs-lookup"><span data-stu-id="5b327-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="5b327-135">_detailed_ - 패키지 ID, 버전, 다운로드, 전체 설명, 쿼리 URL과 같은 기타 정보</span><span class="sxs-lookup"><span data-stu-id="5b327-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="5b327-136">예</span><span class="sxs-lookup"><span data-stu-id="5b327-136">Examples</span></span>

<span data-ttu-id="5b327-137">기본 원본에서 *로깅* 관련 패키지를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5b327-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="5b327-138">자세한 세부 정보로 *로깅* 관련 패키지를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5b327-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="5b327-139">*로깅* 관련 패키지를 검색하고 상위 5개 결과만 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="5b327-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="5b327-140">지정된 소스/피드에서 *JSON* 관련 패키지(릴리스 전 버전 포함)를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5b327-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="5b327-141">여러 원본/피드에서 *JSON* 관련 패키지를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="5b327-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
