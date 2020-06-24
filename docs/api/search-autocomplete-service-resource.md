---
title: 자동 완성, NuGet API
description: 검색 자동 완성 서비스는 패키지 Id 및 버전의 대화형 검색을 지원 합니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: f574849bf99cd4da4eefd55c3dd5a0648042f0c1
ms.sourcegitcommit: 7e9c0630335ef9ec1e200e2ee9065f702e52a8ec
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85292295"
---
# <a name="autocomplete"></a><span data-ttu-id="30496-103">자동 완성</span><span class="sxs-lookup"><span data-stu-id="30496-103">Autocomplete</span></span>

<span data-ttu-id="30496-104">V3 API를 사용 하 여 패키지 ID 및 버전 자동 완성 환경을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30496-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="30496-105">자동 완성 쿼리를 만드는 데 사용 되는 리소스는 `SearchAutocompleteService` [서비스 인덱스](service-index.md)에 있는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="30496-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="30496-106">버전 관리</span><span class="sxs-lookup"><span data-stu-id="30496-106">Versioning</span></span>

<span data-ttu-id="30496-107">사용 되는 `@type` 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="30496-107">The following `@type` values are used:</span></span>

<span data-ttu-id="30496-108">@type 값</span><span class="sxs-lookup"><span data-stu-id="30496-108">@type value</span></span>                          | <span data-ttu-id="30496-109">참고</span><span class="sxs-lookup"><span data-stu-id="30496-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="30496-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="30496-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="30496-111">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="30496-111">The initial release</span></span>
<span data-ttu-id="30496-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="30496-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="30496-113">별칭`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="30496-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="30496-114">SearchAutocompleteService/3.0.0</span><span class="sxs-lookup"><span data-stu-id="30496-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="30496-115">별칭`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="30496-115">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="30496-116">SearchAutocompleteService/3.5.0</span><span class="sxs-lookup"><span data-stu-id="30496-116">SearchAutocompleteService/3.5.0</span></span>      | <span data-ttu-id="30496-117">쿼리 매개 변수에 대 한 지원을 포함 합니다. `packageType`</span><span class="sxs-lookup"><span data-stu-id="30496-117">Includes support for `packageType` query parameter</span></span>

### <a name="searchautocompleteservice350"></a><span data-ttu-id="30496-118">SearchAutocompleteService/3.5.0</span><span class="sxs-lookup"><span data-stu-id="30496-118">SearchAutocompleteService/3.5.0</span></span>
<span data-ttu-id="30496-119">이 버전은 쿼리 매개 변수에 대 한 지원을 도입 `packageType` 하 여 작성 된 패키지 형식으로 필터링 할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="30496-119">This version introduces support for the `packageType` query parameter, allowing filtering by author defined package types.</span></span> <span data-ttu-id="30496-120">에 대 한 쿼리와 완전히 호환 됩니다 `SearchAutocompleteService` .</span><span class="sxs-lookup"><span data-stu-id="30496-120">It is fully backwards compatible with queries to `SearchAutocompleteService`.</span></span>

## <a name="base-url"></a><span data-ttu-id="30496-121">기준 URL</span><span class="sxs-lookup"><span data-stu-id="30496-121">Base URL</span></span>

<span data-ttu-id="30496-122">다음 Api에 대 한 기준 URL은 `@id` 앞서 언급 한 리소스 값 중 하 나와 연결 된 속성의 값입니다 `@type` .</span><span class="sxs-lookup"><span data-stu-id="30496-122">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="30496-123">다음 문서에서는 자리 표시자 기준 URL `{@id}` 이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30496-123">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="30496-124">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="30496-124">HTTP Methods</span></span>

<span data-ttu-id="30496-125">등록 리소스에서 찾은 모든 Url은 HTTP 메서드 및를 지원 합니다 `GET` `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="30496-125">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="30496-126">패키지 Id 검색</span><span class="sxs-lookup"><span data-stu-id="30496-126">Search for package IDs</span></span>

<span data-ttu-id="30496-127">첫 번째 자동 완성 API는 패키지 ID 문자열의 일부 검색을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="30496-127">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="30496-128">이는 NuGet 패키지 원본과 통합 된 사용자 인터페이스에 패키지 형식 미리 기능을 제공 하려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="30496-128">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="30496-129">목록에 없는 버전만 포함 된 패키지는 결과에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30496-129">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}

### <a name="request-parameters"></a><span data-ttu-id="30496-130">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="30496-130">Request parameters</span></span>

<span data-ttu-id="30496-131">Name</span><span class="sxs-lookup"><span data-stu-id="30496-131">Name</span></span>        | <span data-ttu-id="30496-132">In(다음 안에)</span><span class="sxs-lookup"><span data-stu-id="30496-132">In</span></span>     | <span data-ttu-id="30496-133">형식</span><span class="sxs-lookup"><span data-stu-id="30496-133">Type</span></span>    | <span data-ttu-id="30496-134">필수</span><span class="sxs-lookup"><span data-stu-id="30496-134">Required</span></span> | <span data-ttu-id="30496-135">참고</span><span class="sxs-lookup"><span data-stu-id="30496-135">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="30496-136">q</span><span class="sxs-lookup"><span data-stu-id="30496-136">q</span></span>           | <span data-ttu-id="30496-137">URL</span><span class="sxs-lookup"><span data-stu-id="30496-137">URL</span></span>    | <span data-ttu-id="30496-138">문자열</span><span class="sxs-lookup"><span data-stu-id="30496-138">string</span></span>  | <span data-ttu-id="30496-139">아니요</span><span class="sxs-lookup"><span data-stu-id="30496-139">no</span></span>       | <span data-ttu-id="30496-140">패키지 Id와 비교할 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="30496-140">The string to compare against package IDs</span></span>
<span data-ttu-id="30496-141">skip</span><span class="sxs-lookup"><span data-stu-id="30496-141">skip</span></span>        | <span data-ttu-id="30496-142">URL</span><span class="sxs-lookup"><span data-stu-id="30496-142">URL</span></span>    | <span data-ttu-id="30496-143">integer</span><span class="sxs-lookup"><span data-stu-id="30496-143">integer</span></span> | <span data-ttu-id="30496-144">아니요</span><span class="sxs-lookup"><span data-stu-id="30496-144">no</span></span>       | <span data-ttu-id="30496-145">페이지를 매길 때 건너뛸 결과의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="30496-145">The number of results to skip, for pagination</span></span>
<span data-ttu-id="30496-146">take</span><span class="sxs-lookup"><span data-stu-id="30496-146">take</span></span>        | <span data-ttu-id="30496-147">URL</span><span class="sxs-lookup"><span data-stu-id="30496-147">URL</span></span>    | <span data-ttu-id="30496-148">integer</span><span class="sxs-lookup"><span data-stu-id="30496-148">integer</span></span> | <span data-ttu-id="30496-149">아니요</span><span class="sxs-lookup"><span data-stu-id="30496-149">no</span></span>       | <span data-ttu-id="30496-150">페이지를 매길 때 반환할 결과의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="30496-150">The number of results to return, for pagination</span></span>
<span data-ttu-id="30496-151">prerelease</span><span class="sxs-lookup"><span data-stu-id="30496-151">prerelease</span></span>  | <span data-ttu-id="30496-152">URL</span><span class="sxs-lookup"><span data-stu-id="30496-152">URL</span></span>    | <span data-ttu-id="30496-153">boolean</span><span class="sxs-lookup"><span data-stu-id="30496-153">boolean</span></span> | <span data-ttu-id="30496-154">아니요</span><span class="sxs-lookup"><span data-stu-id="30496-154">no</span></span>       | <span data-ttu-id="30496-155">`true`또는 `false` [시험판 패키지](../create-packages/prerelease-packages.md) 를 포함할지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="30496-155">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="30496-156">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="30496-156">semVerLevel</span></span> | <span data-ttu-id="30496-157">URL</span><span class="sxs-lookup"><span data-stu-id="30496-157">URL</span></span>    | <span data-ttu-id="30496-158">문자열</span><span class="sxs-lookup"><span data-stu-id="30496-158">string</span></span>  | <span data-ttu-id="30496-159">아니요</span><span class="sxs-lookup"><span data-stu-id="30496-159">no</span></span>       | <span data-ttu-id="30496-160">SemVer 1.0.0 버전 문자열</span><span class="sxs-lookup"><span data-stu-id="30496-160">A SemVer 1.0.0 version string</span></span> 
<span data-ttu-id="30496-161">packageType</span><span class="sxs-lookup"><span data-stu-id="30496-161">packageType</span></span> | <span data-ttu-id="30496-162">URL</span><span class="sxs-lookup"><span data-stu-id="30496-162">URL</span></span>    | <span data-ttu-id="30496-163">문자열</span><span class="sxs-lookup"><span data-stu-id="30496-163">string</span></span>  | <span data-ttu-id="30496-164">아니요</span><span class="sxs-lookup"><span data-stu-id="30496-164">no</span></span>       | <span data-ttu-id="30496-165">패키지를 필터링 하는 데 사용할 패키지 유형 (에 추가 됨 `SearchAutocompleteService/3.5.0` )</span><span class="sxs-lookup"><span data-stu-id="30496-165">The package type to use to filter packages (added in `SearchAutocompleteService/3.5.0`)</span></span>

<span data-ttu-id="30496-166">자동 완성 쿼리는 `q` 서버 구현에 정의 된 방식으로 구문 분석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30496-166">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="30496-167">nuget.org는 원본에서 카멜식 대/소문자 및 기호 문자를 spliting 하 여 생성 된 ID의 일부인 패키지 ID 토큰의 접두사 쿼리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="30496-167">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="30496-168">`skip`매개 변수의 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="30496-168">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="30496-169">`take`매개 변수는 0 보다 큰 정수 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30496-169">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="30496-170">서버 구현에서 최 댓 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30496-170">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="30496-171">`prerelease`을 지정 하지 않으면 시험판 패키지가 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30496-171">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="30496-172">`semVerLevel`Query 매개 변수는 [SemVer 2.0.0 패키지](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)를 옵트인 (opt in) 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30496-172">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="30496-173">이 쿼리 매개 변수가 제외 되 면 SemVer 1.0.0 호환 버전이 포함 된 패키지 Id만 반환 됩니다 (4 개의 정수 부분을 포함 하는 버전 문자열과 같은 [표준 NuGet 버전 관리](../concepts/package-versioning.md) 에 대 한 주의).</span><span class="sxs-lookup"><span data-stu-id="30496-173">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="30496-174">`semVerLevel=2.0.0`가 제공 되는 경우 SemVer 1.0.0 및 SemVer 2.0.0 호환 패키지가 모두 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30496-174">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="30496-175">자세한 내용은 [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="30496-175">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

<span data-ttu-id="30496-176">매개 변수는 패키지 유형 `packageType` 이름과 일치 하는 패키지 유형이 하나 이상 포함 된 패키지만 자동 완성 결과를 추가로 필터링 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30496-176">The `packageType` parameter is used to further filter the autocomplete results to only packages that have at least one package type matching the package type name.</span></span>
<span data-ttu-id="30496-177">제공 된 패키지 유형이 [패키지 유형 문서](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D)에 정의 된 유효한 패키지 유형이 아닌 경우 빈 결과가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30496-177">If the provided package type is not a valid package type as defined by the [Package Type document](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), an empty result will returned.</span></span>
<span data-ttu-id="30496-178">제공 된 패키지 유형이 비어 있는 경우 필터가 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30496-178">If the provided package type is empty, no filter will be applied.</span></span> <span data-ttu-id="30496-179">즉, 매개 변수에 값을 전달 하지 않으면 `packageType` 매개 변수가 전달 되지 않은 것 처럼 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="30496-179">In other words, passing no value to the `packageType` parameter will behave as if the parameter was not passed.</span></span>

### <a name="response"></a><span data-ttu-id="30496-180">응답</span><span class="sxs-lookup"><span data-stu-id="30496-180">Response</span></span>

<span data-ttu-id="30496-181">응답은 최대 자동 완성 결과를 포함 하는 JSON 문서입니다 `take` .</span><span class="sxs-lookup"><span data-stu-id="30496-181">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="30496-182">루트 JSON 개체에는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30496-182">The root JSON object has the following properties:</span></span>

<span data-ttu-id="30496-183">Name</span><span class="sxs-lookup"><span data-stu-id="30496-183">Name</span></span>      | <span data-ttu-id="30496-184">Type</span><span class="sxs-lookup"><span data-stu-id="30496-184">Type</span></span>             | <span data-ttu-id="30496-185">필수</span><span class="sxs-lookup"><span data-stu-id="30496-185">Required</span></span> | <span data-ttu-id="30496-186">참고</span><span class="sxs-lookup"><span data-stu-id="30496-186">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="30496-187">totalHits</span><span class="sxs-lookup"><span data-stu-id="30496-187">totalHits</span></span> | <span data-ttu-id="30496-188">integer</span><span class="sxs-lookup"><span data-stu-id="30496-188">integer</span></span>          | <span data-ttu-id="30496-189">예</span><span class="sxs-lookup"><span data-stu-id="30496-189">yes</span></span>      | <span data-ttu-id="30496-190">총 일치 항목 수, 무시 `skip` 및`take`</span><span class="sxs-lookup"><span data-stu-id="30496-190">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="30496-191">데이터</span><span class="sxs-lookup"><span data-stu-id="30496-191">data</span></span>      | <span data-ttu-id="30496-192">문자열 배열</span><span class="sxs-lookup"><span data-stu-id="30496-192">array of strings</span></span> | <span data-ttu-id="30496-193">예</span><span class="sxs-lookup"><span data-stu-id="30496-193">yes</span></span>      | <span data-ttu-id="30496-194">요청과 일치 하는 패키지 Id</span><span class="sxs-lookup"><span data-stu-id="30496-194">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="30496-195">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="30496-195">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="30496-196">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="30496-196">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="30496-197">패키지 버전 열거</span><span class="sxs-lookup"><span data-stu-id="30496-197">Enumerate package versions</span></span>

<span data-ttu-id="30496-198">이전 API를 사용 하 여 패키지 ID가 검색 되 면 클라이언트는 자동 완성 API를 사용 하 여 제공 된 패키지 ID에 대 한 패키지 버전을 열거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30496-198">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="30496-199">나열 되지 않은 패키지 버전은 결과에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30496-199">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="30496-200">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="30496-200">Request parameters</span></span>

<span data-ttu-id="30496-201">Name</span><span class="sxs-lookup"><span data-stu-id="30496-201">Name</span></span>        | <span data-ttu-id="30496-202">In(다음 안에)</span><span class="sxs-lookup"><span data-stu-id="30496-202">In</span></span>     | <span data-ttu-id="30496-203">형식</span><span class="sxs-lookup"><span data-stu-id="30496-203">Type</span></span>    | <span data-ttu-id="30496-204">필수</span><span class="sxs-lookup"><span data-stu-id="30496-204">Required</span></span> | <span data-ttu-id="30496-205">참고</span><span class="sxs-lookup"><span data-stu-id="30496-205">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="30496-206">id</span><span class="sxs-lookup"><span data-stu-id="30496-206">id</span></span>          | <span data-ttu-id="30496-207">URL</span><span class="sxs-lookup"><span data-stu-id="30496-207">URL</span></span>    | <span data-ttu-id="30496-208">문자열</span><span class="sxs-lookup"><span data-stu-id="30496-208">string</span></span>  | <span data-ttu-id="30496-209">예</span><span class="sxs-lookup"><span data-stu-id="30496-209">yes</span></span>      | <span data-ttu-id="30496-210">버전을 가져올 패키지 ID</span><span class="sxs-lookup"><span data-stu-id="30496-210">The package ID to fetch versions for</span></span>
<span data-ttu-id="30496-211">prerelease</span><span class="sxs-lookup"><span data-stu-id="30496-211">prerelease</span></span>  | <span data-ttu-id="30496-212">URL</span><span class="sxs-lookup"><span data-stu-id="30496-212">URL</span></span>    | <span data-ttu-id="30496-213">boolean</span><span class="sxs-lookup"><span data-stu-id="30496-213">boolean</span></span> | <span data-ttu-id="30496-214">아니요</span><span class="sxs-lookup"><span data-stu-id="30496-214">no</span></span>       | <span data-ttu-id="30496-215">`true`또는 `false` [시험판 패키지](../create-packages/prerelease-packages.md) 를 포함할지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="30496-215">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="30496-216">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="30496-216">semVerLevel</span></span> | <span data-ttu-id="30496-217">URL</span><span class="sxs-lookup"><span data-stu-id="30496-217">URL</span></span>    | <span data-ttu-id="30496-218">문자열</span><span class="sxs-lookup"><span data-stu-id="30496-218">string</span></span>  | <span data-ttu-id="30496-219">아니요</span><span class="sxs-lookup"><span data-stu-id="30496-219">no</span></span>       | <span data-ttu-id="30496-220">SemVer 2.0.0 version 문자열</span><span class="sxs-lookup"><span data-stu-id="30496-220">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="30496-221">`prerelease`을 지정 하지 않으면 시험판 패키지가 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30496-221">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="30496-222">`semVerLevel`Query 매개 변수는 SemVer 2.0.0 패키지를 옵트인 (opt in) 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30496-222">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="30496-223">이 쿼리 매개 변수가 제외 되 면 SemVer 1.0.0 버전만 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30496-223">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="30496-224">`semVerLevel=2.0.0`가 제공 되 면 SemVer 1.0.0 및 SemVer 2.0.0 버전이 모두 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30496-224">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="30496-225">자세한 내용은 [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="30496-225">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="30496-226">응답</span><span class="sxs-lookup"><span data-stu-id="30496-226">Response</span></span>

<span data-ttu-id="30496-227">응답은 지정 된 쿼리 매개 변수를 기준으로 필터링 하 여 제공 된 패키지 ID의 모든 패키지 버전을 포함 하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="30496-227">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="30496-228">루트 JSON 개체에는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30496-228">The root JSON object has the following property:</span></span>

<span data-ttu-id="30496-229">Name</span><span class="sxs-lookup"><span data-stu-id="30496-229">Name</span></span>      | <span data-ttu-id="30496-230">Type</span><span class="sxs-lookup"><span data-stu-id="30496-230">Type</span></span>             | <span data-ttu-id="30496-231">필수</span><span class="sxs-lookup"><span data-stu-id="30496-231">Required</span></span> | <span data-ttu-id="30496-232">참고</span><span class="sxs-lookup"><span data-stu-id="30496-232">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="30496-233">데이터</span><span class="sxs-lookup"><span data-stu-id="30496-233">data</span></span>      | <span data-ttu-id="30496-234">문자열 배열</span><span class="sxs-lookup"><span data-stu-id="30496-234">array of strings</span></span> | <span data-ttu-id="30496-235">예</span><span class="sxs-lookup"><span data-stu-id="30496-235">yes</span></span>      | <span data-ttu-id="30496-236">요청과 일치 하는 패키지 버전</span><span class="sxs-lookup"><span data-stu-id="30496-236">The package versions matched by the request</span></span>

<span data-ttu-id="30496-237">`data` `1.0.0+metadata` `semVerLevel=2.0.0` 가 쿼리 문자열에 제공 되는 경우 배열의 패키지 버전에는 SemVer 2.0.0 build 메타 데이터 (예:)가 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30496-237">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="30496-238">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="30496-238">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="30496-239">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="30496-239">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
