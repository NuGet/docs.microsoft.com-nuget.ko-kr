---
title: 리포지토리 서명, NuGet API | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: 리포지토리 서명 리소스를 사용 하면 클라이언트 패키지 원본에서 리포지토리 서명 기능을 알릴 수 있습니다.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775332"
---
# <a name="repository-signatures"></a><span data-ttu-id="46f11-103">리포지토리 서명</span><span class="sxs-lookup"><span data-stu-id="46f11-103">Repository signatures</span></span>

<span data-ttu-id="46f11-104">패키지 원본에서 게시 된 패키지에 리포지토리 서명 추가를 지 원하는 경우 클라이언트는 패키지 원본에서 사용 하는 서명 인증서를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="46f11-105">이 리소스를 통해 클라이언트는 리포지토리의 서명 된 패키지가 변조 되었거나 예기치 않은 서명 인증서가 있는지 여부를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="46f11-106">이 리포지토리 서명 정보를 인출 하는 데 사용 되는 리소스는 `RepositorySignatures` [서비스 인덱스](service-index.md)에 있는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="46f11-107">버전 관리</span><span class="sxs-lookup"><span data-stu-id="46f11-107">Versioning</span></span>

<span data-ttu-id="46f11-108">사용 되는 `@type` 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-108">The following `@type` value is used:</span></span>

<span data-ttu-id="46f11-109">@type 값</span><span class="sxs-lookup"><span data-stu-id="46f11-109">@type value</span></span>                | <span data-ttu-id="46f11-110">메모</span><span class="sxs-lookup"><span data-stu-id="46f11-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="46f11-111">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="46f11-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="46f11-112">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="46f11-112">The initial release</span></span>
<span data-ttu-id="46f11-113">RepositorySignatures/4.9.0</span><span class="sxs-lookup"><span data-stu-id="46f11-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="46f11-114">NuGet v 4.9 + 클라이언트에서 지원</span><span class="sxs-lookup"><span data-stu-id="46f11-114">Supported by NuGet v4.9+ clients</span></span>
<span data-ttu-id="46f11-115">RepositorySignatures/5.0.0</span><span class="sxs-lookup"><span data-stu-id="46f11-115">RepositorySignatures/5.0.0</span></span> | <span data-ttu-id="46f11-116">사용 `allRepositorySigned` 을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-116">Allows enabling `allRepositorySigned`.</span></span> <span data-ttu-id="46f11-117">NuGet v 5.0 이상 클라이언트에서 지원 됨</span><span class="sxs-lookup"><span data-stu-id="46f11-117">Supported by NuGet v5.0+ clients</span></span>

## <a name="base-url"></a><span data-ttu-id="46f11-118">기준 URL</span><span class="sxs-lookup"><span data-stu-id="46f11-118">Base URL</span></span>

<span data-ttu-id="46f11-119">다음 Api에 대 한 진입점 URL은 `@id` 앞서 언급 한 리소스 값과 연결 된 속성의 값입니다 `@type` .</span><span class="sxs-lookup"><span data-stu-id="46f11-119">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="46f11-120">이 항목에서는 자리 표시자 URL을 사용 `{@id}` 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-120">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="46f11-121">다른 리소스와 달리 `{@id}` URL은 HTTPS를 통해 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-121">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="46f11-122">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="46f11-122">HTTP methods</span></span>

<span data-ttu-id="46f11-123">리포지토리 서명 리소스에서 찾은 모든 Url은 HTTP 메서드 및만 지원 `GET` 합니다 `HEAD` .</span><span class="sxs-lookup"><span data-stu-id="46f11-123">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="46f11-124">리포지토리 서명 인덱스</span><span class="sxs-lookup"><span data-stu-id="46f11-124">Repository signatures index</span></span>

<span data-ttu-id="46f11-125">리포지토리 서명 인덱스에는 다음과 같은 두 가지 정보가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-125">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="46f11-126">원본에 있는 모든 패키지가이 패키지 소스에서 서명한 리포지토리입니다 여부입니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-126">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="46f11-127">패키지에 서명 하기 위해 패키지 원본에서 사용 하는 인증서 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-127">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="46f11-128">대부분의 경우 인증서 목록은에만 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-128">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="46f11-129">이전 서명 인증서가 만료 되 고 패키지 원본이 새 서명 인증서를 사용 하 여 시작 해야 하는 경우 새 인증서가 목록에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-129">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="46f11-130">인증서가 목록에서 제거 되 면 제거 된 서명 인증서를 사용 하 여 만든 모든 패키지 서명이 더 이상 클라이언트에서 유효한 것으로 간주 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-130">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="46f11-131">이 경우 패키지 서명 (반드시 패키지는 아님)이 유효 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-131">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="46f11-132">클라이언트 정책을 사용 하면 패키지를 unsigned로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-132">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="46f11-133">인증서 해지 (예: 키 손상)의 경우 패키지 원본에서 영향을 받는 인증서로 서명 된 모든 패키지를 다시 서명 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-133">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="46f11-134">또한 패키지 원본은 서명 인증서 목록에서 영향을 받는 인증서를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-134">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="46f11-135">다음 요청은 리포지토리 서명 인덱스를 인출 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-135">The following request fetches the repository signatures index.</span></span>

```
GET {@id}
```

<span data-ttu-id="46f11-136">리포지토리 서명 인덱스는 다음 속성을 포함 하는 개체를 포함 하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-136">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="46f11-137">Name</span><span class="sxs-lookup"><span data-stu-id="46f11-137">Name</span></span>                | <span data-ttu-id="46f11-138">Type</span><span class="sxs-lookup"><span data-stu-id="46f11-138">Type</span></span>             | <span data-ttu-id="46f11-139">필수</span><span class="sxs-lookup"><span data-stu-id="46f11-139">Required</span></span> | <span data-ttu-id="46f11-140">메모</span><span class="sxs-lookup"><span data-stu-id="46f11-140">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="46f11-141">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="46f11-141">allRepositorySigned</span></span> | <span data-ttu-id="46f11-142">boolean</span><span class="sxs-lookup"><span data-stu-id="46f11-142">boolean</span></span>          | <span data-ttu-id="46f11-143">예</span><span class="sxs-lookup"><span data-stu-id="46f11-143">yes</span></span>      | <span data-ttu-id="46f11-144">`false`4.7.0 및 4.9.0 리소스에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-144">Must be `false` on 4.7.0 and 4.9.0 resources</span></span>
<span data-ttu-id="46f11-145">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="46f11-145">signingCertificates</span></span> | <span data-ttu-id="46f11-146">개체의 배열</span><span class="sxs-lookup"><span data-stu-id="46f11-146">array of objects</span></span> | <span data-ttu-id="46f11-147">예</span><span class="sxs-lookup"><span data-stu-id="46f11-147">yes</span></span>      | 

<span data-ttu-id="46f11-148">`allRepositorySigned`패키지 원본에 리포지토리 서명이 없는 일부 패키지가 있는 경우 부울이 false로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-148">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="46f11-149">부울이 true로 설정 된 경우 원본에서 사용할 수 있는 모든 패키지에는에 설명 된 서명 인증서 중 하나에서 생성 한 리포지토리 서명이 있어야 합니다 `signingCertificates` .</span><span class="sxs-lookup"><span data-stu-id="46f11-149">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="46f11-150">`allRepositorySigned`부울은 4.7.0 및 4.9.0 리소스에 대해 false 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-150">The `allRepositorySigned` boolean must be false on the 4.7.0 and 4.9.0 resources.</span></span> <span data-ttu-id="46f11-151">NuGet v 4.7, v 4.8 및 v 4.9 클라이언트는가 true로 설정 된 원본에서 패키지를 설치할 수 없습니다 `allRepositorySigned` .</span><span class="sxs-lookup"><span data-stu-id="46f11-151">NuGet v4.7, v4.8, and v4.9 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="46f11-152">`signingCertificates` `allRepositorySigned` 부울이 true로 설정 된 경우 배열에 하나 이상의 서명 인증서가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-152">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="46f11-153">배열이 비어 있고 `allRepositorySigned` 이 true로 설정 된 경우에도 클라이언트 정책에서 패키지 사용을 허용할 수 있지만 원본의 모든 패키지는 유효 하지 않은 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-153">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="46f11-154">이 배열의 각 요소는 다음 속성을 포함 하는 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-154">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="46f11-155">Name</span><span class="sxs-lookup"><span data-stu-id="46f11-155">Name</span></span>         | <span data-ttu-id="46f11-156">Type</span><span class="sxs-lookup"><span data-stu-id="46f11-156">Type</span></span>   | <span data-ttu-id="46f11-157">필수</span><span class="sxs-lookup"><span data-stu-id="46f11-157">Required</span></span> | <span data-ttu-id="46f11-158">메모</span><span class="sxs-lookup"><span data-stu-id="46f11-158">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="46f11-159">contentUrl</span><span class="sxs-lookup"><span data-stu-id="46f11-159">contentUrl</span></span>   | <span data-ttu-id="46f11-160">문자열</span><span class="sxs-lookup"><span data-stu-id="46f11-160">string</span></span> | <span data-ttu-id="46f11-161">예</span><span class="sxs-lookup"><span data-stu-id="46f11-161">yes</span></span>      | <span data-ttu-id="46f11-162">DER로 인코딩된 공용 인증서의 절대 URL</span><span class="sxs-lookup"><span data-stu-id="46f11-162">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="46f11-163">지문</span><span class="sxs-lookup"><span data-stu-id="46f11-163">fingerprints</span></span> | <span data-ttu-id="46f11-164">개체</span><span class="sxs-lookup"><span data-stu-id="46f11-164">object</span></span> | <span data-ttu-id="46f11-165">예</span><span class="sxs-lookup"><span data-stu-id="46f11-165">yes</span></span>      |
<span data-ttu-id="46f11-166">subject</span><span class="sxs-lookup"><span data-stu-id="46f11-166">subject</span></span>      | <span data-ttu-id="46f11-167">문자열</span><span class="sxs-lookup"><span data-stu-id="46f11-167">string</span></span> | <span data-ttu-id="46f11-168">예</span><span class="sxs-lookup"><span data-stu-id="46f11-168">yes</span></span>      | <span data-ttu-id="46f11-169">인증서의 주체 고유 이름</span><span class="sxs-lookup"><span data-stu-id="46f11-169">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="46f11-170">발급자</span><span class="sxs-lookup"><span data-stu-id="46f11-170">issuer</span></span>       | <span data-ttu-id="46f11-171">문자열</span><span class="sxs-lookup"><span data-stu-id="46f11-171">string</span></span> | <span data-ttu-id="46f11-172">예</span><span class="sxs-lookup"><span data-stu-id="46f11-172">yes</span></span>      | <span data-ttu-id="46f11-173">인증서 발급자의 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-173">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="46f11-174">notBefore</span><span class="sxs-lookup"><span data-stu-id="46f11-174">notBefore</span></span>    | <span data-ttu-id="46f11-175">문자열</span><span class="sxs-lookup"><span data-stu-id="46f11-175">string</span></span> | <span data-ttu-id="46f11-176">예</span><span class="sxs-lookup"><span data-stu-id="46f11-176">yes</span></span>      | <span data-ttu-id="46f11-177">인증서 유효 기간의 시작 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-177">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="46f11-178">notAfter</span><span class="sxs-lookup"><span data-stu-id="46f11-178">notAfter</span></span>     | <span data-ttu-id="46f11-179">문자열</span><span class="sxs-lookup"><span data-stu-id="46f11-179">string</span></span> | <span data-ttu-id="46f11-180">예</span><span class="sxs-lookup"><span data-stu-id="46f11-180">yes</span></span>      | <span data-ttu-id="46f11-181">인증서 유효 기간의 끝 타임 스탬프입니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-181">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="46f11-182">는 HTTPS를 `contentUrl` 통해 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-182">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="46f11-183">이 URL에는 특정 URL 패턴이 없으며이 리포지토리 서명 인덱스 문서를 사용 하 여 동적으로 검색 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-183">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="46f11-184">이 개체의 모든 속성 (제외 `contentUrl` )은에 있는 인증서에서 파생 가능한 해야 합니다 `contentUrl` .</span><span class="sxs-lookup"><span data-stu-id="46f11-184">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="46f11-185">이러한 파생 가능한 속성은 라운드트립을 최소화 하기 위해 편리 하 게 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-185">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="46f11-186">`fingerprints` 개체의 속성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-186">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="46f11-187">Name</span><span class="sxs-lookup"><span data-stu-id="46f11-187">Name</span></span>                   | <span data-ttu-id="46f11-188">Type</span><span class="sxs-lookup"><span data-stu-id="46f11-188">Type</span></span>   | <span data-ttu-id="46f11-189">필수</span><span class="sxs-lookup"><span data-stu-id="46f11-189">Required</span></span> | <span data-ttu-id="46f11-190">메모</span><span class="sxs-lookup"><span data-stu-id="46f11-190">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="46f11-191">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="46f11-191">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="46f11-192">문자열</span><span class="sxs-lookup"><span data-stu-id="46f11-192">string</span></span> | <span data-ttu-id="46f11-193">예</span><span class="sxs-lookup"><span data-stu-id="46f11-193">yes</span></span>      | <span data-ttu-id="46f11-194">SHA-256 지문</span><span class="sxs-lookup"><span data-stu-id="46f11-194">The SHA-256 fingerprint</span></span>

<span data-ttu-id="46f11-195">키 이름은 `2.16.840.1.101.3.4.2.1` SHA-256 해시 알고리즘의 OID입니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-195">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="46f11-196">모든 해시 값은 해시 다이제스트의 소문자, 16 진수로 인코딩된 문자열 표현 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="46f11-196">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="46f11-197">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="46f11-197">Sample request</span></span>

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a><span data-ttu-id="46f11-198">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="46f11-198">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
