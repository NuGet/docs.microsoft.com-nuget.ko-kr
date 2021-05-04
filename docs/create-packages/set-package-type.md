---
title: NuGet 패키지 유형 선택
description: 패키지 유형을 설명하여 패키지의 용도를 나타냅니다.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: fa369e8327330e13f5adda39a75008e42ac99896
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067282"
---
# <a name="set-a-nuget-package-type"></a>NuGet 패키지 유형 선택

용도를 나타내기 위해 패키지를 하나 이상의 패키지 유형으로 표시할 수 있습니다.

## <a name="known-package-types"></a>알려진 패키지 형식

- `Dependency` 유형 패키지는 라이브러리 또는 애플리케이션에 빌드 시간 자산 또는 런타임 자산을 추가하며, 모든 프로젝트 형식에 설치할 수 있습니다(호환된다고 가정할 경우).

- `DotnetTool` 유형 패키지는 [dotnet CLI](/dotnet/articles/core/tools/index)로 설치할 수 있는 .NET 도구입니다.

- `Template` 유형 패키지에서는 앱, 서비스, 도구 또는 클래스 라이브러리와 같은 파일 또는 프로젝트를 만드는 데 사용할 수 있는 [사용자 지정 템플릿](/dotnet/core/tools/custom-templates)을 제공합니다.

이전 버전의 NuGet으로 만든 모든 패키지를 포함하여 유형으로 표시되지 않은 패키지의 기본값은 `Dependency` 유형입니다.

> [!NOTE]
> NuGet 3.5에 패키지 형식에 대한 지원이 추가되었습니다.
> 사용자 지정 패키지 유형이 필요하지 않은 경우 패키지 유형을 명시적으로 설정하지 않는 것이 가장 좋습니다.
> 형식이 지정되지 않은 경우 NuGet은 기본적으로 `Dependency` 형식이 됩니다.

## <a name="custom-package-types"></a>사용자 지정 패키지 유형

패키지의 사용이 [알려진 패키지 형식](#known-package-types)에 맞지 않는 경우 하나 이상의 사용자 지정 패키지 형식으로 패키지를 표시할 수 있습니다.

예를 들어 `Contoso` 앱의 고객이 확장 프로그램을 설치할 수 있다고 가정합니다. 앱은 확장 프로그램 작성자가 사용자 지정 패키지 형식 `ContosoExtension`을 사용하여 필요한 규칙을 따르는 적절한 확장 프로그램으로 패키지를 식별하도록 요구할 수 있습니다.

> [!WARNING]
> 사용자 지정 패키지 형식의 패키지는 Visual Studio 또는 nuget.exe에서 설치할 수 없습니다. 자세한 내용은 [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468)을 참조하세요.

# <a name="using-dotnet-cli"></a>[dotnet CLI 사용](#tab/dotnet)

패키지 형식은 프로젝트 파일(`.csproj`)에서 설정할 수 있습니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

다양한 용도를 가진 패키지는 `;` 구분 기호를 사용하여 여러 패키지 형식으로 표시할 수 있습니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

패키지 형식은 패키지 형식과 [`Version`](/dotnet/api/system.version) 문자열 사이의 `,` 구분 기호를 사용하여 버전을 지정할 수 있습니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[nuget.exe 사용](#tab/nugetexe)

패키지 유형이 `<metadata>` 요소 아래의 `packageTypes\packageType` 노드 내에 있는 `.nuspec` 파일에 설정됩니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="ContosoExtension" />
        </packageTypes>
    </metadata>
</package>
```

다양한 용도를 가진 패키지는 여러 패키지 형식으로 표시될 수 있습니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

패키지 형식은 [`Version`](/dotnet/api/system.version) 문자열을 사용하여 버전을 지정할 수 있습니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" version="1.0.0.0" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

---

패키지 형식 문자열의 유형은 패키지 ID와 동일합니다. 즉 패키지 형식은 최소 1개의 문자와 최대 100개의 문자를 가지고 있는 정규식 `^\w+([_.-]\w+)*$`과 일치하는 대/소문자를 구분하지 않는 문자열입니다.

제공되는 경우 패키지 형식 버전은 [`Version`](/dotnet/api/system.version) 문자열입니다. 패키지 유형 버전은 선택 사항이며 기본값은 `0.0`입니다.
