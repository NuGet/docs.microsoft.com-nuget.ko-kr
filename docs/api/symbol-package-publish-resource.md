---
title: 기호 패키지, NuGet API 푸시 | Microsoft Docs
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 게시 서비스에는 새 기호 패키지를 게시 하는 클라이언트 수 있습니다.
keywords: NuGet API 푸시 기호 패키지
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580416"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="1c1f8-104">기호 패키지 푸시</span><span class="sxs-lookup"><span data-stu-id="1c1f8-104">Push Symbol Packages</span></span>

<span data-ttu-id="1c1f8-105">패키지를 푸시 하려면 기호 수 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) NuGet V3 API를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="1c1f8-106">이러한 작업은 기반을 둔 합니다 `SymbolPackagePublish` 에서 리소스를 찾을 합니다 [서비스 인덱스](service-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="1c1f8-107">버전 관리</span><span class="sxs-lookup"><span data-stu-id="1c1f8-107">Versioning</span></span>

<span data-ttu-id="1c1f8-108">다음 `@type` 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-108">The following `@type` value is used:</span></span>

<span data-ttu-id="1c1f8-109">@type 값</span><span class="sxs-lookup"><span data-stu-id="1c1f8-109">@type value</span></span>                 | <span data-ttu-id="1c1f8-110">노트</span><span class="sxs-lookup"><span data-stu-id="1c1f8-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="1c1f8-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="1c1f8-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="1c1f8-112">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="1c1f8-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="1c1f8-113">기준 URL</span><span class="sxs-lookup"><span data-stu-id="1c1f8-113">Base URL</span></span>

<span data-ttu-id="1c1f8-114">다음 Api에 대 한 기본 URL의 값은를 `@id` 의 속성을 `SymbolPackagePublish/4.9.0` 패키지 원본에 대 한 리소스 [서비스 인덱스](service-index.md).</span><span class="sxs-lookup"><span data-stu-id="1c1f8-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="1c1f8-115">아래 설명서 nuget.org의 URL은 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="1c1f8-116">것이 좋습니다 `https://www.nuget.org/api/v2/symbolpackage` 자리 표시자로는 `@id` 서비스 인덱스에서 찾을 값입니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="1c1f8-117">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="1c1f8-117">HTTP methods</span></span>

<span data-ttu-id="1c1f8-118">`PUT` HTTP 메서드는이 리소스에서 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="1c1f8-119">기호 패키지를 푸시</span><span class="sxs-lookup"><span data-stu-id="1c1f8-119">Push a symbol package</span></span>

<span data-ttu-id="1c1f8-120">nuget.org에 푸시하는 새 기호 패키지 형식 지원 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 다음 API를 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="1c1f8-121">기호 패키지는 동일한 ID 및 버전을 사용 하 여 여러 번 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="1c1f8-122">기호 패키지는 다음과 같은 경우 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="1c1f8-123">패키지는 동일한 ID 및 버전을 사용 하 여 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="1c1f8-124">동일한 ID 및 버전을 사용 하 여 기호 패키지 푸시된 있지만 아직 게시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="1c1f8-125">기호 패키지 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 잘못 되었습니다 (참조 [기호 패키지 제약 조건](../create-packages/Symbol-Packages-snupkg.md)).</span><span class="sxs-lookup"><span data-stu-id="1c1f8-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="1c1f8-126">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="1c1f8-126">Request parameters</span></span>

<span data-ttu-id="1c1f8-127">이름</span><span class="sxs-lookup"><span data-stu-id="1c1f8-127">Name</span></span>           | <span data-ttu-id="1c1f8-128">입력</span><span class="sxs-lookup"><span data-stu-id="1c1f8-128">In</span></span>     | <span data-ttu-id="1c1f8-129">형식</span><span class="sxs-lookup"><span data-stu-id="1c1f8-129">Type</span></span>   | <span data-ttu-id="1c1f8-130">필수</span><span class="sxs-lookup"><span data-stu-id="1c1f8-130">Required</span></span> | <span data-ttu-id="1c1f8-131">노트</span><span class="sxs-lookup"><span data-stu-id="1c1f8-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="1c1f8-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="1c1f8-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="1c1f8-133">헤더</span><span class="sxs-lookup"><span data-stu-id="1c1f8-133">Header</span></span> | <span data-ttu-id="1c1f8-134">string</span><span class="sxs-lookup"><span data-stu-id="1c1f8-134">string</span></span> | <span data-ttu-id="1c1f8-135">예</span><span class="sxs-lookup"><span data-stu-id="1c1f8-135">yes</span></span>      | <span data-ttu-id="1c1f8-136">예를 들면 `X-NuGet-ApiKey: {USER_API_KEY}`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="1c1f8-137">API 키는 사용자가 패키지 원본에서 받은 및 클라이언트를 구성 하는 불투명 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="1c1f8-138">특정 문자열 서식 없음은 위임 하지만 API 키의 길이 HTTP 헤더 값에 대 한 적절 한 크기를 초과할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="1c1f8-139">요청 본문</span><span class="sxs-lookup"><span data-stu-id="1c1f8-139">Request body</span></span>

<span data-ttu-id="1c1f8-140">기호 푸시에 대 한 요청 본문은 패키지 푸시 요청의 요청 본문을 사용 하 여 동일 (참조 [패키지 푸시 및 삭제](package-publish-resource.md)).</span><span class="sxs-lookup"><span data-stu-id="1c1f8-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="1c1f8-141">응답</span><span class="sxs-lookup"><span data-stu-id="1c1f8-141">Response</span></span>

<span data-ttu-id="1c1f8-142">상태 코드</span><span class="sxs-lookup"><span data-stu-id="1c1f8-142">Status Code</span></span> | <span data-ttu-id="1c1f8-143">의미</span><span class="sxs-lookup"><span data-stu-id="1c1f8-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="1c1f8-144">201</span><span class="sxs-lookup"><span data-stu-id="1c1f8-144">201</span></span>         | <span data-ttu-id="1c1f8-145">기호 패키지를 푸시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="1c1f8-146">400</span><span class="sxs-lookup"><span data-stu-id="1c1f8-146">400</span></span>         | <span data-ttu-id="1c1f8-147">제공 된 기호 패키지 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="1c1f8-148">401</span><span class="sxs-lookup"><span data-stu-id="1c1f8-148">401</span></span>         | <span data-ttu-id="1c1f8-149">사용자는이 작업을 수행할 수 있는 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="1c1f8-150">404</span><span class="sxs-lookup"><span data-stu-id="1c1f8-150">404</span></span>         | <span data-ttu-id="1c1f8-151">제공 된 ID와 버전을 사용 하 여 해당 패키지가 존재 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="1c1f8-152">409</span><span class="sxs-lookup"><span data-stu-id="1c1f8-152">409</span></span>         | <span data-ttu-id="1c1f8-153">제공 된 ID와 버전을 사용 하 여 기호 패키지 푸시된 있지만 아직 사용할 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="1c1f8-154">413</span><span class="sxs-lookup"><span data-stu-id="1c1f8-154">413</span></span>         | <span data-ttu-id="1c1f8-155">패키지가 너무 큽니다.</span><span class="sxs-lookup"><span data-stu-id="1c1f8-155">The package is too large.</span></span>

