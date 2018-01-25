---
title: "자동 완성, NuGet API | Microsoft Docs"
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
ms.technology: 
description: "검색 자동 완성 서비스 패키지 Id의 대화형 검색 및 버전을 지원합니다."
keywords: "NuGet 자동 완성 API, NuGet 패키지 ID, 패키지 ID 부분 문자열을 검색합니다."
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7c984ca61799293d7832851b80cf3fefc4734288
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="autocomplete"></a><span data-ttu-id="cc7f0-104">자동 완성</span><span class="sxs-lookup"><span data-stu-id="cc7f0-104">Autocomplete</span></span>

<span data-ttu-id="cc7f0-105">V3 API를 사용 하 여 패키지 ID 및 버전 자동 완성 환경을 구축 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-105">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="cc7f0-106">자동 완성 쿼리를 만드는 데 사용 되는 리소스는는 `SearchAutocompleteService` 에서 리소스를 찾을 [서비스 인덱스](service-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-106">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="cc7f0-107">버전 관리</span><span class="sxs-lookup"><span data-stu-id="cc7f0-107">Versioning</span></span>

<span data-ttu-id="cc7f0-108">다음 `@type` 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-108">The following `@type` values are used:</span></span>

<span data-ttu-id="cc7f0-109">@type 값</span><span class="sxs-lookup"><span data-stu-id="cc7f0-109">@type value</span></span>                          | <span data-ttu-id="cc7f0-110">노트</span><span class="sxs-lookup"><span data-stu-id="cc7f0-110">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="cc7f0-111">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="cc7f0-111">SearchAutocompleteService</span></span>            | <span data-ttu-id="cc7f0-112">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="cc7f0-112">The initial release</span></span>
<span data-ttu-id="cc7f0-113">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="cc7f0-113">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="cc7f0-114">별칭`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="cc7f0-114">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="cc7f0-115">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="cc7f0-115">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="cc7f0-116">별칭`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="cc7f0-116">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="cc7f0-117">기준 URL</span><span class="sxs-lookup"><span data-stu-id="cc7f0-117">Base URL</span></span>

<span data-ttu-id="cc7f0-118">다음 Api에 대 한 기본 URL의 값은는 `@id` 앞에서 언급 한 리소스 중 하나가 지정 된 연결 된 속성 `@type` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-118">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="cc7f0-119">다음 문서에서 자리 표시자 기준 URL `{@id}` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="cc7f0-120">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="cc7f0-120">HTTP Methods</span></span>

<span data-ttu-id="cc7f0-121">HTTP 메서드를 등록 리소스 지원에 있는 모든 Url `GET` 및 `HEAD`합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="cc7f0-122">패키지 Id에 대 한 검색</span><span class="sxs-lookup"><span data-stu-id="cc7f0-122">Search for package IDs</span></span>

<span data-ttu-id="cc7f0-123">첫 번째 자동 완성 API 패키지 ID 문자열의 일부에 대 한 검색 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-123">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="cc7f0-124">NuGet 패키지 소스와 통합 하 여 사용자 인터페이스에서 패키지 typeahead 기능을 제공 하려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-124">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="cc7f0-125">목록에 없는 버전에만 사용 하 여 패키지 결과에 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-125">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="cc7f0-126">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="cc7f0-126">Request parameters</span></span>

<span data-ttu-id="cc7f0-127">name</span><span class="sxs-lookup"><span data-stu-id="cc7f0-127">Name</span></span>        | <span data-ttu-id="cc7f0-128">입력</span><span class="sxs-lookup"><span data-stu-id="cc7f0-128">In</span></span>     | <span data-ttu-id="cc7f0-129">형식</span><span class="sxs-lookup"><span data-stu-id="cc7f0-129">Type</span></span>    | <span data-ttu-id="cc7f0-130">필수</span><span class="sxs-lookup"><span data-stu-id="cc7f0-130">Required</span></span> | <span data-ttu-id="cc7f0-131">노트</span><span class="sxs-lookup"><span data-stu-id="cc7f0-131">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="cc7f0-132">q</span><span class="sxs-lookup"><span data-stu-id="cc7f0-132">q</span></span>           | <span data-ttu-id="cc7f0-133">URL</span><span class="sxs-lookup"><span data-stu-id="cc7f0-133">URL</span></span>    | <span data-ttu-id="cc7f0-134">string</span><span class="sxs-lookup"><span data-stu-id="cc7f0-134">string</span></span>  | <span data-ttu-id="cc7f0-135">아니요</span><span class="sxs-lookup"><span data-stu-id="cc7f0-135">no</span></span>       | <span data-ttu-id="cc7f0-136">패키지 Id와 비교할 문자열</span><span class="sxs-lookup"><span data-stu-id="cc7f0-136">The string to compare against package IDs</span></span>
<span data-ttu-id="cc7f0-137">skip</span><span class="sxs-lookup"><span data-stu-id="cc7f0-137">skip</span></span>        | <span data-ttu-id="cc7f0-138">URL</span><span class="sxs-lookup"><span data-stu-id="cc7f0-138">URL</span></span>    | <span data-ttu-id="cc7f0-139">정수</span><span class="sxs-lookup"><span data-stu-id="cc7f0-139">integer</span></span> | <span data-ttu-id="cc7f0-140">아니요</span><span class="sxs-lookup"><span data-stu-id="cc7f0-140">no</span></span>       | <span data-ttu-id="cc7f0-141">페이지 매김 건너뛸 결과의 수</span><span class="sxs-lookup"><span data-stu-id="cc7f0-141">The number of results to skip, for pagination</span></span>
<span data-ttu-id="cc7f0-142">take</span><span class="sxs-lookup"><span data-stu-id="cc7f0-142">take</span></span>        | <span data-ttu-id="cc7f0-143">URL</span><span class="sxs-lookup"><span data-stu-id="cc7f0-143">URL</span></span>    | <span data-ttu-id="cc7f0-144">정수</span><span class="sxs-lookup"><span data-stu-id="cc7f0-144">integer</span></span> | <span data-ttu-id="cc7f0-145">아니요</span><span class="sxs-lookup"><span data-stu-id="cc7f0-145">no</span></span>       | <span data-ttu-id="cc7f0-146">페이지 매김 반환할 결과의 수</span><span class="sxs-lookup"><span data-stu-id="cc7f0-146">The number of results to return, for pagination</span></span>
<span data-ttu-id="cc7f0-147">시험판</span><span class="sxs-lookup"><span data-stu-id="cc7f0-147">prerelease</span></span>  | <span data-ttu-id="cc7f0-148">URL</span><span class="sxs-lookup"><span data-stu-id="cc7f0-148">URL</span></span>    | <span data-ttu-id="cc7f0-149">boolean</span><span class="sxs-lookup"><span data-stu-id="cc7f0-149">boolean</span></span> | <span data-ttu-id="cc7f0-150">아니요</span><span class="sxs-lookup"><span data-stu-id="cc7f0-150">no</span></span>       | <span data-ttu-id="cc7f0-151">`true`또는 `false` 포함할지 여부를 결정 [시험판 패키지](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="cc7f0-151">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="cc7f0-152">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="cc7f0-152">semVerLevel</span></span> | <span data-ttu-id="cc7f0-153">URL</span><span class="sxs-lookup"><span data-stu-id="cc7f0-153">URL</span></span>    | <span data-ttu-id="cc7f0-154">string</span><span class="sxs-lookup"><span data-stu-id="cc7f0-154">string</span></span>  | <span data-ttu-id="cc7f0-155">아니요</span><span class="sxs-lookup"><span data-stu-id="cc7f0-155">no</span></span>       | <span data-ttu-id="cc7f0-156">SemVer 1.0.0 버전 문자열</span><span class="sxs-lookup"><span data-stu-id="cc7f0-156">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="cc7f0-157">자동 완성 쿼리 `q` 서버 구현에 의해 정의 된 방식으로 구문 분석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-157">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="cc7f0-158">nuget.org 카멜식 대/소문자 및 기호 문자만 여 원래를 접두사 부분인 spliting에서 생성 된 ID의 패키지 ID 토큰에 대 한 쿼리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-158">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="cc7f0-159">`skip` 매개 변수 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-159">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="cc7f0-160">`take` 매개 변수는 0 보다 큰 정수 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-160">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="cc7f0-161">서버 구현에는 최대 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-161">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="cc7f0-162">경우 `prerelease` 을 제공 하지 않으면 시험판 패키지 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-162">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="cc7f0-163">`semVerLevel` 쿼리 매개 변수를 사용에 동의 [SemVer 2.0.0 패키지](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-163">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="cc7f0-164">이 쿼리 매개 변수가 제외 되 면 SemVer 1.0.0 호환 되는 버전을 사용 하 여 유일한 패키지 Id가 반환 됩니다 (으로 [표준 NuGet 버전 관리](../reference/package-versioning.md) 4 정수 부분을 사용 하 여 버전 문자열 등의 제한 사항).</span><span class="sxs-lookup"><span data-stu-id="cc7f0-164">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="cc7f0-165">경우 `semVerLevel=2.0.0` 제공 1.0.0 SemVer와 호환 패키지가 SemVer 2.0.0 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-165">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="cc7f0-166">참조는 [nuget.org에 대 한 SemVer 2.0.0 지원](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-166">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="cc7f0-167">응답</span><span class="sxs-lookup"><span data-stu-id="cc7f0-167">Response</span></span>

<span data-ttu-id="cc7f0-168">응답은 최대에 포함 된 JSON 문서 `take` 자동 완성 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-168">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="cc7f0-169">루트 JSON 개체에 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-169">The root JSON object has the following properties:</span></span>

<span data-ttu-id="cc7f0-170">name</span><span class="sxs-lookup"><span data-stu-id="cc7f0-170">Name</span></span>      | <span data-ttu-id="cc7f0-171">형식</span><span class="sxs-lookup"><span data-stu-id="cc7f0-171">Type</span></span>             | <span data-ttu-id="cc7f0-172">필수</span><span class="sxs-lookup"><span data-stu-id="cc7f0-172">Required</span></span> | <span data-ttu-id="cc7f0-173">노트</span><span class="sxs-lookup"><span data-stu-id="cc7f0-173">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="cc7f0-174">totalHits</span><span class="sxs-lookup"><span data-stu-id="cc7f0-174">totalHits</span></span> | <span data-ttu-id="cc7f0-175">정수</span><span class="sxs-lookup"><span data-stu-id="cc7f0-175">integer</span></span>          | <span data-ttu-id="cc7f0-176">예</span><span class="sxs-lookup"><span data-stu-id="cc7f0-176">yes</span></span>      | <span data-ttu-id="cc7f0-177">총 수에 관계 없이 일치 `skip` 및`take`</span><span class="sxs-lookup"><span data-stu-id="cc7f0-177">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="cc7f0-178">데이터</span><span class="sxs-lookup"><span data-stu-id="cc7f0-178">data</span></span>      | <span data-ttu-id="cc7f0-179">문자열의 배열</span><span class="sxs-lookup"><span data-stu-id="cc7f0-179">array of strings</span></span> | <span data-ttu-id="cc7f0-180">예</span><span class="sxs-lookup"><span data-stu-id="cc7f0-180">yes</span></span>      | <span data-ttu-id="cc7f0-181">요청에서 일치 하는 패키지 Id</span><span class="sxs-lookup"><span data-stu-id="cc7f0-181">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="cc7f0-182">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="cc7f0-182">Sample request</span></span>

<span data-ttu-id="cc7f0-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="cc7f0-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="cc7f0-184">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="cc7f0-184">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="cc7f0-185">패키지 버전을 열거 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-185">Enumerate package versions</span></span>

<span data-ttu-id="cc7f0-186">이전 API를 사용 하 여 패키지 ID가 검색, 되 면 클라이언트가 제공 된 패키지 ID에 대해 패키지 버전을 열거 하 자동 완성 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-186">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="cc7f0-187">패키지 버전이 나열 되지 않은 결과에 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-187">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="cc7f0-188">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="cc7f0-188">Request parameters</span></span>

<span data-ttu-id="cc7f0-189">name</span><span class="sxs-lookup"><span data-stu-id="cc7f0-189">Name</span></span>        | <span data-ttu-id="cc7f0-190">입력</span><span class="sxs-lookup"><span data-stu-id="cc7f0-190">In</span></span>     | <span data-ttu-id="cc7f0-191">형식</span><span class="sxs-lookup"><span data-stu-id="cc7f0-191">Type</span></span>    | <span data-ttu-id="cc7f0-192">필수</span><span class="sxs-lookup"><span data-stu-id="cc7f0-192">Required</span></span> | <span data-ttu-id="cc7f0-193">노트</span><span class="sxs-lookup"><span data-stu-id="cc7f0-193">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="cc7f0-194">ID</span><span class="sxs-lookup"><span data-stu-id="cc7f0-194">id</span></span>          | <span data-ttu-id="cc7f0-195">URL</span><span class="sxs-lookup"><span data-stu-id="cc7f0-195">URL</span></span>    | <span data-ttu-id="cc7f0-196">string</span><span class="sxs-lookup"><span data-stu-id="cc7f0-196">string</span></span>  | <span data-ttu-id="cc7f0-197">예</span><span class="sxs-lookup"><span data-stu-id="cc7f0-197">yes</span></span>      | <span data-ttu-id="cc7f0-198">에 대 한 버전을 인출 하는 패키지 ID</span><span class="sxs-lookup"><span data-stu-id="cc7f0-198">The package ID to fetch versions for</span></span>
<span data-ttu-id="cc7f0-199">시험판</span><span class="sxs-lookup"><span data-stu-id="cc7f0-199">prerelease</span></span>  | <span data-ttu-id="cc7f0-200">URL</span><span class="sxs-lookup"><span data-stu-id="cc7f0-200">URL</span></span>    | <span data-ttu-id="cc7f0-201">boolean</span><span class="sxs-lookup"><span data-stu-id="cc7f0-201">boolean</span></span> | <span data-ttu-id="cc7f0-202">아니요</span><span class="sxs-lookup"><span data-stu-id="cc7f0-202">no</span></span>       | <span data-ttu-id="cc7f0-203">`true`또는 `false` 포함할지 여부를 결정 [시험판 패키지](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="cc7f0-203">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="cc7f0-204">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="cc7f0-204">semVerLevel</span></span> | <span data-ttu-id="cc7f0-205">URL</span><span class="sxs-lookup"><span data-stu-id="cc7f0-205">URL</span></span>    | <span data-ttu-id="cc7f0-206">string</span><span class="sxs-lookup"><span data-stu-id="cc7f0-206">string</span></span>  | <span data-ttu-id="cc7f0-207">아니요</span><span class="sxs-lookup"><span data-stu-id="cc7f0-207">no</span></span>       | <span data-ttu-id="cc7f0-208">SemVer 2.0.0 버전 문자열</span><span class="sxs-lookup"><span data-stu-id="cc7f0-208">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="cc7f0-209">경우 `prerelease` 을 제공 하지 않으면 시험판 패키지 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-209">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="cc7f0-210">`semVerLevel` 쿼리 매개 변수는 SemVer 2.0.0 패키지에 옵트인 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-210">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="cc7f0-211">이 쿼리 매개 변수가 제외 되 면 SemVer 1.0.0 버전에만 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-211">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="cc7f0-212">경우 `semVerLevel=2.0.0` 제공 SemVer 1.0.0 및 SemVer 2.0.0 버전을 모두 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-212">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="cc7f0-213">참조는 [nuget.org에 대 한 SemVer 2.0.0 지원](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-213">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="cc7f0-214">응답</span><span class="sxs-lookup"><span data-stu-id="cc7f0-214">Response</span></span>

<span data-ttu-id="cc7f0-215">응답에는 지정 된 쿼리 매개 변수에 의해 필터링 된 제공 된 패키지 ID의 모든 패키지 버전을 포함 하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-215">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="cc7f0-216">루트 JSON 개체에 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-216">The root JSON object has the following property:</span></span>

<span data-ttu-id="cc7f0-217">name</span><span class="sxs-lookup"><span data-stu-id="cc7f0-217">Name</span></span>      | <span data-ttu-id="cc7f0-218">형식</span><span class="sxs-lookup"><span data-stu-id="cc7f0-218">Type</span></span>             | <span data-ttu-id="cc7f0-219">필수</span><span class="sxs-lookup"><span data-stu-id="cc7f0-219">Required</span></span> | <span data-ttu-id="cc7f0-220">노트</span><span class="sxs-lookup"><span data-stu-id="cc7f0-220">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="cc7f0-221">데이터</span><span class="sxs-lookup"><span data-stu-id="cc7f0-221">data</span></span>      | <span data-ttu-id="cc7f0-222">문자열의 배열</span><span class="sxs-lookup"><span data-stu-id="cc7f0-222">array of strings</span></span> | <span data-ttu-id="cc7f0-223">예</span><span class="sxs-lookup"><span data-stu-id="cc7f0-223">yes</span></span>      | <span data-ttu-id="cc7f0-224">패키지 버전 요청에 의해 일치</span><span class="sxs-lookup"><span data-stu-id="cc7f0-224">The package versions matched by the request</span></span>

<span data-ttu-id="cc7f0-225">패키지 버전은 `data` 배열 SemVer 2.0.0 빌드 메타 데이터를 포함할 수 (예: `1.0.0+metadata`) 하는 경우는 `semVerLevel=2.0.0` 쿼리 문자열에 제공 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cc7f0-225">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="cc7f0-226">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="cc7f0-226">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="cc7f0-227">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="cc7f0-227">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
