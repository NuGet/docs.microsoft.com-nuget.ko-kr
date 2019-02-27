---
title: tools.json nuget.exe 버전 검색
description: 에 대 한 끝점
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 003139abac7808dbdaef4aa66119e09772db2b4f
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852535"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="dac8b-103">tools.json nuget.exe 버전 검색</span><span class="sxs-lookup"><span data-stu-id="dac8b-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="dac8b-104">현재는 스크립팅 가능한 방식으로 컴퓨터에 최신 버전의 nuget.exe 가져오려면 몇 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="dac8b-105">다운로드를 추출 하는 예를 들어 합니다 [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) nuget.org에서 패키지 있습니다. Nuget.exe를 이미가지고 있다고 하거나 필요 하므로이 일부 복잡성 (에 대 한 `nuget.exe install`)는 기본 압축 풀기 도구를 사용 하 여.nupkg 압축을 풀고 이진 내부 찾을를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="dac8b-106">Nuget.exe가 이미 있는 경우 사용할 수도 있습니다 `nuget.exe update -self`이지만 nuget.exe의 기존 복사본을 포함 합니다.이 또한 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="dac8b-107">이 방법은 또한 업데이트를 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="dac8b-108">특정 버전을 사용 하 여를 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="dac8b-109">`tools.json` 끝점 수 둘 다 부트스트래핑 문제를 해결 및 다운로드 nuget.exe의 버전 제어를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="dac8b-110">이 수 사용자 지정 스크립트 또는 CI/CD 환경에서 검색 하 고 릴리스된 모든 버전의 nuget.exe 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="dac8b-111">합니다 `tools.json` 인증 되지 않은 HTTP 요청을 사용 하 여 끝점을 인출할 수 있습니다 (예: `Invoke-WebRequest` PowerShell에서 또는 `wget`).</span><span class="sxs-lookup"><span data-stu-id="dac8b-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="dac8b-112">JSON 역직렬 변환기를 사용 하 여 구문 분석할 수 및 HTTP 요청을 인증 되지 않은 후속 nuget.exe 다운로드를 사용 하 여 Url 인출할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="dac8b-113">사용 하 여 끝점을 인출할 수 있습니다는 `GET` 메서드:</span><span class="sxs-lookup"><span data-stu-id="dac8b-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="dac8b-114">합니다 [JSON 스키마](http://json-schema.org/) 끝점 여기 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="dac8b-115">응답</span><span class="sxs-lookup"><span data-stu-id="dac8b-115">Response</span></span>

<span data-ttu-id="dac8b-116">응답은 모든 사용 가능한 버전의 nuget.exe 포함 하는 JSON 문서입니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="dac8b-117">루트 JSON 개체에는 다음과 같은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="dac8b-118">이름</span><span class="sxs-lookup"><span data-stu-id="dac8b-118">Name</span></span>      | <span data-ttu-id="dac8b-119">형식</span><span class="sxs-lookup"><span data-stu-id="dac8b-119">Type</span></span>             | <span data-ttu-id="dac8b-120">필수</span><span class="sxs-lookup"><span data-stu-id="dac8b-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="dac8b-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="dac8b-121">nuget.exe</span></span> | <span data-ttu-id="dac8b-122">개체의 배열</span><span class="sxs-lookup"><span data-stu-id="dac8b-122">array of objects</span></span> | <span data-ttu-id="dac8b-123">예</span><span class="sxs-lookup"><span data-stu-id="dac8b-123">yes</span></span>

<span data-ttu-id="dac8b-124">각 개체는 `nuget.exe` 배열에는 다음 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="dac8b-125">이름</span><span class="sxs-lookup"><span data-stu-id="dac8b-125">Name</span></span>     | <span data-ttu-id="dac8b-126">형식</span><span class="sxs-lookup"><span data-stu-id="dac8b-126">Type</span></span>   | <span data-ttu-id="dac8b-127">필수</span><span class="sxs-lookup"><span data-stu-id="dac8b-127">Required</span></span> | <span data-ttu-id="dac8b-128">노트</span><span class="sxs-lookup"><span data-stu-id="dac8b-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="dac8b-129">버전</span><span class="sxs-lookup"><span data-stu-id="dac8b-129">version</span></span>  | <span data-ttu-id="dac8b-130">string</span><span class="sxs-lookup"><span data-stu-id="dac8b-130">string</span></span> | <span data-ttu-id="dac8b-131">예</span><span class="sxs-lookup"><span data-stu-id="dac8b-131">yes</span></span>      | <span data-ttu-id="dac8b-132">SemVer 2.0.0 문자열</span><span class="sxs-lookup"><span data-stu-id="dac8b-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="dac8b-133">url</span><span class="sxs-lookup"><span data-stu-id="dac8b-133">url</span></span>      | <span data-ttu-id="dac8b-134">string</span><span class="sxs-lookup"><span data-stu-id="dac8b-134">string</span></span> | <span data-ttu-id="dac8b-135">예</span><span class="sxs-lookup"><span data-stu-id="dac8b-135">yes</span></span>      | <span data-ttu-id="dac8b-136">이 버전의 nuget.exe 다운로드 하는 것에 대 한 절대 URL</span><span class="sxs-lookup"><span data-stu-id="dac8b-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="dac8b-137">stage(단계)</span><span class="sxs-lookup"><span data-stu-id="dac8b-137">stage</span></span>    | <span data-ttu-id="dac8b-138">string</span><span class="sxs-lookup"><span data-stu-id="dac8b-138">string</span></span> | <span data-ttu-id="dac8b-139">예</span><span class="sxs-lookup"><span data-stu-id="dac8b-139">yes</span></span>      | <span data-ttu-id="dac8b-140">열거형 문자열</span><span class="sxs-lookup"><span data-stu-id="dac8b-140">An enum string</span></span>
<span data-ttu-id="dac8b-141">업로드</span><span class="sxs-lookup"><span data-stu-id="dac8b-141">uploaded</span></span> | <span data-ttu-id="dac8b-142">string</span><span class="sxs-lookup"><span data-stu-id="dac8b-142">string</span></span> | <span data-ttu-id="dac8b-143">예</span><span class="sxs-lookup"><span data-stu-id="dac8b-143">yes</span></span>      | <span data-ttu-id="dac8b-144">버전을 사용할 수 있었던 경우의 대략적인 ISO 8601 타임 스탬프를</span><span class="sxs-lookup"><span data-stu-id="dac8b-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="dac8b-145">배열의 항목 내림차순, SemVer 2.0.0 순서로 정렬 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="dac8b-146">이러한 변환이 가장 높은 버전 번호를 클라이언트의 부담을 줄일 수 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="dac8b-147">그러나 시간 순서 대로 정렬에서 된 목록이 정렬 되지 않으면이 의미가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="dac8b-148">예를 들어, 낮은 주 버전은 더 높은 주 버전 이후 날짜에 서비스를 제공 하는 경우이 서비스 버전 목록 위쪽에 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="dac8b-149">출시 된 최신 버전을 원하는 경우 *타임 스탬프*, 단순히로 배열의 정렬를 `uploaded` 문자열.</span><span class="sxs-lookup"><span data-stu-id="dac8b-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="dac8b-150">이므로이 방법을 사용 합니다 `uploaded` 타임 스탬프에는 [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 사전순으로 정렬 (즉, 간단한 문자열 정렬)을 사용 하 여 시간 순으로 정렬 될 수 있는 형식으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="dac8b-151">`stage` 속성 하는 방법을 점검이 버전의 도구 인지 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="dac8b-152">단계</span><span class="sxs-lookup"><span data-stu-id="dac8b-152">Stage</span></span>              | <span data-ttu-id="dac8b-153">의미</span><span class="sxs-lookup"><span data-stu-id="dac8b-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="dac8b-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="dac8b-154">EarlyAccessPreview</span></span> | <span data-ttu-id="dac8b-155">에 표시 되지 않습니다 합니다 [웹 페이지 다운로드](https://www.nuget.org/downloads) 파트너가 유효성을 검사 해야 하 고</span><span class="sxs-lookup"><span data-stu-id="dac8b-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="dac8b-156">Released</span><span class="sxs-lookup"><span data-stu-id="dac8b-156">Released</span></span>           | <span data-ttu-id="dac8b-157">다운로드 사이트에서 사용 가능 하지만 아직 광범위 소비에 대 한 권장</span><span class="sxs-lookup"><span data-stu-id="dac8b-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="dac8b-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="dac8b-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="dac8b-159">다운로드 사이트에서 사용할 수 있는 사용에 대 한 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="dac8b-160">최신 것에 대 한 한 가지 간단한 방법은 권장 버전이 있는 목록의 첫 번째 버전을 사용 하는 `stage` 의 값 `ReleasedAndBlessed`합니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="dac8b-161">이 버전은 SemVer 2.0.0 순서로 정렬 되므로 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="dac8b-162">합니다 `NuGet.CommandLine` nuget.org에서 패키지는 일반적으로 사용 하 여 업데이트만 `ReleasedAndBlessed` 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="dac8b-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="dac8b-163">샘플 요청</span><span class="sxs-lookup"><span data-stu-id="dac8b-163">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="dac8b-164">샘플 응답</span><span class="sxs-lookup"><span data-stu-id="dac8b-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
