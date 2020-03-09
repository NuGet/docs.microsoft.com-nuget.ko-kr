---
title: MSBuild를 사용하여 NuGet 패키지 만들기
description: 파일 및 버전 관리와 같은 주요 결정 사항을 포함하여 NuGet 패키지를 디자인하고 만드는 과정을 자세히 안내합니다.
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 7166d622ef9d3975fc1c931d30caf570a765a6da
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231320"
---
# <a name="create-a-nuget-package-using-msbuild"></a><span data-ttu-id="dfc4f-103">MSBuild를 사용하여 NuGet 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="dfc4f-103">Create a NuGet package using MSBuild</span></span>

<span data-ttu-id="dfc4f-104">코드에서 NuGet 패키지를 만드는 경우 해당 기능을 여러 다른 개발자가 공유하고 사용할 수 있는 구성 요소로 패키징할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-104">When you create a NuGet package from your code, you package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="dfc4f-105">이 문서에서는 MSBuild를 사용하여 패키지를 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-105">This article describes how to create a package using MSBuild.</span></span> <span data-ttu-id="dfc4f-106">MSBuild는 NuGet이 포함된 모든 Visual Studio 워크로드와 함께 미리 설치되어 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-106">MSBuild comes preinstalled with every Visual Studio workload that contains NuGet.</span></span> <span data-ttu-id="dfc4f-107">또한 [dotnet msbuild](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild)가 포함된 dotnet CLI를 통해 MSBuild도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-107">Additionally you can also use MSBuild through the dotnet CLI with [dotnet msbuild](https://docs.microsoft.com/dotnet/core/tools/dotnet-msbuild).</span></span>

<span data-ttu-id="dfc4f-108">[SDK 스타일 형식](../resources/check-project-format.md)을 사용하는 .NET Core 및 .NET Standard 프로젝트와 또 다른 SDK 스타일 프로젝트의 경우, NuGet은 프로젝트 파일의 정보를 직접 사용하여 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span>  <span data-ttu-id="dfc4f-109">`<PackageReference>`를 사용하는 비SDK 프로젝트의 경우 NuGet에서 프로젝트 파일을 사용하여 패키지를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-109">For a non-SDK-style project that uses `<PackageReference>`, NuGet also uses the project file to create a package.</span></span>

<span data-ttu-id="dfc4f-110">SDK 스타일 프로젝트에는 기본적으로 사용할 수 있는 pack 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-110">SDK-style projects have the pack functionality available by default.</span></span> <span data-ttu-id="dfc4f-111">비SDK 스타일 PackageReference 프로젝트의 경우 프로젝트 종속성에 NuGet.Build.Tasks.Pack 패키지를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-111">For non SDK-style PackageReference projects, you need to add the NuGet.Build.Tasks.Pack package to the project dependencies.</span></span> <span data-ttu-id="dfc4f-112">Msbuild pack 대상에 대한 자세한 내용은 [MSBuild 대상으로서의 NuGet pack 및 복원](../reference/msbuild-targets.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-112">For detailed information about MSBuild pack targets, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

<span data-ttu-id="dfc4f-113">패키지를 만드는 명령인 `msbuild -t:pack`은 `dotnet pack`과 기능이 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-113">The command that creates a package, `msbuild -t:pack`, is functionality equivalent to `dotnet pack`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dfc4f-114">이 토픽은 [SDK-스타일](../resources/check-project-format.md) 프로젝트(일반적으로 .NET Core 및 .NET Standard 프로젝트)와 PackageReference를 사용하는 비SDK-스타일 프로젝트에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-114">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects, and to non-SDK-style projects that use PackageReference.</span></span>

## <a name="set-properties"></a><span data-ttu-id="dfc4f-115">속성 설정</span><span class="sxs-lookup"><span data-stu-id="dfc4f-115">Set properties</span></span>

<span data-ttu-id="dfc4f-116">패키지를 만들려면 다음 속성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-116">The following properties are required to create a package.</span></span>

- <span data-ttu-id="dfc4f-117">`PackageId`: 패키지를 호스트하는 갤러리에서 고유해야 하는 패키지 식별자.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-117">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="dfc4f-118">지정하지 않으면 기본값 `AssemblyName`입니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-118">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="dfc4f-119">`Version`: *Major.Minor.Patch[-Suffix]* 형식의 특정 버전 번호(여기서 *-Suffix*는 [시험판 버전](prerelease-packages.md)을 식별함).</span><span class="sxs-lookup"><span data-stu-id="dfc4f-119">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="dfc4f-120">지정하지 않으면 기본값은 1.0.0입니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-120">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="dfc4f-121">호스트에 표시되어야 하는 패키지 제목(예: nuget.org)</span><span class="sxs-lookup"><span data-stu-id="dfc4f-121">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="dfc4f-122">`Authors`: 작성자 및 소유자 정보.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-122">`Authors`, author and owner information.</span></span> <span data-ttu-id="dfc4f-123">지정하지 않으면 기본값 `AssemblyName`입니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-123">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="dfc4f-124">`Company`: 회사 이름.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-124">`Company`, your company name.</span></span> <span data-ttu-id="dfc4f-125">지정하지 않으면 기본값 `AssemblyName`입니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-125">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="dfc4f-126">또한 PackageReference를 사용하는, SDK 스타일이 아닌 프로젝트를 패키지하는 경우 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-126">Additionally if you are packing non-SDK-style projects that use PackageReference, the following is required:</span></span>

- <span data-ttu-id="dfc4f-127">`PackageOutputPath`에서 패키지를 호출할 때 생성되는 패키지의 출력 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-127">`PackageOutputPath`, the output folder for the package generated when calling pack.</span></span>

<span data-ttu-id="dfc4f-128">Visual Studio의 프로젝트 속성에서 이러한 값을 설정할 수 있습니다(솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택한 다음, **패키지** 탭 선택).</span><span class="sxs-lookup"><span data-stu-id="dfc4f-128">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="dfc4f-129">프로젝트 파일( *.csproj*)에서 직접 속성을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-129">You can also set these properties directly in the project files (*.csproj*).</span></span>

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="dfc4f-130">nuget.org 또는 사용 중인 패키지 원본에서 고유한 식별자를 패키지에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-130">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="dfc4f-131">다음 예제에서는 해당 속성이 포함된 간단한 전체 프로젝트 파일을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-131">The following example shows a simple, complete project file with these properties included.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="dfc4f-132">[MSBuild pack 대상](../reference/msbuild-targets.md#pack-target), [종속성 자산 제어](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) 및 [NuGet 메타데이터 속성](/dotnet/core/tools/csproj#nuget-metadata-properties)에 설명된 대로 `Title`, `PackageDescription` 및 `PackageTags`와 같은 선택적 속성을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-132">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="dfc4f-133">공용으로 빌드된 패키지의 경우 **PackageTags** 속성에 특히 주의하세요. 이러한 태그는 다른 사람들이 패키지를 찾고 그 기능을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-133">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="dfc4f-134">종속성 선언 및 버전 번호 지정에 대한 자세한 내용은 [프로젝트 파일의 패키지 참조](../consume-packages/package-references-in-project-files.md) 및 [패키지 버전](../concepts/package-versioning.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-134">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="dfc4f-135">`<IncludeAssets>` 및 `<ExcludeAssets>` 특성을 사용하여 패키지에 종속성의 자산을 직접 공개할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-135">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="dfc4f-136">자세한 내용은 [종속성 자산 제어](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-136">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="dfc4f-137">설명 필드(선택 사항) 추가</span><span class="sxs-lookup"><span data-stu-id="dfc4f-137">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="dfc4f-138">고유한 패키지 식별자 선택 및 버전 번호 설정</span><span class="sxs-lookup"><span data-stu-id="dfc4f-138">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a><span data-ttu-id="dfc4f-139">NuGet.Build.Tasks.Pack 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="dfc4f-139">Add the NuGet.Build.Tasks.Pack package</span></span>

<span data-ttu-id="dfc4f-140">비SDK 스타일 프로젝트 및 PackageReference와 MSBuild를 사용하는 경우 프로젝트에 NuGet.Build.Tasks.Pack 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-140">If you are using MSBuild with a non-SDK-style project and PackageReference, add the NuGet.Build.Tasks.Pack package to your project.</span></span>

1. <span data-ttu-id="dfc4f-141">프로젝트 파일을 열고 `<PropertyGroup>` 요소 뒤에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-141">Open the project file and add the following after the `<PropertyGroup>` element:</span></span>

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="dfc4f-142">개발자 명령 프롬프트를 엽니다(**검색** 상자에 **개발자 명령 프롬프트** 입력).</span><span class="sxs-lookup"><span data-stu-id="dfc4f-142">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="dfc4f-143">(일반적으로 **시작** 메뉴에서 “Visual Studio용 개발자 명령 프롬프트”를 시작하는 것이 좋습니다. MSBuild에 필요한 모든 경로로 구성되기 때문입니다.)</span><span class="sxs-lookup"><span data-stu-id="dfc4f-143">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

3. <span data-ttu-id="dfc4f-144">프로젝트 파일을 포함하는 폴더로 전환하고 다음 명령을 입력하여 NuGet.Build.Tasks.Pack 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-144">Switch to the folder containing the project file and type the following command to install the NuGet.Build.Tasks.Pack package.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   <span data-ttu-id="dfc4f-145">MSBuild 출력이 빌드가 성공적으로 완료되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-145">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="run-the-msbuild--tpack-command"></a><span data-ttu-id="dfc4f-146">msbuild -t:pack 명령 실행</span><span class="sxs-lookup"><span data-stu-id="dfc4f-146">Run the msbuild -t:pack command</span></span>

<span data-ttu-id="dfc4f-147">프로젝트에서 NuGet 패키지(`.nupkg` 파일)를 빌드하려면 `msbuild -t:pack` 명령을 실행합니다. 이 명령은 프로젝트도 자동으로 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-147">To build a NuGet package (a `.nupkg` file) from the project, run the `msbuild -t:pack` command, which also builds the project automatically:</span></span>

<span data-ttu-id="dfc4f-148">Visual Studio용 개발자 명령 프롬프트에서 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-148">In the Developer command prompt for Visual Studio, type the following command:</span></span>

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

<span data-ttu-id="dfc4f-149">출력에는 `.nupkg` 파일의 경로가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-149">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="dfc4f-150">빌드 시 패키지를 자동으로 생성</span><span class="sxs-lookup"><span data-stu-id="dfc4f-150">Automatically generate package on build</span></span>

<span data-ttu-id="dfc4f-151">프로젝트를 빌드하거나 복원할 때 `msbuild -t:pack`을 자동으로 실행하려면 `<PropertyGroup>`의 프로젝트 파일에 다음 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-151">To automatically run `msbuild -t:pack` when you build or restore the project, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="dfc4f-152">솔루션에서 `msbuild -t:pack`을 실행하는 경우 패키지에 포함할 수 있는 모든 프로젝트가 솔루션에 압축됩니다([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) 속성은 `true`로 설정됨).</span><span class="sxs-lookup"><span data-stu-id="dfc4f-152">When you run `msbuild -t:pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="dfc4f-153">패키지를 자동으로 생성할 때 압축하는 데 소요되는 시간 때문에 프로젝트의 빌드 시간이 늘어납니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-153">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="dfc4f-154">패키지 설치 테스트</span><span class="sxs-lookup"><span data-stu-id="dfc4f-154">Test package installation</span></span>

<span data-ttu-id="dfc4f-155">일반적으로 패키지를 게시하기 전에 프로젝트에 패키지를 설치하는 프로세스를 테스트하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-155">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="dfc4f-156">테스트를 통해 모든 파일이 프로젝트의 올바른 위치에 있는지 반드시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-156">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="dfc4f-157">일반적인 [패키지 설치 단계](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)를 사용하여 Visual Studio 또는 명령줄에서 수동으로 설치를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-157">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dfc4f-158">패키지는 변경할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-158">Packages are immutable.</span></span> <span data-ttu-id="dfc4f-159">문제를 수정하고 패키지의 내용을 변경한 후 다시 압축하는 경우 다시 테스트해도 [전역 패키지](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) 폴더를 지울 때까지 이전 버전의 패키지가 계속 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-159">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="dfc4f-160">이러한 특성은 모든 빌드에서 고유한 시험판 레이블을 사용하지는 않는 패키지를 테스트할 때는 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-160">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfc4f-161">다음 단계</span><span class="sxs-lookup"><span data-stu-id="dfc4f-161">Next Steps</span></span>

<span data-ttu-id="dfc4f-162">패키지(`.nupkg` 파일)를 만들었으면 [패키지 게시](../nuget-org/publish-a-package.md)에서 설명한 대로 원하는 갤러리에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-162">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="dfc4f-163">다음 항목에서 설명한 대로 패키지의 기능을 확장하거나 그렇지 않고 다른 시나리오를 지원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-163">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="dfc4f-164">MSBuild 대상으로서의 NuGet pack 및 restore</span><span class="sxs-lookup"><span data-stu-id="dfc4f-164">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
- [<span data-ttu-id="dfc4f-165">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="dfc4f-165">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="dfc4f-166">여러 대상 프레임워크 지원</span><span class="sxs-lookup"><span data-stu-id="dfc4f-166">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="dfc4f-167">원본 및 구성 파일 변환</span><span class="sxs-lookup"><span data-stu-id="dfc4f-167">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="dfc4f-168">지역화</span><span class="sxs-lookup"><span data-stu-id="dfc4f-168">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="dfc4f-169">시험판 버전</span><span class="sxs-lookup"><span data-stu-id="dfc4f-169">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="dfc4f-170">패키지 형식 설정</span><span class="sxs-lookup"><span data-stu-id="dfc4f-170">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="dfc4f-171">COM interop 어셈블리가 포함된 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="dfc4f-171">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="dfc4f-172">마지막으로 주의해야 할 추가 패키지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc4f-172">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="dfc4f-173">네이티브 패키지</span><span class="sxs-lookup"><span data-stu-id="dfc4f-173">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="dfc4f-174">기호 패키지</span><span class="sxs-lookup"><span data-stu-id="dfc4f-174">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
