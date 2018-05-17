---
title: 속도 제한을 NuGet API
description: NuGet Api 남용 하지 않으려면 속도 제한을 강제 적용 됩니다.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: e236d685a700d0f47480336cece8edfd44c28863
ms.sourcegitcommit: 68c8a494a11c892ac671fec3170ba7be97fb044d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="rate-limits"></a><span data-ttu-id="90d51-103">속도 제한</span><span class="sxs-lookup"><span data-stu-id="90d51-103">Rate Limits</span></span>

<span data-ttu-id="90d51-104">NuGet.org API 남용 하지 않으려면 속도 제한 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="90d51-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="90d51-105">요청 속도 제한을 초과 하는 다음 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="90d51-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="90d51-106">다음 표에서 NuGet.org API에 대 한 속도 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="90d51-106">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="90d51-107">패키지 검색</span><span class="sxs-lookup"><span data-stu-id="90d51-107">Package search</span></span>

> [!Note]
> <span data-ttu-id="90d51-108">NuGet.org의를 사용 하는 것이 좋습니다 [V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource) 고성능 이며가 없는 있는 검색에 대 한 현재를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="90d51-108">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="90d51-109">V1 및 V2 검색 Api, followins 제한이 적용:</span><span class="sxs-lookup"><span data-stu-id="90d51-109">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="90d51-110">API</span><span class="sxs-lookup"><span data-stu-id="90d51-110">API</span></span> | <span data-ttu-id="90d51-111">제한 유형</span><span class="sxs-lookup"><span data-stu-id="90d51-111">Limit Type</span></span> | <span data-ttu-id="90d51-112">제한 값</span><span class="sxs-lookup"><span data-stu-id="90d51-112">Limit Value</span></span> | <span data-ttu-id="90d51-113">API 사용</span><span class="sxs-lookup"><span data-stu-id="90d51-113">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="90d51-114">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="90d51-114">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="90d51-115">IP</span><span class="sxs-lookup"><span data-stu-id="90d51-115">IP</span></span> | <span data-ttu-id="90d51-116">1000 / 분</span><span class="sxs-lookup"><span data-stu-id="90d51-116">1000 / minute</span></span> | <span data-ttu-id="90d51-117">OData v 1 통해 NuGet 패키지 메타 데이터를 쿼리 `Packages` 컬렉션</span><span class="sxs-lookup"><span data-stu-id="90d51-117">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="90d51-118">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="90d51-118">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="90d51-119">IP</span><span class="sxs-lookup"><span data-stu-id="90d51-119">IP</span></span> | <span data-ttu-id="90d51-120">3000 / 분</span><span class="sxs-lookup"><span data-stu-id="90d51-120">3000 / minute</span></span> | <span data-ttu-id="90d51-121">V1 검색 끝점을 통해 NuGet 패키지에 대 한 검색</span><span class="sxs-lookup"><span data-stu-id="90d51-121">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="90d51-122">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="90d51-122">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="90d51-123">IP</span><span class="sxs-lookup"><span data-stu-id="90d51-123">IP</span></span> | <span data-ttu-id="90d51-124">20000 / 분</span><span class="sxs-lookup"><span data-stu-id="90d51-124">20000 / minute</span></span> | <span data-ttu-id="90d51-125">OData v 2 통해 NuGet 패키지 메타 데이터 쿼리 `Packages` 컬렉션</span><span class="sxs-lookup"><span data-stu-id="90d51-125">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="90d51-126">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="90d51-126">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="90d51-127">IP</span><span class="sxs-lookup"><span data-stu-id="90d51-127">IP</span></span> | <span data-ttu-id="90d51-128">100 / 분</span><span class="sxs-lookup"><span data-stu-id="90d51-128">100 / minute</span></span> | <span data-ttu-id="90d51-129">NuGet 패키지 개수 v2 OData 통해 쿼리 `Packages` 컬렉션</span><span class="sxs-lookup"><span data-stu-id="90d51-129">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="90d51-130">패키지 푸시하고 Unlist</span><span class="sxs-lookup"><span data-stu-id="90d51-130">Package Push and Unlist</span></span>

| <span data-ttu-id="90d51-131">API</span><span class="sxs-lookup"><span data-stu-id="90d51-131">API</span></span> | <span data-ttu-id="90d51-132">제한 유형</span><span class="sxs-lookup"><span data-stu-id="90d51-132">Limit Type</span></span> | <span data-ttu-id="90d51-133">제한 값</span><span class="sxs-lookup"><span data-stu-id="90d51-133">Limit Value</span></span> | <span data-ttu-id="90d51-134">API 사용</span><span class="sxs-lookup"><span data-stu-id="90d51-134">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="90d51-135">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="90d51-135">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="90d51-136">API 키</span><span class="sxs-lookup"><span data-stu-id="90d51-136">API Key</span></span> | <span data-ttu-id="90d51-137">100 / 분</span><span class="sxs-lookup"><span data-stu-id="90d51-137">100 / minute</span></span> | <span data-ttu-id="90d51-138">V2 푸시 끝점을 통해 새 NuGet 패키지 (버전)를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="90d51-138">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="90d51-139">**삭제** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="90d51-139">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="90d51-140">API 키</span><span class="sxs-lookup"><span data-stu-id="90d51-140">API Key</span></span> | <span data-ttu-id="90d51-141">100 / 분</span><span class="sxs-lookup"><span data-stu-id="90d51-141">100 / minute</span></span> | <span data-ttu-id="90d51-142">Unlist v2 끝점을 통해 NuGet 패키지 (버전)</span><span class="sxs-lookup"><span data-stu-id="90d51-142">Unlist a NuGet package (version) via v2 endpoint</span></span> 
