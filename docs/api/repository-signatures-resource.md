---
title: 리포지토리 서명, NuGet API | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: 리포지토리 서명을 리소스 클라이언트 기능을 서명 하는 리포지토리의 기쁘게 패키지 소스를 수 있습니다.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: ea318446c41a0d85d3fbf959dd38c929a0d0e9a1
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2019
ms.locfileid: "59509024"
---
# <a name="repository-signatures"></a><span data-ttu-id="452f3-103">리포지토리 서명</span><span class="sxs-lookup"><span data-stu-id="452f3-103">Repository signatures</span></span>

<span data-ttu-id="452f3-104">패키지 원본에서 게시 된 패키지에 추가 리포지토리 서명의 지 원하는 경우 패키지 원본에서 사용 되는 서명 인증서를 확인 하려면 클라이언트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="452f3-105">이 리소스에 클라이언트를 패키지 변조 또는 예기치 않은 서명 인증서가 포함 된 리포지토리를 서명할지 여부를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="452f3-106">이 리포지토리 서명 정보를 가져오는 중에 사용 되는 리소스를 `RepositorySignatures` 에서 리소스를 찾을 합니다 [서비스 인덱스](service-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="452f3-107">버전 관리</span><span class="sxs-lookup"><span data-stu-id="452f3-107">Versioning</span></span>

<span data-ttu-id="452f3-108">다음 `@type` 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-108">The following `@type` value is used:</span></span>

<span data-ttu-id="452f3-109">@type 값</span><span class="sxs-lookup"><span data-stu-id="452f3-109">@type value</span></span>                | <span data-ttu-id="452f3-110">노트</span><span class="sxs-lookup"><span data-stu-id="452f3-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="452f3-111">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="452f3-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="452f3-112">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="452f3-112">The initial release</span></span>
<span data-ttu-id="452f3-113">RepositorySignatures/4.9.0</span><span class="sxs-lookup"><span data-stu-id="452f3-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="452f3-114">NuGet v4.9 + 클라이언트 지원</span><span class="sxs-lookup"><span data-stu-id="452f3-114">Supported by NuGet v4.9+ clients</span></span>
<span data-ttu-id="452f3-115">RepositorySignatures/5.0.0</span><span class="sxs-lookup"><span data-stu-id="452f3-115">RepositorySignatures/5.0.0</span></span> | <span data-ttu-id="452f3-116">사용 하도록 설정 하면 허용 `allRepositorySigned`합니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-116">Allows enabling `allRepositorySigned`.</span></span> <span data-ttu-id="452f3-117">NuGet v5.0 + 클라이언트 지원</span><span class="sxs-lookup"><span data-stu-id="452f3-117">Supported by NuGet v5.0+ clients</span></span>

## <a name="base-url"></a><span data-ttu-id="452f3-118">기준 URL</span><span class="sxs-lookup"><span data-stu-id="452f3-118">Base URL</span></span>

<span data-ttu-id="452f3-119">다음 Api에 대 한 항목 지점 URL의 값인 합니다 `@id` 앞에서 언급 한 리소스와 연결 된 속성 `@type` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-119">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="452f3-120">자리 표시자 URL을 사용 하 여이 항목에서는 `{@id}`합니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-120">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="452f3-121">다른 리소스와 달리는 `{@id}` URL은 HTTPS를 통해 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-121">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="452f3-122">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="452f3-122">HTTP methods</span></span>

<span data-ttu-id="452f3-123">리포지토리 서명 리소스 지원만 HTTP 메서드에서 발견 한 모든 Url `GET` 고 `HEAD`입니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-123">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="452f3-124">저장소 서명 인덱스</span><span class="sxs-lookup"><span data-stu-id="452f3-124">Repository signatures index</span></span>

<span data-ttu-id="452f3-125">저장소 서명을 인덱스는 두 가지 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-125">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="452f3-126">이 패키지 원본에서 서명 하는 리포지토리는 여부를 모든 패키지에 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-126">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="452f3-127">패키지를 패키지 원본에서 사용 되는 인증서의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-127">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="452f3-128">대부분의 경우에서 인증서 목록에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-128">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="452f3-129">새 인증서 이전 서명 인증서가 만료 및 패키지 원본에서 새 서명 인증서를 사용 하 여 시작 해야 하는 경우 목록에 추가할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-129">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="452f3-130">경우는 인증서는 제거 서명 인증서를 사용 하 여 만든 모든 패키지 서명을 해야 더 이상 유효 하지 클라이언트에서 의미 하는 목록에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-130">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="452f3-131">이 경우 패키지 서명을 (반드시 패키지) 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-131">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="452f3-132">클라이언트 정책으로 서명 되지 않은 패키지를 설치 하 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-132">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="452f3-133">인증서 해지 (예: 키 손상)의 경우 패키지 소스는 영향을 받는 인증서로 서명 된 모든 패키지를 다시 서명 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-133">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="452f3-134">또한 패키지 원본을 서명 인증서 목록에서 영향을 받는 인증서를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-134">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="452f3-135">다음 요청은 리포지토리 서명을 인덱스를 페치합니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-135">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="452f3-136">저장소 서명 인덱스는 다음 속성을 가진 개체를 포함 하는 JSON 문서:</span><span class="sxs-lookup"><span data-stu-id="452f3-136">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="452f3-137">이름</span><span class="sxs-lookup"><span data-stu-id="452f3-137">Name</span></span>                | <span data-ttu-id="452f3-138">형식</span><span class="sxs-lookup"><span data-stu-id="452f3-138">Type</span></span>             | <span data-ttu-id="452f3-139">필수</span><span class="sxs-lookup"><span data-stu-id="452f3-139">Required</span></span> | <span data-ttu-id="452f3-140">노트</span><span class="sxs-lookup"><span data-stu-id="452f3-140">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="452f3-141">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="452f3-141">allRepositorySigned</span></span> | <span data-ttu-id="452f3-142">boolean</span><span class="sxs-lookup"><span data-stu-id="452f3-142">boolean</span></span>          | <span data-ttu-id="452f3-143">예</span><span class="sxs-lookup"><span data-stu-id="452f3-143">yes</span></span>      | <span data-ttu-id="452f3-144">해야 `false` 4.7.0 및 4.9.0 리소스</span><span class="sxs-lookup"><span data-stu-id="452f3-144">Must be `false` on 4.7.0 and 4.9.0 resources</span></span>
<span data-ttu-id="452f3-145">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="452f3-145">signingCertificates</span></span> | <span data-ttu-id="452f3-146">개체의 배열</span><span class="sxs-lookup"><span data-stu-id="452f3-146">array of objects</span></span> | <span data-ttu-id="452f3-147">예</span><span class="sxs-lookup"><span data-stu-id="452f3-147">yes</span></span>      | 

<span data-ttu-id="452f3-148">`allRepositorySigned` 패키지 원본 리포지토리 서명이 있는 일부 패키지가 있으면 부울 false로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-148">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="452f3-149">원본에서 언급 한 서명 인증서 중 하나에서 생성 된 리포지토리 서명이 있어야 부울에서 사용 가능한 모든 패키지를 true로 설정 된 경우 `signingCertificates`합니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-149">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="452f3-150">`allRepositorySigned` 부울 4.7.0 및 4.9.0 리소스에 false 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-150">The `allRepositorySigned` boolean must be false on the 4.7.0 and 4.9.0 resources.</span></span> <span data-ttu-id="452f3-151">NuGet v4.7, v4.8, 및 v4.9 클라이언트가 있는 원본에서 패키지를 설치할 수 없습니다 `allRepositorySigned` true로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-151">NuGet v4.7, v4.8, and v4.9 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="452f3-152">서명 인증서를 하나 이상 있어야 합니다 `signingCertificates` 배열을 `allRepositorySigned` 부울 설정 되어 true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-152">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="452f3-153">배열이 비어 있는 경우 및 `allRepositorySigned` 로 설정 된 true 이면 모든 패키지 소스에서 고려해 야 잘못 된 경우에 클라이언트 정책을 여전히 패키지의 사용을 허용 하지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-153">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="452f3-154">이 배열의 각 요소에는 다음 속성을 사용 하 여 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-154">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="452f3-155">이름</span><span class="sxs-lookup"><span data-stu-id="452f3-155">Name</span></span>         | <span data-ttu-id="452f3-156">형식</span><span class="sxs-lookup"><span data-stu-id="452f3-156">Type</span></span>   | <span data-ttu-id="452f3-157">필수</span><span class="sxs-lookup"><span data-stu-id="452f3-157">Required</span></span> | <span data-ttu-id="452f3-158">노트</span><span class="sxs-lookup"><span data-stu-id="452f3-158">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="452f3-159">contentUrl</span><span class="sxs-lookup"><span data-stu-id="452f3-159">contentUrl</span></span>   | <span data-ttu-id="452f3-160">string</span><span class="sxs-lookup"><span data-stu-id="452f3-160">string</span></span> | <span data-ttu-id="452f3-161">예</span><span class="sxs-lookup"><span data-stu-id="452f3-161">yes</span></span>      | <span data-ttu-id="452f3-162">DER로 인코딩된 공용 인증서에 절대 URL</span><span class="sxs-lookup"><span data-stu-id="452f3-162">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="452f3-163">지문</span><span class="sxs-lookup"><span data-stu-id="452f3-163">fingerprints</span></span> | <span data-ttu-id="452f3-164">object</span><span class="sxs-lookup"><span data-stu-id="452f3-164">object</span></span> | <span data-ttu-id="452f3-165">예</span><span class="sxs-lookup"><span data-stu-id="452f3-165">yes</span></span>      |
<span data-ttu-id="452f3-166">제목</span><span class="sxs-lookup"><span data-stu-id="452f3-166">subject</span></span>      | <span data-ttu-id="452f3-167">string</span><span class="sxs-lookup"><span data-stu-id="452f3-167">string</span></span> | <span data-ttu-id="452f3-168">예</span><span class="sxs-lookup"><span data-stu-id="452f3-168">yes</span></span>      | <span data-ttu-id="452f3-169">인증서의 주체 고유 이름</span><span class="sxs-lookup"><span data-stu-id="452f3-169">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="452f3-170">issuer</span><span class="sxs-lookup"><span data-stu-id="452f3-170">issuer</span></span>       | <span data-ttu-id="452f3-171">string</span><span class="sxs-lookup"><span data-stu-id="452f3-171">string</span></span> | <span data-ttu-id="452f3-172">예</span><span class="sxs-lookup"><span data-stu-id="452f3-172">yes</span></span>      | <span data-ttu-id="452f3-173">인증서의 발급자의 고유 이름</span><span class="sxs-lookup"><span data-stu-id="452f3-173">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="452f3-174">notBefore</span><span class="sxs-lookup"><span data-stu-id="452f3-174">notBefore</span></span>    | <span data-ttu-id="452f3-175">string</span><span class="sxs-lookup"><span data-stu-id="452f3-175">string</span></span> | <span data-ttu-id="452f3-176">예</span><span class="sxs-lookup"><span data-stu-id="452f3-176">yes</span></span>      | <span data-ttu-id="452f3-177">인증서의 유효 기간의 시작 타임 스탬프</span><span class="sxs-lookup"><span data-stu-id="452f3-177">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="452f3-178">notAfter</span><span class="sxs-lookup"><span data-stu-id="452f3-178">notAfter</span></span>     | <span data-ttu-id="452f3-179">string</span><span class="sxs-lookup"><span data-stu-id="452f3-179">string</span></span> | <span data-ttu-id="452f3-180">예</span><span class="sxs-lookup"><span data-stu-id="452f3-180">yes</span></span>      | <span data-ttu-id="452f3-181">인증서의 유효 기간의 끝 타임 스탬프</span><span class="sxs-lookup"><span data-stu-id="452f3-181">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="452f3-182">`contentUrl` 는 HTTPS를 통해 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-182">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="452f3-183">이 URL 없는 특정 URL 패턴과 있으며이 저장소 서명을 인덱스 문서를 사용 하 여 동적으로 검색 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-183">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="452f3-184">이 개체의 모든 속성 (보인다는 `contentUrl`)에 있는 인증서에서 결과 해야 `contentUrl`합니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-184">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="452f3-185">이러한 결과 속성 왕복을 최소화 하기 위해 편의상 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-185">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="452f3-186">`fingerprints` 개체에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-186">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="452f3-187">이름</span><span class="sxs-lookup"><span data-stu-id="452f3-187">Name</span></span>                   | <span data-ttu-id="452f3-188">형식</span><span class="sxs-lookup"><span data-stu-id="452f3-188">Type</span></span>   | <span data-ttu-id="452f3-189">필수</span><span class="sxs-lookup"><span data-stu-id="452f3-189">Required</span></span> | <span data-ttu-id="452f3-190">노트</span><span class="sxs-lookup"><span data-stu-id="452f3-190">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="452f3-191">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="452f3-191">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="452f3-192">string</span><span class="sxs-lookup"><span data-stu-id="452f3-192">string</span></span> | <span data-ttu-id="452f3-193">예</span><span class="sxs-lookup"><span data-stu-id="452f3-193">yes</span></span>      | <span data-ttu-id="452f3-194">SHA-256 지문</span><span class="sxs-lookup"><span data-stu-id="452f3-194">The SHA-256 fingerprint</span></span>

<span data-ttu-id="452f3-195">키 이름 `2.16.840.1.101.3.4.2.1` 는 SHA-256 해시 알고리즘의 OID입니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-195">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="452f3-196">모든 해시 값에는 해시 다이제스트의 소문자 16 진수로 인코딩된 문자열 표현 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="452f3-196">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="452f3-197">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="452f3-197">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="452f3-198">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="452f3-198">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
