---
title: "UWP 프로젝트가 있는 NuGet project.json 파일 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 07/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "project.json 파일을 사용하여 UWP(유니버설 Windows 플랫폼) 프로젝트에서 NuGet 종속성을 추적하는 방법을 설명합니다."
keywords: "NuGet 종속성, NuGet 및 UWP, UWP 및 project.json, NuGet project.json 파일"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f1ec086d6404c441ca5ad53028af2265a2344905
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="projectjson-and-uwp"></a>project.json 및 UWP

> [!Important]
> 이 콘텐츠는 더 이상 사용되지 않습니다. 프로젝트는 `packages.config` 또는 PackageReference 형식을 사용해야 합니다.

이 문서에서는 NuGet 3 이상(Visual Studio 2015 이상)의 기능을 사용하는 패키지 구조에 대해 설명합니다. `.nuspec`의 `minClientVersion` 속성은 3.1로 설정하여 여기서 설명하는 기능이 필요하다고 명시하는 데 사용할 수 있습니다.

## <a name="adding-uwp-support-to-an-existing-package"></a>기존 패키지에 UWP 지원 추가

기존 패키지가 있고 UWP 응용 프로그램에 대한 지원을 추가하려는 경우 여기서 설명하는 패키징 형식을 사용할 필요가 없습니다. 여기서 설명하는 기능이 필요하고 NuGet 클라이언트 버전 3 이상으로 업데이트된 클라이언트에서만 작동하도록 하려면 이 형식을 채택하면 됩니다.

## <a name="i-already-target-netcore45"></a>이미 netcore45를 대상으로 하고 있는 경우

이미 `netcore45`를 대상으로 지정하고 있고 여기서 설명하는 기능을 활용할 필요가 없는 경우 아무 작업도 필요하지 않습니다. `netcore45` 패키지는 UWP 응용 프로그램에서 사용할 수 있습니다.

## <a name="i-want-to-take-advantage-of-windows-10-specific-apis"></a>Windows 10 특정 API를 활용하려는 경우

이 경우에는 `uap10.0` 대상 프레임워크 모니커(TFM 또는 TxM)를 패키지에 추가해야 합니다. 패키지에 새 폴더를 만들고 Windows 10에서 작동하도록 컴파일된 어셈블리를 해당 폴더에 추가합니다.

## <a name="i-dont-need-windows-10-specific-apis-but-want-new-net-features-or-dont-have-netcore45-already"></a>Windows 10 특정 API는 필요하지 않지만 새 .NET 기능을 원하거나 netcore45가 아직 없는 경우

이 경우에는 `dotnet` TxM을 패키지에 추가합니다. 다른 TxM과 달리 `dotnet`은 노출 영역 또는 플랫폼을 의미하지 않습니다. 이는 종속성이 작동하는 모든 플랫폼에서 패키지가 작동한다는 것을 나타냅니다. `dotnet` TxM을 사용하여 패키지를 빌드하는 경우 사용자에게 필요한 BCL 패키지(예: `System.Text`, `System.Xml` 등)를 정의해야 하므로 `.nuspec`에 더 많은 TxM 특정 종속성이 있을 수 있습니다. 이러한 종속성이 작동하는 위치는 패키지가 작동하는 위치를 정의합니다.

### <a name="how-do-i-find-out-my-dependencies"></a>내 종속성을 찾으려면 어떻게 할까요?

나열할 종속성을 파악하는 데에는 다음 두 가지 방법이 있습니다.

1. [NuSpec 종속성 생성기](https://github.com/onovotny/ReferenceGenerator) **타사** 도구를 사용합니다. 이 도구는 프로세스를 자동화하고 빌드 시 `.nuspec` 파일을 종속 패키지로 업데이트합니다. [NuSpec.ReferenceGenerator](https://www.nuget.org/packages/NuSpec.ReferenceGenerator/) NuGet 패키지를 통해 사용할 수 있습니다.

1. (어려운 방법) 런타임에 실제로 필요한 어셈블리를 확인하려면 `ILDasm`을 사용하여 `.dll`을 살펴봅니다. 그런 다음 각각에서 제공하는 NuGet 패키지를 결정합니다.

`dotnet` TxM을 지원하는 패키지를 만드는 데 도움이 되는 기능에 대한 자세한 내용은 [`project.json`](project-json.md) 항목을 참조하세요.

> [!Important]
> 패키지가 PCL 프로젝트에서 작동하도록 만들어진 경우 경고 및 잠재적인 호환성 문제를 방지하기 위해 `dotnet` 폴더를 만드는 것이 좋습니다.

## <a name="directory-structure"></a>디렉터리 구조

이 형식을 사용하는 NuGet 패키지에는 다음과 같은 잘 알려진 폴더와 동작이 있습니다.

| 폴더 | 동작 |
| --- | --- |
| 빌드 | 프로젝트에 다르게 통합되어 있지만 그렇지 않은 경우 변경되지 않은 MSBuild targets 및 props 파일을 포함합니다. |
| 도구 | `install.ps1` 및 `uninstall.ps1`은 실행되지 않습니다. `init.ps1`은 항상 있는 그대로 작동합니다. |
| 콘텐츠 | 사용자의 프로젝트에 자동으로 복사되지 않습니다. 프로젝트의 콘텐츠 포함에 대한 지원은 이후 릴리스에 예정되어 있습니다. |
| Lib | `lib`는 많은 패키지에 대해 NuGet 2.x에서 작동하는 것과 동일한 방식으로 작동하지만, 패키지를 사용할 때 패키지 내부에서 사용할 수 있는 이름에 대한 확장된 옵션 및 올바른 하위 폴더를 선택하기 위한 더 나은 논리를 사용할 수 있습니다. 그러나 `ref`와 함께 사용하는 경우 `lib` 폴더에는 `ref` 폴더의 어셈블리에서 정의한 노출 영역을 구현하는 어셈블리가 포함됩니다. |
| Ref | `ref`는 컴파일할 응용 프로그램에 대한 공용 노출 영역(공용 형식 및 메서드)을 정의하는 .NET 어셈블리가 포함되는 선택적 폴더입니다. 이 폴더에 있는 어셈블리는 구현이 없어도 컴파일러에 대한 노출 영역을 전적으로 정의하는 데 사용됩니다. 패키지에 `ref` 폴더가 없으면 `lib`는 참조 어셈블리와 구현 어셈블리입니다. |
| runtimes | `runtimes`는 OS 특정 코드(예: CPU 아키텍처 및 OS 특정 이진 파일 또는 플랫폼에 종속된 이진 파일)가 포함된 선택적 폴더입니다. |

## <a name="msbuild-targets-and-props-files-in-packages"></a>패키지의 MSBuild targets 및 props 파일

NuGet 패키지에는 패키지가 설치된 MSBuild 프로젝트에 가져오는 `.targets` 및 `.props` 파일이 포함될 수 있습니다. NuGet 2.x에서는 `<Import>` 문을 `.csproj` 파일에 삽입하여 수행했지만, NuGet 3.0에서는 특정 "프로젝트에 설치" 작업이 없습니다. 대신 패키지 복원 프로세스는 두 파일, `[projectname].nuget.props`과 `[projectname].NuGet.targets`를 씁니다.

MSBuild는 이러한 두 파일을 찾고 프로젝트 빌드 프로세스의 시작과 끝 무렵에 자동으로 해당 파일을 가져옵니다. 이는 NuGet 2.x와 매우 비슷한 동작을 제공하지만, 주요 차이점 중 하나는 *이 경우 targets/props 파일의 순서가 보장되지 않는다*는 것입니다. 그러나 MSBuild는 `<Target>` 정의의 `BeforeTargets` 및 `AfterTargets` 특성을 통해 대상의 순서를 지정하는 방법을 제공합니다([Target 요소(MSBuild)](/visualstudio/msbuild/target-element-msbuild) 참조).

## <a name="lib-and-ref"></a>Lib 및 Ref

NuGet v3에서는 `lib` 폴더의 동작이 크게 변경되지 않았습니다. 그러나 모든 어셈블리는 TxM이라는 하위 폴더 내에 있어야 하며 더 이상 `lib` 폴더 바로 아래에 배치할 수 없습니다. TxM은 패키지에 지정된 특정 자산이 작동해야 하는 플랫폼의 이름입니다. 이러한 이름은 논리적으로 TFM(Target Framework Monikers)의 확장입니다. 예를 들어 `net45`, `net46`, `netcore50` 및 `dnxcore50`는 모두 TxM의 예입니다([대상 프레임워크](../reference/target-frameworks.md) 참조). TxM은 다른 플랫폼 특정 노출 영역뿐만 아니라 프레임워크(TFM)도 참조할 수 있습니다. 예를 들어 UWP TxM(`uap10.0`)은 .NET 노출 영역과 UWP 응용 프로그램에 대한 Windows 노출 영역을 나타냅니다.

lib 구조의 예:

    lib
    ├───net40
    │       MyLibrary.dll
    └───wp81
            MyLibrary.dll

`lib` 폴더에는 런타임에 사용되는 어셈블리가 포함되어 있습니다. 대부분의 패키지에는 각 대상 TxM에 대한 `lib` 아래의 폴더만 있으면 됩니다.

## <a name="ref"></a>Ref

컴파일하는 동안 다른 어셈블리를 사용해야 하는 경우도 있습니다(이 작업은 현재 .NET 참조 어셈블리에서 수행함). 이러한 경우 `ref`("Reference Assemblies(참조 어셈블리)" 약어)라는 최상위 폴더를 사용합니다.

대부분의 패키지 작성자에게는 `ref` 폴더가 필요하지 않습니다. 이 폴더는 컴파일 및 IntelliSense에 일관된 노출 영역을 제공해야 하지만 다른 TxM에 대해 별도의 구현이 필요한 패키지에 유용합니다. 이 폴더에 대한 가장 큰 사용 사례는 NuGet에 대한 .NET Core 제공의 일환으로 생성되는 `System.*` 패키지입니다. 이러한 패키지에는 일관된 참조 어셈블리 집합으로 통합되는 다양한 구현이 있습니다.

`ref` 폴더에 포함된 어셈블리는 컴파일러에 기계적으로 전달되는 참조 어셈블리입니다. csc.exe를 사용한 사용자의 어셈블리는 [C# /reference 옵션](/dotnet/articles/csharp/language-reference/compiler-options/reference-compiler-option) 스위치에 전달할 어셈블리입니다.

`ref` 폴더의 구조는 `lib`와 같습니다. 예를 들어 다음과 같습니다.

    └───MyImageProcessingLib
         ├───lib
         │   ├───net40
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   ├───net451
         │   │       MyImageProcessingLibrary.dll
         │   │
         │   └───win81
         │           MyImageProcessingLibrary.dll
         │
         └───ref
             ├───net40
             │       MyImageProcessingLibrary.dll
             │
             └───portable-net451-win81
                     MyImageProcessingLibrary.dll

이 예에서 `ref` 디렉터리의 어셈블리는 모두 동일합니다.

## <a name="runtimes"></a>runtimes

runtimes 폴더는 일반적으로 운영 체제 및 CPU 아키텍처에서 정의되는 특정 "런타임"에서 실행하는 데 필요한 어셈블리 및 네이티브 라이브러리를 포함합니다. 이러한 런타임은 `win`, `win-x86`, `win7-x86`, `win8-64` 등과 같이 [RID(런타임 식별자)](/dotnet/core/rid-catalog)를 사용하여 식별됩니다.

## <a name="native-light-up"></a>네이티브 폴더에 대한 설명

다음 예에서는 여러 플랫폼에 대해 전적으로 관리되는 구현이 있지만 Windows 8 특정 네이티브 API를 호출할 수 있는 네이티브 도우미를 Windows 8에서 사용하는 패키지를 보여줍니다.

    └───MyLibrary
         ├───lib
         │   └───net40
         │           MyLibrary.dll
         │
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net40
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyNativeLibrary.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net40
                 │           MyLibrary.dll
                 │
                 └───native
                         MyNativeLibrary.dll

위 패키지가 제공되면 다음과 같은 상황이 발생합니다.

- Windows 8이 아닌 경우 `lib/net40/MyLibrary.dll` 어셈블리가 사용됩니다.

- Windows 8인 경우 `runtimes/win8-<architecture>/lib/MyLibrary.dll`이 사용되고 `native/MyNativeHelper.dll`이 빌드 출력에 복사됩니다.

위의 예에서 `lib/net40` 어셈블리는 전적으로 관리되는 코드이지만, runtimes 폴더에 있는 어셈블리는 네이티브 도우미 어셈블리를 호출하여 Windows 8 특정 API를 호출합니다.

단일 `lib` 폴더만 선택되므로 런타임 특정 폴더가 있으면 해당 폴더가 런타임 이외의 특정 `lib`를 통해 선택됩니다. 네이티브 폴더는 추가 항목이며, 존재하는 경우 빌드 출력에 복사됩니다.

## <a name="managed-wrapper"></a>관리되는 래퍼

런타임을 사용하는 또 다른 방법은 전적으로 관리되는 래퍼인 패키지를 네이티브 어셈블리를 통해 제공하는 것입니다. 이 시나리오에서는 다음과 같은 패키지를 만듭니다.

    └───MyLibrary
         └───runtimes
             ├───win8-x64
             │   ├───lib
             │   │   └───net451
             │   │           MyLibrary.dll
             │   │
             │   └───native
             │           MyImplementation.dll
             │
             └───win8-x86
                 ├───lib
                 │   └───net451
                 │           MyLibrary.dll
                 │
                 └───native
                         MyImplementation.dll

이 경우 해당 네이티브 어셈블리에 종속되지 않는 이 패키지의 구현이 없으므로 해당 폴더와 같은 최상위 `lib` 폴더가 없습니다. 두 경우 모두에서 `MyLibrary.dll` 관리되는 어셈블리가 정확히 동일한 경우 최상위 `lib` 폴더에 넣을 수 있습니다. 그러나 win-x86 또는 win-x64가 아닌 플랫폼에 설치되어 있으면, 네이티브 어셈블리의 부족으로 인해 패키지 설치가 실패하지 않으며, 최상위 lib가 사용되지만 네이티브 어셈블리는 복사되지 않습니다.

## <a name="authoring-packages-for-nuget-2-and-nuget-3"></a>NuGet 2 및 NuGet 3 패키지 제작

`packages.config`를 사용하는 프로젝트와 `project.json`을 사용하는 패키지에서 사용할 수 있는 패키지를 만들려는 경우 다음이 적용됩니다.

- Ref 및 runtimes는 NuGet 3에서만 작동하며, NuGet 2에서는 모두 무시됩니다.

- `install.ps1` 또는 `uninstall.ps1`을 사용하여 작동할 수 없습니다. 이러한 파일은 `packages.config`를 사용하면 실행되지만 `project.json`에서는 무시됩니다. 따라서 패키지는 실행하지 않고도 사용할 수 있어야 합니다. `init.ps1`은 NuGet 3에서 계속 실행됩니다.

- Targets 및 Props 설치가 서로 다르므로 패키지가 두 클라이언트 모두에서 예상대로 작동하는지 확인합니다.

- lib의 하위 디렉터리는 NuGet 3에서 TxM이어야 합니다. `lib` 폴더의 루트에 라이브러리를 배치할 수 없습니다.

- Content는 NuGet 3과 함께 자동으로 복사되지 않습니다. 패키지 소비자가 파일을 직접 복사하거나 작업 실행기와 같은 도구를 사용하여 파일의 복사를 자동화할 수 있습니다.

- 원본 및 config 파일 변환은 NuGet 3에서 실행되지 않습니다.

NuGet 2 및 NuGet 3을 지원하는 경우 `minClientVersion`은 패키지가 작동하는 NuGet 2 클라이언트의 가장 낮은 버전이어야 합니다. 기존 패키지의 경우 변경할 필요가 없습니다.