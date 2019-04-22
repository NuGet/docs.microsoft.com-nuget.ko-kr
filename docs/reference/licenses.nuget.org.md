---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 4a40cc1f7d333e8d35a721f3eed2e6b9365faf7b
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58921561"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="b2658-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="b2658-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="b2658-103">설명</span><span class="sxs-lookup"><span data-stu-id="b2658-103">Rationale</span></span>

<span data-ttu-id="b2658-104">도입 된 [식 라이선스](nuspec.md#license), 개별 라이선스 식별자, 예외 식별자 또는 라이선스 식에 대 한 참조 텍스트를 제공 하는 신뢰할 수 있는 서비스에 등장 한 후 요구 사항.</span><span class="sxs-lookup"><span data-stu-id="b2658-104">With the introduction of the [license expressions](nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="b2658-105">이 서비스에 대 한 추가 요구 사항은 이전 버전의 클라이언트에 대 한 이전 버전과 호환성을 제공 하기 안전 하 게 사용할 수 있도록, rot에 대 한 연결에 취약 하지 않은 안정적인 URL 스키마를 가진 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b2658-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="b2658-106">Licenses.nuget.org 해당 역할을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2658-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="b2658-107">Nuget.org는 라이선스 식을 사용 하 여 해당 라이선스를 지정 하는 패키지에 대 한 라이선스 텍스트 참조를 제공 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2658-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="b2658-108">`nuget pack` 또는 다른 압축 [클라이언트 도구](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) 설정 된 [ `licenseUrl` ](nuspec.md#licenseurl) licenses.nuget.org 이전 버전과 호환성을 제공 하기를 지원 하지 않는 이전 버전의 클라이언트를 가리키도록 요소는 `license` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="b2658-108">`nuget pack` or packing with other [client tools](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) set the [`licenseUrl`](nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="b2658-109">프로토콜</span><span class="sxs-lookup"><span data-stu-id="b2658-109">Protocol</span></span>

<span data-ttu-id="b2658-110">사용자가 브라우저에서 볼 수 있도록 Licenses.nuget.org 것, 컴퓨터가 읽을 수 있는 응답이 없습니다 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2658-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="b2658-111">HTTPS 프로토콜을 사용 해야 하 고 요청을 특정 방식으로 생성할 수 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2658-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="b2658-112">지원 `GET` 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2658-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="b2658-113">라이선스 식 또는 라이선스 예외 식별자 아래에 지정 하는 방법에 대 한 입력으로 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2658-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="b2658-114">하세요 note, 라이선스 식의 모든 요소는 대 소문자를 구분 하 고 따라서 licenses.nuget.org에 대 한 모든 입력도 대/소문자 구분 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2658-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="b2658-115">라이선스 식</span><span class="sxs-lookup"><span data-stu-id="b2658-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="b2658-116">요청</span><span class="sxs-lookup"><span data-stu-id="b2658-116">Request</span></span>

<span data-ttu-id="b2658-117">라이선스 식 (식은 단일 라이선스의 경우 간단한 사례 포함) 일 필요가 [URL로 인코딩된](https://tools.ietf.org/html/rfc3986#section-2.1) licenses.nuget.org 요청에 경로로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2658-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="b2658-118">라이선스 식</span><span class="sxs-lookup"><span data-stu-id="b2658-118">License expression</span></span> | <span data-ttu-id="b2658-119">사용 하는 URL</span><span class="sxs-lookup"><span data-stu-id="b2658-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="b2658-120">MIT</span><span class="sxs-lookup"><span data-stu-id="b2658-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="b2658-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="b2658-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="b2658-122">(LGPL 2.0 전용 FLTK 예외 또는 Apache를 사용 하 여-2.0+)</span><span class="sxs-lookup"><span data-stu-id="b2658-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="b2658-123">서비스는 라이선스 식별자 및 nuget.org에서 허용 되는 라이선스 예외 식별자만 지원 합니다. 모든 라이선스 식은 지원 되지 않는 라이선스 식별자 또는 라이선스 예외 식별자를 포함 하는 라이선스 식 구문에 맞지 않습니다 또는 잘못 된 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2658-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="b2658-124">응답</span><span class="sxs-lookup"><span data-stu-id="b2658-124">Response</span></span>

<span data-ttu-id="b2658-125">Licenses.nuget.org는 HTTP 200 상태 코드 및 라이선스 식의 설명이 포함 된 웹 페이지를 사용 하 여 식이 유효한 라이선스가 포함 된 요청에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2658-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="b2658-126">라이선스 식을 제공 하는 경우 해당 라이선스 참조 텍스트를 포함 하는 웹 페이지는 반환 하는 단일 라이선스 식별자가 포함</span><span class="sxs-lookup"><span data-stu-id="b2658-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="b2658-127">제공 된 경우 라이선스 식은 복합 라이선스 식이고, 웹 페이지의 개별 라이선스 또는 라이선스 예외 참조에 대 한 링크를 사용 하 여 라이선스 식을 포함 하는 반환 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b2658-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="b2658-128">HTTP 404 응답에 잘못 된 라이선스 식 결과 포함 하는 모든 요청 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2658-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="b2658-129">라이선스 예외</span><span class="sxs-lookup"><span data-stu-id="b2658-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="b2658-130">요청</span><span class="sxs-lookup"><span data-stu-id="b2658-130">Request</span></span>

<span data-ttu-id="b2658-131">라이선스 예외 식별자 URL로 인코딩된 및 licenses.nuget.org 요청에 경로 사용 해야 합니다. 단일 라이선스 예외 식별자만 단일 요청에 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2658-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="b2658-132">라이선스 예외 식별자 외에도 추가 문자가 없는 URL의 경로 부분에 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b2658-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="b2658-133">라이선스 예외 식별자</span><span class="sxs-lookup"><span data-stu-id="b2658-133">License exception identifier</span></span> | <span data-ttu-id="b2658-134">사용 하는 URL</span><span class="sxs-lookup"><span data-stu-id="b2658-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="b2658-135">FLTK 예외</span><span class="sxs-lookup"><span data-stu-id="b2658-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="b2658-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="b2658-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="b2658-137">응답</span><span class="sxs-lookup"><span data-stu-id="b2658-137">Response</span></span>

<span data-ttu-id="b2658-138">Licenses.nuget.org는 HTTP 200 응답 및 지정 된 라이선스는 예외에 대 한 참조 텍스트를 포함 하는 웹 페이지를 사용 하 여 알려진된 라이선스 예외 식별자를 사용 하 여 요청에 응답 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2658-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="b2658-139">지원 되지 않는 라이선스 예외 식별자를 포함 하는 모든 요청에서 HTTP 404 응답을 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="b2658-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>