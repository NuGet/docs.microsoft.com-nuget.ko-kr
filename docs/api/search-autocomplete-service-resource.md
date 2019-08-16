---
title: 자동 완성, NuGet API
description: 검색 자동 완성 서비스는 패키지 Id 및 버전의 대화형 검색을 지원 합니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488302"
---
# <a name="autocomplete"></a><span data-ttu-id="57f38-103">자동 완성</span><span class="sxs-lookup"><span data-stu-id="57f38-103">Autocomplete</span></span>

<span data-ttu-id="57f38-104">V3 API를 사용 하 여 패키지 ID 및 버전 자동 완성 환경을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="57f38-105">자동 완성 쿼리를 만드는 데 사용 되는 `SearchAutocompleteService` 리소스는 [서비스 인덱스](service-index.md)에 있는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="57f38-106">버전 관리</span><span class="sxs-lookup"><span data-stu-id="57f38-106">Versioning</span></span>

<span data-ttu-id="57f38-107">사용 되는 값은 다음과 같습니다. `@type`</span><span class="sxs-lookup"><span data-stu-id="57f38-107">The following `@type` values are used:</span></span>

<span data-ttu-id="57f38-108">@type 값</span><span class="sxs-lookup"><span data-stu-id="57f38-108">@type value</span></span>                          | <span data-ttu-id="57f38-109">참고</span><span class="sxs-lookup"><span data-stu-id="57f38-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="57f38-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="57f38-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="57f38-111">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="57f38-111">The initial release</span></span>
<span data-ttu-id="57f38-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="57f38-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="57f38-113">별칭`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="57f38-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="57f38-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="57f38-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="57f38-115">별칭`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="57f38-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="57f38-116">기준 URL</span><span class="sxs-lookup"><span data-stu-id="57f38-116">Base URL</span></span>

<span data-ttu-id="57f38-117">다음 api에 대 한 기준 URL은 앞서 언급 한 리소스 `@id` `@type` 값 중 하 나와 연결 된 속성의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="57f38-118">다음 문서에서는 자리 표시자 기준 URL `{@id}` 이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="57f38-119">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="57f38-119">HTTP Methods</span></span>

<span data-ttu-id="57f38-120">등록 리소스에서 찾은 모든 url은 HTTP 메서드 `GET` 및 `HEAD`를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="57f38-121">패키지 Id 검색</span><span class="sxs-lookup"><span data-stu-id="57f38-121">Search for package IDs</span></span>

<span data-ttu-id="57f38-122">첫 번째 자동 완성 API는 패키지 ID 문자열의 일부 검색을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="57f38-123">이는 NuGet 패키지 원본과 통합 된 사용자 인터페이스에 패키지 형식 미리 기능을 제공 하려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="57f38-124">목록에 없는 버전만 포함 된 패키지는 결과에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="57f38-125">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="57f38-125">Request parameters</span></span>

<span data-ttu-id="57f38-126">이름</span><span class="sxs-lookup"><span data-stu-id="57f38-126">Name</span></span>        | <span data-ttu-id="57f38-127">입력</span><span class="sxs-lookup"><span data-stu-id="57f38-127">In</span></span>     | <span data-ttu-id="57f38-128">형식</span><span class="sxs-lookup"><span data-stu-id="57f38-128">Type</span></span>    | <span data-ttu-id="57f38-129">필수</span><span class="sxs-lookup"><span data-stu-id="57f38-129">Required</span></span> | <span data-ttu-id="57f38-130">참고</span><span class="sxs-lookup"><span data-stu-id="57f38-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="57f38-131">q</span><span class="sxs-lookup"><span data-stu-id="57f38-131">q</span></span>           | <span data-ttu-id="57f38-132">URL</span><span class="sxs-lookup"><span data-stu-id="57f38-132">URL</span></span>    | <span data-ttu-id="57f38-133">string</span><span class="sxs-lookup"><span data-stu-id="57f38-133">string</span></span>  | <span data-ttu-id="57f38-134">no</span><span class="sxs-lookup"><span data-stu-id="57f38-134">no</span></span>       | <span data-ttu-id="57f38-135">패키지 Id와 비교할 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-135">The string to compare against package IDs</span></span>
<span data-ttu-id="57f38-136">skip</span><span class="sxs-lookup"><span data-stu-id="57f38-136">skip</span></span>        | <span data-ttu-id="57f38-137">URL</span><span class="sxs-lookup"><span data-stu-id="57f38-137">URL</span></span>    | <span data-ttu-id="57f38-138">integer</span><span class="sxs-lookup"><span data-stu-id="57f38-138">integer</span></span> | <span data-ttu-id="57f38-139">no</span><span class="sxs-lookup"><span data-stu-id="57f38-139">no</span></span>       | <span data-ttu-id="57f38-140">페이지를 매길 때 건너뛸 결과의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="57f38-141">노트</span><span class="sxs-lookup"><span data-stu-id="57f38-141">take</span></span>        | <span data-ttu-id="57f38-142">URL</span><span class="sxs-lookup"><span data-stu-id="57f38-142">URL</span></span>    | <span data-ttu-id="57f38-143">integer</span><span class="sxs-lookup"><span data-stu-id="57f38-143">integer</span></span> | <span data-ttu-id="57f38-144">no</span><span class="sxs-lookup"><span data-stu-id="57f38-144">no</span></span>       | <span data-ttu-id="57f38-145">페이지를 매길 때 반환할 결과의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="57f38-146">시험판</span><span class="sxs-lookup"><span data-stu-id="57f38-146">prerelease</span></span>  | <span data-ttu-id="57f38-147">URL</span><span class="sxs-lookup"><span data-stu-id="57f38-147">URL</span></span>    | <span data-ttu-id="57f38-148">boolean</span><span class="sxs-lookup"><span data-stu-id="57f38-148">boolean</span></span> | <span data-ttu-id="57f38-149">no</span><span class="sxs-lookup"><span data-stu-id="57f38-149">no</span></span>       | <span data-ttu-id="57f38-150">`true`또는 `false` [시험판 패키지](../create-packages/prerelease-packages.md) 를 포함할지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="57f38-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="57f38-151">semVerLevel</span></span> | <span data-ttu-id="57f38-152">URL</span><span class="sxs-lookup"><span data-stu-id="57f38-152">URL</span></span>    | <span data-ttu-id="57f38-153">string</span><span class="sxs-lookup"><span data-stu-id="57f38-153">string</span></span>  | <span data-ttu-id="57f38-154">no</span><span class="sxs-lookup"><span data-stu-id="57f38-154">no</span></span>       | <span data-ttu-id="57f38-155">SemVer 1.0.0 버전 문자열</span><span class="sxs-lookup"><span data-stu-id="57f38-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="57f38-156">자동 완성 쿼리 `q` 는 서버 구현에 정의 된 방식으로 구문 분석 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="57f38-157">nuget.org는 원본에서 카멜식 대/소문자 및 기호 문자를 spliting 하 여 생성 된 ID의 일부인 패키지 ID 토큰의 접두사 쿼리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="57f38-158">매개 `skip` 변수의 기본값은 0입니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="57f38-159">매개 `take` 변수는 0 보다 큰 정수 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="57f38-160">서버 구현에서 최 댓 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="57f38-161">을 `prerelease` 지정 하지 않으면 시험판 패키지가 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="57f38-162">Query 매개 변수는 [SemVer 2.0.0 패키지](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)를 옵트인 (opt in) 하는 데 사용 됩니다. `semVerLevel`</span><span class="sxs-lookup"><span data-stu-id="57f38-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="57f38-163">이 쿼리 매개 변수가 제외 되 면 SemVer 1.0.0 호환 버전이 포함 된 패키지 Id만 반환 됩니다 (4 개의 정수 부분을 포함 하는 버전 문자열과 같은 [표준 NuGet 버전 관리](../concepts/package-versioning.md) 에 대 한 주의).</span><span class="sxs-lookup"><span data-stu-id="57f38-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="57f38-164">가 `semVerLevel=2.0.0` 제공 되는 경우 SemVer 1.0.0 및 SemVer 2.0.0 호환 패키지가 모두 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="57f38-165">자세한 내용은 [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="57f38-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="57f38-166">응답</span><span class="sxs-lookup"><span data-stu-id="57f38-166">Response</span></span>

<span data-ttu-id="57f38-167">응답은 최대 자동 완성 결과를 `take` 포함 하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="57f38-168">루트 JSON 개체에는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="57f38-169">이름</span><span class="sxs-lookup"><span data-stu-id="57f38-169">Name</span></span>      | <span data-ttu-id="57f38-170">형식</span><span class="sxs-lookup"><span data-stu-id="57f38-170">Type</span></span>             | <span data-ttu-id="57f38-171">필수</span><span class="sxs-lookup"><span data-stu-id="57f38-171">Required</span></span> | <span data-ttu-id="57f38-172">참고</span><span class="sxs-lookup"><span data-stu-id="57f38-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="57f38-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="57f38-173">totalHits</span></span> | <span data-ttu-id="57f38-174">integer</span><span class="sxs-lookup"><span data-stu-id="57f38-174">integer</span></span>          | <span data-ttu-id="57f38-175">예</span><span class="sxs-lookup"><span data-stu-id="57f38-175">yes</span></span>      | <span data-ttu-id="57f38-176">총 일치 항목 수, 무시 `skip` 및`take`</span><span class="sxs-lookup"><span data-stu-id="57f38-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="57f38-177">데이터</span><span class="sxs-lookup"><span data-stu-id="57f38-177">data</span></span>      | <span data-ttu-id="57f38-178">문자열 배열</span><span class="sxs-lookup"><span data-stu-id="57f38-178">array of strings</span></span> | <span data-ttu-id="57f38-179">예</span><span class="sxs-lookup"><span data-stu-id="57f38-179">yes</span></span>      | <span data-ttu-id="57f38-180">요청과 일치 하는 패키지 Id</span><span class="sxs-lookup"><span data-stu-id="57f38-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="57f38-181">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="57f38-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="57f38-182">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="57f38-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="57f38-183">패키지 버전 열거</span><span class="sxs-lookup"><span data-stu-id="57f38-183">Enumerate package versions</span></span>

<span data-ttu-id="57f38-184">이전 API를 사용 하 여 패키지 ID가 검색 되 면 클라이언트는 자동 완성 API를 사용 하 여 제공 된 패키지 ID에 대 한 패키지 버전을 열거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="57f38-185">나열 되지 않은 패키지 버전은 결과에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="57f38-186">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="57f38-186">Request parameters</span></span>

<span data-ttu-id="57f38-187">이름</span><span class="sxs-lookup"><span data-stu-id="57f38-187">Name</span></span>        | <span data-ttu-id="57f38-188">입력</span><span class="sxs-lookup"><span data-stu-id="57f38-188">In</span></span>     | <span data-ttu-id="57f38-189">형식</span><span class="sxs-lookup"><span data-stu-id="57f38-189">Type</span></span>    | <span data-ttu-id="57f38-190">필수</span><span class="sxs-lookup"><span data-stu-id="57f38-190">Required</span></span> | <span data-ttu-id="57f38-191">참고</span><span class="sxs-lookup"><span data-stu-id="57f38-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="57f38-192">id</span><span class="sxs-lookup"><span data-stu-id="57f38-192">id</span></span>          | <span data-ttu-id="57f38-193">URL</span><span class="sxs-lookup"><span data-stu-id="57f38-193">URL</span></span>    | <span data-ttu-id="57f38-194">string</span><span class="sxs-lookup"><span data-stu-id="57f38-194">string</span></span>  | <span data-ttu-id="57f38-195">예</span><span class="sxs-lookup"><span data-stu-id="57f38-195">yes</span></span>      | <span data-ttu-id="57f38-196">버전을 가져올 패키지 ID</span><span class="sxs-lookup"><span data-stu-id="57f38-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="57f38-197">시험판</span><span class="sxs-lookup"><span data-stu-id="57f38-197">prerelease</span></span>  | <span data-ttu-id="57f38-198">URL</span><span class="sxs-lookup"><span data-stu-id="57f38-198">URL</span></span>    | <span data-ttu-id="57f38-199">boolean</span><span class="sxs-lookup"><span data-stu-id="57f38-199">boolean</span></span> | <span data-ttu-id="57f38-200">no</span><span class="sxs-lookup"><span data-stu-id="57f38-200">no</span></span>       | <span data-ttu-id="57f38-201">`true`또는 `false` [시험판 패키지](../create-packages/prerelease-packages.md) 를 포함할지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-201">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="57f38-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="57f38-202">semVerLevel</span></span> | <span data-ttu-id="57f38-203">URL</span><span class="sxs-lookup"><span data-stu-id="57f38-203">URL</span></span>    | <span data-ttu-id="57f38-204">string</span><span class="sxs-lookup"><span data-stu-id="57f38-204">string</span></span>  | <span data-ttu-id="57f38-205">no</span><span class="sxs-lookup"><span data-stu-id="57f38-205">no</span></span>       | <span data-ttu-id="57f38-206">SemVer 2.0.0 version 문자열</span><span class="sxs-lookup"><span data-stu-id="57f38-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="57f38-207">을 `prerelease` 지정 하지 않으면 시험판 패키지가 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="57f38-208">`semVerLevel` Query 매개 변수는 SemVer 2.0.0 패키지를 옵트인 (opt in) 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="57f38-209">이 쿼리 매개 변수가 제외 되 면 SemVer 1.0.0 버전만 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="57f38-210">가 `semVerLevel=2.0.0` 제공 되 면 SemVer 1.0.0 및 SemVer 2.0.0 버전이 모두 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="57f38-211">자세한 내용은 [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="57f38-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="57f38-212">응답</span><span class="sxs-lookup"><span data-stu-id="57f38-212">Response</span></span>

<span data-ttu-id="57f38-213">응답은 지정 된 쿼리 매개 변수를 기준으로 필터링 하 여 제공 된 패키지 ID의 모든 패키지 버전을 포함 하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="57f38-214">루트 JSON 개체에는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57f38-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="57f38-215">이름</span><span class="sxs-lookup"><span data-stu-id="57f38-215">Name</span></span>      | <span data-ttu-id="57f38-216">형식</span><span class="sxs-lookup"><span data-stu-id="57f38-216">Type</span></span>             | <span data-ttu-id="57f38-217">필수</span><span class="sxs-lookup"><span data-stu-id="57f38-217">Required</span></span> | <span data-ttu-id="57f38-218">참고</span><span class="sxs-lookup"><span data-stu-id="57f38-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="57f38-219">데이터</span><span class="sxs-lookup"><span data-stu-id="57f38-219">data</span></span>      | <span data-ttu-id="57f38-220">문자열 배열</span><span class="sxs-lookup"><span data-stu-id="57f38-220">array of strings</span></span> | <span data-ttu-id="57f38-221">예</span><span class="sxs-lookup"><span data-stu-id="57f38-221">yes</span></span>      | <span data-ttu-id="57f38-222">요청과 일치 하는 패키지 버전</span><span class="sxs-lookup"><span data-stu-id="57f38-222">The package versions matched by the request</span></span>

<span data-ttu-id="57f38-223">가 쿼리 문자열에 제공 `data` 되는 경우 `1.0.0+metadata`배열의 패키지 버전에는 SemVer 2.0.0 build 메타 데이터 (예:)가 포함 될 수 있습니다. `semVerLevel=2.0.0`</span><span class="sxs-lookup"><span data-stu-id="57f38-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="57f38-224">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="57f38-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="57f38-225">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="57f38-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
