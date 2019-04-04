---
title: 자동 완성, NuGet API
description: 검색 자동 완성 서비스 패키지 Id의 대화형 검색 버전을 지원 합니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fdc3ad8aa239a42d8a4c169a757715e856bdcb41
ms.sourcegitcommit: 9f94e00428d83aef4a7a87db679129eff7720c59
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/03/2019
ms.locfileid: "58911051"
---
# <a name="autocomplete"></a><span data-ttu-id="e0005-103">자동 완성</span><span class="sxs-lookup"><span data-stu-id="e0005-103">Autocomplete</span></span>

<span data-ttu-id="e0005-104">V3 API를 사용 하는 패키지 ID 및 버전 자동 완성 환경을 빌드하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="e0005-105">자동 완성 쿼리를 만드는 데 사용할 리소스를 `SearchAutocompleteService` 에서 리소스를 찾을 합니다 [서비스 인덱스](service-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="e0005-106">버전 관리</span><span class="sxs-lookup"><span data-stu-id="e0005-106">Versioning</span></span>

<span data-ttu-id="e0005-107">다음 `@type` 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-107">The following `@type` values are used:</span></span>

<span data-ttu-id="e0005-108">@type 값</span><span class="sxs-lookup"><span data-stu-id="e0005-108">@type value</span></span>                          | <span data-ttu-id="e0005-109">노트</span><span class="sxs-lookup"><span data-stu-id="e0005-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="e0005-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="e0005-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="e0005-111">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="e0005-111">The initial release</span></span>
<span data-ttu-id="e0005-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="e0005-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="e0005-113">별칭</span><span class="sxs-lookup"><span data-stu-id="e0005-113">Alias of</span></span> `SearchAutocompleteService`
<span data-ttu-id="e0005-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="e0005-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="e0005-115">별칭</span><span class="sxs-lookup"><span data-stu-id="e0005-115">Alias of</span></span> `SearchAutocompleteService`

## <a name="base-url"></a><span data-ttu-id="e0005-116">기준 URL</span><span class="sxs-lookup"><span data-stu-id="e0005-116">Base URL</span></span>

<span data-ttu-id="e0005-117">다음 Api에 대 한 기본 URL의 값은는 `@id` 앞에서 언급 한 리소스 중 하나를 사용 하 여 연결 된 속성 `@type` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="e0005-118">다음 문서에서 자리 표시자 기준 URL `{@id}` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e0005-119">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="e0005-119">HTTP Methods</span></span>

<span data-ttu-id="e0005-120">HTTP 메서드를 등록 리소스 지원에서 발견 한 모든 Url `GET` 고 `HEAD`입니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="e0005-121">패키지 Id 검색</span><span class="sxs-lookup"><span data-stu-id="e0005-121">Search for package IDs</span></span>

<span data-ttu-id="e0005-122">첫 번째 자동 완성 API 패키지 ID 문자열의 부분에 대 한 검색 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="e0005-123">NuGet 패키지 소스를 통합 하는 사용자 인터페이스에서 패키지 미리 입력 기능을 제공 하려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="e0005-124">목록에 없는 버전만 사용 하 여 패키지 결과에 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="e0005-125">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="e0005-125">Request parameters</span></span>

<span data-ttu-id="e0005-126">이름</span><span class="sxs-lookup"><span data-stu-id="e0005-126">Name</span></span>        | <span data-ttu-id="e0005-127">입력</span><span class="sxs-lookup"><span data-stu-id="e0005-127">In</span></span>     | <span data-ttu-id="e0005-128">형식</span><span class="sxs-lookup"><span data-stu-id="e0005-128">Type</span></span>    | <span data-ttu-id="e0005-129">필수</span><span class="sxs-lookup"><span data-stu-id="e0005-129">Required</span></span> | <span data-ttu-id="e0005-130">노트</span><span class="sxs-lookup"><span data-stu-id="e0005-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="e0005-131">q</span><span class="sxs-lookup"><span data-stu-id="e0005-131">q</span></span>           | <span data-ttu-id="e0005-132">URL</span><span class="sxs-lookup"><span data-stu-id="e0005-132">URL</span></span>    | <span data-ttu-id="e0005-133">string</span><span class="sxs-lookup"><span data-stu-id="e0005-133">string</span></span>  | <span data-ttu-id="e0005-134">아니요</span><span class="sxs-lookup"><span data-stu-id="e0005-134">no</span></span>       | <span data-ttu-id="e0005-135">패키지 Id와 비교할 문자열</span><span class="sxs-lookup"><span data-stu-id="e0005-135">The string to compare against package IDs</span></span>
<span data-ttu-id="e0005-136">skip</span><span class="sxs-lookup"><span data-stu-id="e0005-136">skip</span></span>        | <span data-ttu-id="e0005-137">URL</span><span class="sxs-lookup"><span data-stu-id="e0005-137">URL</span></span>    | <span data-ttu-id="e0005-138">정수</span><span class="sxs-lookup"><span data-stu-id="e0005-138">integer</span></span> | <span data-ttu-id="e0005-139">아니요</span><span class="sxs-lookup"><span data-stu-id="e0005-139">no</span></span>       | <span data-ttu-id="e0005-140">페이지 매김 건너뛸 결과 수</span><span class="sxs-lookup"><span data-stu-id="e0005-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="e0005-141">Take</span><span class="sxs-lookup"><span data-stu-id="e0005-141">take</span></span>        | <span data-ttu-id="e0005-142">URL</span><span class="sxs-lookup"><span data-stu-id="e0005-142">URL</span></span>    | <span data-ttu-id="e0005-143">정수</span><span class="sxs-lookup"><span data-stu-id="e0005-143">integer</span></span> | <span data-ttu-id="e0005-144">아니요</span><span class="sxs-lookup"><span data-stu-id="e0005-144">no</span></span>       | <span data-ttu-id="e0005-145">페이지 매김 반환할 결과 수</span><span class="sxs-lookup"><span data-stu-id="e0005-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="e0005-146">시험판</span><span class="sxs-lookup"><span data-stu-id="e0005-146">prerelease</span></span>  | <span data-ttu-id="e0005-147">URL</span><span class="sxs-lookup"><span data-stu-id="e0005-147">URL</span></span>    | <span data-ttu-id="e0005-148">boolean</span><span class="sxs-lookup"><span data-stu-id="e0005-148">boolean</span></span> | <span data-ttu-id="e0005-149">아니요</span><span class="sxs-lookup"><span data-stu-id="e0005-149">no</span></span>       | `true` <span data-ttu-id="e0005-150">또는 `false` 포함할지 여부를 결정 [시험판 패키지](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="e0005-150">or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="e0005-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="e0005-151">semVerLevel</span></span> | <span data-ttu-id="e0005-152">URL</span><span class="sxs-lookup"><span data-stu-id="e0005-152">URL</span></span>    | <span data-ttu-id="e0005-153">string</span><span class="sxs-lookup"><span data-stu-id="e0005-153">string</span></span>  | <span data-ttu-id="e0005-154">아니요</span><span class="sxs-lookup"><span data-stu-id="e0005-154">no</span></span>       | <span data-ttu-id="e0005-155">SemVer 1.0.0 버전 문자열</span><span class="sxs-lookup"><span data-stu-id="e0005-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="e0005-156">자동 완성 쿼리 `q` 서버 구현에 의해 정의 된 방식으로 구문 분석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="e0005-157">nuget.org에 카멜식 대/소문자 및 기호 문자는 원래를 조각을 페이지 분할에서 생성 된 ID의 패키지 ID 토큰의 접두사에 대 한 쿼리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="e0005-158">`skip` 매개 변수의 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="e0005-159">`take` 매개 변수는 0 보다 큰 정수 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="e0005-160">서버 구현은 최대 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="e0005-161">경우 `prerelease` 을 제공 하지 않으면 시험판 패키지 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="e0005-162">합니다 `semVerLevel` 쿼리 매개 변수를 사용 하도록 옵트인 [SemVer 2.0.0 패키지](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="e0005-163">이 쿼리 매개 변수를 제외 하는 경우 1.0.0 SemVer 호환 되는 버전을 사용 하 여 패키지 Id만 반환 됩니다 (사용 하 여는 [표준 NuGet 버전 관리](../reference/package-versioning.md) 4 정수 부분을 사용 하 여 버전 문자열과 같은 주의).</span><span class="sxs-lookup"><span data-stu-id="e0005-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="e0005-164">경우 `semVerLevel=2.0.0` 제공 SemVer 1.0.0 및 2.0.0 SemVer 호환 패키지 모두 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="e0005-165">참조를 [nuget.org SemVer 2.0.0 지원을](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="e0005-166">응답</span><span class="sxs-lookup"><span data-stu-id="e0005-166">Response</span></span>

<span data-ttu-id="e0005-167">응답은 최대 담긴 JSON 문서가 `take` 자동 완성 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="e0005-168">루트 JSON 개체의 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="e0005-169">이름</span><span class="sxs-lookup"><span data-stu-id="e0005-169">Name</span></span>      | <span data-ttu-id="e0005-170">형식</span><span class="sxs-lookup"><span data-stu-id="e0005-170">Type</span></span>             | <span data-ttu-id="e0005-171">필수</span><span class="sxs-lookup"><span data-stu-id="e0005-171">Required</span></span> | <span data-ttu-id="e0005-172">노트</span><span class="sxs-lookup"><span data-stu-id="e0005-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="e0005-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="e0005-173">totalHits</span></span> | <span data-ttu-id="e0005-174">정수</span><span class="sxs-lookup"><span data-stu-id="e0005-174">integer</span></span>          | <span data-ttu-id="e0005-175">예</span><span class="sxs-lookup"><span data-stu-id="e0005-175">yes</span></span>      | <span data-ttu-id="e0005-176">총 개수에 관계 없이 일치 `skip` 및</span><span class="sxs-lookup"><span data-stu-id="e0005-176">The total number of matches, disregarding `skip` and</span></span> `take`
<span data-ttu-id="e0005-177">데이터</span><span class="sxs-lookup"><span data-stu-id="e0005-177">data</span></span>      | <span data-ttu-id="e0005-178">문자열의 배열</span><span class="sxs-lookup"><span data-stu-id="e0005-178">array of strings</span></span> | <span data-ttu-id="e0005-179">예</span><span class="sxs-lookup"><span data-stu-id="e0005-179">yes</span></span>      | <span data-ttu-id="e0005-180">요청에서 일치 하는 패키지 Id</span><span class="sxs-lookup"><span data-stu-id="e0005-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="e0005-181">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="e0005-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="e0005-182">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="e0005-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="e0005-183">패키지 버전을 열거 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-183">Enumerate package versions</span></span>

<span data-ttu-id="e0005-184">이전 API를 사용 하 여 패키지 ID가 검색 되 면 클라이언트는 제공 된 패키지 ID의 패키지 버전을 열거 하려면 자동 완성 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="e0005-185">나열 되지 않은 패키지 버전을 결과에 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="e0005-186">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="e0005-186">Request parameters</span></span>

<span data-ttu-id="e0005-187">이름</span><span class="sxs-lookup"><span data-stu-id="e0005-187">Name</span></span>        | <span data-ttu-id="e0005-188">입력</span><span class="sxs-lookup"><span data-stu-id="e0005-188">In</span></span>     | <span data-ttu-id="e0005-189">형식</span><span class="sxs-lookup"><span data-stu-id="e0005-189">Type</span></span>    | <span data-ttu-id="e0005-190">필수</span><span class="sxs-lookup"><span data-stu-id="e0005-190">Required</span></span> | <span data-ttu-id="e0005-191">노트</span><span class="sxs-lookup"><span data-stu-id="e0005-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="e0005-192">ID</span><span class="sxs-lookup"><span data-stu-id="e0005-192">id</span></span>          | <span data-ttu-id="e0005-193">URL</span><span class="sxs-lookup"><span data-stu-id="e0005-193">URL</span></span>    | <span data-ttu-id="e0005-194">string</span><span class="sxs-lookup"><span data-stu-id="e0005-194">string</span></span>  | <span data-ttu-id="e0005-195">예</span><span class="sxs-lookup"><span data-stu-id="e0005-195">yes</span></span>      | <span data-ttu-id="e0005-196">에 대 한 버전을 가져올 패키지 ID</span><span class="sxs-lookup"><span data-stu-id="e0005-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="e0005-197">시험판</span><span class="sxs-lookup"><span data-stu-id="e0005-197">prerelease</span></span>  | <span data-ttu-id="e0005-198">URL</span><span class="sxs-lookup"><span data-stu-id="e0005-198">URL</span></span>    | <span data-ttu-id="e0005-199">boolean</span><span class="sxs-lookup"><span data-stu-id="e0005-199">boolean</span></span> | <span data-ttu-id="e0005-200">아니요</span><span class="sxs-lookup"><span data-stu-id="e0005-200">no</span></span>       | `true` <span data-ttu-id="e0005-201">또는 `false` 포함할지 여부를 결정 [시험판 패키지](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="e0005-201">or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="e0005-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="e0005-202">semVerLevel</span></span> | <span data-ttu-id="e0005-203">URL</span><span class="sxs-lookup"><span data-stu-id="e0005-203">URL</span></span>    | <span data-ttu-id="e0005-204">string</span><span class="sxs-lookup"><span data-stu-id="e0005-204">string</span></span>  | <span data-ttu-id="e0005-205">아니요</span><span class="sxs-lookup"><span data-stu-id="e0005-205">no</span></span>       | <span data-ttu-id="e0005-206">SemVer 2.0.0 버전 문자열</span><span class="sxs-lookup"><span data-stu-id="e0005-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="e0005-207">경우 `prerelease` 을 제공 하지 않으면 시험판 패키지 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="e0005-208">`semVerLevel` 쿼리 매개 변수는 SemVer 2.0.0 패키지에 옵트인 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="e0005-209">이 쿼리 매개 변수를 제외 하는 경우 SemVer 1.0.0 버전에만 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="e0005-210">경우 `semVerLevel=2.0.0` 제공 SemVer 1.0.0 및 SemVer 2.0.0 버전이 모두 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="e0005-211">참조를 [nuget.org SemVer 2.0.0 지원을](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="e0005-212">응답</span><span class="sxs-lookup"><span data-stu-id="e0005-212">Response</span></span>

<span data-ttu-id="e0005-213">응답에는 지정 된 쿼리 매개 변수에 의해 필터링 제공 된 패키지 ID의 모든 패키지 버전을 포함 하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="e0005-214">루트 JSON 개체에는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="e0005-215">이름</span><span class="sxs-lookup"><span data-stu-id="e0005-215">Name</span></span>      | <span data-ttu-id="e0005-216">형식</span><span class="sxs-lookup"><span data-stu-id="e0005-216">Type</span></span>             | <span data-ttu-id="e0005-217">필수</span><span class="sxs-lookup"><span data-stu-id="e0005-217">Required</span></span> | <span data-ttu-id="e0005-218">노트</span><span class="sxs-lookup"><span data-stu-id="e0005-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="e0005-219">데이터</span><span class="sxs-lookup"><span data-stu-id="e0005-219">data</span></span>      | <span data-ttu-id="e0005-220">문자열의 배열</span><span class="sxs-lookup"><span data-stu-id="e0005-220">array of strings</span></span> | <span data-ttu-id="e0005-221">예</span><span class="sxs-lookup"><span data-stu-id="e0005-221">yes</span></span>      | <span data-ttu-id="e0005-222">요청에서 일치 하는 패키지 버전</span><span class="sxs-lookup"><span data-stu-id="e0005-222">The package versions matched by the request</span></span>

<span data-ttu-id="e0005-223">패키지 버전을 `data` 배열 SemVer 2.0.0 빌드 메타 데이터를 포함할 수 있습니다 (예: `1.0.0+metadata`) 하는 경우는 `semVerLevel=2.0.0` 쿼리 문자열에 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0005-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e0005-224">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="e0005-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="e0005-225">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="e0005-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
