---
title: COM interop 어셈블리가 포함된 패키지 만들기
description: COM interop 어셈블리가 포함된 패키지를 만드는 방법을 설명합니다.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b12672e81a974e113ffbda80560c9d3eede9c69d
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859124"
---
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>COM interop 어셈블리가 포함된 패키지 만들기

COM interop 어셈블리가 포함된 패키지에는 적절한 [targets 파일](creating-a-package.md#include-msbuild-props-and-targets-in-a-package)이 포함되어야 올바른 `EmbedInteropTypes` 메타데이터가 PackageReference 형식을 사용하여 프로젝트에 추가됩니다. 기본적으로 PackageReference를 사용하는 경우 `EmbedInteropTypes` 메타데이터는 모든 어셈블리에 대해 항상 false이므로 targets 파일에는 이 메타데이터가 명시적으로 추가됩니다. 충돌을 방지하기 위해 대상 이름은 고유해야 합니다. 이상적으로는 패키지 이름과 포함되는 어셈블리의 조합을 사용하여 아래 예제의 `{InteropAssemblyName}`을 해당 값으로 바꿉니다. (예제는 [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/main/NuGet.Samples.Interop)을 참조하세요.)

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

`packages.config` 관리 형식을 사용하는 경우 패키지에서 어셈블리에 대한 참조를 추가하면 NuGet 및 Visual Studio에서 COM interop 어셈블리를 확인하고 프로젝트 파일에서 `EmbedInteropTypes`를 true로 설정합니다. 이 경우 대상 파일이 재정의됩니다.

또한 기본적으로 [빌드 자산은 전이적으로 이동하지 않습니다](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). 여기서 설명한 대로 작성된 패키지는 프로젝트 간 참조에서 전이 종속성으로 끌어올 때 다르게 작동합니다. 패키지 소비자는 빌드를 포함하지 않도록 PrivateAssets 기본값을 수정하여 패키지를 이동할 수 있도록 합니다.

<a name="creating-the-package"></a>