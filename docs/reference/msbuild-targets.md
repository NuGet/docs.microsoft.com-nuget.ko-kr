---
title: MSBuild 대상으로서의 NuGet pack 및 restore
description: NuGet pack 및 restore는 NuGet 4.0 이상에서 MSBuild 대상으로 직접 작동할 수 있습니다.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: a9427d87f69a2e942a9802fbdae5193eead1c724
ms.sourcegitcommit: af58d59669674c3bc0a230d5764e37020a9a3f1e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2018
ms.locfileid: "52831022"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>MSBuild 대상으로서의 NuGet pack 및 restore

*NuGet 4.0 이상*

PackageReference 형식을 사용하면 NuGet 4.0 이상은 별도의 `.nuspec` 파일을 사용하는 대신 프로젝트 파일 내에서 모든 매니페스트 메타데이터를 직접 저장할 수 있습니다.

MSBuild 15.1 이상에서 NuGet은 아래에서 설명한 대로 `pack` 및 `restore` 대상이 있는 일류 MSBuild 시민이기도 합니다. 이러한 대상을 사용하면 다른 MSBuild 작업 또는 대상과 마찬가지로 NuGet을 사용하여 작업할 수 있습니다. (NuGet 3.x 및 이전 버전의 경우 NuGet CLI를 통해 [pack](../tools/cli-ref-pack.md) 및 [restore](../tools/cli-ref-restore.md) 명령을 대신 사용합니다.)

## <a name="target-build-order"></a>대상 빌드 순서

`pack` 및 `restore`는 MSBuild 대상이므로 이 대상에 액세스하여 워크플로를 향상시킬 수 있습니다. 예를 들어 패키지를 압축한 후 네트워크 공유에 복사한다고 가정해 보겠습니다. 이렇게 하려면 프로젝트 파일에 다음을 추가하면 됩니다.

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

마찬가지로, MSBuild 작업을 작성하고, 고유한 대상을 작성하고, MSBuild 작업에서 NuGet 속성을 사용할 수 있습니다.

## <a name="pack-target"></a>pack 대상

PackageReference 형식을 사용 하 여.NET Standard 프로젝트에 대 한 `msbuild -t:pack` NuGet 패키지를 만드는 데 사용할 프로젝트 파일에서 입력을 가져옵니다.

아래 표에서는 첫 번째 `<PropertyGroup>` 노드 내에서 프로젝트 파일에 추가할 수 있는 MSBuild 속성을 설명합니다. Visual Studio 2017 이상에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **{project_name} 편집**을 선택하여 이러한 편집 작업을 쉽게 수행할 수 있습니다. 편의상 이 표는 [`.nuspec` 파일 ](../reference/nuspec.md)에 있는 동등한 속성으로 구성되었습니다.

`.nuspec`의 `Owners` 및 `Summary` 속성은 MSBuild에서 지원되지 않습니다.

| 특성/NuSpec 값 | MSBuild 속성 | 기본 | 노트 |
|--------|--------|--------|--------|
| ID | PackageId | AssemblyName | MSBuild의 $(AssemblyName)입니다. |
| 버전 | PackageVersion | 버전 | "1.0.0", "1.0.0-beta" 또는 "1.0.0-beta-00345"와 같이 semver와 호환됩니다. |
| VersionPrefix | PackageVersionPrefix | 비어 있음 | PackageVersion을 설정하면 PackageVersionPrefix를 덮어씁니다. |
| VersionSuffix | PackageVersionSuffix | 비어 있음 | MSBuild의 $(VersionSuffix)입니다. PackageVersion을 설정하면 PackageVersionSuffix를 덮어씁니다. |
| 만든 이 | 만든 이 | 현재 사용자의 사용자 이름 | |
| Owners | N/A | NuSpec에는 없음 | |
| 제목 | 제목 | PackageId| |
| 설명 | 설명 | "패키지 설명" | |
| Copyright | Copyright | 비어 있음 | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | False | |
| 라이선스 | PackageLicenseExpression | 비어 있음 | 에 해당 `<license type="expression">` |
| 라이선스 | PackageLicenseFile | 비어 있음 | `<license type="file">`에 해당합니다. 명시적으로 참조 된 라이선스 파일을 압축 해야 합니다. |
| LicenseUrl | PackageLicenseUrl | 비어 있음 | `licenseUrl` PackageLicenseExpression 또는 PackageLicenseFile 속성을 사용 하 여 계속 |
| ProjectUrl | PackageProjectUrl | 비어 있음 | |
| IconUrl | PackageIconUrl | 비어 있음 | |
| Tags | PackageTags | 비어 있음 | 세미콜론으로 구분합니다. |
| ReleaseNotes | PackageReleaseNotes | 비어 있음 | |
| 리포지토리/Url | RepositoryUrl | 비어 있음 | 복제 또는 소스 코드를 검색 하는 데 사용 되는 리포지토리 URL입니다. 예: *https://github.com/NuGet/NuGet.Client.git* |
| 저장소/유형 | RepositoryType | 비어 있음 | 리포지토리 유형입니다. 예: *git*하십시오 *tfs*합니다. |
| 리포지토리/분기 | RepositoryBranch | 비어 있음 | 선택적 리포지토리에서 분기 정보입니다. *RepositoryUrl* 포함 되도록이 속성에도 지정 해야 합니다. 예: *마스터* (NuGet 4.7.0+) |
| 저장소/커밋 | RepositoryCommit | 비어 있음 | 선택적 저장소 커밋 또는 패키지 소스를 나타내기 위해 변경 집합에 대해 구축 되었습니다. *RepositoryUrl* 포함 되도록이 속성에도 지정 해야 합니다. 예: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| 요약 | 지원 안 함 | | |

### <a name="pack-target-inputs"></a>pack 대상 입력

- IsPackable
- PackageVersion
- PackageId
- 만든 이
- 설명
- Copyright
- PackageRequireLicenseAcceptance
- DevelopmentDependency
- PackageLicenseExpression
- PackageLicenseFile
- PackageLicenseUrl
- PackageProjectUrl
- PackageIconUrl
- PackageReleaseNotes
- PackageTags
- PackageOutputPath
- IncludeSymbols
- IncludeSource
- PackageTypes
- IsTool
- RepositoryUrl
- RepositoryType
- RepositoryBranch
- RepositoryCommit
- NoPackageAnalysis
- MinClientVersion
- IncludeBuildOutput
- IncludeContentInPack
- BuildOutputTargetFolder
- ContentTargetFolders
- NuspecFile
- NuspecBasePath
- NuspecProperties

## <a name="pack-scenarios"></a>pack 시나리오

### <a name="packageiconurl"></a>PackageIconUrl

에 대 한 변경의 일부로 [NuGet 문제 352](https://github.com/NuGet/Home/issues/352)를 `PackageIconUrl` 최종적으로 변경 됩니다 `PackageIconUri` 및 결과 패키지의 루트에 포함 될 아이콘 파일에 상대 경로가 될 수 있습니다.

### <a name="output-assemblies"></a>출력 어셈블리

`nuget pack`은 `.exe`, `.dll`, `.xml`, `.winmd`, `.json` 및 `.pri` 확장명의 출력 파일을 복사합니다. 복사되는 출력 파일은 `BuiltOutputProjectGroup` 대상에서 제공하는 MSBuild에 따라 다릅니다.

프로젝트 파일 또는 명령줄에서 출력 어셈블리의 위치를 제어하는 데 사용할 수 있는 두 가지 MSBuild 속성이 있습니다.

- `IncludeBuildOutput`: 빌드 출력 어셈블리를 패키지에 포함할지 여부를 결정하는 부울입니다.
- `BuildOutputTargetFolder`: 출력 어셈블리를 배치할 폴더를 지정합니다. 출력 어셈블리(및 기타 출력 파일)는 해당 프레임워크 폴더에 복사됩니다.

### <a name="package-references"></a>패키지 참조

[프로젝트 파일의 패키지 참조](../consume-packages/package-references-in-project-files.md)를 참조하세요.

### <a name="project-to-project-references"></a>프로젝트 간 참조

프로젝트 간 참조는 기본적으로 NuGet 패키지 참조로 간주됩니다. 예를 들어 다음과 같습니다.

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

모든 내용을 특정 루트 폴더(`content` 및 `contentFiles` 대신)에만 복사하려면 `ContentTargetFolders` MSBuild 속성을 사용할 수 있습니다. 이 속성은 기본적으로 "content; contentFiles"이지만 다른 폴더 이름으로 설정할 수 있습니다. `ContentTargetFolders`에 "contentFiles"를 지정하면 파일이 `buildAction`에 따라 `contentFiles\any\<target_framework>` 또는 `contentFiles\<language>\<target_framework>`에 배치됩니다.

`PackagePath`는 세미콜론으로 구분된 대상 경로의 집합일 수 있습니다. 빈 패키지 경로를 지정하면 파일이 패키지의 루트에 추가됩니다. 예를 들어 다음은 `libuv.txt`를 `content\myfiles`, `content\samples` 및 패키지 루트에 추가합니다.

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

또한 `$(IncludeContentInPack)` MSBuild 속성이 있으며 기본값은 `true`입니다. 모든 프로젝트에서 이 값을 `false`로 설정하면 해당 프로젝트의 내용이 NuGet 패키지에 포함되지 않습니다.

위의 항목 중 하나에서 설정할 수 있는 다른 pack 특정 메타데이터에는 nuspec 출력의 ```contentFiles``` 항목에 ```CopyToOutput``` 및 ```Flatten``` 값을 설정하는 ```<PackageCopyToOutput>``` 및 ```<PackageFlatten>```이 포함됩니다.

> [!Note]
> Content 항목 외에도, 빌드 작업이 Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource 또는 None으로 설정된 파일에 `<Pack>` 및 `<PackagePath>` 메타데이터를 설정할 수도 있습니다.
>
> GLOB 패턴을 사용할 때 pack에서 파일 이름을 패키지 경로에 추가하려면 패키지 경로가 폴더 구분 문자로 끝나야 합니다. 그렇지 않으면 패키지 경로가 파일 이름을 포함한 전체 경로로 처리됩니다.

### <a name="includesymbols"></a>IncludeSymbols

`MSBuild -t:pack -p:IncludeSymbols=true`를 사용하면 해당 `.pdb` 파일이 다른 출력 파일(`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`)과 함께 복사됩니다. `IncludeSymbols=true`를 설정하면 일반 패키지 *및* 기호 패키지가 만들어집니다.

### <a name="includesource"></a>IncludeSource

`.pdb` 파일과 함께 원본 파일을 복사한다는 점을 제외하고는 `IncludeSymbols`와 동일합니다. `Compile` 형식의 모든 파일이 결과 패키지에서 상대 경로 폴더 구조를 유지하면서 `src\<ProjectName>\`에 복사됩니다. 또한 `TreatAsPackageReference`가 `false`로 설정된 `ProjectReference`의 원본 파일에 대해서도 마찬가지입니다.

Compile 형식의 파일이 프로젝트 폴더의 외부에 있는 경우 이 파일은 `src\<ProjectName>\`에 추가됩니다.

### <a name="packing-a-license-expression-or-a-license-file"></a>라이선스 식 또는 라이선스 파일을 압축합니다.

라이선스 식 사용 PackageLicenseExpression 속성을 사용 해야 합니다. 
[라이선스 식 샘플](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)합니다.

라이선스 파일을 압축할 때 PackageLicenseFile 속성을 사용 하 여 패키지의 루트에 상대적인 패키지 경로 지정 해야 합니다. 또한 파일 패키지에 포함 되어 있는지 확인 해야 합니다. 예를 들어 다음과 같습니다.

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath="$(PackageLicenseFile)"/>
</ItemGroup>
```
[라이선스 파일 샘플](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)합니다.

### <a name="istool"></a>IsTool

`MSBuild -t:pack -p:IsTool=true`를 사용하면 [출력 어셈블리](#output-assemblies) 시나리오에서 지정한 대로 모든 출력 파일이 `lib` 폴더 대신 `tools` 폴더에 복사됩니다. 이는 `.csproj` 파일에서 `PackageType`을 설정하여 지정된 `DotNetCliTool`과 다릅니다.

### <a name="packing-using-a-nuspec"></a>.nuspec을 사용하여 압축

사용할 수는 `.nuspec` SDK 프로젝트 파일을 가져올가 있는 경우 프로젝트를 압축 파일 `NuGet.Build.Tasks.Pack.targets` 팩 작업을 실행할 수 있도록 합니다. Nuspec 파일을 압축 하기 전에 프로젝트를 복원 해야 합니다. 프로젝트 파일의 대상 프레임 워크로 관련이 없는 고 nuspec을 압축할 때 사용 되지 않습니다. 다음 세 가지 MSBuild 속성은 `.nuspec`을 사용하여 압축하는 것과 관련이 있습니다.

1. `NuspecFile`: 압축에 사용되는 `.nuspec` 파일에 대한 상대 또는 절대 경로입니다.
1. `NuspecProperties`: 세미콜론으로 구분된 key=value 쌍의 목록입니다. MSBuild 명령줄 구문 분석이 작동하는 방식으로 인해 여러 속성을 `-p:NuspecProperties=\"key1=value1;key2=value2\"`와 같이 지정해야 합니다.  
1. `NuspecBasePath`: `.nuspec` 파일에 대한 기본 경로입니다.

`dotnet.exe`를 사용하여 프로젝트를 압축하는 경우 다음 명령을 사용합니다.

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

MSBuild를 사용하여 프로젝트를 압축하는 경우 다음 명령을 사용합니다.

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

해당 nuspec dotnet.exe를 사용 하 여 압축을 유의 하십시오 또는 기본적으로 프로젝트를 구축 하는 데 msbuild 많아집니다. 전달 하 여이 방지할 수 있습니다 ```--no-build``` 속성을 설정의 해당 하는 dotnet.exe ```<NoBuild>true</NoBuild> ``` 설정 함께 프로젝트 파일에서 ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` 프로젝트 파일에서

Nuspec 파일을 압축할 csproj 파일의 예제는 다음과 같습니다.

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

### <a name="advanced-extension-points-to-create-customized-package"></a>고급 사용자 지정된 패키지를 만들려면 확장 지점

`pack` 대상 내부 대상 프레임 워크 특정 빌드에서 실행 되는 두 개의 확장 지점을 제공 합니다. 대상 프레임 워크 특정 콘텐츠 및 어셈블리는 패키지를 비롯 하 여 확장 지점을 지원합니다.

- `TargetsForTfmSpecificBuildOutput` 대상: 내에서 파일에 대 한 사용 합니다 `lib` 를 사용 하 여 지정 된 폴더나 폴더 `BuildOutputTargetFolder`.
- `TargetsForTfmSpecificContentInPackage` 대상: 외부 파일에 대 한 사용을 `BuildOutputTargetFolder`입니다.

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

사용자 지정 대상을 작성 하 고 값으로 지정 된 `$(TargetsForTfmSpecificBuildOutput)` 속성입니다. 로 이동 해야 하는 모든 파일에 대 한는 `BuildOutputTargetFolder` (lib) 기본적으로 대상의 ItemGroup에 해당 파일을 작성 해야 `BuildOutputInPackage` 다음 두 메타 데이터 값을 설정 합니다.

- `FinalOutputPath`파일의 절대 경로: 지정 하지 않으면 Id 원본 경로 평가에 사용 됩니다.
- `TargetPath`: (선택 사항) 파일 내에서 하위 폴더로 이동 해야 할 때 설정 `lib\<TargetFramework>` 과 같이 위성 어셈블리는 각 문화권 폴더 아래에 있는 해당 이동 합니다. 기본값은 파일의 이름입니다.

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

#### <a name="targetsfortfmspecificcontentinpackage"></a>TargetsForTfmSpecificContentInPackage

사용자 지정 대상을 작성 하 고 값으로 지정 된 `$(TargetsForTfmSpecificContentInPackage)` 속성입니다. 패키지에 포함할 모든 파일에 대 한 대상 해야 해당 파일에 쓸 ItemGroup `TfmSpecificPackageFile` 다음과 같은 선택적 메타 데이터를 설정 합니다.

- `PackagePath`: 파일은 패키지의 출력 이어야 하는 위치 경로입니다. 둘 이상의 파일에서 동일한 패키지 경로에 추가 되 면 NuGet 경고를 발생 시킵니다.
- `BuildAction`: 빌드 작업 파일을 할당할 패키지 경로만 필요 합니다 `contentFiles` 폴더입니다. 기본값은 "None"입니다.

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
1. msbuild 데이터를 NuGet.Build.Tasks.dll에 전달합니다.
1. restore를 실행합니다.
1. 패키지를 다운로드합니다.
1. 자산, targets 및 props 파일을 작성합니다.

합니다 `restore` works 대상 **만** PackageReference 형식을 사용 하 여 프로젝트에 대 한 합니다. 것 **되지** 사용 하 여 프로젝트에 대해 작동 합니다 `packages.config` 은 형식을 사용 하 여 [nuget 복원](../tools/cli-ref-restore.md) 대신 합니다.

### <a name="restore-properties"></a>restore 속성

추가 restore 설정은 프로젝트 파일의 MSBuild 속성에서 가져올 수 있습니다. 또한 값은 `-p:` 스위치를 사용하여 명령줄에서 설정할 수 있습니다(아래 예제 참조).

| 속성 | 설명 |
|--------|--------|
| RestoreSources | 세미콜론으로 구분된 패키지 원본의 목록입니다. |
| RestorePackagesPath | 사용자 패키지 폴더에 대한 경로입니다. |
| RestoreDisableParallel | 다운로드를 한 번에 하나씩으로 제한합니다. |
| RestoreConfigFile | 적용할 `Nuget.Config` 파일에 대한 경로입니다. |
| RestoreNoCache | True 이면 캐시 된 패키지를 사용 하 여 방지할 수 있습니다. 참조 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다. |
| RestoreIgnoreFailedSources | true이면 실패했거나 누락된 패키지 원본을 무시합니다. |
| RestoreTaskAssemblyFile | `NuGet.Build.Tasks.dll`에 대한 경로입니다. |
| RestoreGraphProjectInput | 세미콜론으로 구분된 복원할 프로젝트의 목록이며, 절대 경로가 포함되어야 합니다. |
| RestoreOutputPath | 출력 폴더이며, 기본값은 `obj` 폴더입니다. |

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

| 파일 | 설명 |
|--------|--------|
| `project.assets.json` | 패키지에 대 한 모든 참조의 종속성 그래프를 포함합니다. |
| `{projectName}.projectFileExtension.nuget.g.props` | 패키지에 포함된 MSBuild props 파일에 대한 참조 |
| `{projectName}.projectFileExtension.nuget.g.targets` | 패키지에 포함된 MSBuild targets 파일에 대한 참조 |

### <a name="packagetargetfallback"></a>PackageTargetFallback

`PackageTargetFallback` 요소를 사용하면 패키지를 복원할 때 사용할 호환 가능한 대상 집합을 지정할 수 있습니다. dotnet [TxM](../reference/target-frameworks.md)을 사용하는 패키지가 dotnet TxM을 선언하지 않은 호환 패키지와 함께 작동하도록 설계되었습니다. 즉 프로젝트에서 dotnet TxM을 사용하는 경우, 비dotnet 플랫폼이 dotnet과 호환될 수 있도록 이상 프로젝트에 `<PackageTargetFallback>`을 추가하지 않는 한, 종속되는 모든 패키지에도 dotnet TxM이 있어야 합니다.

예를 들어 프로젝트에서 `netstandard1.6` TxM을 사용하고 종속 패키지에 `lib/net45/a.dll` 및 `lib/portable-net45+win81/a.dll`만 포함되어 있으면 프로젝트 빌드에 실패합니다. 가져오려는 항목이 후자의 DLL이면 다음과 같이 `PackageTargetFallback`을 추가하여 `portable-net45+win81` DLL이 호환 가능하다고 나타낼 수 있습니다.

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

프로젝트의 모든 대상에 대해 대체(fallback)를 선언하려면 `Condition` 특성을 해제합니다. 또한 다음과 같이 `$(PackageTargetFallback)`을 포함하여 기존 `PackageTargetFallback`을 확장할 수도 있습니다.

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

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
