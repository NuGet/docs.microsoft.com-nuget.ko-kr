---
title: 프로젝트에서 참조하는 어셈블리 선택
description: 모든 어셈블리를 런타임에 사용할 수 있는 동안 패키지의 어셈블리 하위 집합을 컴파일러에서 사용할 수 있도록 합니다.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b32075c3f2c06c15c07d36602bdabdaee8b9405a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427478"
---
# <a name="select-assemblies-referenced-by-projects"></a>프로젝트에서 참조하는 어셈블리 선택

모든 어셈블리를 런타임에 사용할 수 있는 동안 명시적 어셈블리 참조는 IntelliSense 및 컴파일에 사용되는 어셈블리의 하위 집합을 허용합니다. `PackageReference` 및 `packages.config`는 다르게 작동하며, 결과적으로 패키지 작성자는 두 프로젝트 유형 모두와 호환되도록 패키지를 만들어야 합니다.

> [!Note]
> 명시적 어셈블리 참조는 .NET 어셈블리와 관련이 있습니다. 관리 어셈블리에 의해 P/호출된 네이티브 어셈블리를 배포하는 메서드가 아닙니다.

## <a name="packagereference-support"></a>`PackageReference` 지원

프로젝트가 `PackageReference`가 있는 패키지를 사용하고 패키지에 `ref\<tfm>\` 디렉터리가 포함된 경우, NuGet은 해당 어셈블리를 컴파일 타임 자산으로 분류하고 `lib\<tfm>\` 어셈블리는 런타임 자산으로 분류합니다. `ref\<tfm>\`의 어셈블리는 런타임 시 사용되지 않습니다. 즉, `ref\<tfm>\`의 모든 어셈블리에는 `lib\<tfm>\` 또는 관련 `runtime\` 디렉터리에 일치하는 어셈블리가 있어야 합니다. 그렇지 않으면 런타임 오류가 발생할 수 있습니다. `ref\<tfm>\`의 어셈블리는 런타임에 사용되지 않으므로 패키지 크기를 줄이기 위한 [메타데이터 전용 어셈블리](https://github.com/dotnet/roslyn/blob/master/docs/features/refout.md)일 수 있습니다.

> [!Important]
> 패키지에 nuspec `<references>` 요소(`packages.config`에서 사용됨, 아래 참조)가 있고 `ref\<tfm>\`의 어셈블리가 포함되어 있지 않은 경우, NuGet은 nuspec `<references>` 요소에 나열된 어셈블리를 컴파일 및 런타임 자산으로 보급합니다. 이는 참조된 어셈블리가 `lib\<tfm>\` 디렉터리에 다른 어셈블리를 로드해야 하는 경우 런타임 예외가 있음을 의미합니다.

> [!Note]
> 패키지에 `runtime\` 디렉터리가 포함된 경우 NuGet은 `lib\` 디렉터리의 자산을 사용하지 않을 수 있습니다.

## <a name="packagesconfig-support"></a>`packages.config` 지원

`packages.config`를 사용하여 NuGet 패키지를 관리하는 프로젝트는 일반적으로 `lib\<tfm>\` 디렉터리의 모든 어셈블리에 참조를 추가합니다. `ref\` 디렉터리는 `PackageReference`를 지원하기 위해 추가되었으므로 `packages.config` 사용 시 고려되지 않습니다. `packages.config`를 사용하는 프로젝트에 대해 참조되는 어셈블리를 명시적으로 설정하려면 패키지에서 [nuspec 파일의 `<references>` 요소](../reference/nuspec.md#explicit-assembly-references)를 사용해야 합니다. 다음은 그 예입니다.

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> `packages.config` 프로젝트는 [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/master/documentation/wiki/ResolveAssemblyReference.md)라는 프로세스를 사용하여 어셈블리를 `bin\<configuration>\` 출력 디렉터리에 복사합니다. 프로젝트의 어셈블리가 복사된 다음, 빌드 시스템이 참조된 어셈블리에 대한 어셈블리 매니페스트를 살펴본 후, 해당 어셈블리를 복사하고 모든 어셈블리에 대해 재귀적으로 반복합니다. 즉, `lib\<tfm>\` 디렉터리에 있는 어셈블리가 다른 어셈블리의 매니페스트에 종속성으로 나열되지 않은 경우(`Assembly.Load`, MEF 또는 다른 종속성 주입 프레임워크를 사용하여 런타임 시 어셈블리가 로드된 경우), `bin\<configuration>\`에 있더라도 프로젝트의 `bin\<tfm>\` 출력 디렉터리에 복사되지 않을 수 있습니다.

## <a name="example"></a>예제

내 패키지에는 .NET Framework 4.7.2를 대상으로 하는 세 개의 어셈블리 `MyLib.dll`, `MyHelpers.dll` 및 `MyUtilities.dll`이 포함됩니다. `MyUtilities.dll`에는 다른 두 어셈블리에서만 사용할 수 있는 클래스가 포함되어 있으므로 IntelliSense에서 또는 패키지를 사용하여 프로젝트를 컴파일할 때 해당 클래스를 사용할 수 없도록 합니다. 내 `nuspec` 파일에 다음 XML 요소가 포함되어 있어야 합니다.

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

패키지의 파일은 다음과 같습니다.

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
