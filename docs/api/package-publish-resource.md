---
title: 밀어넣기 및 삭제, NuGet API
description: 게시 서비스를 사용 하면 클라이언트가 새 패키지를 게시 하 고 기존 패키지를 목록에서 삭제 하거나 삭제할 수 있습니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773924"
---
# <a name="push-and-delete"></a><span data-ttu-id="5743b-103">밀어넣기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="5743b-103">Push and Delete</span></span>

<span data-ttu-id="5743b-104">서버 구현에 따라 푸시, 삭제 또는 나열을 취소할 수 있으며 NuGet V3 API를 사용 하 여 패키지를 다시 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="5743b-105">이러한 작업은 `PackagePublish` [서비스 인덱스](service-index.md)에 있는 리소스를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="5743b-106">버전 관리</span><span class="sxs-lookup"><span data-stu-id="5743b-106">Versioning</span></span>

<span data-ttu-id="5743b-107">사용 되는 `@type` 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-107">The following `@type` value is used:</span></span>

<span data-ttu-id="5743b-108">@type 값</span><span class="sxs-lookup"><span data-stu-id="5743b-108">@type value</span></span>          | <span data-ttu-id="5743b-109">메모</span><span class="sxs-lookup"><span data-stu-id="5743b-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="5743b-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="5743b-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="5743b-111">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="5743b-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="5743b-112">기준 URL</span><span class="sxs-lookup"><span data-stu-id="5743b-112">Base URL</span></span>

<span data-ttu-id="5743b-113">다음 Api에 대 한 기준 URL은 `@id` `PackagePublish/2.0.0` 패키지 소스의 [서비스 인덱스](service-index.md)에 있는 리소스의 속성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="5743b-114">아래 설명서의 경우에는 nuget.exe의 URL이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="5743b-115">`https://www.nuget.org/api/v2/package`서비스 인덱스에 있는 값에 대 한 자리 표시자로 간주 `@id` 합니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="5743b-116">이 URL은 프로토콜이 동일 하기 때문에 레거시 V2 push 끝점과 동일한 위치를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="5743b-117">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="5743b-117">HTTP methods</span></span>

<span data-ttu-id="5743b-118">`PUT`, `POST` 및 `DELETE` HTTP 메서드는이 리소스에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="5743b-119">각 끝점에서 지원 되는 메서드는 아래를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5743b-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="5743b-120">패키지 푸시</span><span class="sxs-lookup"><span data-stu-id="5743b-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="5743b-121">nuget.org에는 푸시 끝점과 상호 작용 하기 위한 [추가 요구 사항이](NuGet-Protocols.md) 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="5743b-122">nuget.org은 다음 API를 사용 하 여 새 패키지를 푸시하는 것을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="5743b-123">제공 된 ID와 버전이 있는 패키지가 이미 있는 경우 nuget.org은 푸시를 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="5743b-124">다른 패키지 원본은 기존 패키지를 바꾸는 것을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="5743b-125">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="5743b-125">Request parameters</span></span>

<span data-ttu-id="5743b-126">Name</span><span class="sxs-lookup"><span data-stu-id="5743b-126">Name</span></span>           | <span data-ttu-id="5743b-127">In(다음 안에)</span><span class="sxs-lookup"><span data-stu-id="5743b-127">In</span></span>     | <span data-ttu-id="5743b-128">Type</span><span class="sxs-lookup"><span data-stu-id="5743b-128">Type</span></span>   | <span data-ttu-id="5743b-129">필수</span><span class="sxs-lookup"><span data-stu-id="5743b-129">Required</span></span> | <span data-ttu-id="5743b-130">메모</span><span class="sxs-lookup"><span data-stu-id="5743b-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="5743b-131">X NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="5743b-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="5743b-132">헤더</span><span class="sxs-lookup"><span data-stu-id="5743b-132">Header</span></span> | <span data-ttu-id="5743b-133">문자열</span><span class="sxs-lookup"><span data-stu-id="5743b-133">string</span></span> | <span data-ttu-id="5743b-134">예</span><span class="sxs-lookup"><span data-stu-id="5743b-134">yes</span></span>      | <span data-ttu-id="5743b-135">예를 들어 `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="5743b-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="5743b-136">API 키는 사용자가 패키지 원본에서 가져온 불투명 문자열이 며 클라이언트에 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="5743b-137">특정 문자열 형식은 지정 되지 않지만 API 키의 길이는 HTTP 헤더 값에 대 한 적절 한 크기를 초과 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="5743b-138">요청 본문</span><span class="sxs-lookup"><span data-stu-id="5743b-138">Request body</span></span>

<span data-ttu-id="5743b-139">요청 본문은 다음과 같은 형식으로 제공 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="5743b-140">다중 파트 폼 데이터</span><span class="sxs-lookup"><span data-stu-id="5743b-140">Multipart form data</span></span>

<span data-ttu-id="5743b-141">요청 헤더는 `Content-Type` 이 `multipart/form-data` 고 요청 본문의 첫 번째 항목은 푸시되는 nupkg의 원시 바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="5743b-142">Multipart 본문의 후속 항목은 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="5743b-143">파일 이름 또는 multipart 항목의 다른 헤더는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="5743b-144">응답</span><span class="sxs-lookup"><span data-stu-id="5743b-144">Response</span></span>

<span data-ttu-id="5743b-145">상태 코드</span><span class="sxs-lookup"><span data-stu-id="5743b-145">Status Code</span></span> | <span data-ttu-id="5743b-146">의미</span><span class="sxs-lookup"><span data-stu-id="5743b-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="5743b-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="5743b-147">201, 202</span></span>    | <span data-ttu-id="5743b-148">패키지를 푸시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-148">The package was successfully pushed</span></span>
<span data-ttu-id="5743b-149">400</span><span class="sxs-lookup"><span data-stu-id="5743b-149">400</span></span>         | <span data-ttu-id="5743b-150">제공 된 패키지가 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-150">The provided package is invalid</span></span>
<span data-ttu-id="5743b-151">409</span><span class="sxs-lookup"><span data-stu-id="5743b-151">409</span></span>         | <span data-ttu-id="5743b-152">제공 된 ID 및 버전의 패키지가 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="5743b-153">서버 구현은 패키지가 성공적으로 푸시되는 경우 반환 되는 성공 상태 코드에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="5743b-154">패키지 삭제</span><span class="sxs-lookup"><span data-stu-id="5743b-154">Delete a package</span></span>

<span data-ttu-id="5743b-155">nuget.org는 패키지 삭제 요청을 "unlist"로 해석 합니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="5743b-156">즉, 패키지를 기존 소비자에 게 계속 사용할 수 있지만 패키지가 검색 결과 나 웹 인터페이스에 더 이상 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="5743b-157">이 방법에 대 한 자세한 내용은 삭제 된 [패키지](../nuget-org/policies/deleting-packages.md) 정책을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="5743b-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="5743b-158">다른 서버 구현에서는이 신호를 하드 삭제, 일시 삭제 또는 unlist로 자유롭게 해석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="5743b-159">예를 들어, [NuGet. 서버](https://www.nuget.org/packages/NuGet.Server) (이전 V2 API를 지 원하는 서버 구현)는 구성 옵션에 따라이 요청을 나열 취소 또는 hard delete로 처리 하는 것을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="5743b-160">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="5743b-160">Request parameters</span></span>

<span data-ttu-id="5743b-161">Name</span><span class="sxs-lookup"><span data-stu-id="5743b-161">Name</span></span>           | <span data-ttu-id="5743b-162">In(다음 안에)</span><span class="sxs-lookup"><span data-stu-id="5743b-162">In</span></span>     | <span data-ttu-id="5743b-163">Type</span><span class="sxs-lookup"><span data-stu-id="5743b-163">Type</span></span>   | <span data-ttu-id="5743b-164">필수</span><span class="sxs-lookup"><span data-stu-id="5743b-164">Required</span></span> | <span data-ttu-id="5743b-165">메모</span><span class="sxs-lookup"><span data-stu-id="5743b-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="5743b-166">ID</span><span class="sxs-lookup"><span data-stu-id="5743b-166">ID</span></span>             | <span data-ttu-id="5743b-167">URL</span><span class="sxs-lookup"><span data-stu-id="5743b-167">URL</span></span>    | <span data-ttu-id="5743b-168">문자열</span><span class="sxs-lookup"><span data-stu-id="5743b-168">string</span></span> | <span data-ttu-id="5743b-169">예</span><span class="sxs-lookup"><span data-stu-id="5743b-169">yes</span></span>      | <span data-ttu-id="5743b-170">삭제할 패키지의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-170">The ID of the package to delete</span></span>
<span data-ttu-id="5743b-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="5743b-171">VERSION</span></span>        | <span data-ttu-id="5743b-172">URL</span><span class="sxs-lookup"><span data-stu-id="5743b-172">URL</span></span>    | <span data-ttu-id="5743b-173">문자열</span><span class="sxs-lookup"><span data-stu-id="5743b-173">string</span></span> | <span data-ttu-id="5743b-174">예</span><span class="sxs-lookup"><span data-stu-id="5743b-174">yes</span></span>      | <span data-ttu-id="5743b-175">삭제할 패키지의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-175">The version of the package to delete</span></span>
<span data-ttu-id="5743b-176">X NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="5743b-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="5743b-177">헤더</span><span class="sxs-lookup"><span data-stu-id="5743b-177">Header</span></span> | <span data-ttu-id="5743b-178">문자열</span><span class="sxs-lookup"><span data-stu-id="5743b-178">string</span></span> | <span data-ttu-id="5743b-179">예</span><span class="sxs-lookup"><span data-stu-id="5743b-179">yes</span></span>      | <span data-ttu-id="5743b-180">예를 들어 `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="5743b-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="5743b-181">응답</span><span class="sxs-lookup"><span data-stu-id="5743b-181">Response</span></span>

<span data-ttu-id="5743b-182">상태 코드</span><span class="sxs-lookup"><span data-stu-id="5743b-182">Status Code</span></span> | <span data-ttu-id="5743b-183">의미</span><span class="sxs-lookup"><span data-stu-id="5743b-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="5743b-184">204</span><span class="sxs-lookup"><span data-stu-id="5743b-184">204</span></span>         | <span data-ttu-id="5743b-185">패키지가 삭제 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-185">The package was deleted</span></span>
<span data-ttu-id="5743b-186">404</span><span class="sxs-lookup"><span data-stu-id="5743b-186">404</span></span>         | <span data-ttu-id="5743b-187">제공 된 `ID` 및가 있는 패키지가 없습니다. `VERSION`</span><span class="sxs-lookup"><span data-stu-id="5743b-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="5743b-188">패키지 다시 나열</span><span class="sxs-lookup"><span data-stu-id="5743b-188">Relist a package</span></span>

<span data-ttu-id="5743b-189">패키지가 나열 되지 않은 경우 "relist" 끝점을 사용 하 여 검색 결과에 해당 패키지를 다시 한 번 표시 하 게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="5743b-190">이 끝점은 [delete (unlist) 끝점과](#delete-a-package) 동일한 셰이프를 갖지만 `POST` 메서드 대신 HTTP 메서드를 사용 합니다 `DELETE` .</span><span class="sxs-lookup"><span data-stu-id="5743b-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="5743b-191">패키지가 이미 나열 되어 있으면 여전히 요청이 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-191">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="5743b-192">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="5743b-192">Request parameters</span></span>

<span data-ttu-id="5743b-193">Name</span><span class="sxs-lookup"><span data-stu-id="5743b-193">Name</span></span>           | <span data-ttu-id="5743b-194">In(다음 안에)</span><span class="sxs-lookup"><span data-stu-id="5743b-194">In</span></span>     | <span data-ttu-id="5743b-195">Type</span><span class="sxs-lookup"><span data-stu-id="5743b-195">Type</span></span>   | <span data-ttu-id="5743b-196">필수</span><span class="sxs-lookup"><span data-stu-id="5743b-196">Required</span></span> | <span data-ttu-id="5743b-197">메모</span><span class="sxs-lookup"><span data-stu-id="5743b-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="5743b-198">ID</span><span class="sxs-lookup"><span data-stu-id="5743b-198">ID</span></span>             | <span data-ttu-id="5743b-199">URL</span><span class="sxs-lookup"><span data-stu-id="5743b-199">URL</span></span>    | <span data-ttu-id="5743b-200">문자열</span><span class="sxs-lookup"><span data-stu-id="5743b-200">string</span></span> | <span data-ttu-id="5743b-201">예</span><span class="sxs-lookup"><span data-stu-id="5743b-201">yes</span></span>      | <span data-ttu-id="5743b-202">다시 나열할 패키지의 ID입니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-202">The ID of the package to relist</span></span>
<span data-ttu-id="5743b-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="5743b-203">VERSION</span></span>        | <span data-ttu-id="5743b-204">URL</span><span class="sxs-lookup"><span data-stu-id="5743b-204">URL</span></span>    | <span data-ttu-id="5743b-205">문자열</span><span class="sxs-lookup"><span data-stu-id="5743b-205">string</span></span> | <span data-ttu-id="5743b-206">예</span><span class="sxs-lookup"><span data-stu-id="5743b-206">yes</span></span>      | <span data-ttu-id="5743b-207">다시 나열할 패키지의 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-207">The version of the package to relist</span></span>
<span data-ttu-id="5743b-208">X NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="5743b-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="5743b-209">헤더</span><span class="sxs-lookup"><span data-stu-id="5743b-209">Header</span></span> | <span data-ttu-id="5743b-210">문자열</span><span class="sxs-lookup"><span data-stu-id="5743b-210">string</span></span> | <span data-ttu-id="5743b-211">예</span><span class="sxs-lookup"><span data-stu-id="5743b-211">yes</span></span>      | <span data-ttu-id="5743b-212">예를 들어 `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="5743b-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="5743b-213">응답</span><span class="sxs-lookup"><span data-stu-id="5743b-213">Response</span></span>

<span data-ttu-id="5743b-214">상태 코드</span><span class="sxs-lookup"><span data-stu-id="5743b-214">Status Code</span></span> | <span data-ttu-id="5743b-215">의미</span><span class="sxs-lookup"><span data-stu-id="5743b-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="5743b-216">200</span><span class="sxs-lookup"><span data-stu-id="5743b-216">200</span></span>         | <span data-ttu-id="5743b-217">이제 패키지가 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5743b-217">The package is now listed</span></span>
<span data-ttu-id="5743b-218">404</span><span class="sxs-lookup"><span data-stu-id="5743b-218">404</span></span>         | <span data-ttu-id="5743b-219">제공 된 `ID` 및가 있는 패키지가 없습니다. `VERSION`</span><span class="sxs-lookup"><span data-stu-id="5743b-219">No package with the provided `ID` and `VERSION` exists</span></span>
