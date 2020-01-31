---
title: 요율 한도, NuGet API
description: NuGet Api는 남용을 방지 하기 위해 적용 되는 요금 제한을 적용 합니다.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813197"
---
# <a name="rate-limits"></a><span data-ttu-id="f1b4b-103">속도 제한</span><span class="sxs-lookup"><span data-stu-id="f1b4b-103">Rate Limits</span></span>

<span data-ttu-id="f1b4b-104">NuGet.org API는 악용을 방지 하기 위해 요금 제한을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b4b-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="f1b4b-105">Rate 제한을 초과 하는 요청은 다음 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b4b-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="f1b4b-106">요금 제한을 사용 하 여 요청을 제한 하는 것 외에도 일부 Api는 할당량을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b4b-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="f1b4b-107">할당량을 초과 하는 요청은 다음 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b4b-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="f1b4b-108">다음 표에서는 NuGet.org API에 대 한 요율 제한을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="f1b4b-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="f1b4b-109">패키지 검색</span><span class="sxs-lookup"><span data-stu-id="f1b4b-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="f1b4b-110">현재는 전송률이 제한 되지 않으므로 Nuget.exe의 [V3 검색 api](search-query-service-resource.md) 를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f1b4b-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="f1b4b-111">V1 및 V2 검색 Api의 경우 다음과 같은 제한이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1b4b-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="f1b4b-112">API</span><span class="sxs-lookup"><span data-stu-id="f1b4b-112">API</span></span> | <span data-ttu-id="f1b4b-113">제한 유형</span><span class="sxs-lookup"><span data-stu-id="f1b4b-113">Limit Type</span></span> | <span data-ttu-id="f1b4b-114">제한 값</span><span class="sxs-lookup"><span data-stu-id="f1b4b-114">Limit Value</span></span> | <span data-ttu-id="f1b4b-115">API 사용 사례</span><span class="sxs-lookup"><span data-stu-id="f1b4b-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="f1b4b-116">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="f1b4b-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="f1b4b-117">IP</span><span class="sxs-lookup"><span data-stu-id="f1b4b-117">IP</span></span> | <span data-ttu-id="f1b4b-118">1000/분</span><span class="sxs-lookup"><span data-stu-id="f1b4b-118">1000 / minute</span></span> | <span data-ttu-id="f1b4b-119">V1 OData `Packages` 컬렉션을 통해 NuGet 패키지 메타 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="f1b4b-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="f1b4b-120">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="f1b4b-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="f1b4b-121">IP</span><span class="sxs-lookup"><span data-stu-id="f1b4b-121">IP</span></span> | <span data-ttu-id="f1b4b-122">3000/분</span><span class="sxs-lookup"><span data-stu-id="f1b4b-122">3000 / minute</span></span> | <span data-ttu-id="f1b4b-123">V1 검색 끝점을 통해 NuGet 패키지 검색</span><span class="sxs-lookup"><span data-stu-id="f1b4b-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="f1b4b-124">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="f1b4b-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="f1b4b-125">IP</span><span class="sxs-lookup"><span data-stu-id="f1b4b-125">IP</span></span> | <span data-ttu-id="f1b4b-126">2만/분</span><span class="sxs-lookup"><span data-stu-id="f1b4b-126">20000 / minute</span></span> | <span data-ttu-id="f1b4b-127">V2 OData `Packages` 컬렉션을 통해 NuGet 패키지 메타 데이터 쿼리</span><span class="sxs-lookup"><span data-stu-id="f1b4b-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="f1b4b-128">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="f1b4b-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="f1b4b-129">IP</span><span class="sxs-lookup"><span data-stu-id="f1b4b-129">IP</span></span> | <span data-ttu-id="f1b4b-130">100/분</span><span class="sxs-lookup"><span data-stu-id="f1b4b-130">100 / minute</span></span> | <span data-ttu-id="f1b4b-131">V2 OData `Packages` 컬렉션을 통해 NuGet 패키지 수 쿼리</span><span class="sxs-lookup"><span data-stu-id="f1b4b-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="f1b4b-132">패키지 푸시 및 목록 제거</span><span class="sxs-lookup"><span data-stu-id="f1b4b-132">Package Push and Unlist</span></span>

| <span data-ttu-id="f1b4b-133">API</span><span class="sxs-lookup"><span data-stu-id="f1b4b-133">API</span></span> | <span data-ttu-id="f1b4b-134">제한 유형</span><span class="sxs-lookup"><span data-stu-id="f1b4b-134">Limit Type</span></span> | <span data-ttu-id="f1b4b-135">제한 값</span><span class="sxs-lookup"><span data-stu-id="f1b4b-135">Limit Value</span></span> | <span data-ttu-id="f1b4b-136">API 사용 사례</span><span class="sxs-lookup"><span data-stu-id="f1b4b-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="f1b4b-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="f1b4b-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="f1b4b-138">API 키</span><span class="sxs-lookup"><span data-stu-id="f1b4b-138">API Key</span></span> | <span data-ttu-id="f1b4b-139">350/시간</span><span class="sxs-lookup"><span data-stu-id="f1b4b-139">350 / hour</span></span> | <span data-ttu-id="f1b4b-140">V2 푸시 끝점을 통해 새 NuGet 패키지 (버전) 업로드</span><span class="sxs-lookup"><span data-stu-id="f1b4b-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="f1b4b-141">`/api/v2/package/{id}/{version}` **삭제**</span><span class="sxs-lookup"><span data-stu-id="f1b4b-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="f1b4b-142">API 키</span><span class="sxs-lookup"><span data-stu-id="f1b4b-142">API Key</span></span> | <span data-ttu-id="f1b4b-143">250/시간</span><span class="sxs-lookup"><span data-stu-id="f1b4b-143">250 / hour</span></span> | <span data-ttu-id="f1b4b-144">V2 끝점을 통해 NuGet 패키지 (버전) 나열 제거</span><span class="sxs-lookup"><span data-stu-id="f1b4b-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
