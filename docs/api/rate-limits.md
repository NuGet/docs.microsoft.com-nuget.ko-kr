---
title: 속도 제한, NuGet API
description: 속도 제한 남용을 방지 하기 위해 NuGet Api을 강제 적용 됩니다.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548679"
---
# <a name="rate-limits"></a><span data-ttu-id="cbd81-103">속도 제한</span><span class="sxs-lookup"><span data-stu-id="cbd81-103">Rate Limits</span></span>

<span data-ttu-id="cbd81-104">NuGet.org API 남용을 방지 하기 위해 속도 제한을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbd81-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="cbd81-105">요청 속도 제한을 초과 하는 다음 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbd81-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="cbd81-106">요청 속도 제한을 사용 하 여 제한 하는 것 외에도 일부 Api도 할당량을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbd81-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="cbd81-107">다음 오류를 반환 하는 할당량을 초과 하는 요청:</span><span class="sxs-lookup"><span data-stu-id="cbd81-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="cbd81-108">다음 표에서 NuGet.org API에 대 한 속도 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbd81-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="cbd81-109">패키지 검색</span><span class="sxs-lookup"><span data-stu-id="cbd81-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="cbd81-110">NuGet.org의를 사용 하는 것이 좋습니다 [V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource) 현재 검색 성능이 없는 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbd81-110">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="cbd81-111">V1 및 V2에 대 한 검색 Api, followins 제한이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cbd81-111">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="cbd81-112">API</span><span class="sxs-lookup"><span data-stu-id="cbd81-112">API</span></span> | <span data-ttu-id="cbd81-113">제한 유형</span><span class="sxs-lookup"><span data-stu-id="cbd81-113">Limit Type</span></span> | <span data-ttu-id="cbd81-114">제한 값</span><span class="sxs-lookup"><span data-stu-id="cbd81-114">Limit Value</span></span> | <span data-ttu-id="cbd81-115">API 사용</span><span class="sxs-lookup"><span data-stu-id="cbd81-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="cbd81-116">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="cbd81-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="cbd81-117">IP</span><span class="sxs-lookup"><span data-stu-id="cbd81-117">IP</span></span> | <span data-ttu-id="cbd81-118">1000 / 분</span><span class="sxs-lookup"><span data-stu-id="cbd81-118">1000 / minute</span></span> | <span data-ttu-id="cbd81-119">V1 OData 통해 NuGet 패키지 메타 데이터를 쿼리하여 `Packages` 컬렉션</span><span class="sxs-lookup"><span data-stu-id="cbd81-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="cbd81-120">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="cbd81-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="cbd81-121">IP</span><span class="sxs-lookup"><span data-stu-id="cbd81-121">IP</span></span> | <span data-ttu-id="cbd81-122">3000 / 분</span><span class="sxs-lookup"><span data-stu-id="cbd81-122">3000 / minute</span></span> | <span data-ttu-id="cbd81-123">V1 검색 끝점을 통해 NuGet 패키지 검색</span><span class="sxs-lookup"><span data-stu-id="cbd81-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="cbd81-124">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="cbd81-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="cbd81-125">IP</span><span class="sxs-lookup"><span data-stu-id="cbd81-125">IP</span></span> | <span data-ttu-id="cbd81-126">20000 / 분</span><span class="sxs-lookup"><span data-stu-id="cbd81-126">20000 / minute</span></span> | <span data-ttu-id="cbd81-127">V2 OData 통해 NuGet 패키지 메타 데이터를 쿼리하여 `Packages` 컬렉션</span><span class="sxs-lookup"><span data-stu-id="cbd81-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="cbd81-128">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="cbd81-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="cbd81-129">IP</span><span class="sxs-lookup"><span data-stu-id="cbd81-129">IP</span></span> | <span data-ttu-id="cbd81-130">100 / 분</span><span class="sxs-lookup"><span data-stu-id="cbd81-130">100 / minute</span></span> | <span data-ttu-id="cbd81-131">NuGet 패키지 개수 v2 OData 통해 쿼리 `Packages` 컬렉션</span><span class="sxs-lookup"><span data-stu-id="cbd81-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="cbd81-132">패키지의 나열을 취소 하 고 푸시</span><span class="sxs-lookup"><span data-stu-id="cbd81-132">Package Push and Unlist</span></span>

| <span data-ttu-id="cbd81-133">API</span><span class="sxs-lookup"><span data-stu-id="cbd81-133">API</span></span> | <span data-ttu-id="cbd81-134">제한 유형</span><span class="sxs-lookup"><span data-stu-id="cbd81-134">Limit Type</span></span> | <span data-ttu-id="cbd81-135">제한 값</span><span class="sxs-lookup"><span data-stu-id="cbd81-135">Limit Value</span></span> | <span data-ttu-id="cbd81-136">API 사용</span><span class="sxs-lookup"><span data-stu-id="cbd81-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="cbd81-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="cbd81-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="cbd81-138">API 키</span><span class="sxs-lookup"><span data-stu-id="cbd81-138">API Key</span></span> | <span data-ttu-id="cbd81-139">250 / 시간</span><span class="sxs-lookup"><span data-stu-id="cbd81-139">250 / hour</span></span> | <span data-ttu-id="cbd81-140">V2 푸시 끝점을 통해 새 NuGet 패키지 (버전)를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbd81-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="cbd81-141">**DELETE** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="cbd81-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="cbd81-142">API 키</span><span class="sxs-lookup"><span data-stu-id="cbd81-142">API Key</span></span> | <span data-ttu-id="cbd81-143">250 / 시간</span><span class="sxs-lookup"><span data-stu-id="cbd81-143">250 / hour</span></span> | <span data-ttu-id="cbd81-144">V2 끝점을 통해 NuGet 패키지 (버전)를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="cbd81-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
