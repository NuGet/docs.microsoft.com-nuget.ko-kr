---
title: 패키지 세부 정보 URL 템플릿을 NuGet API
description: 패키지 세부 정보 URL 템플릿을 한 패키지 세부 정보로 링크 웹 UI에 표시 하는 클라이언트 수
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638080"
---
# <a name="package-details-url-template"></a><span data-ttu-id="de6bb-103">패키지 세부 정보 URL 템플릿</span><span class="sxs-lookup"><span data-stu-id="de6bb-103">Package details URL template</span></span>

<span data-ttu-id="de6bb-104">웹 브라우저에서 더 많은 패키지 세부 정보를 보려면 사용자가 사용할 수 있는 URL을 작성 하는 클라이언트는 것이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="de6bb-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="de6bb-105">패키지 소스를 NuGet 클라이언트 응용 프로그램 표시 범위 내에서 맞지 않을 수 있습니다 하는 패키지에 대 한 추가 정보를 표시 하려고 할 때 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="de6bb-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="de6bb-106">이 URL을 작성에 사용 되는 리소스를 `PackageDetailsUriTemplate` 에서 리소스를 찾을 합니다 [서비스 인덱스](service-index.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="de6bb-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="de6bb-107">버전 관리</span><span class="sxs-lookup"><span data-stu-id="de6bb-107">Versioning</span></span>

<span data-ttu-id="de6bb-108">다음 `@type` 값이 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de6bb-108">The following `@type` values are used:</span></span>

<span data-ttu-id="de6bb-109">@type 값</span><span class="sxs-lookup"><span data-stu-id="de6bb-109">@type value</span></span>                     | <span data-ttu-id="de6bb-110">노트</span><span class="sxs-lookup"><span data-stu-id="de6bb-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="de6bb-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="de6bb-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="de6bb-112">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="de6bb-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="de6bb-113">URL 템플릿</span><span class="sxs-lookup"><span data-stu-id="de6bb-113">URL template</span></span>

<span data-ttu-id="de6bb-114">다음 API에 대 한 URL의 값은는 `@id` 앞에서 언급 한 리소스 중 하나를 사용 하 여 연결 된 속성 `@type` 값입니다.</span><span class="sxs-lookup"><span data-stu-id="de6bb-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="de6bb-115">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="de6bb-115">HTTP methods</span></span>

<span data-ttu-id="de6bb-116">웹 페이지를 지원 해야 클라이언트 사용자를 대신 하 여 패키지 세부 정보 URL 요청을 하려면 없습니다, 있지만 `GET` 쉽게 웹 브라우저에서 열 수를 클릭 한 URL을 허용 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="de6bb-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="de6bb-117">URL 생성</span><span class="sxs-lookup"><span data-stu-id="de6bb-117">Construct the URL</span></span>

<span data-ttu-id="de6bb-118">알려진된 패키지 ID 및 버전을 지정 하 여 클라이언트 구현 웹 인터페이스에 액세스 하는 데 사용 하는 URL을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de6bb-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="de6bb-119">클라이언트 구현에는 URL로 웹 브라우저를 열고을 패키지에 자세히 알아보려면 수 있도록 사용자에 게이 구성 된 URL (또는 클릭 가능한 링크) 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de6bb-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="de6bb-120">패키지 세부 정보 페이지의 내용은 서버 구현에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de6bb-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="de6bb-121">URL은 절대 URL 이어야 하 고 (프로토콜) 체계는 HTTPS 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de6bb-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="de6bb-122">값을 `@id` 서비스에서 인덱스는 다음과 같은 자리 표시자 토큰 중 하나를 포함 하는 URL 문자열:</span><span class="sxs-lookup"><span data-stu-id="de6bb-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="de6bb-123">URL 자리 표시자</span><span class="sxs-lookup"><span data-stu-id="de6bb-123">URL placeholders</span></span>

<span data-ttu-id="de6bb-124">이름</span><span class="sxs-lookup"><span data-stu-id="de6bb-124">Name</span></span>        | <span data-ttu-id="de6bb-125">형식</span><span class="sxs-lookup"><span data-stu-id="de6bb-125">Type</span></span>    | <span data-ttu-id="de6bb-126">필수</span><span class="sxs-lookup"><span data-stu-id="de6bb-126">Required</span></span> | <span data-ttu-id="de6bb-127">노트</span><span class="sxs-lookup"><span data-stu-id="de6bb-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="de6bb-128">string</span><span class="sxs-lookup"><span data-stu-id="de6bb-128">string</span></span>  | <span data-ttu-id="de6bb-129">아니요</span><span class="sxs-lookup"><span data-stu-id="de6bb-129">no</span></span>       | <span data-ttu-id="de6bb-130">패키지 ID에 대 한 세부 정보를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="de6bb-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="de6bb-131">string</span><span class="sxs-lookup"><span data-stu-id="de6bb-131">string</span></span>  | <span data-ttu-id="de6bb-132">아니요</span><span class="sxs-lookup"><span data-stu-id="de6bb-132">no</span></span>       | <span data-ttu-id="de6bb-133">패키지 버전에 대 한 세부 정보를 가져오려면</span><span class="sxs-lookup"><span data-stu-id="de6bb-133">The package version to get details for</span></span>

<span data-ttu-id="de6bb-134">서버를 승인할지 `{id}` 및 `{version}` 모든 대/소문자를 사용 하 여 값입니다.</span><span class="sxs-lookup"><span data-stu-id="de6bb-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="de6bb-135">서버를 버전 인지는 중요 한 있어야 뿐만 [정규화 된](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers)합니다.</span><span class="sxs-lookup"><span data-stu-id="de6bb-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="de6bb-136">즉, 서버를 승인할지 정규화 되지 않은 버전을 그대로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de6bb-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="de6bb-137">예를 들어, nuget.org의 패키지 세부 정보 템플릿을 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="de6bb-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="de6bb-138">클라이언트 구현 NuGet.Versioning 4.3.0에 대 한 링크 패키지 세부 정보를 표시 하는 경우는 다음 URL을 생성 하 고 사용자에 게 제공:</span><span class="sxs-lookup"><span data-stu-id="de6bb-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
