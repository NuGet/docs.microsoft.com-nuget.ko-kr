---
title: NuGet PackageReference 형식(프로젝트 파일의 패키지 참조)
description: NuGet 4.0 이상, VS2017 및 .NET Core 2.0에서 지원되는 프로젝트 파일에 있는 NuGet PackageReference에 대한 세부 정보
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: d4f0177183ee3edf595c4ce10d1f26cbaca5755d
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453574"
---
# <a name="package-references-packagereference-in-project-files"></a>프로젝트 파일의 패키지 참조(PackageReference)

`PackageReference` 노드를 사용하는 패키지 참조는 별도의 `packages.config` 파일이 아닌 프로젝트 파일 내에서 직접 NuGet 종속성을 관리합니다. PackageReference를 사용하면 NuGet의 다른 측면이 영향을 받지 않습니다. 예를 들어 `NuGet.config` 파일의 설정(패키지 소스 포함)은 [NuGet 동작 구성](configuring-nuget-behavior.md)에 설명된 대로 계속 적용됩니다.

또한 PackageReference를 사용하면 MSBuild 조건을 사용하여 대상 프레임워크, 구성, 플랫폼 또는 기타 그룹화당 패키지 참조를 선택할 수 있습니다. 종속성과 콘텐츠 흐름을 세밀하게 제어할 수도 있습니다. (자세한 내용은 [MSBuild 대상으로서의 NuGet pack 및 restore](../reference/msbuild-targets.md)를 참조하세요.)

기본적으로 PackageReference는 Windows 10 빌드 15063(크리에이터스 업데이트) 이상을 대상으로 하는 .NET Core 프로젝트, .NET Standard 프로젝트 및 UWP 프로젝트에 사용됩니다(C++ UWP 프로젝트는 제외). .NET Framework 프로젝트는 PackageReference를 지원하지만 현재 기본값은 `packages.config`입니다. PackageReference를 사용하려면 종속성을 `packages.config`에서 프로젝트 파일로 마이그레이션한 후 packages.config를 제거하세요.

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

위의 예에서 3.6.0은 [패키지 버전 관리](../reference/package-versioning.md#version-ranges-and-wildcards)에 설명된 대로 가장 낮은 버전의 기본 설정으로 >=3.6.0인 버전을 가르킵니다.

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

## <a name="floating-versions"></a>부동 버전

[부동 버전](../consume-packages/dependency-resolution.md#floating-versions)은 `PackageReference`에서 지원됩니다.

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
| 런타임(runtime) | `lib` 및 `runtimes` 폴더의 콘텐츠이며 이러한 어셈블리가 빌드 출력 디렉터리에 복사되는지 여부 제어 |
| contentFiles | `contentfiles` 폴더의 콘텐츠 |
| 빌드 | `build` 폴더의 prop 및 대상 |
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

## <a name="locking-dependencies"></a>종속성 잠금
‘이 기능은 NuGet **4.9** 이상 및 Visual Studio 2017 **15.9 미리 보기 5** 이상에서 사용할 수 있습니다.’

NuGet 복원의 입력은 프로젝트 파일(최상위 또는 직접 종속성)의 패키지 참조 세트이며, 출력은 전이 종속성을 포함한 모든 패키지 종속성의 전체 클로저입니다. 입력 PackageReference 목록이 변경되지 않은 경우 NuGet은 항상 패키지 종속성의 동일한 전체 클로저를 생성합니다. 그러나 이렇게 할 수 없는 몇 가지 경우가 있습니다. 예:

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
응용 프로그램, 실행 파일을 빌드하는 동안 원하는 프로젝트가 종속성 체인의 끝에 있으면 NuGet이 복원 중에 사용할 수 있도록 소스 코드 리포지토리에 잠금 파일을 체크 인합니다.

그러나 프로젝트가 사용자가 제공하지 않는 라이브러리 프로젝트이거나 다른 프로젝트가 사용하는 공통 코드 프로젝트인 경우에는 잠금 파일을 소스 코드의 일부로 체크 인하면 **안 됩니다**. 잠금 파일을 보존해도 문제가 되지 않지만, 공통 코드 프로젝트의 잠긴 패키지 종속성은 이 공통 코드 프로젝트를 사용하는 프로젝트의 복원/빌드 중에 잠금 파일에 나열된 대로 사용되지 않을 수 있습니다.

예:
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
`ProjectA`가 `PackageX` 버전 `2.0.0`에 대한 종속성을 포함하고 `PackageX` 버전 `1.0.0`을 사용하는 `ProjectB`를 참조하는 경우 `ProjectB`의 잠금 파일은 `PackageX` 버전 `1.0.0`에 대한 종속성을 나열합니다. 그러나 `ProjectA`가 빌드되면 해당 잠금 파일에는 `ProjectB`의 잠금 파일에 나열된 `1.0.0`이 **아닌** `PackageX` 버전 **`2.0.0`** 에 대한 종속성이 포함됩니다. 따라서 공통 코드 프로젝트의 잠금 파일에는 이 파일을 사용하는 프로젝트에 대해 확인된 패키지가 거의 언급되지 않습니다.

### <a name="lock-file-extensibility"></a>잠금 파일 확장성
다음 설명과 같이 잠금 파일을 사용하여 다양한 복원 동작을 제어할 수 있습니다.

| 옵션 | MSBuild 해당 옵션 | 
|:---  |:--- |
| `--use-lock-file` | 프로젝트의 잠금 파일 사용을 부트스트랩합니다. 또는 프로젝트 파일에서 `RestorePackagesWithLockFile` 속성을 설정할 수 있습니다. | 
| `--locked-mode` | 복원에 잠금 모드를 사용하도록 설정합니다. 이는 반복 가능한 빌드를 가져오려는 CI/CD 시나리오에서 유용합니다. `RestoreLockedMode` MSBuild 속성을 `true`로 설정할 수도 있습니다. |  
| `--force-evaluate` | 이 옵션은 프로젝트에 정의된 부동 버전의 패키지에 유용합니다. 기본적으로 NuGet 복원은 `--force-evaluate` 옵션으로 복원을 실행하지 않는 한 각 복원에서 패키지 버전을 자동으로 업데이트하지 않습니다. |
| `--lock-file-path` | 프로젝트의 사용자 지정 잠금 파일 위치를 정의합니다. MSBuild 속성 `NuGetLockFilePath`을 설정할 수도 있습니다. 기본적으로 NuGet은 루트 디렉터리에서 `packages.lock.json`을 지원합니다. 같은 디렉터리에 여러 프로젝트가 있는 경우 NuGet은 프로젝트별 잠금 파일 `packages.<project_name>.lock.json`을 지원합니다. |
