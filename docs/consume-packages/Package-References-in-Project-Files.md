---
title: NuGet PackageReference 형식(프로젝트 파일의 패키지 참조) | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet 4.0 이상, VS2017 및 .NET Core 2.0에서 지원되는 프로젝트 파일에 있는 NuGet PackageReference에 대한 세부 정보
keywords: NuGet 패키지 종속성, 패키지 참조, 프로젝트 파일, PackageReference, packages.config, VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 7844ace0565b2e70f8f68e6e61548f0f28171689
ms.sourcegitcommit: 5b223c5814799caa6309e95792a2d338df692778
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="package-references-packagereference-in-project-files"></a>프로젝트 파일의 패키지 참조(PackageReference)

`PackageReference` 노드를 사용하는 패키지 참조는 별도의 `packages.config` 파일이 아닌 프로젝트 파일 내에서 직접 NuGet 종속성을 관리합니다. PackageReference를 사용하면 NuGet의 다른 측면이 영향을 받지 않습니다. 예를 들어 `NuGet.Config` 파일의 설정(패키지 소스 포함)은 [NuGet 동작 구성](configuring-nuget-behavior.md)에 설명된 대로 계속 적용됩니다.

또한 PackageReference를 사용하면 MSBuild 조건을 사용하여 대상 프레임워크, 구성, 플랫폼 또는 기타 그룹화당 패키지 참조를 선택할 수 있습니다. 종속성과 콘텐츠 흐름을 세밀하게 제어할 수도 있습니다. (자세한 내용은 [MSBuild 대상으로서의 NuGet pack 및 restore](../reference/msbuild-targets.md)를 참조하세요.)

기본적으로 PackageReference는 Windows 10 빌드 15063(크리에이터스 업데이트) 이상을 대상으로 하는 .NET Core 프로젝트, .NET Standard 프로젝트 및 UWP 프로젝트에 사용됩니다(C++ UWP 프로젝트는 제외). .NET 전체 프레임워크 프로젝트는 PackageReference를 지원하지만 현재 기본값은 `packages.config`입니다. PackageReference를 사용하려면 종속성을 `packages.config`에서 프로젝트 파일로 마이그레이션한 후 packages.config를 제거하세요.

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
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

이 프로젝트를 사용하여 빌드한 패키지는 Newtonsoft.json이 `net452` 대상에서만 종속성으로 포함되어 있다고 표시합니다.

![VS2017에서 PackageReference에 대한 조건을 적용한 결과](media/PackageReference-Condition.png)

조건은 `ItemGroup` 수준에도 적용될 수 있고 모든 자식 `PackageReference` 요소에 적용됩니다.

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
