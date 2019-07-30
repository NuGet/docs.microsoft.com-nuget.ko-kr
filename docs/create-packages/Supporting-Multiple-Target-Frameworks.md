---
title: NuGet 패키지의 멀티 타기팅
description: 단일 NuGet 패키지 내에서 여러 .NET Framework 버전을 대상으로 하는 다양한 방법에 대한 설명입니다.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: d12b12c4670f5dcb4c1e7e475d77926bd5d3935b
ms.sourcegitcommit: 0f5363353f9dc1c3d68e7718f51b7ff92bb35e21
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342507"
---
# <a name="support-multiple-net-versions"></a>여러 .NET 버전 지원

많은 라이브러리는 특정 버전의 .NET Framework를 대상으로 지정합니다. 예를 들어 UWP에 관련된 한 버전의 라이브러리 및 .NET Framework 4.6에서 기능을 활용하는 다른 버전의 라이브러리가 있을 수 있습니다. 이를 위해 NuGet은 동일한 라이브러리의 여러 버전을 단일 패키지에 배치하는 것을 지원합니다.

이 문서에서는 패키지 또는 어셈블리를 빌드하는 방법에 관계없이 NuGet 패키지의 레이아웃에 대해 설명합니다. 즉, 이 레이아웃은 여러 비 SDK 스타일 *.csproj* 파일, 사용자 지정 *.nuspec* 또는 단일 다중 대상 SDK 스타일 *.csproj* 중 어떤 파일을 사용하든 동일합니다. SDK 스타일 프로젝트의 경우 NuGet [pack targets](../reference/msbuild-targets.md)는 패키지 레이아웃 방식을 알고, 어셈블리를 올바른 lib 폴더에 배치한 후 각 TFM(대상 프레임워크)에 대해 종속성 그룹을 만드는 과정을 자동화합니다. 자세한 지침은 [프로젝트 파일에서 여러 .NET Framework 버전 지원](multiple-target-frameworks-project-file.md)을 참조하세요.

[패키지 만들기](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)에 설명된 규칙 기반 작업 디렉터리 방법을 사용하는 경우 이 문서에 설명된 대로 패키지 레이아웃을 수동으로 지정해야 합니다. SDK 스타일 프로젝트의 경우 자동화된 방법을 권장하지만 이 문서에 설명된 대로 패키지 레이아웃을 수동으로 지정하도록 선택할 수도 있습니다.

## <a name="framework-version-folder-structure"></a>프레임워크 버전 폴더 구조

하나의 라이브러리 버전을 포함하거나 여러 프레임워크를 대상으로 하는 패키지를 빌드하는 경우 항상 다음 규칙으로 다른 대/소문자 구분 프레임워크 이름을 사용하여 `lib` 아래에서 하위 폴더를 만듭니다.

    lib\{framework name}[{version}]

지원되는 이름의 전체 목록은 [대상 프레임워크 참조](../reference/target-frameworks.md#supported-frameworks)를 참조하세요.

프레임워크에 관련되지 않는 버전의 라이브러리를 포함하거나 루트 `lib` 폴더에 배치하지 않아야 합니다. (이 기능은 `packages.config`에만 지원됩니다.) 그렇게 하면 라이브러리를 모든 대상 프레임워크와 호환되도록 만들고 어디에나 설치할 수 있습니다. 따라서 예기치 않은 런타임 오류가 발생할 가능성이 큽니다. 루트 폴더(예: `lib\abc.dll`) 또는 하위 폴더(예: `lib\abc\abc.dll`)에 어셈블리를 추가하는 작업은 사용되지 않으며 PackagesReference 형식을 사용할 때 무시됩니다.

예를 들어 다음 폴더 구조는 프레임워크에 관련된 4개 버전의 어셈블리를 지원합니다.

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

패키지를 빌드할 때 이러한 파일 중 일부를 쉽게 포함하려면 `.nuspec`의 `<files>` 섹션에서 재귀 `**` 와일드 카드를 사용합니다.

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>아키텍처 관련 폴더

아키텍처 관련 어셈블리, 즉, ARM, x86 및 x64를 대상으로 하는 별도 어셈블리가 있는 경우 `{platform}-{architecture}\lib\{framework}` 또는 `{platform}-{architecture}\native`라는 하위 폴더 내에서 `runtimes`라는 폴더에 배치해야 합니다. 예를 들어 다음 폴더 구조는 Windows 10 및 `uap10.0` 프레임워크를 대상으로 하는 네이티브 및 관리 DLL을 모두 수용합니다.

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

이러한 어셈블리는 런타임에만 사용할 수 있으므로 해당 컴파일 시간 어셈블리도 제공하려면 `AnyCPU` 어셈블리를 `/ref{tfm}` 폴더에 포함합니다. 

NuGet은 항상 하나의 폴더에서 이러한 컴파일 또는 런타임 자산을 선택하므로, `/ref`의 호환 가능한 자산이 있는 경우 컴파일 시간 어셈블리를 추가하기 위해 `/lib`가 무시됩니다. 마찬가지로 `/runtime`의 일부 호환 가능한 자산이 있는 경우에도 런타임을 위해 `/lib`가 무시됩니다.

`.nuspec` 매니페스트에서 이러한 파일을 참조하는 예제는 [UWP 패키지 만들기](../guides/create-uwp-packages.md)를 참조하세요.

또한 [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)(NuGet으로 Windows 스토어 앱 구성 요소 압축)을 참조하세요.

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>프로젝트에서 어셈블리 버전 및 대상 프레임워크 일치

NuGet이 여러 어셈블리 버전을 포함하는 패키지를 설치하면 프로젝트의 대상 프레임워크와 어셈블리의 프레임워크 이름을 일치하도록 합니다.

일치 항목이 없으면 NuGet은 사용 가능한 경우 프로젝트의 대상 프레임워크 이전에 릴리스된 가장 높은 버전의 어셈블리를 복사합니다. 호환 가능한 어셈블리를 찾는 경우 NuGet은 적절한 오류 메시지를 반환합니다.

예를 들어 패키지에 다음과 같은 폴더 구조가 있다고 가정합니다.

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

.NET Framework 4.6을 대상으로 하는 프로젝트에서 이 패키지를 설치하는 경우 NuGet은 `net45` 폴더에 어셈블리를 설치합니다. 4.6 이전에 릴리스된 사용 가능한 가장 높은 버전이기 때문입니다.

반면 프로젝트가 .NET Framework 4.6.1을 대상으로 하는 경우 NuGet은 `net461` 폴더에 어셈블리를 설치합니다.

프로젝트가 .NET framework 4.0 이전을 대상으로 하는 경우 NuGet은 호환 가능한 어셈블리를 찾을 수 없는 경우에 적절한 오류 메시지를 throw합니다.

## <a name="grouping-assemblies-by-framework-version"></a>프레임워크 버전에 따라 어셈블리 그룹화

NuGet은 패키지의 단일 라이브러리 폴더에서 어셈블리를 복사합니다. 예를 들어 패키지에 다음과 같은 폴더 구조가 있다고 가정합니다.

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

.NET Framework 4.5를 대상으로 하는 프로젝트에서 패키지를 설치할 때 `MyAssembly.dll`(v2.0)이 설치된 유일한 어셈블리입니다. `MyAssembly.Core.dll`(v1.0)이 `net45` 폴더에 나열되지 않기 때문에 설치되지 않습니다. `MyAssembly.Core.dll`이 2.0 버전의 `MyAssembly.dll`에 병합되기 때문에 NuGet은 이런 방식으로 작동합니다.

`MyAssembly.Core.dll`을 .NET Framework 4.5에 설치하려는 경우 복사본을 `net45` 폴더에 배치합니다.

## <a name="grouping-assemblies-by-framework-profile"></a>프레임워크 프로필에 따라 어셈블리 그룹화

또한 NuGet은 대시와 프로필 이름을 폴더의 끝에 추가하여 특정 프레임워크 프로필을 대상으로 하도록 지원합니다.

    lib\{framework name}-{profile}

지원되는 프로필은 다음과 같습니다.

- `client`: 클라이언트 프로필
- `full`: 전체 프로필
- `wp`: Windows Phone
- `cf`: Compact Framework

## <a name="determining-which-nuget-target-to-use"></a>사용할 NuGet 대상 결정

이식 가능한 클래스 라이브러리를 대상으로 하는 라이브러리를 패키지할 때 특히 PCL의 하위 집합만 대상으로 하는 경우 폴더 이름 및 `.nuspec` 파일에서 사용해야 하는 NuGet 대상을 결정하는 작업이 까다로울 수 있습니다. 다음 외부 리소스는 이런 기능에 도움이 됩니다.

- [.NET의 프레임워크 프로필](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html)(stephencleary.com)
- [이식 가능한 클래스 라이브러리 프로필](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview)(plnkr.co): PCL 프로필 및 동등한 해당 NuGet 대상을 열거하는 표
- [이식 가능한 클래스 라이브러리 프로필 도구](https://github.com/StephenCleary/PortableLibraryProfiles)(github.com): 시스템에서 사용할 수 있는 PCL 프로필을 결정하는 명령줄 도구

## <a name="content-files-and-powershell-scripts"></a>콘텐츠 파일 및 PowerShell 스크립트

> [!Warning]
> 변경할 수 있는 콘텐츠 파일 및 스크립트 실행은 `packages.config` 형식에서만 제공됩니다. 모든 다른 형식과 함께 더 이상 사용되지 않으며 새 패키지에서 사용하면 안 됩니다.

`packages.config`에서 `content` 및 `tools` 폴더 내의 동일한 폴더 규칙을 사용하는 대상 프레임워크에서 콘텐츠 파일 및 PowerShell 스크립트를 그룹화할 수 있습니다. 예:

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

프레임워크 폴더를 비워 두면 NuGet은 어셈블리 참조 또는 콘텐츠 파일을 추가하거나 해당 프레임워크에서 PowerShell 스크립트를 실행하지 않습니다.

> [!Note]
> `init.ps1`은 솔루션 수준에서 실행되고 프로젝트를 사용하지 않기 때문에 `tools` 폴더 바로 아래에 배치되야 합니다. 프레임워크 폴더 아래에 있는 경우 무시됩니다.
