---
title: nuget.org 프로토콜
description: NuGet 클라이언트와 상호 작용 하는 진화 하는 nuget.org 프로토콜입니다.
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773980"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="0092a-103">nuget.org 프로토콜</span><span class="sxs-lookup"><span data-stu-id="0092a-103">nuget.org protocols</span></span>

<span data-ttu-id="0092a-104">Nuget.org와 상호 작용 하려면 클라이언트가 특정 프로토콜을 따라야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="0092a-105">이러한 프로토콜은 계속 진화 하기 때문에 클라이언트는 특정 nuget.org Api를 호출할 때 사용 하는 프로토콜 버전을 식별 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="0092a-106">이렇게 하면 nuget.org가 이전 클라이언트에 대해 중단 되지 않는 방식으로 변경 내용을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="0092a-107">이 페이지에서 설명 하는 Api는 nuget.org에만 적용 되며, 다른 NuGet 서버 구현에서 이러한 Api를 도입 하는 것은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="0092a-108">NuGet 에코 시스템에서 광범위 하 게 구현 된 NuGet API에 대 한 자세한 내용은 [API 개요](overview.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0092a-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="0092a-109">이 항목에서는 다양 한 프로토콜의 존재 여부를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="0092a-110">NuGet 프로토콜 버전 4.1.0</span><span class="sxs-lookup"><span data-stu-id="0092a-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="0092a-111">4.1.0 프로토콜은 nuget.org 계정에 대해 패키지의 유효성을 검사 하기 위해 nuget.org 이외의 서비스와 상호 작용 하는 verify 범위 키의 사용을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="0092a-112">`4.1.0`버전 번호는 불투명 문자열 이지만이 프로토콜을 지 원하는 공식 NuGet 클라이언트의 첫 번째 버전과 일치 하는 경우에 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="0092a-113">유효성 검사를 통해 사용자가 만든 API 키는 nuget.org 에서만 사용 되 고 타사 서비스의 다른 확인 또는 유효성 검사는 일회성 사용 확인 범위 키를 통해 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="0092a-114">이러한 검증 범위 키는 패키지가 nuget.org의 특정 사용자 (계정)에 속해 있는지 확인 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="0092a-115">클라이언트 요구 사항</span><span class="sxs-lookup"><span data-stu-id="0092a-115">Client requirement</span></span>

<span data-ttu-id="0092a-116">클라이언트는 nuget.org에 패키지를 **푸시하** 는 API 호출을 수행할 때 다음 헤더를 전달 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="0092a-117">`X-NuGet-Client-Version`헤더의 의미 체계가 유사 하지만 공식 NuGet 클라이언트 에서만 사용 하도록 예약 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="0092a-118">타사 클라이언트는 헤더 및 값을 사용 해야 합니다 `X-NuGet-Protocol-Version` .</span><span class="sxs-lookup"><span data-stu-id="0092a-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="0092a-119">**푸시** 프로토콜 자체는 [ `PackagePublish` 리소스](package-publish-resource.md)에 대 한 설명서에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="0092a-120">클라이언트가 외부 서비스와 상호 작용 하 고 패키지가 특정 사용자 (계정)에 속하는지 여부를 확인 해야 하는 경우 다음 프로토콜을 사용 하 고 nuget.org의 API 키가 아닌 확인 범위 키를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="0092a-121">확인 범위 키를 요청 하는 API</span><span class="sxs-lookup"><span data-stu-id="0092a-121">API to request a verify-scope key</span></span>

<span data-ttu-id="0092a-122">이 API는 nuget.org 작성자가 자신이 소유한 패키지의 유효성을 검사 하기 위한 확인 범위 키를 가져오는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="0092a-123">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="0092a-123">Request parameters</span></span>

<span data-ttu-id="0092a-124">Name</span><span class="sxs-lookup"><span data-stu-id="0092a-124">Name</span></span>           | <span data-ttu-id="0092a-125">In(다음 안에)</span><span class="sxs-lookup"><span data-stu-id="0092a-125">In</span></span>     | <span data-ttu-id="0092a-126">Type</span><span class="sxs-lookup"><span data-stu-id="0092a-126">Type</span></span>   | <span data-ttu-id="0092a-127">필수</span><span class="sxs-lookup"><span data-stu-id="0092a-127">Required</span></span> | <span data-ttu-id="0092a-128">메모</span><span class="sxs-lookup"><span data-stu-id="0092a-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="0092a-129">ID</span><span class="sxs-lookup"><span data-stu-id="0092a-129">ID</span></span>             | <span data-ttu-id="0092a-130">URL</span><span class="sxs-lookup"><span data-stu-id="0092a-130">URL</span></span>    | <span data-ttu-id="0092a-131">문자열</span><span class="sxs-lookup"><span data-stu-id="0092a-131">string</span></span> | <span data-ttu-id="0092a-132">예</span><span class="sxs-lookup"><span data-stu-id="0092a-132">yes</span></span>      | <span data-ttu-id="0092a-133">범위 키 확인이 요청 된 패키지 identidier</span><span class="sxs-lookup"><span data-stu-id="0092a-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="0092a-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="0092a-134">VERSION</span></span>        | <span data-ttu-id="0092a-135">URL</span><span class="sxs-lookup"><span data-stu-id="0092a-135">URL</span></span>    | <span data-ttu-id="0092a-136">문자열</span><span class="sxs-lookup"><span data-stu-id="0092a-136">string</span></span> | <span data-ttu-id="0092a-137">아니요</span><span class="sxs-lookup"><span data-stu-id="0092a-137">no</span></span>       | <span data-ttu-id="0092a-138">패키지 버전</span><span class="sxs-lookup"><span data-stu-id="0092a-138">The package version</span></span>
<span data-ttu-id="0092a-139">X NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="0092a-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="0092a-140">헤더</span><span class="sxs-lookup"><span data-stu-id="0092a-140">Header</span></span> | <span data-ttu-id="0092a-141">문자열</span><span class="sxs-lookup"><span data-stu-id="0092a-141">string</span></span> | <span data-ttu-id="0092a-142">예</span><span class="sxs-lookup"><span data-stu-id="0092a-142">yes</span></span>      | <span data-ttu-id="0092a-143">예를 들어 `X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="0092a-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="0092a-144">응답</span><span class="sxs-lookup"><span data-stu-id="0092a-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="0092a-145">확인 범위 키를 확인 하는 API</span><span class="sxs-lookup"><span data-stu-id="0092a-145">API to verify the verify scope key</span></span>

<span data-ttu-id="0092a-146">이 API는 nuget.org author에서 소유 하는 패키지에 대 한 확인 범위 키의 유효성을 검사 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="0092a-147">요청 매개 변수</span><span class="sxs-lookup"><span data-stu-id="0092a-147">Request parameters</span></span>

<span data-ttu-id="0092a-148">Name</span><span class="sxs-lookup"><span data-stu-id="0092a-148">Name</span></span>           | <span data-ttu-id="0092a-149">In(다음 안에)</span><span class="sxs-lookup"><span data-stu-id="0092a-149">In</span></span>     | <span data-ttu-id="0092a-150">Type</span><span class="sxs-lookup"><span data-stu-id="0092a-150">Type</span></span>   | <span data-ttu-id="0092a-151">필수</span><span class="sxs-lookup"><span data-stu-id="0092a-151">Required</span></span> | <span data-ttu-id="0092a-152">메모</span><span class="sxs-lookup"><span data-stu-id="0092a-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="0092a-153">ID</span><span class="sxs-lookup"><span data-stu-id="0092a-153">ID</span></span>             | <span data-ttu-id="0092a-154">URL</span><span class="sxs-lookup"><span data-stu-id="0092a-154">URL</span></span>    | <span data-ttu-id="0092a-155">문자열</span><span class="sxs-lookup"><span data-stu-id="0092a-155">string</span></span> | <span data-ttu-id="0092a-156">예</span><span class="sxs-lookup"><span data-stu-id="0092a-156">yes</span></span>      | <span data-ttu-id="0092a-157">범위 키 확인이 요청 된 패키지 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="0092a-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="0092a-158">VERSION</span></span>        | <span data-ttu-id="0092a-159">URL</span><span class="sxs-lookup"><span data-stu-id="0092a-159">URL</span></span>    | <span data-ttu-id="0092a-160">문자열</span><span class="sxs-lookup"><span data-stu-id="0092a-160">string</span></span> | <span data-ttu-id="0092a-161">아니요</span><span class="sxs-lookup"><span data-stu-id="0092a-161">no</span></span>       | <span data-ttu-id="0092a-162">패키지 버전</span><span class="sxs-lookup"><span data-stu-id="0092a-162">The package version</span></span>
<span data-ttu-id="0092a-163">X NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="0092a-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="0092a-164">헤더</span><span class="sxs-lookup"><span data-stu-id="0092a-164">Header</span></span> | <span data-ttu-id="0092a-165">문자열</span><span class="sxs-lookup"><span data-stu-id="0092a-165">string</span></span> | <span data-ttu-id="0092a-166">예</span><span class="sxs-lookup"><span data-stu-id="0092a-166">yes</span></span>      | <span data-ttu-id="0092a-167">예를 들어 `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="0092a-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="0092a-168">이 확인 범위 API 키는 하루 중에 만료 되거나 처음 사용 될 때 (어느 쪽이 든 먼저 발생 하는 경우) 만료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="0092a-169">응답</span><span class="sxs-lookup"><span data-stu-id="0092a-169">Response</span></span>

<span data-ttu-id="0092a-170">상태 코드</span><span class="sxs-lookup"><span data-stu-id="0092a-170">Status Code</span></span> | <span data-ttu-id="0092a-171">의미</span><span class="sxs-lookup"><span data-stu-id="0092a-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="0092a-172">200</span><span class="sxs-lookup"><span data-stu-id="0092a-172">200</span></span>         | <span data-ttu-id="0092a-173">API 키가 올바릅니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-173">The API key is valid</span></span>
<span data-ttu-id="0092a-174">403</span><span class="sxs-lookup"><span data-stu-id="0092a-174">403</span></span>         | <span data-ttu-id="0092a-175">API 키가 잘못 되었거나 패키지에 대해 푸시할 수 있는 권한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="0092a-176">404</span><span class="sxs-lookup"><span data-stu-id="0092a-176">404</span></span>         | <span data-ttu-id="0092a-177">`ID`및 `VERSION` (선택 사항)에서 참조 하는 패키지가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0092a-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
