---
title: NuGet 클라이언트 SDK
description: API는 아직 문서화 되지 않고 진화 하 고 있지만 예제는 Dave Glick 위한 블로그에서 사용할 수 있습니다.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: a5c542379318f24ee35ccf25651d0e8de91253ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231242"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="c7685-103">NuGet 클라이언트 SDK</span><span class="sxs-lookup"><span data-stu-id="c7685-103">NuGet Client SDK</span></span>

<span data-ttu-id="c7685-104">*Nuget 클라이언트 SDK* 는 nuget 패키지의 그룹을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7685-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="c7685-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -HTTP 및 파일 기반 NuGet 피드를 조작 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7685-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="c7685-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -NuGet 패키지와 상호 작용 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7685-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="c7685-107">이 패키지에 종속 `NuGet.Protocol`</span><span class="sxs-lookup"><span data-stu-id="c7685-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="c7685-108">[Nuget/nuget. 클라이언트](https://github.com/NuGet/NuGet.Client) GitHub 리포지토리에서 이러한 패키지에 대 한 소스 코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7685-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="c7685-109">NuGet 서버 프로토콜에 대 한 설명서는 [Nuget 서버 API](~/api/overview.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c7685-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="c7685-110">시작</span><span class="sxs-lookup"><span data-stu-id="c7685-110">Getting started</span></span>

### <a name="install-the-package"></a><span data-ttu-id="c7685-111">패키지 설치</span><span class="sxs-lookup"><span data-stu-id="c7685-111">Install the package</span></span>

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a><span data-ttu-id="c7685-112">예</span><span class="sxs-lookup"><span data-stu-id="c7685-112">Examples</span></span>

<span data-ttu-id="c7685-113">GitHub의 [nuget.exe](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) 프로젝트에서 이러한 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7685-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="c7685-114">패키지 버전 나열</span><span class="sxs-lookup"><span data-stu-id="c7685-114">List package versions</span></span>

<span data-ttu-id="c7685-115">[NuGet V3 패키지 콘텐츠 API](../api/package-base-address-resource.md#enumerate-package-versions)를 사용 하 여 newtonsoft.json의 모든 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c7685-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="c7685-116">패키지 다운로드</span><span class="sxs-lookup"><span data-stu-id="c7685-116">Download a package</span></span>

<span data-ttu-id="c7685-117">[NuGet V3 패키지 콘텐츠 API](../api/package-base-address-resource.md)를 사용 하 여 newtonsoft.json v 12.0.1를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7685-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="c7685-118">패키지 메타 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="c7685-118">Get package metadata</span></span>

<span data-ttu-id="c7685-119">[NuGet V3 패키지 메타 데이터 API](../api/registration-base-url-resource.md)를 사용 하 여 "newtonsoft.json" 패키지에 대 한 메타 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c7685-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="c7685-120">패키지 검색</span><span class="sxs-lookup"><span data-stu-id="c7685-120">Search packages</span></span>

<span data-ttu-id="c7685-121">[NuGet V3 검색 API](../api/search-query-service-resource.md)를 사용 하 여 "json" 패키지를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7685-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a><span data-ttu-id="c7685-122">타사 설명서</span><span class="sxs-lookup"><span data-stu-id="c7685-122">Third-party documentation</span></span>

<span data-ttu-id="c7685-123">다음 블로그 시리즈의 일부 API에 대 한 예제 및 설명서는 2016 게시에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7685-123">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="c7685-124">NuGet v3 라이브러리 탐색, 1 부: 소개 및 개념</span><span class="sxs-lookup"><span data-stu-id="c7685-124">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="c7685-125">NuGet v3 라이브러리 탐색, 2 부: 패키지 검색</span><span class="sxs-lookup"><span data-stu-id="c7685-125">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="c7685-126">NuGet v3 라이브러리 탐색, 3 부: 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="c7685-126">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="c7685-127">이러한 블로그 게시물은 NuGet 클라이언트 SDK 패키지의 **3.4.3** 버전이 릴리스된 직후에 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c7685-127">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="c7685-128">최신 버전의 패키지가 블로그 게시물의 정보와 호환 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7685-128">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="c7685-129">Martin Björkström에는 nuget 클라이언트 SDK를 사용 하 여 NuGet 패키지를 설치 하는 다른 방법을 소개 하는 Dave Glick의 블로그 시리즈에 대 한 후속 블로그 게시물이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7685-129">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="c7685-130">NuGet v3 라이브러리를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7685-130">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
