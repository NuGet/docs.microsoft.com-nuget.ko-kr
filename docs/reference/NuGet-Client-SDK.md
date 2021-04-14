---
title: NuGet 클라이언트 SDK
description: API는 아직 문서화 되지 않고 진화 하 고 있지만 예제는 Dave Glick 위한 블로그에서 사용할 수 있습니다.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 6417c971dc13cf9ed05dcec4e4156af94c0ea058
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387389"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="78d7d-103">NuGet 클라이언트 SDK</span><span class="sxs-lookup"><span data-stu-id="78d7d-103">NuGet Client SDK</span></span>

<span data-ttu-id="78d7d-104">*Nuget 클라이언트 SDK* 는 nuget 패키지의 그룹을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="78d7d-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -HTTP 및 파일 기반 NuGet 피드를 조작 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="78d7d-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -NuGet 패키지와 상호 작용 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="78d7d-107">`NuGet.Protocol` 이 패키지에 종속</span><span class="sxs-lookup"><span data-stu-id="78d7d-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="78d7d-108">[Nuget/nuget. 클라이언트](https://github.com/NuGet/NuGet.Client) GitHub 리포지토리에서 이러한 패키지에 대 한 소스 코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>
<span data-ttu-id="78d7d-109">GitHub의 [NuGet. Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) 프로젝트에서 이러한 예제에 대 한 소스 코드를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-109">You can find the source code for these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) project on GitHub.</span></span>

> [!Note]
> <span data-ttu-id="78d7d-110">NuGet 서버 프로토콜에 대 한 설명서는 [Nuget 서버 API](~/api/overview.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="78d7d-110">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="nugetprotocol"></a><span data-ttu-id="78d7d-111">NuGet. 프로토콜</span><span class="sxs-lookup"><span data-stu-id="78d7d-111">NuGet.Protocol</span></span>

<span data-ttu-id="78d7d-112">`NuGet.Protocol`HTTP 및 폴더 기반 NuGet 패키지 피드를 사용 하 여 상호 작용 하는 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-112">Install the `NuGet.Protocol` package to interact with HTTP and folder-based NuGet package feeds:</span></span>

```ps1
dotnet add package NuGet.Protocol
```

> [!Tip]
> <span data-ttu-id="78d7d-113">`Repository.Factory` 는 네임 스페이스에 정의 되 `NuGet.Protocol.Core.Types` 고 `GetCoreV3` 메서드는 네임 스페이스에 정의 된 확장 메서드입니다 `NuGet.Protocol` .</span><span class="sxs-lookup"><span data-stu-id="78d7d-113">`Repository.Factory` is defined in the `NuGet.Protocol.Core.Types` namespace, and the `GetCoreV3` method is an extension method defined in the `NuGet.Protocol` namespace.</span></span> <span data-ttu-id="78d7d-114">따라서 `using` 두 네임 스페이스에 대 한 문을 추가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-114">Therefore, you will need to add `using` statements for both namespaces.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="78d7d-115">패키지 버전 나열</span><span class="sxs-lookup"><span data-stu-id="78d7d-115">List package versions</span></span>

<span data-ttu-id="78d7d-116">[NuGet V3 패키지 콘텐츠 API](../api/package-base-address-resource.md#enumerate-package-versions)를 사용 하 여 Newtonsoft.Js모든 버전을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-116">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="78d7d-117">패키지 다운로드</span><span class="sxs-lookup"><span data-stu-id="78d7d-117">Download a package</span></span>

<span data-ttu-id="78d7d-118">[NuGet V3 패키지 콘텐츠 API](../api/package-base-address-resource.md)를 사용 하 여 v 12.0.1에서 Newtonsoft.Js를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-118">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="78d7d-119">패키지 메타 데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="78d7d-119">Get package metadata</span></span>

<span data-ttu-id="78d7d-120">[NuGet V3 패키지 메타 데이터 API](../api/registration-base-url-resource.md)를 사용 하 여 "Newtonsoft.Json" 패키지에 대 한 메타 데이터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-120">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="78d7d-121">패키지 검색</span><span class="sxs-lookup"><span data-stu-id="78d7d-121">Search packages</span></span>

<span data-ttu-id="78d7d-122">[NuGet V3 검색 API](../api/search-query-service-resource.md)를 사용 하 여 "json" 패키지를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-122">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a><span data-ttu-id="78d7d-123">패키지 푸시</span><span class="sxs-lookup"><span data-stu-id="78d7d-123">Push a package</span></span>

<span data-ttu-id="78d7d-124">[NuGet V3 push 및 DELETE API](../api/package-publish-resource.md)를 사용 하 여 패키지를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-124">Push a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a><span data-ttu-id="78d7d-125">패키지 삭제</span><span class="sxs-lookup"><span data-stu-id="78d7d-125">Delete a package</span></span>

<span data-ttu-id="78d7d-126">[NuGet V3 Push 및 DELETE API](../api/package-publish-resource.md)를 사용 하 여 패키지를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-126">Delete a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

> [!Note]
> <span data-ttu-id="78d7d-127">NuGet 서버는 패키지 삭제 요청을 "하드 삭제", "일시 삭제" 또는 "unlist"로 자유롭게 해석할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-127">NuGet servers are free to interpret a package delete request as a "hard delete", "soft delete", or "unlist".</span></span>
> <span data-ttu-id="78d7d-128">예를 들어 nuget.org는 패키지 삭제 요청을 "unlist"로 해석 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-128">For example, nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="78d7d-129">이 방법에 대 한 자세한 내용은 [패키지 삭제](../nuget-org/policies/deleting-packages.md) 정책을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="78d7d-129">For more information about this practice, see the [Deleting Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span>

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a><span data-ttu-id="78d7d-130">인증 된 피드에 대 한 작업</span><span class="sxs-lookup"><span data-stu-id="78d7d-130">Work with authenticated feeds</span></span>

<span data-ttu-id="78d7d-131">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol)인증 된 피드에 대 한 작업을 수행 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-131">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) to work with authenticated feeds.</span></span>

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a><span data-ttu-id="78d7d-132">NuGet. 패키징</span><span class="sxs-lookup"><span data-stu-id="78d7d-132">NuGet.Packaging</span></span>

<span data-ttu-id="78d7d-133">`NuGet.Packaging`스트림에서 및 파일과 상호 작용 하는 패키지를 설치 합니다 `.nupkg` `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="78d7d-133">Install the `NuGet.Packaging` package to interact with `.nupkg` and `.nuspec` files from a stream:</span></span>

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a><span data-ttu-id="78d7d-134">패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="78d7d-134">Create a package</span></span>

<span data-ttu-id="78d7d-135">를 사용 하 여 패키지를 만들고, 메타 데이터를 설정 하 고, 종속성을 추가 [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-135">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78d7d-136">이 낮은 수준의 API를 사용 **하지 않고** 공식 nuget 도구를 사용 하 여 nuget 패키지를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-136">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="78d7d-137">잘 구성 된 패키지에는 다양 한 특성이 중요 하며, 최신 버전의 도구는 이러한 모범 사례를 통합 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-137">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="78d7d-138">NuGet 패키지를 만드는 방법에 대 한 자세한 내용은 [패키지 만들기 워크플로의](../create-packages/overview-and-workflow.md) 개요 및 공식 팩 도구 (예: [dotnet CLI 사용](../create-packages/creating-a-package-dotnet-cli.md))에 대 한 설명서를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="78d7d-138">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="78d7d-139">패키지 읽기</span><span class="sxs-lookup"><span data-stu-id="78d7d-139">Read a package</span></span>

<span data-ttu-id="78d7d-140">을 사용 하 여 파일 스트림에서 패키지를 읽습니다 [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .</span><span class="sxs-lookup"><span data-stu-id="78d7d-140">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="78d7d-141">타사 설명서</span><span class="sxs-lookup"><span data-stu-id="78d7d-141">Third-party documentation</span></span>

<span data-ttu-id="78d7d-142">다음 블로그 시리즈의 일부 API에 대 한 예제 및 설명서는 2016 게시에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-142">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="78d7d-143">NuGet v3 라이브러리 탐색, 1 부: 소개 및 개념</span><span class="sxs-lookup"><span data-stu-id="78d7d-143">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="78d7d-144">NuGet v3 라이브러리 탐색, 2 부: 패키지 검색</span><span class="sxs-lookup"><span data-stu-id="78d7d-144">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="78d7d-145">NuGet v3 라이브러리 탐색, 3 부: 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="78d7d-145">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="78d7d-146">이러한 블로그 게시물은 NuGet 클라이언트 SDK 패키지의 **3.4.3** 버전이 릴리스된 직후에 작성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-146">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="78d7d-147">최신 버전의 패키지가 블로그 게시물의 정보와 호환 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-147">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="78d7d-148">Martin Björkström에는 nuget 클라이언트 SDK를 사용 하 여 NuGet 패키지를 설치 하는 다른 방법을 소개 하는 Dave Glick의 블로그 시리즈에 대 한 후속 블로그 게시물이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-148">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="78d7d-149">NuGet v3 라이브러리를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="78d7d-149">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
