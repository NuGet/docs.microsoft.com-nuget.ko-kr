---
title: NuGet대상으로 팩 및 복원 MSBuild
description: NuGet pack 및 복원은 MSBuild 4.0 +의 대상으로 직접 작동할 수 있습니다 NuGet .
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 9d40d43d972537ee1cb11d54194ed6450ccd0b6e
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/23/2021
ms.locfileid: "104858968"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet대상으로 팩 및 복원 MSBuild

*NuGet 4.0 이상*

[PackageReference](../consume-packages/package-references-in-project-files.md) 형식을 사용 하는 경우 NuGet 4.0 이상에서는 별도의 파일을 사용 하지 않고 프로젝트 파일 내에 모든 매니페스트 메타 데이터를 직접 저장할 수 있습니다 `.nuspec` .

15.1 +를 사용 하는 경우 MSBuild 아래에 NuGet 설명 된 MSBuild 및 대상과 함께 최고 수준의 시민 이기도 합니다 `pack` `restore` . 이러한 대상을 사용 하면 NuGet 다른 MSBuild 작업 또는 대상과 마찬가지로 작업할 수 있습니다. 를 사용 하 여 패키지를 만드는 방법은를 NuGet MSBuild [ NuGet 사용 하 여 MSBuild 패키지 만들기 ](../create-packages/creating-a-package-msbuild.md)를 참조 하세요. (의 경우 NuGet ) 3. x 및 이전 버전에서는 대신 CLI를 통해 [pack](../reference/cli-reference/cli-ref-pack.md) 및 [restore](../reference/cli-reference/cli-ref-restore.md) 명령을 사용 NuGet 합니다.)

## <a name="target-build-order"></a>대상 빌드 순서

`pack`및는 대상 이기 때문에 액세스 하 여 `restore` 워크플로를 향상 시킬 수 있습니다 MSBuild . 예를 들어 패키지를 압축 한 후에 네트워크 공유에 복사 하려는 경우를 가정해 보겠습니다. 이렇게 하려면 프로젝트 파일에 다음을 추가하면 됩니다.

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

마찬가지로 작업 MSBuild 을 작성 하 고, 고유한 대상을 작성 하 고, NuGet 작업에서 속성을 사용할 수 있습니다 MSBuild .

> [!NOTE]
> `$(OutputPath)` 는 상대적 이며 프로젝트 루트에서 명령을 실행 하는 것으로 예상 합니다.

## <a name="pack-target"></a>pack 대상

형식을 사용 하는 .NET 프로젝트의 경우 `PackageReference` 를 사용 하 여 `msbuild -t:pack` 패키지를 만드는 데 사용할 프로젝트 파일의 입력을 그립니다 NuGet .

다음 표에서는 MSBuild 첫 번째 노드 내에서 프로젝트 파일에 추가할 수 있는 속성을 설명 합니다 `<PropertyGroup>` . Visual Studio 2017 이상에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **{project_name} 편집** 을 선택하여 이러한 편집 작업을 쉽게 수행할 수 있습니다. 편의상 테이블은 [ `.nuspec` 파일](../reference/nuspec.md)의 해당 속성을 기준으로 구성 됩니다.

> [!NOTE]
> `Owners` 및 `Summary` 의 속성 `.nuspec` 은에서 지원 되지 않습니다 MSBuild .

| 특성/ nuspec 값 | MSBuild 속성 | 기본값 | 참고 |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | MSBuild의 `$(AssemblyName)` |
| `Version` | `PackageVersion` | 버전 | 이는 semver와 호환 됩니다. 예를 들어, 또는입니다. `1.0.0` `1.0.0-beta``1.0.0-beta-00345` |
| `VersionPrefix` | `PackageVersionPrefix` | 비어 있음 | `PackageVersion`덮어쓰기 설정`PackageVersionPrefix` |
| `VersionSuffix` | `PackageVersionSuffix` | 비어 있음 | `$(VersionSuffix)` 에서 MSBuild . `PackageVersion`덮어쓰기 설정`PackageVersionSuffix` |
| `Authors` | `Authors` | 현재 사용자의 사용자 이름 | Nuget.org의 프로필 이름과 일치 하는, 세미콜론으로 구분 된 패키지 작성자 목록입니다. 이러한는 NuGet nuget.org의 갤러리에 표시 되 고 동일한 작성자가 패키지를 상호 참조 하는 데 사용 됩니다. |
| `Owners` | 해당 없음 | 에 없음 nuspec | |
| `Title` | `Title` | `PackageId`입니다. | 사람들에게 친숙한 패키지 제목이며 보통 nuget.org 및 Visual Studio의 패키지 관리자에서 UI 표시에 사용됩니다. |
| `Description` | `Description` | "패키지 설명" | 어셈블리에 대한 자세한 설명입니다. `PackageDescription`을 지정하지 않으면 이 속성이 패키지 설명으로도 사용됩니다. |
| `Copyright` | `Copyright` | 비어 있음 | 패키지에 대한 저작권 정보입니다. |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | 클라이언트에서, 소비자가 패키지를 설치하기 전에 패키지 라이선스에 동의하도록 물어야 할지 여부를 지정하는 부울 값입니다. |
| `license` | `PackageLicenseExpression` | 비어 있음 | `<license type="expression">`에 해당합니다. [라이선스 식 또는 라이선스 파일 압축을](#packing-a-license-expression-or-a-license-file)참조 하세요. |
| `license` | `PackageLicenseFile` | 비어 있음 | 사용자 지정 라이선스 또는 SPDX 식별자가 할당 되지 않은 라이선스를 사용 하는 경우 패키지 내의 라이선스 파일 경로입니다. 참조 된 라이선스 파일을 명시적으로 압축 해야 합니다. `<license type="file">`에 해당합니다. [라이선스 식 또는 라이선스 파일 압축을](#packing-a-license-expression-or-a-license-file)참조 하세요. |
| `LicenseUrl` | `PackageLicenseUrl` | 비어 있음 | `PackageLicenseUrl`는 사용되지 않습니다. 대신 `PackageLicenseExpression` 또는 `PackageLicenseFile`를 사용하십시오. |
| `ProjectUrl` | `PackageProjectUrl` | 비어 있음 | |
| `Icon` | `PackageIcon` | 비어 있음 | 패키지 아이콘으로 사용할 패키지의 이미지에 대한 경로입니다. 참조 된 아이콘 이미지 파일을 명시적으로 압축 해야 합니다. 자세한 내용은 [아이콘 이미지 파일](#packing-an-icon-image-file) 및 [ `icon` 메타 데이터](/nuget/reference/nuspec#icon)압축을 참조 하세요. |
| `IconUrl` | `PackageIconUrl` | 비어 있음 | `PackageIconUrl` 는를 위해 더 이상 사용 되지 않습니다 `PackageIcon` . 그러나 최상의 하위 환경에서는 이외에를 지정 해야 `PackageIconUrl` `PackageIcon` 합니다. |
| `Tags` | `PackageTags` | 비어 있음 | 패키지를 지정하는 세미콜론으로 구분된 태그 목록입니다. |
| `ReleaseNotes` | `PackageReleaseNotes` | 비어 있음 | 패키지에 대한 릴리스 정보입니다. |
| `Repository/Url` | `RepositoryUrl` | 비어 있음 | 소스 코드를 복제 하거나 검색 하는 데 사용 되는 리포지토리 URL입니다. 예: *https://github.com/ NuGet / NuGet . 클라이언트. git*. |
| `Repository/Type` | `RepositoryType` | 비어 있음 | 리포지토리 유형입니다. 예: `git` (기본값), `tfs` . |
| `Repository/Branch` | `RepositoryBranch` | 비어 있음 | 선택적 리포지토리 분기 정보입니다. `RepositoryUrl`도 이 속성을 포함하도록 지정해야 합니다. 예: *master* ( NuGet 4.7.0 +). |
| `Repository/Commit` | `RepositoryCommit` | 비어 있음 | 패키지가 빌드된 소스를 나타내는 선택적 리포지토리 커밋 또는 변경 집합입니다. `RepositoryUrl`도 이 속성을 포함하도록 지정해야 합니다. 예: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +). |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | 지원되지 않음 | | |

### <a name="pack-target-inputs"></a>pack 대상 입력

| 속성 | Description |
| - | - |
| `IsPackable` | 프로젝트를 압축할 수 있는지 여부를 지정하는 부울 값입니다. 기본값은 `true`입니다. |
| `SuppressDependenciesWhenPacking` | 생성 된 `true` 패키지에서 패키지 종속성을 표시 하지 않으려면로 설정 NuGet 합니다. |
| `PackageVersion` | 결과 패키지의 버전을 지정합니다. 모든 형식의 NuGet 버전 문자열을 허용 합니다. 기본값은 `$(Version)`의 값입니다. 즉 프로젝트에서 `Version` 속성의 값입니다. |
| `PackageId` | 결과 패키지의 이름을 지정합니다. 지정하지 않으면 `pack` 작업에서 기본값으로 `AssemblyName`을 사용하거나 패키지 이름으로 디렉터리 이름을 사용합니다. |
| `PackageDescription` | UI 표시를 위한 패키지에 대한 자세한 설명입니다. |
| `Authors` | Nuget.org의 프로필 이름과 일치 하는, 세미콜론으로 구분 된 패키지 작성자 목록입니다. 이러한는 NuGet nuget.org의 갤러리에 표시 되 고 동일한 작성자가 패키지를 상호 참조 하는 데 사용 됩니다. |
| `Description` | 어셈블리에 대한 자세한 설명입니다. `PackageDescription`을 지정하지 않으면 이 속성이 패키지 설명으로도 사용됩니다. |
| `Copyright` | 패키지에 대한 저작권 정보입니다. |
| `PackageRequireLicenseAcceptance` | 클라이언트에서, 소비자가 패키지를 설치하기 전에 패키지 라이선스에 동의하도록 물어야 할지 여부를 지정하는 부울 값입니다. 기본값은 `false`입니다. |
| `DevelopmentDependency` | 패키지가 다른 패키지의 종속성으로 포함되지 않도록 패키지를 개발 전용 종속성으로 표시할지 여부를 지정하는 부울 값입니다. `PackageReference`( NuGet 4.8 +)를 사용 하는 경우이 플래그는 컴파일 타임 자산이 컴파일에서 제외 됨을 의미 하기도 합니다. 자세한 내용은 [PackageReference에 대한 DevelopmentDependency 지원](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)을 참조하세요. |
| `PackageLicenseExpression` | [Spdx 라이선스 식별자](https://spdx.org/licenses/) 또는 식입니다 (예:) `Apache-2.0` . 자세한 내용은 [라이선스 식 또는 라이선스 파일 압축](#packing-a-license-expression-or-a-license-file)을 참조 하세요. |
| `PackageLicenseFile` | 사용자 지정 라이선스 또는 SPDX 식별자가 할당 되지 않은 라이선스를 사용 하는 경우 패키지 내의 라이선스 파일 경로입니다. |
| `PackageLicenseUrl` | `PackageLicenseUrl`는 사용되지 않습니다. 대신 `PackageLicenseExpression` 또는 `PackageLicenseFile`를 사용하십시오. |
| `PackageProjectUrl` | |
| `PackageIcon` | 패키지의 루트에 상대적인 패키지 아이콘 경로를 지정 합니다. 자세한 내용은 [아이콘 이미지 파일 압축](#packing-an-icon-image-file)을 참조 하세요. |
| `PackageReleaseNotes` | 패키지에 대한 릴리스 정보입니다. |
| `PackageTags` | 패키지를 지정하는 세미콜론으로 구분된 태그 목록입니다. |
| `PackageOutputPath` | 압축된 패키지가 삭제되는 출력 경로를 결정합니다. 기본값은 `$(OutputPath)`입니다. |
| `IncludeSymbols` | 이 부울 값은 프로젝트가 압축될 때 패키지에서 추가 기호 패키지를 만들어야 하는지 여부를 나타냅니다. 기호 패키지의 형식은 `SymbolPackageFormat` 속성으로 제어됩니다. 자세한 내용은 [includesymbols](#includesymbols)을 참조 하세요. |
| `IncludeSource` | 이 부울 값은 팩 프로세스에서 소스 패키지를 만들어야 하는지 여부를 나타냅니다. 소스 패키지에는 PDB 파일뿐만 아니라 라이브러리의 소스 코드가 포함되어 있습니다. 소스 파일은 결과 패키지 파일의 `src/ProjectName` 디렉터리 아래에 놓입니다. 자세한 내용은 [Includesource](#includesource)를 참조 하세요. |
| `PackageType` | |
| `IsTool` | 모든 출력 파일이 *lib* 폴더 대신 *tools* 폴더에 복사되는지 여부를 지정합니다. 자세한 내용은 [IsTool](#istool)를 참조 하세요. |
| `RepositoryUrl` | 소스 코드를 복제 하거나 검색 하는 데 사용 되는 리포지토리 URL입니다. 예: *https://github.com/ NuGet / NuGet . 클라이언트. git*. |
| `RepositoryType` | 리포지토리 유형입니다. 예: `git` (기본값), `tfs` . |
| `RepositoryBranch` | 선택적 리포지토리 분기 정보입니다. `RepositoryUrl`도 이 속성을 포함하도록 지정해야 합니다. 예: *master* ( NuGet 4.7.0 +). |
| `RepositoryCommit` | 패키지가 빌드된 소스를 나타내는 선택적 리포지토리 커밋 또는 변경 집합입니다. `RepositoryUrl`도 이 속성을 포함하도록 지정해야 합니다. 예: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +). |
| `SymbolPackageFormat` | 기호 패키지의 형식을 지정합니다. "Nupkg" 인 경우 Pdb, Dll 및 기타 출력 파일을 포함 하는 *nupkg* 확장을 사용 하 여 레거시 기호 패키지를 만듭니다. "Snupkg" 인 경우 이식 가능한 Pdb를 포함 하는 snupkg 기호 패키지가 생성 됩니다. 기본값은 "nupkg"입니다. |
| `NoPackageAnalysis` | `pack`에서 패키지를 빌드한 후 패키지 분석을 실행 하지 않도록 지정 합니다. |
| `MinClientVersion` | NuGet이 패키지를 설치할 수 있는 클라이언트의 최소 버전을 지정 하 고 nuget.exe 및 Visual Studio 패키지 관리자에 의해 적용 됩니다. |
| `IncludeBuildOutput` | 이 부울 값은 빌드 출력 어셈블리를 *.nupkg* 파일에 압축해야 할지 여부를 지정합니다. |
| `IncludeContentInPack` | 이 부울 값은 형식이 인 항목이 `Content` 자동으로 결과 패키지에 포함 되는지 여부를 지정 합니다. 기본값은 `true`입니다. |
| `BuildOutputTargetFolder` | 출력 어셈블리를 배치할 폴더를 지정합니다. 출력 어셈블리(및 기타 출력 파일)는 해당 프레임워크 폴더에 복사됩니다. 자세한 내용은 [출력 어셈블리](#output-assemblies)를 참조 하세요. |
| `ContentTargetFolders` | 가 지정 되지 않은 경우 모든 콘텐츠 파일이 이동 해야 하는 기본 위치를 지정 합니다 `PackagePath` . 기본값은 "content;contentFiles"입니다. 자세한 내용은 [패키지에 콘텐츠 포함](#including-content-in-a-package)을 참조하세요. |
| `NuspecFile` | 압축에 사용 되는 파일에 대 한 상대 또는 절대 경로 *.nuspec* 입니다. 지정 된 경우 패키징 정보에 **만** 사용 되며 프로젝트의 정보는 사용 되지 않습니다. 자세한 내용은 [를 .nuspec 사용 하 여 압축 ](#packing-using-a-nuspec-file)을 참조 하세요. |
| `NuspecBasePath` | 파일의 기본 경로 *.nuspec* 입니다. 자세한 내용은 [를 .nuspec 사용 하 여 압축 ](#packing-using-a-nuspec-file)을 참조 하세요. |
| `NuspecProperties` | key=value 쌍의 세미콜론으로 구분된 목록입니다. 자세한 내용은 [를 .nuspec 사용 하 여 압축 ](#packing-using-a-nuspec-file)을 참조 하세요. |

## <a name="pack-scenarios"></a>pack 시나리오

### <a name="suppressing-dependencies"></a>종속성 표시 안 함

생성 된 패키지에서 패키지 종속성을 표시 하지 않으려면 NuGet `SuppressDependenciesWhenPacking` 생성 된 `true` nupkg 파일에서 모든 종속성을 건너뛰도록 허용 하는을로 설정 합니다.

### `PackageIconUrl`

`PackageIconUrl` 는 속성을 위해 더 이상 사용 되지 않습니다 [`PackageIcon`](#packageicon) . NuGet5.3 및 Visual Studio 2019 버전 16.3부터 `pack` 패키지 메타 데이터는만 지정 하는 경우 [NU5048](./errors-and-warnings/nu5048.md) 경고를 발생 시킵니다 `PackageIconUrl` .

### `PackageIcon`

> [!Tip]
> 아직 지원 되지 않는 클라이언트 및 원본에 대 한 이전 버전과의 호환성을 유지 하려면 `PackageIcon` 및를 모두 지정 `PackageIcon` `PackageIconUrl` 합니다. Visual Studio `PackageIcon` 는 폴더 기반 소스에서 가져온 패키지를 지원 합니다.

#### <a name="packing-an-icon-image-file"></a>아이콘 이미지 파일 압축

아이콘 이미지 파일을 압축 하는 경우 `PackageIcon` 속성을 사용 하 여 패키지의 루트에 상대적인 아이콘 파일 경로를 지정 합니다. 또한 파일이 패키지에 포함 되어 있는지 확인 합니다. 이미지 파일 크기는 1mb로 제한 됩니다. 지원 되는 파일 형식에는 JPEG 및 PNG가 있습니다. 128x128 이미지를 확인 하는 것이 좋습니다.

예를 들어:

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

[패키지 아이콘 샘플](https://github.com/NuGet/Samples/tree/main/PackageIconExample).

이에 대 한 nuspec [ nuspec 참조는 아이콘에 대 한 참조](nuspec.md#icon)를 살펴보겠습니다.

### <a name="output-assemblies"></a>출력 어셈블리

`nuget pack`은 `.exe`, `.dll`, `.xml`, `.winmd`, `.json` 및 `.pri` 확장명의 출력 파일을 복사합니다. 복사 된 출력 파일은 대상의에서 제공 하는 내용에 따라 달라 집니다 MSBuild `BuiltOutputProjectGroup` .

MSBuild출력 어셈블리의 이동 위치를 제어 하기 위해 프로젝트 파일이 나 명령줄에서 사용할 수 있는 두 가지 속성이 있습니다.

- `IncludeBuildOutput`: 빌드 출력 어셈블리를 패키지에 포함할지 여부를 결정하는 부울입니다.
- `BuildOutputTargetFolder`: 출력 어셈블리를 배치할 폴더를 지정합니다. 출력 어셈블리(및 기타 출력 파일)는 해당 프레임워크 폴더에 복사됩니다.

### <a name="package-references"></a>패키지 참조

[프로젝트 파일의 패키지 참조](../consume-packages/package-references-in-project-files.md)를 참조하세요.

### <a name="project-to-project-references"></a>프로젝트 간 참조

프로젝트 간 참조는 기본적으로 패키지 참조로 간주 됩니다 NuGet . 예를 들어:

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

또한 다음 메타데이터를 프로젝트 참조에 추가할 수도 있습니다.

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>패키지에 내용 포함

콘텐츠를 포함하려면 기존 `<Content>` 항목에 추가 메타데이터를 추가합니다. 기본적으로 "Content" 형식의 모든 항목은 다음과 같은 항목으로 재정의하지 않는 한 패키지에 포함됩니다.

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

패키지 경로를 지정하지 않으면 기본적으로 `content` 및 `contentFiles\any\<target_framework>` 패키지 폴더의 루트에 모든 항목이 추가되고 상대 폴더 구조가 유지됩니다.

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

모든 콘텐츠를 특정 루트 폴더 (대신 `content` 및 둘 다)로 복사 하려는 경우 `contentFiles` MSBuild `ContentTargetFolders` "content; contentfiles"로 기본 설정 되지만 다른 폴더 이름으로 설정 될 수 있는 속성을 사용할 수 있습니다. `ContentTargetFolders`에 "contentFiles"를 지정하면 파일이 `buildAction`에 따라 `contentFiles\any\<target_framework>` 또는 `contentFiles\<language>\<target_framework>`에 배치됩니다.

`PackagePath`는 세미콜론으로 구분된 대상 경로의 집합일 수 있습니다. 빈 패키지 경로를 지정하면 파일이 패키지의 루트에 추가됩니다. 예를 들어 다음은 `libuv.txt`를 `content\myfiles`, `content\samples` 및 패키지 루트에 추가합니다.

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

또한 MSBuild 속성은 `$(IncludeContentInPack)` 로 기본 설정 됩니다 `true` . 모든 프로젝트에서 이 값을 `false`로 설정하면 해당 프로젝트의 내용이 NuGet 패키지에 포함되지 않습니다.

위의 항목에 대해 설정할 수 있는 기타 pack 관련 메타 데이터에는 ```<PackageCopyToOutput>``` ```<PackageFlatten>``` ```CopyToOutput``` ```Flatten``` 출력의 항목에 대 한 및 값을 설정 ```contentFiles``` nuspec 하는 및가 포함 됩니다.

> [!Note]
> Content 항목 외에도, 빌드 작업이 Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource 또는 None으로 설정된 파일에 `<Pack>` 및 `<PackagePath>` 메타데이터를 설정할 수도 있습니다.
>
> GLOB 패턴을 사용할 때 pack에서 파일 이름을 패키지 경로에 추가하려면 패키지 경로가 폴더 구분 문자로 끝나야 합니다. 그렇지 않으면 패키지 경로가 파일 이름을 포함한 전체 경로로 처리됩니다.

### <a name="includesymbols"></a>IncludeSymbols

`MSBuild -t:pack -p:IncludeSymbols=true`를 사용하면 해당 `.pdb` 파일이 다른 출력 파일(`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`)과 함께 복사됩니다. `IncludeSymbols=true`를 설정하면 일반 패키지 *및* 기호 패키지가 만들어집니다.

### <a name="includesource"></a>IncludeSource

`.pdb` 파일과 함께 원본 파일을 복사한다는 점을 제외하고는 `IncludeSymbols`와 동일합니다. `Compile` 형식의 모든 파일이 결과 패키지에서 상대 경로 폴더 구조를 유지하면서 `src\<ProjectName>\`에 복사됩니다. 또한 `TreatAsPackageReference`가 `false`로 설정된 `ProjectReference`의 원본 파일에 대해서도 마찬가지입니다.

Compile 형식의 파일이 프로젝트 폴더의 외부에 있는 경우 이 파일은 `src\<ProjectName>\`에 추가됩니다.

### <a name="packing-a-license-expression-or-a-license-file"></a>라이선스 식 또는 라이선스 파일 압축

라이선스 식을 사용 하는 경우 속성을 사용 `PackageLicenseExpression` 합니다. 샘플은 [라이선스 식 샘플](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample)을 참조 하세요.

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

. 조직에서 허용 하는 라이선스 식 및 라이선스에 대 한 자세한 NuGet 내용은 [라이선스 메타 데이터](nuspec.md#license)를 참조 하세요.

라이선스 파일을 압축 하는 경우 속성을 사용 하 여 패키지 `PackageLicenseFile` 의 루트에 상대적인 패키지 경로를 지정 합니다. 또한 파일이 패키지에 포함 되어 있는지 확인 합니다. 예를 들어:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

샘플은 [라이선스 파일 샘플](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample)을 참조 하세요.

> [!NOTE]
> , 및 중 하나만 한 `PackageLicenseExpression` `PackageLicenseFile` `PackageLicenseUrl` 번에 지정할 수 있습니다.

### <a name="packing-a-file-without-an-extension"></a>확장명 없이 파일 압축

라이선스 파일을 압축 하는 경우와 같은 일부 시나리오에서는 확장명이 없는 파일을 포함 하는 것이 좋습니다.
기록을 위해 NuGet  &  MSBuild 확장명이 없는 경로를 디렉터리로 처리 합니다.

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

[확장명 샘플이 없는 파일](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/)입니다.

### <a name="istool"></a>IsTool

`MSBuild -t:pack -p:IsTool=true`를 사용하면 [출력 어셈블리](#output-assemblies) 시나리오에서 지정한 대로 모든 출력 파일이 `lib` 폴더 대신 `tools` 폴더에 복사됩니다. 이는 `.csproj` 파일에서 `PackageType`을 설정하여 지정된 `DotNetCliTool`과 다릅니다.

### <a name="packing-using-a-nuspec-file"></a>파일을 사용 하 여 압축 `.nuspec`

일반적으로 파일에 있는 [모든 속성](../reference/msbuild-targets.md#pack-target) 을 프로젝트 파일에 포함 하는 것이 좋지만 `.nuspec` , 파일을 사용 하 여 프로젝트를 압축 하도록 선택할 수 있습니다 `.nuspec` . 를 사용 하는 비 SDK 스타일 프로젝트의 경우 `PackageReference` `NuGet.Build.Tasks.Pack.targets` pack 작업을 실행할 수 있도록를 가져와야 합니다. 여전히 프로젝트를 복원 해야 파일을 압축할 수 있습니다 nuspec . SDK 스타일 프로젝트는 기본적으로 pack 대상을 포함 합니다.

프로젝트 파일의 대상 프레임 워크는 관련이 없으며를 압축 하는 경우에는 사용 되지 않습니다 nuspec . 다음 세 가지 MSBuild 속성은을 사용 하 여 압축 하는 것과 관련이 있습니다 `.nuspec` .

1. `NuspecFile`: 압축에 사용되는 `.nuspec` 파일에 대한 상대 또는 절대 경로입니다.
1. `NuspecProperties`: 세미콜론으로 구분된 key=value 쌍의 목록입니다. 명령줄 구문 분석이 작동 하는 방식으로 인해 MSBuild 여러 속성을 다음과 같이 지정 해야 합니다 `-p:NuspecProperties="key1=value1;key2=value2"` .  
1. `NuspecBasePath`: `.nuspec` 파일에 대한 기본 경로입니다.

`dotnet.exe`를 사용하여 프로젝트를 압축하는 경우 다음 명령을 사용합니다.

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

MSBuild를 사용하여 프로젝트를 압축하는 경우 다음 명령을 사용합니다.

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

nuspecdotnet.exe 또는 msbuild를 사용 하 여를 압축 하면 기본적으로 프로젝트를 빌드할 수 있습니다. 이는 프로젝트 파일의 ```--no-build``` ```<NoBuild>true</NoBuild> ``` 설정과 함께 프로젝트 파일의 설정과 동일한 속성을 dotnet.exe 전달 하 여 방지할 수 있습니다 ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` .

파일을 압축 하는 *.csproj* 파일의 예는 nuspec 다음과 같습니다.

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a>사용자 지정 패키지를 만들기 위한 고급 확장점

`pack`대상은 내부, 대상 프레임 워크 특정 빌드에서 실행 되는 두 개의 확장 지점이 제공 됩니다. 확장 지점은 대상 프레임 워크 관련 콘텐츠 및 어셈블리를 패키지에 포함 하 여 지원 합니다.

- `TargetsForTfmSpecificBuildOutput` 대상: `lib` 폴더 또는를 사용 하 여 지정 된 폴더 내의 파일에 사용 `BuildOutputTargetFolder` 합니다.
- `TargetsForTfmSpecificContentInPackage` 대상: 외부의 파일에 사용 `BuildOutputTargetFolder` 합니다.

#### `TargetsForTfmSpecificBuildOutput`

사용자 지정 대상을 작성 하 고이를 속성의 값으로 지정 `$(TargetsForTfmSpecificBuildOutput)` 합니다. 로 이동 해야 하는 파일 `BuildOutputTargetFolder` (기본적으로 lib)의 경우 대상은 해당 파일을 ItemGroup에 쓰고 `BuildOutputInPackage` 다음 두 메타 데이터 값을 설정 해야 합니다.

- `FinalOutputPath`: 파일의 절대 경로입니다. 제공 하지 않으면 Id가 원본 경로를 평가 하는 데 사용 됩니다.
- `TargetPath`: (선택 사항) `lib\<TargetFramework>` 해당 문화권 폴더 아래에 있는 위성 어셈블리와 같이 파일을 내 하위 폴더로 이동 해야 하는 경우에 설정 합니다. 기본값은 파일의 이름입니다.

예제:

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### `TargetsForTfmSpecificContentInPackage`

사용자 지정 대상을 작성 하 고이를 속성의 값으로 지정 `$(TargetsForTfmSpecificContentInPackage)` 합니다. 패키지에 포함할 파일의 경우 대상은 해당 파일을 ItemGroup에 쓰고 `TfmSpecificPackageFile` 다음과 같은 선택적 메타 데이터를 설정 해야 합니다.

- `PackagePath`: 패키지에서 파일이 출력 되어야 하는 경로입니다. NuGet 두 개 이상의 파일이 동일한 패키지 경로에 추가 되 면 경고를 발생 시킵니다.
- `BuildAction`: 파일에 할당할 빌드 작업으로, 패키지 경로가 폴더에 있는 경우에만 필요 합니다 `contentFiles` . 기본값은 "None"입니다.

예제:
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a>restore 대상

`MSBuild -t:restore`(.NET Core 프로젝트에서 `nuget restore` 및 `dotnet restore` 사용)는 프로젝트 파일에서 참조된 패키지를 다음과 같이 복원합니다.

1. 모든 프로젝트 간 참조를 읽습니다.
1. 프로젝트 속성을 읽어 중간 폴더 및 대상 프레임워크를 찾습니다.
1. MSBuild.Build.Tasks.dll에 데이터 NuGet 전달
1. restore를 실행합니다.
1. 패키지를 다운로드합니다.
1. 자산, targets 및 props 파일을 작성합니다.

`restore`대상은 PackageReference 형식을 사용 하는 프로젝트에 대해 작동 합니다.
`MSBuild 16.5+` 또한에서는 형식에 대 한 [옵트인 지원도 제공](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) `packages.config` 합니다.

> [!NOTE]
> 대상은 `restore` 대상과 함께 [실행 해서는](#restoring-and-building-with-one-msbuild-command) 안 됩니다 `build` .

### <a name="restore-properties"></a>restore 속성

추가 복원 설정은 MSBuild 프로젝트 파일의 속성에서 가져올 수 있습니다. 또한 값은 `-p:` 스위치를 사용하여 명령줄에서 설정할 수 있습니다(아래 예제 참조).

| 속성 | Description |
|--------|--------|
| `RestoreSources` | 세미콜론으로 구분된 패키지 원본의 목록입니다. |
| `RestorePackagesPath` | 사용자 패키지 폴더에 대한 경로입니다. |
| `RestoreDisableParallel` | 다운로드를 한 번에 하나씩으로 제한합니다. |
| `RestoreConfigFile` | 적용할 `Nuget.Config` 파일에 대한 경로입니다. |
| `RestoreNoCache` | True 이면 캐시 된 패키지를 사용 하지 않습니다. [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요. |
| `RestoreIgnoreFailedSources` | true이면 실패했거나 누락된 패키지 원본을 무시합니다. |
| `RestoreFallbackFolders` | 사용자 패키지 폴더를 사용 하는 것과 같은 방식으로 사용 되는 대체 (Fallback) 폴더 |
| `RestoreAdditionalProjectSources` | 복원 하는 동안 사용할 추가 원본입니다. |
| `RestoreAdditionalProjectFallbackFolders` | 복원 중에 사용할 추가 대체 폴더입니다. |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | 에 지정 된 대체 폴더를 제외 합니다. `RestoreAdditionalProjectFallbackFolders` |
| `RestoreTaskAssemblyFile` | `NuGet.Build.Tasks.dll`에 대한 경로입니다. |
| `RestoreGraphProjectInput` | 세미콜론으로 구분된 복원할 프로젝트의 목록이며, 절대 경로가 포함되어야 합니다. |
| `RestoreUseSkipNonexistentTargets`  | 프로젝트를 통해 수집 된 프로젝트는 MSBuild 최적화를 사용 하 여 수집 되는지 여부를 결정 합니다 `SkipNonexistentTargets` . 설정 하지 않으면 기본적으로로 설정 `true` 됩니다. 결과는 프로젝트의 대상을 가져올 수 없는 경우의 빠른 오류 동작입니다. |
| `MSBuildProjectExtensionsPath` | 출력 폴더, 및 폴더에 대 한 기본값입니다 `BaseIntermediateOutputPath` `obj` . |
| `RestoreForce` | PackageReference 기반 프로젝트에서 마지막 복원이 성공한 경우에도 모든 종속성이 확인 되도록 합니다. 이 플래그를 지정 하는 것은 파일을 삭제 하는 것과 비슷합니다 `project.assets.json` . 이는 http 캐시를 우회 하지 않습니다. |
| `RestorePackagesWithLockFile` | 잠금 파일을 사용합니다. |
| `RestoreLockedMode` | 잠금 모드에서 복원을 실행 합니다. 즉, 복원은 종속성을 다시 평가 하지 않습니다. |
| `NuGetLockFilePath` | 잠금 파일의 사용자 지정 위치입니다. 기본 위치는 프로젝트 옆에 있고 이름은 `packages.lock.json` 입니다. |
| `RestoreForceEvaluate` | 강제로 복원 하 여 종속성을 다시 계산 하 고 경고 없이 잠금 파일을 업데이트 합니다. |
| `RestorePackagesConfig` | packages.config를 사용 하 여 프로젝트를 복원 하는 옵트인 스위치. 만 지원 `MSBuild -t:restore` 합니다. |
| `RestoreUseStaticGraphEvaluation` | 표준 평가 대신 정적 그래프 평가를 사용 하는 옵트인 스위치입니다 MSBuild . 정적 그래프 평가는 큰 리포지토리 및 솔루션에 대해 훨씬 더 빠른 실험적 기능입니다. |

#### <a name="examples"></a>예제

명령줄:

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

프로젝트 파일:

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a>restore 출력

restore는 `obj` 빌드 폴더에 다음 파일을 만듭니다.

| 파일 | Description |
|--------|--------|
| `project.assets.json` | 모든 패키지 참조의 종속성 그래프를 포함 합니다. |
| `{projectName}.projectFileExtension.nuget.g.props` | MSBuild패키지에 포함 된 props에 대 한 참조 |
| `{projectName}.projectFileExtension.nuget.g.targets` | MSBuild패키지에 포함 된 대상에 대 한 참조 |

### <a name="restoring-and-building-with-one-msbuild-command"></a>단일 명령을 사용 하 여 복원 및 빌드 MSBuild

NuGet MSBuild 대상 및 props을 가져오는 패키지를 복원할 수 있으므로 복원 및 빌드 평가는 다른 전역 속성을 사용 하 여 실행 됩니다.
즉, 다음은 예측할 수 없으며 종종 잘못 된 동작을 의미 합니다.

```cli
msbuild -t:restore,build
```

 대신에 권장 되는 방법은 다음과 같습니다.

```cli
msbuild -t:build -restore
```

같은 논리는와 유사한 다른 대상에도 적용 됩니다 `build` .

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a>PackageReference 및 packages.config 프로젝트 복원 MSBuild

MSBuild16.5 +를 사용 하는 경우에도 packages.config 지원 됩니다 `msbuild -t:restore` .

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> `packages.config` restore는와 함께 사용할 수 `MSBuild 16.5+` 없습니다. `dotnet.exe`

### <a name="restoring-with-msbuild-static-graph-evaluation"></a>정적 그래프 평가를 사용 하 여 복원 MSBuild

> [!NOTE]
> MSBuild16.6 +를 사용 하는 경우 NuGet 큰 리포지토리의 복원 시간이 크게 향상 되는 명령줄에서 정적 그래프 평가를 사용 하는 실험적 기능을 추가 했습니다.

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

또는 디렉터리에 속성을 설정 하 여 사용 하도록 설정할 수 있습니다.

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> Visual Studio 2019. x 및 2.x의 NuGet 경우이 기능은 실험적 이며 옵트인 (opt in) 이라고 간주 됩니다. 이 기능이 기본적으로 사용 되는 경우에 대 한 자세한 내용은 [ NuGet /Home # 9803](https://github.com/NuGet/Home/issues/9803) 를 따르세요.

정적 그래프 복원은 복원, 프로젝트 읽기 및 평가의 msbuild 부분을 변경 하지만 복원 알고리즘은 변경 하지 않습니다. 복원 알고리즘은 모든 NuGet 도구 ( NuGet .exe, MSBuild .exe, dotnet.exe 및 Visual Studio)에서 동일 합니다.

거의 모든 시나리오에서 정적 그래프 복원은 현재 복원과 다르게 동작할 수 있으며 선언 된 특정 PackageReferences 또는 ProjectReferences가 누락 될 수 있습니다.

정적 그래프 복원으로 마이그레이션할 때를 한 번만 확인 하는 것이 좋습니다.

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

NuGet 변경 *내용을 보고 하면 안 됩니다* . 불일치가 표시 되는 경우 [ NuGet /Home](https://github.com/nuget/home/issues/new)에서 문제를 파일에 입력 하세요.

### <a name="replacing-one-library-from-a-restore-graph"></a>복원 그래프에서 단일 라이브러리 대체

restore에서 잘못된 어셈블리를 가져오는 경우 해당 패키지의 기본 선택 항목을 제외하는 한편 원하는 선택 항목으로 대체할 수 있습니다. 먼저 최상위 `PackageReference`를 사용하여 모든 자산을 제외합니다.

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

그런 다음 DLL의 적절한 로컬 복사본에 대한 고유한 참조를 추가합니다.

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
