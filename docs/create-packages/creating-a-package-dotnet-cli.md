---
title: dotnet CLI를 사용하여 NuGet 패키지 만들기
description: 파일 및 버전 관리와 같은 주요 결정 사항을 포함하여 NuGet 패키지를 디자인하고 만드는 과정을 자세히 안내합니다.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: da5dbc8b1659cef66e8439b9a3c3bb2c9205cbe6
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68462460"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="084ed-103">dotnet CLI를 사용하여 NuGet 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="084ed-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="084ed-104">패키지의 기능 또는 포함된 코드와 관계없이 CLI 도구인 `nuget.exe` 또는 `dotnet.exe`를 사용하여 해당 기능을 임의 수의 다른 개발자와 공유하고 사용할 수 있는 구성 요소로 패키지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="084ed-105">이 문서에서는 dotnet CLI를 사용하여 패키지를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="084ed-106">`dotnet` CLI를 설치하려면 [NuGet 클라이언트 도구 설치](../install-nuget-client-tools.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="084ed-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="084ed-107">Visual Studio 2017부터 dotnet CLI가 .NET Core 워크로드에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="084ed-108">[SDK 스타일 형식](../resources/check-project-format.md)을 사용하는 .NET Core 및 .NET Standard 프로젝트와 또 다른 SDK 스타일 프로젝트의 경우, NuGet은 프로젝트 파일의 정보를 직접 사용하여 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="084ed-109">단계별 자습서를 보려면 [dotnet CLI를 사용하여 .NET Standard 패키지 만들기](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md), [Visual Studion를 사용하여 .NET Standard 패키지 만들기](../quickstart/create-and-publish-a-package-using-visual-studio.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="084ed-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md), [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="084ed-110">`msbuild -t:pack`은 기능적으로 `dotnet pack`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="084ed-111">MSBuild로 빌드하려는 경우 사용되는 개념은 이 문서에 설명된 것과 동일하지만 명령줄 명령은 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-111">To build with MSBuild, the concepts are the same as described in this article, but the command line commands are slightly different.</span></span> <span data-ttu-id="084ed-112">마찬가지로 비 SDK 스타일 프로젝트 및 `<PackageReference>`에서는 `msbuild /t:pack`을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-112">Similarly, with a non-SDK-style project and `<PackageReference>`, you can use `msbuild /t:pack`.</span></span> <span data-ttu-id="084ed-113">이러한 시나리오에서는 종속성에 Nuget.exe 패키지를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-113">In these scenarios, you need to add the NuGet.Build.Tasks.Pack package to their dependencies.</span></span> <span data-ttu-id="084ed-114">[MSBuild 대상으로서의 NuGet pack 및 restore](../reference/msbuild-targets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="084ed-114">See [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="084ed-115">이 항목은 일반적으로 .NET Core 및 .NET Standard 프로젝트에 해당하는 [SDK 스타일](../resources/check-project-format.md) 프로젝트에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-115">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="084ed-116">속성 설정</span><span class="sxs-lookup"><span data-stu-id="084ed-116">Set properties</span></span>

<span data-ttu-id="084ed-117">패키지를 만들려면 다음 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-117">The following properties are required to create a package.</span></span>

- <span data-ttu-id="084ed-118">`PackageId`: 패키지를 호스트하는 갤러리에서 고유해야 하는 패키지 식별자.</span><span class="sxs-lookup"><span data-stu-id="084ed-118">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="084ed-119">지정하지 않으면 기본값 `AssemblyName`입니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-119">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="084ed-120">`Version`: *Major.Minor.Patch[-Suffix]* 형식의 특정 버전 번호(여기서 *-Suffix*는 [시험판 버전](prerelease-packages.md)을 식별함).</span><span class="sxs-lookup"><span data-stu-id="084ed-120">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="084ed-121">지정하지 않으면 기본값은 1.0.0입니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-121">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="084ed-122">호스트에 표시되어야 하는 패키지 제목(예: nuget.org)</span><span class="sxs-lookup"><span data-stu-id="084ed-122">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="084ed-123">`Authors`: 작성자 및 소유자 정보.</span><span class="sxs-lookup"><span data-stu-id="084ed-123">`Authors`, author and owner information.</span></span> <span data-ttu-id="084ed-124">지정하지 않으면 기본값 `AssemblyName`입니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-124">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="084ed-125">`Company`: 회사 이름.</span><span class="sxs-lookup"><span data-stu-id="084ed-125">`Company`, your company name.</span></span> <span data-ttu-id="084ed-126">지정하지 않으면 기본값 `AssemblyName`입니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-126">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="084ed-127">Visual Studio의 프로젝트 속성에서 이러한 값을 설정할 수 있습니다(솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택한 다음, **패키지** 탭 선택).</span><span class="sxs-lookup"><span data-stu-id="084ed-127">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="084ed-128">프로젝트 파일(`.csproj`)에서 직접 이러한 속성을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-128">You can also set these properties directly in the project files (`.csproj`).</span></span>

    ```xml
    <PropertyGroup>
      ...
      <PackageId>AppLogger</PackageId>
      <Version>1.0.0</Version>
      <Authors>your_name</Authors>
      <Company>your_company</Company>
    </PropertyGroup>
    ```

> [!Important]
> <span data-ttu-id="084ed-129">nuget.org 또는 사용 중인 패키지 원본에서 고유한 식별자를 패키지에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-129">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="084ed-130">[MSBuild pack 대상](../reference/msbuild-targets.md#pack-target), [종속성 자산 제어](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) 및 [NuGet 메타데이터 속성](/dotnet/core/tools/csproj#nuget-metadata-properties)에 설명된 대로 `Title`, `PackageDescription` 및 `PackageTags`와 같은 선택적 속성을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-130">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="084ed-131">공용으로 빌드된 패키지의 경우 **PackageTags** 속성에 특히 주의하세요. 이러한 태그는 다른 사람들이 패키지를 찾고 그 기능을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-131">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="084ed-132">종속성 선언 및 버전 번호 지정에 대한 자세한 내용은 [패키지 버전 관리](../reference/package-versioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="084ed-132">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="084ed-133">`<IncludeAssets>` 및 `<ExcludeAssets>` 특성을 사용하여 패키지에 종속성의 자산을 직접 공개할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-133">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="084ed-134">자세한 내용은 [종속성 자산 제어](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="084ed-134">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="084ed-135">고유한 패키지 식별자 선택 및 버전 번호 설정</span><span class="sxs-lookup"><span data-stu-id="084ed-135">Choose a unique package identifier and set the version number</span></span>

<span data-ttu-id="084ed-136">패키지 식별자와 버전 번호는 패키지에 포함된 정확한 코드를 고유하게 식별하므로 프로젝트에서 가장 중요한 두 가지 값입니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-136">The package identifier and the version number are the two most important values in the project because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="084ed-137">**패키지 식별자에 대한 모범 사례:**</span><span class="sxs-lookup"><span data-stu-id="084ed-137">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="084ed-138">**고유성**: 식별자는 nuget.org 또는 패키지를 호스팅하는 모든 갤러리에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-138">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="084ed-139">식별자를 결정하기 전에 해당 갤러리를 검색하여 해당 이름이 이미 사용 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-139">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="084ed-140">충돌을 방지하기 위한 좋은 패턴은 회사 이름을 식별자의 첫 번째 부분(예: `Contoso.`)으로 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-140">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="084ed-141">**네임스페이스 형식의 이름**: 하이픈 대신 점 표기법을 사용하여 .NET의 네임스페이스와 비슷한 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-141">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="084ed-142">예를 들어 `Contoso-Utility-UsefulStuff` 또는 `Contoso_Utility_UsefulStuff` 대신 `Contoso.Utility.UsefulStuff`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-142">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="084ed-143">패키지 식별자가 코드에 사용된 네임스페이스와 일치할 때 소비자가 이 형식의 이름이 유용하다는 것을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-143">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="084ed-144">**샘플 패키지**: 다른 패키지를 사용하는 방법을 보여 주는 샘플 코드 패키지를 생성하는 경우 `Contoso.Utility.UsefulStuff.Sample`(와)과 같이 `.Sample`을(를) 접미사로 식별자에 붙입니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-144">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="084ed-145">(물론 샘플 패키지에는 다른 패키지에 대한 종속성이 있습니다.) 샘플 패키지를 만들 때는 `contentFiles`의 `<IncludeAssets>`값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-145">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the `contentFiles` value in `<IncludeAssets>`.</span></span> <span data-ttu-id="084ed-146">`content` 폴더에서 `\Samples\Contoso.Utility.UsefulStuff.Sample`과 같이 `\Samples\<identifier>`라는 폴더에 샘플 코드를 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-146">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="084ed-147">**패키지 버전에 대한 모범 사례:**</span><span class="sxs-lookup"><span data-stu-id="084ed-147">**Best practices for the package version:**</span></span>

- <span data-ttu-id="084ed-148">일반적으로 반드시 필요한 것은 아니지만 프로젝트(또는 어셈블리)의 버전과 일치하도록 패키지의 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-148">In general, set the version of the package to match the project (or assembly), though this is not strictly required.</span></span> <span data-ttu-id="084ed-149">이는 패키지를 단일 어셈블리로 제한할 때는 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-149">This is a simple matter when you limit a package to a single assembly.</span></span> <span data-ttu-id="084ed-150">전반적으로 NuGet 자체는 종속성을 확인할 때 어셈블리 버전이 아니라 패키지 버전을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-150">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="084ed-151">비표준 버전 구성표를 사용하는 경우 [패키지 버전 관리](../reference/package-versioning.md)에서 설명한 대로 NuGet 버전 관리 규칙을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-151">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="084ed-152">NuGet은 대부분 [semver 2와 호환](../reference/package-versioning.md#semantic-versioning-200)됩니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-152">NuGet is mostly [semver 2 compliant](../reference/package-versioning.md#semantic-versioning-200).</span></span>

> <span data-ttu-id="084ed-153">종속성 확인에 대한 자세한 내용은 [PackageReference를 사용하여 종속성 확인](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="084ed-153">For information on dependency resolution, see [Dependency resolution with PackageReference](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).</span></span> <span data-ttu-id="084ed-154">버전 관리를 보다 잘 이해하는 데 도움이 될 수 있는 이전 정보는 다음의 블로그 게시물 시리지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="084ed-154">For older information that may also be helpful to better understand versioning, see this series of blog posts.</span></span>
>
> - [<span data-ttu-id="084ed-155">1부: DLL 지옥에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="084ed-155">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="084ed-156">2부: 핵심 알고리즘</span><span class="sxs-lookup"><span data-stu-id="084ed-156">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="084ed-157">3부: 바인딩 리디렉션을 통한 통합</span><span class="sxs-lookup"><span data-stu-id="084ed-157">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="run-the-pack-command"></a><span data-ttu-id="084ed-158">pack 명령 실행</span><span class="sxs-lookup"><span data-stu-id="084ed-158">Run the pack command</span></span>

<span data-ttu-id="084ed-159">프로젝트에서 NuGet 패키지(`.nupkg` 파일)를 빌드하려면 `dotnet pack` 명령을 실행합니다. 이 명령은 프로젝트도 자동으로 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-159">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="084ed-160">출력에는 `.nupkg` 파일의 경로가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-160">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="084ed-161">빌드 시 패키지를 자동으로 생성</span><span class="sxs-lookup"><span data-stu-id="084ed-161">Automatically generate package on build</span></span>

<span data-ttu-id="084ed-162">`dotnet build`를 실행할 때 `dotnet pack`을 자동으로 실행하려면 프로젝트 파일의 `<PropertyGroup>` 내에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-162">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="084ed-163">솔루션에서 `dotnet pack`을 실행하는 경우 패키지에 포함할 수 있는 모든 프로젝트가 솔루션에 압축됩니다([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) 속성은 `true`로 설정됨).</span><span class="sxs-lookup"><span data-stu-id="084ed-163">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="084ed-164">패키지를 자동으로 생성할 때 압축하는 데 소요되는 시간 때문에 프로젝트의 빌드 시간이 늘어납니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-164">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="084ed-165">패키지 설치 테스트</span><span class="sxs-lookup"><span data-stu-id="084ed-165">Test package installation</span></span>

<span data-ttu-id="084ed-166">일반적으로 패키지를 게시하기 전에 프로젝트에 패키지를 설치하는 프로세스를 테스트하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-166">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="084ed-167">테스트를 통해 모든 파일이 프로젝트의 올바른 위치에 있는지 반드시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-167">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="084ed-168">일반적인 [패키지 설치 단계](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)를 사용하여 Visual Studio 또는 명령줄에서 수동으로 설치를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-168">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="084ed-169">패키지는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-169">Packages are immutable.</span></span> <span data-ttu-id="084ed-170">문제를 수정하고 패키지의 내용을 변경한 후 다시 압축하는 경우 다시 테스트해도 [전역 패키지](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) 폴더를 지울 때까지 이전 버전의 패키지가 계속 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-170">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="084ed-171">이러한 특성은 모든 빌드에서 고유한 시험판 레이블을 사용하지는 않는 패키지를 테스트할 때는 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-171">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="084ed-172">다음 단계</span><span class="sxs-lookup"><span data-stu-id="084ed-172">Next Steps</span></span>

<span data-ttu-id="084ed-173">패키지(`.nupkg` 파일)를 만들었으면 [패키지 게시](../nuget-org/publish-a-package.md)에서 설명한 대로 원하는 갤러리에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-173">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="084ed-174">다음 항목에서 설명한 대로 패키지의 기능을 확장하거나 그렇지 않고 다른 시나리오를 지원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-174">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="084ed-175">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="084ed-175">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="084ed-176">여러 대상 프레임워크 지원</span><span class="sxs-lookup"><span data-stu-id="084ed-176">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="084ed-177">원본 및 구성 파일 변환</span><span class="sxs-lookup"><span data-stu-id="084ed-177">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="084ed-178">지역화</span><span class="sxs-lookup"><span data-stu-id="084ed-178">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="084ed-179">시험판 버전</span><span class="sxs-lookup"><span data-stu-id="084ed-179">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="084ed-180">패키지 형식 설정</span><span class="sxs-lookup"><span data-stu-id="084ed-180">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="084ed-181">COM interop 어셈블리가 포함된 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="084ed-181">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="084ed-182">마지막으로 주의해야 할 추가 패키지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="084ed-182">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="084ed-183">네이티브 패키지</span><span class="sxs-lookup"><span data-stu-id="084ed-183">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="084ed-184">기호 패키지</span><span class="sxs-lookup"><span data-stu-id="084ed-184">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
