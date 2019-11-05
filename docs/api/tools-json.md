---
title: nuget.exe 버전을 검색 하기 위한 도구입니다.
description: 의 끝점
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: a186db9727bdfd1b55bf73a1f29283352555dede
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611026"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="aeec8-103">nuget.exe 버전을 검색 하기 위한 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="aeec8-104">현재는 스크립트 가능한 방식으로 컴퓨터에서 최신 버전의 nuget.exe를 가져오는 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="aeec8-105">예를 들어 nuget.org에서 [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) 패키지를 다운로드 하 여 추출할 수 있습니다. 이는 이미 nuget.exe (`nuget.exe install`)를 사용 하거나, 기본 압축 풀기 도구를 사용 하 여 nupkg의 압축을 풀고 내부에서 이진 파일을 찾아야 하기 때문에 다소 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="aeec8-106">이미 nuget.exe를 사용 하 고 있는 경우에는 `nuget.exe update -self`를 사용할 수도 있지만이 경우에는 nuget.exe의 기존 복사본도 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="aeec8-107">이 방법은 사용자를 최신 버전으로 업데이트 하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="aeec8-108">특정 버전을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="aeec8-109">`tools.json` 끝점은 부트스트래핑 문제를 해결 하 고 다운로드 하는 nuget.exe 버전을 제어 하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="aeec8-110">이를 CI/CD 환경 또는 사용자 지정 스크립트에서 사용 하 여 모든 릴리스 버전의 nuget.exe를 검색 하 고 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="aeec8-111">`tools.json` 끝점은 인증 되지 않은 HTTP 요청 (예: PowerShell 또는 `wget``Invoke-WebRequest`)을 사용 하 여 페치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="aeec8-112">JSON 역직렬 변환기를 사용 하 여 구문 분석할 수 있으며 후속 nuget .exe 다운로드 Url은 인증 되지 않은 HTTP 요청을 사용 하 여 페치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="aeec8-113">`GET` 메서드를 사용 하 여 끝점을 페치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="aeec8-114">끝점에 대 한 [JSON 스키마](https://json-schema.org/) 는 여기에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="aeec8-115">응답</span><span class="sxs-lookup"><span data-stu-id="aeec8-115">Response</span></span>

<span data-ttu-id="aeec8-116">응답은 사용 가능한 모든 버전의 nuget.exe를 포함 하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="aeec8-117">루트 JSON 개체에는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="aeec8-118">name</span><span class="sxs-lookup"><span data-stu-id="aeec8-118">Name</span></span>      | <span data-ttu-id="aeec8-119">Type</span><span class="sxs-lookup"><span data-stu-id="aeec8-119">Type</span></span>             | <span data-ttu-id="aeec8-120">필요한 공간</span><span class="sxs-lookup"><span data-stu-id="aeec8-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="aeec8-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="aeec8-121">nuget.exe</span></span> | <span data-ttu-id="aeec8-122">개체의 배열</span><span class="sxs-lookup"><span data-stu-id="aeec8-122">array of objects</span></span> | <span data-ttu-id="aeec8-123">예</span><span class="sxs-lookup"><span data-stu-id="aeec8-123">yes</span></span>

<span data-ttu-id="aeec8-124">`nuget.exe` 배열에 있는 각 개체에는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="aeec8-125">name</span><span class="sxs-lookup"><span data-stu-id="aeec8-125">Name</span></span>     | <span data-ttu-id="aeec8-126">Type</span><span class="sxs-lookup"><span data-stu-id="aeec8-126">Type</span></span>   | <span data-ttu-id="aeec8-127">필요한 공간</span><span class="sxs-lookup"><span data-stu-id="aeec8-127">Required</span></span> | <span data-ttu-id="aeec8-128">노트</span><span class="sxs-lookup"><span data-stu-id="aeec8-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="aeec8-129">version</span><span class="sxs-lookup"><span data-stu-id="aeec8-129">version</span></span>  | <span data-ttu-id="aeec8-130">string</span><span class="sxs-lookup"><span data-stu-id="aeec8-130">string</span></span> | <span data-ttu-id="aeec8-131">예</span><span class="sxs-lookup"><span data-stu-id="aeec8-131">yes</span></span>      | <span data-ttu-id="aeec8-132">SemVer 2.0.0 문자열</span><span class="sxs-lookup"><span data-stu-id="aeec8-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="aeec8-133">url</span><span class="sxs-lookup"><span data-stu-id="aeec8-133">url</span></span>      | <span data-ttu-id="aeec8-134">string</span><span class="sxs-lookup"><span data-stu-id="aeec8-134">string</span></span> | <span data-ttu-id="aeec8-135">예</span><span class="sxs-lookup"><span data-stu-id="aeec8-135">yes</span></span>      | <span data-ttu-id="aeec8-136">이 버전의 nuget.exe를 다운로드 하는 데 사용할 절대 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="aeec8-137">단계</span><span class="sxs-lookup"><span data-stu-id="aeec8-137">stage</span></span>    | <span data-ttu-id="aeec8-138">string</span><span class="sxs-lookup"><span data-stu-id="aeec8-138">string</span></span> | <span data-ttu-id="aeec8-139">예</span><span class="sxs-lookup"><span data-stu-id="aeec8-139">yes</span></span>      | <span data-ttu-id="aeec8-140">열거형 문자열</span><span class="sxs-lookup"><span data-stu-id="aeec8-140">An enum string</span></span>
<span data-ttu-id="aeec8-141">함</span><span class="sxs-lookup"><span data-stu-id="aeec8-141">uploaded</span></span> | <span data-ttu-id="aeec8-142">string</span><span class="sxs-lookup"><span data-stu-id="aeec8-142">string</span></span> | <span data-ttu-id="aeec8-143">예</span><span class="sxs-lookup"><span data-stu-id="aeec8-143">yes</span></span>      | <span data-ttu-id="aeec8-144">버전을 사용 가능 하 게 설정한 경우의 대략적인 ISO 8601 타임 스탬프</span><span class="sxs-lookup"><span data-stu-id="aeec8-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="aeec8-145">배열의 항목은 내림차순 (SemVer 2.0.0 order)으로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="aeec8-146">이러한 보장은 가장 높은 버전 번호에 관심이 있는 클라이언트의 부담을 줄이기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="aeec8-147">그러나이는 목록이 시간순으로 정렬 되지 않음을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="aeec8-148">예를 들어 더 낮은 주 버전이 더 높은 주 버전 보다 나중에 서비스 되는 경우이 서비스 버전은 목록 맨 위에 나타나지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="aeec8-149">*타임 스탬프로*최신 버전을 해제 하려면 `uploaded` 문자열을 기준으로 배열을 정렬 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="aeec8-150">이는 `uploaded` 타임 스탬프가 [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 형식이 기 때문에 작동 합니다 .이는 사전순 정렬 (즉, 간단한 문자열 정렬)을 사용 하 여 시간순으로 정렬할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="aeec8-151">`stage` 속성은이 도구 버전의 점검 되었다는 방법을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="aeec8-152">단계</span><span class="sxs-lookup"><span data-stu-id="aeec8-152">Stage</span></span>              | <span data-ttu-id="aeec8-153">의미</span><span class="sxs-lookup"><span data-stu-id="aeec8-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="aeec8-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="aeec8-154">EarlyAccessPreview</span></span> | <span data-ttu-id="aeec8-155">[다운로드 웹 페이지](https://www.nuget.org/downloads) 에 아직 표시 되지 않으며 파트너가 유효성을 검사 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="aeec8-156">Released</span><span class="sxs-lookup"><span data-stu-id="aeec8-156">Released</span></span>           | <span data-ttu-id="aeec8-157">다운로드 사이트에서 사용할 수 있지만, 광범위 한 사용량에는 아직 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="aeec8-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="aeec8-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="aeec8-159">다운로드 사이트에서 사용할 수 있으며 소비에 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="aeec8-160">최신 권장 버전을 사용 하는 간단한 방법 중 하나는 `stage` 값이 `ReleasedAndBlessed`인 목록의 첫 번째 버전을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="aeec8-161">이는 버전이 SemVer 2.0.0 order로 정렬 되기 때문에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="aeec8-162">Nuget.org의 `NuGet.CommandLine` 패키지는 일반적으로 `ReleasedAndBlessed` 버전 으로만 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="aeec8-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="aeec8-163">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="aeec8-163">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="aeec8-164">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="aeec8-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
