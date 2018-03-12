---
title: "서비스 인덱스, NuGet API | Microsoft Docs"
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
description: "서비스 인덱스 NuGet HTTP API의 진입점이 고 서버 기능을 열거 합니다."
keywords: "NuGet API 진입점을 NuGetA PI 끝점 검색"
ms.reviewer:
- karann
- unnir
ms.openlocfilehash: 8de0bc15edc358d091d84da54b8b67c085f29645
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="service-index"></a><span data-ttu-id="5b455-104">서비스 인덱스</span><span class="sxs-lookup"><span data-stu-id="5b455-104">Service index</span></span>

<span data-ttu-id="5b455-105">서비스 인덱스에는 NuGet 패키지 원본에 대 한 진입점이 되며 패키지 원본 기능을 검색 하는 클라이언트 구현이 포함을 허용 하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-105">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="5b455-106">서비스 인덱스는 두 개의 필수 속성만 사용 하는 JSON 개체: `version` (서비스 인덱스의 스키마 버전) 및 `resources` (끝점 또는 패키지 원본의 기능).</span><span class="sxs-lookup"><span data-stu-id="5b455-106">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="5b455-107">nuget.org의 서비스 인덱스에 위치한 `https://api.nuget.org/v3/index.json`합니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-107">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="5b455-108">버전 관리</span><span class="sxs-lookup"><span data-stu-id="5b455-108">Versioning</span></span>

<span data-ttu-id="5b455-109">`version` 값은 서비스 인덱스의 스키마 버전을 나타내는 SemVer 2.0.0 구문 버전 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-109">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="5b455-110">API 버전 문자열의 주 버전 번호에 보내도록 규정 `3`합니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-110">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="5b455-111">서비스 인덱스 스키마에 사소한 변경, 버전 문자열의 부 버전을 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-111">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="5b455-112">서비스 인덱스의 각 리소스는 서비스 인덱스 스키마 버전에서 독립적으로 버전이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-112">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="5b455-113">현재 스키마 버전은 `3.0.0`합니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-113">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="5b455-114">`3.0.0` 버전은 다음 이전 `3.0.0-beta.1` 버전 수 있지만 기본 설정으로 안정적이 고 정의 된 스키마를 보다 명확 하 게 통신 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-114">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="5b455-115">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="5b455-115">HTTP methods</span></span>

<span data-ttu-id="5b455-116">서비스 인덱스는 HTTP 메서드를 사용 하 여 액세스할 `GET` 및 `HEAD`합니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-116">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="5b455-117">자료</span><span class="sxs-lookup"><span data-stu-id="5b455-117">Resources</span></span>

<span data-ttu-id="5b455-118">`resources` 속성에는이 패키지 소스에서 지 원하는 리소스의 배열을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-118">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="5b455-119">리소스</span><span class="sxs-lookup"><span data-stu-id="5b455-119">Resource</span></span>

<span data-ttu-id="5b455-120">리소스는에 있는 개체는 `resources` 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-120">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="5b455-121">패키지 원본 버전 관리 기능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-121">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="5b455-122">리소스에는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-122">A resource has the following properties:</span></span>

<span data-ttu-id="5b455-123">name</span><span class="sxs-lookup"><span data-stu-id="5b455-123">Name</span></span>          | <span data-ttu-id="5b455-124">형식</span><span class="sxs-lookup"><span data-stu-id="5b455-124">Type</span></span>   | <span data-ttu-id="5b455-125">필수</span><span class="sxs-lookup"><span data-stu-id="5b455-125">Required</span></span> | <span data-ttu-id="5b455-126">노트</span><span class="sxs-lookup"><span data-stu-id="5b455-126">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="5b455-127">string</span><span class="sxs-lookup"><span data-stu-id="5b455-127">string</span></span> | <span data-ttu-id="5b455-128">예</span><span class="sxs-lookup"><span data-stu-id="5b455-128">yes</span></span>      | <span data-ttu-id="5b455-129">리소스에 대 한 URL</span><span class="sxs-lookup"><span data-stu-id="5b455-129">The URL to the resource</span></span>
@type         | <span data-ttu-id="5b455-130">string</span><span class="sxs-lookup"><span data-stu-id="5b455-130">string</span></span> | <span data-ttu-id="5b455-131">예</span><span class="sxs-lookup"><span data-stu-id="5b455-131">yes</span></span>      | <span data-ttu-id="5b455-132">리소스 종류를 나타내는 문자열 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-132">A string constant representing the resource type</span></span>
<span data-ttu-id="5b455-133">주석</span><span class="sxs-lookup"><span data-stu-id="5b455-133">comment</span></span>       | <span data-ttu-id="5b455-134">string</span><span class="sxs-lookup"><span data-stu-id="5b455-134">string</span></span> | <span data-ttu-id="5b455-135">아니요</span><span class="sxs-lookup"><span data-stu-id="5b455-135">no</span></span>       | <span data-ttu-id="5b455-136">리소스의 사람이 읽을 수 있는 설명</span><span class="sxs-lookup"><span data-stu-id="5b455-136">A human readable description of the resource</span></span>

<span data-ttu-id="5b455-137">`@id` 절대 경로 여야 하 고 수행 해야 할 하는 URL에는 HTTP 또는 HTTPS 스키마가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-137">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="5b455-138">`@type` 리소스와 상호 작용할 때 사용 하 여 특정 프로토콜을 식별 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-138">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="5b455-139">리소스의 불투명 문자열이 아니지만 일반적으로 형식이:</span><span class="sxs-lookup"><span data-stu-id="5b455-139">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="5b455-140">클라이언트는 하드 코딩 것으로 예상 되는 `@type` 것을 파악 하 고 패키지 소스의 서비스 인덱스에서 조회 값입니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-140">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="5b455-141">정확한 `@type` 오늘날에서 사용 되는 값에 나열 된 개별 리소스 참조 문서에 열거 되는 [API 개요](overview.md#resources-and-schema)합니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-141">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="5b455-142">이 설명서를 위해 다양 한 리소스에 대 한 설명서 기본적으로로 그룹화 되는 `{RESOURCE_NAME}` 그룹화 시나리오에 따라 유사한 서비스 인덱스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-142">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="5b455-143">각 리소스에는 고유한 요구 사항이 없을 `@id` 또는 `@type`합니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-143">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="5b455-144">리소스에서 다른 것을 선호할를 결정 하는 클라이언트 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-144">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="5b455-145">한 가지 구현을의 같거나 호환 되는 리소스 `@type` 연결 오류 또는 서버 오류 시 라운드 로빈 방식으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5b455-145">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="5b455-146">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="5b455-146">Sample request</span></span>

<span data-ttu-id="5b455-147">GET https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="5b455-147">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="5b455-148">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="5b455-148">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
