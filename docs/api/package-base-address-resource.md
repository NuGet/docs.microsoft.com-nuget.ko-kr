---
title: 패키지 콘텐츠를 NuGet API
description: 패키지의 기본 주소는 패키지 자체를 가져오기 위해 간단한 인터페이스입니다.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a6ac40368f30d33f35d4ca0b6cc18ce4bd6efee5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819179"
---
# <a name="package-content"></a><span data-ttu-id="3d854-103">패키지 내용</span><span class="sxs-lookup"><span data-stu-id="3d854-103">Package Content</span></span>

<span data-ttu-id="3d854-104">V3 API를 사용 하는 임의의 패키지의 콘텐츠 (.nupkg 파일)를 인출 하는 URL을 생성 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="3d854-105">패키지 콘텐츠를 가져오기 위해 사용 되는 리소스는는 `PackageBaseAddress` 에서 리소스를 찾을 [서비스 인덱스](service-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="3d854-106">이 리소스에도 모든 버전의 나열 된 패키지를 검색할 수 있도록 또는 목록에 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="3d854-107">이 리소스는 일반적으로 라고 "패키지 기본 주소가" 또는 "플랫 컨테이너" 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="3d854-108">버전 관리</span><span class="sxs-lookup"><span data-stu-id="3d854-108">Versioning</span></span>

<span data-ttu-id="3d854-109">다음 `@type` 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-109">The following `@type` value is used:</span></span>

<span data-ttu-id="3d854-110">@type 값</span><span class="sxs-lookup"><span data-stu-id="3d854-110">@type value</span></span>              | <span data-ttu-id="3d854-111">노트</span><span class="sxs-lookup"><span data-stu-id="3d854-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="3d854-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="3d854-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="3d854-113">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="3d854-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="3d854-114">기준 URL</span><span class="sxs-lookup"><span data-stu-id="3d854-114">Base URL</span></span>

<span data-ttu-id="3d854-115">다음 Api에 대 한 기본 URL의 값은 고 `@id` 앞에서 언급 한 리소스와 연결 된 속성 `@type` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="3d854-116">다음 문서에서 자리 표시자 기준 URL `{@id}` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="3d854-117">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="3d854-117">HTTP methods</span></span>

<span data-ttu-id="3d854-118">HTTP 메서드를 등록 리소스 지원에 있는 모든 Url `GET` 및 `HEAD`합니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="3d854-119">패키지 버전을 열거 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-119">Enumerate package versions</span></span>

<span data-ttu-id="3d854-120">클라이언트는 패키지 ID를 알고 있는 패키지 버전의 패키지를 검색 하려는 경우 원본에 사용할 수 있는, 클라이언트가 모든 패키지 버전을 열거 하는 예측 가능한 URL을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="3d854-121">이 목록은 사용할 계획이 "디렉터리 목록" 아래에 언급 된 패키지 콘텐츠 API에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="3d854-122">이 목록에 나열 된 및 목록에 없는 패키지 버전을 모두 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="3d854-123">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="3d854-123">Request parameters</span></span>

<span data-ttu-id="3d854-124">이름</span><span class="sxs-lookup"><span data-stu-id="3d854-124">Name</span></span>     | <span data-ttu-id="3d854-125">입력</span><span class="sxs-lookup"><span data-stu-id="3d854-125">In</span></span>     | <span data-ttu-id="3d854-126">형식</span><span class="sxs-lookup"><span data-stu-id="3d854-126">Type</span></span>    | <span data-ttu-id="3d854-127">필수</span><span class="sxs-lookup"><span data-stu-id="3d854-127">Required</span></span> | <span data-ttu-id="3d854-128">노트</span><span class="sxs-lookup"><span data-stu-id="3d854-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="3d854-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="3d854-129">LOWER_ID</span></span> | <span data-ttu-id="3d854-130">URL</span><span class="sxs-lookup"><span data-stu-id="3d854-130">URL</span></span>    | <span data-ttu-id="3d854-131">string</span><span class="sxs-lookup"><span data-stu-id="3d854-131">string</span></span>  | <span data-ttu-id="3d854-132">예</span><span class="sxs-lookup"><span data-stu-id="3d854-132">yes</span></span>      | <span data-ttu-id="3d854-133">패키지 ID, 소문자</span><span class="sxs-lookup"><span data-stu-id="3d854-133">The package ID, lowercase</span></span>

<span data-ttu-id="3d854-134">`LOWER_ID` 값은 소문자를 유지 하 여 구현 하는 규칙을 사용 하 여 원하는 패키지 ID입니다. NET의 [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) 메서드.</span><span class="sxs-lookup"><span data-stu-id="3d854-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="3d854-135">응답</span><span class="sxs-lookup"><span data-stu-id="3d854-135">Response</span></span>

<span data-ttu-id="3d854-136">패키지 소스가 제공 된 패키지 ID의 버전을 가진 경우에 404 상태 코드 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="3d854-137">패키지 소스가 하나 이상의 버전을 가진 경우에 200 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="3d854-138">응답 본문은 다음과 같은 속성이 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="3d854-139">이름</span><span class="sxs-lookup"><span data-stu-id="3d854-139">Name</span></span>     | <span data-ttu-id="3d854-140">형식</span><span class="sxs-lookup"><span data-stu-id="3d854-140">Type</span></span>             | <span data-ttu-id="3d854-141">필수</span><span class="sxs-lookup"><span data-stu-id="3d854-141">Required</span></span> | <span data-ttu-id="3d854-142">노트</span><span class="sxs-lookup"><span data-stu-id="3d854-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="3d854-143">버전</span><span class="sxs-lookup"><span data-stu-id="3d854-143">versions</span></span> | <span data-ttu-id="3d854-144">문자열의 배열</span><span class="sxs-lookup"><span data-stu-id="3d854-144">array of strings</span></span> | <span data-ttu-id="3d854-145">예</span><span class="sxs-lookup"><span data-stu-id="3d854-145">yes</span></span>      | <span data-ttu-id="3d854-146">패키지 Id 제공</span><span class="sxs-lookup"><span data-stu-id="3d854-146">The package IDs available</span></span>

<span data-ttu-id="3d854-147">문자열은 `versions` 배열 모두 소문자 [NuGet 버전 문자열 정규화](../reference/package-versioning.md#normalized-version-numbers)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="3d854-148">버전 문자열 SemVer 2.0.0 빌드 메타 데이터가 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="3d854-149">이 배열에 버전 문자열에 대 한 정확 하 게 사용할 수 있는지는 `LOWER_VERSION` 다음 끝점에 있는 토큰이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="3d854-150">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="3d854-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="3d854-151">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="3d854-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="3d854-152">패키지 콘텐츠 (.nupkg) 다운로드</span><span class="sxs-lookup"><span data-stu-id="3d854-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="3d854-153">클라이언트 패키지 ID와 버전을 알고 있는 패키지 콘텐츠 다운로드 하려는 경우 다음 URL을 생성할만 필요:</span><span class="sxs-lookup"><span data-stu-id="3d854-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="3d854-154">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="3d854-154">Request parameters</span></span>

<span data-ttu-id="3d854-155">이름</span><span class="sxs-lookup"><span data-stu-id="3d854-155">Name</span></span>          | <span data-ttu-id="3d854-156">입력</span><span class="sxs-lookup"><span data-stu-id="3d854-156">In</span></span>     | <span data-ttu-id="3d854-157">형식</span><span class="sxs-lookup"><span data-stu-id="3d854-157">Type</span></span>   | <span data-ttu-id="3d854-158">필수</span><span class="sxs-lookup"><span data-stu-id="3d854-158">Required</span></span> | <span data-ttu-id="3d854-159">노트</span><span class="sxs-lookup"><span data-stu-id="3d854-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="3d854-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="3d854-160">LOWER_ID</span></span>      | <span data-ttu-id="3d854-161">URL</span><span class="sxs-lookup"><span data-stu-id="3d854-161">URL</span></span>    | <span data-ttu-id="3d854-162">string</span><span class="sxs-lookup"><span data-stu-id="3d854-162">string</span></span> | <span data-ttu-id="3d854-163">예</span><span class="sxs-lookup"><span data-stu-id="3d854-163">yes</span></span>      | <span data-ttu-id="3d854-164">패키지 ID, 소문자</span><span class="sxs-lookup"><span data-stu-id="3d854-164">The package ID, lowercase</span></span>
<span data-ttu-id="3d854-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="3d854-165">LOWER_VERSION</span></span> | <span data-ttu-id="3d854-166">URL</span><span class="sxs-lookup"><span data-stu-id="3d854-166">URL</span></span>    | <span data-ttu-id="3d854-167">string</span><span class="sxs-lookup"><span data-stu-id="3d854-167">string</span></span> | <span data-ttu-id="3d854-168">예</span><span class="sxs-lookup"><span data-stu-id="3d854-168">yes</span></span>      | <span data-ttu-id="3d854-169">소문자를 유지 하 고 정규화 된 패키지 버전</span><span class="sxs-lookup"><span data-stu-id="3d854-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="3d854-170">둘 다 `LOWER_ID` 및 `LOWER_VERSION` 하 여 구현 하는 규칙을 사용 하 여 소문자를 유지 됩니다. NET의 [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) 메서드.</span><span class="sxs-lookup"><span data-stu-id="3d854-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="3d854-171">`LOWER_VERSION` 원하는 패키지 버전 정규화 된 NuGet의 버전을 사용 하 여 [정규화 규칙](../reference/package-versioning.md#normalized-version-numbers)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-171">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="3d854-172">즉, SemVer 2.0.0 사양에서 허용 되는 빌드 메타 데이터를이 경우 제외 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-172">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="3d854-173">응답 본문</span><span class="sxs-lookup"><span data-stu-id="3d854-173">Response body</span></span>

<span data-ttu-id="3d854-174">패키지는 패키지 원본에 있는 경우에 200 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-174">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="3d854-175">응답 본문에 패키지 콘텐츠 자체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-175">The response body will be the package content itself.</span></span>

<span data-ttu-id="3d854-176">패키지는 패키지 원본에 없는 경우에 404 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-176">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="3d854-177">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="3d854-177">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="3d854-178">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="3d854-178">Sample response</span></span>

<span data-ttu-id="3d854-179">Newtonsoft.Json 9.0.1에 대 한.nupkg 있는 이진 스트림.</span><span class="sxs-lookup"><span data-stu-id="3d854-179">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="3d854-180">패키지 매니페스트 (.nuspec) 다운로드</span><span class="sxs-lookup"><span data-stu-id="3d854-180">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="3d854-181">클라이언트 패키지 ID와 버전을 알고 있는 패키지 매니페스트를 다운로드 하는 경우 다음 URL을 생성할만 필요:</span><span class="sxs-lookup"><span data-stu-id="3d854-181">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="3d854-182">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="3d854-182">Request parameters</span></span>

<span data-ttu-id="3d854-183">이름</span><span class="sxs-lookup"><span data-stu-id="3d854-183">Name</span></span>          | <span data-ttu-id="3d854-184">입력</span><span class="sxs-lookup"><span data-stu-id="3d854-184">In</span></span>     | <span data-ttu-id="3d854-185">형식</span><span class="sxs-lookup"><span data-stu-id="3d854-185">Type</span></span>    | <span data-ttu-id="3d854-186">필수</span><span class="sxs-lookup"><span data-stu-id="3d854-186">Required</span></span> | <span data-ttu-id="3d854-187">노트</span><span class="sxs-lookup"><span data-stu-id="3d854-187">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="3d854-188">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="3d854-188">LOWER_ID</span></span>      | <span data-ttu-id="3d854-189">URL</span><span class="sxs-lookup"><span data-stu-id="3d854-189">URL</span></span>    | <span data-ttu-id="3d854-190">string</span><span class="sxs-lookup"><span data-stu-id="3d854-190">string</span></span>  | <span data-ttu-id="3d854-191">예</span><span class="sxs-lookup"><span data-stu-id="3d854-191">yes</span></span>      | <span data-ttu-id="3d854-192">패키지 ID, 소문자</span><span class="sxs-lookup"><span data-stu-id="3d854-192">The package ID, lowercase</span></span>
<span data-ttu-id="3d854-193">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="3d854-193">LOWER_VERSION</span></span> | <span data-ttu-id="3d854-194">URL</span><span class="sxs-lookup"><span data-stu-id="3d854-194">URL</span></span>    | <span data-ttu-id="3d854-195">정수</span><span class="sxs-lookup"><span data-stu-id="3d854-195">integer</span></span> | <span data-ttu-id="3d854-196">예</span><span class="sxs-lookup"><span data-stu-id="3d854-196">yes</span></span>      | <span data-ttu-id="3d854-197">소문자를 유지 하 고 정규화 된 패키지 버전</span><span class="sxs-lookup"><span data-stu-id="3d854-197">The package version, normalized and lowercased</span></span>

<span data-ttu-id="3d854-198">둘 다 `LOWER_ID` 및 `LOWER_VERSION` 하 여 구현 하는 규칙을 사용 하 여 소문자를 유지 됩니다. NET의 [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) 메서드.</span><span class="sxs-lookup"><span data-stu-id="3d854-198">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="3d854-199">`LOWER_VERSION` 원하는 패키지 버전 정규화 된 NuGet의 버전을 사용 하 여 [정규화 규칙](../reference/package-versioning.md#normalized-version-numbers)합니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-199">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="3d854-200">즉, SemVer 2.0.0 사양에서 허용 되는 빌드 메타 데이터를이 경우 제외 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-200">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="3d854-201">응답 본문</span><span class="sxs-lookup"><span data-stu-id="3d854-201">Response body</span></span>

<span data-ttu-id="3d854-202">패키지는 패키지 원본에 있는 경우에 200 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-202">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="3d854-203">응답 본문에는 해당.nupkg에 포함 된.nuspec 패키지 매니페스트를 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-203">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="3d854-204">.nuspec XML 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-204">The .nuspec is an XML document.</span></span>

<span data-ttu-id="3d854-205">패키지는 패키지 원본에 없는 경우에 404 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d854-205">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="3d854-206">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="3d854-206">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="3d854-207">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="3d854-207">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
