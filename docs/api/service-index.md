---
title: 서비스 인덱스를 NuGet API
description: 서비스 인덱스 NuGet HTTP API의 진입점이 고 서버 기능을 열거 합니다.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 84e623e8480e4d17edad2ec3b2da6dcb6e53d21b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822096"
---
# <a name="service-index"></a><span data-ttu-id="38f78-103">서비스 인덱스</span><span class="sxs-lookup"><span data-stu-id="38f78-103">Service index</span></span>

<span data-ttu-id="38f78-104">서비스 인덱스에는 NuGet 패키지 원본에 대 한 진입점이 되며 패키지 원본 기능을 검색 하는 클라이언트 구현이 포함을 허용 하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="38f78-105">서비스 인덱스는 두 개의 필수 속성만 사용 하는 JSON 개체: `version` (서비스 인덱스의 스키마 버전) 및 `resources` (끝점 또는 패키지 원본의 기능).</span><span class="sxs-lookup"><span data-stu-id="38f78-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="38f78-106">nuget.org의 서비스 인덱스에 위치한 `https://api.nuget.org/v3/index.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="38f78-107">버전 관리</span><span class="sxs-lookup"><span data-stu-id="38f78-107">Versioning</span></span>

<span data-ttu-id="38f78-108">`version` 값은 서비스 인덱스의 스키마 버전을 나타내는 SemVer 2.0.0 구문 버전 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="38f78-109">API 버전 문자열의 주 버전 번호에 보내도록 규정 `3`합니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="38f78-110">서비스 인덱스 스키마에 사소한 변경, 버전 문자열의 부 버전을 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="38f78-111">서비스 인덱스의 각 리소스는 서비스 인덱스 스키마 버전에서 독립적으로 버전이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="38f78-112">현재 스키마 버전은 `3.0.0`합니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="38f78-113">`3.0.0` 버전은 다음 이전 `3.0.0-beta.1` 버전 수 있지만 기본 설정으로 안정적이 고 정의 된 스키마를 보다 명확 하 게 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="38f78-114">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="38f78-114">HTTP methods</span></span>

<span data-ttu-id="38f78-115">서비스 인덱스는 HTTP 메서드를 사용 하 여 액세스할 `GET` 및 `HEAD`합니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="38f78-116">자료</span><span class="sxs-lookup"><span data-stu-id="38f78-116">Resources</span></span>

<span data-ttu-id="38f78-117">`resources` 속성에는이 패키지 소스에서 지 원하는 리소스의 배열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="38f78-118">리소스</span><span class="sxs-lookup"><span data-stu-id="38f78-118">Resource</span></span>

<span data-ttu-id="38f78-119">리소스는에 있는 개체는 `resources` 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="38f78-120">패키지 원본 버전 관리 기능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="38f78-121">리소스에는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-121">A resource has the following properties:</span></span>

<span data-ttu-id="38f78-122">이름</span><span class="sxs-lookup"><span data-stu-id="38f78-122">Name</span></span>          | <span data-ttu-id="38f78-123">형식</span><span class="sxs-lookup"><span data-stu-id="38f78-123">Type</span></span>   | <span data-ttu-id="38f78-124">필수</span><span class="sxs-lookup"><span data-stu-id="38f78-124">Required</span></span> | <span data-ttu-id="38f78-125">노트</span><span class="sxs-lookup"><span data-stu-id="38f78-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="38f78-126">string</span><span class="sxs-lookup"><span data-stu-id="38f78-126">string</span></span> | <span data-ttu-id="38f78-127">예</span><span class="sxs-lookup"><span data-stu-id="38f78-127">yes</span></span>      | <span data-ttu-id="38f78-128">리소스에 대 한 URL</span><span class="sxs-lookup"><span data-stu-id="38f78-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="38f78-129">string</span><span class="sxs-lookup"><span data-stu-id="38f78-129">string</span></span> | <span data-ttu-id="38f78-130">예</span><span class="sxs-lookup"><span data-stu-id="38f78-130">yes</span></span>      | <span data-ttu-id="38f78-131">리소스 종류를 나타내는 문자열 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-131">A string constant representing the resource type</span></span>
<span data-ttu-id="38f78-132">comment</span><span class="sxs-lookup"><span data-stu-id="38f78-132">comment</span></span>       | <span data-ttu-id="38f78-133">string</span><span class="sxs-lookup"><span data-stu-id="38f78-133">string</span></span> | <span data-ttu-id="38f78-134">아니요</span><span class="sxs-lookup"><span data-stu-id="38f78-134">no</span></span>       | <span data-ttu-id="38f78-135">리소스의 사람이 읽을 수 있는 설명</span><span class="sxs-lookup"><span data-stu-id="38f78-135">A human readable description of the resource</span></span>

<span data-ttu-id="38f78-136">`@id` 절대 경로 여야 하 고 수행 해야 할 하는 URL에는 HTTP 또는 HTTPS 스키마가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="38f78-137">`@type` 리소스와 상호 작용할 때 사용 하 여 특정 프로토콜을 식별 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="38f78-138">리소스의 불투명 문자열이 아니지만 일반적으로 형식이:</span><span class="sxs-lookup"><span data-stu-id="38f78-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="38f78-139">클라이언트는 하드 코딩 것으로 예상 되는 `@type` 것을 파악 하 고 패키지 소스의 서비스 인덱스에서 조회 값입니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="38f78-140">정확한 `@type` 오늘날에서 사용 되는 값에 나열 된 개별 리소스 참조 문서에 열거 되는 [API 개요](overview.md#resources-and-schema)합니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="38f78-141">이 설명서를 위해 다양 한 리소스에 대 한 설명서 기본적으로로 그룹화 되는 `{RESOURCE_NAME}` 그룹화 시나리오에 따라 유사한 서비스 인덱스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="38f78-142">각 리소스에는 고유한 요구 사항이 없을 `@id` 또는 `@type`합니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="38f78-143">리소스에서 다른 것을 선호할를 결정 하는 클라이언트 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="38f78-144">한 가지 구현을의 같거나 호환 되는 리소스 `@type` 연결 오류 또는 서버 오류 시 라운드 로빈 방식으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="38f78-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="38f78-145">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="38f78-145">Sample request</span></span>

<span data-ttu-id="38f78-146">가져오기 https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="38f78-146">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="38f78-147">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="38f78-147">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]