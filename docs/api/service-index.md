---
title: 서비스 인덱스, NuGet API
description: 서비스 인덱스는 NuGet HTTP API의 진입점 이며 서버의 기능을 열거 합니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775358"
---
# <a name="service-index"></a><span data-ttu-id="e9bb0-103">인덱스 제공</span><span class="sxs-lookup"><span data-stu-id="e9bb0-103">Service index</span></span>

<span data-ttu-id="e9bb0-104">서비스 인덱스는 NuGet 패키지 소스에 대 한 진입점인 JSON 문서로, 클라이언트 구현에서 패키지 소스의 기능을 검색할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="e9bb0-105">서비스 인덱스는 두 개의 필수 속성 `version` (서비스 인덱스의 스키마 버전) 및 `resources`  (패키지 원본의 끝점 또는 기능)을 포함 하는 JSON 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="e9bb0-106">nuget. org의 서비스 인덱스는에 있습니다 `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="e9bb0-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="e9bb0-107">버전 관리</span><span class="sxs-lookup"><span data-stu-id="e9bb0-107">Versioning</span></span>

<span data-ttu-id="e9bb0-108">`version`값은 서비스 인덱스의 스키마 버전을 나타내는 SemVer 2.0.0 구문 분석할 version 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="e9bb0-109">API는 버전 문자열의 주 버전 번호를 요구 `3` 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="e9bb0-110">서비스 인덱스 스키마에 대 한 주요 변경 내용이 적용 되지 않으므로 버전 문자열의 부 버전이 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="e9bb0-111">서비스 인덱스의 각 리소스는 서비스 인덱스 스키마 버전과 독립적으로 버전이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="e9bb0-112">현재 스키마 버전은 `3.0.0` 입니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="e9bb0-113">`3.0.0`버전은 이전 버전과 기능적으로 동일 `3.0.0-beta.1` 하지만, 안정적이 고 정의 된 스키마를 보다 명확 하 게 전달 하므로 선호 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e9bb0-114">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="e9bb0-114">HTTP methods</span></span>

<span data-ttu-id="e9bb0-115">서비스 인덱스는 HTTP 메서드 및를 사용 하 여 액세스할 수 `GET` `HEAD` 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="e9bb0-116">리소스</span><span class="sxs-lookup"><span data-stu-id="e9bb0-116">Resources</span></span>

<span data-ttu-id="e9bb0-117">속성에는 `resources` 이 패키지 소스에서 지 원하는 리소스 배열이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="e9bb0-118">리소스</span><span class="sxs-lookup"><span data-stu-id="e9bb0-118">Resource</span></span>

<span data-ttu-id="e9bb0-119">리소스는 배열의 개체입니다 `resources` .</span><span class="sxs-lookup"><span data-stu-id="e9bb0-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="e9bb0-120">패키지 소스의 버전이 지정 된 기능을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="e9bb0-121">리소스에는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-121">A resource has the following properties:</span></span>

<span data-ttu-id="e9bb0-122">Name</span><span class="sxs-lookup"><span data-stu-id="e9bb0-122">Name</span></span>          | <span data-ttu-id="e9bb0-123">Type</span><span class="sxs-lookup"><span data-stu-id="e9bb0-123">Type</span></span>   | <span data-ttu-id="e9bb0-124">필수</span><span class="sxs-lookup"><span data-stu-id="e9bb0-124">Required</span></span> | <span data-ttu-id="e9bb0-125">메모</span><span class="sxs-lookup"><span data-stu-id="e9bb0-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="e9bb0-126">문자열</span><span class="sxs-lookup"><span data-stu-id="e9bb0-126">string</span></span> | <span data-ttu-id="e9bb0-127">예</span><span class="sxs-lookup"><span data-stu-id="e9bb0-127">yes</span></span>      | <span data-ttu-id="e9bb0-128">리소스에 대 한 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="e9bb0-129">문자열</span><span class="sxs-lookup"><span data-stu-id="e9bb0-129">string</span></span> | <span data-ttu-id="e9bb0-130">예</span><span class="sxs-lookup"><span data-stu-id="e9bb0-130">yes</span></span>      | <span data-ttu-id="e9bb0-131">리소스 형식을 나타내는 문자열 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-131">A string constant representing the resource type</span></span>
<span data-ttu-id="e9bb0-132">주석</span><span class="sxs-lookup"><span data-stu-id="e9bb0-132">comment</span></span>       | <span data-ttu-id="e9bb0-133">문자열</span><span class="sxs-lookup"><span data-stu-id="e9bb0-133">string</span></span> | <span data-ttu-id="e9bb0-134">아니요</span><span class="sxs-lookup"><span data-stu-id="e9bb0-134">no</span></span>       | <span data-ttu-id="e9bb0-135">사람이 읽을 수 있는 리소스에 대 한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-135">A human readable description of the resource</span></span>

<span data-ttu-id="e9bb0-136">는 `@id` 절대 URL 이어야 하며 HTTP 또는 HTTPS 스키마가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="e9bb0-137">는 `@type` 리소스와 상호 작용할 때 사용할 특정 프로토콜을 식별 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="e9bb0-138">리소스의 형식은 불투명 문자열 이지만 일반적으로 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-138">The type of the resource is an opaque string but generally has the format:</span></span>

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

<span data-ttu-id="e9bb0-139">클라이언트는 `@type` 이해 하는 값을 하드 코딩 하 고 패키지 소스의 서비스 인덱스에서 조회 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="e9bb0-140">`@type`현재 사용 중인 정확한 값은 [API 개요](overview.md#resources-and-schema)에 나열 된 개별 리소스 참조 문서에 열거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="e9bb0-141">이 설명서의 편의를 위해 다른 리소스에 대 한 설명서는 기본적으로 서비스 인덱스에 있는로 그룹화 되며,이는 `{RESOURCE_NAME}` 시나리오 별로 그룹화 하는 것과 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="e9bb0-142">각 리소스에는 고유한 또는가 있어야 `@id` `@type` 합니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="e9bb0-143">다른 리소스를 선호 하는 리소스를 결정 하는 것은 클라이언트 구현에 따라 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="e9bb0-144">한 가지 가능한 구현은 `@type` 연결 실패 또는 서버 오류 발생 시 라운드 로빈 방식으로 같거나 호환 되는 리소스를 사용할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e9bb0-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e9bb0-145">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="e9bb0-145">Sample request</span></span>

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a><span data-ttu-id="e9bb0-146">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="e9bb0-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
