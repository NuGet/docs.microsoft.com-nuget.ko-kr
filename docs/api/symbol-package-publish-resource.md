---
title: 푸시 기호 패키지, NuGet API | Microsoft Docs
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 게시 서비스를 사용 하면 클라이언트가 새 기호 패키지를 게시할 수 있습니다.
keywords: NuGet API 푸시 기호 패키지
ms.reviewer: karann
ms.openlocfilehash: 91bb4c9ca77fd7f1ff35831e02eb4f9d65d641c5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773897"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="af6a4-104">기호 패키지 푸시</span><span class="sxs-lookup"><span data-stu-id="af6a4-104">Push Symbol Packages</span></span>

<span data-ttu-id="af6a4-105">NuGet V3 API를 사용 하 여 기호 패키지 ([snupkg](../create-packages/Symbol-Packages-snupkg.md))를 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="af6a4-106">이러한 작업은 `SymbolPackagePublish` [서비스 인덱스](service-index.md)에 있는 리소스를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="af6a4-107">버전 관리</span><span class="sxs-lookup"><span data-stu-id="af6a4-107">Versioning</span></span>

<span data-ttu-id="af6a4-108">사용 되는 `@type` 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-108">The following `@type` value is used:</span></span>

<span data-ttu-id="af6a4-109">@type 값</span><span class="sxs-lookup"><span data-stu-id="af6a4-109">@type value</span></span>                 | <span data-ttu-id="af6a4-110">메모</span><span class="sxs-lookup"><span data-stu-id="af6a4-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="af6a4-111">기호 Packagepublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="af6a4-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="af6a4-112">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="af6a4-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="af6a4-113">기준 URL</span><span class="sxs-lookup"><span data-stu-id="af6a4-113">Base URL</span></span>

<span data-ttu-id="af6a4-114">다음 Api에 대 한 기준 URL은 `@id` `SymbolPackagePublish/4.9.0` 패키지 소스의 [서비스 인덱스](service-index.md)에 있는 리소스의 속성 값입니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="af6a4-115">아래 설명서의 경우에는 nuget.exe의 URL이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="af6a4-116">`https://www.nuget.org/api/v2/symbolpackage`서비스 인덱스에 있는 값에 대 한 자리 표시자로 간주 `@id` 합니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="af6a4-117">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="af6a4-117">HTTP methods</span></span>

<span data-ttu-id="af6a4-118">`PUT`이 리소스에서 HTTP 메서드가 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="af6a4-119">기호 패키지 푸시</span><span class="sxs-lookup"><span data-stu-id="af6a4-119">Push a symbol package</span></span>

<span data-ttu-id="af6a4-120">nuget.org은 다음 API를 사용 하 여 새 기호 패키지 형식 ([snupkg](../create-packages/Symbol-Packages-snupkg.md))을 푸시하는 것을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

```
PUT https://www.nuget.org/api/v2/symbolpackage
```

<span data-ttu-id="af6a4-121">ID와 버전이 같은 기호 패키지는 여러 번 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="af6a4-122">기호 패키지는 다음과 같은 경우에 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="af6a4-123">ID와 버전이 같은 패키지가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="af6a4-124">ID와 버전이 동일한 기호 패키지를 푸시 했지만 아직 게시 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="af6a4-125">기호 패키지 ([snupkg](../create-packages/Symbol-Packages-snupkg.md))가 잘못 되었습니다 ( [기호 패키지 제약 조건](../create-packages/Symbol-Packages-snupkg.md)참조).</span><span class="sxs-lookup"><span data-stu-id="af6a4-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="af6a4-126">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="af6a4-126">Request parameters</span></span>

<span data-ttu-id="af6a4-127">Name</span><span class="sxs-lookup"><span data-stu-id="af6a4-127">Name</span></span>           | <span data-ttu-id="af6a4-128">In(다음 안에)</span><span class="sxs-lookup"><span data-stu-id="af6a4-128">In</span></span>     | <span data-ttu-id="af6a4-129">Type</span><span class="sxs-lookup"><span data-stu-id="af6a4-129">Type</span></span>   | <span data-ttu-id="af6a4-130">필수</span><span class="sxs-lookup"><span data-stu-id="af6a4-130">Required</span></span> | <span data-ttu-id="af6a4-131">메모</span><span class="sxs-lookup"><span data-stu-id="af6a4-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="af6a4-132">X NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="af6a4-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="af6a4-133">헤더</span><span class="sxs-lookup"><span data-stu-id="af6a4-133">Header</span></span> | <span data-ttu-id="af6a4-134">문자열</span><span class="sxs-lookup"><span data-stu-id="af6a4-134">string</span></span> | <span data-ttu-id="af6a4-135">예</span><span class="sxs-lookup"><span data-stu-id="af6a4-135">yes</span></span>      | <span data-ttu-id="af6a4-136">예를 들어 `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="af6a4-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="af6a4-137">API 키는 사용자가 패키지 원본에서 가져온 불투명 문자열이 며 클라이언트에 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="af6a4-138">특정 문자열 형식은 지정 되지 않지만 API 키의 길이는 HTTP 헤더 값에 대 한 적절 한 크기를 초과 하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="af6a4-139">요청 본문</span><span class="sxs-lookup"><span data-stu-id="af6a4-139">Request body</span></span>

<span data-ttu-id="af6a4-140">기호 푸시에 대 한 요청 본문은 패키지 푸시 요청의 요청 본문을 사용 하는 것과 같습니다. [패키지 푸시 및 삭제](package-publish-resource.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="af6a4-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="af6a4-141">응답</span><span class="sxs-lookup"><span data-stu-id="af6a4-141">Response</span></span>

<span data-ttu-id="af6a4-142">상태 코드</span><span class="sxs-lookup"><span data-stu-id="af6a4-142">Status Code</span></span> | <span data-ttu-id="af6a4-143">의미</span><span class="sxs-lookup"><span data-stu-id="af6a4-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="af6a4-144">201</span><span class="sxs-lookup"><span data-stu-id="af6a4-144">201</span></span>         | <span data-ttu-id="af6a4-145">기호 패키지를 푸시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="af6a4-146">400</span><span class="sxs-lookup"><span data-stu-id="af6a4-146">400</span></span>         | <span data-ttu-id="af6a4-147">제공 된 기호 패키지가 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="af6a4-148">401</span><span class="sxs-lookup"><span data-stu-id="af6a4-148">401</span></span>         | <span data-ttu-id="af6a4-149">사용자에 게이 작업을 수행할 수 있는 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="af6a4-150">404</span><span class="sxs-lookup"><span data-stu-id="af6a4-150">404</span></span>         | <span data-ttu-id="af6a4-151">제공 된 ID 및 버전의 해당 패키지가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="af6a4-152">409</span><span class="sxs-lookup"><span data-stu-id="af6a4-152">409</span></span>         | <span data-ttu-id="af6a4-153">제공 된 ID와 버전을 포함 하는 기호 패키지를 푸시 했지만 아직 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="af6a4-154">413</span><span class="sxs-lookup"><span data-stu-id="af6a4-154">413</span></span>         | <span data-ttu-id="af6a4-155">패키지가 너무 깁니다.</span><span class="sxs-lookup"><span data-stu-id="af6a4-155">The package is too large.</span></span>

