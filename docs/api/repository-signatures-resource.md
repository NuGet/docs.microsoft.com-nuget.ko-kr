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
ms.openlocfilehash: 81d32a7011268e45136e00cdb7345a95070aae06
ms.sourcegitcommit: be9c51b4b095aea40ef41bbea7e12ef0a194ee74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248444"
---
# <a name="repository-signatures"></a><span data-ttu-id="ac990-103">리포지토리 서명</span><span class="sxs-lookup"><span data-stu-id="ac990-103">Repository signatures</span></span>

<span data-ttu-id="ac990-104">패키지 원본에서 게시 된 패키지에 추가 리포지토리 서명의 지 원하는 경우 패키지 원본에서 사용 되는 서명 인증서를 확인 하려면 클라이언트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="ac990-105">이 리소스에 클라이언트를 패키지 변조 또는 예기치 않은 서명 인증서가 포함 된 리포지토리를 서명할지 여부를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="ac990-106">이 리포지토리 서명 정보를 가져오는 중에 사용 되는 리소스를 `RepositorySignatures` 에서 리소스를 찾을 합니다 [서비스 인덱스](service-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="ac990-107">버전 관리</span><span class="sxs-lookup"><span data-stu-id="ac990-107">Versioning</span></span>

<span data-ttu-id="ac990-108">다음 `@type` 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-108">The following `@type` value is used:</span></span>

<span data-ttu-id="ac990-109">@type 값</span><span class="sxs-lookup"><span data-stu-id="ac990-109">@type value</span></span>                | <span data-ttu-id="ac990-110">노트</span><span class="sxs-lookup"><span data-stu-id="ac990-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="ac990-111">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="ac990-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="ac990-112">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="ac990-112">The initial release</span></span>
<span data-ttu-id="ac990-113">RepositorySignatures/4.9.0</span><span class="sxs-lookup"><span data-stu-id="ac990-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="ac990-114">사용 하도록 설정 수 있습니다. `allRepositorySigned`</span><span class="sxs-lookup"><span data-stu-id="ac990-114">Allows enabling `allRepositorySigned`</span></span>

## <a name="base-url"></a><span data-ttu-id="ac990-115">기준 URL</span><span class="sxs-lookup"><span data-stu-id="ac990-115">Base URL</span></span>

<span data-ttu-id="ac990-116">다음 Api에 대 한 항목 지점 URL의 값인 합니다 `@id` 앞에서 언급 한 리소스와 연결 된 속성 `@type` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-116">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="ac990-117">자리 표시자 URL을 사용 하 여이 항목에서는 `{@id}`합니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-117">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="ac990-118">다른 리소스와 달리는 `{@id}` URL은 HTTPS를 통해 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-118">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="ac990-119">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="ac990-119">HTTP methods</span></span>

<span data-ttu-id="ac990-120">리포지토리 서명 리소스 지원만 HTTP 메서드에서 발견 한 모든 Url `GET` 고 `HEAD`입니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-120">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="ac990-121">저장소 서명 인덱스</span><span class="sxs-lookup"><span data-stu-id="ac990-121">Repository signatures index</span></span>

<span data-ttu-id="ac990-122">저장소 서명을 인덱스는 두 가지 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-122">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="ac990-123">이 패키지 원본에서 서명 하는 리포지토리는 여부를 모든 패키지에 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-123">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="ac990-124">패키지를 패키지 원본에서 사용 되는 인증서의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-124">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="ac990-125">대부분의 경우에서 인증서 목록에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-125">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="ac990-126">새 인증서 이전 서명 인증서가 만료 및 패키지 원본에서 새 서명 인증서를 사용 하 여 시작 해야 하는 경우 목록에 추가할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-126">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="ac990-127">경우는 인증서는 제거 서명 인증서를 사용 하 여 만든 모든 패키지 서명을 해야 더 이상 유효 하지 클라이언트에서 의미 하는 목록에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-127">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="ac990-128">이 경우 패키지 서명을 (반드시 패키지) 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-128">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="ac990-129">클라이언트 정책으로 서명 되지 않은 패키지를 설치 하 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-129">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="ac990-130">인증서 해지 (예: 키 손상)의 경우 패키지 소스는 영향을 받는 인증서로 서명 된 모든 패키지를 다시 서명 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-130">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="ac990-131">또한 패키지 원본을 서명 인증서 목록에서 영향을 받는 인증서를 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-131">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="ac990-132">다음 요청은 리포지토리 서명을 인덱스를 페치합니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-132">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="ac990-133">저장소 서명 인덱스는 다음 속성을 가진 개체를 포함 하는 JSON 문서:</span><span class="sxs-lookup"><span data-stu-id="ac990-133">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="ac990-134">이름</span><span class="sxs-lookup"><span data-stu-id="ac990-134">Name</span></span>                | <span data-ttu-id="ac990-135">형식</span><span class="sxs-lookup"><span data-stu-id="ac990-135">Type</span></span>             | <span data-ttu-id="ac990-136">필수</span><span class="sxs-lookup"><span data-stu-id="ac990-136">Required</span></span> | <span data-ttu-id="ac990-137">노트</span><span class="sxs-lookup"><span data-stu-id="ac990-137">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="ac990-138">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="ac990-138">allRepositorySigned</span></span> | <span data-ttu-id="ac990-139">boolean</span><span class="sxs-lookup"><span data-stu-id="ac990-139">boolean</span></span>          | <span data-ttu-id="ac990-140">예</span><span class="sxs-lookup"><span data-stu-id="ac990-140">yes</span></span>      | <span data-ttu-id="ac990-141">해야 `false` 4.7.0에서 리소스</span><span class="sxs-lookup"><span data-stu-id="ac990-141">Must be `false` on 4.7.0 resource</span></span>
<span data-ttu-id="ac990-142">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="ac990-142">signingCertificates</span></span> | <span data-ttu-id="ac990-143">개체의 배열</span><span class="sxs-lookup"><span data-stu-id="ac990-143">array of objects</span></span> | <span data-ttu-id="ac990-144">예</span><span class="sxs-lookup"><span data-stu-id="ac990-144">yes</span></span>      | 

<span data-ttu-id="ac990-145">`allRepositorySigned` 패키지 원본 리포지토리 서명이 있는 일부 패키지가 있으면 부울 false로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-145">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="ac990-146">원본에서 언급 한 서명 인증서 중 하나에서 생성 된 리포지토리 서명이 있어야 부울에서 사용 가능한 모든 패키지를 true로 설정 된 경우 `signingCertificates`합니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-146">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="ac990-147">`allRepositorySigned` 부울는 4.7.0에 false 이어야 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-147">The `allRepositorySigned` boolean must be false on the 4.7.0 resource.</span></span> <span data-ttu-id="ac990-148">NuGet v4.7 및 v4.8 클라이언트가 있는 원본에서 패키지를 설치할 수 없습니다 `allRepositorySigned` true로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-148">NuGet v4.7 and v4.8 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="ac990-149">서명 인증서를 하나 이상 있어야 합니다 `signingCertificates` 배열을 `allRepositorySigned` 부울 설정 되어 true로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-149">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="ac990-150">배열이 비어 있는 경우 및 `allRepositorySigned` 로 설정 된 true 이면 모든 패키지 소스에서 고려해 야 잘못 된 경우에 클라이언트 정책을 여전히 패키지의 사용을 허용 하지만 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-150">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="ac990-151">이 배열의 각 요소에는 다음 속성을 사용 하 여 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-151">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="ac990-152">이름</span><span class="sxs-lookup"><span data-stu-id="ac990-152">Name</span></span>         | <span data-ttu-id="ac990-153">형식</span><span class="sxs-lookup"><span data-stu-id="ac990-153">Type</span></span>   | <span data-ttu-id="ac990-154">필수</span><span class="sxs-lookup"><span data-stu-id="ac990-154">Required</span></span> | <span data-ttu-id="ac990-155">노트</span><span class="sxs-lookup"><span data-stu-id="ac990-155">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="ac990-156">contentUrl</span><span class="sxs-lookup"><span data-stu-id="ac990-156">contentUrl</span></span>   | <span data-ttu-id="ac990-157">string</span><span class="sxs-lookup"><span data-stu-id="ac990-157">string</span></span> | <span data-ttu-id="ac990-158">예</span><span class="sxs-lookup"><span data-stu-id="ac990-158">yes</span></span>      | <span data-ttu-id="ac990-159">DER로 인코딩된 공용 인증서에 절대 URL</span><span class="sxs-lookup"><span data-stu-id="ac990-159">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="ac990-160">지문</span><span class="sxs-lookup"><span data-stu-id="ac990-160">fingerprints</span></span> | <span data-ttu-id="ac990-161">object</span><span class="sxs-lookup"><span data-stu-id="ac990-161">object</span></span> | <span data-ttu-id="ac990-162">예</span><span class="sxs-lookup"><span data-stu-id="ac990-162">yes</span></span>      |
<span data-ttu-id="ac990-163">제목</span><span class="sxs-lookup"><span data-stu-id="ac990-163">subject</span></span>      | <span data-ttu-id="ac990-164">string</span><span class="sxs-lookup"><span data-stu-id="ac990-164">string</span></span> | <span data-ttu-id="ac990-165">예</span><span class="sxs-lookup"><span data-stu-id="ac990-165">yes</span></span>      | <span data-ttu-id="ac990-166">인증서의 주체 고유 이름</span><span class="sxs-lookup"><span data-stu-id="ac990-166">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="ac990-167">issuer</span><span class="sxs-lookup"><span data-stu-id="ac990-167">issuer</span></span>       | <span data-ttu-id="ac990-168">string</span><span class="sxs-lookup"><span data-stu-id="ac990-168">string</span></span> | <span data-ttu-id="ac990-169">예</span><span class="sxs-lookup"><span data-stu-id="ac990-169">yes</span></span>      | <span data-ttu-id="ac990-170">인증서의 발급자의 고유 이름</span><span class="sxs-lookup"><span data-stu-id="ac990-170">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="ac990-171">notBefore</span><span class="sxs-lookup"><span data-stu-id="ac990-171">notBefore</span></span>    | <span data-ttu-id="ac990-172">string</span><span class="sxs-lookup"><span data-stu-id="ac990-172">string</span></span> | <span data-ttu-id="ac990-173">예</span><span class="sxs-lookup"><span data-stu-id="ac990-173">yes</span></span>      | <span data-ttu-id="ac990-174">인증서의 유효 기간의 시작 타임 스탬프</span><span class="sxs-lookup"><span data-stu-id="ac990-174">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="ac990-175">notAfter</span><span class="sxs-lookup"><span data-stu-id="ac990-175">notAfter</span></span>     | <span data-ttu-id="ac990-176">string</span><span class="sxs-lookup"><span data-stu-id="ac990-176">string</span></span> | <span data-ttu-id="ac990-177">예</span><span class="sxs-lookup"><span data-stu-id="ac990-177">yes</span></span>      | <span data-ttu-id="ac990-178">인증서의 유효 기간의 끝 타임 스탬프</span><span class="sxs-lookup"><span data-stu-id="ac990-178">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="ac990-179">`contentUrl` 는 HTTPS를 통해 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-179">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="ac990-180">이 URL 없는 특정 URL 패턴과 있으며이 저장소 서명을 인덱스 문서를 사용 하 여 동적으로 검색 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-180">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="ac990-181">이 개체의 모든 속성 (보인다는 `contentUrl`)에 있는 인증서에서 결과 해야 `contentUrl`합니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-181">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="ac990-182">이러한 결과 속성 왕복을 최소화 하기 위해 편의상 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-182">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="ac990-183">`fingerprints` 개체에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-183">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="ac990-184">이름</span><span class="sxs-lookup"><span data-stu-id="ac990-184">Name</span></span>                   | <span data-ttu-id="ac990-185">형식</span><span class="sxs-lookup"><span data-stu-id="ac990-185">Type</span></span>   | <span data-ttu-id="ac990-186">필수</span><span class="sxs-lookup"><span data-stu-id="ac990-186">Required</span></span> | <span data-ttu-id="ac990-187">노트</span><span class="sxs-lookup"><span data-stu-id="ac990-187">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="ac990-188">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="ac990-188">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="ac990-189">string</span><span class="sxs-lookup"><span data-stu-id="ac990-189">string</span></span> | <span data-ttu-id="ac990-190">예</span><span class="sxs-lookup"><span data-stu-id="ac990-190">yes</span></span>      | <span data-ttu-id="ac990-191">SHA-256 지문</span><span class="sxs-lookup"><span data-stu-id="ac990-191">The SHA-256 fingerprint</span></span>

<span data-ttu-id="ac990-192">키 이름 `2.16.840.1.101.3.4.2.1` 는 SHA-256 해시 알고리즘의 OID입니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-192">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="ac990-193">모든 해시 값에는 해시 다이제스트의 소문자 16 진수로 인코딩된 문자열 표현 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac990-193">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="ac990-194">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="ac990-194">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="ac990-195">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="ac990-195">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
