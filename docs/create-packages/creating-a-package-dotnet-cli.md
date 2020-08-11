---
title: dotnet CLI를 사용하여 NuGet 패키지 만들기
description: 파일 및 버전 관리와 같은 주요 결정 사항을 포함하여 NuGet 패키지를 디자인하고 만드는 과정을 자세히 안내합니다.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 2fcba9dd6bbc7ff4e9b5b8b57250c399f59a1c5e
ms.sourcegitcommit: e02482e15c0cef63153086ed50d14f5b2a38f598
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473846"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="8e0bb-103">dotnet CLI를 사용하여 NuGet 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="8e0bb-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="8e0bb-104">패키지의 기능 또는 포함된 코드와 관계없이 CLI 도구인 `nuget.exe` 또는 `dotnet.exe`를 사용하여 해당 기능을 임의 수의 다른 개발자와 공유하고 사용할 수 있는 구성 요소로 패키지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="8e0bb-105">이 문서에서는 dotnet CLI를 사용하여 패키지를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="8e0bb-106">`dotnet` CLI를 설치하려면 [NuGet 클라이언트 도구 설치](../install-nuget-client-tools.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="8e0bb-107">Visual Studio 2017부터 dotnet CLI가 .NET Core 워크로드에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="8e0bb-108">[SDK 스타일 형식](../resources/check-project-format.md)을 사용하는 .NET Core 및 .NET Standard 프로젝트와 또 다른 SDK 스타일 프로젝트의 경우, NuGet은 프로젝트 파일의 정보를 직접 사용하여 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="8e0bb-109">단계별 자습서를 보려면 [dotnet CLI를 사용하여 .NET Standard 패키지 만들기](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) 또는 [Visual Studion를 사용하여 .NET Standard 패키지 만들기](../quickstart/create-and-publish-a-package-using-visual-studio.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) or [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="8e0bb-110">`msbuild -t:pack`은 기능적으로 `dotnet pack`과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="8e0bb-111">Msbuild를 사용하여 빌드하려면 [MSBuild를 사용하여 NuGet 패키지 만들기](creating-a-package-msbuild.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-111">To build with MSBuild, see [Create a NuGet package using MSBuild](creating-a-package-msbuild.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e0bb-112">이 항목은 일반적으로 .NET Core 및 .NET Standard 프로젝트에 해당하는 [SDK 스타일](../resources/check-project-format.md) 프로젝트에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-112">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="8e0bb-113">속성 설정</span><span class="sxs-lookup"><span data-stu-id="8e0bb-113">Set properties</span></span>

<span data-ttu-id="8e0bb-114">패키지를 만들려면 다음 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-114">The following properties are required to create a package.</span></span>

- <span data-ttu-id="8e0bb-115">`PackageId`: 패키지를 호스트하는 갤러리에서 고유해야 하는 패키지 식별자.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-115">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="8e0bb-116">지정하지 않으면 기본값 `AssemblyName`입니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-116">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="8e0bb-117">`Version`: *Major.Minor.Patch[-Suffix]* 형식의 특정 버전 번호(여기서 *-Suffix*는 [시험판 버전](prerelease-packages.md)을 식별함).</span><span class="sxs-lookup"><span data-stu-id="8e0bb-117">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="8e0bb-118">지정하지 않으면 기본값은 1.0.0입니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-118">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="8e0bb-119">호스트에 표시되어야 하는 패키지 제목(예: nuget.org)</span><span class="sxs-lookup"><span data-stu-id="8e0bb-119">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="8e0bb-120">`Authors`: 작성자 및 소유자 정보.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-120">`Authors`, author and owner information.</span></span> <span data-ttu-id="8e0bb-121">지정하지 않으면 기본값 `AssemblyName`입니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-121">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="8e0bb-122">`Company`: 회사 이름.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-122">`Company`, your company name.</span></span> <span data-ttu-id="8e0bb-123">지정하지 않으면 기본값 `AssemblyName`입니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-123">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="8e0bb-124">Visual Studio의 프로젝트 속성에서 이러한 값을 설정할 수 있습니다(솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택한 다음, **패키지** 탭 선택).</span><span class="sxs-lookup"><span data-stu-id="8e0bb-124">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="8e0bb-125">프로젝트 파일(`.csproj`)에서 직접 이러한 속성을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-125">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="8e0bb-126">nuget.org 또는 사용 중인 패키지 원본에서 고유한 식별자를 패키지에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-126">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="8e0bb-127">다음 예제에서는 해당 속성이 포함된 간단한 전체 프로젝트 파일을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-127">The following example shows a simple, complete project file with these properties included.</span></span> <span data-ttu-id="8e0bb-128">(`dotnet new classlib` 명령을 사용하여 새 기본 프로젝트를 만들 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="8e0bb-128">(You can create a new default project using the `dotnet new classlib` command.)</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="8e0bb-129">[MSBuild pack 대상](../reference/msbuild-targets.md#pack-target), [종속성 자산 제어](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) 및 [NuGet 메타데이터 속성](/dotnet/core/tools/csproj#nuget-metadata-properties)에 설명된 대로 `Title`, `PackageDescription` 및 `PackageTags`와 같은 선택적 속성을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-129">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="8e0bb-130">공용으로 빌드된 패키지의 경우 **PackageTags** 속성에 특히 주의하세요. 이러한 태그는 다른 사람들이 패키지를 찾고 그 기능을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-130">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="8e0bb-131">종속성 선언 및 버전 번호 지정에 대한 자세한 내용은 [프로젝트 파일의 패키지 참조](../consume-packages/package-references-in-project-files.md) 및 [패키지 버전](../concepts/package-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-131">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="8e0bb-132">`<IncludeAssets>` 및 `<ExcludeAssets>` 특성을 사용하여 패키지에 종속성의 자산을 직접 공개할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-132">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="8e0bb-133">자세한 내용은 [종속성 자산 제어](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-133">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="8e0bb-134">설명 필드(선택 사항) 추가</span><span class="sxs-lookup"><span data-stu-id="8e0bb-134">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="8e0bb-135">고유한 패키지 식별자 선택 및 버전 번호 설정</span><span class="sxs-lookup"><span data-stu-id="8e0bb-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a><span data-ttu-id="8e0bb-136">pack 명령 실행</span><span class="sxs-lookup"><span data-stu-id="8e0bb-136">Run the pack command</span></span>

<span data-ttu-id="8e0bb-137">프로젝트에서 NuGet 패키지(`.nupkg` 파일)를 빌드하려면 `dotnet pack` 명령을 실행합니다. 이 명령은 프로젝트도 자동으로 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-137">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="8e0bb-138">출력에는 `.nupkg` 파일의 경로가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-138">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="8e0bb-139">빌드 시 패키지를 자동으로 생성</span><span class="sxs-lookup"><span data-stu-id="8e0bb-139">Automatically generate package on build</span></span>

<span data-ttu-id="8e0bb-140">`dotnet build`를 실행할 때 `dotnet pack`을 자동으로 실행하려면 프로젝트 파일의 `<PropertyGroup>` 내에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-140">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="8e0bb-141">솔루션에서 `dotnet pack`을 실행하는 경우 패키지에 포함할 수 있는 모든 프로젝트가 솔루션에 압축됩니다([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) 속성은 `true`로 설정됨).</span><span class="sxs-lookup"><span data-stu-id="8e0bb-141">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="8e0bb-142">패키지를 자동으로 생성할 때 압축하는 데 소요되는 시간 때문에 프로젝트의 빌드 시간이 늘어납니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-142">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="8e0bb-143">패키지 설치 테스트</span><span class="sxs-lookup"><span data-stu-id="8e0bb-143">Test package installation</span></span>

<span data-ttu-id="8e0bb-144">일반적으로 패키지를 게시하기 전에 프로젝트에 패키지를 설치하는 프로세스를 테스트하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-144">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="8e0bb-145">테스트는 필요한 모든 파일이 프로젝트의 올바른 위치에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-145">The tests make sure that the necessary files all end up in their correct places in the project.</span></span>

<span data-ttu-id="8e0bb-146">일반적인 [패키지 설치 단계](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)를 사용하여 Visual Studio 또는 명령줄에서 수동으로 설치를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-146">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e0bb-147">패키지는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-147">Packages are immutable.</span></span> <span data-ttu-id="8e0bb-148">문제를 수정하고 패키지의 내용을 변경한 후 다시 압축하는 경우 다시 테스트해도 [전역 패키지](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) 폴더를 지울 때까지 이전 버전의 패키지가 계속 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-148">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="8e0bb-149">이러한 특성은 모든 빌드에서 고유한 시험판 레이블을 사용하지는 않는 패키지를 테스트할 때는 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-149">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e0bb-150">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8e0bb-150">Next Steps</span></span>

<span data-ttu-id="8e0bb-151">패키지(`.nupkg` 파일)를 만들었으면 [패키지 게시](../nuget-org/publish-a-package.md)에서 설명한 대로 원하는 갤러리에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-151">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="8e0bb-152">다음 항목에서 설명한 대로 패키지의 기능을 확장하거나 그렇지 않고 다른 시나리오를 지원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-152">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="8e0bb-153">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="8e0bb-153">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="8e0bb-154">여러 대상 프레임워크 지원</span><span class="sxs-lookup"><span data-stu-id="8e0bb-154">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="8e0bb-155">패키지 아이콘 추가</span><span class="sxs-lookup"><span data-stu-id="8e0bb-155">Add a package icon</span></span>](../reference/nuspec.md#icon)
- [<span data-ttu-id="8e0bb-156">원본 및 구성 파일 변환</span><span class="sxs-lookup"><span data-stu-id="8e0bb-156">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="8e0bb-157">지역화</span><span class="sxs-lookup"><span data-stu-id="8e0bb-157">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="8e0bb-158">시험판 버전</span><span class="sxs-lookup"><span data-stu-id="8e0bb-158">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="8e0bb-159">패키지 형식 설정</span><span class="sxs-lookup"><span data-stu-id="8e0bb-159">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="8e0bb-160">COM interop 어셈블리가 포함된 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="8e0bb-160">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="8e0bb-161">마지막으로 주의해야 할 추가 패키지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e0bb-161">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="8e0bb-162">네이티브 패키지</span><span class="sxs-lookup"><span data-stu-id="8e0bb-162">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="8e0bb-163">기호 패키지</span><span class="sxs-lookup"><span data-stu-id="8e0bb-163">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
