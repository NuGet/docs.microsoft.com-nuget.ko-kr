---
title: dotnet CLI를 사용하여 NuGet 패키지 만들기
description: 파일 및 버전 관리와 같은 주요 결정 사항을 포함하여 NuGet 패키지를 디자인하고 만드는 과정을 자세히 안내합니다.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: c198bb73f0e4f5a59826db905eaf4622fe8543bc
ms.sourcegitcommit: 1799d4ac23c8aacee7498fdc72c40dd1646d267b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2020
ms.locfileid: "77476258"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a>dotnet CLI를 사용하여 NuGet 패키지 만들기

패키지의 기능 또는 포함된 코드와 관계없이 CLI 도구인 `nuget.exe` 또는 `dotnet.exe`를 사용하여 해당 기능을 임의 수의 다른 개발자와 공유하고 사용할 수 있는 구성 요소로 패키지할 수 있습니다. 이 문서에서는 dotnet CLI를 사용하여 패키지를 만드는 방법을 설명합니다. `dotnet` CLI를 설치하려면 [NuGet 클라이언트 도구 설치](../install-nuget-client-tools.md)를 참조하세요. Visual Studio 2017부터 dotnet CLI가 .NET Core 워크로드에 포함되어 있습니다.

[SDK 스타일 형식](../resources/check-project-format.md)을 사용하는 .NET Core 및 .NET Standard 프로젝트와 또 다른 SDK 스타일 프로젝트의 경우, NuGet은 프로젝트 파일의 정보를 직접 사용하여 패키지를 만듭니다. 단계별 자습서를 보려면 [dotnet CLI를 사용하여 .NET Standard 패키지 만들기](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) 또는 [Visual Studion를 사용하여 .NET Standard 패키지 만들기](../quickstart/create-and-publish-a-package-using-visual-studio.md)를 참조하세요.

`msbuild -t:pack`은 기능적으로 `dotnet pack`과 같습니다. Msbuild를 사용하여 빌드하려면 [MSBuild를 사용하여 NuGet 패키지 만들기](creating-a-package-msbuild.md)를 참조하세요.

> [!IMPORTANT]
> 이 항목은 일반적으로 .NET Core 및 .NET Standard 프로젝트에 해당하는 [SDK 스타일](../resources/check-project-format.md) 프로젝트에 적용됩니다.

## <a name="set-properties"></a>속성 설정

패키지를 만들려면 다음 속성이 필요합니다.

- `PackageId`: 패키지를 호스트하는 갤러리에서 고유해야 하는 패키지 식별자. 지정하지 않으면 기본값 `AssemblyName`입니다.
- `Version`: *Major.Minor.Patch[-Suffix]* 형식의 특정 버전 번호(여기서 *-Suffix*는 [시험판 버전](prerelease-packages.md)을 식별함). 지정하지 않으면 기본값은 1.0.0입니다.
- 호스트에 표시되어야 하는 패키지 제목(예: nuget.org)
- `Authors`: 작성자 및 소유자 정보. 지정하지 않으면 기본값 `AssemblyName`입니다.
- `Company`: 회사 이름. 지정하지 않으면 기본값 `AssemblyName`입니다.

Visual Studio의 프로젝트 속성에서 이러한 값을 설정할 수 있습니다(솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택한 다음, **패키지** 탭 선택). 프로젝트 파일(`.csproj`)에서 직접 이러한 속성을 설정할 수도 있습니다.

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> nuget.org 또는 사용 중인 패키지 원본에서 고유한 식별자를 패키지에 제공합니다.

다음 예제에서는 해당 속성이 포함된 간단한 전체 프로젝트 파일을 보여줍니다. (`dotnet new classlib` 명령을 사용하여 새 기본 프로젝트를 만들 수 있습니다.)

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

[MSBuild pack 대상](../reference/msbuild-targets.md#pack-target), [종속성 자산 제어](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets) 및 [NuGet 메타데이터 속성](/dotnet/core/tools/csproj#nuget-metadata-properties)에 설명된 대로 `Title`, `PackageDescription` 및 `PackageTags`와 같은 선택적 속성을 설정할 수도 있습니다.

> [!NOTE]
> 공용으로 빌드된 패키지의 경우 **PackageTags** 속성에 특히 주의하세요. 이러한 태그는 다른 사람들이 패키지를 찾고 그 기능을 이해하는 데 도움이 됩니다.

종속성 선언 및 버전 번호 지정에 대한 자세한 내용은 [프로젝트 파일의 패키지 참조](../consume-packages/package-references-in-project-files.md) 및 [패키지 버전](../concepts/package-versioning.md)을 참조하세요. `<IncludeAssets>` 및 `<ExcludeAssets>` 특성을 사용하여 패키지에 종속성의 자산을 직접 공개할 수도 있습니다. 자세한 내용은 [종속성 자산 제어](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)를 참조하세요.

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a>고유한 패키지 식별자 선택 및 버전 번호 설정

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a>pack 명령 실행

프로젝트에서 NuGet 패키지(`.nupkg` 파일)를 빌드하려면 `dotnet pack` 명령을 실행합니다. 이 명령은 프로젝트도 자동으로 빌드합니다.

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

출력에는 `.nupkg` 파일의 경로가 표시됩니다.

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>빌드 시 패키지를 자동으로 생성

`dotnet build`를 실행할 때 `dotnet pack`을 자동으로 실행하려면 프로젝트 파일의 `<PropertyGroup>` 내에 다음 줄을 추가합니다.

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

솔루션에서 `dotnet pack`을 실행하는 경우 패키지에 포함할 수 있는 모든 프로젝트가 솔루션에 압축됩니다([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) 속성은 `true`로 설정됨).

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

- [패키지 버전 관리](../concepts/package-versioning.md)
- [여러 대상 프레임워크 지원](../create-packages/multiple-target-frameworks-project-file.md)
- [패키지 아이콘 추가](../reference/nuspec.md#icon)
- [원본 및 구성 파일 변환](../create-packages/source-and-config-file-transformations.md)
- [지역화](../create-packages/creating-localized-packages.md)
- [시험판 버전](../create-packages/prerelease-packages.md)
- [패키지 형식 설정](../create-packages/set-package-type.md)
- [COM interop 어셈블리가 포함된 패키지 만들기](../create-packages/author-packages-with-COM-interop-assemblies.md)

마지막으로 주의해야 할 추가 패키지 유형이 있습니다.

- [네이티브 패키지](../guides/native-packages.md)
- [기호 패키지](../create-packages/symbol-packages-snupkg.md)
