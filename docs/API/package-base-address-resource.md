---
title: "패키지 콘텐츠를 NuGet API | Microsoft Docs"
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
description: "패키지의 기본 주소는 패키지 자체를 가져오기 위해 간단한 인터페이스입니다."
keywords: "컨테이너, NuGet 패키지에 대 한 기본 주소, NuGet nupkg API NuGet API 패키지 버전 NuGet API NuGet 플랫 목록에 없는 패키지, 다운로드 nuspec NuGet API"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c2e631dc0bba95ac849430d77142f27ef591f741
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="package-content"></a><span data-ttu-id="22dbd-104">패키지 내용</span><span class="sxs-lookup"><span data-stu-id="22dbd-104">Package Content</span></span>

<span data-ttu-id="22dbd-105">V3 API를 사용 하는 임의의 패키지의 콘텐츠 (.nupkg 파일)를 인출 하는 URL을 생성 하는 것이 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-105">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="22dbd-106">패키지 콘텐츠를 가져오기 위해 사용 되는 리소스는는 `PackageBaseAddress` 에서 리소스를 찾을 [서비스 인덱스](service-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-106">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="22dbd-107">이 리소스에도 모든 버전의 나열 된 패키지를 검색할 수 있도록 또는 목록에 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-107">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="22dbd-108">이 리소스는 일반적으로 라고 "패키지 기본 주소가" 또는 "플랫 컨테이너" 합니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-108">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="22dbd-109">버전 관리</span><span class="sxs-lookup"><span data-stu-id="22dbd-109">Versioning</span></span>

<span data-ttu-id="22dbd-110">다음 `@type` 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-110">The following `@type` value is used:</span></span>

<span data-ttu-id="22dbd-111">@type 값</span><span class="sxs-lookup"><span data-stu-id="22dbd-111">@type value</span></span>              | <span data-ttu-id="22dbd-112">노트</span><span class="sxs-lookup"><span data-stu-id="22dbd-112">Notes</span></span>
------------------------ | -----
<span data-ttu-id="22dbd-113">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="22dbd-113">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="22dbd-114">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="22dbd-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="22dbd-115">기준 URL</span><span class="sxs-lookup"><span data-stu-id="22dbd-115">Base URL</span></span>

<span data-ttu-id="22dbd-116">다음 Api에 대 한 기본 URL의 값은 고 `@id` 앞에서 언급 한 리소스와 연결 된 속성 `@type` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-116">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="22dbd-117">다음 문서에서 자리 표시자 기준 URL `{@id}` 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-117">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="22dbd-118">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="22dbd-118">HTTP methods</span></span>

<span data-ttu-id="22dbd-119">HTTP 메서드를 등록 리소스 지원에 있는 모든 Url `GET` 및 `HEAD`합니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-119">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="22dbd-120">패키지 버전을 열거 합니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-120">Enumerate package versions</span></span>

<span data-ttu-id="22dbd-121">클라이언트는 패키지 ID를 알고 있는 패키지 버전의 패키지를 검색 하려는 경우 원본에 사용할 수 있는, 클라이언트가 모든 패키지 버전을 열거 하는 예측 가능한 URL을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-121">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="22dbd-122">이 목록은 사용할 계획이 "디렉터리 목록" 아래에 언급 된 패키지 콘텐츠 API에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-122">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="22dbd-123">이 목록에 나열 된 및 목록에 없는 패키지 버전을 모두 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-123">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="22dbd-124">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="22dbd-124">Request parameters</span></span>

<span data-ttu-id="22dbd-125">name</span><span class="sxs-lookup"><span data-stu-id="22dbd-125">Name</span></span>     | <span data-ttu-id="22dbd-126">입력</span><span class="sxs-lookup"><span data-stu-id="22dbd-126">In</span></span>     | <span data-ttu-id="22dbd-127">형식</span><span class="sxs-lookup"><span data-stu-id="22dbd-127">Type</span></span>    | <span data-ttu-id="22dbd-128">필수</span><span class="sxs-lookup"><span data-stu-id="22dbd-128">Required</span></span> | <span data-ttu-id="22dbd-129">노트</span><span class="sxs-lookup"><span data-stu-id="22dbd-129">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="22dbd-130">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="22dbd-130">LOWER_ID</span></span> | <span data-ttu-id="22dbd-131">URL</span><span class="sxs-lookup"><span data-stu-id="22dbd-131">URL</span></span>    | <span data-ttu-id="22dbd-132">string</span><span class="sxs-lookup"><span data-stu-id="22dbd-132">string</span></span>  | <span data-ttu-id="22dbd-133">예</span><span class="sxs-lookup"><span data-stu-id="22dbd-133">yes</span></span>      | <span data-ttu-id="22dbd-134">패키지 ID, 소문자</span><span class="sxs-lookup"><span data-stu-id="22dbd-134">The package ID, lowercase</span></span>

<span data-ttu-id="22dbd-135">`LOWER_ID` 값은 소문자를 유지 하 여 구현 하는 규칙을 사용 하 여 원하는 패키지 ID입니다. NET의 [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) 메서드.</span><span class="sxs-lookup"><span data-stu-id="22dbd-135">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="22dbd-136">응답</span><span class="sxs-lookup"><span data-stu-id="22dbd-136">Response</span></span>

<span data-ttu-id="22dbd-137">패키지 소스가 제공 된 패키지 ID의 버전을 가진 경우에 404 상태 코드 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-137">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="22dbd-138">패키지 소스가 하나 이상의 버전을 가진 경우에 200 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-138">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="22dbd-139">응답 본문은 다음과 같은 속성이 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-139">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="22dbd-140">name</span><span class="sxs-lookup"><span data-stu-id="22dbd-140">Name</span></span>     | <span data-ttu-id="22dbd-141">형식</span><span class="sxs-lookup"><span data-stu-id="22dbd-141">Type</span></span>             | <span data-ttu-id="22dbd-142">필수</span><span class="sxs-lookup"><span data-stu-id="22dbd-142">Required</span></span> | <span data-ttu-id="22dbd-143">노트</span><span class="sxs-lookup"><span data-stu-id="22dbd-143">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="22dbd-144">버전</span><span class="sxs-lookup"><span data-stu-id="22dbd-144">versions</span></span> | <span data-ttu-id="22dbd-145">문자열의 배열</span><span class="sxs-lookup"><span data-stu-id="22dbd-145">array of strings</span></span> | <span data-ttu-id="22dbd-146">예</span><span class="sxs-lookup"><span data-stu-id="22dbd-146">yes</span></span>      | <span data-ttu-id="22dbd-147">패키지 Id 제공</span><span class="sxs-lookup"><span data-stu-id="22dbd-147">The package IDs available</span></span>

<span data-ttu-id="22dbd-148">문자열은 `versions` 배열 모두 소문자 [NuGet 버전 문자열 정규화](../reference/package-versioning.md#normalized-version-numbers)합니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-148">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="22dbd-149">버전 문자열 SemVer 2.0.0 빌드 메타 데이터가 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-149">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="22dbd-150">이 배열에 버전 문자열에 대 한 정확 하 게 사용할 수 있는지는 `LOWER_VERSION` 다음 끝점에 있는 토큰이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-150">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="22dbd-151">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="22dbd-151">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="22dbd-152">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="22dbd-152">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="22dbd-153">패키지 콘텐츠 (.nupkg) 다운로드</span><span class="sxs-lookup"><span data-stu-id="22dbd-153">Download package content (.nupkg)</span></span>

<span data-ttu-id="22dbd-154">클라이언트 패키지 ID와 버전을 알고 있는 패키지 콘텐츠 다운로드 하려는 경우 다음 URL을 생성할만 필요:</span><span class="sxs-lookup"><span data-stu-id="22dbd-154">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="22dbd-155">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="22dbd-155">Request parameters</span></span>

<span data-ttu-id="22dbd-156">name</span><span class="sxs-lookup"><span data-stu-id="22dbd-156">Name</span></span>          | <span data-ttu-id="22dbd-157">입력</span><span class="sxs-lookup"><span data-stu-id="22dbd-157">In</span></span>     | <span data-ttu-id="22dbd-158">형식</span><span class="sxs-lookup"><span data-stu-id="22dbd-158">Type</span></span>   | <span data-ttu-id="22dbd-159">필수</span><span class="sxs-lookup"><span data-stu-id="22dbd-159">Required</span></span> | <span data-ttu-id="22dbd-160">노트</span><span class="sxs-lookup"><span data-stu-id="22dbd-160">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="22dbd-161">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="22dbd-161">LOWER_ID</span></span>      | <span data-ttu-id="22dbd-162">URL</span><span class="sxs-lookup"><span data-stu-id="22dbd-162">URL</span></span>    | <span data-ttu-id="22dbd-163">string</span><span class="sxs-lookup"><span data-stu-id="22dbd-163">string</span></span> | <span data-ttu-id="22dbd-164">예</span><span class="sxs-lookup"><span data-stu-id="22dbd-164">yes</span></span>      | <span data-ttu-id="22dbd-165">패키지 ID, 소문자</span><span class="sxs-lookup"><span data-stu-id="22dbd-165">The package ID, lowercase</span></span>
<span data-ttu-id="22dbd-166">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="22dbd-166">LOWER_VERSION</span></span> | <span data-ttu-id="22dbd-167">URL</span><span class="sxs-lookup"><span data-stu-id="22dbd-167">URL</span></span>    | <span data-ttu-id="22dbd-168">string</span><span class="sxs-lookup"><span data-stu-id="22dbd-168">string</span></span> | <span data-ttu-id="22dbd-169">예</span><span class="sxs-lookup"><span data-stu-id="22dbd-169">yes</span></span>      | <span data-ttu-id="22dbd-170">소문자를 유지 하 고 정규화 된 패키지 버전</span><span class="sxs-lookup"><span data-stu-id="22dbd-170">The package version, normalized and lowercased</span></span>

<span data-ttu-id="22dbd-171">둘 다 `LOWER_ID` 및 `LOWER_VERSION` 하 여 구현 하는 규칙을 사용 하 여 소문자를 유지 됩니다. NET의 [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) 메서드.</span><span class="sxs-lookup"><span data-stu-id="22dbd-171">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="22dbd-172">`LOWER_VERSION` 원하는 패키지 버전 정규화 된 NuGet의 버전을 사용 하 여 [정규화 규칙](../reference/package-versioning.md#normalized-version-numbers)합니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="22dbd-173">즉, SemVer 2.0.0 사양에서 허용 되는 빌드 메타 데이터를이 경우 제외 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="22dbd-174">응답 본문</span><span class="sxs-lookup"><span data-stu-id="22dbd-174">Response body</span></span>

<span data-ttu-id="22dbd-175">패키지는 패키지 원본에 있는 경우에 200 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="22dbd-176">응답 본문에 패키지 콘텐츠 자체 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="22dbd-177">패키지는 패키지 원본에 없는 경우에 404 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="22dbd-178">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="22dbd-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="22dbd-179">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="22dbd-179">Sample response</span></span>

<span data-ttu-id="22dbd-180">Newtonsoft.Json 9.0.1에 대 한.nupkg 있는 이진 스트림.</span><span class="sxs-lookup"><span data-stu-id="22dbd-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="22dbd-181">패키지 매니페스트 (.nuspec) 다운로드</span><span class="sxs-lookup"><span data-stu-id="22dbd-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="22dbd-182">클라이언트 패키지 ID와 버전을 알고 있는 패키지 매니페스트를 다운로드 하는 경우 다음 URL을 생성할만 필요:</span><span class="sxs-lookup"><span data-stu-id="22dbd-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="22dbd-183">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="22dbd-183">Request parameters</span></span>

<span data-ttu-id="22dbd-184">name</span><span class="sxs-lookup"><span data-stu-id="22dbd-184">Name</span></span>          | <span data-ttu-id="22dbd-185">입력</span><span class="sxs-lookup"><span data-stu-id="22dbd-185">In</span></span>     | <span data-ttu-id="22dbd-186">형식</span><span class="sxs-lookup"><span data-stu-id="22dbd-186">Type</span></span>    | <span data-ttu-id="22dbd-187">필수</span><span class="sxs-lookup"><span data-stu-id="22dbd-187">Required</span></span> | <span data-ttu-id="22dbd-188">노트</span><span class="sxs-lookup"><span data-stu-id="22dbd-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="22dbd-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="22dbd-189">LOWER_ID</span></span>      | <span data-ttu-id="22dbd-190">URL</span><span class="sxs-lookup"><span data-stu-id="22dbd-190">URL</span></span>    | <span data-ttu-id="22dbd-191">string</span><span class="sxs-lookup"><span data-stu-id="22dbd-191">string</span></span>  | <span data-ttu-id="22dbd-192">예</span><span class="sxs-lookup"><span data-stu-id="22dbd-192">yes</span></span>      | <span data-ttu-id="22dbd-193">패키지 ID, 소문자</span><span class="sxs-lookup"><span data-stu-id="22dbd-193">The package ID, lowercase</span></span>
<span data-ttu-id="22dbd-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="22dbd-194">LOWER_VERSION</span></span> | <span data-ttu-id="22dbd-195">URL</span><span class="sxs-lookup"><span data-stu-id="22dbd-195">URL</span></span>    | <span data-ttu-id="22dbd-196">정수</span><span class="sxs-lookup"><span data-stu-id="22dbd-196">integer</span></span> | <span data-ttu-id="22dbd-197">예</span><span class="sxs-lookup"><span data-stu-id="22dbd-197">yes</span></span>      | <span data-ttu-id="22dbd-198">소문자를 유지 하 고 정규화 된 패키지 버전</span><span class="sxs-lookup"><span data-stu-id="22dbd-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="22dbd-199">둘 다 `LOWER_ID` 및 `LOWER_VERSION` 하 여 구현 하는 규칙을 사용 하 여 소문자를 유지 됩니다. NET의 [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) 메서드.</span><span class="sxs-lookup"><span data-stu-id="22dbd-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="22dbd-200">`LOWER_VERSION` 원하는 패키지 버전 정규화 된 NuGet의 버전을 사용 하 여 [정규화 규칙](../reference/package-versioning.md#normalized-version-numbers)합니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="22dbd-201">즉, SemVer 2.0.0 사양에서 허용 되는 빌드 메타 데이터를이 경우 제외 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="22dbd-202">응답 본문</span><span class="sxs-lookup"><span data-stu-id="22dbd-202">Response body</span></span>

<span data-ttu-id="22dbd-203">패키지는 패키지 원본에 있는 경우에 200 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="22dbd-204">응답 본문에는 해당.nupkg에 포함 된.nuspec 패키지 매니페스트를 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="22dbd-205">.nuspec XML 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="22dbd-206">패키지는 패키지 원본에 없는 경우에 404 상태 코드가 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="22dbd-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="22dbd-207">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="22dbd-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="22dbd-208">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="22dbd-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
