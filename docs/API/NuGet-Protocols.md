---
title: "nuget.org 프로토콜 | Microsoft Docs"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba1d9742-9f1c-42ff-8c30-8e953e23c501
description: "NuGet 클라이언트와 상호 작용할 수 발전 nuget.org 프로토콜입니다."
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 097b7a86d056b692c52d6de76bc2fb99d1b58c6f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="ba8a8-103">nuget.org 프로토콜</span><span class="sxs-lookup"><span data-stu-id="ba8a8-103">nuget.org Protocols</span></span>

<span data-ttu-id="ba8a8-104">Nuget.org를 상호작용 하려면 클라이언트를 특정 프로토콜을 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="ba8a8-105">이러한 프로토콜 진화 유지 하기 때문에 클라이언트가 특정 nuget.org Api를 호출할 때 사용 하 여 프로토콜 버전을 식별 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="ba8a8-106">이렇게 하면 이전 클라이언트에 대 한 줄 바꿈하지 않는 방식으로 변경 내용을 소개 하기 위한 nuget.org가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="ba8a8-107">이 페이지에서 설명 하는 Api nuget.org 관련이 이며 이러한 Api를 소개 하기 위한 다른 NuGet 서버 구현에 없는 기대 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="ba8a8-108">NuGet 에코 시스템에서 광범위 하 게 구현 하는 NuGet API에 대 한 정보를 참조 하십시오.는 [API 개요](overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="ba8a8-109">이 항목으로 다양 한 프로토콜 및 존재에 나올 때 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="ba8a8-110">NuGet 프로토콜 버전 4.1.0</span><span class="sxs-lookup"><span data-stu-id="ba8a8-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="ba8a8-111">4.1.0 프로토콜 확인 범위 nuget.org nuget.org 계정에 대해 패키지의 유효성 검사를 제외한 다른 서비스와 상호 작용 하는 키의 사용을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="ba8a8-112">`4.1.0` 버전 번호는 불투명 문자열 이지만이 프로토콜을 지원 하는 공식 NuGet 클라이언트의 첫 번째 버전과 일치 하 게 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="ba8a8-113">유효성 검사를 수행 하면 사용자가 만든 API 키, nuget.org에만 사용 됩니다이 다른 확인 또는 제 3 자 서비스에서 유효성 검사 일회용 범위 확인 키를 통해 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="ba8a8-114">패키지 nuget.org에 있는 특정 사용자 (계정)에 속해 있는지 확인 하 이러한 범위 확인 키를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="ba8a8-115">클라이언트 요구 사항</span><span class="sxs-lookup"><span data-stu-id="ba8a8-115">Client requirement</span></span>

<span data-ttu-id="ba8a8-116">클라이언트에 대 한 API 호출을 할 때 다음 헤더를 전달 하는 데 필요한 **푸시** nuget.org 패키지:</span><span class="sxs-lookup"><span data-stu-id="ba8a8-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="ba8a8-117">기존 `X-NuGet-Client-Version` 헤더 같은 목적에 있지만 현재 사용 되지 않으며 더 이상 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-117">Note that the pre-existing `X-NuGet-Client-Version` header has the same purpose but is now deprecated and should no longer be used.</span></span>

<span data-ttu-id="ba8a8-118">**푸시** 프로토콜 자체에 대 한 설명서에서 설명 된 [ `PackagePublish` 리소스](package-publish-resource.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-118">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="ba8a8-119">외부 서비스 및 패키지 특정 사용자 (계정)에 속하는지 여부를 확인 하는 요구와 클라이언트 상호 작용을 하는 경우 다음 프로토콜을 사용 하 고 확인 범위 키 및 하지 nuget.org에서 API 키를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-119">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="ba8a8-120">범위 확인 키를 요청 하는 API</span><span class="sxs-lookup"><span data-stu-id="ba8a8-120">API to request a verify-scope key</span></span>

<span data-ttu-id="ba8a8-121">이 API는 즉 사용자가 소유 하는 패키지의 유효성 검사에 nuget.org 작성자에 대 한 범위 확인 키를 가져오는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-121">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="ba8a8-122">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="ba8a8-122">Request parameters</span></span>

<span data-ttu-id="ba8a8-123">이름</span><span class="sxs-lookup"><span data-stu-id="ba8a8-123">Name</span></span>           | <span data-ttu-id="ba8a8-124">입력</span><span class="sxs-lookup"><span data-stu-id="ba8a8-124">In</span></span>     | <span data-ttu-id="ba8a8-125">형식</span><span class="sxs-lookup"><span data-stu-id="ba8a8-125">Type</span></span>   | <span data-ttu-id="ba8a8-126">필수</span><span class="sxs-lookup"><span data-stu-id="ba8a8-126">Required</span></span> | <span data-ttu-id="ba8a8-127">참고</span><span class="sxs-lookup"><span data-stu-id="ba8a8-127">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="ba8a8-128">ID</span><span class="sxs-lookup"><span data-stu-id="ba8a8-128">ID</span></span>             | <span data-ttu-id="ba8a8-129">URL</span><span class="sxs-lookup"><span data-stu-id="ba8a8-129">URL</span></span>    | <span data-ttu-id="ba8a8-130">string</span><span class="sxs-lookup"><span data-stu-id="ba8a8-130">string</span></span> | <span data-ttu-id="ba8a8-131">예</span><span class="sxs-lookup"><span data-stu-id="ba8a8-131">yes</span></span>      | <span data-ttu-id="ba8a8-132">범위 확인 키를 요청한 대상 패키지 identidier</span><span class="sxs-lookup"><span data-stu-id="ba8a8-132">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="ba8a8-133">VERSION</span><span class="sxs-lookup"><span data-stu-id="ba8a8-133">VERSION</span></span>        | <span data-ttu-id="ba8a8-134">URL</span><span class="sxs-lookup"><span data-stu-id="ba8a8-134">URL</span></span>    | <span data-ttu-id="ba8a8-135">string</span><span class="sxs-lookup"><span data-stu-id="ba8a8-135">string</span></span> | <span data-ttu-id="ba8a8-136">no</span><span class="sxs-lookup"><span data-stu-id="ba8a8-136">no</span></span>       | <span data-ttu-id="ba8a8-137">패키지 버전</span><span class="sxs-lookup"><span data-stu-id="ba8a8-137">The package version</span></span>
<span data-ttu-id="ba8a8-138">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="ba8a8-138">X-NuGet-ApiKey</span></span> | <span data-ttu-id="ba8a8-139">Header</span><span class="sxs-lookup"><span data-stu-id="ba8a8-139">Header</span></span> | <span data-ttu-id="ba8a8-140">string</span><span class="sxs-lookup"><span data-stu-id="ba8a8-140">string</span></span> | <span data-ttu-id="ba8a8-141">예</span><span class="sxs-lookup"><span data-stu-id="ba8a8-141">yes</span></span>      | <span data-ttu-id="ba8a8-142">예를 들면 `X-NuGet-ApiKey: {USER_API_KEY}`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-142">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="ba8a8-143">응답</span><span class="sxs-lookup"><span data-stu-id="ba8a8-143">Response</span></span>

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="ba8a8-144">범위 확인 키를 확인 하는 API</span><span class="sxs-lookup"><span data-stu-id="ba8a8-144">API to verify the verify scope key</span></span>

<span data-ttu-id="ba8a8-145">이 API는 사용 하 여을 nuget.org 작성자가 소유 하는 패키지에 대 한 범위 확인 키를 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-145">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="ba8a8-146">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="ba8a8-146">Request parameters</span></span>

<span data-ttu-id="ba8a8-147">이름</span><span class="sxs-lookup"><span data-stu-id="ba8a8-147">Name</span></span>           | <span data-ttu-id="ba8a8-148">입력</span><span class="sxs-lookup"><span data-stu-id="ba8a8-148">In</span></span>     | <span data-ttu-id="ba8a8-149">형식</span><span class="sxs-lookup"><span data-stu-id="ba8a8-149">Type</span></span>   | <span data-ttu-id="ba8a8-150">필수</span><span class="sxs-lookup"><span data-stu-id="ba8a8-150">Required</span></span> | <span data-ttu-id="ba8a8-151">참고</span><span class="sxs-lookup"><span data-stu-id="ba8a8-151">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="ba8a8-152">ID</span><span class="sxs-lookup"><span data-stu-id="ba8a8-152">ID</span></span>             | <span data-ttu-id="ba8a8-153">URL</span><span class="sxs-lookup"><span data-stu-id="ba8a8-153">URL</span></span>    | <span data-ttu-id="ba8a8-154">string</span><span class="sxs-lookup"><span data-stu-id="ba8a8-154">string</span></span> | <span data-ttu-id="ba8a8-155">예</span><span class="sxs-lookup"><span data-stu-id="ba8a8-155">yes</span></span>      | <span data-ttu-id="ba8a8-156">범위 확인 키를 요청한 대상 패키지 식별자</span><span class="sxs-lookup"><span data-stu-id="ba8a8-156">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="ba8a8-157">VERSION</span><span class="sxs-lookup"><span data-stu-id="ba8a8-157">VERSION</span></span>        | <span data-ttu-id="ba8a8-158">URL</span><span class="sxs-lookup"><span data-stu-id="ba8a8-158">URL</span></span>    | <span data-ttu-id="ba8a8-159">string</span><span class="sxs-lookup"><span data-stu-id="ba8a8-159">string</span></span> | <span data-ttu-id="ba8a8-160">no</span><span class="sxs-lookup"><span data-stu-id="ba8a8-160">no</span></span>       | <span data-ttu-id="ba8a8-161">패키지 버전</span><span class="sxs-lookup"><span data-stu-id="ba8a8-161">The package version</span></span>
<span data-ttu-id="ba8a8-162">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="ba8a8-162">X-NuGet-ApiKey</span></span> | <span data-ttu-id="ba8a8-163">Header</span><span class="sxs-lookup"><span data-stu-id="ba8a8-163">Header</span></span> | <span data-ttu-id="ba8a8-164">string</span><span class="sxs-lookup"><span data-stu-id="ba8a8-164">string</span></span> | <span data-ttu-id="ba8a8-165">예</span><span class="sxs-lookup"><span data-stu-id="ba8a8-165">yes</span></span>      | <span data-ttu-id="ba8a8-166">예를 들면 `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-166">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="ba8a8-167">이 확인 범위 API 키 날의 시간에 만료 됩니다. 또는 처음 사용할 때 중 먼저 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-167">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="ba8a8-168">응답</span><span class="sxs-lookup"><span data-stu-id="ba8a8-168">Response</span></span>

<span data-ttu-id="ba8a8-169">상태 코드</span><span class="sxs-lookup"><span data-stu-id="ba8a8-169">Status Code</span></span> | <span data-ttu-id="ba8a8-170">의미</span><span class="sxs-lookup"><span data-stu-id="ba8a8-170">Meaning</span></span>
----------- | -------
<span data-ttu-id="ba8a8-171">200</span><span class="sxs-lookup"><span data-stu-id="ba8a8-171">200</span></span>         | <span data-ttu-id="ba8a8-172">API 키가 유효</span><span class="sxs-lookup"><span data-stu-id="ba8a8-172">The API key is valid</span></span>
<span data-ttu-id="ba8a8-173">403</span><span class="sxs-lookup"><span data-stu-id="ba8a8-173">403</span></span>         | <span data-ttu-id="ba8a8-174">API 키가 잘못 되었거나 패키지에 대해 적용할 인증 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="ba8a8-174">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="ba8a8-175">404</span><span class="sxs-lookup"><span data-stu-id="ba8a8-175">404</span></span>         | <span data-ttu-id="ba8a8-176">패키지에서 참조 `ID` 및 `VERSION` (선택 사항) 존재 하지 않는</span><span class="sxs-lookup"><span data-stu-id="ba8a8-176">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
