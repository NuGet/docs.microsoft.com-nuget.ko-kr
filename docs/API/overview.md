---
title: 개요, NuGet API | Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet API는 패키지를 다운로드, 메타 데이터 인출, 새로운 패키지 등 게시를 사용할 수 있는 HTTP 끝점의 집합입니다.
keywords: NuGet V3 API, NuGet V2 API, NuGet JSON, NuGet 등록 API를 NuGet API 플랫 컨테이너, NuGet nupkg API, NuGet 메타 데이터 API, NuGet 검색 API, NuGet 푸시 API NuGe API를 게시, NuGet API를 삭제, NuGet unlist API, NuGet 프로토콜
ms.reviewer:
- karann
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 7053a971c80a94cf035e8f149c332b36e66a9ea9
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-api"></a><span data-ttu-id="62562-104">NuGet API</span><span class="sxs-lookup"><span data-stu-id="62562-104">NuGet API</span></span>

<span data-ttu-id="62562-105">NuGet API는 패키지를 다운로드, 메타 데이터 인출, 새로운 패키지를 게시 및 공식 NuGet 클라이언트에서 사용할 수 있는 다른 대부분 작업을 수행 하는 데 사용할 수 있는 HTTP 끝점의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="62562-105">The NuGet API is a set of HTTP endpoints that can be used to download packages, fetch metadata, publish new packages, and perform most other operations available in the official NuGet clients.</span></span>

<span data-ttu-id="62562-106">이 API는 데 Visual Studio, nuget.exe,.NET CLI에는 NuGet 클라이언트와 같은 NuGet 작업을 수행 [ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore), Visual Studio UI에서 검색 하 고 [ `nuget.exe push` ](../tools/cli-ref-push.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-106">This API is used by the NuGet client in Visual Studio, nuget.exe, and the .NET CLI to perform NuGet operations such as [`dotnet restore`](/dotnet/articles/core/preview3/tools/dotnet-restore), search in the Visual Studio UI, and [`nuget.exe push`](../tools/cli-ref-push.md).</span></span>

<span data-ttu-id="62562-107">Nuget.org의 다른 패키지 소스에 적용 되지 않은 다른 요구 사항이 있을 경우에 따라 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-107">Note in some cases, nuget.org has additional requirements that are not enforced by other package sources.</span></span> <span data-ttu-id="62562-108">이러한 차이 단계의 유형별로 설명 되어는 [nuget.org 프로토콜](nuget-protocols.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-108">These differences are documented by the [nuget.org Protocols](nuget-protocols.md).</span></span>

## <a name="service-index"></a><span data-ttu-id="62562-109">서비스 인덱스</span><span class="sxs-lookup"><span data-stu-id="62562-109">Service index</span></span>

<span data-ttu-id="62562-110">API에 대 한 진입점에는 잘 알려진 위치에 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="62562-110">The entry point for the API is a JSON document in a well known location.</span></span> <span data-ttu-id="62562-111">이 문서는 라고는 **서비스 인덱스**합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-111">This document is called the **service index**.</span></span> <span data-ttu-id="62562-112">Nuget.org에 대 한 서비스 인덱스의 위치는 `https://api.nuget.org/v3/index.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-112">The location of the service index for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

<span data-ttu-id="62562-113">이 JSON 문서 목록이 포함 되어 *리소스* 다른 기능을 제공 하 고 다른 사용 사례를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-113">This JSON document contains a list of *resources* which provide different functionality and fulfill different use cases.</span></span>

<span data-ttu-id="62562-114">API를 지 원하는 클라이언트는 해당 패키지 소스에 연결 하는 수단으로 이러한 서비스 인덱스 URL 중 하나 이상을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-114">Clients that support the API should accept one or more of these service index URL as the means of connecting to the respective package sources.</span></span>

<span data-ttu-id="62562-115">서비스 인덱스에 대 한 자세한 내용은 참조 [해당 API 참조](service-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-115">For more information about the service index, see [its API reference](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="62562-116">버전 관리</span><span class="sxs-lookup"><span data-stu-id="62562-116">Versioning</span></span>

<span data-ttu-id="62562-117">API에는 NuGet의 HTTP 프로토콜의 버전 3입니다.</span><span class="sxs-lookup"><span data-stu-id="62562-117">The API is version 3 of NuGet's HTTP protocol.</span></span> <span data-ttu-id="62562-118">이 프로토콜 때때로 이라고 "V3 API입니다."</span><span class="sxs-lookup"><span data-stu-id="62562-118">This protocol is sometimes referred to as "the V3 API."</span></span> <span data-ttu-id="62562-119">이러한 참조 문서에서는 "API입니다." 처럼 간단 하 게이 버전의 프로토콜을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="62562-119">These reference documents will refer to this version of the protocol simply as "the API."</span></span>

<span data-ttu-id="62562-120">서비스 인덱스 스키마 버전으로 표시 됩니다는 `version` 서비스 인덱스에서 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="62562-120">The service index schema version is indicated by the `version` property in the service index.</span></span> <span data-ttu-id="62562-121">API 버전 문자열의 주 버전 번호에 보내도록 규정 `3`합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-121">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="62562-122">서비스 인덱스 스키마에 사소한 변경, 버전 문자열의 부 버전을 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62562-122">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="62562-123">이전 버전의 클라이언트 (nuget.exe 같은 2.x) V3 API를 지원 하지 않으며 여기에 문서화 되지 않은 이전 V2 API를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-123">Older clients (such as nuget.exe 2.x) do not support the V3 API and only support the older V2 API, which is not documented here.</span></span>

<span data-ttu-id="62562-124">NuGet V3 API V2 API의 후속 작업을 설정 하는 공식 NuGet 클라이언트 2.x 버전에서 구현 하는 OData 기반 프로토콜을 임이 있기 때문에 따라서 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-124">The NuGet V3 API is named as such because it's the successor of the V2 API, which was the OData-based protocol implemented by the 2.x version of the official NuGet client.</span></span> <span data-ttu-id="62562-125">V3 API 공식 NuGet 클라이언트 버전 3.0에서 처음 지원 되었습니다 및 여전히 주요 프로토콜 최신 버전에서 지원 됩니다 4.0 NuGet 클라이언트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62562-125">The V3 API was first supported by the 3.0 version of the official NuGet client and is still the latest major protocol version supported by the NuGet client, 4.0 and on.</span></span> 

<span data-ttu-id="62562-126">주요 변경 아님 프로토콜 변경이 이루어진 API에 첫 번째 릴리스 이후입니다.</span><span class="sxs-lookup"><span data-stu-id="62562-126">Non-breaking protocol changes have been made to the API since it was first release.</span></span>

## <a name="resources-and-schema"></a><span data-ttu-id="62562-127">리소스 및 스키마</span><span class="sxs-lookup"><span data-stu-id="62562-127">Resources and schema</span></span>

<span data-ttu-id="62562-128">**서비스 인덱스** 다양 한 리소스에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-128">The **service index** describes a variety of resources.</span></span> <span data-ttu-id="62562-129">지원 되는 리소스의 현재 집합은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="62562-129">The current set of supported resources are as follows:</span></span>

<span data-ttu-id="62562-130">리소스 이름</span><span class="sxs-lookup"><span data-stu-id="62562-130">Resource name</span></span>                                                          | <span data-ttu-id="62562-131">필수</span><span class="sxs-lookup"><span data-stu-id="62562-131">Required</span></span> | <span data-ttu-id="62562-132">설명</span><span class="sxs-lookup"><span data-stu-id="62562-132">Description</span></span>
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | <span data-ttu-id="62562-133">예</span><span class="sxs-lookup"><span data-stu-id="62562-133">yes</span></span>      | <span data-ttu-id="62562-134">푸시 및 삭제 (또는 unlist) 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-134">Push and delete (or unlist) packages.</span></span>
[`SearchQueryService`](search-query-service-resource.md)               | <span data-ttu-id="62562-135">예</span><span class="sxs-lookup"><span data-stu-id="62562-135">yes</span></span>      | <span data-ttu-id="62562-136">필터 및 키워드로 패키지에 대 한 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-136">Filter and search for packages by keyword.</span></span>
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | <span data-ttu-id="62562-137">예</span><span class="sxs-lookup"><span data-stu-id="62562-137">yes</span></span>      | <span data-ttu-id="62562-138">패키지 메타 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="62562-138">Get package metadata.</span></span>
[`PackageBaseAddress`](package-base-address-resource.md)               | <span data-ttu-id="62562-139">예</span><span class="sxs-lookup"><span data-stu-id="62562-139">yes</span></span>      | <span data-ttu-id="62562-140">패키지 콘텐츠를 (.nupkg)를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="62562-140">Get package content (.nupkg).</span></span>
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | <span data-ttu-id="62562-141">아니요</span><span class="sxs-lookup"><span data-stu-id="62562-141">no</span></span>       | <span data-ttu-id="62562-142">부분 문자열이 패키지 Id 및 버전을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-142">Discover package IDs and versions by substring.</span></span>
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | <span data-ttu-id="62562-143">아니요</span><span class="sxs-lookup"><span data-stu-id="62562-143">no</span></span>       | <span data-ttu-id="62562-144">"신고" 웹 페이지에 액세스 하는 URL을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-144">Construct a URL to access a "report abuse" web page.</span></span>
[`Catalog`](catalog-resource.md)                                       | <span data-ttu-id="62562-145">아니요</span><span class="sxs-lookup"><span data-stu-id="62562-145">no</span></span>       | <span data-ttu-id="62562-146">모든 패키지 이벤트의 전체 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="62562-146">Full record of all package events.</span></span>

<span data-ttu-id="62562-147">일반적으로 API 리소스에 의해 반환 되는 모든 이진이 아닌 데이터는 JSON을 사용 하 여 serialize 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62562-147">In general, all non-binary data returned by a API resource are serialized using JSON.</span></span> <span data-ttu-id="62562-148">서비스 인덱스의 각 리소스에서 반환 된 응답 스키마는 해당 리소스에 대해 개별적으로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="62562-148">The response schema returned by each resource in the service index is defined individually for that resource.</span></span> <span data-ttu-id="62562-149">각 리소스에 대 한 자세한 내용은 위에 나열 된 항목을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="62562-149">For more information about each resource, see the topics listed above.</span></span>

> [!Note]
> <span data-ttu-id="62562-150">원본 구현 하지 않는 `SearchAutocompleteService` 모든 자동 완성 동작을 적절 하 게 해제 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-150">When a source does not implement `SearchAutocompleteService` any autocomplete behavior should be disabled gracefully.</span></span> <span data-ttu-id="62562-151">때 `ReportAbuseUriTemplate` 구현 되지 않은 nuget.org의로 공식 NuGet 클라이언트 변경 보고서 남용 URL (에서 추적 [NuGet/홈 #4924](https://github.com/NuGet/Home/issues/4924)).</span><span class="sxs-lookup"><span data-stu-id="62562-151">When `ReportAbuseUriTemplate` is not implemented, the official NuGet client falls back to nuget.org's report abuse URL (tracked by [NuGet/Home#4924](https://github.com/NuGet/Home/issues/4924)).</span></span> <span data-ttu-id="62562-152">다른 클라이언트를 보고서 남용 URL을 사용자에 게 표시 되지 않도록에 간단히 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62562-152">Other clients may opt to simply not show a report abuse URL to the user.</span></span>

## <a name="timestamps"></a><span data-ttu-id="62562-153">타임스탬프</span><span class="sxs-lookup"><span data-stu-id="62562-153">Timestamps</span></span>

<span data-ttu-id="62562-154">API에서 반환 하는 모든 타임 스탬프는 UTC 또는 사용 하 여 별도로 지정 [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 표현 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-154">All timestamps returned by the API are UTC or are otherwise specified using [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) representation.</span></span> 

## <a name="http-methods"></a><span data-ttu-id="62562-155">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="62562-155">HTTP methods</span></span>

<span data-ttu-id="62562-156">동사</span><span class="sxs-lookup"><span data-stu-id="62562-156">Verb</span></span>   | <span data-ttu-id="62562-157">사용</span><span class="sxs-lookup"><span data-stu-id="62562-157">Use</span></span>
------ | -----------
<span data-ttu-id="62562-158">가져오기</span><span class="sxs-lookup"><span data-stu-id="62562-158">GET</span></span>    | <span data-ttu-id="62562-159">일반적으로 데이터를 검색 하는 읽기 전용 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-159">Performs a read-only operation, typically retrieving data.</span></span>
<span data-ttu-id="62562-160">HEAD</span><span class="sxs-lookup"><span data-stu-id="62562-160">HEAD</span></span>   | <span data-ttu-id="62562-161">응답 헤더에는 해당 인출 `GET` 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-161">Fetches the response headers for the corresponding `GET` request.</span></span>
<span data-ttu-id="62562-162">PUT</span><span class="sxs-lookup"><span data-stu-id="62562-162">PUT</span></span>    | <span data-ttu-id="62562-163">존재 하지 않거나 파일이 존재 하는 경우 업데이트 하는 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="62562-163">Creates a resource that doesn't exist or, if it does exist, updates it.</span></span> <span data-ttu-id="62562-164">일부 리소스는 업데이트를 지원 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62562-164">Some resources may not support update.</span></span>
<span data-ttu-id="62562-165">Delete</span><span class="sxs-lookup"><span data-stu-id="62562-165">DELETE</span></span> | <span data-ttu-id="62562-166">삭제 하거나 리소스 unlists 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-166">Deletes or unlists a resource.</span></span>

## <a name="http-status-codes"></a><span data-ttu-id="62562-167">HTTP 상태 코드</span><span class="sxs-lookup"><span data-stu-id="62562-167">HTTP status codes</span></span>

<span data-ttu-id="62562-168">코드</span><span class="sxs-lookup"><span data-stu-id="62562-168">Code</span></span> | <span data-ttu-id="62562-169">설명</span><span class="sxs-lookup"><span data-stu-id="62562-169">Description</span></span>
---- | -----
<span data-ttu-id="62562-170">200</span><span class="sxs-lookup"><span data-stu-id="62562-170">200</span></span>  | <span data-ttu-id="62562-171">성공할 경우 응답 본문은 및입니다.</span><span class="sxs-lookup"><span data-stu-id="62562-171">Success, and there is a response body.</span></span>
<span data-ttu-id="62562-172">201</span><span class="sxs-lookup"><span data-stu-id="62562-172">201</span></span>  | <span data-ttu-id="62562-173">성공 및 리소스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="62562-173">Success, and the resource was created.</span></span>
<span data-ttu-id="62562-174">202</span><span class="sxs-lookup"><span data-stu-id="62562-174">202</span></span>  | <span data-ttu-id="62562-175">성공, 요청이 승인 된 되지만 몇 가지 작업 수 불완전 한 시간 및 완료 된 비동기적으로.</span><span class="sxs-lookup"><span data-stu-id="62562-175">Success, the request has been accepted but some work may still be incomplete and completed asynchronously.</span></span>
<span data-ttu-id="62562-176">204</span><span class="sxs-lookup"><span data-stu-id="62562-176">204</span></span>  | <span data-ttu-id="62562-177">성공 하지만 응답 본문이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62562-177">Success, but there is no response body.</span></span>
<span data-ttu-id="62562-178">301</span><span class="sxs-lookup"><span data-stu-id="62562-178">301</span></span>  | <span data-ttu-id="62562-179">영구 리디렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="62562-179">A permanent redirect.</span></span>
<span data-ttu-id="62562-180">302</span><span class="sxs-lookup"><span data-stu-id="62562-180">302</span></span>  | <span data-ttu-id="62562-181">임시 리디렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="62562-181">A temporary redirect.</span></span>
<span data-ttu-id="62562-182">400</span><span class="sxs-lookup"><span data-stu-id="62562-182">400</span></span>  | <span data-ttu-id="62562-183">매개 변수는 URL에 또는 요청 본문에서 유효 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62562-183">The parameters in the URL or in the request body aren't valid.</span></span>
<span data-ttu-id="62562-184">401</span><span class="sxs-lookup"><span data-stu-id="62562-184">401</span></span>  | <span data-ttu-id="62562-185">제공 된 자격 증명이 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62562-185">The provided credentials are invalid.</span></span>
<span data-ttu-id="62562-186">403</span><span class="sxs-lookup"><span data-stu-id="62562-186">403</span></span>  | <span data-ttu-id="62562-187">작업이 제공 된 자격 증명이 제공 하는 것을 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62562-187">The action is not allowed given the provided credentials.</span></span>
<span data-ttu-id="62562-188">404</span><span class="sxs-lookup"><span data-stu-id="62562-188">404</span></span>  | <span data-ttu-id="62562-189">요청 된 리소스는 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62562-189">The requested resource doesn't exist.</span></span>
<span data-ttu-id="62562-190">409</span><span class="sxs-lookup"><span data-stu-id="62562-190">409</span></span>  | <span data-ttu-id="62562-191">기존 리소스와 함께 요청 충돌 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-191">The request conflicts with an existing resource.</span></span>
<span data-ttu-id="62562-192">500</span><span class="sxs-lookup"><span data-stu-id="62562-192">500</span></span>  | <span data-ttu-id="62562-193">서비스에 예기치 않은 오류가 발생 했습니다.</span><span class="sxs-lookup"><span data-stu-id="62562-193">The service has encountered an unexpected error.</span></span>
<span data-ttu-id="62562-194">503</span><span class="sxs-lookup"><span data-stu-id="62562-194">503</span></span>  | <span data-ttu-id="62562-195">서비스를 일시적으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="62562-195">The service is temporarily unavailable.</span></span>

<span data-ttu-id="62562-196">모든 `GET` API 끝점에 대 한 요청에 HTTP 리디렉션을 (301 또는 302) 반환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62562-196">Any `GET` request made to a API endpoint may return an HTTP redirect (301 or 302).</span></span> <span data-ttu-id="62562-197">관찰 하 여 클라이언트가 이러한 리디렉션을 적절히 처리 해야는 `Location` 헤더 및 후속 내림 `GET`합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-197">Clients should gracefully handle such redirects by observing the `Location` header and issueing a subsequent `GET`.</span></span> <span data-ttu-id="62562-198">특정 끝점에 관한 설명서 리디렉션을 사용할 수 있습니다. 아웃 명시적으로 호출 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="62562-198">Documentation concerning specific endpoints will not explicitly call out where redirects may be used.</span></span>

<span data-ttu-id="62562-199">500 수준 상태 코드의 경우 클라이언트는 적절 한 재시도 메커니즘을 구현 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62562-199">In the case of a 500-level status code, the client can implement a reasonable retry mechanism.</span></span> <span data-ttu-id="62562-200">공식 NuGet 클라이언트 다시 시도가 3 번 500 수준 상태 코드 또는 TCP/DNS 오류를 발견할 때.</span><span class="sxs-lookup"><span data-stu-id="62562-200">The official NuGet client retries three times when encountering any 500-level status code or TCP/DNS error.</span></span>

## <a name="http-request-headers"></a><span data-ttu-id="62562-201">HTTP 요청 헤더</span><span class="sxs-lookup"><span data-stu-id="62562-201">HTTP request headers</span></span>

<span data-ttu-id="62562-202">이름</span><span class="sxs-lookup"><span data-stu-id="62562-202">Name</span></span>                     | <span data-ttu-id="62562-203">설명</span><span class="sxs-lookup"><span data-stu-id="62562-203">Description</span></span>
------------------------ | -----------
<span data-ttu-id="62562-204">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="62562-204">X-NuGet-ApiKey</span></span>           | <span data-ttu-id="62562-205">필수 푸시 및 삭제를 참조 하십시오 [ `PackagePublish` 리소스](package-publish-resource.md)</span><span class="sxs-lookup"><span data-stu-id="62562-205">Required for push and delete, see [`PackagePublish` resource](package-publish-resource.md)</span></span>
<span data-ttu-id="62562-206">X-NuGet-Client-Version</span><span class="sxs-lookup"><span data-stu-id="62562-206">X-NuGet-Client-Version</span></span>   | <span data-ttu-id="62562-207">**사용 되지 않는** 대체 `X-NuGet-Protocol-Version`</span><span class="sxs-lookup"><span data-stu-id="62562-207">**Deprecated** and replaced by `X-NuGet-Protocol-Version`</span></span>
<span data-ttu-id="62562-208">X-NuGet-Protocol-Version</span><span class="sxs-lookup"><span data-stu-id="62562-208">X-NuGet-Protocol-Version</span></span> | <span data-ttu-id="62562-209">Nuget.org에 대해서만 특정 경우에 필요한 참조 [nuget.org 프로토콜](NuGet-Protocols.md)</span><span class="sxs-lookup"><span data-stu-id="62562-209">Required in certain cases only on nuget.org, see [nuget.org protocols](NuGet-Protocols.md)</span></span>
<span data-ttu-id="62562-210">X-NuGet-Session-Id</span><span class="sxs-lookup"><span data-stu-id="62562-210">X-NuGet-Session-Id</span></span>       | <span data-ttu-id="62562-211">*선택적*합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-211">*Optional*.</span></span> <span data-ttu-id="62562-212">NuGet 클라이언트가 v4.7 + 같은 NuGet 클라이언트 세션의 일부인 HTTP 요청을 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-212">NuGet clients v4.7+ identify HTTP requests that are part of the same NuGet client session.</span></span> <span data-ttu-id="62562-213">에 대 한 `PackageReference` 있는 복원 작업은 자동 완성, 등의 다른 시나리오에는 단일 세션 id 및 `packages.config` 복원 몇 가지 다른 세션 id의 코드는 포함 하는 방법으로 인해 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62562-213">For `PackageReference` restore operations there is a single session id, for other scenarios such as auto complete, and `packages.config` restore there may be several different session id's due to how the code is factored.</span></span>

## <a name="authentication"></a><span data-ttu-id="62562-214">인증</span><span class="sxs-lookup"><span data-stu-id="62562-214">Authentication</span></span>

<span data-ttu-id="62562-215">인증을 정의 하는 패키지 원본 구현을 몫입니다.</span><span class="sxs-lookup"><span data-stu-id="62562-215">Authentication is left up to the package source implementation to define.</span></span> <span data-ttu-id="62562-216">만 nuget.org에 대 한는 `PackagePublish` 리소스는 특별 한 API 키 헤더를 통해 인증이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-216">For nuget.org, only the `PackagePublish` resource requires authentication via a special API key header.</span></span> <span data-ttu-id="62562-217">참조 [ `PackagePublish` 리소스](package-publish-resource.md) 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="62562-217">See [`PackagePublish` resource](package-publish-resource.md) for details.</span></span>
