---
title: Visual Studio 2015를 사용하여 .NET Standard 및 .NET Framework NuGet 패키지 만들기 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: NuGet 3.x 및 Visual Studio 2015를 사용하여 .NET Standard 및 .NET Framework NuGet 패키지를 만드는 종단 간 연습입니다.
keywords: 패키지 만들기, .NET Standard 패키지, .NET Framework 패키지
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: dbe0a0788b5fc9ba37f7db601bd51c3e4f78f5b8
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>Visual Studio 2015를 사용하여 .NET Standard 및 .NET Framework 패키지 만들기

**참고:** .NET Standard 라이브러리를 개발할 때는 Visual Studio 2017을 사용하는 것이 좋습니다. Visual Studio 2015도 사용해도 되지만 .NET Core 도구가 미리 보기 상태로만 제공되었습니다. NuGet 4.x 이상과 Visual Studio 2017을 사용하려면 [Visual Studio 2017을 사용하여 패키지 생성 및 게시](../quickstart/create-and-publish-a-package-using-visual-studio.md)를 참조하세요.

[.NET Standard 라이브러리](/dotnet/articles/standard/library)는 모든 .NET 런타임에서 사용할 수 있도록 만들어진 .NET API의 공식 사양이며, 이에 따라 .NET 생태계에서 더 균일하게 설정됩니다. .NET Standard 라이브러리는 워크로드와는 별도로 구현할 모든 .NET 플랫폼에 대해 균일한 BCL(기본 클래스 라이브러리) API 집합을 정의합니다. 개발자가 모든 .NET 런타임에서 사용할 수 있는 코드를 생성할 수 있으며, 공유 코드에서 플랫폼별 조건부 컴파일 지시문을 제거하지 않더라도 이를 줄일 수 있습니다.

이 가이드에서는 .NET Standard 라이브러리 1.4를 대상으로 하는 NuGet 패키지 또는 .NET Framework 4.6을 대상으로 하는 NuGet 패키지를 만드는 과정을 안내합니다. .NET Standard 1.4 라이브러리는 .NET Framework 4.6.1, 유니버설 Windows 플랫폼 10, .NET Core 및 Mono/Xamarin에서 작동합니다. 자세한 내용은 [.NET Standard 매핑 테이블](/dotnet/standard/net-standard#net-implementation-support)(.NET 설명서)을 참조하세요. 원하는 경우 다른 버전의 .NET Standard 라이브러리를 선택할 수 있습니다.

## <a name="prerequisites"></a>전제 조건

1. Visual Studio 2015 업데이트 3
1. (.NET Standard에만 해당) [.NET Core SDK](https://www.microsoft.com/net/download/)
1. NuGet CLI - [nuget.org/downloads](https://nuget.org/downloads)에서 최신 버전의 nuget.exe를 다운로드하여 원하는 위치에 저장합니다. 그런 다음 해당 위치를 PATH 환경 변수에 추가합니다(아직 없는 경우).

    > [!Note]
    > nuget.exe는 설치 관리자가 아니라 CLI 도구 자체이므로 브라우저에서 다운로드한 파일을 실행하는 대신 저장해야 합니다.

## <a name="create-the-class-library-project"></a>클래스 라이브러리 프로젝트 만들기

1. Visual Studio의 **파일> 새로 만들기> 프로젝트**에서 **Visual C# > Windows** 노드를 확장하고, **클래스 라이브러리(이식 가능)**를 선택하고, 이름을 AppLogger로 변경한 다음, **확인**을 클릭합니다.

    ![새 클래스 라이브러리 프로젝트 만들기](media/NetStandard-NewProject.png)

1. **이식 가능한 클래스 라이브러리 추가** 대화 상자가 표시되면 `.NET Framework 4.6` 및 `ASP.NET Core 1.0`에 대한 옵션을 선택합니다. (.NET Framework를 대상으로 하는 경우에는 원하는 적절한 옵션을 선택할 수 있습니다.)

1. .NET Standard를 대상으로 지정하는 경우 솔루션 탐색기에서 `AppLogger (Portable)`을 마우스 오른쪽 단추로 클릭하고, **속성**을 선택하고, **라이브러리** 탭을 선택한 다음, **대상 지정** 섹션에서 **.NET 플랫폼 표준을 대상으로 지정**을 선택합니다. 그러면 확인을 묻는 메시지가 표시되며, 확인하면 드롭다운에서 `.NET Standard 1.4`(또는 다른 사용 가능한 버전)를 선택할 수 있습니다.

    ![대상을 .NET Standard 1.4로 설정](media/NetStandard-ChangeTarget.png)

1. **빌드** 탭을 클릭하고, **구성**을 `Release`로 변경하고, **XML 문서 파일** 확인란을 선택합니다.

1. 구성 요소에 다음과 같은 코드를 추가합니다.

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. 구성을 릴리스로 설정하고, 프로젝트를 빌드하고, DLL 및 XML 파일이 `bin\Release` 폴더 내에 생성되는지 확인합니다.

## <a name="create-and-update-the-nuspec-file"></a>.nuspec 파일 만들기 및 업데이트

1. 명령 프롬프트를 열고, `.sln` 파일이 있는 위치에서 한 수준 아래의 `AppLogger.csproj` 폴더로 이동한 다음, NuGet `spec` 명령을 실행하여 초기 `AppLogger.nuspec` 파일을 만듭니다.

    ```cli
    nuget spec
    ```

1. 편집기에서 `AppLogger.nuspec`을 열고 YOUR_NAME을 적절한 값으로 바꿔 다음과 일치하도록 업데이트합니다. 특히 `<id>` 값은 nuget.org 전체에서 고유해야 합니다([패키지 만들기](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)에서 설명한 명명 규칙 참조). 또한 작성자 및 설명 태그도 업데이트해야 합니다. 그렇지 않으면 압축 단계에서 오류가 발생합니다.

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. 참조 어셈블리를 `.nuspec` 파일, 즉 라이브러리의 DLL 및 IntelliSense XML 파일에 추가합니다.

    .NET Standard를 대상으로 지정하는 경우 항목은 다음과 유사하게 표시되고,

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    .NET Framework를 대상으로 하는 경우 항목이 다음과 유사하게 표시됩니다.

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. 솔루션을 마우스 오른쪽 단추로 클릭하고 **솔루션 빌드**를 선택하여 패키지에 대한 모든 파일을 생성합니다.

### <a name="declaring-dependencies"></a>종속성 선언

다른 NuGet 패키지에 대한 종속성이 있는 경우 매니페스트의 `<dependencies>` 요소에서 `<group>` 요소를 사용하여 해당 패키지를 나열합니다. 예를 들어 NewtonSoft.Json 8.0.3 이상에 대한 종속성을 선언하려면 다음을 추가합니다.

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

여기서 *version* 특성의 구문은 버전 8.0.3 이상을 사용할 수 있음을 나타냅니다. 다른 버전 범위를 지정하려면 [패키지 버전 관리](../reference/package-versioning.md)를 참조하세요.

### <a name="adding-a-readme"></a>추가 정보 추가

`readme.txt` 파일을 만들어 프로젝트 루트 폴더에 배치하고 `.nuspec` 파일에서 이를 참조합니다.

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```

프로젝트에 패키지가 설치되면 Visual Studio에서 `readme.txt`를 표시합니다. .NET Core 프로젝트에 패키지가 설치되거나 패키지가 종속성으로 설치된 경우에는 파일이 표시되지 않습니다.

## <a name="package-the-component"></a>구성 요소 패키징

완료된 `.nuspec`에서 패키지에 포함되어야 하는 모든 파일을 참조하면 `pack` 명령을 실행할 준비가 되었습니다.

```cli
nuget pack AppLogger.nuspec
```

이 명령은 `AppLogger.YOUR_NAME.1.0.0.nupkg`를 생성합니다. [NuGet 패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)와 같은 도구에서 이 파일을 열고 모든 노드를 확장하면 다음과 같은 내용이 표시됩니다(.NET Standard의 경우).

![AppLogger 패키지를 보여 주는 NuGet 패키지 탐색기](media/NetStandard-PackageExplorer.png)

> [!Tip]
> `.nupkg` 파일은 확장명이 다른 ZIP 파일일 뿐입니다. `.nupkg`를 `.zip`으로 변경하여 패키지 내용을 검사할 수도 있지만 패키지를 nuget.org에 업로드하려면 먼저 확장명을 복원해야 합니다.

다른 개발자가 패키지를 사용할 수 있게 하려면 [패키지 게시](../create-packages/publish-a-package.md)의 지침을 따르세요.

`pack`에는 Mac OS X에서 Mono 4.4.2가 필요하며, Linux 시스템에서는 작동하지 않습니다. 또한 Mac에서는 `.nuspec` 파일의 Windows 경로 이름을 Unix 스타일 경로로 변환해야 합니다.

## <a name="related-topics"></a>관련 항목

- [.nuspec 참조](../reference/nuspec.md)
- [여러 .NET Framework 버전 지원](../create-packages/supporting-multiple-target-frameworks.md)
- [패키지에 MSBuild props 및 targets 포함](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [지역화된 패키지 만들기](../create-packages/creating-localized-packages.md)
- [기호 패키지](../create-packages/symbol-packages.md)
- [패키지 버전 관리](../reference/package-versioning.md)
- [.NET Standard 라이브러리 설명서](/dotnet/articles/standard/library)
- [.NET Framework에서 .NET Core로 이식](/dotnet/articles/core/porting/index)
