---
title: 자동 완성, NuGet API
description: 검색 자동 완성 서비스 패키지 Id의 대화형 검색 및 버전을 지원합니다.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d5e1936c6c5406a1a376c16b2bad5351320dfb4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822138"
---
# <a name="autocomplete"></a><span data-ttu-id="f315e-103">자동 완성</span><span class="sxs-lookup"><span data-stu-id="f315e-103">Autocomplete</span></span>

<span data-ttu-id="f315e-104">V3 API를 사용 하 여 패키지 ID 및 버전 자동 완성 환경을 구축 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="f315e-105">자동 완성 쿼리를 만드는 데 사용 되는 리소스는는 `SearchAutocompleteService` 에서 리소스를 찾을 [서비스 인덱스](service-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="f315e-106">버전 관리</span><span class="sxs-lookup"><span data-stu-id="f315e-106">Versioning</span></span>

<span data-ttu-id="f315e-107">다음 `@type` 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-107">The following `@type` values are used:</span></span>

<span data-ttu-id="f315e-108">@type 값</span><span class="sxs-lookup"><span data-stu-id="f315e-108">@type value</span></span>                          | <span data-ttu-id="f315e-109">노트</span><span class="sxs-lookup"><span data-stu-id="f315e-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="f315e-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="f315e-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="f315e-111">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="f315e-111">The initial release</span></span>
<span data-ttu-id="f315e-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="f315e-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="f315e-113">별칭 `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="f315e-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="f315e-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="f315e-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="f315e-115">별칭 `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="f315e-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="f315e-116">기준 URL</span><span class="sxs-lookup"><span data-stu-id="f315e-116">Base URL</span></span>

<span data-ttu-id="f315e-117">다음 Api에 대 한 기본 URL의 값은는 `@id` 앞에서 언급 한 리소스 중 하나가 지정 된 연결 된 속성 `@type` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="f315e-118">다음 문서에서 자리 표시자 기준 URL `{@id}` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="f315e-119">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="f315e-119">HTTP Methods</span></span>

<span data-ttu-id="f315e-120">HTTP 메서드를 등록 리소스 지원에 있는 모든 Url `GET` 및 `HEAD`합니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="f315e-121">패키지 Id에 대 한 검색</span><span class="sxs-lookup"><span data-stu-id="f315e-121">Search for package IDs</span></span>

<span data-ttu-id="f315e-122">첫 번째 자동 완성 API 패키지 ID 문자열의 일부에 대 한 검색 기능을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="f315e-123">NuGet 패키지 소스와 통합 하 여 사용자 인터페이스에서 패키지 typeahead 기능을 제공 하려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="f315e-124">목록에 없는 버전에만 사용 하 여 패키지 결과에 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="f315e-125">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="f315e-125">Request parameters</span></span>

<span data-ttu-id="f315e-126">이름</span><span class="sxs-lookup"><span data-stu-id="f315e-126">Name</span></span>        | <span data-ttu-id="f315e-127">입력</span><span class="sxs-lookup"><span data-stu-id="f315e-127">In</span></span>     | <span data-ttu-id="f315e-128">형식</span><span class="sxs-lookup"><span data-stu-id="f315e-128">Type</span></span>    | <span data-ttu-id="f315e-129">필수</span><span class="sxs-lookup"><span data-stu-id="f315e-129">Required</span></span> | <span data-ttu-id="f315e-130">노트</span><span class="sxs-lookup"><span data-stu-id="f315e-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="f315e-131">q</span><span class="sxs-lookup"><span data-stu-id="f315e-131">q</span></span>           | <span data-ttu-id="f315e-132">URL</span><span class="sxs-lookup"><span data-stu-id="f315e-132">URL</span></span>    | <span data-ttu-id="f315e-133">string</span><span class="sxs-lookup"><span data-stu-id="f315e-133">string</span></span>  | <span data-ttu-id="f315e-134">아니요</span><span class="sxs-lookup"><span data-stu-id="f315e-134">no</span></span>       | <span data-ttu-id="f315e-135">패키지 Id와 비교할 문자열</span><span class="sxs-lookup"><span data-stu-id="f315e-135">The string to compare against package IDs</span></span>
<span data-ttu-id="f315e-136">skip</span><span class="sxs-lookup"><span data-stu-id="f315e-136">skip</span></span>        | <span data-ttu-id="f315e-137">URL</span><span class="sxs-lookup"><span data-stu-id="f315e-137">URL</span></span>    | <span data-ttu-id="f315e-138">정수</span><span class="sxs-lookup"><span data-stu-id="f315e-138">integer</span></span> | <span data-ttu-id="f315e-139">아니요</span><span class="sxs-lookup"><span data-stu-id="f315e-139">no</span></span>       | <span data-ttu-id="f315e-140">페이지 매김 건너뛸 결과의 수</span><span class="sxs-lookup"><span data-stu-id="f315e-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="f315e-141">take</span><span class="sxs-lookup"><span data-stu-id="f315e-141">take</span></span>        | <span data-ttu-id="f315e-142">URL</span><span class="sxs-lookup"><span data-stu-id="f315e-142">URL</span></span>    | <span data-ttu-id="f315e-143">정수</span><span class="sxs-lookup"><span data-stu-id="f315e-143">integer</span></span> | <span data-ttu-id="f315e-144">아니요</span><span class="sxs-lookup"><span data-stu-id="f315e-144">no</span></span>       | <span data-ttu-id="f315e-145">페이지 매김 반환할 결과의 수</span><span class="sxs-lookup"><span data-stu-id="f315e-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="f315e-146">시험판</span><span class="sxs-lookup"><span data-stu-id="f315e-146">prerelease</span></span>  | <span data-ttu-id="f315e-147">URL</span><span class="sxs-lookup"><span data-stu-id="f315e-147">URL</span></span>    | <span data-ttu-id="f315e-148">boolean</span><span class="sxs-lookup"><span data-stu-id="f315e-148">boolean</span></span> | <span data-ttu-id="f315e-149">아니요</span><span class="sxs-lookup"><span data-stu-id="f315e-149">no</span></span>       | <span data-ttu-id="f315e-150">`true` 또는 `false` 포함할지 여부를 결정 [시험판 패키지](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="f315e-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="f315e-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="f315e-151">semVerLevel</span></span> | <span data-ttu-id="f315e-152">URL</span><span class="sxs-lookup"><span data-stu-id="f315e-152">URL</span></span>    | <span data-ttu-id="f315e-153">string</span><span class="sxs-lookup"><span data-stu-id="f315e-153">string</span></span>  | <span data-ttu-id="f315e-154">아니요</span><span class="sxs-lookup"><span data-stu-id="f315e-154">no</span></span>       | <span data-ttu-id="f315e-155">SemVer 1.0.0 버전 문자열</span><span class="sxs-lookup"><span data-stu-id="f315e-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="f315e-156">자동 완성 쿼리 `q` 서버 구현에 의해 정의 된 방식으로 구문 분석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="f315e-157">nuget.org 카멜식 대/소문자 및 기호 문자만 여 원래를 접두사 부분인 spliting에서 생성 된 ID의 패키지 ID 토큰에 대 한 쿼리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="f315e-158">`skip` 매개 변수 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="f315e-159">`take` 매개 변수는 0 보다 큰 정수 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="f315e-160">서버 구현에는 최대 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="f315e-161">경우 `prerelease` 을 제공 하지 않으면 시험판 패키지 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="f315e-162">`semVerLevel` 쿼리 매개 변수를 사용에 동의 [SemVer 2.0.0 패키지](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)합니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="f315e-163">이 쿼리 매개 변수가 제외 되 면 SemVer 1.0.0 호환 되는 버전을 사용 하 여 유일한 패키지 Id가 반환 됩니다 (으로 [표준 NuGet 버전 관리](../reference/package-versioning.md) 4 정수 부분을 사용 하 여 버전 문자열 등의 제한 사항).</span><span class="sxs-lookup"><span data-stu-id="f315e-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="f315e-164">경우 `semVerLevel=2.0.0` 제공 1.0.0 SemVer와 호환 패키지가 SemVer 2.0.0 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="f315e-165">참조는 [nuget.org에 대 한 SemVer 2.0.0 지원](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="f315e-166">응답</span><span class="sxs-lookup"><span data-stu-id="f315e-166">Response</span></span>

<span data-ttu-id="f315e-167">응답은 최대에 포함 된 JSON 문서 `take` 자동 완성 결과입니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="f315e-168">루트 JSON 개체에 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="f315e-169">이름</span><span class="sxs-lookup"><span data-stu-id="f315e-169">Name</span></span>      | <span data-ttu-id="f315e-170">형식</span><span class="sxs-lookup"><span data-stu-id="f315e-170">Type</span></span>             | <span data-ttu-id="f315e-171">필수</span><span class="sxs-lookup"><span data-stu-id="f315e-171">Required</span></span> | <span data-ttu-id="f315e-172">노트</span><span class="sxs-lookup"><span data-stu-id="f315e-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="f315e-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="f315e-173">totalHits</span></span> | <span data-ttu-id="f315e-174">정수</span><span class="sxs-lookup"><span data-stu-id="f315e-174">integer</span></span>          | <span data-ttu-id="f315e-175">예</span><span class="sxs-lookup"><span data-stu-id="f315e-175">yes</span></span>      | <span data-ttu-id="f315e-176">총 수에 관계 없이 일치 `skip` 및 `take`</span><span class="sxs-lookup"><span data-stu-id="f315e-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="f315e-177">데이터</span><span class="sxs-lookup"><span data-stu-id="f315e-177">data</span></span>      | <span data-ttu-id="f315e-178">문자열의 배열</span><span class="sxs-lookup"><span data-stu-id="f315e-178">array of strings</span></span> | <span data-ttu-id="f315e-179">예</span><span class="sxs-lookup"><span data-stu-id="f315e-179">yes</span></span>      | <span data-ttu-id="f315e-180">요청에서 일치 하는 패키지 Id</span><span class="sxs-lookup"><span data-stu-id="f315e-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="f315e-181">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="f315e-181">Sample request</span></span>

<span data-ttu-id="f315e-182">가져오기 https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="f315e-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="f315e-183">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="f315e-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="f315e-184">패키지 버전을 열거 합니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-184">Enumerate package versions</span></span>

<span data-ttu-id="f315e-185">이전 API를 사용 하 여 패키지 ID가 검색, 되 면 클라이언트가 제공 된 패키지 ID에 대해 패키지 버전을 열거 하 자동 완성 API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="f315e-186">패키지 버전이 나열 되지 않은 결과에 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-186">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="f315e-187">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="f315e-187">Request parameters</span></span>

<span data-ttu-id="f315e-188">이름</span><span class="sxs-lookup"><span data-stu-id="f315e-188">Name</span></span>        | <span data-ttu-id="f315e-189">입력</span><span class="sxs-lookup"><span data-stu-id="f315e-189">In</span></span>     | <span data-ttu-id="f315e-190">형식</span><span class="sxs-lookup"><span data-stu-id="f315e-190">Type</span></span>    | <span data-ttu-id="f315e-191">필수</span><span class="sxs-lookup"><span data-stu-id="f315e-191">Required</span></span> | <span data-ttu-id="f315e-192">노트</span><span class="sxs-lookup"><span data-stu-id="f315e-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="f315e-193">ID</span><span class="sxs-lookup"><span data-stu-id="f315e-193">id</span></span>          | <span data-ttu-id="f315e-194">URL</span><span class="sxs-lookup"><span data-stu-id="f315e-194">URL</span></span>    | <span data-ttu-id="f315e-195">string</span><span class="sxs-lookup"><span data-stu-id="f315e-195">string</span></span>  | <span data-ttu-id="f315e-196">예</span><span class="sxs-lookup"><span data-stu-id="f315e-196">yes</span></span>      | <span data-ttu-id="f315e-197">에 대 한 버전을 인출 하는 패키지 ID</span><span class="sxs-lookup"><span data-stu-id="f315e-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="f315e-198">시험판</span><span class="sxs-lookup"><span data-stu-id="f315e-198">prerelease</span></span>  | <span data-ttu-id="f315e-199">URL</span><span class="sxs-lookup"><span data-stu-id="f315e-199">URL</span></span>    | <span data-ttu-id="f315e-200">boolean</span><span class="sxs-lookup"><span data-stu-id="f315e-200">boolean</span></span> | <span data-ttu-id="f315e-201">아니요</span><span class="sxs-lookup"><span data-stu-id="f315e-201">no</span></span>       | <span data-ttu-id="f315e-202">`true` 또는 `false` 포함할지 여부를 결정 [시험판 패키지](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="f315e-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="f315e-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="f315e-203">semVerLevel</span></span> | <span data-ttu-id="f315e-204">URL</span><span class="sxs-lookup"><span data-stu-id="f315e-204">URL</span></span>    | <span data-ttu-id="f315e-205">string</span><span class="sxs-lookup"><span data-stu-id="f315e-205">string</span></span>  | <span data-ttu-id="f315e-206">아니요</span><span class="sxs-lookup"><span data-stu-id="f315e-206">no</span></span>       | <span data-ttu-id="f315e-207">SemVer 2.0.0 버전 문자열</span><span class="sxs-lookup"><span data-stu-id="f315e-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="f315e-208">경우 `prerelease` 을 제공 하지 않으면 시험판 패키지 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="f315e-209">`semVerLevel` 쿼리 매개 변수는 SemVer 2.0.0 패키지에 옵트인 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="f315e-210">이 쿼리 매개 변수가 제외 되 면 SemVer 1.0.0 버전에만 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="f315e-211">경우 `semVerLevel=2.0.0` 제공 SemVer 1.0.0 및 SemVer 2.0.0 버전을 모두 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="f315e-212">참조는 [nuget.org에 대 한 SemVer 2.0.0 지원](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="f315e-213">응답</span><span class="sxs-lookup"><span data-stu-id="f315e-213">Response</span></span>

<span data-ttu-id="f315e-214">응답에는 지정 된 쿼리 매개 변수에 의해 필터링 된 제공 된 패키지 ID의 모든 패키지 버전을 포함 하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="f315e-215">루트 JSON 개체에 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="f315e-216">이름</span><span class="sxs-lookup"><span data-stu-id="f315e-216">Name</span></span>      | <span data-ttu-id="f315e-217">형식</span><span class="sxs-lookup"><span data-stu-id="f315e-217">Type</span></span>             | <span data-ttu-id="f315e-218">필수</span><span class="sxs-lookup"><span data-stu-id="f315e-218">Required</span></span> | <span data-ttu-id="f315e-219">노트</span><span class="sxs-lookup"><span data-stu-id="f315e-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="f315e-220">데이터</span><span class="sxs-lookup"><span data-stu-id="f315e-220">data</span></span>      | <span data-ttu-id="f315e-221">문자열의 배열</span><span class="sxs-lookup"><span data-stu-id="f315e-221">array of strings</span></span> | <span data-ttu-id="f315e-222">예</span><span class="sxs-lookup"><span data-stu-id="f315e-222">yes</span></span>      | <span data-ttu-id="f315e-223">패키지 버전 요청에 의해 일치</span><span class="sxs-lookup"><span data-stu-id="f315e-223">The package versions matched by the request</span></span>

<span data-ttu-id="f315e-224">패키지 버전은 `data` 배열 SemVer 2.0.0 빌드 메타 데이터를 포함할 수 (예: `1.0.0+metadata`) 하는 경우는 `semVerLevel=2.0.0` 쿼리 문자열에 제공 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f315e-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="f315e-225">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="f315e-225">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="f315e-226">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="f315e-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]