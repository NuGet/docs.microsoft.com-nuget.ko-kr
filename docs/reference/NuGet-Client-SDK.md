---
title: NuGet 클라이언트 SDK
description: API는 아직 문서화 되지 않고 진화 하 고 있지만 예제는 Dave Glick 위한 블로그에서 사용할 수 있습니다.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: e89b50601deb204892536406b4ddabf7005e0642
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776137"
---
# <a name="nuget-client-sdk"></a>NuGet 클라이언트 SDK

*Nuget 클라이언트 SDK* 는 nuget 패키지의 그룹을 참조 합니다.

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -HTTP 및 파일 기반 NuGet 피드를 조작 하는 데 사용 됩니다.
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -NuGet 패키지와 상호 작용 하는 데 사용 됩니다. `NuGet.Protocol` 이 패키지에 종속

[Nuget/nuget. 클라이언트](https://github.com/NuGet/NuGet.Client) GitHub 리포지토리에서 이러한 패키지에 대 한 소스 코드를 찾을 수 있습니다.
GitHub의 [NuGet. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) 프로젝트에서 이러한 예제에 대 한 소스 코드를 찾을 수 있습니다.

> [!Note]
> NuGet 서버 프로토콜에 대 한 설명서는 [Nuget 서버 API](~/api/overview.md)를 참조 하세요.

## <a name="nugetprotocol"></a>NuGet. 프로토콜

`NuGet.Protocol`HTTP 및 폴더 기반 NuGet 패키지 피드를 사용 하 여 상호 작용 하는 패키지를 설치 합니다.

```ps1
dotnet add package NuGet.Protocol
```

### <a name="list-package-versions"></a>패키지 버전 나열

[NuGet V3 패키지 콘텐츠 API](../api/package-base-address-resource.md#enumerate-package-versions)를 사용 하 여 Newtonsoft.Js모든 버전을 찾습니다.

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>패키지 다운로드

[NuGet V3 패키지 콘텐츠 API](../api/package-base-address-resource.md)를 사용 하 여 v 12.0.1에서 Newtonsoft.Js를 다운로드 합니다.

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>패키지 메타 데이터 가져오기

[NuGet V3 패키지 메타 데이터 API](../api/registration-base-url-resource.md)를 사용 하 여 "Newtonsoft.Json" 패키지에 대 한 메타 데이터를 가져옵니다.

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>패키지 검색

[NuGet V3 검색 API](../api/search-query-service-resource.md)를 사용 하 여 "json" 패키지를 검색 합니다.

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a>패키지 푸시

[NuGet V3 push 및 DELETE API](../api/package-publish-resource.md)를 사용 하 여 패키지를 푸시합니다.

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a>패키지 삭제

[NuGet V3 Push 및 DELETE API](../api/package-publish-resource.md)를 사용 하 여 패키지를 삭제 합니다.

> [!Note]
> NuGet 서버는 패키지 삭제 요청을 "하드 삭제", "일시 삭제" 또는 "unlist"로 자유롭게 해석할 수 있습니다.
> 예를 들어 nuget.org는 패키지 삭제 요청을 "unlist"로 해석 합니다. 이 방법에 대 한 자세한 내용은 [패키지 삭제](../nuget-org/policies/deleting-packages.md) 정책을 참조 하세요.

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a>인증 된 피드에 대 한 작업

[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol)인증 된 피드에 대 한 작업을 수행 하는 데 사용 합니다.

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a>NuGet. 패키징

`NuGet.Packaging`스트림에서 및 파일과 상호 작용 하는 패키지를 설치 합니다 `.nupkg` `.nuspec` .

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a>패키지 만들기

를 사용 하 여 패키지를 만들고, 메타 데이터를 설정 하 고, 종속성을 추가 [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) 합니다.

> [!IMPORTANT]
> 이 낮은 수준의 API를 사용 **하지 않고** 공식 nuget 도구를 사용 하 여 nuget 패키지를 만드는 것이 좋습니다. 잘 구성 된 패키지에는 다양 한 특성이 중요 하며, 최신 버전의 도구는 이러한 모범 사례를 통합 하는 데 도움이 됩니다.
> 
> NuGet 패키지를 만드는 방법에 대 한 자세한 내용은 [패키지 만들기 워크플로의](../create-packages/overview-and-workflow.md) 개요 및 공식 팩 도구 (예: [dotnet CLI 사용](../create-packages/creating-a-package-dotnet-cli.md))에 대 한 설명서를 참조 하세요.

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a>패키지 읽기

을 사용 하 여 파일 스트림에서 패키지를 읽습니다 [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a>타사 설명서

다음 블로그 시리즈의 일부 API에 대 한 예제 및 설명서는 2016 게시에 나와 있습니다.

- [NuGet v3 라이브러리 탐색, 1 부: 소개 및 개념](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [NuGet v3 라이브러리 탐색, 2 부: 패키지 검색](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [NuGet v3 라이브러리 탐색, 3 부: 패키지 설치](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> 이러한 블로그 게시물은 NuGet 클라이언트 SDK 패키지의 **3.4.3** 버전이 릴리스된 직후에 작성 되었습니다.
> 최신 버전의 패키지가 블로그 게시물의 정보와 호환 되지 않을 수 있습니다.

Martin Björkström에는 nuget 클라이언트 SDK를 사용 하 여 NuGet 패키지를 설치 하는 다른 방법을 소개 하는 Dave Glick의 블로그 시리즈에 대 한 후속 블로그 게시물이 있습니다.

- [NuGet v3 라이브러리를 방문 합니다.](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
