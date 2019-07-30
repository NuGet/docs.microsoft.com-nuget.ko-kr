---
title: 프로젝트 파일에서 NuGet 패키지의 멀티 타기팅
description: 단일 NuGet 패키지 내에서 여러 .NET Framework 버전을 대상으로 하는 다양한 방법에 대한 설명입니다.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 1ff02871872cee9e8cbf8c7d7c74d804f7dc5b99
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68346118"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a>프로젝트 파일에서 여러 .NET Framework 버전 지원

프로젝트를 처음 만들 때 가장 넓은 범위의 소비 프로젝트와 호환성되므로 .NET Standard 클래스 라이브러리를 만드는 것이 좋습니다. .NET Standard를 사용하여 기본적으로 .NET 라이브러리에 [플랫폼 간 지원](/dotnet/standard/library-guidance/cross-platform-targeting)을 추가합니다. 그러나 일부 시나리오에서는 특정 프레임워크를 대상으로 하는 코드도 포함해야 할 수 있습니다. 이 문서에서는 [SDK 스타일 ](../resources/check-project-format.md) 프로젝트에 대해 이 작업을 수행하는 방법을 보여 줍니다.

SDK 스타일 프로젝트의 경우 프로젝트 파일에서 여러 대상 프레임워크([TFM](/dotnet/standard/frameworks))에 대한 지원을 구성한 후 `dotnet pack` 또는 `msbuild /t:pack`을 사용하여 패키지를 만들 수 있습니다.

> [!NOTE]
> nuget.exe CLI는 SDK 스타일 프로젝트 압축을 지원하지 않으므로 `dotnet pack` 또는 `msbuild /t:pack`만 사용해야 합니다. 대신 일반적으로 `.nuspec` 파일에 있는 [모든 속성을 프로젝트 파일에 포함](../reference/msbuild-targets.md#pack-target)하는 것이 좋습니다. 비 SDK 스타일 프로젝트에서 여러 .NET Framework 버전을 대상으로 하려면 [여러 .NET Framework 버전 지원](supporting-multiple-target-frameworks.md)을 참조하세요.

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a>여러 .NET Framework 버전을 지원하는 프로젝트 만들기

1. Visual Studio에서 새 .NET Standard 클래스 라이브러리를 만들거나 `dotnet new classlib`를 사용합니다.

   최상의 호환성을 위해 .NET Standard 클래스 라이브러리를 만드는 것이 좋습니다.

2. 대상 프레임워크를 지원하도록 *.csproj* 파일을 편집합니다.

   예를 들어, `<TargetFramework>netstandard2.0</TargetFramework>`를 `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`로 변경합니다.

   XML 요소를 단수형에서 복수형으로 변경했는지 확인합니다(여는 태그 및 닫는 태그 둘 다에 "s" 추가).

3. 하나의 TFM에만 작동하는 코드가 있는 경우 `#if NET45` 또는 `#if NETSTANDARD20`을 사용하여 TFM 종속 코드를 구분할 수 있습니다. (자세한 내용은 [멀티 타기팅 방법](/dotnet/core/tutorials/libraries#how-to-multitarget)을 참조하세요.) 예를 들어 다음 코드를 사용할 수 있습니다.

   ```csharp
   public string Platform {
      get {
   #if NET45
         return ".NET Framework"
   #elif NETSTANDARD2_0
         return ".NET Standard"
   #else
   #error This code block does not match csproj TargetFrameworks list
   #endif
      }
   }
   ```

4. *.csproj*에 원하는 NuGet 메타데이터를 MSBuild 속성으로 추가합니다.

   사용 가능한 패키지 메타데이터 및 MSBuild 속성 이름 목록은 [pack 대상](../reference/msbuild-targets.md#pack-target)을 참조하세요. [종속성 자산 제어](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)도 참조하세요.

   Nuget 메타데이터에서 빌드 관련 속성을 분리하려는 경우 다른 `PropertyGroup`을 사용하거나 NuGet 속성을 다른 파일에 넣고 MSBuild의 `Import` 지시문을 사용하여 포함시킬 수 있습니다. MSBuild 15.0부터 `Directory.Build.Props` 및 `Directory.Build.Targets`도 지원됩니다.

5. 이제 `dotnet pack`을 사용합니다. 그러면 결과 *.nupkg*는 .NET Standard 2.0 및 .NET Framework 4.5 둘 다를 대상으로 합니다.

다음은 이전 단계 및 .NET Core SDK 2.2를 사용하여 생성한 *.csproj* 파일입니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a>참고 항목

[대상 프레임워크를 지정하는 방법](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
[플랫폼 간 대상 지정](/dotnet/standard/library-guidance/cross-platform-targeting)
