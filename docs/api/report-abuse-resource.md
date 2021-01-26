---
title: 신고 URL 템플릿, NuGet API 보고
description: 보고서 신고 URL 템플릿을 사용 하면 클라이언트는 자신의 UI에 신고 링크를 표시할 수 있습니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775234"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="5e853-103">신고 URL 템플릿 신고</span><span class="sxs-lookup"><span data-stu-id="5e853-103">Report abuse URL template</span></span>

<span data-ttu-id="5e853-104">클라이언트는 사용자가 특정 패키지에 대 한 불건전 사용자를 보고 하는 데 사용할 수 있는 URL을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e853-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="5e853-105">이 기능은 패키지 원본에서 모든 클라이언트 환경 (타사)을 사용 하도록 설정 하 여 불건전 보고서를 패키지 원본에 위임 하려는 경우에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e853-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="5e853-106">이 URL을 작성 하는 데 사용 되는 리소스는 `ReportAbuseUriTemplate` [서비스 인덱스](service-index.md)에 있는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="5e853-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="5e853-107">버전 관리</span><span class="sxs-lookup"><span data-stu-id="5e853-107">Versioning</span></span>

<span data-ttu-id="5e853-108">사용 되는 `@type` 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5e853-108">The following `@type` values are used:</span></span>

<span data-ttu-id="5e853-109">@type 값</span><span class="sxs-lookup"><span data-stu-id="5e853-109">@type value</span></span>                       | <span data-ttu-id="5e853-110">메모</span><span class="sxs-lookup"><span data-stu-id="5e853-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="5e853-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="5e853-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="5e853-112">초기 릴리스</span><span class="sxs-lookup"><span data-stu-id="5e853-112">The initial release</span></span>
<span data-ttu-id="5e853-113">ReportAbuseUriTemplate/3.0.0</span><span class="sxs-lookup"><span data-stu-id="5e853-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="5e853-114">별칭 `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="5e853-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="5e853-115">URL 템플릿</span><span class="sxs-lookup"><span data-stu-id="5e853-115">URL template</span></span>

<span data-ttu-id="5e853-116">다음 API에 대 한 URL은 `@id` 앞서 언급 한 리소스 값 중 하 나와 연결 된 속성의 값입니다 `@type` .</span><span class="sxs-lookup"><span data-stu-id="5e853-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="5e853-117">HTTP 메서드</span><span class="sxs-lookup"><span data-stu-id="5e853-117">HTTP methods</span></span>

<span data-ttu-id="5e853-118">클라이언트가 사용자를 대신 하 여 신고 URL에 대 한 요청을 수행 하기 위한 것은 아니지만 웹 페이지는 `GET` 클릭 된 URL을 웹 브라우저에서 쉽게 열도록 허용 하는 메서드를 지원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e853-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="5e853-119">URL 생성</span><span class="sxs-lookup"><span data-stu-id="5e853-119">Construct the URL</span></span>

<span data-ttu-id="5e853-120">알려진 패키지 ID 및 버전이 제공 되 면 클라이언트 구현에서 웹 인터페이스에 액세스 하는 데 사용 되는 URL을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e853-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="5e853-121">클라이언트 구현에서는이 생성 된 URL (또는 클릭 가능한 링크)을 사용자에 게 표시 하 여 URL에 대 한 웹 브라우저를 열고 필요한 불건전 보고서를 만들 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e853-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="5e853-122">불건전 보고서 양식의 구현은 서버 구현에 의해 결정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e853-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="5e853-123">의 값은 `@id` 다음 자리 표시자 토큰 중 하나를 포함 하는 URL 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="5e853-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="5e853-124">URL 자리 표시자</span><span class="sxs-lookup"><span data-stu-id="5e853-124">URL placeholders</span></span>

<span data-ttu-id="5e853-125">Name</span><span class="sxs-lookup"><span data-stu-id="5e853-125">Name</span></span>        | <span data-ttu-id="5e853-126">Type</span><span class="sxs-lookup"><span data-stu-id="5e853-126">Type</span></span>    | <span data-ttu-id="5e853-127">필수</span><span class="sxs-lookup"><span data-stu-id="5e853-127">Required</span></span> | <span data-ttu-id="5e853-128">메모</span><span class="sxs-lookup"><span data-stu-id="5e853-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="5e853-129">문자열</span><span class="sxs-lookup"><span data-stu-id="5e853-129">string</span></span>  | <span data-ttu-id="5e853-130">아니요</span><span class="sxs-lookup"><span data-stu-id="5e853-130">no</span></span>       | <span data-ttu-id="5e853-131">신고를 보고할 패키지 ID</span><span class="sxs-lookup"><span data-stu-id="5e853-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="5e853-132">문자열</span><span class="sxs-lookup"><span data-stu-id="5e853-132">string</span></span>  | <span data-ttu-id="5e853-133">아니요</span><span class="sxs-lookup"><span data-stu-id="5e853-133">no</span></span>       | <span data-ttu-id="5e853-134">신고를 보고할 패키지 버전</span><span class="sxs-lookup"><span data-stu-id="5e853-134">The package version to report abuse for</span></span>

<span data-ttu-id="5e853-135">`{id}` `{version}` 서버 구현에서 해석 되는 및 값은 대/소문자를 구분 하지 않고 버전이 정규화 되었는지 여부를 구분 하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e853-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="5e853-136">예를 들어, nuget.exe의 신고는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5e853-136">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="5e853-137">클라이언트 구현에서 NuGet에 대 한 보고서 불건전 폼의 링크를 표시 해야 하는 경우 다음 URL을 생성 하 여 사용자에 게 제공 합니다. 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="5e853-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
