---
title: NuGet용 .NET Compiler Platform 분석기 형식
description: API 또는 라이브러리를 구현하는 NuGet 패키지를 포함하여 패키지되고 배포되는 .NET 분석기 규칙입니다.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 63880b6b9bbfe6aac9cc6419d6a972062eea3495
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774132"
---
# <a name="analyzer-nuget-formats"></a>NuGet 분석기 형식

개발자는 .NET Compiler Platform("Roslyn"이라고도 함)으로 [분석기](https://github.com/dotnet/roslyn/blob/master/docs/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix.md)를 만들어, 코드 작성 시 구문 트리와 코드 의미 체계를 검사할 수 있습니다. 개발자는 이를 통해 특정 API 또는 라이브러리의 사용을 안내하는 데 도움이 되는 도구 등 도메인 특정 분석 도구를 만들 수 있습니다. 자세한 내용은 [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub Wiki에서 찾을 수 있습니다. 또한 MSDN Magazine의 [Roslyn을 사용하여 API에 대한 라이브 코드 분석기 작성](/archive/msdn-magazine/2014/special-issue/csharp-and-visual-basic-use-roslyn-to-write-a-live-code-analyzer-for-your-api) 문서도 참조하세요.

분석기 자체는 일반적으로 문제의 API 또는 라이브러리를 구현하는 NuGet 패키지의 일부로 패키지되어 배포됩니다.

좋은 예제에 대해서는 다음 콘텐츠가 포함된 [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) 패키지를 참조하세요.

- analyzers\dotnet\System.Runtime.Analyzers.dll
- analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- tools\install.ps1
- tools\uninstall.ps1

여기서 볼 수 있듯이 패키지의 `analyzers` 폴더에 분석기 DLL을 배치합니다.

분석기 구현에 레거시 FxCop 규칙을 사용하지 않도록 설정하기 위해 포함된 props 파일은 `build` 폴더에 배치됩니다.

`packages.config`를 사용하여 프로젝트를 지원하는 설치 및 제거 스크립트는 `tools`에 배치됩니다.

또한 이 패키지에는 플랫폼 특정 요구 사항이 없으므로 `platform` 폴더가 생략됩니다.


## <a name="analyzers-path-format"></a>분석기 경로 형식

`analyzers` 폴더의 사용은 경로의 지정자에서 빌드 시간 대신 개발 호스트 종속성을 설명한다는 점을 제외하고는 [대상 프레임워크](../create-packages/supporting-multiple-target-frameworks.md)에 사용되는 것과 비슷합니다. 일반적인 형식은 다음과 같습니다.

```
$/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll
```

- **framework_name** 및 **version**: 포함된 DLL에서 실행해야 하는 .NET Framework의 *선택적* API 노출 영역입니다. Roslyn은 분석기를 실행할 수 있는 유일한 호스트이므로 `dotnet`은 현재 유효한 값입니다. 대상을 지정하지 않으면 DLL이 *모든* 대상에 적용된다고 가정합니다.
- **supported_language**: DLL이 적용되는 언어로서 `cs`(C#), `vb`(Visual Basic) 및 `fs`(F#) 중 하나입니다. 언어는 해당 언어를 사용하는 프로젝트에만 분석기가 로드되어야 함을 나타냅니다. 언어를 지정하지 않으면 분석기를 지원하는 *모든* 언어에 DLL이 적용되는 것으로 간주됩니다.
- **analyzer_name**: 분석기의 DLL을 지정합니다. DLL 이외의 추가 파일이 필요하며 대상 또는 속성 파일을 통해 포함되어야 합니다.


## <a name="install-and-uninstall-scripts"></a>스크립트 설치 및 제거

사용자의 프로젝트가 `packages.config`를 사용하는 경우 분석기를 선택하는 MSBuild 스크립트가 작동하지 않게 되므로 `install.ps1` 및 `uninstall.ps1`를 아래에 설명된 콘텐츠와 함께 `tools` 폴더에 넣어야 합니다.

**install.ps1 파일 내용**

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Install the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Install language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}
```


**uninstall.ps1 파일 내용**

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                try
                {
                    $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
                }
                catch
                {

                }
            }
        }
    }
}
```
