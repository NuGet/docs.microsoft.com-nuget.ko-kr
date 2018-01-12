---
title: "NuGet 기호 패키지를 만드는 방법 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 9/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 4667a70d-5a17-4f1e-b2f2-b8d0c6af3882
description: "기호를 포함하는 NuGet 패키지를 만들어서 Visual Studio에서 다른 NuGet 패키지의 디버깅을 지원하는 방법입니다."
keywords: "NuGet 기호 패키지, NuGet 패키지 디버깅, NuGet 디버깅 지원, 패키지 기호, 기호 패키지 규칙"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2bdb8a2c946618b0c297c70bf7fcf6a9038b2a02
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/05/2018
---
# <a name="creating-symbol-packages"></a>기호 패키지 만들기

NuGet에서는 nuget.org 또는 기타 소스에 대한 패키지를 빌드하는 것 외에도 연관된 기호 패키지를 만들고 [SymbolSource 리포지토리](http://www.symbolsource.org/Public)에 게시하도록 지원합니다.

패키지 소비자는 Visual Studio에서 해당 기호 원본에 `http://srv.symbolsource.org/pdb/Public`을 추가할 수 있습니다. 그러면 Visual Studio 디버거에서 코드 패키지를 한 단계씩 실행할 수 있습니다. 해당 프로세스에 대한 자세한 내용은 [Visual Studio 디버거에서 기호 파일(.pdb) 및 원본 파일 지정](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)을 참조하세요.


## <a name="creating-a-symbol-package"></a>기호 패키지 만들기

기호 패키지를 만들려면 다음과 같은 규칙을 따릅니다.

- 기본 패키지(코드 포함)의 이름을 `{identifier}.nupkg`로 지정하고 `.pdb` 파일을 제외한 모든 파일을 포함합니다.
- 기호 패키지 이름을 `{identifier}.symbols.nupkg`로 지정하고 어셈블리 DLL, `.pdb` 파일, XMLDOC 파일, 원본 파일을 포함합니다(다음 섹션 참조).

`-Symbols` 옵션을 사용하여 `.nuspec` 파일 또는 프로젝트 파일에서 두 패키지를 만들 수 있습니다.

```
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

`pack`에는 Mac OS X에서 Mono 4.4.2가 필요하며, Linux 시스템에서는 작동하지 않습니다. 또한 Mac에서는 `.nuspec` 파일의 Windows 경로 이름을 Unix 스타일 경로로 변환해야 합니다.

## <a name="symbol-package-structure"></a>기호 패키지 구조

기호 패키지는 라이브러리 패키지가 수행하는 것과 동일한 방식으로 여러 대상 프레임워크를 대상으로 지정할 수 있으므로 `lib` 폴더의 구조는 DLL과 함께 `.pdb` 파일을 비롯한 기본 패키지와 정확히 동일해야 합니다.

예를 들어, .NET 4.0 및 Silverlight 4를 대상으로 하는 기호 패키지의 레이아웃은 다음과 같습니다.

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

그런 다음 소스 파일은 `src`라는 별도 특수 폴더에 저장됩니다. 이 항목은 소스 리포지토리의 상대 구조에 따라야 합니다. PDB에는 일치하는 DLL을 컴파일하는 데 사용되는 소스 파일에 대한 절대 경로가 포함되기 때문이며, 게시 프로세스 중에 찾을 수 있어야 합니다. 기본 경로(공통 경로 접두사)가 제거될 수 있습니다. 예를 들어 이러한 파일에서 빌드된 라이브러리를 고려하세요.

    C:\Projects
        \MyProject
            \Common
                \MyClass.cs
            \Full
                \Properties
                    \AssemblyInfo.cs
                \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
            \Silverlight
                \Properties
                    \AssemblyInfo.cs
                \MySilverlightExtensions.cs
                \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)

`lib` 폴더와 별개로 기호 패키지에 이 레이아웃이 포함되어야 합니다.

    \src
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs

## <a name="referring-to-files-in-the-nuspec"></a>nuspec에서 파일 참조

이전 섹션에 설명된 대로 폴더 구조에서 규칙에 의해 또는 매니페스트의 `files` 섹션에서 해당 내용을 지정하여 기호 패키지를 빌드할 수 있습니다. 예를 들어 이전 섹션에 표시된 패키지를 빌드하려면 `.nuspec` 파일에서 다음을 사용합니다.

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a>기호 패키지 게시

> [!Important]
> nuget.org에 패키지를 푸시하려면 [nuget.exe v4.1.0 이상](https://www.nuget.org/downloads)을 사용해야 합니다. 여기서는 필수 [NuGet 프로토콜](../api/nuget-protocols.md)을 구현합니다.

1. 편의상 먼저 NuGet이 포함된 API 키를 저장합니다([패키지 게시](../create-packages/publish-a-package.md) 참조). 그러면 사용자가 패키지 소유자인지 확인하기 위해 symbolsource.org는 nuget.org를 사용하여 확인하기 때문에 nuget.org 및 symbolsource.org 모두에 적용됩니다.

    ```
    nuget SetApiKey Your-API-Key
    ```

1. nuget.org에 기본 패키지를 게시한 후에 기호 패키지를 다음과 같이 푸시합니다. 그러면 파일 이름의 `.symbols` 때문에 자동으로 symbolsource.org를 대상으로 사용합니다.

    ```
    nuget push MyPackage.symbols.nupkg
    ```
> [!Note]
> nuget.exe 4.5.0 이상에서 기호 패키지는 symbolsource.org로 자동으로 푸시되지 않습니다. 다음 단계에 설명된 대로 별도로 기호 패키지를 푸시해야 합니다.

1. 다른 기호 리포지토리에 게시하거나 명명 규칙을 따르지 않는 기호 패키지를 푸시하려면 `-Source` 옵션을 사용합니다.

    ```
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

1. 동시에 다음을 사용하여 기본 패키지 및 기호 패키지를 두 리포지토리에 푸시할 수도 있습니다.

    ```
    nuget push MyPackage.nupkg
    ```

이 경우에 NuGet은 nuget.org에 기본 패키지를 게시한 후에 `MyPackage.symbols.nupkg`가 있으면 해당 항목을 https://nuget.smbsrc.net/(symbolsource.org의 푸시 URL)에 게시합니다.

## <a name="see-also"></a>참고 항목

 - <a href="https://www.symbolsource.org/Public/Wiki/Using" target="_blank">SymbolSource 사용</a>(symbolsource.org)
