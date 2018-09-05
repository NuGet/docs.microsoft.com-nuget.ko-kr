---
title: 패키지 콘텐츠를 NuGet API
description: 패키지 기준 주소에는 패키지 자체를 가져오기 위해 간단한 인터페이스입니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 740defc34077793b81fb35db73a2eee393ae3bac
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547156"
---
# <a name="package-content"></a><span data-ttu-id="a935b-103">패키지 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="a935b-103">Package Content</span></span>

<span data-ttu-id="a935b-104">V3 API를 사용 하는 임의의 패키지의 콘텐츠 (.nupkg 파일)를 가져올 URL을 생성 하는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="a935b-105">패키지 콘텐츠를 가져오는 중에 사용 되는 리소스를 `PackageBaseAddress` 에서 리소스를 찾을 합니다 [서비스 인덱스](service-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="a935b-106">이 리소스에 나열 된 패키지의 모든 버전의 검색도 사용 하도록 설정 또는 비공개입니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="a935b-107">이 리소스 일반적으로 라고 "플랫 컨테이너" 또는 "패키지 기본 주소가"으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="a935b-108">버전 관리</span><span class="sxs-lookup"><span data-stu-id="a935b-108">Versioning</span></span>

<span data-ttu-id="a935b-109">다음 `@type` 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-109">The following `@type` value is used:</span></span>

<span data-ttu-id="a935b-110">@type 값</span><span class="sxs-lookup"><span data-stu-id="a935b-110">@type value</span></span>              | <span data-ttu-id="a935b-111">노트</span><span class="sxs-lookup"><span data-stu-id="a935b-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="a935b-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="a935b-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="a935b-113">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="a935b-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="a935b-114">기준 URL</span><span class="sxs-lookup"><span data-stu-id="a935b-114">Base URL</span></span>

<span data-ttu-id="a935b-115">다음 Api에 대 한 기본 URL의 값은는 `@id` 앞에서 언급 한 리소스와 연결 된 속성 `@type` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="a935b-116">다음 문서에서 자리 표시자 기준 URL `{@id}` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="a935b-117">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="a935b-117">HTTP methods</span></span>

<span data-ttu-id="a935b-118">HTTP 메서드를 등록 리소스 지원에서 발견 한 모든 Url `GET` 고 `HEAD`입니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="a935b-119">패키지 버전을 열거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-119">Enumerate package versions</span></span>

<span data-ttu-id="a935b-120">클라이언트 패키지 ID를 알고 있는 패키지 버전 패키지를 검색 하려는 경우 원본에서 사용할 수 있는, 클라이언트가 모든 패키지 버전을 열거 하는 예측 가능한 URL을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="a935b-121">이 목록은 아래에 설명 된 패키지 콘텐츠 API에 대 한 "디렉터리 목록" 할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="a935b-122">이 목록에 나열 되며 목록에 없는 패키지 버전을 모두 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="a935b-123">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a935b-123">Request parameters</span></span>

<span data-ttu-id="a935b-124">이름</span><span class="sxs-lookup"><span data-stu-id="a935b-124">Name</span></span>     | <span data-ttu-id="a935b-125">입력</span><span class="sxs-lookup"><span data-stu-id="a935b-125">In</span></span>     | <span data-ttu-id="a935b-126">형식</span><span class="sxs-lookup"><span data-stu-id="a935b-126">Type</span></span>    | <span data-ttu-id="a935b-127">필수</span><span class="sxs-lookup"><span data-stu-id="a935b-127">Required</span></span> | <span data-ttu-id="a935b-128">노트</span><span class="sxs-lookup"><span data-stu-id="a935b-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="a935b-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="a935b-129">LOWER_ID</span></span> | <span data-ttu-id="a935b-130">URL</span><span class="sxs-lookup"><span data-stu-id="a935b-130">URL</span></span>    | <span data-ttu-id="a935b-131">string</span><span class="sxs-lookup"><span data-stu-id="a935b-131">string</span></span>  | <span data-ttu-id="a935b-132">예</span><span class="sxs-lookup"><span data-stu-id="a935b-132">yes</span></span>      | <span data-ttu-id="a935b-133">소문자의 패키지 ID</span><span class="sxs-lookup"><span data-stu-id="a935b-133">The package ID, lowercase</span></span>

<span data-ttu-id="a935b-134">`LOWER_ID` 값은 소문자를 유지 하 여 구현 하는 규칙을 사용 하 여 원하는 패키지 ID입니다. NET의 [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) 메서드.</span><span class="sxs-lookup"><span data-stu-id="a935b-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="a935b-135">응답</span><span class="sxs-lookup"><span data-stu-id="a935b-135">Response</span></span>

<span data-ttu-id="a935b-136">패키지 소스에 제공 된 패키지 ID의 버전 없음, 404 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="a935b-137">패키지 원본 하나 또는 여러 버전에 200 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="a935b-138">응답 본문은 다음 속성과 함께 JSON 개체:</span><span class="sxs-lookup"><span data-stu-id="a935b-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="a935b-139">이름</span><span class="sxs-lookup"><span data-stu-id="a935b-139">Name</span></span>     | <span data-ttu-id="a935b-140">형식</span><span class="sxs-lookup"><span data-stu-id="a935b-140">Type</span></span>             | <span data-ttu-id="a935b-141">필수</span><span class="sxs-lookup"><span data-stu-id="a935b-141">Required</span></span> | <span data-ttu-id="a935b-142">노트</span><span class="sxs-lookup"><span data-stu-id="a935b-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="a935b-143">버전</span><span class="sxs-lookup"><span data-stu-id="a935b-143">versions</span></span> | <span data-ttu-id="a935b-144">문자열의 배열</span><span class="sxs-lookup"><span data-stu-id="a935b-144">array of strings</span></span> | <span data-ttu-id="a935b-145">예</span><span class="sxs-lookup"><span data-stu-id="a935b-145">yes</span></span>      | <span data-ttu-id="a935b-146">패키지 Id 제공</span><span class="sxs-lookup"><span data-stu-id="a935b-146">The package IDs available</span></span>

<span data-ttu-id="a935b-147">문자열을 `versions` 배열의 모든 소문자 [NuGet 버전 문자열을 정규화](../reference/package-versioning.md#normalized-version-numbers)합니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="a935b-148">버전 문자열에는 SemVer 2.0.0 빌드 메타 데이터가 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="a935b-149">의도이 배열에서 찾은 버전 문자열에 대 한 정확 하 게 사용할 수 있는지를 `LOWER_VERSION` 다음 끝점에서 토큰을 찾을.</span><span class="sxs-lookup"><span data-stu-id="a935b-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a935b-150">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="a935b-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="a935b-151">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="a935b-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="a935b-152">패키지 콘텐츠 (.nupkg) 다운로드</span><span class="sxs-lookup"><span data-stu-id="a935b-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="a935b-153">클라이언트 패키지 ID 및 버전을 알고 패키지 콘텐츠 다운로드 하려는 경우 다음 URL을 생성 하려면만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="a935b-154">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a935b-154">Request parameters</span></span>

<span data-ttu-id="a935b-155">이름</span><span class="sxs-lookup"><span data-stu-id="a935b-155">Name</span></span>          | <span data-ttu-id="a935b-156">입력</span><span class="sxs-lookup"><span data-stu-id="a935b-156">In</span></span>     | <span data-ttu-id="a935b-157">형식</span><span class="sxs-lookup"><span data-stu-id="a935b-157">Type</span></span>   | <span data-ttu-id="a935b-158">필수</span><span class="sxs-lookup"><span data-stu-id="a935b-158">Required</span></span> | <span data-ttu-id="a935b-159">노트</span><span class="sxs-lookup"><span data-stu-id="a935b-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="a935b-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="a935b-160">LOWER_ID</span></span>      | <span data-ttu-id="a935b-161">URL</span><span class="sxs-lookup"><span data-stu-id="a935b-161">URL</span></span>    | <span data-ttu-id="a935b-162">string</span><span class="sxs-lookup"><span data-stu-id="a935b-162">string</span></span> | <span data-ttu-id="a935b-163">예</span><span class="sxs-lookup"><span data-stu-id="a935b-163">yes</span></span>      | <span data-ttu-id="a935b-164">소문자의 패키지 ID</span><span class="sxs-lookup"><span data-stu-id="a935b-164">The package ID, lowercase</span></span>
<span data-ttu-id="a935b-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="a935b-165">LOWER_VERSION</span></span> | <span data-ttu-id="a935b-166">URL</span><span class="sxs-lookup"><span data-stu-id="a935b-166">URL</span></span>    | <span data-ttu-id="a935b-167">string</span><span class="sxs-lookup"><span data-stu-id="a935b-167">string</span></span> | <span data-ttu-id="a935b-168">예</span><span class="sxs-lookup"><span data-stu-id="a935b-168">yes</span></span>      | <span data-ttu-id="a935b-169">패키지 버전을 표준화 하 고 소문자를 유지</span><span class="sxs-lookup"><span data-stu-id="a935b-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="a935b-170">둘 다 `LOWER_ID` 고 `LOWER_VERSION` 구현한 규칙을 사용 하 여 소문자를 유지 됩니다. NET의 [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="a935b-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="a935b-171">메서드를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-171">method.</span></span>

<span data-ttu-id="a935b-172">합니다 `LOWER_VERSION` 원하는 패키지 버전 정규화 된 NuGet의 버전을 사용 하 여 [정규화 규칙](../reference/package-versioning.md#normalized-version-numbers)합니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="a935b-173">즉, SemVer 2.0.0 사양에서 허용 되는 빌드 메타 데이터는이 경우 제외 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="a935b-174">응답 본문</span><span class="sxs-lookup"><span data-stu-id="a935b-174">Response body</span></span>

<span data-ttu-id="a935b-175">패키지를 패키지 원본에 있는 경우에 200 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="a935b-176">응답 본문에 패키지 콘텐츠 자체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="a935b-177">패키지는 패키지 원본에 없는 경우, 404 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a935b-178">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="a935b-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="a935b-179">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="a935b-179">Sample response</span></span>

<span data-ttu-id="a935b-180">Newtonsoft.Json 9.0.1에 대 한.nupkg 있는 이진 스트림.</span><span class="sxs-lookup"><span data-stu-id="a935b-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="a935b-181">패키지 매니페스트 (.nuspec) 다운로드</span><span class="sxs-lookup"><span data-stu-id="a935b-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="a935b-182">클라이언트 패키지 ID 및 버전을 알고 있습니다. 패키지 매니페스트를 다운로드 하려는 경우 다음 URL을 생성 하려면만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="a935b-183">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="a935b-183">Request parameters</span></span>

<span data-ttu-id="a935b-184">이름</span><span class="sxs-lookup"><span data-stu-id="a935b-184">Name</span></span>          | <span data-ttu-id="a935b-185">입력</span><span class="sxs-lookup"><span data-stu-id="a935b-185">In</span></span>     | <span data-ttu-id="a935b-186">형식</span><span class="sxs-lookup"><span data-stu-id="a935b-186">Type</span></span>    | <span data-ttu-id="a935b-187">필수</span><span class="sxs-lookup"><span data-stu-id="a935b-187">Required</span></span> | <span data-ttu-id="a935b-188">노트</span><span class="sxs-lookup"><span data-stu-id="a935b-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="a935b-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="a935b-189">LOWER_ID</span></span>      | <span data-ttu-id="a935b-190">URL</span><span class="sxs-lookup"><span data-stu-id="a935b-190">URL</span></span>    | <span data-ttu-id="a935b-191">string</span><span class="sxs-lookup"><span data-stu-id="a935b-191">string</span></span>  | <span data-ttu-id="a935b-192">예</span><span class="sxs-lookup"><span data-stu-id="a935b-192">yes</span></span>      | <span data-ttu-id="a935b-193">소문자의 패키지 ID</span><span class="sxs-lookup"><span data-stu-id="a935b-193">The package ID, lowercase</span></span>
<span data-ttu-id="a935b-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="a935b-194">LOWER_VERSION</span></span> | <span data-ttu-id="a935b-195">URL</span><span class="sxs-lookup"><span data-stu-id="a935b-195">URL</span></span>    | <span data-ttu-id="a935b-196">정수</span><span class="sxs-lookup"><span data-stu-id="a935b-196">integer</span></span> | <span data-ttu-id="a935b-197">예</span><span class="sxs-lookup"><span data-stu-id="a935b-197">yes</span></span>      | <span data-ttu-id="a935b-198">패키지 버전을 표준화 하 고 소문자를 유지</span><span class="sxs-lookup"><span data-stu-id="a935b-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="a935b-199">둘 다 `LOWER_ID` 고 `LOWER_VERSION` 구현한 규칙을 사용 하 여 소문자를 유지 됩니다. NET의 [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) 메서드.</span><span class="sxs-lookup"><span data-stu-id="a935b-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="a935b-200">합니다 `LOWER_VERSION` 원하는 패키지 버전 정규화 된 NuGet의 버전을 사용 하 여 [정규화 규칙](../reference/package-versioning.md#normalized-version-numbers)합니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="a935b-201">즉, SemVer 2.0.0 사양에서 허용 되는 빌드 메타 데이터는이 경우 제외 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="a935b-202">응답 본문</span><span class="sxs-lookup"><span data-stu-id="a935b-202">Response body</span></span>

<span data-ttu-id="a935b-203">패키지를 패키지 원본에 있는 경우에 200 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="a935b-204">응답 본문에는 해당.nupkg에 포함 된.nuspec 패키지 매니페스트를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="a935b-205">.Nuspec는 XML 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="a935b-206">패키지는 패키지 원본에 없는 경우, 404 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a935b-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a935b-207">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="a935b-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="a935b-208">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="a935b-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
