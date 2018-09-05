---
title: 푸시 및 삭제, NuGet API
description: 게시 서비스에는 클라이언트가 새 패키지를 게시 및 나열을 취소 하거나 기존 패키지를 삭제할 수 있습니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: ad66d8e0ffda13aaef744104c213863b0e111e0e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547523"
---
# <a name="push-and-delete"></a><span data-ttu-id="b559f-103">푸시 및 삭제</span><span class="sxs-lookup"><span data-stu-id="b559f-103">Push and Delete</span></span>

<span data-ttu-id="b559f-104">푸시, 삭제 (또는 서버 구현에 따라 나열 취소) 수 및 NuGet V3 API를 사용 하 여 패키지를 다시 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="b559f-105">이러한 작업은 기반을 둔 합니다 `PackagePublish` 에서 리소스를 찾을 합니다 [서비스 인덱스](service-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="b559f-106">버전 관리</span><span class="sxs-lookup"><span data-stu-id="b559f-106">Versioning</span></span>

<span data-ttu-id="b559f-107">다음 `@type` 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-107">The following `@type` value is used:</span></span>

<span data-ttu-id="b559f-108">@type 값</span><span class="sxs-lookup"><span data-stu-id="b559f-108">@type value</span></span>          | <span data-ttu-id="b559f-109">노트</span><span class="sxs-lookup"><span data-stu-id="b559f-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="b559f-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="b559f-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="b559f-111">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="b559f-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="b559f-112">기준 URL</span><span class="sxs-lookup"><span data-stu-id="b559f-112">Base URL</span></span>

<span data-ttu-id="b559f-113">다음 Api에 대 한 기본 URL의 값은를 `@id` 의 속성을 `PackagePublish/2.0.0` 패키지 원본에 대 한 리소스 [서비스 인덱스](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="b559f-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="b559f-114">아래 설명서 nuget.org의 URL은 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="b559f-115">것이 좋습니다 `https://www.nuget.org/api/v2/package` 자리 표시자로는 `@id` 서비스 인덱스에서 찾을 값입니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="b559f-116">동일한 프로토콜은이 URL의 레거시 V2 푸시 끝점으로 동일한 위치를 가리키는지 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="b559f-117">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="b559f-117">HTTP methods</span></span>

<span data-ttu-id="b559f-118">합니다 `PUT`, `POST` 및 `DELETE` HTTP 메서드는이 리소스에 의해 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="b559f-119">각 끝점에 어떤 방법이 지원, 아래 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b559f-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="b559f-120">패키지 푸시</span><span class="sxs-lookup"><span data-stu-id="b559f-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="b559f-121">nuget.org에 [추가 요구 사항](NuGet-Protocols.md) 푸시 끝점과 상호 작용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="b559f-122">nuget.org는 다음 API를 사용 하 여 푸시 새 패키지를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="b559f-123">제공 된 ID와 버전을 사용 하 여 패키지에 이미 있으면 nuget.org에서 푸시를 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="b559f-124">다른 패키지 원본이 기존 패키지를 대체 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="b559f-125">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="b559f-125">Request parameters</span></span>

<span data-ttu-id="b559f-126">이름</span><span class="sxs-lookup"><span data-stu-id="b559f-126">Name</span></span>           | <span data-ttu-id="b559f-127">입력</span><span class="sxs-lookup"><span data-stu-id="b559f-127">In</span></span>     | <span data-ttu-id="b559f-128">형식</span><span class="sxs-lookup"><span data-stu-id="b559f-128">Type</span></span>   | <span data-ttu-id="b559f-129">필수</span><span class="sxs-lookup"><span data-stu-id="b559f-129">Required</span></span> | <span data-ttu-id="b559f-130">노트</span><span class="sxs-lookup"><span data-stu-id="b559f-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b559f-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b559f-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b559f-132">헤더</span><span class="sxs-lookup"><span data-stu-id="b559f-132">Header</span></span> | <span data-ttu-id="b559f-133">string</span><span class="sxs-lookup"><span data-stu-id="b559f-133">string</span></span> | <span data-ttu-id="b559f-134">예</span><span class="sxs-lookup"><span data-stu-id="b559f-134">yes</span></span>      | <span data-ttu-id="b559f-135">예를 들면 `X-NuGet-ApiKey: {USER_API_KEY}`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="b559f-136">API 키는 사용자가 패키지 원본에서 받은 및 클라이언트를 구성 하는 불투명 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="b559f-137">특정 문자열 서식 없음은 위임 하지만 API 키의 길이 HTTP 헤더 값에 대 한 적절 한 크기를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="b559f-138">요청 본문</span><span class="sxs-lookup"><span data-stu-id="b559f-138">Request body</span></span>

<span data-ttu-id="b559f-139">요청 본문에 다음 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="b559f-140">다중 파트 양식 데이터</span><span class="sxs-lookup"><span data-stu-id="b559f-140">Multipart form data</span></span>

<span data-ttu-id="b559f-141">요청 헤더 `Content-Type` 는 `multipart/form-data` 및 요청 본문의 첫째 항목 푸시되.nupkg의 원시 바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="b559f-142">다중 파트 본문의 후속 항목은 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="b559f-143">파일 이름 또는 다중 항목의 다른 모든 헤더는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="b559f-144">응답</span><span class="sxs-lookup"><span data-stu-id="b559f-144">Response</span></span>

<span data-ttu-id="b559f-145">상태 코드</span><span class="sxs-lookup"><span data-stu-id="b559f-145">Status Code</span></span> | <span data-ttu-id="b559f-146">의미</span><span class="sxs-lookup"><span data-stu-id="b559f-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="b559f-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="b559f-147">201, 202</span></span>    | <span data-ttu-id="b559f-148">패키지를 푸시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-148">The package was successfully pushed</span></span>
<span data-ttu-id="b559f-149">400</span><span class="sxs-lookup"><span data-stu-id="b559f-149">400</span></span>         | <span data-ttu-id="b559f-150">제공 된 패키지가 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-150">The provided package is invalid</span></span>
<span data-ttu-id="b559f-151">409</span><span class="sxs-lookup"><span data-stu-id="b559f-151">409</span></span>         | <span data-ttu-id="b559f-152">제공 된 ID와 버전을 사용 하 여 패키지를 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="b559f-153">패키지를 성공적으로 푸시 될 때 반환 된 성공 상태 코드에 서버 구현이 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="b559f-154">패키지 삭제</span><span class="sxs-lookup"><span data-stu-id="b559f-154">Delete a package</span></span>

<span data-ttu-id="b559f-155">nuget.org에서 패키지 삭제 요청으로 해석 "나열" 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="b559f-156">즉, 패키지는 패키지의 기존 소비자에 대 한 계속 사용할 수 있지만 패키지 또는 웹 인터페이스에서 검색 결과에서 더 이상 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="b559f-157">이 연습에 대 한 자세한 내용은 참조는 [패키지 삭제](../policies/deleting-packages.md) 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="b559f-158">다른 서버 구현은 하드 삭제이 신호를 해석 하거나 일시 삭제 하거나 나열을 취소 하는 무료입니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="b559f-159">예를 들어 [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (만 이전 V2 API를 지 원하는 서버 구현)이이 요청을 처리 하는 나열 취소 또는 구성 옵션에 따라 하드 삭제를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="b559f-160">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="b559f-160">Request parameters</span></span>

<span data-ttu-id="b559f-161">이름</span><span class="sxs-lookup"><span data-stu-id="b559f-161">Name</span></span>           | <span data-ttu-id="b559f-162">입력</span><span class="sxs-lookup"><span data-stu-id="b559f-162">In</span></span>     | <span data-ttu-id="b559f-163">형식</span><span class="sxs-lookup"><span data-stu-id="b559f-163">Type</span></span>   | <span data-ttu-id="b559f-164">필수</span><span class="sxs-lookup"><span data-stu-id="b559f-164">Required</span></span> | <span data-ttu-id="b559f-165">노트</span><span class="sxs-lookup"><span data-stu-id="b559f-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b559f-166">ID</span><span class="sxs-lookup"><span data-stu-id="b559f-166">ID</span></span>             | <span data-ttu-id="b559f-167">URL</span><span class="sxs-lookup"><span data-stu-id="b559f-167">URL</span></span>    | <span data-ttu-id="b559f-168">string</span><span class="sxs-lookup"><span data-stu-id="b559f-168">string</span></span> | <span data-ttu-id="b559f-169">예</span><span class="sxs-lookup"><span data-stu-id="b559f-169">yes</span></span>      | <span data-ttu-id="b559f-170">삭제할 패키지의 ID</span><span class="sxs-lookup"><span data-stu-id="b559f-170">The ID of the package to delete</span></span>
<span data-ttu-id="b559f-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="b559f-171">VERSION</span></span>        | <span data-ttu-id="b559f-172">URL</span><span class="sxs-lookup"><span data-stu-id="b559f-172">URL</span></span>    | <span data-ttu-id="b559f-173">string</span><span class="sxs-lookup"><span data-stu-id="b559f-173">string</span></span> | <span data-ttu-id="b559f-174">예</span><span class="sxs-lookup"><span data-stu-id="b559f-174">yes</span></span>      | <span data-ttu-id="b559f-175">삭제할 패키지의 버전</span><span class="sxs-lookup"><span data-stu-id="b559f-175">The version of the package to delete</span></span>
<span data-ttu-id="b559f-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b559f-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b559f-177">헤더</span><span class="sxs-lookup"><span data-stu-id="b559f-177">Header</span></span> | <span data-ttu-id="b559f-178">string</span><span class="sxs-lookup"><span data-stu-id="b559f-178">string</span></span> | <span data-ttu-id="b559f-179">예</span><span class="sxs-lookup"><span data-stu-id="b559f-179">yes</span></span>      | <span data-ttu-id="b559f-180">예를 들면 `X-NuGet-ApiKey: {USER_API_KEY}`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="b559f-181">응답</span><span class="sxs-lookup"><span data-stu-id="b559f-181">Response</span></span>

<span data-ttu-id="b559f-182">상태 코드</span><span class="sxs-lookup"><span data-stu-id="b559f-182">Status Code</span></span> | <span data-ttu-id="b559f-183">의미</span><span class="sxs-lookup"><span data-stu-id="b559f-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="b559f-184">204</span><span class="sxs-lookup"><span data-stu-id="b559f-184">204</span></span>         | <span data-ttu-id="b559f-185">패키지 삭제</span><span class="sxs-lookup"><span data-stu-id="b559f-185">The package was deleted</span></span>
<span data-ttu-id="b559f-186">404</span><span class="sxs-lookup"><span data-stu-id="b559f-186">404</span></span>         | <span data-ttu-id="b559f-187">제공 된 패키지가 없는 `ID` 고 `VERSION` 존재</span><span class="sxs-lookup"><span data-stu-id="b559f-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="b559f-188">패키지를 다시 나열</span><span class="sxs-lookup"><span data-stu-id="b559f-188">Relist a package</span></span>

<span data-ttu-id="b559f-189">패키지 나열 되어 있지 않으면 경우 해당 패키지를 다시 한 번 "버전 다시 나열" 끝점을 사용 하 여 검색 결과에 표시 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="b559f-190">이 끝점으로 동일한 셰이프가 [삭제 (나열) 끝점](#delete-a-package) 같지만 합니다 `POST` 대신 HTTP 메서드를 `DELETE` 메서드.</span><span class="sxs-lookup"><span data-stu-id="b559f-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="b559f-191">패키지가 이미 나열 되 고, 요청은 성공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="b559f-192">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="b559f-192">Request parameters</span></span>

<span data-ttu-id="b559f-193">이름</span><span class="sxs-lookup"><span data-stu-id="b559f-193">Name</span></span>           | <span data-ttu-id="b559f-194">입력</span><span class="sxs-lookup"><span data-stu-id="b559f-194">In</span></span>     | <span data-ttu-id="b559f-195">형식</span><span class="sxs-lookup"><span data-stu-id="b559f-195">Type</span></span>   | <span data-ttu-id="b559f-196">필수</span><span class="sxs-lookup"><span data-stu-id="b559f-196">Required</span></span> | <span data-ttu-id="b559f-197">노트</span><span class="sxs-lookup"><span data-stu-id="b559f-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b559f-198">ID</span><span class="sxs-lookup"><span data-stu-id="b559f-198">ID</span></span>             | <span data-ttu-id="b559f-199">URL</span><span class="sxs-lookup"><span data-stu-id="b559f-199">URL</span></span>    | <span data-ttu-id="b559f-200">string</span><span class="sxs-lookup"><span data-stu-id="b559f-200">string</span></span> | <span data-ttu-id="b559f-201">예</span><span class="sxs-lookup"><span data-stu-id="b559f-201">yes</span></span>      | <span data-ttu-id="b559f-202">패키지의 ID를 다시 나열</span><span class="sxs-lookup"><span data-stu-id="b559f-202">The ID of the package to relist</span></span>
<span data-ttu-id="b559f-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="b559f-203">VERSION</span></span>        | <span data-ttu-id="b559f-204">URL</span><span class="sxs-lookup"><span data-stu-id="b559f-204">URL</span></span>    | <span data-ttu-id="b559f-205">string</span><span class="sxs-lookup"><span data-stu-id="b559f-205">string</span></span> | <span data-ttu-id="b559f-206">예</span><span class="sxs-lookup"><span data-stu-id="b559f-206">yes</span></span>      | <span data-ttu-id="b559f-207">다시 나열 하는 패키지의 버전</span><span class="sxs-lookup"><span data-stu-id="b559f-207">The version of the package to relist</span></span>
<span data-ttu-id="b559f-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b559f-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b559f-209">헤더</span><span class="sxs-lookup"><span data-stu-id="b559f-209">Header</span></span> | <span data-ttu-id="b559f-210">string</span><span class="sxs-lookup"><span data-stu-id="b559f-210">string</span></span> | <span data-ttu-id="b559f-211">예</span><span class="sxs-lookup"><span data-stu-id="b559f-211">yes</span></span>      | <span data-ttu-id="b559f-212">예를 들면 `X-NuGet-ApiKey: {USER_API_KEY}`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="b559f-213">응답</span><span class="sxs-lookup"><span data-stu-id="b559f-213">Response</span></span>

<span data-ttu-id="b559f-214">상태 코드</span><span class="sxs-lookup"><span data-stu-id="b559f-214">Status Code</span></span> | <span data-ttu-id="b559f-215">의미</span><span class="sxs-lookup"><span data-stu-id="b559f-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="b559f-216">200</span><span class="sxs-lookup"><span data-stu-id="b559f-216">200</span></span>         | <span data-ttu-id="b559f-217">패키지는 이제 나열 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b559f-217">The package is now listed</span></span>
<span data-ttu-id="b559f-218">404</span><span class="sxs-lookup"><span data-stu-id="b559f-218">404</span></span>         | <span data-ttu-id="b559f-219">제공 된 패키지가 없는 `ID` 고 `VERSION` 존재</span><span class="sxs-lookup"><span data-stu-id="b559f-219">No package with the provided `ID` and `VERSION` exists</span></span>
