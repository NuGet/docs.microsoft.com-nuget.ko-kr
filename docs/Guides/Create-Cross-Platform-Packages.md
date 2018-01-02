---
title: "플랫폼 간 NuGet 패키지 만들기(iOS, Android 및 Windows용) | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: ae24824b-a138-4d12-a810-1f653ddffd32
description: "iOS, Android 및 Windows에서 네이티브 API를 사용하는 Xamarin에 대한 NuGet 패키지를 만드는 종단 간 연습입니다."
keywords: "패키지 만들기, Xamarin에 대한 패키지, 플랫폼 간 패키지"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8ee825a6299d7de375fd2f242cf456da13b777d9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="create-cross-platform-packages"></a>플랫폼 간 패키지 만들기

플랫폼 간 패키지에는 런타임 운영 체제에 따라 iOS, Android 및 Windows에서 네이티브 API를 사용하는 코드가 포함되어 있습니다. 이 작업은 간단하지만 개발자가 공통 API 노출 영역을 통해 PCL 또는 .NET Standard 라이브러리에서 패키지를 사용할 수 있게 하는 것이 좋습니다.

이 연습에서는 iOS, Android 및 Windows의 모바일 프로젝트에 사용할 수 있는 플랫폼 간 NuGet 패키지를 만듭니다.

1. [필수 구성 요소](#pre-requisites)
1. [프로젝트 구조 및 추상화 코드 만들기](#create-the-project-structure-and-abstraction-code)
1. [플랫폼 특정 코드 작성](#write-your-platform-specific-code)
1. [.nuspec 파일 만들기 및 업데이트](#create-and-update-the-nuspec-file)
1. [구성 요소 패키징](#package-the-component)
1. [관련 항목](#related-topics)

## <a name="pre-requisites"></a>필수 구성 요소

1. UWP(유니버설 Windows 플랫폼) 및 Xamarin이 있는 Visual Studio 2015 - [visualstudio.com](https://www.visualstudio.com/)에서 추가 비용 없이 Community 버전을 설치합니다. Professional 및 Enterprise 버전도 사용할 수 있습니다. UWP 및 Xamarin 도구를 포함하려면 사용자 지정 설치를 선택하고 적절한 옵션을 선택합니다.
1. NuGet CLI - [nuget.org/downloads](https://nuget.org/downloads)에서 최신 버전의 nuget.exe를 다운로드하여 원하는 위치에 저장합니다. 그런 다음 해당 위치를 PATH 환경 변수에 추가합니다(아직 없는 경우).

> [!Note]
> nuget.exe는 설치 관리자가 아니라 CLI 도구 자체이므로 브라우저에서 다운로드한 파일을 실행하는 대신 저장해야 합니다.


## <a name="create-the-project-structure-and-abstraction-code"></a>프로젝트 구조 및 추상화 코드 만들기

1. Visual Studio용 [Plugin for Xamarin Templates 확장](https://visualstudiogallery.msdn.microsoft.com/afead421-3fbf-489a-a4e8-4a244ecdbb1e)을 다운로드하여 실행합니다. 이러한 템플릿을 사용하면 이 연습에 필요한 프로젝트 구조를 쉽게 만들 수 있습니다.
1. Visual Studio의 **파일 > 새로 만들기 > 프로젝트**에서 `Plugin`을 검색하고, **Plugin for Xamarin** 템플릿을 선택하고, 이름을 LoggingLibrary로 변경한 다음, [확인]을 클릭합니다.

    ![Visual Studio에서 비어 있는 새 앱(이식 가능한 Xamarin.Forms) 프로젝트](media/CrossPlatform-NewProject.png)

결과 솔루션에는 다양한 플랫폼 특정 프로젝트와 함께 두 개의 PCL 프로젝트가 포함되어 있습니다.

- `Plugin.LoggingLibrary.Abstractions (Portable)`라는 PCL은 구성 요소의 공용 인터페이스(API 노출 영역)를 정의합니다. 이 경우 ILoggingLibrary.cs 파일에 포함된 `ILoggingLibrary` 인터페이스입니다. 여기서는 라이브러리에 대한 인터페이스를 정의합니다.
- 다른 `Plugin.LoggingLibrary (Portable)` PCL에는 런타임 시 추상 인터페이스의 플랫폼 특정 구현을 찾는 CrossLoggingLibrary.cs의 코드가 포함되어 있습니다. 일반적으로 이 파일은 수정할 필요가 없습니다.
- `Plugin.LoggingLibrary.Android`와 같은 플랫폼 특정 프로젝트에는 각각 해당 LoggingLibraryImplementation.cs 파일의 네이티브 인터페이스 구현이 포함되어 있습니다. 여기서는 라이브러리 코드를 빌드합니다.

기본적으로 Abstractions 프로젝트의 ILoggingLibrary.cs 파일에는 인터페이스 정의가 있지만 메서드는 없습니다. 이 연습의 목적을 위해 다음과 같이 `Log` 메서드를 추가합니다.

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a>플랫폼 특정 코드 작성

`ILoggingLibrary` 인터페이스 및 해당 메서드의 플랫폼 특정 구현을 구현하려면 다음을 수행합니다.

1. 각 플랫폼 프로젝트의 `LoggingLibraryImplementation.cs` 파일을 열고 필요한 코드를 추가합니다. 예를 들어 다음과 같습니다(`Plugin.LoggingLibrary.Android` 프로젝트 사용).

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. 지원하려는 각 플랫폼에 대한 프로젝트에서 이 구현을 반복합니다.
1. iOS 프로젝트를 마우스 오른쪽 단추로 클릭하고, **속성**을 선택하고, **빌드** 탭을 클릭한 다음, **출력 경로** 및 **XML 문서 파일** 설정에서 "\iPhone"을 제거합니다. 이는 이 연습에서 나중의 편의를 위한 작업입니다. 완료되면 파일을 저장합니다.
1. 솔루션을 마우스 오른쪽 단추로 클릭하고, **구성 관리자...**를 선택한 다음, 지원하는 PCL 및 각 플랫폼에 대한 **빌드** 상자를 선택합니다.
1. 솔루션을 마우스 오른쪽 단추로 클릭하고, **솔루션 빌드**를 선택하여 작업을 확인하고, 다음에 패키지할 아티팩트를 생성합니다. 누락된 참조에 대한 오류가 발생하면 솔루션을 마우스 오른쪽 단추로 클릭하고, **NuGet 패키지 복원**을 선택하여 종속성을 설치한 다음, 다시 빌드합니다.

> [!Note]
> iOS용으로 빌드하려면 [Visual Studio용 Xamarin.iOS 소개](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)에서 설명한 대로 네트워크에서 Visual Studio에 연결된 Mac이 필요합니다. Mac을 사용할 수 없는 경우 구성 관리자에서 iOS 프로젝트를 선택 취소합니다(위 3단계).


## <a name="create-and-update-the-nuspec-file"></a>.nuspec 파일 만들기 및 업데이트

1. 명령 프롬프트를 열고, `.sln` 파일이 있는 위치에서 한 수준 아래의 `LoggingLibrary` 폴더로 이동한 다음, NuGet `spec` 명령을 실행하여 초기 `Package.nuspec` 파일을 만듭니다.

```
nuget spec
```

1. 이 파일의 이름을 `LoggingLibrary.nuspec`으로 변경하고 편집기에서 엽니다.
1. YOUR_NAME을 적절한 값으로 바꿔 다음과 일치하도록 파일을 업데이트합니다. 특히 `<id>` 값은 nuget.org 전체에서 고유해야 합니다([패키지 만들기](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)에서 설명한 명명 규칙 참조). 또한 작성자 및 설명 태그도 업데이트해야 합니다. 그렇지 않으면 압축 단계에서 오류가 발생합니다.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```
    
> [!Tip]
> 패키지 버전에 `-alpha`, `-beta` 또는 `-rc` 접미사를 붙여 패키지를 시험판으로 표시할 수 있습니다. 시험판 버전에 대한 자세한 내용은 [시험판 버전](../create-packages/prerelease-packages.md)을 참조하세요.

### <a name="add-reference-assemblies"></a>참조 어셈블리 추가

플랫폼 특정 참조 어셈블리를 포함하려면 지원되는 플랫폼에 맞게 `LoggingLibrary.nuspec`의 `<files>` 요소에 다음을 추가합니다.

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> DLL 및 XML 파일의 이름을 짧게 하려면, 지정된 프로젝트를 마우스 오른쪽 단추로 클릭하고 **라이브러리** 탭을 선택한 다음 어셈블리 이름을 변경합니다.


### <a name="add-dependencies"></a>종속성 추가

네이티브 구현에 대한 특정 종속성이 있는 경우 `<dependencies>` 요소와 함께 `<group>` 요소를 사용하여 해당 종속성을 지정합니다. 예를 들어 다음과 같습니다.

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

예를 들어 다음은 iTextSharp를 UAP 대상에 대한 종속성으로 설정합니다.

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>최종 .nuspec

최종 `.nuspec` 파일은 이제 다음과 같으며, YOUR_NAME을 적절한 값으로 바꾸어야 합니다.

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a>구성 요소 패키징

완료된 `.nuspec`에서 패키지에 포함되어야 하는 모든 파일을 참조하면 `pack` 명령을 실행할 준비가 되었습니다.

```
nuget pack LoggingLibrary.nuspec
```

그러면 `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`가 생성됩니다. [NuGet 패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)와 같은 도구에서 이 파일을 열고 모든 노드를 펼치면 다음과 같은 내용이 표시됩니다.

![LoggingLibrary 패키지를 보여 주는 NuGet 패키지 탐색기](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> `.nupkg` 파일은 확장명이 다른 ZIP 파일일 뿐입니다. `.nupkg`를 `.zip`으로 변경하여 패키지 내용을 검사할 수도 있지만 패키지를 nuget.org에 업로드하려면 먼저 확장명을 복원해야 합니다.


다른 개발자가 패키지를 사용할 수 있게 하려면 [패키지 게시](../create-packages/publish-a-package.md)의 지침을 따르세요.

## <a name="related-topics"></a>관련 항목

- [.nuspec 참조](../schema/nuspec.md)
- [기호 패키지](../create-packages/symbol-packages.md)
- [패키지 버전 관리](../reference/package-versioning.md)
- [여러 .NET Framework 버전 지원](../create-packages/supporting-multiple-target-frameworks.md)
- [패키지에 MSBuild props 및 targets 포함](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [지역화된 패키지 만들기](../create-packages/creating-localized-packages.md)