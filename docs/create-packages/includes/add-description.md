---
ms.openlocfilehash: b615bcb78ad2eaf8524bfbf17864d4652e546ff1
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80151243"
---
<span data-ttu-id="c79a2-101">패키지의 NuGet.org 페이지에 표시되는 패키지 설명(선택 사항)은 `<description></description>` 파일에 사용된 `.csproj`에서 가져오거나 `$description`.nuspec 파일[의 ](../../reference/nuspec.md)을 통해 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c79a2-101">The package's optional description, displayed on the package's NuGet.org page, is either pulled in from the `<description></description>` used in the `.csproj` file or pulled in via the `$description` in the [.nuspec file](../../reference/nuspec.md).</span></span>

<span data-ttu-id="c79a2-102">‘설명’ 필드의 예는 .NET 패키지에 대한  _파일의 다음 XML 텍스트에 나와 있습니다._ `.csproj`</span><span class="sxs-lookup"><span data-stu-id="c79a2-102">An example of a _description_ field is shown in the following XML text of the `.csproj` file for a .NET package:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <PackageId>Azure.Storage.Blobs</PackageId>
    <Version>12.4.0</Version>
    <PackageTags>Microsoft Azure Storage Blobs;Microsoft;Azure;Blobs;Blob;Storage;StorageScalable</PackageTags>
    <Description>
      This client library enables working with the Microsoft Azure Storage Blob service for storing binary and text data.
      For this release see notes - https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/README.md and https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/CHANGELOG.md
      in addition to the breaking changes https://github.com/Azure/azure-sdk-for-net/blob/master/sdk/storage/Azure.Storage.Blobs/BreakingChanges.txt
      Microsoft Azure Storage quickstarts and tutorials - https://docs.microsoft.com/en-us/azure/storage/
      Microsoft Azure Storage REST API Reference - https://docs.microsoft.com/en-us/rest/api/storageservices/
      REST API Reference for Blob Service - https://docs.microsoft.com/en-us/rest/api/storageservices/blob-service-rest-api
    </Description>
  </PropertyGroup>
</PropertyGroup>
```
