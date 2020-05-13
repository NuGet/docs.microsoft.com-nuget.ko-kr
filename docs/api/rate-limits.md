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
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367936"
---
# <a name="rate-limits"></a><span data-ttu-id="df60f-103">속도 제한</span><span class="sxs-lookup"><span data-stu-id="df60f-103">Rate Limits</span></span>

<span data-ttu-id="df60f-104">NuGet.org API는 악용을 방지 하기 위해 요금 제한을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="df60f-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="df60f-105">Rate 제한을 초과 하는 요청은 다음 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="df60f-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="df60f-106">요금 제한을 사용 하 여 요청을 제한 하는 것 외에도 일부 Api는 할당량을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="df60f-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="df60f-107">할당량을 초과 하는 요청은 다음 오류를 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="df60f-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="df60f-108">다음 표에서는 NuGet.org API에 대 한 요율 제한을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="df60f-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="df60f-109">패키지 검색</span><span class="sxs-lookup"><span data-stu-id="df60f-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="df60f-110">현재는 전송률이 제한 되지 않으므로 Nuget.exe의 [V3 검색 api](search-query-service-resource.md) 를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="df60f-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="df60f-111">V1 및 V2 검색 Api의 경우 다음과 같은 제한이 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="df60f-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="df60f-112">API</span><span class="sxs-lookup"><span data-stu-id="df60f-112">API</span></span> | <span data-ttu-id="df60f-113">제한 유형</span><span class="sxs-lookup"><span data-stu-id="df60f-113">Limit Type</span></span> | <span data-ttu-id="df60f-114">제한 값</span><span class="sxs-lookup"><span data-stu-id="df60f-114">Limit Value</span></span> | <span data-ttu-id="df60f-115">API 사용 사례</span><span class="sxs-lookup"><span data-stu-id="df60f-115">API Use Case</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="df60f-116">**GET**`/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="df60f-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="df60f-117">IP</span><span class="sxs-lookup"><span data-stu-id="df60f-117">IP</span></span> | <span data-ttu-id="df60f-118">1000/분</span><span class="sxs-lookup"><span data-stu-id="df60f-118">1000 / minute</span></span> | <span data-ttu-id="df60f-119">V1 OData 컬렉션을 통해 NuGet 패키지 메타 데이터 쿼리 `Packages`</span><span class="sxs-lookup"><span data-stu-id="df60f-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="df60f-120">**GET**`/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="df60f-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="df60f-121">IP</span><span class="sxs-lookup"><span data-stu-id="df60f-121">IP</span></span> | <span data-ttu-id="df60f-122">3000/분</span><span class="sxs-lookup"><span data-stu-id="df60f-122">3000 / minute</span></span> | <span data-ttu-id="df60f-123">V1 검색 끝점을 통해 NuGet 패키지 검색</span><span class="sxs-lookup"><span data-stu-id="df60f-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="df60f-124">**GET**`/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="df60f-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="df60f-125">IP</span><span class="sxs-lookup"><span data-stu-id="df60f-125">IP</span></span> | <span data-ttu-id="df60f-126">2만/분</span><span class="sxs-lookup"><span data-stu-id="df60f-126">20000 / minute</span></span> | <span data-ttu-id="df60f-127">V2 OData 컬렉션을 통해 NuGet 패키지 메타 데이터 쿼리 `Packages`</span><span class="sxs-lookup"><span data-stu-id="df60f-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="df60f-128">**GET**`/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="df60f-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="df60f-129">IP</span><span class="sxs-lookup"><span data-stu-id="df60f-129">IP</span></span> | <span data-ttu-id="df60f-130">100/분</span><span class="sxs-lookup"><span data-stu-id="df60f-130">100 / minute</span></span> | <span data-ttu-id="df60f-131">V2 OData 컬렉션을 통해 NuGet 패키지 수 쿼리 `Packages`</span><span class="sxs-lookup"><span data-stu-id="df60f-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="df60f-132">패키지 푸시 및 목록 제거</span><span class="sxs-lookup"><span data-stu-id="df60f-132">Package Push and Unlist</span></span>

| <span data-ttu-id="df60f-133">API</span><span class="sxs-lookup"><span data-stu-id="df60f-133">API</span></span> | <span data-ttu-id="df60f-134">제한 유형</span><span class="sxs-lookup"><span data-stu-id="df60f-134">Limit Type</span></span> | <span data-ttu-id="df60f-135">제한 값</span><span class="sxs-lookup"><span data-stu-id="df60f-135">Limit Value</span></span> | <span data-ttu-id="df60f-136">API 사용 사례</span><span class="sxs-lookup"><span data-stu-id="df60f-136">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="df60f-137">**PUT**`/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="df60f-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="df60f-138">API 키</span><span class="sxs-lookup"><span data-stu-id="df60f-138">API Key</span></span> | <span data-ttu-id="df60f-139">350/시간</span><span class="sxs-lookup"><span data-stu-id="df60f-139">350 / hour</span></span> | <span data-ttu-id="df60f-140">V2 푸시 끝점을 통해 새 NuGet 패키지 (버전) 업로드</span><span class="sxs-lookup"><span data-stu-id="df60f-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="df60f-141">**삭제**`/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="df60f-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="df60f-142">API 키</span><span class="sxs-lookup"><span data-stu-id="df60f-142">API Key</span></span> | <span data-ttu-id="df60f-143">250/시간</span><span class="sxs-lookup"><span data-stu-id="df60f-143">250 / hour</span></span> | <span data-ttu-id="df60f-144">V2 끝점을 통해 NuGet 패키지 (버전) 나열 제거</span><span class="sxs-lookup"><span data-stu-id="df60f-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 

## <a name="nugetorg-website-page-views"></a><span data-ttu-id="df60f-145">nuget.org 웹 사이트 페이지 보기</span><span class="sxs-lookup"><span data-stu-id="df60f-145">nuget.org website page views</span></span>

<span data-ttu-id="df60f-146">Nuget.org 웹 페이지에 프로그래밍 방식으로 액세스 하는 경우 문서화 된 [V3 api](overview.md)를 조사 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="df60f-146">If you are accessing the nuget.org web pages programmatically, consider investigating our documented [V3 APIs](overview.md).</span></span> <span data-ttu-id="df60f-147">이러한 끝점을 사용 하면 패키지 메타 데이터 및 콘텐츠에 더 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df60f-147">These endpoints allow for simpler access to package metadata and content.</span></span> <span data-ttu-id="df60f-148">V3 API는 더 나은 가용성을 제공 하며, 웹 브라우저 상호 작용을 위해 설계 된 NuGet 갤러리 웹 페이지에 액세스 하는 것 보다 더 높은 성능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="df60f-148">The V3 API has better availability and has higher performance than accessing the NuGet Gallery web pages, which are designed for web browser interaction.</span></span>

| <span data-ttu-id="df60f-149">API</span><span class="sxs-lookup"><span data-stu-id="df60f-149">API</span></span> | <span data-ttu-id="df60f-150">제한 유형</span><span class="sxs-lookup"><span data-stu-id="df60f-150">Limit Type</span></span> | <span data-ttu-id="df60f-151">제한 값</span><span class="sxs-lookup"><span data-stu-id="df60f-151">Limit Value</span></span> | <span data-ttu-id="df60f-152">API 사용 사례</span><span class="sxs-lookup"><span data-stu-id="df60f-152">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="df60f-153">**GET**`/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="df60f-153">**GET** `/package/{id}/{version}`</span></span> | <span data-ttu-id="df60f-154">IP</span><span class="sxs-lookup"><span data-stu-id="df60f-154">IP</span></span> | <span data-ttu-id="df60f-155">50/분</span><span class="sxs-lookup"><span data-stu-id="df60f-155">50 / minute</span></span> | <span data-ttu-id="df60f-156">패키지 (버전) 세부 정보 페이지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="df60f-156">Display package (version) details page.</span></span> 
