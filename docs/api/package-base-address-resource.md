---
title: 패키지 콘텐츠, NuGet API
description: 패키지 기본 주소는 패키지 자체를 인출 하기 위한 간단한 인터페이스입니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8ea03ece635aa06e22032c4fb43ce932dbdf717c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773941"
---
# <a name="package-content"></a><span data-ttu-id="ad322-103">패키지 내용</span><span class="sxs-lookup"><span data-stu-id="ad322-103">Package Content</span></span>

<span data-ttu-id="ad322-104">V3 API를 사용 하 여 임의의 패키지의 콘텐츠 (nupkg 파일)를 인출 하는 URL을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="ad322-105">패키지 콘텐츠를 가져오는 데 사용 되는 리소스는 `PackageBaseAddress` [서비스 인덱스](service-index.md)에 있는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="ad322-106">또한이 리소스는 나열 되거나 나열 되지 않은 패키지의 모든 버전을 검색할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="ad322-107">이 리소스를 일반적으로 "패키지 기본 주소" 또는 "플랫 컨테이너" 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="ad322-108">버전 관리</span><span class="sxs-lookup"><span data-stu-id="ad322-108">Versioning</span></span>

<span data-ttu-id="ad322-109">사용 되는 `@type` 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-109">The following `@type` value is used:</span></span>

<span data-ttu-id="ad322-110">@type 값</span><span class="sxs-lookup"><span data-stu-id="ad322-110">@type value</span></span>              | <span data-ttu-id="ad322-111">메모</span><span class="sxs-lookup"><span data-stu-id="ad322-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="ad322-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="ad322-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="ad322-113">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="ad322-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="ad322-114">기준 URL</span><span class="sxs-lookup"><span data-stu-id="ad322-114">Base URL</span></span>

<span data-ttu-id="ad322-115">다음 Api에 대 한 기준 URL은 `@id` 앞서 언급 한 리소스 값과 연결 된 속성의 값입니다 `@type` .</span><span class="sxs-lookup"><span data-stu-id="ad322-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="ad322-116">다음 문서에서는 자리 표시자 기준 URL `{@id}` 이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="ad322-117">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="ad322-117">HTTP methods</span></span>

<span data-ttu-id="ad322-118">등록 리소스에서 찾은 모든 Url은 HTTP 메서드 및를 지원 합니다 `GET` `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="ad322-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="ad322-119">패키지 버전 열거</span><span class="sxs-lookup"><span data-stu-id="ad322-119">Enumerate package versions</span></span>

<span data-ttu-id="ad322-120">클라이언트에서 패키지 ID를 알고 있고 패키지 원본에서 사용할 수 있는 패키지 버전을 검색 하려는 경우 클라이언트는 예측 가능한 URL을 생성 하 여 모든 패키지 버전을 열거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="ad322-121">이 목록은 아래에 설명 된 패키지 콘텐츠 API에 대 한 "디렉터리 목록"입니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="ad322-122">이 목록에는 나열 되거나 나열 되지 않은 패키지 버전이 모두 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-122">This list contains both listed and unlisted package versions.</span></span>

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a><span data-ttu-id="ad322-123">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="ad322-123">Request parameters</span></span>

<span data-ttu-id="ad322-124">Name</span><span class="sxs-lookup"><span data-stu-id="ad322-124">Name</span></span>     | <span data-ttu-id="ad322-125">In(다음 안에)</span><span class="sxs-lookup"><span data-stu-id="ad322-125">In</span></span>     | <span data-ttu-id="ad322-126">Type</span><span class="sxs-lookup"><span data-stu-id="ad322-126">Type</span></span>    | <span data-ttu-id="ad322-127">필수</span><span class="sxs-lookup"><span data-stu-id="ad322-127">Required</span></span> | <span data-ttu-id="ad322-128">메모</span><span class="sxs-lookup"><span data-stu-id="ad322-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="ad322-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="ad322-129">LOWER_ID</span></span> | <span data-ttu-id="ad322-130">URL</span><span class="sxs-lookup"><span data-stu-id="ad322-130">URL</span></span>    | <span data-ttu-id="ad322-131">문자열</span><span class="sxs-lookup"><span data-stu-id="ad322-131">string</span></span>  | <span data-ttu-id="ad322-132">예</span><span class="sxs-lookup"><span data-stu-id="ad322-132">yes</span></span>      | <span data-ttu-id="ad322-133">패키지 ID, lowercased</span><span class="sxs-lookup"><span data-stu-id="ad322-133">The package ID, lowercased</span></span>

<span data-ttu-id="ad322-134">값은에 `LOWER_ID` 의해 구현 된 규칙을 사용 하 여 원하는 패키지 ID lowercased. NET의 [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) method.</span></span>

### <a name="response"></a><span data-ttu-id="ad322-135">응답</span><span class="sxs-lookup"><span data-stu-id="ad322-135">Response</span></span>

<span data-ttu-id="ad322-136">패키지 원본에 제공 된 패키지 ID 버전이 없으면 404 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="ad322-137">패키지 원본에 하나 이상의 버전이 있는 경우 200 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="ad322-138">응답 본문은 다음 속성을 포함 하는 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="ad322-139">Name</span><span class="sxs-lookup"><span data-stu-id="ad322-139">Name</span></span>     | <span data-ttu-id="ad322-140">Type</span><span class="sxs-lookup"><span data-stu-id="ad322-140">Type</span></span>             | <span data-ttu-id="ad322-141">필수</span><span class="sxs-lookup"><span data-stu-id="ad322-141">Required</span></span> | <span data-ttu-id="ad322-142">메모</span><span class="sxs-lookup"><span data-stu-id="ad322-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="ad322-143">versions</span><span class="sxs-lookup"><span data-stu-id="ad322-143">versions</span></span> | <span data-ttu-id="ad322-144">문자열 배열</span><span class="sxs-lookup"><span data-stu-id="ad322-144">array of strings</span></span> | <span data-ttu-id="ad322-145">예</span><span class="sxs-lookup"><span data-stu-id="ad322-145">yes</span></span>      | <span data-ttu-id="ad322-146">사용 가능한 버전</span><span class="sxs-lookup"><span data-stu-id="ad322-146">The versions available</span></span>

<span data-ttu-id="ad322-147">배열의 문자열은 `versions` [정규화 된 NuGet 버전 문자열](../concepts/package-versioning.md#normalized-version-numbers)lowercased입니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="ad322-148">버전 문자열에는 SemVer 2.0.0 build 메타 데이터가 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="ad322-149">이 배열에 있는 버전 문자열을 다음 끝점에 있는 토큰에 대해 약어를 사용 하 여 사용할 수 있습니다 `LOWER_VERSION` .</span><span class="sxs-lookup"><span data-stu-id="ad322-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="ad322-150">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="ad322-150">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a><span data-ttu-id="ad322-151">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="ad322-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="ad322-152">패키지 콘텐츠 다운로드 (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="ad322-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="ad322-153">클라이언트에서 패키지 ID 및 버전을 인식 하 고 패키지 콘텐츠를 다운로드 하려는 경우 다음 URL을 생성 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a><span data-ttu-id="ad322-154">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="ad322-154">Request parameters</span></span>

<span data-ttu-id="ad322-155">Name</span><span class="sxs-lookup"><span data-stu-id="ad322-155">Name</span></span>          | <span data-ttu-id="ad322-156">In(다음 안에)</span><span class="sxs-lookup"><span data-stu-id="ad322-156">In</span></span>     | <span data-ttu-id="ad322-157">Type</span><span class="sxs-lookup"><span data-stu-id="ad322-157">Type</span></span>   | <span data-ttu-id="ad322-158">필수</span><span class="sxs-lookup"><span data-stu-id="ad322-158">Required</span></span> | <span data-ttu-id="ad322-159">메모</span><span class="sxs-lookup"><span data-stu-id="ad322-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="ad322-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="ad322-160">LOWER_ID</span></span>      | <span data-ttu-id="ad322-161">URL</span><span class="sxs-lookup"><span data-stu-id="ad322-161">URL</span></span>    | <span data-ttu-id="ad322-162">문자열</span><span class="sxs-lookup"><span data-stu-id="ad322-162">string</span></span> | <span data-ttu-id="ad322-163">예</span><span class="sxs-lookup"><span data-stu-id="ad322-163">yes</span></span>      | <span data-ttu-id="ad322-164">패키지 ID, 소문자</span><span class="sxs-lookup"><span data-stu-id="ad322-164">The package ID, lowercase</span></span>
<span data-ttu-id="ad322-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="ad322-165">LOWER_VERSION</span></span> | <span data-ttu-id="ad322-166">URL</span><span class="sxs-lookup"><span data-stu-id="ad322-166">URL</span></span>    | <span data-ttu-id="ad322-167">문자열</span><span class="sxs-lookup"><span data-stu-id="ad322-167">string</span></span> | <span data-ttu-id="ad322-168">예</span><span class="sxs-lookup"><span data-stu-id="ad322-168">yes</span></span>      | <span data-ttu-id="ad322-169">패키지 버전, 정규화 및 lowercased</span><span class="sxs-lookup"><span data-stu-id="ad322-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="ad322-170">`LOWER_ID`및 `LOWER_VERSION` 는 모두에서 구현 된 규칙을 사용 하 여 lowercased 됩니다. 네트워크[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ad322-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)</span></span>
<span data-ttu-id="ad322-171">메서드를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-171">method.</span></span>

<span data-ttu-id="ad322-172">는 `LOWER_VERSION` NuGet의 버전 [정규화 규칙](../concepts/package-versioning.md#normalized-version-numbers)을 사용 하 여 정규화 된 패키지 버전을 정규화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="ad322-173">즉,이 경우 SemVer 2.0.0 사양에서 허용 하는 빌드 메타 데이터를 제외 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="ad322-174">응답 본문</span><span class="sxs-lookup"><span data-stu-id="ad322-174">Response body</span></span>

<span data-ttu-id="ad322-175">패키지가 패키지 원본에 있으면 200 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="ad322-176">응답 본문은 패키지 콘텐츠 자체가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="ad322-177">패키지가 패키지 원본에 없으면 404 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="ad322-178">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="ad322-178">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a><span data-ttu-id="ad322-179">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="ad322-179">Sample response</span></span>

<span data-ttu-id="ad322-180">9.0.1의 Newtonsoft.Js에 대 한 nupkg 이진 스트림입니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="ad322-181">패키지 매니페스트 (. nuspec) 다운로드</span><span class="sxs-lookup"><span data-stu-id="ad322-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="ad322-182">클라이언트에서 패키지 ID 및 버전을 인식 하 고 패키지 매니페스트를 다운로드 하려는 경우 다음 URL을 생성 하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a><span data-ttu-id="ad322-183">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="ad322-183">Request parameters</span></span>

<span data-ttu-id="ad322-184">Name</span><span class="sxs-lookup"><span data-stu-id="ad322-184">Name</span></span>          | <span data-ttu-id="ad322-185">In(다음 안에)</span><span class="sxs-lookup"><span data-stu-id="ad322-185">In</span></span>     | <span data-ttu-id="ad322-186">Type</span><span class="sxs-lookup"><span data-stu-id="ad322-186">Type</span></span>   | <span data-ttu-id="ad322-187">필수</span><span class="sxs-lookup"><span data-stu-id="ad322-187">Required</span></span> | <span data-ttu-id="ad322-188">메모</span><span class="sxs-lookup"><span data-stu-id="ad322-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="ad322-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="ad322-189">LOWER_ID</span></span>      | <span data-ttu-id="ad322-190">URL</span><span class="sxs-lookup"><span data-stu-id="ad322-190">URL</span></span>    | <span data-ttu-id="ad322-191">문자열</span><span class="sxs-lookup"><span data-stu-id="ad322-191">string</span></span> | <span data-ttu-id="ad322-192">예</span><span class="sxs-lookup"><span data-stu-id="ad322-192">yes</span></span>      | <span data-ttu-id="ad322-193">패키지 ID, 소문자</span><span class="sxs-lookup"><span data-stu-id="ad322-193">The package ID, lowercase</span></span>
<span data-ttu-id="ad322-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="ad322-194">LOWER_VERSION</span></span> | <span data-ttu-id="ad322-195">URL</span><span class="sxs-lookup"><span data-stu-id="ad322-195">URL</span></span>    | <span data-ttu-id="ad322-196">문자열</span><span class="sxs-lookup"><span data-stu-id="ad322-196">string</span></span> | <span data-ttu-id="ad322-197">예</span><span class="sxs-lookup"><span data-stu-id="ad322-197">yes</span></span>      | <span data-ttu-id="ad322-198">패키지 버전, 정규화 및 lowercased</span><span class="sxs-lookup"><span data-stu-id="ad322-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="ad322-199">`LOWER_ID`및 `LOWER_VERSION` 는 모두에서 구현 된 규칙을 사용 하 여 lowercased 됩니다. NET의 [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) method.</span></span>

<span data-ttu-id="ad322-200">는 `LOWER_VERSION` NuGet의 버전 [정규화 규칙](../concepts/package-versioning.md#normalized-version-numbers)을 사용 하 여 정규화 된 패키지 버전을 정규화 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="ad322-201">즉,이 경우 SemVer 2.0.0 사양에서 허용 하는 빌드 메타 데이터를 제외 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="ad322-202">응답 본문</span><span class="sxs-lookup"><span data-stu-id="ad322-202">Response body</span></span>

<span data-ttu-id="ad322-203">패키지가 패키지 원본에 있으면 200 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="ad322-204">응답 본문은 해당. nupkg에 포함 된 nuspec 패키지 매니페스트입니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="ad322-205">. Nuspec은 XML 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="ad322-206">패키지가 패키지 원본에 없으면 404 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ad322-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="ad322-207">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="ad322-207">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a><span data-ttu-id="ad322-208">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="ad322-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
