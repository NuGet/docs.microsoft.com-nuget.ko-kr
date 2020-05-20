---
title: NuGet PackageReference 형식(프로젝트 파일의 패키지 참조)
description: NuGet 4.0 이상, VS2017 및 .NET Core 2.0에서 지원되는 프로젝트 파일에 있는 NuGet PackageReference에 대한 세부 정보
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428506"
---
# <a name="package-references-packagereference-in-project-files"></a>프로젝트 파일의 패키지 참조(PackageReference)

`PackageReference` 노드를 사용하는 패키지 참조는 별도의 `packages.config` 파일이 아닌 프로젝트 파일 내에서 직접 NuGet 종속성을 관리합니다. PackageReference를 사용하면 NuGet의 다른 측면이 영향을 받지 않습니다. 예를 들어 `NuGet.config` 파일의 설정(패키지 소스 포함)은 [일반적인 NuGet 구성](configuring-nuget-behavior.md)에 설명된 대로 계속 적용됩니다.

또한 PackageReference를 사용하면 MSBuild 조건을 사용하여 대상 프레임워크 또는 기타 그룹화당 패키지 참조를 선택할 수 있습니다. 종속성과 콘텐츠 흐름을 세밀하게 제어할 수도 있습니다. (자세한 내용은 [MSBuild 대상으로서의 NuGet pack 및 restore](../reference/msbuild-targets.md)를 참조하세요.)

## <a name="project-type-support"></a>프로젝트 형식 지원

기본적으로 PackageReference는 Windows 10 빌드 15063(크리에이터스 업데이트) 이상을 대상으로 하는 .NET Core 프로젝트, .NET Standard 프로젝트 및 UWP 프로젝트에 사용됩니다(C++ UWP 프로젝트는 제외). .NET Framework 프로젝트는 PackageReference를 지원하지만 현재 기본값은 `packages.config`입니다. PackageReference를 사용하려면 종속성을 `packages.config`에서 프로젝트 파일로 [마이그레이션](../consume-packages/migrate-packages-config-to-package-reference.md)한 후 packages.config를 제거하세요.

전체 .NET Framework를 대상으로 하는 ASP.NET 앱은 PackageReference에 대한 [제한적 지원](https://github.com/NuGet/Home/issues/5877)만 포함합니다. C++ 및 JavaScript 프로젝트 형식은 지원되지 않습니다.

## <a name="adding-a-packagereference"></a>PackageReference 추가

다음 구문을 사용하여 프로젝트 파일에서 종속성을 추가합니다.

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>종속성 버전 제어

패키지의 버전을 지정하는 규칙은 `packages.config`를 사용하는 경우와 동일합니다.

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

위의 예에서 3.6.0은 [패키지 버전 관리](../concepts/package-versioning.md#version-ranges)에 설명된 대로 가장 낮은 버전의 기본 설정으로 >=3.6.0인 버전을 가르킵니다.

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>PackageReferences가 없는 프로젝트에 대해 PackageReference 사용

고급: 프로젝트에 설치된 패키지가 없지만(프로젝트 파일에 PackageReferences가 없고 packages.config 파일이 없음) 프로젝트를 PackageReference 스타일로 복원하려는 경우 프로젝트 속성 RestoreProjectStyle을 프로젝트 파일의 PackageReference로 설정할 수 있습니다.

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

PackageReference 스타일인 프로젝트(기존 csproj 또는 SDK 스타일 프로젝트)를 참조하는 경우에 유용할 수 있습니다. 이렇게 하면 해당 프로젝트가 참조하는 패키지는 프로젝트에서 "전이적으로" 참조합니다.

## <a name="packagereference-and-sources"></a>PackageReference 및 소스

PackageReference 프로젝트에서 전이 종속성 버전은 복원 시간에 확인됩니다. 따라서 PackageReference 프로젝트에서 모든 복원에 대해 모든 소스를 사용할 수 있어야 합니다. 

## <a name="floating-versions"></a>부동 버전

[부동 버전](../concepts/dependency-resolution.md#floating-versions)은 `PackageReference`에서 지원됩니다.

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>종속성 자산 제어

종속성을 개발 도구로서 전적으로 사용하면 패키지를 사용하는 프로젝트에 노출하지 않을 수도 있습니다. 이 시나리오에서는 `PrivateAssets` 메타데이터를 사용하여 이 동작을 제어할 수 있습니다.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

다음 메타데이터 태그는 종속성 자산을 제어합니다.

| 태그 | 설명 | 기본값 |
| --- | --- | --- |
| IncludeAssets | 이러한 자산을 사용합니다. | 모두 |
| ExcludeAssets | 이러한 자산을 사용하지 않습니다. | 없음 |
| PrivateAssets | 이러한 자산을 사용하지만 부모 프로젝트로 흐르지 않습니다. | contentfiles;analyzers;build |

이러한 태그에 허용 가능한 값은 단독으로 표시해야 하는 `all` 및 `none`를 제외하고 세미콜론으로 구분된 값이 여러 개인 다음과 같습니다.

| 값 | 설명 |
| --- | ---
| compile | `lib` 폴더의 콘텐츠이며 프로젝트에서 폴더 내의 어셈블리를 컴파일할 수 있는지 여부 제어 |
| 런타임 | `lib` 및 `runtimes` 폴더의 콘텐츠이며 이러한 어셈블리가 빌드 출력 디렉터리에 복사되는지 여부 제어 |
| contentFiles | `contentfiles` 폴더의 콘텐츠 |
| 빌드 | `build` 폴더의 `.props` 및 `.targets` |
| buildMultitargeting | *(4.0)* 프레임워크 간 타기팅을 위한 `buildMultitargeting` 폴더의 `.props` 및 `.targets` |
| buildTransitive | ‘(5.0 이상)’ 사용하는 프로젝트로 전이적으로 흐르는 자산을 위한 `buildTransitive` 폴더의 `.props` 및 `.targets`  [기능](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) 페이지를 참조하세요. |
| 분석기 | .NET 분석기 |
| native | `native` 폴더의 콘텐츠 |
| 없음 | 위의 항목을 사용하지 않습니다. |
| 모두 | 위 모두 해당(`none` 제외) |

다음 예제에서는 패키지의 콘텐츠 파일을 제외한 모든 항목을 프로젝트에서 사용할 수 있으며 콘텐츠 파일과 분석기를 제외한 모든 항목이 부모 프로젝트로 전달됩니다.

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

`build`가 `PrivateAssets`에 포함되지 않기 때문에 대상 및 props은 부모 프로젝트로 전달되게 *됩니다*. 예를 들어 위의 참조가 AppLogger라는 NuGet 패키지를 빌드하는 프로젝트에서 사용됩니다. 프로젝트가 AppLogger를 사용할 수 있는 것처럼 AppLogger는 `Contoso.Utility.UsefulStuff`의 대상 및 props을 사용할 수 있습니다.

> [!NOTE]
> `.nuspec` 파일에서 `developmentDependency`가 `true`로 설정되면 패키지가 개발 전용 종속성으로 표시되므로 해당 패키지가 다른 패키지의 종속성으로 포함되지 않습니다. PackageReference *(NuGet 4.8 이상)* 를 사용하는 경우 이 플래그는 컴파일 시간 자산을 컴파일에서 제외한다는 의미이기도 합니다. 자세한 내용은 [PackageReference에 대한 DevelopmentDependency 지원](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)을 참조하세요.

## <a name="adding-a-packagereference-condition"></a>PackageReference 조건 추가

조건이 모든 MSBuild 변수 또는 대상이나 props 파일에 정의된 변수를 사용할 수 있는 경우에 패키지가 포함되어 있는지를 제어하는 조건을 사용할 수 있습니다. 그러나 현재는 `TargetFramework` 변수만이 지원됩니다.

예를 들어 `net452`뿐만 아니라 `netstandard1.4`를 대상으로 지정했지만 `net452`에만 적용할 수 있는 종속성이 있다고 가정합니다. 이 경우에 불필요한 해당 종속성을 추가하는 패키지를 사용하는 `netstandard1.4` 프로젝트를 사용하지 않으려고 합니다. 이를 방지하려면 다음과 같이 `PackageReference`에 대한 조건을 지정합니다.

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

이 프로젝트를 사용하여 빌드한 패키지는 Newtonsoft.Json이 `net452` 대상에서만 종속성으로 포함되어 있다고 표시합니다.

![VS2017에서 PackageReference에 대한 조건을 적용한 결과](media/PackageReference-Condition.png)

조건은 `ItemGroup` 수준에도 적용될 수 있고 모든 자식 `PackageReference` 요소에 적용됩니다.

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a>GeneratePathProperty

이 기능은 NuGet **5.0** 이상 및 Visual Studio 2019 **16.0** 이상에서 사용할 수 있습니다.

경우에 따라 MSBuild 대상의 패키지 파일을 참조하는 것이 좋습니다.
`packages.config` 기반 프로젝트에서 패키지는 프로젝트 파일의 상대 폴더에 설치됩니다. 그러나 PackageReference에서는 머신마다 다를 수 있는 *global-packages* 폴더의 패키지가 [사용](../concepts/package-installation-process.md)됩니다.

이 문제를 해결하기 위해 NuGet은 사용할 패키지의 위치를 가리키는 속성을 도입했습니다.

예:

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

또한 NuGet은 tools 폴더를 포함하는 패키지의 속성을 자동으로 생성합니다.

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

MSBuild 속성과 패키지 ID에는 동일한 제한이 없기 때문에 패키지 ID를 MSBuild 이름으로 변경하고 `Pkg` 단어를 앞에 추가해야 합니다.
생성된 속성의 정확한 이름을 확인하려면 생성된 [nuget.exe](../reference/msbuild-targets.md#restore-outputs) 파일을 확인합니다.

## <a name="nuget-warnings-and-errors"></a>NuGet 경고 및 오류

‘이 기능은 NuGet **4.3** 이상 및 Visual Studio 2017 **15.3** 이상에서 사용할 수 있습니다.’

많은 패키지 및 복원 시나리오에서는 모든 NuGet 경고 및 오류가 코딩되고 `NU****`로 시작합니다. 모든 NuGet 경고 및 오류는 [참조](../reference/errors-and-warnings.md) 문서에 나와 있습니다.

NuGet은 다음과 같은 경고 속성을 확인합니다.

- `TreatWarningsAsErrors` - 모든 경고를 오류로 처리
- `WarningsAsErrors` - 특정 경고를 오류로 처리
- `NoWarn` - 프로젝트 수준 또는 패키지 수준에서 특정 경고 숨기기

예:

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a>NuGet 경고 표시 안 함

패키지 및 복원 작업 중에 발생하는 모든 NuGet 경고를 해결하는 것이 좋지만, 특정 상황에서는 경고를 표시하지 않을 수도 있습니다.
프로젝트 수준에서 경고를 표시하지 않으려면 다음을 수행합니다.

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

경고가 그래프의 특정 패키지에만 적용되는 경우도 있습니다. PackageReference 항목에 `NoWarn`을 추가하면 보다 선택적으로 경고 표시를 해제할 수 있습니다. 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a>Visual Studio에서 NuGet 패키지 경고 표시 안 함

Visual Studio에서 IDE를 통해 [경고 표시를 해제](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
)할 수도 있습니다.

## <a name="locking-dependencies"></a>종속성 잠금

이 기능은 NuGet **4.9** 이상 및 Visual Studio 2017 **15.9** 이상에서 사용할 수 있습니다.

NuGet 복원의 입력은 프로젝트 파일(최상위 또는 직접 종속성)의 패키지 참조 세트이며, 출력은 전이 종속성을 포함한 모든 패키지 종속성의 전체 클로저입니다. 입력 PackageReference 목록이 변경되지 않은 경우 NuGet은 항상 패키지 종속성의 동일한 전체 클로저를 생성합니다. 그러나 이렇게 할 수 없는 몇 가지 경우가 있습니다. 예를 들어:

* `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` 같은 부동 버전을 사용하는 경우. 여기서 의도는 패키지의 모든 복원에서 최신 버전으로 이동하는 것이지만, 사용자가 그래프를 특정 최신 버전으로 잠그고 명시적 제스처에 따라 이후 버전(사용 가능한 경우)으로 이동하는 경우가 있습니다.
* PackageReference 버전 요구 사항과 일치하는 패키지의 최신 버전이 게시됩니다. 예: 

  * 1일: `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`을 지정하지만 NuGet 리포지토리에서 사용 가능한 버전이 4.1.0, 4.2.0, 4.3.0인 경우. 이 경우 NuGet은 4.1.0(가장 가까운 최소 버전)으로 확인합니다.

  * 2일: 버전 4.0.0이 게시됩니다. NuGet은 이제 정확한 일치 항목을 찾고 4.0.0으로 확인을 시작합니다.

* 지정된 패키지 버전이 리포지토리에서 제거됩니다. nuget.org에서는 패키지 삭제를 허용하지 않지만 일부 패키지 리포지토리에는 이 제약 조건이 없습니다. 따라서 NuGet은 삭제된 버전으로 확인할 수 없는 경우 가장 일치하는 항목을 찾습니다.

### <a name="enabling-lock-file"></a>잠금 파일 사용

패키지 종속성의 전체 클로저를 유지하기 위해 프로젝트의 MSBuild 속성 `RestorePackagesWithLockFile`을 설정하여 잠금 파일 기능을 옵트인할 수 있습니다.

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

이 속성을 설정하면 NuGet 복원은 모든 패키지 종속성을 나열하는 프로젝트 루트 디렉터리에 잠금 파일인 `packages.lock.json` 파일을 생성합니다. 

> [!Note]
> 프로젝트의 루트 디렉터리에 `packages.lock.json` 파일이 있으면 `RestorePackagesWithLockFile` 속성이 설정되지 않은 경우에도 복원에는 항상 잠금 파일이 사용됩니다. 따라서 이 기능을 옵트인하는 또 다른 방법은 프로젝트의 루트 디렉터리에 더미 공백 `packages.lock.json` 파일을 만드는 것입니다.

### <a name="restore-behavior-with-lock-file"></a>잠금 파일을 사용한 `restore` 동작
프로젝트에 대한 잠금 파일이 있으면 NuGet은 이 잠금 파일을 사용하여 `restore`를 실행합니다. NuGet은 프로젝트 파일(또는 종속 프로젝트 파일)에 언급된 패키지 종속성에 변경 내용이 있는지 빠르게 확인하고, 변경 내용이 없으면 잠금 파일에 언급된 패키지를 복원합니다. 패키지 종속성은 다시 평가되지 않습니다.

NuGet은 프로젝트 파일에 언급된 정의된 종속성에서 변경을 발견하면 패키지 그래프를 다시 평가하고 잠금 파일을 업데이트하여 프로젝트의 새 패키지 클로저를 반영합니다.

CI/CD 및 기타 시나리오의 경우 패키지 종속성을 즉시 변경하지 않으려면 `lockedmode`를 `true`로 설정하면 됩니다.

dotnet.exe의 경우 다음을 실행합니다.

```
> dotnet.exe restore --locked-mode
```

msbuild.exe의 경우 다음을 실행합니다.

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

프로젝트 파일에서 이 조건부 MSBuild 속성을 설정할 수도 있습니다.

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

잠김 모드가 `true`인 경우 잠금 파일에 나열된 정확한 패키지가 복원되거나, 잠금 파일이 생성된 후 프로젝트의 정의된 패키지 종속성을 업데이트한 경우 복원에 실패합니다.

### <a name="make-lock-file-part-of-your-source-repository"></a>소스 리포지토리의 잠금 파일 파트 만들기
애플리케이션, 실행 파일을 빌드하는 동안 원하는 프로젝트가 종속성 체인의 시작 부분에 있으면 NuGet이 복원 중에 사용할 수 있도록 소스 코드 리포지토리에 잠금 파일을 체크 인합니다.

그러나 프로젝트가 사용자가 제공하지 않는 라이브러리 프로젝트이거나 다른 프로젝트가 사용하는 공통 코드 프로젝트인 경우에는 잠금 파일을 소스 코드의 일부로 체크 인하면 **안 됩니다**. 잠금 파일을 보존해도 문제가 되지 않지만, 공통 코드 프로젝트의 잠긴 패키지 종속성은 이 공통 코드 프로젝트를 사용하는 프로젝트의 복원/빌드 중에 잠금 파일에 나열된 대로 사용되지 않을 수 있습니다.

예:

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

`ProjectA`가 `PackageX` 버전 `2.0.0`에 대한 종속성을 포함하고 `PackageX` 버전 `1.0.0`을 사용하는 `ProjectB`를 참조하는 경우 `ProjectB`의 잠금 파일은 `PackageX` 버전 `1.0.0`에 대한 종속성을 나열합니다. 그러나 `ProjectA`를 빌드하면 해당 잠금 파일에는 `ProjectB`의 잠금 파일에 나열된 대로 `PackageX` 버전 `1.0.0`이 **아닌** **`2.0.0`** 에 대한 종속성이 포함됩니다. 따라서 공통 코드 프로젝트의 잠금 파일에는 이 파일을 사용하는 프로젝트에 대해 확인된 패키지가 거의 언급되지 않습니다.

### <a name="lock-file-extensibility"></a>잠금 파일 확장성

다음 설명과 같이 잠금 파일을 사용하여 다양한 복원 동작을 제어할 수 있습니다.

| NuGet.exe 옵션 | dotnet 옵션 | MSBuild 해당 옵션 | 설명 |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | RestorePackagesWithLockFile | 잠금 파일을 사용합니다. |
| `-LockedMode` | `--locked-mode` | RestoreLockedMode | 복원에 잠금 모드를 사용하도록 설정합니다. 이는 반복 가능한 빌드를 원하는 CI/CD 시나리오에서 유용합니다.|   
| `-ForceEvaluate` | `--force-evaluate` | RestoreForceEvaluate | 이 옵션은 프로젝트에 정의된 부동 버전의 패키지에 유용합니다. 기본적으로 NuGet 복원은 이 옵션으로 복원을 실행하지 않는 한 각 복원에서 패키지 버전을 자동으로 업데이트하지 않습니다. |
| `-LockFilePath` | `--lock-file-path` | NuGetLockFilePath | 프로젝트의 사용자 지정 잠금 파일 위치를 정의합니다. 기본적으로 NuGet은 루트 디렉터리에서 `packages.lock.json`을 지원합니다. 같은 디렉터리에 여러 프로젝트가 있는 경우 NuGet은 프로젝트별 잠금 파일 `packages.<project_name>.lock.json`을 지원합니다. |
