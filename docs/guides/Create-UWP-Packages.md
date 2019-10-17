---
title: 유니버설 Windows 플랫폼용 NuGet 패키지 만들기
description: 유니버설 Windows 플랫폼용 Windows 런타임 구성 요소를 사용하여 NuGet 패키지를 만드는 엔드투엔드 연습입니다.
author: karann-msft
ms.author: karann
ms.date: 03/21/2017
ms.topic: tutorial
ms.openlocfilehash: 77aa186291122a8d05018ecacd1329da459badad
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380757"
---
# <a name="create-uwp-packages"></a>UWP 패키지 만들기

[UWP(유니버설 Windows 플랫폼)](https://developer.microsoft.com/windows)은 Windows 10을 실행하는 모든 디바이스에 공통된 응용 프로그램 플랫폼을 제공합니다. 이 모델 내에서 UWP 응용 프로그램은 모든 디바이스에 공통적인 WinRT API 및 응용 프로그램이 실행되는 디바이스 제품군에만 적용되는 API(Win32 및 .NET 포함)를 모두 호출할 수 있습니다.

이 연습에서는 관리 및 네이티브 프로젝트에서 모두 사용할 수 있는 네이티브 UWP 구성 요소(XAML 컨트롤 포함)를 사용하여 NuGet 패키지를 만듭니다.

## <a name="prerequisites"></a>전제 조건

1. Visual Studio 2017 또는 Visual Studio 2015 - [visualstudio.com](https://www.visualstudio.com/)에서 추가 비용 없이 2017 Community 버전을 설치합니다. Professional 및 Enterprise 버전도 사용할 수 있습니다.

1. NuGet CLI - [nuget.org/downloads](https://nuget.org/downloads)에서 최신 버전의 `nuget.exe`를 다운로드하여 선택한 위치에 저장합니다(다운로드는 바로 `.exe`임). 그런 다음 해당 위치를 PATH 환경 변수에 추가합니다(아직 없는 경우).

## <a name="create-a-uwp-windows-runtime-component"></a>UWP Windows 런타임 구성 요소 만들기

1. Visual Studio에서 **파일 > 새로 만들기 > 프로젝트**를 차례로 선택하고, **Visual C++ > Windows> 유니버설** 노드를 차례로 펼치고, **Windows 런타임 구성 요소(유니버설 Windows)** 템플릿을 선택하고, 이름을 ImageEnhancer로 변경한 다음, [확인]을 클릭합니다. 메시지가 표시되면 대상 버전 및 최소 버전에 대한 기본값을 적용합니다.

    ![새 UWP Windows 런타임 구성 요소 프로젝트 만들기](media/UWP-NewProject.png)

1. [솔루션 탐색기]에서 프로젝트를 마우스 오른쪽 단추로 클릭하고, **추가 > 새 항목**을 차례로 선택하고, **Visual C++ > XAML** 노드를 차례로 클릭하고, **템플릿 기반 컨트롤**을 선택하고, 이름을 AwesomeImageControl.cpp로 변경한 다음, **추가**를 클릭합니다.

    ![프로젝트에 새 XAML 템플릿 기반 컨트롤 항목 추가](media/UWP-NewXAMLControl.png)

1. [솔루션 탐색기]에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. [속성] 페이지에서 **구성 속성 > C/C++** 를 차례로 펼치고 **출력 파일**을 클릭합니다. 오른쪽 창에서 **XML 문서 파일 생성**의 값을 Yes로 변경합니다.

    ![XML 문서 파일 생성을 Yes로 설정](media/UWP-GenerateXMLDocFiles.png)

1. 이제 *솔루션*을 마우스 오른쪽 단추로 클릭하고, **일괄 빌드**를 선택하고, 아래 그림과 같이 대화 상자에서 세 개의 [디버그] 확인란을 선택합니다. 이렇게 하면 빌드를 수행할 때 Windows에서 지원하는 각 대상 시스템에 대한 전체 아티팩트 집합이 생성됩니다.

    ![일괄 빌드](media/UWP-BatchBuild.png)

1. [일괄 빌드] 대화 상자에서 **빌드**를 클릭하여 프로젝트를 확인하고, NuGet 패키지에 필요한 출력 파일을 만듭니다.

> [!Note]
> 이 연습에서는 패키지에 대한 [디버그] 아티팩트를 사용합니다. 디버그가 아닌 패키지의 경우 [일괄 빌드] 대화 상자에서 [릴리스] 옵션을 대신 선택하고 다음 단계에서 나오는 결과 [Release] 폴더를 참조하세요.

## <a name="create-and-update-the-nuspec-file"></a>.nuspec 파일 만들기 및 업데이트

초기 `.nuspec` 파일을 만들려면 아래의 세 단계를 수행합니다. 다음에 나오는 섹션에서 필요한 다른 업데이트를 안내합니다.

1. 명령 프롬프트를 열고 `ImageEnhancer.vcxproj`가 포함된 폴더(솔루션 파일이 있는 폴더의 하위 폴더)로 이동합니다.
1. NuGet `spec` 명령을 실행하여 `ImageEnhancer.nuspec`(`.vcxproj` 파일의 이름에서 가져온 파일 이름)을 생성합니다.

    ```cli
    nuget spec
    ```

1. 편집기에서 `ImageEnhancer.nuspec`을 열고 YOUR_NAME을 적절한 값으로 바꿔 다음과 일치하도록 업데이트합니다. 특히 `<id>` 값은 nuget.org 전체에서 고유해야 합니다([패키지 만들기](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)에서 설명한 명명 규칙 참조). 또한 작성자 및 설명 태그도 업데이트해야 합니다. 그렇지 않으면 압축 단계에서 오류가 발생합니다.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> 공용으로 빌드된 패키지의 경우 `<tags>` 요소에 특히 주의하세요. 이러한 태그는 다른 사람들이 패키지를 찾고 그 기능을 이해하는 데 도움이 됩니다.

### <a name="adding-windows-metadata-to-the-package"></a>패키지에 Windows 메타데이터 추가

Windows 런타임 구성 요소에는 공개적으로 사용할 수 있는 모든 형식을 설명하는 메타데이터가 필요하며, 이를 통해 다른 앱과 라이브러리에서 해당 구성 요소를 사용할 수 있습니다. 이 메타데이터는 프로젝트를 컴파일할 때 만들어지며 NuGet 패키지에 포함되어야 하는 .winmd 파일에 포함되어 있습니다. 또한 IntelliSense 데이터가 있는 XML 파일도 동시에 빌드되므로 포함되어야 합니다.

다음 `<files>` 노드를 `.nuspec` 파일에 추가합니다.

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a>XAML 콘텐츠 추가

구성 요소에 XAML 컨트롤을 포함하려면 프로젝트 템플릿으로 생성되는 컨트롤에 대한 기본 템플릿이 있는 XAML 파일을 추가해야 합니다. 이는 `<files>` 섹션에도 포함됩니다.

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a>네이티브 구현 라이브러리 추가

구성 요소 내에서 ImageEnhancer 형식의 핵심 논리는 각 대상 런타임(ARM, x86 및 x64)에 대해 생성되는 다양한 `ImageEnhancer.dll` 어셈블리에 포함된 네이티브 코드에 있습니다. 패키지에 이러한 어셈블리를 포함하려면 다음과 같이 `<files>` 섹션에서 관련된 .pri 리소스 파일과 함께 이를 참조합니다.

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
        <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a>.targets 추가

다음으로 NuGet 패키지를 사용할 수 있는 C++ 및 JavaScript 프로젝트에는 필요한 어셈블리 및 winmd 파일을 식별하는 .targets 파일이 필요합니다. (C# 및 Visual Basic 프로젝트는 이 작업을 자동으로 수행합니다.) 이 파일은 아래 텍스트를 `ImageEnhancer.targets`에 복사하여 만들고 `.nuspec` 파일과 동일한 폴더에 저장합니다. _참고_: 이 `.targets` 파일은 패키지 ID와 같은 이름이어야 합니다(예: `.nupspec` 파일의 `<Id>` 요소).

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

그런 다음 `.nuspec` 파일에서 `ImageEnhancer.targets`를 참조합니다.

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a>최종 .nuspec

최종 `.nuspec` 파일은 이제 다음과 같으며, YOUR_NAME을 적절한 값으로 바꾸어야 합니다.

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm64\native"/>
    <file src="..\ARM64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm64\native"/>     
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a>구성 요소 패키징

완료된 `.nuspec`에서 패키지에 포함되어야 하는 모든 파일을 참조하면 `pack` 명령을 실행할 준비가 되었습니다.

```cli
nuget pack ImageEnhancer.nuspec
```

이 명령은 `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`를 생성합니다. [NuGet 패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)와 같은 도구에서 이 파일을 열고 모든 노드를 확장하면 다음과 같은 내용이 표시됩니다.

![ImageEnhancer 패키지를 보여 주는 NuGet 패키지 탐색기](media/UWP-PackageExplorer.png)

> [!Tip]
> `.nupkg` 파일은 확장명이 다른 ZIP 파일일 뿐입니다. `.nupkg`를 `.zip`으로 변경하여 패키지 내용을 검사할 수도 있지만 패키지를 nuget.org에 업로드하려면 먼저 확장명을 복원해야 합니다.

다른 개발자가 패키지를 사용할 수 있게 하려면 [패키지 게시](../nuget-org/publish-a-package.md)의 지침을 따르세요.

## <a name="related-topics"></a>관련 항목

- [.nuspec 참조](../reference/nuspec.md)
- [기호 패키지](../create-packages/symbol-packages-snupkg.md)
- [패키지 버전 관리](../concepts/package-versioning.md)
- [여러 .NET Framework 버전 지원](../create-packages/supporting-multiple-target-frameworks.md)
- [패키지에 MSBuild props 및 targets 포함](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [지역화된 패키지 만들기](../create-packages/creating-localized-packages.md)
