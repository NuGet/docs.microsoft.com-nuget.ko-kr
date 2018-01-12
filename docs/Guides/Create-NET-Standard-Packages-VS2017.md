---
title: "Visual Studio 2017을 사용하여 .NET Standard 2.0 NuGet 패키지 만들기 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: "NuGet 4.x 및 Visual Studio 2017을 사용하여 .NET Standard 2.0 NuGet 패키지를 만드는 종단 간 연습입니다."
keywords: "패키지 만들기, .NET Standard 패키지, .NET Core"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5b48ad2f062fd3a9b99985dbda6f89e6039dac4d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/05/2018
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a>Visual Studio 2017을 사용하여 .NET Standard 2.0 패키지 만들기

*Visual Studio 2017 업데이트 3에서 제공하는 NuGet 4.x 이상 및 MSBuild 15.3 이상에 적용됩니다. Visual Studio 2017 이전 버전의 경우 이 지침은 \<TargetFramework\> 속성을 변경하여 .NET Standard 1.4 - 1.6에 적용됩니다. 또한 NuGet 3.x 이상을 사용하려면 [Visual Studio 2015를 사용하여 .NET Standard 패키지 만들기](../guides/create-net-standard-packages-vs2015.md)를 참조하세요.*

[.NET Standard 라이브러리](/dotnet/articles/standard/library)는 모든 .NET 런타임에서 사용할 수 있도록 만들어진 .NET API의 공식 사양이며, 이에 따라 .NET 생태계에서 더 균일하게 설정됩니다. .NET Standard 라이브러리는 워크로드와는 별도로 구현할 모든 .NET 플랫폼에 대해 균일한 BCL(기본 클래스 라이브러리) API 집합을 정의합니다. 개발자가 모든 .NET 런타임에서 사용할 수 있는 PCL을 생성할 수 있으며, 공유 코드에서 플랫폼별 조건부 컴파일 지시문을 제거하지 않더라도 이를 줄일 수 있습니다.

이 가이드에서는 Visual Studio 2017 업데이트 3 및 NuGet 4.0을 사용하여 .NET Standard 라이브러리 2.0을 대상으로 하는 NuGet 패키지를 만드는 과정을 안내합니다.

1. [필수 구성 요소](#pre-requisites)
1. [클래스 라이브러리 프로젝트 만들기](#create-the-netstandard-class-library-project)
1. [.csproj 파일에서 메타데이터 편집](#edit-metadata-in-the-csproj-file)
1. [구성 요소 패키징](#package-the-component)
1. [관련 항목](#related-topics)

## <a name="pre-requisites"></a>필수 구성 요소

이 연습에는 **.NET Core 플랫폼 간 개발** 워크로드가 포함된 Visual Studio 2017 업데이트 3이 필요합니다. [visualstudio.com](https://www.visualstudio.com/)에서 추가 비용 없이 Community 버전을 설치하거나 Professional 및 Enterprise 버전을 사용할 수 있습니다.

필요한 워크로드는 Visual Studio 설치 관리자에서 다음과 같이 표시됩니다.

![Visual Studio Installer에서 .NET Core 플랫폼 간 개발 워크로드](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a>.NET Standard 클래스 라이브러리 프로젝트 만들기

1. Visual Studio의 **파일> 새로 만들기> 프로젝트**에서 **Visual C# > .NET Standard** 노드를 차례로 펼치고, **클래스 라이브러리(.NET Standard)**를 선택하고, 이름을 AppLogger로 변경한 다음, [확인]을 클릭합니다.

    ![새 클래스 라이브러리 프로젝트 만들기](media/NuGet4-02-NewProject.png)

1. 빌드 구성을 **릴리스**로 변경합니다.
1. [솔루션 탐색기]에서 `AppLogger` 프로젝트를 마우스 오른쪽 단추로 클릭하고, **속성**을 선택하고, **빌드** 탭을 선택하고, **XML 문서 파일** 확인란을 선택한 다음, 파일 이름을 `AppLogger.xml`로 설정합니다. 그런 다음 해당 프로젝트를 저장합니다.

1. 다음과 같은 구성 요소에 코드를 추가합니다(이는 방금 명확하게 콘솔에 메시지를 출력한 것임).

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

1. 프로젝트를 빌드하고([릴리스] 구성 사용), DLL 및 XML 파일이 `bin\Release\netstandard2.0` 폴더 내에 생성되는지 확인합니다.

## <a name="edit-metadata-in-the-csproj-file"></a>.csproj 파일에서 메타데이터 편집

NuGet 4.0 및 .NET Core 프로젝트를 사용하면 패키지 메타데이터가 `.nuspec`과 같은 외부 파일 대신 `.csproj` 파일에 직접 포함됩니다. 해당 메타데이터에 대한 전체 설명은 [MSBuild 대상으로서의 NuGet pack 및 restore](../schema/msbuild-targets.md#pack-target)에서 찾을 수 있습니다.

1. [솔루션 탐색기]에서 프로젝트를 마우스 오른쪽 단추로 클릭하고, **AppLogger.csproj 편집**을 선택한 다음, 다음과 같은 패키지 정보를 포함하도록 첫 번째 속성 그룹을 편집합니다.

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. 프로젝트를 저장한 다음, 솔루션을 마우스 오른쪽 단추로 클릭하고, 여기서 패키지에 대한 모든 파일을 올바른 메타데이터로 다시 생성하려면 **솔루션 빌드**를 선택합니다.


## <a name="package-the-component"></a>구성 요소 패키징

이전 섹션에서 추가한 대로 프로젝트에 필요한 패키지 메타데이터가 포함되어 있는 경우, NuGet 4.0은 MSBuild 버전 15.1 이상(Visual Studio 2017 업데이트 3의 일부로 MSBuild 15.3 포함)을 사용하여 pack 대상을 지원합니다. 이러한 방식으로 MSBuild를 호출하려면 명령줄에 `.csproj` 파일과 동일한 폴더에 있는 pack 대상을 지정하기만 하면 됩니다.

    msbuild /t:pack /p:Configuration=Release

콘텐츠 파일, 기호 및 소스 코드 포함과 같이 `msbuild /t:pack`을 사용하는 추가 옵션은 [MSBuild 대상으로서의 NuGet pack 및 restore](../schema/msbuild-targets.md#pack-target)를 참조하세요.

어쨌든 위의 명령은 해당 구성을 빌드할 때 기본적으로 `bin\Release` 폴더에 `AppLogger.YOUR_NAME.1.0.0.nupkg`를 생성합니다. `/p` 스위치를 생략하면 기본 구성은 `Debug`가 됩니다. 

[NuGet 패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)와 같은 도구에서 이 파일을 열고 모든 노드를 펼치면 다음과 같은 내용이 표시됩니다.

![AppLogger 패키지를 보여 주는 NuGet 패키지 탐색기](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> `.nupkg` 파일은 확장명이 다른 ZIP 파일일 뿐입니다. `.nupkg`를 `.zip`으로 변경하여 패키지 내용을 검사할 수도 있지만 패키지를 nuget.org에 업로드하려면 먼저 확장명을 복원해야 합니다.

다른 개발자가 패키지를 사용할 수 있게 하려면 [패키지 게시](../create-packages/publish-a-package.md)의 지침을 따르세요.

## <a name="related-topics"></a>관련 항목

- [프로젝트 파일의 패키지 참조](../consume-packages/package-references-in-project-files.md)는 프로젝트 파일에서 패키지를 직접 설명하는 모든 세부 정보를 설명합니다.
- [MSBuild 대상으로서의 NuGet pack 및 restore](../schema/msbuild-targets.md)는 `msbuild /t:pack`을 사용하여 패키지를 만드는 모든 옵션을 설명합니다.
- [.NET Standard 라이브러리 설명서](/dotnet/articles/standard/library)
- [.NET Framework에서 .NET Core로 이식](/dotnet/articles/core/porting/index)
