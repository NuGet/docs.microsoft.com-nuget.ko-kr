---
title: NuGet 클라이언트 SDK
description: API는 아직 문서화 되지 않고 진화 하 고 있지만 예제는 Dave Glick 위한 블로그에서 사용할 수 있습니다.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 39a4de4071eec70c88a2add158f2a3a734f7d7b7
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622930"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="a3e73-103">NuGet 클라이언트 SDK</span><span class="sxs-lookup"><span data-stu-id="a3e73-103">NuGet Client SDK</span></span>

<span data-ttu-id="a3e73-104">*Nuget 클라이언트 SDK* 는 nuget 패키지의 그룹을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e73-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="a3e73-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -HTTP 및 파일 기반 NuGet 피드를 조작 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3e73-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="a3e73-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -NuGet 패키지와 상호 작용 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3e73-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="a3e73-107">`NuGet.Protocol` 이 패키지에 종속</span><span class="sxs-lookup"><span data-stu-id="a3e73-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="a3e73-108">[Nuget/nuget. 클라이언트](https://github.com/NuGet/NuGet.Client) GitHub 리포지토리에서 이러한 패키지에 대 한 소스 코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e73-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="a3e73-109">NuGet 서버 프로토콜에 대 한 설명서는 [Nuget 서버 API](~/api/overview.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a3e73-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="a3e73-110">시작</span><span class="sxs-lookup"><span data-stu-id="a3e73-110">Getting started</span></span>

### <a name="install-the-packages"></a><span data-ttu-id="a3e73-111">패키지 설치</span><span class="sxs-lookup"><span data-stu-id="a3e73-111">Install the packages</span></span>

```ps1
dotnet add package NuGet.Protocol  # interact with HTTP and folder-based NuGet package feeds, includes NuGet.Packaging

dotnet add package NuGet.Packaging # interact with .nupkg and .nuspec files from a stream
```

## <a name="examples"></a><span data-ttu-id="a3e73-112">예제</span><span class="sxs-lookup"><span data-stu-id="a3e73-112">Examples</span></span>

<span data-ttu-id="a3e73-113">GitHub의 [nuget.exe](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) 프로젝트에서 이러한 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e73-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="a3e73-114">패키지 버전 나열</span><span class="sxs-lookup"><span data-stu-id="a3e73-114">List package versions</span></span>

<span data-ttu-id="a3e73-115">[NuGet V3 패키지 콘텐츠 API](../api/package-base-address-resource.md#enumerate-package-versions)를 사용 하 여 Newtonsoft.Js모든 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e73-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="a3e73-116">패키지 다운로드</span><span class="sxs-lookup"><span data-stu-id="a3e73-116">Download a package</span></span>

<span data-ttu-id="a3e73-117">[NuGet V3 패키지 콘텐츠 API](../api/package-base-address-resource.md)를 사용 하 여 v 12.0.1에서 Newtonsoft.Js를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e73-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="a3e73-118">패키지 메타 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="a3e73-118">Get package metadata</span></span>

<span data-ttu-id="a3e73-119">[NuGet V3 패키지 메타 데이터 API](../api/registration-base-url-resource.md)를 사용 하 여 "Newtonsoft.Json" 패키지에 대 한 메타 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a3e73-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="a3e73-120">패키지 검색</span><span class="sxs-lookup"><span data-stu-id="a3e73-120">Search packages</span></span>

<span data-ttu-id="a3e73-121">[NuGet V3 검색 API](../api/search-query-service-resource.md)를 사용 하 여 "json" 패키지를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e73-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="create-a-package"></a><span data-ttu-id="a3e73-122">패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="a3e73-122">Create a package</span></span>

<span data-ttu-id="a3e73-123">를 사용 하 여 패키지를 만들고, 메타 데이터를 설정 하 고, 종속성을 추가 [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e73-123">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a3e73-124">이 낮은 수준의 API를 사용 **하지 않고** 공식 nuget 도구를 사용 하 여 nuget 패키지를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e73-124">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="a3e73-125">잘 구성 된 패키지에는 다양 한 특성이 중요 하며, 최신 버전의 도구는 이러한 모범 사례를 통합 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a3e73-125">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="a3e73-126">NuGet 패키지를 만드는 방법에 대 한 자세한 내용은 [패키지 만들기 워크플로의](../create-packages/overview-and-workflow.md) 개요 및 공식 팩 도구 (예: [dotnet CLI 사용](../create-packages/creating-a-package-dotnet-cli.md))에 대 한 설명서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a3e73-126">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="a3e73-127">패키지 읽기</span><span class="sxs-lookup"><span data-stu-id="a3e73-127">Read a package</span></span>

<span data-ttu-id="a3e73-128">을 사용 하 여 파일 스트림에서 패키지를 읽습니다 [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="a3e73-128">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="a3e73-129">타사 설명서</span><span class="sxs-lookup"><span data-stu-id="a3e73-129">Third-party documentation</span></span>

<span data-ttu-id="a3e73-130">다음 블로그 시리즈의 일부 API에 대 한 예제 및 설명서는 2016 게시에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e73-130">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="a3e73-131">NuGet v3 라이브러리 탐색, 1 부: 소개 및 개념</span><span class="sxs-lookup"><span data-stu-id="a3e73-131">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="a3e73-132">NuGet v3 라이브러리 탐색, 2 부: 패키지 검색</span><span class="sxs-lookup"><span data-stu-id="a3e73-132">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="a3e73-133">NuGet v3 라이브러리 탐색, 3 부: 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="a3e73-133">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="a3e73-134">이러한 블로그 게시물은 NuGet 클라이언트 SDK 패키지의 **3.4.3** 버전이 릴리스된 직후에 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e73-134">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="a3e73-135">최신 버전의 패키지가 블로그 게시물의 정보와 호환 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e73-135">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="a3e73-136">Martin Björkström에는 nuget 클라이언트 SDK를 사용 하 여 NuGet 패키지를 설치 하는 다른 방법을 소개 하는 Dave Glick의 블로그 시리즈에 대 한 후속 블로그 게시물이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a3e73-136">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="a3e73-137">NuGet v3 라이브러리를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="a3e73-137">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
