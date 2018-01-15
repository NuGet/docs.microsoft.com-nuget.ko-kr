---
title: "nuget.org에 게시된 모든 패키지에 대한 쿼리 | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 11/2/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 5d017cd4-3d75-4341-ba90-3c57be093b7d
description: "NuGet API를 사용하면 nuget.org에 게시된 모든 패키지에 대해 쿼리하고 시간이 지남에 따라 최신 상태를 유지할 수 있습니다."
keywords: "NuGet API는 모든 패키지를 열거하고, NuGet API는 패키지, 즉 nuget.org에 게시된 최신 패키지를 복제합니다."
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 5559a7cd104861b1a10aa8d1513696e609c51c15
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/05/2018
---
# <a name="query-for-all-packages-published-to-nugetorg"></a>nuget.org에 게시된 모든 패키지에 대한 쿼리

레거시 OData V2 API의 일반적인 쿼리 패턴 중 하나는 패키지를 게시할 때 nuget.org에 게시된 모든 패키지를 지정한 정렬 순서대로 열거한 것입니다. nuget.org에 대해 이러한 종류의 쿼리가 필요한 시나리오는 다음과 같이 매우 다양합니다.

- nuget.org 전체 복제
- 패키지의 새 버전이 출시된 경우에 대한 검색
- 패키지에 종속된 패키지 찾기

이를 수행하는 레거시 방식에서는 일반적으로 `skip` 및 `top`(페이지 크기) 매개 변수를 사용하여 대규모 결과 집합 전체에서 OData 패키지 엔터티를 타임스탬프 및 페이징 기준으로 정렬합니다. 그러나 이 방식에는 몇 가지 단점이 있습니다.

- 순서가 자주 변경되는 데이터에 대한 쿼리로 인한 패키지 누락 가능성
- 최적화되지 않은 쿼리로 인한 느린 쿼리 응답 시간(가장 효율적으로 최적화된 쿼리는 공식 NuGet 클라이언트에 대한 주요 시나리오를 지원하는 쿼리임)
- 사용되지 않고 문서화되지 않은 API 사용(나중에는 이러한 쿼리에 대한 지원이 보장되지 않음)
- 발생된 정확한 순서대로 재생할 수 없는 기록

이러한 이유로 앞에서 언급한 시나리오를 더 안정적이고 미래를 보증할 수 있는 방식으로 해결하기 위해 다음 지침을 수행할 수 있습니다.

## <a name="overview"></a>개요

이 지침의 중심에는 **카탈로그**라는 [NuGet API](../../api/overview.md)의 리소스가 있습니다. 카탈로그는 호출자가 nuget.org에서 추가, 수정 및 삭제된 패키지에 대한 전체 기록을 볼 수 있게 하는 추가 전용 API입니다. nuget.org에 게시된 패키지의 전체 또는 일부에 관심이 있는 경우 카탈로그는 시간이 지남에 따라 현재 사용 가능한 패키지의 집합을 최신 상태로 유지할 수 있는 좋은 방법입니다.

이 지침은 상위 수준 연습을 위한 것이지만, 카탈로그에 대해 매우 자세한 정보에 관심이 있는 경우 [API 참조 문서](../../api/catalog-resource.md)를 참조하세요.

다음에 나오는 단계는 원하는 프로그래밍 언어로 구현할 수 있습니다. 전체 실행 샘플을 원하는 경우 아래에서 설명하는 [C# 샘플](#c-sample-code)을 살펴보세요.

그렇지 않으면 아래 지침에 따라 신뢰할 수 있는 카탈로그 판독기를 작성합니다.

## <a name="initialize-a-cursor"></a>커서 초기화

신뢰할 수 있는 카탈로그 판독기를 작성하는 첫 번째 단계는 커서를 구현하는 것입니다. 카탈로그 커서의 디자인에 대한 자세한 내용은 [카탈로그 참조 문서](../../api/catalog-resource.md#cursor)를 참조하세요. 간단히 말해, 커서는 카탈로그에서 이벤트를 처리한 시점입니다. 카탈로그의 이벤트는 패키지 게시 및 기타 패키지 변경을 나타냅니다. 시작된 이후 NuGet에 게시된 모든 패키지에 대해 관심이 있으면 커서를 "최소값" 타임스탬프(예: .NET의 `DateTime.MinValue`)로 초기화합니다. 지금 시작하여 게시된 패키지에 대해서만 관심이 있으면 현재 타임스탬프를 초기 커서 값으로 사용합니다.

이 지침에서는 커서를 한 시간 전의 타임스탬프로 초기화합니다. 지금은 단지 해당 타임스탬프를 메모리에 저장하기만 합니다.

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>카탈로그 인덱스 URL 확인

NuGet API의 모든 리소스(엔드포인트)에 대한 위치는 [서비스 인덱스](../../api/service-index.md)를 사용하여 검색해야 합니다. 이 지침은 nuget.org에 초점을 맞추고 있으므로 nuget.org의 서비스 인덱스를 사용합니다.

```
GET https://api.nuget.org/v3/index.json
```

서비스 문서는 nuget.org의 모든 리소스가 포함된 JSON 문서입니다. `@type` 속성 값이 `Catalog/3.0.0`인 리소스를 찾습니다. 연결된 `@id` 속성 값은 카탈로그 인덱스 자체에 대한 URL입니다.

## <a name="find-new-catalog-leaves"></a>새 카탈로그 리프 찾기

이전 단계에서 찾은 `@id` 속성 값을 사용하여 카탈로그 인덱스를 다운로드합니다.

```
GET https://api.nuget.org/v3/catalog0/index.json
```

[카탈로그 인덱스](../../api/catalog-resource.md#catalog-index)를 역직렬화합니다. 현재 커서 값보다 작거나 같은 `commitTimeStamp`을 사용하여 [카탈로그 페이지 개체](../../api/catalog-resource.md#catalog-page-object-in-the-index)를 모두 필터링합니다.

나머지 카탈로그 페이지마다 `@id` 속성을 사용하여 전체 문서를 다운로드합니다.

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

[카탈로그 페이지](../../api/catalog-resource.md#catalog-page)를 역직렬화합니다. 현재 커서 값보다 작거나 같은 `commitTimeStamp`로 모든 [카탈로그 리프 개체](../../api/catalog-resource.md#catalog-item-object-in-a-page)를 필터링합니다.

필터링되지 않은 카탈로그 페이지를 모두 다운로드하면 커서 타임스탬프와 현재 시간 사이에 게시, 나열되지 않음, 나열 또는 삭제된 패키지를 나타내는 카탈로그 리프 개체 집합을 갖게 됩니다.

## <a name="process-catalog-leaves"></a>프로세스 카탈로그 리프

이 시점에서 카탈로그 항목에 대해 원하는 모든 사용자 지정 처리를 수행할 수 있습니다. 패키지의 ID와 버전이 모두 필요한 경우 페이지에 있는 카탈로그 항목 개체에서 `nuget:id` 및 `nuget:version` 속성을 검사할 수 있습니다. `@type` 속성을 살펴보고 카탈로그 항목이 기존 패키지 또는 삭제된 패키지와 관련이 있는지 확인합니다.

패키지에 대한 메타데이터(예: 설명, 종속성, .nupkg 크기 등)에 관심이 있으면 `@id` 속성을 사용하여 [카탈로그 리프 문서](../../api/catalog-resource.md#catalog-leaf)를 페치할 수 있습니다.

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

이 문서에는 [패키지 메타데이터 리소스](../../api/registration-base-url-resource.md) 등에 포함된 모든 메타데이터가 포함되어 있습니다.

이 단계에서는 사용자 지정 논리를 구현합니다. 이 지침의 다른 단계에서는 카탈로그 리프를 사용하여 수행하는 작업과 관계없이 거의 동일한 방식으로 구현합니다.

### <a name="downloading-the-nupkg"></a>.nupkg 다운로드

카탈로그에 있는 패키지에 대한 .nupkg를 다운로드하려면 [패키지 콘텐츠 리소스](../../api/package-base-address-resource.md)를 사용할 수 있습니다. 그러나 카탈로그에서 패키지를 찾은 후 패키지 콘텐츠 리소스에서 패키지를 사용할 수 있을 때까지 약간의 지연이 있습니다. 따라서 카탈로그에 있는 패키지에 대한 .nupkg를 다운로드하려고 할 때 `404 Not Found`가 발생하면 잠시 후에 다시 시도하면 됩니다. [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455) GitHub 문제에서 이 지연에 대한 수정을 추적하고 있습니다.

## <a name="move-the-cursor-forward"></a>커서를 앞으로 이동

카탈로그 항목을 성공적으로 처리했으면 저장할 새 커서 값을 결정해야 합니다. 이렇게 하려면 처리한 모든 카탈로그 항목 중 최대(최신 시간순) `commitTimeStamp`을 찾습니다. 이 항목이 새 커서 값이 됩니다. 데이터베이스, 파일 시스템 또는 Blob 저장소와 같은 일부 영구 저장소에 저장합니다. 더 많은 카탈로그 항목을 가져오려면 이 영구 저장소에서 커서 값을 초기화하여 [첫 번째 단계](#initialize-a-cursor)부터 시작하기만 하면 됩니다.

응용 프로그램에서 예외 또는 오류를 throw하는 경우 커서를 앞으로 이동하지 않습니다. 커서를 앞으로 이동하는 것은 커서 이전의 카탈로그 항목을 다시 처리할 필요가 없다는 의미입니다.

어떤 이유로 카탈로그 리프를 처리하는 방법에 버그가 있는 경우 단순히 커서를 해당 시점에서 뒤로 이동하여 코드에서 이전 카탈로그 항목을 다시 처리할 수 있습니다.

## <a name="c-sample-code"></a>C# 샘플 코드

카탈로그는 HTTP를 통해 사용할 수 있는 JSON 문서의 집합이므로, HTTP 클라이언트 및 JSON 역직렬 변환기가 있는 프로그래밍 언어를 사용하여 상호 작용할 수 있습니다.

C# 샘플은 [NuGet/샘플 리포지토리](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample)에서 사용할 수 있습니다.

```
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>카탈로그 SDK

카탈로그를 사용하는 가장 쉬운 방법은 [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog) 시험판 .NET 카탈로그 SDK 패키지를 사용하는 것입니다.
이 패키지는`https://dotnet.myget.org/F/nuget-build/api/v3/index.json` NuGet 패키지 원본 URL을 사용하는 `nuget-build` MyGet 피드에서 사용할 수 있습니다.

이 패키지는 `netstandard1.3` 이상과 호환되는 프로젝트(예: .NET Framework 4.6)에 설치할 수 있습니다.

이 패키지를 사용하는 샘플은 GitHub의 [NuGet.Protocol.Catalog.Sample 프로젝트](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample)에서 사용할 수 있습니다.

#### <a name="sample-output"></a>샘플 출력

```
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a>최소 샘플

카탈로그와의 상호 작용을 더 자세히 보여 주는 종속성이 적은 예제는 [CatalogReaderExample 샘플 프로젝트](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample)를 참조하세요.
프로젝트는 `netcoreapp2.0`을 대상으로 하며, [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0)(서비스 인덱스 확인용) 및 [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1)(JSON 역직렬화용)에 따라 다릅니다.

코드의 주요 논리는 [Program.cs 파일](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs)에 표시됩니다.

#### <a name="sample-output"></a>샘플 출력

```
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
