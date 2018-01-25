---
title: "밀어넣기 및 삭제를 NuGet API | Microsoft Docs"
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
description: "게시 서비스에는 클라이언트가 새 패키지를 게시 하 고 unlist 또는 기존 패키지를 삭제할 수 있습니다."
keywords: "NuGet API 푸시 패키지 API NuGet 패키지를 삭제, API NuGet 패키지를 NuGet API 업로드 패키지가 unlist, API NuGet 패키지를 만듭니다."
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: f8051ca57fccae77917567d8c9f2f8a120a8d884
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="6f978-104">밀어넣기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="6f978-104">Push and Delete</span></span>

<span data-ttu-id="6f978-105">Push, 삭제 (또는 서버 구현에 따라 unlist) 수는 relist NuGet V3 API를 사용 하 여 패키지 및 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-105">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="6f978-106">이러한 작업은에 기반을 둔는 `PackagePublish` 에서 리소스를 찾을 [서비스 인덱스](service-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-106">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="6f978-107">버전 관리</span><span class="sxs-lookup"><span data-stu-id="6f978-107">Versioning</span></span>

<span data-ttu-id="6f978-108">다음 `@type` 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-108">The following `@type` value is used:</span></span>

<span data-ttu-id="6f978-109">@type 값</span><span class="sxs-lookup"><span data-stu-id="6f978-109">@type value</span></span>          | <span data-ttu-id="6f978-110">노트</span><span class="sxs-lookup"><span data-stu-id="6f978-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="6f978-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="6f978-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="6f978-112">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="6f978-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="6f978-113">기준 URL</span><span class="sxs-lookup"><span data-stu-id="6f978-113">Base URL</span></span>

<span data-ttu-id="6f978-114">다음 Api에 대 한 기본 URL의 값은는 `@id` 의 속성은 `PackagePublish/2.0.0` 패키지 소스에서 리소스 [서비스 인덱스](service-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="6f978-115">아래 설명서에 대 한 nuget.org의 URL이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="6f978-116">고려 `https://www.nuget.org/api/v2/package` 에 대 한 자리 표시자로는 `@id` 서비스 인덱스에서 값을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="6f978-117">동일한 프로토콜은이 URL의 레거시 V2 푸시 끝점으로 같은 위치를 가리키는지 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="6f978-118">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="6f978-118">HTTP methods</span></span>

<span data-ttu-id="6f978-119">`PUT`, `POST` 및 `DELETE` HTTP 메서드가이 리소스에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-119">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="6f978-120">각 끝점에서 지원 되는 어떤 메서드는, 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="6f978-121">푸시 한 패키지</span><span class="sxs-lookup"><span data-stu-id="6f978-121">Push a package</span></span>

> [!Note]
> <span data-ttu-id="6f978-122">nuget.org에 [요구 사항이 추가로 적용](NuGet-Protocols.md) 푸시 끝점과 상호 작용 하기 위한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-122">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="6f978-123">nuget.org 다음 API를 사용 하 여 푸시 새 패키지를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-123">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="6f978-124">제공 된 ID와 버전을 사용 하 여 패키지에 이미 있으면 nuget.org 푸시를 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-124">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="6f978-125">기존 패키지를 대체 합니다. 다른 패키지 원본을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-125">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="6f978-126">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="6f978-126">Request parameters</span></span>

<span data-ttu-id="6f978-127">name</span><span class="sxs-lookup"><span data-stu-id="6f978-127">Name</span></span>           | <span data-ttu-id="6f978-128">입력</span><span class="sxs-lookup"><span data-stu-id="6f978-128">In</span></span>     | <span data-ttu-id="6f978-129">형식</span><span class="sxs-lookup"><span data-stu-id="6f978-129">Type</span></span>   | <span data-ttu-id="6f978-130">필수</span><span class="sxs-lookup"><span data-stu-id="6f978-130">Required</span></span> | <span data-ttu-id="6f978-131">노트</span><span class="sxs-lookup"><span data-stu-id="6f978-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="6f978-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="6f978-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="6f978-133">Header</span><span class="sxs-lookup"><span data-stu-id="6f978-133">Header</span></span> | <span data-ttu-id="6f978-134">string</span><span class="sxs-lookup"><span data-stu-id="6f978-134">string</span></span> | <span data-ttu-id="6f978-135">예</span><span class="sxs-lookup"><span data-stu-id="6f978-135">yes</span></span>      | <span data-ttu-id="6f978-136">예를 들면 `X-NuGet-ApiKey: {USER_API_KEY}`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="6f978-137">API 키는 사용자가 패키지 소스에서 수신 하 고 클라이언트를 구성 하는 불투명 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="6f978-138">특정 문자열 형식은 없습니다 위임 되는지 있지만 API 키의 길이 HTTP 헤더 값에 대 한 적절 한 크기를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="6f978-139">요청 본문</span><span class="sxs-lookup"><span data-stu-id="6f978-139">Request body</span></span>

<span data-ttu-id="6f978-140">요청 본문에는 다음과 같은 형태로 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-140">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="6f978-141">다중 파트 양식 데이터</span><span class="sxs-lookup"><span data-stu-id="6f978-141">Multipart form data</span></span>

<span data-ttu-id="6f978-142">요청 헤더 `Content-Type` 은 `multipart/form-data` 및 요청 본문의 첫 번째 항목은 눌렀는지.nupkg의 원시 바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-142">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="6f978-143">다중 파트 본문에 있는 다음 항목은 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-143">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="6f978-144">파일 이름 또는 다중 항목의 다른 모든 헤더는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-144">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="6f978-145">응답</span><span class="sxs-lookup"><span data-stu-id="6f978-145">Response</span></span>

<span data-ttu-id="6f978-146">상태 코드</span><span class="sxs-lookup"><span data-stu-id="6f978-146">Status Code</span></span> | <span data-ttu-id="6f978-147">의미</span><span class="sxs-lookup"><span data-stu-id="6f978-147">Meaning</span></span>
----------- | -------
<span data-ttu-id="6f978-148">201, 202</span><span class="sxs-lookup"><span data-stu-id="6f978-148">201, 202</span></span>    | <span data-ttu-id="6f978-149">패키지가는 성공적으로 푸시되 지</span><span class="sxs-lookup"><span data-stu-id="6f978-149">The package was successfully pushed</span></span>
<span data-ttu-id="6f978-150">400</span><span class="sxs-lookup"><span data-stu-id="6f978-150">400</span></span>         | <span data-ttu-id="6f978-151">제공 된 패키지가 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-151">The provided package is invalid</span></span>
<span data-ttu-id="6f978-152">409</span><span class="sxs-lookup"><span data-stu-id="6f978-152">409</span></span>         | <span data-ttu-id="6f978-153">제공 된 ID와 버전을 사용 하 여 패키지 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-153">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="6f978-154">패키지를 성공적으로 푸시 될 때 반환 되는 성공 상태 코드에 서버 구현은 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-154">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="6f978-155">패키지 삭제</span><span class="sxs-lookup"><span data-stu-id="6f978-155">Delete a package</span></span>

<span data-ttu-id="6f978-156">nuget.org 패키지 삭제 요청으로 해석 하는 "unlist"입니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-156">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="6f978-157">즉, 패키지를 패키지의 기존 사용자가 계속 사용할 수 있지만 패키지 또는 웹 인터페이스 검색 결과에 더 이상 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-157">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="6f978-158">이 연습에 대 한 자세한 내용은 참조는 [패키지 삭제](../policies/deleting-packages.md) 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-158">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="6f978-159">하드 delete이 신호를 해석 하거나 일시 삭제 하거나 unlist 하는 다른 서버 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-159">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="6f978-160">예를 들어 [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (만 이전 V2 API를 지 원하는 서버 구현)는 unlist 또는 구성 옵션에 따라 하드 삭제로이 요청을 처리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-160">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="6f978-161">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="6f978-161">Request parameters</span></span>

<span data-ttu-id="6f978-162">name</span><span class="sxs-lookup"><span data-stu-id="6f978-162">Name</span></span>           | <span data-ttu-id="6f978-163">입력</span><span class="sxs-lookup"><span data-stu-id="6f978-163">In</span></span>     | <span data-ttu-id="6f978-164">형식</span><span class="sxs-lookup"><span data-stu-id="6f978-164">Type</span></span>   | <span data-ttu-id="6f978-165">필수</span><span class="sxs-lookup"><span data-stu-id="6f978-165">Required</span></span> | <span data-ttu-id="6f978-166">노트</span><span class="sxs-lookup"><span data-stu-id="6f978-166">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="6f978-167">ID</span><span class="sxs-lookup"><span data-stu-id="6f978-167">ID</span></span>             | <span data-ttu-id="6f978-168">URL</span><span class="sxs-lookup"><span data-stu-id="6f978-168">URL</span></span>    | <span data-ttu-id="6f978-169">string</span><span class="sxs-lookup"><span data-stu-id="6f978-169">string</span></span> | <span data-ttu-id="6f978-170">예</span><span class="sxs-lookup"><span data-stu-id="6f978-170">yes</span></span>      | <span data-ttu-id="6f978-171">패키지의 ID를 삭제 하려면</span><span class="sxs-lookup"><span data-stu-id="6f978-171">The ID of the package to delete</span></span>
<span data-ttu-id="6f978-172">VERSION</span><span class="sxs-lookup"><span data-stu-id="6f978-172">VERSION</span></span>        | <span data-ttu-id="6f978-173">URL</span><span class="sxs-lookup"><span data-stu-id="6f978-173">URL</span></span>    | <span data-ttu-id="6f978-174">string</span><span class="sxs-lookup"><span data-stu-id="6f978-174">string</span></span> | <span data-ttu-id="6f978-175">예</span><span class="sxs-lookup"><span data-stu-id="6f978-175">yes</span></span>      | <span data-ttu-id="6f978-176">삭제할 패키지의 버전</span><span class="sxs-lookup"><span data-stu-id="6f978-176">The version of the package to delete</span></span>
<span data-ttu-id="6f978-177">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="6f978-177">X-NuGet-ApiKey</span></span> | <span data-ttu-id="6f978-178">Header</span><span class="sxs-lookup"><span data-stu-id="6f978-178">Header</span></span> | <span data-ttu-id="6f978-179">string</span><span class="sxs-lookup"><span data-stu-id="6f978-179">string</span></span> | <span data-ttu-id="6f978-180">예</span><span class="sxs-lookup"><span data-stu-id="6f978-180">yes</span></span>      | <span data-ttu-id="6f978-181">예를 들면 `X-NuGet-ApiKey: {USER_API_KEY}`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-181">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="6f978-182">응답</span><span class="sxs-lookup"><span data-stu-id="6f978-182">Response</span></span>

<span data-ttu-id="6f978-183">상태 코드</span><span class="sxs-lookup"><span data-stu-id="6f978-183">Status Code</span></span> | <span data-ttu-id="6f978-184">의미</span><span class="sxs-lookup"><span data-stu-id="6f978-184">Meaning</span></span>
----------- | -------
<span data-ttu-id="6f978-185">204</span><span class="sxs-lookup"><span data-stu-id="6f978-185">204</span></span>         | <span data-ttu-id="6f978-186">패키지 삭제</span><span class="sxs-lookup"><span data-stu-id="6f978-186">The package was deleted</span></span>
<span data-ttu-id="6f978-187">404</span><span class="sxs-lookup"><span data-stu-id="6f978-187">404</span></span>         | <span data-ttu-id="6f978-188">제공 된 패키지가 `ID` 및 `VERSION` 존재</span><span class="sxs-lookup"><span data-stu-id="6f978-188">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="6f978-189">패키지 relist</span><span class="sxs-lookup"><span data-stu-id="6f978-189">Relist a package</span></span>

<span data-ttu-id="6f978-190">패키지 나열 되어 있지 않으면 경우 해당 패키지를 다시 한 번 "relist" 끝점을 사용 하 여 검색 결과에 표시 하도록 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-190">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="6f978-191">이 끝점에는와 같은 형태로 [삭제 (unlist) 끝점](#delete-a-package) 하지만 사용 하 여는 `POST` 대신 HTTP 메서드는 `DELETE` 메서드.</span><span class="sxs-lookup"><span data-stu-id="6f978-191">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="6f978-192">패키지 목록에 이미는 요청은 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-192">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="6f978-193">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="6f978-193">Request parameters</span></span>

<span data-ttu-id="6f978-194">name</span><span class="sxs-lookup"><span data-stu-id="6f978-194">Name</span></span>           | <span data-ttu-id="6f978-195">입력</span><span class="sxs-lookup"><span data-stu-id="6f978-195">In</span></span>     | <span data-ttu-id="6f978-196">형식</span><span class="sxs-lookup"><span data-stu-id="6f978-196">Type</span></span>   | <span data-ttu-id="6f978-197">필수</span><span class="sxs-lookup"><span data-stu-id="6f978-197">Required</span></span> | <span data-ttu-id="6f978-198">노트</span><span class="sxs-lookup"><span data-stu-id="6f978-198">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="6f978-199">ID</span><span class="sxs-lookup"><span data-stu-id="6f978-199">ID</span></span>             | <span data-ttu-id="6f978-200">URL</span><span class="sxs-lookup"><span data-stu-id="6f978-200">URL</span></span>    | <span data-ttu-id="6f978-201">string</span><span class="sxs-lookup"><span data-stu-id="6f978-201">string</span></span> | <span data-ttu-id="6f978-202">예</span><span class="sxs-lookup"><span data-stu-id="6f978-202">yes</span></span>      | <span data-ttu-id="6f978-203">Relist를 패키지의 ID</span><span class="sxs-lookup"><span data-stu-id="6f978-203">The ID of the package to relist</span></span>
<span data-ttu-id="6f978-204">VERSION</span><span class="sxs-lookup"><span data-stu-id="6f978-204">VERSION</span></span>        | <span data-ttu-id="6f978-205">URL</span><span class="sxs-lookup"><span data-stu-id="6f978-205">URL</span></span>    | <span data-ttu-id="6f978-206">string</span><span class="sxs-lookup"><span data-stu-id="6f978-206">string</span></span> | <span data-ttu-id="6f978-207">예</span><span class="sxs-lookup"><span data-stu-id="6f978-207">yes</span></span>      | <span data-ttu-id="6f978-208">Relist 패키지의 버전</span><span class="sxs-lookup"><span data-stu-id="6f978-208">The version of the package to relist</span></span>
<span data-ttu-id="6f978-209">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="6f978-209">X-NuGet-ApiKey</span></span> | <span data-ttu-id="6f978-210">Header</span><span class="sxs-lookup"><span data-stu-id="6f978-210">Header</span></span> | <span data-ttu-id="6f978-211">string</span><span class="sxs-lookup"><span data-stu-id="6f978-211">string</span></span> | <span data-ttu-id="6f978-212">예</span><span class="sxs-lookup"><span data-stu-id="6f978-212">yes</span></span>      | <span data-ttu-id="6f978-213">예를 들면 `X-NuGet-ApiKey: {USER_API_KEY}`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6f978-213">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="6f978-214">응답</span><span class="sxs-lookup"><span data-stu-id="6f978-214">Response</span></span>

<span data-ttu-id="6f978-215">상태 코드</span><span class="sxs-lookup"><span data-stu-id="6f978-215">Status Code</span></span> | <span data-ttu-id="6f978-216">의미</span><span class="sxs-lookup"><span data-stu-id="6f978-216">Meaning</span></span>
----------- | -------
<span data-ttu-id="6f978-217">200</span><span class="sxs-lookup"><span data-stu-id="6f978-217">200</span></span>         | <span data-ttu-id="6f978-218">패키지 나열 되어</span><span class="sxs-lookup"><span data-stu-id="6f978-218">The package is now listed</span></span>
<span data-ttu-id="6f978-219">404</span><span class="sxs-lookup"><span data-stu-id="6f978-219">404</span></span>         | <span data-ttu-id="6f978-220">제공 된 패키지가 `ID` 및 `VERSION` 존재</span><span class="sxs-lookup"><span data-stu-id="6f978-220">No package with the provided `ID` and `VERSION` exists</span></span>
