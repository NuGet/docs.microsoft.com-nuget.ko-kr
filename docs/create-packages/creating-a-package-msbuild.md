---
title: MSBuild를 사용하여 NuGet 패키지 만들기
description: 파일 및 버전 관리와 같은 주요 결정 사항을 포함하여 NuGet 패키지를 디자인하고 만드는 과정을 자세히 안내합니다.
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: 92b42f0a6133565844d0b6df2cb50770793055ec
ms.sourcegitcommit: e763d9549cee3b6254ec2d6382baccb44433d42c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68860630"
---
# <a name="create-a-nuget-package-using-msbuild"></a>MSBuild를 사용하여 NuGet 패키지 만들기

코드에서 NuGet 패키지를 만드는 경우 해당 기능을 여러 다른 개발자가 공유하고 사용할 수 있는 구성 요소로 패키징할 수 있습니다. 이 문서에서는 MSBuild를 사용하여 패키지를 만드는 방법을 설명합니다. MSBuild는 NuGet이 포함된 모든 Visual Studio 워크로드와 함께 미리 설치되어 제공됩니다. 또한 [dotnet msbuild](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild)가 포함된 donet CLI를 통해 MSBuild도 사용할 수 있습니다.

[SDK 스타일 형식](../resources/check-project-format.md)을 사용하는 .NET Core 및 .NET Standard 프로젝트와 또 다른 SDK 스타일 프로젝트의 경우, NuGet은 프로젝트 파일의 정보를 직접 사용하여 패키지를 만듭니다.  `<PackageReference>`를 사용하는 비SDK 프로젝트의 경우 NuGet에서 프로젝트 파일을 사용하여 패키지를 만들 수도 있습니다.

SDK 스타일 프로젝트에는 기본적으로 사용할 수 있는 pack 기능이 있습니다. 비SDK 스타일 PackageReference 프로젝트의 경우 프로젝트 종속성에 NuGet.Build.Tasks.Pack 패키지를 추가해야 합니다. Msbuild pack 대상에 대한 자세한 내용은 [MSBuild 대상으로서의 NuGet pack 및 복원](../reference/msbuild-targets.md)을 참조하세요.

패키지를 만드는 명령인 `msbuild -t:pack`은 `dotnet pack`과 기능이 같습니다.

> [!IMPORTANT]
> 이 토픽은 [SDK-스타일](../resources/check-project-format.md) 프로젝트(일반적으로 .NET Core 및 .NET Standard 프로젝트)와 PackageReference를 사용하는 비SDK-스타일 프로젝트에 적용됩니다.

## <a name="set-properties"></a>속성 설정

패키지를 만들려면 다음 속성이 필요합니다.

- `PackageId`: 패키지를 호스트하는 갤러리에서 고유해야 하는 패키지 식별자. 지정하지 않으면 기본값 `AssemblyName`입니다.
- `Version`: *Major.Minor.Patch[-Suffix]* 형식의 특정 버전 번호(여기서 *-Suffix*는 [시험판 버전](prerelease-packages.md)을 식별함). 지정하지 않으면 기본값은 1.0.0입니다.
- 호스트에 표시되어야 하는 패키지 제목(예: nuget.org)
- `Authors`: 작성자 및 소유자 정보. 지정하지 않으면 기본값 `AssemblyName`입니다.
- `Company`: 회사 이름. 지정하지 않으면 기본값 `AssemblyName`입니다.

Visual Studio의 프로젝트 속성에서 이러한 값을 설정할 수 있습니다(솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택한 다음, **패키지** 탭 선택). 프로젝트 파일( *.csproj*)에서 직접 속성을 설정할 수도 있습니다.

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> nuget.org 또는 사용 중인 패키지 원본에서 고유한 식별자를 패키지에 제공합니다.

다음 예제에서는 해당 속성이 포함된 간단한 전체 프로젝트 파일을 보여줍니다.

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

[MSBuild pack 대상](../reference/msbuild-targets.md#pack-target), [종속성 자산 제어](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) 및 [NuGet 메타데이터 속성](/dotnet/core/tools/csproj#nuget-metadata-properties)에 설명된 대로 `Title`, `PackageDescription` 및 `PackageTags`와 같은 선택적 속성을 설정할 수도 있습니다.

> [!NOTE]
> 공용으로 빌드된 패키지의 경우 **PackageTags** 속성에 특히 주의하세요. 이러한 태그는 다른 사람들이 패키지를 찾고 그 기능을 이해하는 데 도움이 됩니다.

종속성 선언 및 버전 번호 지정에 대한 자세한 내용은 [프로젝트 파일의 패키지 참조](../consume-packages/package-references-in-project-files.md) 및 [패키지 버전](../reference/package-versioning.md)을 참조하세요. `<IncludeAssets>` 및 `<ExcludeAssets>` 특성을 사용하여 패키지에 종속성의 자산을 직접 공개할 수도 있습니다. 자세한 내용은 [종속성 자산 제어](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)를 참조하세요.

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>고유한 패키지 식별자 선택 및 버전 번호 설정

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a>NuGet.Build.Tasks.Pack 패키지 추가

비SDK 스타일 프로젝트 및 PackageReference와 MSBuild를 사용하는 경우 프로젝트에 NuGet.Build.Tasks.Pack 패키지를 추가합니다.

1. 프로젝트 파일을 열고 `<PropertyGroup>` 요소 뒤에 다음을 추가합니다.

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. 개발자 명령 프롬프트를 엽니다(**검색** 상자에 **개발자 명령 프롬프트** 입력).

   (일반적으로 **시작** 메뉴에서 “Visual Studio용 개발자 명령 프롬프트”를 시작하는 것이 좋습니다. MSBuild에 필요한 모든 경로로 구성되기 때문입니다.)

3. 프로젝트 파일을 포함하는 폴더로 전환하고 다음 명령을 입력하여 NuGet.Build.Tasks.Pack 패키지를 설치합니다.

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   MSBuild 출력이 빌드가 성공적으로 완료되었음을 나타냅니다.

## <a name="run-the-msbuild--tpack-command"></a>msbuild -t:pack 명령 실행

프로젝트에서 NuGet 패키지(`.nupkg` 파일)를 빌드하려면 `msbuild -t:pack` 명령을 실행합니다. 이 명령은 프로젝트도 자동으로 빌드합니다.

Visual Studio용 개발자 명령 프롬프트에서 다음 명령을 입력합니다.

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

출력에는 `.nupkg` 파일의 경로가 표시됩니다.

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

### <a name="automatically-generate-package-on-build"></a>빌드 시 패키지를 자동으로 생성

프로젝트를 빌드하거나 복원할 때 `msbuild -t:pack`을 자동으로 실행하려면 `<PropertyGroup>`의 프로젝트 파일에 다음 줄을 추가합니다.

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

솔루션에서 `msbuild -t:pack`을 실행하는 경우 패키지에 포함할 수 있는 모든 프로젝트가 솔루션에 압축됩니다([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) 속성은 `true`로 설정됨).

> [!NOTE]
> 패키지를 자동으로 생성할 때 압축하는 데 소요되는 시간 때문에 프로젝트의 빌드 시간이 늘어납니다.

### <a name="test-package-installation"></a>패키지 설치 테스트

일반적으로 패키지를 게시하기 전에 프로젝트에 패키지를 설치하는 프로세스를 테스트하려고 합니다. 테스트를 통해 모든 파일이 프로젝트의 올바른 위치에 있는지 반드시 확인합니다.

일반적인 [패키지 설치 단계](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)를 사용하여 Visual Studio 또는 명령줄에서 수동으로 설치를 테스트할 수 있습니다.

> [!IMPORTANT]
> 패키지는 변경할 수 없습니다. 문제를 수정하고 패키지의 내용을 변경한 후 다시 압축하는 경우 다시 테스트해도 [전역 패키지](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) 폴더를 지울 때까지 이전 버전의 패키지가 계속 사용됩니다. 이러한 특성은 모든 빌드에서 고유한 시험판 레이블을 사용하지는 않는 패키지를 테스트할 때는 문제가 되지 않습니다.

## <a name="next-steps"></a>다음 단계

패키지(`.nupkg` 파일)를 만들었으면 [패키지 게시](../nuget-org/publish-a-package.md)에서 설명한 대로 원하는 갤러리에 게시할 수 있습니다.

다음 항목에서 설명한 대로 패키지의 기능을 확장하거나 그렇지 않고 다른 시나리오를 지원할 수도 있습니다.

- [MSBuild 대상으로서의 NuGet pack 및 restore](../reference/msbuild-targets.md)
- [패키지 버전 관리](../reference/package-versioning.md)
- [여러 대상 프레임워크 지원](../create-packages/multiple-target-frameworks-project-file.md)
- [원본 및 구성 파일 변환](../create-packages/source-and-config-file-transformations.md)
- [지역화](../create-packages/creating-localized-packages.md)
- [시험판 버전](../create-packages/prerelease-packages.md)
- [패키지 형식 설정](../create-packages/set-package-type.md)
- [COM interop 어셈블리가 포함된 패키지 만들기](../create-packages/author-packages-with-COM-interop-assemblies.md)

마지막으로 주의해야 할 추가 패키지 유형이 있습니다.

- [네이티브 패키지](../create-packages/native-packages.md)
- [기호 패키지](../create-packages/symbol-packages.md)
