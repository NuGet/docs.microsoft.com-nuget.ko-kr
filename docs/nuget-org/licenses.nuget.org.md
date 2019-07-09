---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427118"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="e5a91-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="e5a91-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="e5a91-103">설명</span><span class="sxs-lookup"><span data-stu-id="e5a91-103">Rationale</span></span>

<span data-ttu-id="e5a91-104">[라이선스 식](../reference/nuspec.md#license)의 도입으로 인해 개별 라이선스 식별자, 예외 식별자 또는 라이선스 식에 대한 참조 텍스트를 제공하는 신뢰할 수 있는 서비스를 갖추어야 하는 요구 사항이 대두되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-104">With the introduction of the [license expressions](../reference/nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="e5a91-105">이 서비스에 대한 추가 요구 사항은 링크 손실에 취약하지 않은 안정적인 URL 스키마를 갖추어 오래된 클라이언트에 대해 이전 버전과의 호환성을 제공하여 안전하게 사용할 수 있도록 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="e5a91-106">Licenses.nuget.org는 해당 역할을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="e5a91-107">Nuget.org는 이를 통해 라이선스 식을 사용하여 라이선스를 지정하는 패키지에 대한 라이선스 텍스트 참조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="e5a91-108">`nuget pack` 또는 다른 [클라이언트 도구](../install-nuget-client-tools.md)로 패킹하여 [`licenseUrl`](../reference/nuspec.md#licenseurl) 요소가 licenses.nuget.org를 가리키도록 설정하여 `license` 요소가 지원되지 않은 오래된 클라이언트에게 이전 버전과의 호환성을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-108">`nuget pack` or packing with other [client tools](../install-nuget-client-tools.md) set the [`licenseUrl`](../reference/nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="e5a91-109">프로토콜</span><span class="sxs-lookup"><span data-stu-id="e5a91-109">Protocol</span></span>

<span data-ttu-id="e5a91-110">Licenses.nuget.org는 브라우저에 있는 사용자가 볼 수 있도록 고안되었으며, 머신이 읽을 수 있는 응답은 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="e5a91-111">HTTPS 프로토콜을 사용해야 하며 요청은 특정 방법으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="e5a91-112">`GET` 요청만 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="e5a91-113">아래에 지정된 방법으로 라이선스 식 또는 라이선스 예외 식별자를 입력으로 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="e5a91-114">라이선스 식의 모든 요소는 대/소문자를 구분하므로 licenses.nuget.org에 대한 모든 입력도 대/소문자를 구분한다는 점에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="e5a91-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="e5a91-115">라이선스 식</span><span class="sxs-lookup"><span data-stu-id="e5a91-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="e5a91-116">요청</span><span class="sxs-lookup"><span data-stu-id="e5a91-116">Request</span></span>

<span data-ttu-id="e5a91-117">라이선스 식(식은 단일 라이선스로 구성되는 간단한 사례 포함)은 [URL로 인코딩](https://tools.ietf.org/html/rfc3986#section-2.1)되어야 하며 licenses.nuget.org에 대한 요청의 경로로 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="e5a91-118">라이선스 식</span><span class="sxs-lookup"><span data-stu-id="e5a91-118">License expression</span></span> | <span data-ttu-id="e5a91-119">사용할 URL</span><span class="sxs-lookup"><span data-stu-id="e5a91-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="e5a91-120">MIT</span><span class="sxs-lookup"><span data-stu-id="e5a91-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="e5a91-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="e5a91-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="e5a91-122">(FLTK 예외가 있는 LGPL 2.0 전용 OR Apache-2.0+)</span><span class="sxs-lookup"><span data-stu-id="e5a91-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="e5a91-123">이 서비스는 nuget.org에서 허용되는 라이선스 식별자와 예외 식별자만 지원합니다. 지원되지 않는 라이선스 식별자 또는 라이선스 예외 식별자를 포함하거나 라이선스 식 구문을 준수하지 않는 모든 라이선스 식은 유효하지 않은 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="e5a91-124">응답</span><span class="sxs-lookup"><span data-stu-id="e5a91-124">Response</span></span>

<span data-ttu-id="e5a91-125">Licenses.nuget.org는 HTTP 200 상태 코드와 함께 유효한 라이선스 식을 포함하는 요청 및 라이선스 식에 대한 설명이 포함된 웹 페이지에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="e5a91-126">제공된 라이선스 식에 단일 라이선스 식별자가 포함된 경우 라이선스 참조 텍스트가 포함된 웹 페이지가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="e5a91-127">제공된 라이선스 식이 복합 라이선스 식인 경우 개별 라이선스 또는 라이선스 예외 참조에 대한 링크와 함께 라이선스 식이 포함된 웹 페이지가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="e5a91-128">잘못된 라이선스 식을 포함하는 모든 요청은 HTTP 404 응답을 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="e5a91-129">라이선스 예외</span><span class="sxs-lookup"><span data-stu-id="e5a91-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="e5a91-130">요청</span><span class="sxs-lookup"><span data-stu-id="e5a91-130">Request</span></span>

<span data-ttu-id="e5a91-131">라이선스 예외 식별자는 URL로 인코딩되어 licenses.nuget.org에 대한 요청의 경로로 사용되어야 합니다. 단일 라이선스 예외 식별자만 단일 요청으로 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="e5a91-132">라이선스 예외 식별자 외에도 추가 문자는 URL의 경로 부분에 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="e5a91-133">라이선스 예외 식별자</span><span class="sxs-lookup"><span data-stu-id="e5a91-133">License exception identifier</span></span> | <span data-ttu-id="e5a91-134">사용할 URL</span><span class="sxs-lookup"><span data-stu-id="e5a91-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="e5a91-135">FLTK 예외</span><span class="sxs-lookup"><span data-stu-id="e5a91-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="e5a91-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="e5a91-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="e5a91-137">응답</span><span class="sxs-lookup"><span data-stu-id="e5a91-137">Response</span></span>

<span data-ttu-id="e5a91-138">Licenses.nuget.org는 알려진 라이선스 예외 식별자가 있는 요청에 대해 HTTP 200 응답 및 지정된 라이선스 예외에 대한 참조 텍스트가 포함된 웹 페이지로 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="e5a91-139">지원되지 않는 라이선스 예외 식별자를 포함하는 모든 요청은 HTTP 404 응답을 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="e5a91-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>