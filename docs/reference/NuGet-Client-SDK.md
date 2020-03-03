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
# <a name="nuget-client-sdk"></a>NuGet 클라이언트 SDK

*Nuget 클라이언트 SDK* 는 nuget 패키지의 그룹을 참조 합니다.

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -HTTP 및 파일 기반 NuGet 피드를 조작 하는 데 사용 됩니다.
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -NuGet 패키지와 상호 작용 하는 데 사용 됩니다. 이 패키지에 종속 `NuGet.Protocol`

[Nuget/nuget. 클라이언트](https://github.com/NuGet/NuGet.Client) GitHub 리포지토리에서 이러한 패키지에 대 한 소스 코드를 찾을 수 있습니다.

> [!Note]
> NuGet 서버 프로토콜에 대 한 설명서는 [Nuget 서버 API](~/api/overview.md)를 참조 하세요.

## <a name="getting-started"></a>시작

### <a name="install-the-package"></a>패키지 설치

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a>예

GitHub의 [nuget.exe](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) 프로젝트에서 이러한 예제를 찾을 수 있습니다.

### <a name="list-package-versions"></a>패키지 버전 나열

[NuGet V3 패키지 콘텐츠 API](../api/package-base-address-resource.md#enumerate-package-versions)를 사용 하 여 newtonsoft.json의 모든 버전을 찾습니다.

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>패키지 다운로드

[NuGet V3 패키지 콘텐츠 API](../api/package-base-address-resource.md)를 사용 하 여 newtonsoft.json v 12.0.1를 다운로드 합니다.

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>패키지 메타 데이터 가져오기

[NuGet V3 패키지 메타 데이터 API](../api/registration-base-url-resource.md)를 사용 하 여 "newtonsoft.json" 패키지에 대 한 메타 데이터를 가져옵니다.

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>패키지 검색

[NuGet V3 검색 API](../api/search-query-service-resource.md)를 사용 하 여 "json" 패키지를 검색 합니다.

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

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
