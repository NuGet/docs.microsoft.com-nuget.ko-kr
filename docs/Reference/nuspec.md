---
title: NuGet에 대한 .nuspec 파일 참조 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/29/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: .nuspec 파일은 패키지를 빌드하고 패키지 소비자에게 정보를 제공하는 데 사용되는 패키지 메타데이터를 포함합니다.
keywords: nuspec 참조, NuGet 패키지 메타데이터, NuGet 패키지 매니페스트, nuspec 스키마
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 086826b47402bb5e7066c7a10b1e2ff246fd58ea
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/03/2018
---
# <a name="nuspec-reference"></a>.nuspec 참조

`.nuspec` 파일은 패키지 메타데이터가 포함된 XML 매니페스트입니다. 이 매니페스트는 패키지를 빌드하고 소비자에게 정보를 제공하는 데 사용됩니다. 매니페스트는 항상 패키지에 포함됩니다.

항목 내용:

- [일반 형식 및 스키마](#general-form-and-schema)
- [대체 토큰](#replacement-tokens)(Visual Studio 프로젝트에서 사용하는 경우)
- [종속성](#dependencies)
- [명시적 어셈블리 참조](#explicit-assembly-references)
- [프레임워크 어셈블리 참조](#framework-assembly-references)
- [어셈블리 파일 포함](#including-assembly-files)
- [콘텐츠 파일 포함](#including-content-files)
- [예제](#examples)

## <a name="general-form-and-schema"></a>일반 형식 및 스키마

현재 `nuspec.xsd` 스키마 파일은 [NuGet GitHub 리포지토리](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)에 있습니다.

이 스키마 내에서 `.nuspec` 파일의 일반 형식은 다음과 같습니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

스키마를 시각적으로 명확하게 표시하려면, Visual Studio에서 디자인 모드로 스키마 파일을 열고 **XML 스키마 탐색기** 링크를 클릭합니다. 또는 파일을 코드로 열고, 편집기에서 마우스 오른쪽 단추를 클릭한 다음, **XML 스키마 탐색기 표시**를 선택합니다. 어느 방법이든 아래와 같은 보기가 표시됩니다(대부분의 경우 펼쳐져 있음).

![nuspec.xsd가 열려 있는 Visual Studio 스키마 탐색기](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a>metadata 특성

`<metadata>` 요소는 다음 표에서 설명하는 특성을 지원합니다.

| 특성 | 필수 | 설명 |
| --- | --- | --- | 
| **minClientVersion** | 아니요 | nuget.exe 및 Visual Studio 패키지 관리자에 의해 적용되는, 이 패키지를 설치할 수 있는 NuGet 클라이언트의 최소 버전을 지정합니다. 패키지가 특정 버전의 NuGet 클라이언트에 추가된 `.nuspec` 파일의 특정 기능에 종속될 때마다 이 특성이 사용됩니다. 예를 들어 `developmentDependency` 특성을 사용하는 패키지는 `minClientVersion`에 대해 "2.8"을 지정해야 합니다. 마찬가지로 `contentFiles` 요소(다음 섹션 참조)를 사용하는 패키지는 `minClientVersion`을 "3.3"으로 설정해야 합니다. 또한 2.5 이전의 NuGet 클라이언트에서는 이 플래그를 인식하지 못하기 때문에 `minClientVersion`에 포함된 내용에 관계없이 *항상* 패키지 설치를 거부합니다. |

### <a name="required-metadata-elements"></a>필수 metadata 요소

다음 요소는 패키지에 대한 최소 요구 사항이지만, [선택적 metadata 요소](#optional-metadata-elements)를 추가하여 개발자가 사용하는 패키지에 대한 전반적인 환경을 향상시키는 것이 좋습니다.

이러한 요소는 `<metadata>` 요소 내에 나타나야 합니다.

| 요소 | 설명 |
| --- | --- |
| **ID** | 대/소문자를 구분하지 않는 패키지 식별자이며, nuget.org 또는 패키지가 상주하는 모든 갤러리에서 고유해야 합니다. ID는 URL에 유효하지 않은 공백 또는 문자를 포함할 수 없고, 일반적으로 .NET 네임스페이스 규칙을 따릅니다. 지침은 [고유한 패키지 식별자 선택](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)을 참조하세요. |
| **version** | *major.minor.patch* 패턴을 따르는 패키지의 버전입니다. 버전 번호는 [패키지 버전 관리](../reference/package-versioning.md#pre-release-versions)에서 설명한 대로 시험판 접미사를 포함할 수 있습니다. |
| **description** | UI 표시를 위한 패키지에 대한 자세한 설명입니다. |
| **authors** | nuget.org에서 프로필 이름과 일치하는, 쉼표로 구분된 패키지 작성자 목록입니다. 이러한 목록은 nuget.org의 NuGet 갤러리에 표시되고 동일한 작성자가 패키지를 상호 참조하는 데 사용됩니다. |

### <a name="optional-metadata-elements"></a>선택적 metadata 요소

이러한 요소는 `<metadata>` 요소 내에 나타날 수 있습니다.

#### <a name="single-elements"></a>단일 요소

| 요소 | 설명 |
| --- | --- |
| **title** | 사람들에게 친숙한 패키지 제목이며 보통 nuget.org 및 Visual Studio의 패키지 관리자에서 UI 표시에 사용됩니다. 지정하지 않으면 패키지 ID가 사용됩니다. |
| **owners** | nuget.org에서 프로필 이름을 사용하는 패키지 작성자에 대한 쉼표로 구분된 목록입니다. 이는 종종 `authors`에 있는 것과 동일한 목록이며, 패키지를 nuget.org에 업로드할 때 무시됩니다. [nuget.org에서 패키지 소유자 관리](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg)를 참조하세요. |
| **projectUrl** | nuget.org뿐만 아니라 종종 UI 표시에 표시되는 패키지의 홈페이지에 대한 URL입니다. |
| **licenseUrl** | nuget.org뿐만 아니라 UI 표시에도 종종 표시되는 패키지의 라이선스에 대한 URL입니다. |
| **iconUrl** | UI 표시에서 패키지에 대한 아이콘으로 사용하는 투명한 배경이 있는 64x64 이미지에 대한 URL입니다. 이 요소에는 이미지가 포함된 웹 페이지의 URL이 아니라 *직접 이미지 URL*이 포함되어야 합니다. 예를 들어 GitHub에서 이미지를 사용 하려면 원시 파일 URL을 사용 하 여  *https://github.com/ \<username\>/\<리포지토리\>/raw/\<분기\> / \<logo.png\>*합니다. |
| **requireLicenseAcceptance** | 패키지를 설치하기 전에 클라이언트에서 소비자가 패키지 라이선스에 동의하도록 요구하는 메시지를 표시해야 할지 여부를 지정하는 부울 값입니다. |
| **developmentDependency** | *(2.8 이상)* 패키지가 다른 패키지의 종속성으로 포함되지 않도록 패키지를 개발 전용 종속성으로 표시할지 여부를 지정 하는 부울 값입니다. |
| **요약** | UI 표시를 위한 패키지에 대한 간단한 설명입니다. 생략하면 `description`의 잘린 버전이 사용됩니다. |
| **releaseNotes** | *(1.5 이상)* 패키지 설명 대신 Visual Studio 패키지 관리자의 **업데이트** 탭처럼 UI에서 자주 사용되는 이 패키지 릴리스의 변경 내용에 대한 설명입니다. |
| **copyright** | *(1.5 이상)* 패키지에 대한 저작권 세부 정보입니다. |
| **language** | 패키지에 대한 로캘 ID입니다. [지역화된 패키지 만들기](../create-packages/creating-localized-packages.md)를 참조하세요. |
| **tags** | 패키지를 설명하고 검색 및 필터링을 통해 패키지의 검색 기능을 지원하는 태그 및 키워드에 대한 공백으로 구분된 목록입니다. |
| **serviceable** | *(3.3 이상)* NuGet 내부 전용입니다. |

#### <a name="collection-elements"></a>컬렉션 요소

| 요소 | 설명 |
| --- | --- |
**packageTypes** | *(3.5 이상)* 기존 종속 패키지가 아닌 경우 패키지의 유형을 지정하는 0개 이상의 `<packageType>` 요소 컬렉션입니다. 각 packageType에는 *name* 및 *version* 특성이 있습니다. [패키지 유형 설정](../create-packages/creating-a-package.md#setting-a-package-type)을 참조하세요. |
| **dependencies** | 패키지에 대한 종속성을 지정하는 0개 이상의 `<dependency>` 요소 컬렉션입니다. 각 종속성에는 *id*, *version*, *include*(3.x 이상) 및 *exclude*(3.x 이상) 특성이 있습니다. 아래의 [종속성](#dependencies)을 참조하세요. |
| **frameworkAssemblies** | *(1.2 이상)* 이 패키지에 필요한 .NET Framework 어셈블리 참조를 식별하는 0개 이상의 `<frameworkAssembly>` 요소 컬렉션이며, 패키지를 사용하는 프로젝트에 참조가 추가되도록 합니다. 각 frameworkAssembly에는 *assemblyName* 및 *targetFramework* 특성이 있습니다. 아래의 [프레임워크 어셈블리 참조 GAC 지정](#specifying-framework-assembly-references-gac)을 참조하세요. |
| **references** | *(1.5 이상)* 프로젝트 참조로 추가된 패키지의 `lib` 폴더에 있는 어셈블리를 명명하는 0개 이상의 `<reference>` 요소 컬렉션입니다. 각 참조에는 *file* 특성이 있습니다. 또한 `<references>`에는 *targetFramework* 특성이 있는 `<group>` 요소도 포함될 수 있으며, 그런 다음 `<reference>` 요소가 포함됩니다. 생략하면 `lib`의 모든 참조가 포함됩니다. 아래의 [명시적 어셈블리 참조 지정](#specifying-explicit-assembly-references)을 참조하세요. |
| **contentFiles** | *(3.3 이상)* 사용하는 프로젝트에 포함할 콘텐츠 파일을 식별하는 `<files>` 요소 컬렉션입니다. 이러한 파일은 프로젝트 시스템 내에서 사용되는 방법을 설명하는 일단의 특성으로 지정됩니다. 아래의 [패키지에 포함할 파일 지정](#specifying-files-to-include-in-the-package)을 참조하세요. |

### <a name="files-element"></a>Files 요소

`<package>` 노드는 패키지에 포함할 어셈블리 및 콘텐츠 파일을 지정하기 위해 `<files>` 노드를 `<metadata>`에 대한 형제로 포함하고 a 또는 `<contentFiles>` 자식을 `<metadata>` 아래에 포함할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 있는 [어셈블리 파일 포함](#including-assembly-files) 및 [콘텐츠 파일 포함](#including-content-files)을 참조하세요.

## <a name="replacement-tokens"></a>대체 토큰

패키지를 만들 때 [`nuget pack` 명령](../tools/cli-ref-pack.md)은 `.nuspec` 파일의 `<metadata>` 노드에 있는 $로 구분된 토큰을 프로젝트 파일 또는 `pack` 명령의 `-properties` 스위치에서 제공하는 값으로 바꿉니다 .

명령줄에서 `nuget pack -properties <name>=<value>;<name>=<value>`를 사용하여 토큰 값을 지정합니다. 예를 들어 `.nuspec`에서 `$owners$` 및 `$desc$`와 같은 토큰을 사용하고 다음과 같이 압축 시간에 값을 제공할 수 있습니다.

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

프로젝트의 값을 사용하려면 아래 표에서 설명한 토큰을 지정합니다(AssemblyInfo는 `AssemblyInfo.cs` 또는 `AssemblyInfo.vb`과 같이 `Properties`의 파일을 나타냄).

이러한 토큰을 사용하려면 `.nuspec` 대신 프로젝트 파일이 있는 `nuget pack`을 실행합니다. 예를 들어 다음 명령을 사용하는 경우 `.nuspec` 파일의 `$id$` 및 `$version$` 토큰을 프로젝트의 `AssemblyName` 및 `AssemblyVersion` 값으로 바꿉니다.

```ps
nuget pack MyProject.csproj
```

일반적으로 프로젝트가 있는 경우 처음에는 이러한 표준 토큰 중 일부가 자동으로 포함되는 `nuget spec MyProject.csproj`를 사용하여 `.nuspec`을 만듭니다. 그러나 프로젝트에 필요한 `.nuspec` 요소 값이 부족하면 `nuget pack`이 실패합니다. 또한 프로젝트 값을 변경하는 경우 패키지를 만들기 전에 다시 빌드해야 합니다. 이 경우 pack 명령의 `build` 스위치를 사용하여 편리하게 수행할 수 있습니다.

`$configuration$`을 제외하고는 프로젝트의 값이 명령줄에서 동일한 토큰에 할당된 값보다 우선적으로 사용됩니다.

| 토큰 | 값 원본 | 값
| --- | --- | ---
| **$id$** | 프로젝트 파일 | 프로젝트 파일에서 AssemblyName (제목) |
| **$version$** | AssemblyInfo | 있는 경우 AssemblyInformationalVersion, 그렇지 않으면 AssemblyVersion |
| **$author$** | AssemblyInfo | AssemblyCompany |
| **$title$** | AssemblyInfo | AssemblyTitle |
| **$description$** | AssemblyInfo | AssemblyDescription |
| **$copyright$** | AssemblyInfo | AssemblyCopyright |
| **$configuration$** | 어셈블리 DLL | 어셈블리를 빌드하는 데 사용되는 구성이며, 기본값은 Debug입니다. Release 구성을 사용하여 패키지를 만들려면 항상 명령줄에서 `-properties Configuration=Release`를 사용합니다. |

또한 토큰은 [어셈블리 파일](#including-assembly-files) 및 [콘텐츠 파일](#including-content-files)을 포함할 때 경로를 확인하는 데 사용할 수도 있습니다. 토큰의 이름은 MSBuild 속성과 동일하므로 현재 빌드 구성에 따라 포함할 파일을 선택할 수 있습니다. 예를 들어 `.nuspec` 파일에서 다음 토큰을 사용하는 경우가 있습니다.

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

그리고 MSBuild의 `Release` 구성을 사용하여 `AssemblyName`이 `LoggingLibrary`인 어셈블리를 빌드합니다. 이 경우 패키지에 있는 `.nuspec` 파일의 결과 줄은 다음과 같습니다.

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a>종속성

`<metadata>` 내의 `<dependencies>` 요소에는 최상위 패키지가 종속되는 다른 패키지를 식별하는 임의 개수의 `<dependency>` 요소가 포함됩니다. 각 `<dependency>`에 대한 특성은 다음과 같습니다.

| 특성 | 설명 |
| --- | --- |
| `id` | (필수) 패키지 페이지에서 “EntityFramework” 및 “NUnit” 패키지 nuget.org의 이름인 같은 종속성의 패키지 ID를 보여 줍니다. |
| `version` | (필수) 종속성으로 허용되는 버전 범위입니다. 정확한 구문은 [패키지 버전 관리](../reference/package-versioning.md#version-ranges-and-wildcards)를 참조하세요. |
| include | 최종 패키지에 포함할 종속성을 나타내는 include/exclude 태그(아래 참조)에 대한 쉼표로 구분된 목록입니다. 기본값은 `none`입니다. |
| Exclude | 최종 패키지에서 제외할 종속성을 나타내는 include/exclude 태그(아래 참조)에 대한 쉼표로 구분된 목록입니다. 기본값은 `all`입니다. `exclude`로 지정된 태그는 `include`로 지정된 태그보다 우선 순위가 높습니다. 예를 들어 `include="runtime, compile" exclude="compile"`은 `include="runtime"`과 같습니다. |

| include/exclude 태그 | 영향을 받는 대상 폴더 |
| --- | --- |
| contentFiles | 콘텐츠  |
| 런타임(runtime) | Runtime, Resources 및 FrameworkAssemblies  |
| compile | lib |
| 빌드 | build(MSBuild props 및 targets) |
| native | native |
| 없음 | 영향을 받는 폴더 없음 |
| 모두 | 모든 폴더 |

예를 들어 다음 줄은 `PackageA` 버전 1.1.0 이상 및 `PackageB` 버전 1.x에 대한 종속성을 나타냅니다.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

다음 줄은 동일한 패키지에 대한 종속성을 나타내지만, `PackageA`의 `contentFiles` 및 `build` 폴더와 `PackageB`의 `native` 및 `compile` 폴더 이외의 모든 폴더를 포함하도록 지정합니다.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

참고: `nuget spec`을 사용하여 프로젝트에서 `.nuspec`을 만드는 경우 해당 프로젝트에 있는 종속성이 결과 `.nuspec` 파일에 자동으로 포함됩니다.

### <a name="dependency-groups"></a>종속성 그룹

*버전 2.0 이상*

단일 단순 목록의 대안으로, `<dependencies>` 내에서 `<group>` 요소를 사용하여 대상 프로젝트의 프레임워크 프로필에 따라 종속성을 지정할 수 있습니다.

각 그룹에는 `targetFramework`라는 특성이 있으며 0개 이상의 `<dependency>` 요소가 포함됩니다. 이러한 종속성은 대상 프레임워크가 프로젝트의 프레임워크 프로필과 호환될 때 함께 설치됩니다.

`targetFramework` 특성이 없는 `<group>` 요소는 종속성의 기본 또는 대체(fallback) 목록으로 사용됩니다. 정확한 프레임워크 식별자는 [대상 프레임워크](../reference/target-frameworks.md)를 참조하세요.

> [!Important]
> 그룹 형식은 단순 목록과 섞일 수 없습니다.

다음 예제에서는 `<group>` 요소의 여러 변형을 보여줍니다.

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>명시적 어셈블리 참조

`<references>` 요소는 패키지를 사용할 때 대상 프로젝트에서 참조해야 하는 어셈블리를 명시적으로 지정합니다. 이 요소가 있으면 NuGet은 나열된 어셈블리에 대한 참조만 추가합니다. 패키지의 `lib` 폴더에 있는 다른 어셈블리에 대한 참조는 추가하지 않습니다.

예를 들어 다음 `<references>` 요소는 패키지에 추가 어셈블리가 있는 경우에도 `xunit.dll` 및 `xunit.extensions.dll`에 대한 참조만 추가하도록 NuGet에 지시합니다.

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

명시적 참조는 일반적으로 디자인 타임 전용 어셈블리에만 사용됩니다. 예를 들어 [코드 계약](/dotnet/framework/debug-trace-profile/code-contracts)을 사용하는 경우 계약 어셈블리는 확장하는 런타임 어셈블리 옆에 있어야 Visual Studio에서 찾을 수 있습니다. 그러나 계약 어셈블리는 프로젝트에서 참조하거나 프로젝트의 `bin` 폴더에 복사할 필요가 없습니다.

마찬가지로 명시적 참조는 런타임 어셈블리 옆에 있는 도구 어셈블리가 필요하지만 프로젝트 참조로 포함될 필요가 없는 XUnit과 같은 단위 테스트 프레임워크에 사용할 수 있습니다.

### <a name="reference-groups"></a>참조 그룹

단일 단순 목록의 대안으로, `<references>` 내에서 `<group>` 요소를 사용하여 대상 프로젝트의 프레임워크 프로필에 따라 참조를 지정할 수 있습니다.

각 그룹에는 `targetFramework`라는 특성이 있으며 0개 이상의 `<reference>` 요소가 포함됩니다. 이러한 참조는 대상 프레임워크가 프로젝트의 프레임워크 프로필과 호환될 때 프로젝트에 추가 됩니다.

`targetFramework` 특성이 없는 `<group>` 요소는 참조의 기본 또는 대체(fallback) 목록으로 사용됩니다. 정확한 프레임워크 식별자는 [대상 프레임워크](../reference/target-frameworks.md)를 참조하세요.

> [!Important]
> 그룹 형식은 단순 목록과 섞일 수 없습니다.

다음 예제에서는 `<group>` 요소의 여러 변형을 보여줍니다.

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a>프레임워크 어셈블리 참조

프레임워크 어셈블리는 .NET Framework의 일부이며, 지정된 컴퓨터에 대한 GAC(전역 어셈블리 캐시)에 이미 있어야 합니다. 패키지는 `<frameworkAssemblies>` 요소 내에서 이러한 어셈블리를 식별하여 프로젝트에 해당 참조가 아직 없는 경우 필요한 참조가 프로젝트에 추가되도록 할 수 있습니다. 물론 이러한 어셈블리는 패키지에 직접 포함되지 않습니다.

`<frameworkAssemblies>` 요소는 0개 이상의 `<frameworkAssembly>` 요소를 포함하며, 각 요소마다 다음 특성을 지정합니다.

| 특성 | 설명 |
| --- | --- |
| **assemblyName** | (필수) 정규화된 어셈블리 이름입니다. |
| **targetFramework** | (선택) 이 참조가 적용되는 대상 프레임워크를 지정합니다. 생략하면 참조가 모든 프레임워크에 적용됨을 나타냅니다. 정확한 프레임워크 식별자는 [대상 프레임워크](../reference/target-frameworks.md)를 참조하세요. |

다음 예제에서는 모든 대상 프레임워크의 `System.Net`에 대한 참조와 .NET Framework 4.0 전용의 `System.ServiceModel`에 대한 참조를 보여줍니다.

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>어셈블리 파일 포함

[패키지 만들기](../create-packages/creating-a-package.md)에서 설명한 규칙을 따르면 파일 목록을 `.nuspec` 파일에 명시적으로 지정할 필요가 없습니다. `nuget pack` 명령은 필요한 파일을 자동으로 선택합니다.

> [!Important]
> 패키지가 프로젝트에 설치되면 어셈블리 참조가 지역화된 위성 어셈블리로 간주되므로 NuGet은 `.resources.dll`이라는 DLL을 *제외한* 패키지의 DLL에 해당 어셈블리 참조를 자동으로 추가합니다. 이러한 이유로 다른 경우에 필수 패키지 코드가 포함되는 파일에는 `.resources.dll`을 사용하지 마세요.

이러한 자동 동작을 무시하고 패키지에 포함되는 파일을 명시적으로 제어하려면 `<files>` 요소를 `<package>`의 자식(및 `<metadata>`의 형제)으로 배치하고 각 파일을 별도의 `<file>` 요소로 식별합니다. 예를 들어:

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

NuGet 2.x 및 이전 버전과 `packages.config`를 사용하는 프로젝트의 경우 `<files>` 요소는 패키지를 설치할 때 변경할 수 없는 콘텐츠 파일을 포함하는 데에도 사용됩니다. NuGet 3.3 이상 및 프로젝트 PackageReference에서는 `<contentFiles>` 요소가 대신 사용됩니다. 자세한 내용은 아래의 [콘텐츠 파일 포함](#including-content-files)을 참조하세요.

### <a name="file-element-attributes"></a>파일 요소 특성

각 `<file>` 요소는 다음과 같은 특성을 지정합니다.

| 특성 | 설명 |
| --- | --- |
| **src** | `exclude` 특성으로 지정된 제외에 따라 포함할 파일의 위치입니다. 절대 경로가 지정되지 않으면 경로는 `.nuspec` 파일에 대한 상대 경로입니다. `*` 와일드카드 문자가 허용되고, `**` 이중 와일드카드는 재귀적 폴더 검색을 의미합니다. |
| **target** | 원본 파일이 있는 패키지 내의 폴더에 대한 상대 경로이며, `lib`, `content`, `build` 또는 `tools`로 시작해야 합니다. [규칙 기반 작업 디렉터리에서 .nuspec 만들기](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)를 참조하세요. |
| **exclude** | `src` 위치에서 제외할 파일 또는 파일 패턴에 대한 세미콜론으로 구분된 목록입니다. `*` 와일드카드 문자가 허용되고, `**` 이중 와일드카드는 재귀적 폴더 검색을 의미합니다. |

### <a name="examples"></a>예제

**단일 어셈블리**

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

**특정 대상 프레임워크에 대한 단일 어셈블리**

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

**와일드카드를 사용하는 DLL 집합**

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

**여러 프레임워크에 대한 DLL**

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

**파일 제외**

    Source files:
        \tools\*.bak
        \tools\*.log
        \tools\build\*.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a>콘텐츠 파일 포함

콘텐츠 파일은 패키지에서 프로젝트에 포함해야 하는 변경할 수 없는 파일입니다. 변경할 수 없으므로 사용하는 프로젝트에서 수정되지 않습니다. 콘텐츠 파일의 예는 다음과 같습니다.

- 리소스로 포함된 이미지
- 이미 컴파일된 원본 파일
- 프로젝트의 빌드 출력에 포함되어야 하는 스크립트
- 프로젝트에 포함되어야 하지만 프로젝트별 변경이 필요하지 않은 패키지에 대한 구성 파일

콘텐츠 파일은 `<files>` 요소를 사용하고 `target` 특성에서 `content` 폴더를 지정하여 패키지에 포함됩니다. 그러나 `<contentFiles>` 요소를 대신 사용하는 PackageReference를 사용하여 프로젝트에 패키지를 설치하는 경우 이러한 파일은 무시됩니다.

사용하는 프로젝트와의 호환성을 최대화하기 위해 패키지는 두 요소 모두에 콘텐츠 파일을 이상적으로 지정합니다.

### <a name="using-the-files-element-for-content-files"></a>콘텐츠 파일에 대한 files 요소 사용

콘텐츠 파일의 경우 단순히 어셈블리 파일과 동일한 형식을 사용하고 다음 예제와 같이 `content`를 `target` 특성의 기본 폴더로 지정합니다.

**기본 콘텐츠 파일**

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

**디렉터리 구조가 포함된 콘텐츠 파일**

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

**특정 대상 프레임워크에 대한 콘텐츠 파일**

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

**이름에 점이 있는 폴더에 복사되는 콘텐츠 파일**

이 경우 NuGet은 `target`과 `src`의 확장명이 일치하지 않는지 확인하여 `target`의 이름 중 해당 부분을 폴더로 처리합니다.

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

**확장명이 없는 콘텐츠 파일**

확장명이 없는 파일을 포함하려면 `*` 또는 `**` 와일드카드를 사용합니다.

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

**전체 경로와 전체 대상이 포함된 콘텐츠 파일**

이 경우 원본과 대상의 파일 확장명이 일치하므로 NuGet은 대상이 폴더가 아니라 파일 이름이라고 가정합니다.

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

**패키지의 콘텐츠 파일 이름 바꾸기**

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

**파일 제외**

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a>콘텐츠 파일에 대한 contentFiles 요소 사용

*NuGet 4.0 이상(PackageReference 사용)*

기본적으로 패키지는 `contentFiles` 폴더(아래 참조) 및 기본 특성을 사용하여 해당 폴더의 모든 파일이 포함되는 `nuget pack`에 콘텐츠 파일을 배치합니다. 이 경우 `.nuspec`에 `contentFiles` 노드를 포함할 필요가 없습니다.

포함되는 파일을 제어하려면 `<contentFiles>` 요소에서 포함할 파일을 정확히 식별하는 `<files>` 요소 컬렉션을 지정합니다.

이러한 파일은 프로젝트 시스템 내에서 사용되는 방법을 설명하는 일단의 특성으로 지정됩니다.

| 특성 | 설명 |
| --- | --- |
| **include** | (필수) `exclude` 특성으로 지정된 제외에 따라 포함할 파일의 위치입니다. 절대 경로가 지정되지 않으면 경로는 `.nuspec` 파일에 대한 상대 경로입니다. `*` 와일드카드 문자가 허용되고, `**` 이중 와일드카드는 재귀적 폴더 검색을 의미합니다. |
| **exclude** | `src` 위치에서 제외할 파일 또는 파일 패턴에 대한 세미콜론으로 구분된 목록입니다. `*` 와일드카드 문자가 허용되고, `**` 이중 와일드카드는 재귀적 폴더 검색을 의미합니다. |
| **buildAction** | `Content`, `None`, `Embedded Resource`, `Compile` 등과 같이 MSBuild의 콘텐츠 항목에 할당할 빌드 작업입니다. 기본값은 `Compile`입니다. |
| **copyToOutput** | 출력 폴더를 콘텐츠 항목을 빌드 복사 (또는 게시)를 나타내는 부울입니다. 기본값은 false입니다. |
| **flatten** | 빌드 출력의 단일 폴더에 콘텐츠 항목을 복사할지(true), 아니면 패키지의 폴더 구조를 유지할지(false) 여부를 나타내는 부울 값입니다. 이 플래그는 copyToOutput 플래그가 true로 설정된 경우에만 작동합니다. 기본값은 false입니다. |

패키지를 설치할 때 NuGet에서 `<contentFiles>`의 자식 요소를 위쪽에서 아래쪽으로 적용합니다. 여러 항목이 동일한 파일과 일치하면 모든 항목이 적용됩니다. 동일한 특성에 대한 충돌이 있는 경우 최상위 항목이 하위 항목을 재정의합니다.

#### <a name="package-folder-structure"></a>패키지 폴더 구조

패키지 프로젝트는 다음 패턴을 사용하여 콘텐츠를 구성해야 합니다.

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- `codeLanguages`는 `cs`, `vb`, `fs`, `any` 또는 지정된 `$(ProjectLanguage)`에 해당하는 소문자일 수 있습니다.
- `TxM`은 NuGet에서 지원하는 모든 법적 대상 프레임워크 모니커입니다([대상 프레임워크](../reference/target-frameworks.md) 참조).
- 모든 폴더 구조는 이 구문의 끝에 추가될 수 있습니다.

예를 들어:

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

빈 폴더는 `.`을 사용하여 언어 및 TxM의 특정 조합에 대한 콘텐츠 제공을 거부할 수 있습니다. 예를 들어 다음과 같습니다.

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a>contentFiles 섹션 예제

```xml
<contentFiles>
    <!-- Embed image resources -->
    <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
    <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

    <!-- Embed all image resources under contentFiles/cs/ -->
    <files include="cs/**/*.png" buildAction="EmbeddedResource" />

    <!-- Copy config.xml to the root of the output folder -->
    <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

    <!-- Copy run.cmd to the output folder and keep the directory structure -->
    <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

    <!-- Include everything in the scripts folder except exe files -->
    <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
</contentFiles>
```

## <a name="example-nuspec-files"></a>.nuspec 파일 예제

**dependencies 또는 files를 지정하지 않은 간단한 `.nuspec`**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
    </metadata>
</package>
```

**dependencies가 있는 `.nuspec`**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

**files가 있는 `.nuspec`**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

**프레임워크 어셈블리가 있는 `.nuspec`**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

이 예제에서는 특정 프로젝트 대상에 대해 다음이 설치됩니다.

- .NET4 -> `System.Web`, `System.Net`
- .NET4 클라이언트 프로필 -> `System.Net`
- Silverlight 3 -> `System.Json`
- Silverlight 4 -> `System.Windows.Controls.DomainServices`
- WindowsPhone -> `Microsoft.Devices.Sensors`
