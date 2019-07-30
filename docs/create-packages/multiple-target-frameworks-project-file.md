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
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a><span data-ttu-id="659f0-103">프로젝트 파일에서 여러 .NET Framework 버전 지원</span><span class="sxs-lookup"><span data-stu-id="659f0-103">Support multiple .NET Framework versions in your project file</span></span>

<span data-ttu-id="659f0-104">프로젝트를 처음 만들 때 가장 넓은 범위의 소비 프로젝트와 호환성되므로 .NET Standard 클래스 라이브러리를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="659f0-104">When you first create a project, we recommend you create a .NET Standard class library, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="659f0-105">.NET Standard를 사용하여 기본적으로 .NET 라이브러리에 [플랫폼 간 지원](/dotnet/standard/library-guidance/cross-platform-targeting)을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="659f0-105">By using .NET Standard, you add [cross-platform support](/dotnet/standard/library-guidance/cross-platform-targeting) to a .NET library by default.</span></span> <span data-ttu-id="659f0-106">그러나 일부 시나리오에서는 특정 프레임워크를 대상으로 하는 코드도 포함해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="659f0-106">However, in some scenarios, you may also need to include code that targets a particular framework.</span></span> <span data-ttu-id="659f0-107">이 문서에서는 [SDK 스타일 ](../resources/check-project-format.md) 프로젝트에 대해 이 작업을 수행하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="659f0-107">This article shows you how to do that for [SDK-style](../resources/check-project-format.md) projects.</span></span>

<span data-ttu-id="659f0-108">SDK 스타일 프로젝트의 경우 프로젝트 파일에서 여러 대상 프레임워크([TFM](/dotnet/standard/frameworks))에 대한 지원을 구성한 후 `dotnet pack` 또는 `msbuild /t:pack`을 사용하여 패키지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="659f0-108">For SDK-style projects, you can configure support for multiple targets frameworks ([TFM](/dotnet/standard/frameworks)) in your project file, then use `dotnet pack` or `msbuild /t:pack` to create the package.</span></span>

> [!NOTE]
> <span data-ttu-id="659f0-109">nuget.exe CLI는 SDK 스타일 프로젝트 압축을 지원하지 않으므로 `dotnet pack` 또는 `msbuild /t:pack`만 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="659f0-109">nuget.exe CLI does not support packing SDK-style projects, so you should only use `dotnet pack` or `msbuild /t:pack`.</span></span> <span data-ttu-id="659f0-110">대신 일반적으로 `.nuspec` 파일에 있는 [모든 속성을 프로젝트 파일에 포함](../reference/msbuild-targets.md#pack-target)하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="659f0-110">We recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="659f0-111">비 SDK 스타일 프로젝트에서 여러 .NET Framework 버전을 대상으로 하려면 [여러 .NET Framework 버전 지원](supporting-multiple-target-frameworks.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="659f0-111">To target multiple .NET Framework versions in a non-SDK-style project, see [Supporting multiple .NET Framework versions](supporting-multiple-target-frameworks.md).</span></span>

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a><span data-ttu-id="659f0-112">여러 .NET Framework 버전을 지원하는 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="659f0-112">Create a project that supports multiple .NET Framework versions</span></span>

1. <span data-ttu-id="659f0-113">Visual Studio에서 새 .NET Standard 클래스 라이브러리를 만들거나 `dotnet new classlib`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="659f0-113">Create a new .NET Standard class library either in Visual Studio or use `dotnet new classlib`.</span></span>

   <span data-ttu-id="659f0-114">최상의 호환성을 위해 .NET Standard 클래스 라이브러리를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="659f0-114">We recommend that you create a .NET Standard class library for best compatibility.</span></span>

2. <span data-ttu-id="659f0-115">대상 프레임워크를 지원하도록 *.csproj* 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="659f0-115">Edit the *.csproj* file to support the target frameworks.</span></span>

   <span data-ttu-id="659f0-116">예를 들어, `<TargetFramework>netstandard2.0</TargetFramework>`를 `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="659f0-116">For example, change `<TargetFramework>netstandard2.0</TargetFramework>` to `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`.</span></span>

   <span data-ttu-id="659f0-117">XML 요소를 단수형에서 복수형으로 변경했는지 확인합니다(여는 태그 및 닫는 태그 둘 다에 "s" 추가).</span><span class="sxs-lookup"><span data-stu-id="659f0-117">Make sure that you change the XML element changed from singular to plural (add the "s" to both the open and close tags).</span></span>

3. <span data-ttu-id="659f0-118">하나의 TFM에만 작동하는 코드가 있는 경우 `#if NET45` 또는 `#if NETSTANDARD20`을 사용하여 TFM 종속 코드를 구분할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="659f0-118">If you have any code that only works in one TFM, you can use `#if NET45` or `#if NETSTANDARD20` to separate TFM-dependent code.</span></span> <span data-ttu-id="659f0-119">(자세한 내용은 [멀티 타기팅 방법](/dotnet/core/tutorials/libraries#how-to-multitarget)을 참조하세요.) 예를 들어 다음 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="659f0-119">(For more information, see [How to multitarget](/dotnet/core/tutorials/libraries#how-to-multitarget).) For example, you can use the following code:</span></span>

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

4. <span data-ttu-id="659f0-120">*.csproj*에 원하는 NuGet 메타데이터를 MSBuild 속성으로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="659f0-120">Add any NuGet metadata you want to the *.csproj* as MSBuild properties.</span></span>

   <span data-ttu-id="659f0-121">사용 가능한 패키지 메타데이터 및 MSBuild 속성 이름 목록은 [pack 대상](../reference/msbuild-targets.md#pack-target)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="659f0-121">For the list of available package metadata and the MSBuild property names, see [pack target](../reference/msbuild-targets.md#pack-target).</span></span> <span data-ttu-id="659f0-122">[종속성 자산 제어](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)도 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="659f0-122">Also see [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

   <span data-ttu-id="659f0-123">Nuget 메타데이터에서 빌드 관련 속성을 분리하려는 경우 다른 `PropertyGroup`을 사용하거나 NuGet 속성을 다른 파일에 넣고 MSBuild의 `Import` 지시문을 사용하여 포함시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="659f0-123">If you want to separate build-related properties from NuGet metadata, you can use a different `PropertyGroup`, or put the NuGet properties in another file and use MSBuild's `Import` directive to include it.</span></span> <span data-ttu-id="659f0-124">MSBuild 15.0부터 `Directory.Build.Props` 및 `Directory.Build.Targets`도 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="659f0-124">`Directory.Build.Props` and `Directory.Build.Targets` are also supported starting with MSBuild 15.0.</span></span>

5. <span data-ttu-id="659f0-125">이제 `dotnet pack`을 사용합니다. 그러면 결과 *.nupkg*는 .NET Standard 2.0 및 .NET Framework 4.5 둘 다를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="659f0-125">Now, use `dotnet pack` and the resulting *.nupkg* targets both .NET Standard 2.0 and .NET Framework 4.5.</span></span>

<span data-ttu-id="659f0-126">다음은 이전 단계 및 .NET Core SDK 2.2를 사용하여 생성한 *.csproj* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="659f0-126">Here is the *.csproj* file that is generated using the preceding steps and .NET Core SDK 2.2.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a><span data-ttu-id="659f0-127">참고 항목</span><span class="sxs-lookup"><span data-stu-id="659f0-127">See also</span></span>

<span data-ttu-id="659f0-128">[대상 프레임워크를 지정하는 방법](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
[플랫폼 간 대상 지정](/dotnet/standard/library-guidance/cross-platform-targeting)</span><span class="sxs-lookup"><span data-stu-id="659f0-128">[How to specify target frameworks](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
[Cross-platform targeting](/dotnet/standard/library-guidance/cross-platform-targeting)</span></span>
