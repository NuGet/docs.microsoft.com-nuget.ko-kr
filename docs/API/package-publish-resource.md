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
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "게시 서비스에는 클라이언트가 새 패키지를 게시 하 고 unlist 또는 기존 패키지를 삭제할 수 있습니다."
keywords: "NuGet API 푸시 패키지 API NuGet 패키지를 삭제, API NuGet 패키지를 NuGet API 업로드 패키지가 unlist, API NuGet 패키지를 만듭니다."
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 1fa3c0e1698a11208d9ef29fdf26a4980cb60cf5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="push-and-delete"></a><span data-ttu-id="37dd0-104">밀어넣기 및 삭제</span><span class="sxs-lookup"><span data-stu-id="37dd0-104">Push and Delete</span></span>

<span data-ttu-id="37dd0-105">푸시 및 삭제 (또는 서버 구현에 따라 unlist) 수는 NuGet V3 API를 사용 하 여 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-105">It is possible to push and delete (or unlist, depending on the server implementation) packages using the NuGet V3 API.</span></span>
<span data-ttu-id="37dd0-106">두 작업은에 기반을 둔는 `PackagePublish` 에서 리소스를 찾을 [서비스 인덱스](service-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-106">Both operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="37dd0-107">버전 관리</span><span class="sxs-lookup"><span data-stu-id="37dd0-107">Versioning</span></span>

<span data-ttu-id="37dd0-108">다음 `@type` 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-108">The following `@type` value is used:</span></span>

<span data-ttu-id="37dd0-109">@type 값</span><span class="sxs-lookup"><span data-stu-id="37dd0-109">@type value</span></span>          | <span data-ttu-id="37dd0-110">참고</span><span class="sxs-lookup"><span data-stu-id="37dd0-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="37dd0-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="37dd0-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="37dd0-112">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="37dd0-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="37dd0-113">기준 URL</span><span class="sxs-lookup"><span data-stu-id="37dd0-113">Base URL</span></span>

<span data-ttu-id="37dd0-114">다음 Api에 대 한 기본 URL의 값은는 `@id` 의 속성은 `PackagePublish/2.0.0` 패키지 소스에서 리소스 [서비스 인덱스](service-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="37dd0-115">아래 설명서에 대 한 nuget.org의 URL이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="37dd0-116">고려 `https://www.nuget.org/api/v2/package` 에 대 한 자리 표시자로는 `@id` 서비스 인덱스에서 값을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="37dd0-117">동일한 프로토콜은이 URL의 레거시 V2 푸시 끝점으로 같은 위치를 가리키는지 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="37dd0-118">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="37dd0-118">HTTP methods</span></span>

<span data-ttu-id="37dd0-119">`PUT` 및 `DELETE` HTTP 메서드가이 리소스에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-119">The `PUT` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="37dd0-120">각 끝점에서 지원 되는 어떤 메서드는, 다음을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="37dd0-121">푸시 한 패키지</span><span class="sxs-lookup"><span data-stu-id="37dd0-121">Push a package</span></span>

<span data-ttu-id="37dd0-122">nuget.org 다음 API를 사용 하 여 푸시 새 패키지를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="37dd0-123">제공 된 ID와 버전을 사용 하 여 패키지에 이미 있으면 nuget.org 푸시를 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="37dd0-124">기존 패키지를 대체 합니다. 다른 패키지 원본을 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="37dd0-125">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="37dd0-125">Request parameters</span></span>

<span data-ttu-id="37dd0-126">이름</span><span class="sxs-lookup"><span data-stu-id="37dd0-126">Name</span></span>           | <span data-ttu-id="37dd0-127">입력</span><span class="sxs-lookup"><span data-stu-id="37dd0-127">In</span></span>     | <span data-ttu-id="37dd0-128">형식</span><span class="sxs-lookup"><span data-stu-id="37dd0-128">Type</span></span>   | <span data-ttu-id="37dd0-129">필수</span><span class="sxs-lookup"><span data-stu-id="37dd0-129">Required</span></span> | <span data-ttu-id="37dd0-130">참고</span><span class="sxs-lookup"><span data-stu-id="37dd0-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="37dd0-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="37dd0-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="37dd0-132">Header</span><span class="sxs-lookup"><span data-stu-id="37dd0-132">Header</span></span> | <span data-ttu-id="37dd0-133">string</span><span class="sxs-lookup"><span data-stu-id="37dd0-133">string</span></span> | <span data-ttu-id="37dd0-134">예</span><span class="sxs-lookup"><span data-stu-id="37dd0-134">yes</span></span>      | <span data-ttu-id="37dd0-135">예를 들면 `X-NuGet-ApiKey: {USER_API_KEY}`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="37dd0-136">API 키는 사용자가 패키지 소스에서 수신 하 고 클라이언트를 구성 하는 불투명 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="37dd0-137">특정 문자열 형식은 없습니다 위임 되는지 있지만 API 키의 길이 HTTP 헤더 값에 대 한 적절 한 크기를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="37dd0-138">요청 본문</span><span class="sxs-lookup"><span data-stu-id="37dd0-138">Request body</span></span>

<span data-ttu-id="37dd0-139">요청 본문에는 다음과 같은 형태로 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="37dd0-140">다중 파트 양식 데이터</span><span class="sxs-lookup"><span data-stu-id="37dd0-140">Multipart form data</span></span>

<span data-ttu-id="37dd0-141">요청 헤더 `Content-Type` 은 `multipart/form-data` 및 요청 본문의 첫 번째 항목은 눌렀는지.nupkg의 원시 바이트입니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="37dd0-142">다중 파트 본문에 있는 다음 항목은 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="37dd0-143">파일 이름 또는 다중 항목의 다른 모든 헤더는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="37dd0-144">응답</span><span class="sxs-lookup"><span data-stu-id="37dd0-144">Response</span></span>

<span data-ttu-id="37dd0-145">상태 코드</span><span class="sxs-lookup"><span data-stu-id="37dd0-145">Status Code</span></span> | <span data-ttu-id="37dd0-146">의미</span><span class="sxs-lookup"><span data-stu-id="37dd0-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="37dd0-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="37dd0-147">201, 202</span></span>    | <span data-ttu-id="37dd0-148">패키지가는 성공적으로 푸시되 지</span><span class="sxs-lookup"><span data-stu-id="37dd0-148">The package was successfully pushed</span></span>
<span data-ttu-id="37dd0-149">400</span><span class="sxs-lookup"><span data-stu-id="37dd0-149">400</span></span>         | <span data-ttu-id="37dd0-150">제공 된 패키지가 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-150">The provided package is invalid</span></span>
<span data-ttu-id="37dd0-151">409</span><span class="sxs-lookup"><span data-stu-id="37dd0-151">409</span></span>         | <span data-ttu-id="37dd0-152">제공 된 ID와 버전을 사용 하 여 패키지 이미 있습니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="37dd0-153">패키지를 성공적으로 푸시 될 때 반환 되는 성공 상태 코드에 서버 구현은 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="37dd0-154">패키지 삭제</span><span class="sxs-lookup"><span data-stu-id="37dd0-154">Delete a package</span></span>

<span data-ttu-id="37dd0-155">nuget.org 패키지 삭제 요청으로 해석 하는 "unlist"입니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="37dd0-156">즉, 패키지를 패키지의 기존 사용자가 계속 사용할 수 있지만 패키지 또는 웹 인터페이스 검색 결과에 더 이상 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="37dd0-157">이 연습에 대 한 자세한 내용은 참조는 [패키지 삭제](../policies/deleting-packages.md) 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="37dd0-158">하드 delete이 신호를 해석 하거나 일시 삭제 하거나 unlist 하는 다른 서버 구현입니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="37dd0-159">예를 들어 [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (만 이전 V2 API를 지 원하는 서버 구현)는 unlist 또는 구성 옵션에 따라 하드 삭제로이 요청을 처리를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="37dd0-160">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="37dd0-160">Request parameters</span></span>

<span data-ttu-id="37dd0-161">이름</span><span class="sxs-lookup"><span data-stu-id="37dd0-161">Name</span></span>           | <span data-ttu-id="37dd0-162">입력</span><span class="sxs-lookup"><span data-stu-id="37dd0-162">In</span></span>     | <span data-ttu-id="37dd0-163">형식</span><span class="sxs-lookup"><span data-stu-id="37dd0-163">Type</span></span>   | <span data-ttu-id="37dd0-164">필수</span><span class="sxs-lookup"><span data-stu-id="37dd0-164">Required</span></span> | <span data-ttu-id="37dd0-165">참고</span><span class="sxs-lookup"><span data-stu-id="37dd0-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="37dd0-166">ID</span><span class="sxs-lookup"><span data-stu-id="37dd0-166">ID</span></span>             | <span data-ttu-id="37dd0-167">URL</span><span class="sxs-lookup"><span data-stu-id="37dd0-167">URL</span></span>    | <span data-ttu-id="37dd0-168">string</span><span class="sxs-lookup"><span data-stu-id="37dd0-168">string</span></span> | <span data-ttu-id="37dd0-169">예</span><span class="sxs-lookup"><span data-stu-id="37dd0-169">yes</span></span>      | <span data-ttu-id="37dd0-170">패키지의 ID를 삭제 하려면</span><span class="sxs-lookup"><span data-stu-id="37dd0-170">The ID of the package to delete</span></span>
<span data-ttu-id="37dd0-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="37dd0-171">VERSION</span></span>        | <span data-ttu-id="37dd0-172">URL</span><span class="sxs-lookup"><span data-stu-id="37dd0-172">URL</span></span>    | <span data-ttu-id="37dd0-173">string</span><span class="sxs-lookup"><span data-stu-id="37dd0-173">string</span></span> | <span data-ttu-id="37dd0-174">예</span><span class="sxs-lookup"><span data-stu-id="37dd0-174">yes</span></span>      | <span data-ttu-id="37dd0-175">삭제할 패키지의 버전</span><span class="sxs-lookup"><span data-stu-id="37dd0-175">The version of the package to delete</span></span>
<span data-ttu-id="37dd0-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="37dd0-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="37dd0-177">Header</span><span class="sxs-lookup"><span data-stu-id="37dd0-177">Header</span></span> | <span data-ttu-id="37dd0-178">string</span><span class="sxs-lookup"><span data-stu-id="37dd0-178">string</span></span> | <span data-ttu-id="37dd0-179">예</span><span class="sxs-lookup"><span data-stu-id="37dd0-179">yes</span></span>      | <span data-ttu-id="37dd0-180">예를 들면 `X-NuGet-ApiKey: {USER_API_KEY}`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="37dd0-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="37dd0-181">응답</span><span class="sxs-lookup"><span data-stu-id="37dd0-181">Response</span></span>

<span data-ttu-id="37dd0-182">상태 코드</span><span class="sxs-lookup"><span data-stu-id="37dd0-182">Status Code</span></span> | <span data-ttu-id="37dd0-183">의미</span><span class="sxs-lookup"><span data-stu-id="37dd0-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="37dd0-184">204</span><span class="sxs-lookup"><span data-stu-id="37dd0-184">204</span></span>         | <span data-ttu-id="37dd0-185">패키지 삭제</span><span class="sxs-lookup"><span data-stu-id="37dd0-185">The package was deleted</span></span>
<span data-ttu-id="37dd0-186">404</span><span class="sxs-lookup"><span data-stu-id="37dd0-186">404</span></span>         | <span data-ttu-id="37dd0-187">제공 된 패키지가 `ID` 및 `VERSION` 존재</span><span class="sxs-lookup"><span data-stu-id="37dd0-187">No package with the provided `ID` and `VERSION` exists</span></span>
