---
title: 패키지 세부 정보 URL 템플릿, NuGet API
description: 패키지 세부 정보 URL 템플릿을 사용 하면 클라이언트에서 추가 패키지 세부 정보에 대 한 웹 링크를 UI에 표시할 수 있습니다.
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 3102cb9a20f354e92a0da8bba6457dc2ad0f0f2d
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610953"
---
# <a name="package-details-url-template"></a><span data-ttu-id="8f3b0-103">패키지 세부 정보 URL 템플릿</span><span class="sxs-lookup"><span data-stu-id="8f3b0-103">Package details URL template</span></span>

<span data-ttu-id="8f3b0-104">클라이언트는 사용자가 웹 브라우저에서 추가 패키지 세부 정보를 볼 때 사용할 수 있는 URL을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b0-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="8f3b0-105">이는 NuGet 클라이언트 응용 프로그램에서 표시 하는 범위 내에 적합 하지 않을 수 있는 패키지에 대 한 추가 정보를 패키지 원본에서 표시 하려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b0-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="8f3b0-106">이 URL을 작성 하는 데 사용 되는 리소스는 [서비스 인덱스](service-index.md)에 있는 `PackageDetailsUriTemplate` 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b0-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="8f3b0-107">버전 관리</span><span class="sxs-lookup"><span data-stu-id="8f3b0-107">Versioning</span></span>

<span data-ttu-id="8f3b0-108">사용 되는 `@type` 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b0-108">The following `@type` values are used:</span></span>

<span data-ttu-id="8f3b0-109">@type 값</span><span class="sxs-lookup"><span data-stu-id="8f3b0-109">@type value</span></span>                     | <span data-ttu-id="8f3b0-110">노트</span><span class="sxs-lookup"><span data-stu-id="8f3b0-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="8f3b0-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="8f3b0-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="8f3b0-112">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="8f3b0-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="8f3b0-113">URL 템플릿</span><span class="sxs-lookup"><span data-stu-id="8f3b0-113">URL template</span></span>

<span data-ttu-id="8f3b0-114">다음 API에 대 한 URL은 앞서 언급 한 리소스 `@type` 값 중 하 나와 연결 된 `@id` 속성의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b0-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="8f3b0-115">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="8f3b0-115">HTTP methods</span></span>

<span data-ttu-id="8f3b0-116">클라이언트는 사용자를 대신 하 여 패키지 세부 정보 URL에 대 한 요청을 수행 하지 않지만, 웹 브라우저에서 클릭 한 URL을 쉽게 열 수 있도록 웹 페이지에서 `GET` 방법을 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b0-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="8f3b0-117">URL 생성</span><span class="sxs-lookup"><span data-stu-id="8f3b0-117">Construct the URL</span></span>

<span data-ttu-id="8f3b0-118">알려진 패키지 ID 및 버전이 제공 되 면 클라이언트 구현에서 웹 인터페이스에 액세스 하는 데 사용 되는 URL을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b0-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="8f3b0-119">클라이언트 구현에서는이 생성 된 URL (또는 클릭 가능한 링크)을 사용자에 게 표시 하 여 URL에 대 한 웹 브라우저를 열고 패키지에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b0-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="8f3b0-120">패키지 세부 정보 페이지의 내용은 서버 구현에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b0-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="8f3b0-121">URL은 절대 URL 이어야 하 고 스키마 (프로토콜)는 HTTPS 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b0-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="8f3b0-122">서비스 인덱스에 있는 `@id`의 값은 다음 자리 표시자 토큰 중 하나를 포함 하는 URL 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b0-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="8f3b0-123">URL 자리 표시자</span><span class="sxs-lookup"><span data-stu-id="8f3b0-123">URL placeholders</span></span>

<span data-ttu-id="8f3b0-124">name</span><span class="sxs-lookup"><span data-stu-id="8f3b0-124">Name</span></span>        | <span data-ttu-id="8f3b0-125">Type</span><span class="sxs-lookup"><span data-stu-id="8f3b0-125">Type</span></span>    | <span data-ttu-id="8f3b0-126">필요한 공간</span><span class="sxs-lookup"><span data-stu-id="8f3b0-126">Required</span></span> | <span data-ttu-id="8f3b0-127">노트</span><span class="sxs-lookup"><span data-stu-id="8f3b0-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="8f3b0-128">string</span><span class="sxs-lookup"><span data-stu-id="8f3b0-128">string</span></span>  | <span data-ttu-id="8f3b0-129">아니요</span><span class="sxs-lookup"><span data-stu-id="8f3b0-129">no</span></span>       | <span data-ttu-id="8f3b0-130">세부 정보를 가져올 패키지 ID</span><span class="sxs-lookup"><span data-stu-id="8f3b0-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="8f3b0-131">string</span><span class="sxs-lookup"><span data-stu-id="8f3b0-131">string</span></span>  | <span data-ttu-id="8f3b0-132">아니요</span><span class="sxs-lookup"><span data-stu-id="8f3b0-132">no</span></span>       | <span data-ttu-id="8f3b0-133">세부 정보를 가져올 패키지 버전</span><span class="sxs-lookup"><span data-stu-id="8f3b0-133">The package version to get details for</span></span>

<span data-ttu-id="8f3b0-134">서버는 대/소문자를 구분 하 여 `{id}` 및 `{version}` 값을 수락 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b0-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="8f3b0-135">또한 서버는 버전이 [정규화](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers)되었는지 여부를 구분 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b0-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/nuget/concepts/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="8f3b0-136">즉, 서버에도 정규화 되지 않은 버전이 허용 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b0-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="8f3b0-137">예를 들어, nuget.exe의 패키지 세부 정보 템플릿은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b0-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="8f3b0-138">클라이언트 구현에서 NuGet의 패키지 세부 정보에 대 한 링크를 표시 해야 하는 경우 4.3.0는 다음 URL을 생성 하 여 사용자에 게 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8f3b0-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
