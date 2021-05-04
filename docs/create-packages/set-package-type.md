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
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="b1a66-103">NuGet 패키지 유형 선택</span><span class="sxs-lookup"><span data-stu-id="b1a66-103">Set a NuGet package type</span></span>

<span data-ttu-id="b1a66-104">용도를 나타내기 위해 패키지를 하나 이상의 패키지 유형으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-104">Packages can be marked with one more more *package types* to indicate its intended use.</span></span>

## <a name="known-package-types"></a><span data-ttu-id="b1a66-105">알려진 패키지 형식</span><span class="sxs-lookup"><span data-stu-id="b1a66-105">Known package types</span></span>

- <span data-ttu-id="b1a66-106">`Dependency` 유형 패키지는 라이브러리 또는 애플리케이션에 빌드 시간 자산 또는 런타임 자산을 추가하며, 모든 프로젝트 형식에 설치할 수 있습니다(호환된다고 가정할 경우).</span><span class="sxs-lookup"><span data-stu-id="b1a66-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="b1a66-107">`DotnetTool` 유형 패키지는 [dotnet CLI](/dotnet/articles/core/tools/index)로 설치할 수 있는 .NET 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-107">`DotnetTool` type packages are .NET tools that can be installed by the [dotnet CLI](/dotnet/articles/core/tools/index).</span></span>

- <span data-ttu-id="b1a66-108">`Template` 유형 패키지에서는 앱, 서비스, 도구 또는 클래스 라이브러리와 같은 파일 또는 프로젝트를 만드는 데 사용할 수 있는 [사용자 지정 템플릿](/dotnet/core/tools/custom-templates)을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-108">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

<span data-ttu-id="b1a66-109">이전 버전의 NuGet으로 만든 모든 패키지를 포함하여 유형으로 표시되지 않은 패키지의 기본값은 `Dependency` 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-109">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

> [!NOTE]
> <span data-ttu-id="b1a66-110">NuGet 3.5에 패키지 형식에 대한 지원이 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-110">Support for package types was added in NuGet 3.5.</span></span>
> <span data-ttu-id="b1a66-111">사용자 지정 패키지 유형이 필요하지 않은 경우 패키지 유형을 명시적으로 설정하지 않는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-111">If you don't need a custom package type, it's best to *not* explicitly set the package type.</span></span>
> <span data-ttu-id="b1a66-112">형식이 지정되지 않은 경우 NuGet은 기본적으로 `Dependency` 형식이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-112">NuGet defaults to the `Dependency` type when no type is specified.</span></span>

## <a name="custom-package-types"></a><span data-ttu-id="b1a66-113">사용자 지정 패키지 유형</span><span class="sxs-lookup"><span data-stu-id="b1a66-113">Custom package types</span></span>

<span data-ttu-id="b1a66-114">패키지의 사용이 [알려진 패키지 형식](#known-package-types)에 맞지 않는 경우 하나 이상의 사용자 지정 패키지 형식으로 패키지를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-114">You can mark your package with one or more custom package types if its use does not fit the [known package types](#known-package-types).</span></span>

<span data-ttu-id="b1a66-115">예를 들어 `Contoso` 앱의 고객이 확장 프로그램을 설치할 수 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-115">For example, imagine that customers of the `Contoso` app can install extensions.</span></span> <span data-ttu-id="b1a66-116">앱은 확장 프로그램 작성자가 사용자 지정 패키지 형식 `ContosoExtension`을 사용하여 필요한 규칙을 따르는 적절한 확장 프로그램으로 패키지를 식별하도록 요구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-116">The app could require extension authors to use the custom package type `ContosoExtension` to identify their packages as proper extensions that follow the required conventions.</span></span>

> [!WARNING]
> <span data-ttu-id="b1a66-117">사용자 지정 패키지 형식의 패키지는 Visual Studio 또는 nuget.exe에서 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-117">A package with a custom package type cannot be installed by Visual Studio or nuget.exe.</span></span> <span data-ttu-id="b1a66-118">자세한 내용은 [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b1a66-118">See [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468) for more information.</span></span>

# <a name="using-dotnet-cli"></a>[<span data-ttu-id="b1a66-119">dotnet CLI 사용</span><span class="sxs-lookup"><span data-stu-id="b1a66-119">Using dotnet CLI</span></span>](#tab/dotnet)

<span data-ttu-id="b1a66-120">패키지 형식은 프로젝트 파일(`.csproj`)에서 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-120">Package types can be set in the project file (`.csproj`):</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="b1a66-121">다양한 용도를 가진 패키지는 `;` 구분 기호를 사용하여 여러 패키지 형식으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-121">Packages with multiple intended uses can be marked with multiple package types using the `;` delimiter:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="b1a66-122">패키지 형식은 패키지 형식과 [`Version`](/dotnet/api/system.version) 문자열 사이의 `,` 구분 기호를 사용하여 버전을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-122">Package types can be versioned using a `,` delimiter between the package type and its [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[<span data-ttu-id="b1a66-123">nuget.exe 사용</span><span class="sxs-lookup"><span data-stu-id="b1a66-123">Using nuget.exe</span></span>](#tab/nugetexe)

<span data-ttu-id="b1a66-124">패키지 유형이 `<metadata>` 요소 아래의 `packageTypes\packageType` 노드 내에 있는 `.nuspec` 파일에 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-124">Package types are set in the `.nuspec` file within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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

<span data-ttu-id="b1a66-125">다양한 용도를 가진 패키지는 여러 패키지 형식으로 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-125">Packages with multiple intended uses may be marked with multiple package types:</span></span>

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

<span data-ttu-id="b1a66-126">패키지 형식은 [`Version`](/dotnet/api/system.version) 문자열을 사용하여 버전을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-126">Package types can be versioned using a [`Version`](/dotnet/api/system.version) string:</span></span>

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

<span data-ttu-id="b1a66-127">패키지 형식 문자열의 유형은 패키지 ID와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-127">The format of a package type string is exactly like a package ID.</span></span> <span data-ttu-id="b1a66-128">즉 패키지 형식은 최소 1개의 문자와 최대 100개의 문자를 가지고 있는 정규식 `^\w+([_.-]\w+)*$`과 일치하는 대/소문자를 구분하지 않는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-128">That is, a package type is a case-insensitive string matching the regular expression `^\w+([_.-]\w+)*$` having at least one character and at most 100 characters.</span></span>

<span data-ttu-id="b1a66-129">제공되는 경우 패키지 형식 버전은 [`Version`](/dotnet/api/system.version) 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-129">If provided, the package type version is a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="b1a66-130">패키지 유형 버전은 선택 사항이며 기본값은 `0.0`입니다.</span><span class="sxs-lookup"><span data-stu-id="b1a66-130">The package type version is optional and defaults to `0.0`.</span></span>
