---
title: "nuget.org에 게시된 모든 패키지에 대한 쿼리 | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 11/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "NuGet API를 사용하면 nuget.org에 게시된 모든 패키지에 대해 쿼리하고 시간이 지남에 따라 최신 상태를 유지할 수 있습니다."
keywords: "NuGet API는 모든 패키지를 열거하고, NuGet API는 패키지, 즉 nuget.org에 게시된 최신 패키지를 복제합니다."
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: ce25680f3b591e9c6b0234b6ac30b82205d10ad3
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2018
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="d0cdb-104">nuget.org에 게시된 모든 패키지에 대한 쿼리</span><span class="sxs-lookup"><span data-stu-id="d0cdb-104">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="d0cdb-105">레거시 OData V2 API의 일반적인 쿼리 패턴 중 하나는 패키지를 게시할 때 nuget.org에 게시된 모든 패키지를 지정한 정렬 순서대로 열거한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-105">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="d0cdb-106">nuget.org에 대해 이러한 종류의 쿼리가 필요한 시나리오는 다음과 같이 매우 다양합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-106">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="d0cdb-107">nuget.org 전체 복제</span><span class="sxs-lookup"><span data-stu-id="d0cdb-107">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="d0cdb-108">패키지의 새 버전이 출시된 경우에 대한 검색</span><span class="sxs-lookup"><span data-stu-id="d0cdb-108">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="d0cdb-109">패키지에 종속된 패키지 찾기</span><span class="sxs-lookup"><span data-stu-id="d0cdb-109">Finding packages that depend on your package</span></span>

<span data-ttu-id="d0cdb-110">이를 수행하는 레거시 방식에서는 일반적으로 `skip` 및 `top`(페이지 크기) 매개 변수를 사용하여 대규모 결과 집합 전체에서 OData 패키지 엔터티를 타임스탬프 및 페이징 기준으로 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-110">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="d0cdb-111">그러나 이 방식에는 몇 가지 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-111">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="d0cdb-112">순서가 자주 변경되는 데이터에 대한 쿼리로 인한 패키지 누락 가능성</span><span class="sxs-lookup"><span data-stu-id="d0cdb-112">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="d0cdb-113">최적화되지 않은 쿼리로 인한 느린 쿼리 응답 시간(가장 효율적으로 최적화된 쿼리는 공식 NuGet 클라이언트에 대한 주요 시나리오를 지원하는 쿼리임)</span><span class="sxs-lookup"><span data-stu-id="d0cdb-113">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="d0cdb-114">사용되지 않고 문서화되지 않은 API 사용(나중에는 이러한 쿼리에 대한 지원이 보장되지 않음)</span><span class="sxs-lookup"><span data-stu-id="d0cdb-114">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="d0cdb-115">발생된 정확한 순서대로 재생할 수 없는 기록</span><span class="sxs-lookup"><span data-stu-id="d0cdb-115">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="d0cdb-116">이러한 이유로 앞에서 언급한 시나리오를 더 안정적이고 미래를 보증할 수 있는 방식으로 해결하기 위해 다음 지침을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-116">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="d0cdb-117">개요</span><span class="sxs-lookup"><span data-stu-id="d0cdb-117">Overview</span></span>

<span data-ttu-id="d0cdb-118">이 지침의 중심에는 **카탈로그**라는 [NuGet API](../../api/overview.md)의 리소스가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-118">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="d0cdb-119">카탈로그는 호출자가 nuget.org에서 추가, 수정 및 삭제된 패키지에 대한 전체 기록을 볼 수 있게 하는 추가 전용 API입니다. nuget.org에 게시된 패키지의 전체 또는 일부에 관심이 있는 경우 카탈로그는 시간이 지남에 따라 현재 사용 가능한 패키지의 집합을 최신 상태로 유지할 수 있는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-119">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="d0cdb-120">이 지침은 상위 수준 연습을 위한 것이지만, 카탈로그에 대해 매우 자세한 정보에 관심이 있는 경우 [API 참조 문서](../../api/catalog-resource.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-120">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="d0cdb-121">다음에 나오는 단계는 원하는 프로그래밍 언어로 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-121">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="d0cdb-122">전체 실행 샘플을 원하는 경우 아래에서 설명하는 [C# 샘플](#c-sample-code)을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-122">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="d0cdb-123">그렇지 않으면 아래 지침에 따라 신뢰할 수 있는 카탈로그 판독기를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-123">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="d0cdb-124">커서 초기화</span><span class="sxs-lookup"><span data-stu-id="d0cdb-124">Initialize a cursor</span></span>

<span data-ttu-id="d0cdb-125">신뢰할 수 있는 카탈로그 판독기를 작성하는 첫 번째 단계는 커서를 구현하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-125">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="d0cdb-126">카탈로그 커서의 디자인에 대한 자세한 내용은 [카탈로그 참조 문서](../../api/catalog-resource.md#cursor)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-126">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="d0cdb-127">간단히 말해, 커서는 카탈로그에서 이벤트를 처리한 시점입니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-127">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="d0cdb-128">카탈로그의 이벤트는 패키지 게시 및 기타 패키지 변경을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-128">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="d0cdb-129">시작된 이후 NuGet에 게시된 모든 패키지에 대해 관심이 있으면 커서를 "최소값" 타임스탬프(예: .NET의 `DateTime.MinValue`)로 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-129">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="d0cdb-130">지금 시작하여 게시된 패키지에 대해서만 관심이 있으면 현재 타임스탬프를 초기 커서 값으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-130">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="d0cdb-131">이 지침에서는 커서를 한 시간 전의 타임스탬프로 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-131">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="d0cdb-132">지금은 단지 해당 타임스탬프를 메모리에 저장하기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-132">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="d0cdb-133">카탈로그 인덱스 URL 확인</span><span class="sxs-lookup"><span data-stu-id="d0cdb-133">Determine catalog index URL</span></span>

<span data-ttu-id="d0cdb-134">NuGet API의 모든 리소스(엔드포인트)에 대한 위치는 [서비스 인덱스](../../api/service-index.md)를 사용하여 검색해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-134">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="d0cdb-135">이 지침은 nuget.org에 초점을 맞추고 있으므로 nuget.org의 서비스 인덱스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-135">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

    GET https://api.nuget.org/v3/index.json

<span data-ttu-id="d0cdb-136">서비스 문서는 nuget.org의 모든 리소스가 포함된 JSON 문서입니다. `@type` 속성 값이 `Catalog/3.0.0`인 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-136">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="d0cdb-137">연결된 `@id` 속성 값은 카탈로그 인덱스 자체에 대한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-137">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="d0cdb-138">새 카탈로그 리프 찾기</span><span class="sxs-lookup"><span data-stu-id="d0cdb-138">Find new catalog leaves</span></span>

<span data-ttu-id="d0cdb-139">이전 단계에서 찾은 `@id` 속성 값을 사용하여 카탈로그 인덱스를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-139">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

    GET https://api.nuget.org/v3/catalog0/index.json

<span data-ttu-id="d0cdb-140">[카탈로그 인덱스](../../api/catalog-resource.md#catalog-index)를 역직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-140">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="d0cdb-141">현재 커서 값보다 작거나 같은 `commitTimeStamp`을 사용하여 [카탈로그 페이지 개체](../../api/catalog-resource.md#catalog-page-object-in-the-index)를 모두 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-141">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="d0cdb-142">나머지 카탈로그 페이지마다 `@id` 속성을 사용하여 전체 문서를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-142">For each remaining catalog page, download the full document using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/page2926.json

<span data-ttu-id="d0cdb-143">[카탈로그 페이지](../../api/catalog-resource.md#catalog-page)를 역직렬화합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-143">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="d0cdb-144">현재 커서 값보다 작거나 같은 `commitTimeStamp`로 모든 [카탈로그 리프 개체](../../api/catalog-resource.md#catalog-item-object-in-a-page)를 필터링합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-144">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="d0cdb-145">필터링되지 않은 카탈로그 페이지를 모두 다운로드하면 커서 타임스탬프와 현재 시간 사이에 게시, 나열되지 않음, 나열 또는 삭제된 패키지를 나타내는 카탈로그 리프 개체 집합을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-145">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="d0cdb-146">프로세스 카탈로그 리프</span><span class="sxs-lookup"><span data-stu-id="d0cdb-146">Process catalog leaves</span></span>

<span data-ttu-id="d0cdb-147">이 시점에서 카탈로그 항목에 대해 원하는 모든 사용자 지정 처리를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-147">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="d0cdb-148">패키지의 ID와 버전이 모두 필요한 경우 페이지에 있는 카탈로그 항목 개체에서 `nuget:id` 및 `nuget:version` 속성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-148">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="d0cdb-149">`@type` 속성을 살펴보고 카탈로그 항목이 기존 패키지 또는 삭제된 패키지와 관련이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-149">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="d0cdb-150">패키지에 대한 메타데이터(예: 설명, 종속성, .nupkg 크기 등)에 관심이 있으면 `@id` 속성을 사용하여 [카탈로그 리프 문서](../../api/catalog-resource.md#catalog-leaf)를 페치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-150">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

<span data-ttu-id="d0cdb-151">이 문서에는 [패키지 메타데이터 리소스](../../api/registration-base-url-resource.md) 등에 포함된 모든 메타데이터가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-151">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="d0cdb-152">이 단계에서는 사용자 지정 논리를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-152">This step is where you implement your custom logic.</span></span> <span data-ttu-id="d0cdb-153">이 지침의 다른 단계에서는 카탈로그 리프를 사용하여 수행하는 작업과 관계없이 거의 동일한 방식으로 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-153">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="d0cdb-154">.nupkg 다운로드</span><span class="sxs-lookup"><span data-stu-id="d0cdb-154">Downloading the .nupkg</span></span>

<span data-ttu-id="d0cdb-155">카탈로그에 있는 패키지에 대한 .nupkg를 다운로드하려면 [패키지 콘텐츠 리소스](../../api/package-base-address-resource.md)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-155">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="d0cdb-156">그러나 카탈로그에서 패키지를 찾은 후 패키지 콘텐츠 리소스에서 패키지를 사용할 수 있을 때까지 약간의 지연이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-156">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="d0cdb-157">따라서 카탈로그에 있는 패키지에 대한 .nupkg를 다운로드하려고 할 때 `404 Not Found`가 발생하면 잠시 후에 다시 시도하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-157">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="d0cdb-158">[NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455) GitHub 문제에서 이 지연에 대한 수정을 추적하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-158">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="d0cdb-159">커서를 앞으로 이동</span><span class="sxs-lookup"><span data-stu-id="d0cdb-159">Move the cursor forward</span></span>

<span data-ttu-id="d0cdb-160">카탈로그 항목을 성공적으로 처리했으면 저장할 새 커서 값을 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-160">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="d0cdb-161">이렇게 하려면 처리한 모든 카탈로그 항목 중 최대(최신 시간순) `commitTimeStamp`을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-161">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="d0cdb-162">이 항목이 새 커서 값이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-162">This is your new cursor value.</span></span> <span data-ttu-id="d0cdb-163">데이터베이스, 파일 시스템 또는 Blob 저장소와 같은 일부 영구 저장소에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-163">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="d0cdb-164">더 많은 카탈로그 항목을 가져오려면 이 영구 저장소에서 커서 값을 초기화하여 [첫 번째 단계](#initialize-a-cursor)부터 시작하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-164">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="d0cdb-165">응용 프로그램에서 예외 또는 오류를 throw하는 경우 커서를 앞으로 이동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-165">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="d0cdb-166">커서를 앞으로 이동하는 것은 커서 이전의 카탈로그 항목을 다시 처리할 필요가 없다는 의미입니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-166">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="d0cdb-167">어떤 이유로 카탈로그 리프를 처리하는 방법에 버그가 있는 경우 단순히 커서를 해당 시점에서 뒤로 이동하여 코드에서 이전 카탈로그 항목을 다시 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-167">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="d0cdb-168">C# 샘플 코드</span><span class="sxs-lookup"><span data-stu-id="d0cdb-168">C# sample code</span></span>

<span data-ttu-id="d0cdb-169">카탈로그는 HTTP를 통해 사용할 수 있는 JSON 문서의 집합이므로, HTTP 클라이언트 및 JSON 역직렬 변환기가 있는 프로그래밍 언어를 사용하여 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-169">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="d0cdb-170">C# 샘플은 [NuGet/샘플 리포지토리](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-170">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="d0cdb-171">카탈로그 SDK</span><span class="sxs-lookup"><span data-stu-id="d0cdb-171">Catalog SDK</span></span>

<span data-ttu-id="d0cdb-172">카탈로그를 사용하는 가장 쉬운 방법은 [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog) 시험판 .NET 카탈로그 SDK 패키지를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-172">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span></span> <span data-ttu-id="d0cdb-173">이 패키지는`https://dotnet.myget.org/F/nuget-build/api/v3/index.json` NuGet 패키지 원본 URL을 사용하는 `nuget-build` MyGet 피드에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-173">This package is available on the `nuget-build` MyGet feed, for which you use the NuGet package source URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span></span>

<span data-ttu-id="d0cdb-174">이 패키지는 `netstandard1.3` 이상과 호환되는 프로젝트(예: .NET Framework 4.6)에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-174">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="d0cdb-175">이 패키지를 사용하는 샘플은 GitHub의 [NuGet.Protocol.Catalog.Sample 프로젝트](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-175">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="d0cdb-176">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="d0cdb-176">Sample output</span></span>

```output
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a><span data-ttu-id="d0cdb-177">최소 샘플</span><span class="sxs-lookup"><span data-stu-id="d0cdb-177">Minimal sample</span></span>

<span data-ttu-id="d0cdb-178">카탈로그와의 상호 작용을 더 자세히 보여 주는 종속성이 적은 예제는 [CatalogReaderExample 샘플 프로젝트](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-178">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="d0cdb-179">프로젝트는 `netcoreapp2.0`을 대상으로 하며, [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0)(서비스 인덱스 확인용) 및 [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1)(JSON 역직렬화용)에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-179">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="d0cdb-180">코드의 주요 논리는 [Program.cs 파일](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs)에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d0cdb-180">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="d0cdb-181">샘플 출력</span><span class="sxs-lookup"><span data-stu-id="d0cdb-181">Sample output</span></span>

```output
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
