---
title: 속도 제한 | Microsoft Docs
author:
- cmanu
- anangaur
ms.author:
- cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet Api 남용 하지 않으려면 속도 제한을 강제 적용 됩니다.
keywords: NuGet API 비율 제한
ms.reviewer:
- skofman
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f7891d5e4c008219d9f4808f223f3e5e7ae06ced
ms.sourcegitcommit: fa40be739d093a37d5f7072b62ebdb4f595f4110
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2018
---
# <a name="rate-limits"></a><span data-ttu-id="f9dd6-104">속도 제한</span><span class="sxs-lookup"><span data-stu-id="f9dd6-104">Rate Limits</span></span>

<span data-ttu-id="f9dd6-105">NuGet.org API 남용 하지 않으려면 속도 제한 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dd6-105">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="f9dd6-106">요청 속도 제한을 초과 하는 다음 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dd6-106">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="f9dd6-107">다음 표에서 NuGet.org API에 대 한 속도 제한입니다.</span><span class="sxs-lookup"><span data-stu-id="f9dd6-107">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="f9dd6-108">패키지 검색</span><span class="sxs-lookup"><span data-stu-id="f9dd6-108">Package search</span></span>

> [!Note]
> <span data-ttu-id="f9dd6-109">NuGet.org의를 사용 하는 것이 좋습니다 [V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource) 고성능 이며가 없는 있는 검색에 대 한 현재를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dd6-109">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="f9dd6-110">V1 및 V2 검색 Api, followins 제한이 적용:</span><span class="sxs-lookup"><span data-stu-id="f9dd6-110">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="f9dd6-111">API</span><span class="sxs-lookup"><span data-stu-id="f9dd6-111">API</span></span> | <span data-ttu-id="f9dd6-112">제한 유형</span><span class="sxs-lookup"><span data-stu-id="f9dd6-112">Limit Type</span></span> | <span data-ttu-id="f9dd6-113">제한 값</span><span class="sxs-lookup"><span data-stu-id="f9dd6-113">Limit Value</span></span> | <span data-ttu-id="f9dd6-114">API 사용</span><span class="sxs-lookup"><span data-stu-id="f9dd6-114">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="f9dd6-115">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="f9dd6-115">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="f9dd6-116">IP</span><span class="sxs-lookup"><span data-stu-id="f9dd6-116">IP</span></span> | <span data-ttu-id="f9dd6-117">1000 / 분</span><span class="sxs-lookup"><span data-stu-id="f9dd6-117">1000 / minute</span></span> | <span data-ttu-id="f9dd6-118">OData v 1 통해 NuGet 패키지 메타 데이터를 쿼리 `Packages` 컬렉션</span><span class="sxs-lookup"><span data-stu-id="f9dd6-118">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="f9dd6-119">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="f9dd6-119">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="f9dd6-120">IP</span><span class="sxs-lookup"><span data-stu-id="f9dd6-120">IP</span></span> | <span data-ttu-id="f9dd6-121">3000 / 분</span><span class="sxs-lookup"><span data-stu-id="f9dd6-121">3000 / minute</span></span> | <span data-ttu-id="f9dd6-122">V1 검색 끝점을 통해 NuGet 패키지에 대 한 검색</span><span class="sxs-lookup"><span data-stu-id="f9dd6-122">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="f9dd6-123">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="f9dd6-123">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="f9dd6-124">IP</span><span class="sxs-lookup"><span data-stu-id="f9dd6-124">IP</span></span> | <span data-ttu-id="f9dd6-125">20000 / 분</span><span class="sxs-lookup"><span data-stu-id="f9dd6-125">20000 / minute</span></span> | <span data-ttu-id="f9dd6-126">OData v 2 통해 NuGet 패키지 메타 데이터 쿼리 `Packages` 컬렉션</span><span class="sxs-lookup"><span data-stu-id="f9dd6-126">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="f9dd6-127">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="f9dd6-127">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="f9dd6-128">IP</span><span class="sxs-lookup"><span data-stu-id="f9dd6-128">IP</span></span> | <span data-ttu-id="f9dd6-129">100 / 분</span><span class="sxs-lookup"><span data-stu-id="f9dd6-129">100 / minute</span></span> | <span data-ttu-id="f9dd6-130">NuGet 패키지 개수 v2 OData 통해 쿼리 `Packages` 컬렉션</span><span class="sxs-lookup"><span data-stu-id="f9dd6-130">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="f9dd6-131">패키지 푸시하고 Unlist</span><span class="sxs-lookup"><span data-stu-id="f9dd6-131">Package Push and Unlist</span></span>

| <span data-ttu-id="f9dd6-132">API</span><span class="sxs-lookup"><span data-stu-id="f9dd6-132">API</span></span> | <span data-ttu-id="f9dd6-133">제한 유형</span><span class="sxs-lookup"><span data-stu-id="f9dd6-133">Limit Type</span></span> | <span data-ttu-id="f9dd6-134">제한 값</span><span class="sxs-lookup"><span data-stu-id="f9dd6-134">Limit Value</span></span> | <span data-ttu-id="f9dd6-135">동력 사용</span><span class="sxs-lookup"><span data-stu-id="f9dd6-135">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="f9dd6-136">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="f9dd6-136">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="f9dd6-137">API 키</span><span class="sxs-lookup"><span data-stu-id="f9dd6-137">API Key</span></span> | <span data-ttu-id="f9dd6-138">100 / 분</span><span class="sxs-lookup"><span data-stu-id="f9dd6-138">100 / minute</span></span> | <span data-ttu-id="f9dd6-139">V2 푸시 끝점을 통해 새 NuGet 패키지 (버전)를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="f9dd6-139">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="f9dd6-140">**DELETE** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="f9dd6-140">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="f9dd6-141">API 키</span><span class="sxs-lookup"><span data-stu-id="f9dd6-141">API Key</span></span> | <span data-ttu-id="f9dd6-142">100 / 분</span><span class="sxs-lookup"><span data-stu-id="f9dd6-142">100 / minute</span></span> | <span data-ttu-id="f9dd6-143">Unlist v2 끝점을 통해 NuGet 패키지 (버전)</span><span class="sxs-lookup"><span data-stu-id="f9dd6-143">Unlist a NuGet package (version) via v2 endpoint</span></span> 
