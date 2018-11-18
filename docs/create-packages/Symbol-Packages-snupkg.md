---
title: 새 기호 패키지 형식 '.snupkg'를 사용하여 NuGet 기호 패키지를 게시하는 방법 | Microsoft Docs
author:
- cristinamanu
- kraigb
ms.author:
- cristinamanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet 기호 패키지(snupkg)를 만드는 방법.
keywords: NuGet 기호 패키지, NuGet 패키지 디버깅, NuGet 디버깅 지원, 패키지 기호, 기호 패키지 규칙
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: a72b59a391ed25e9617ba3ba3656301a2ed90ddc
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580436"
---
# <a name="creating-symbol-packages-snupkg"></a>기호 패키지(.snupkg) 만들기

## <a name="prerequisites"></a>전제 조건

필수 [NuGet protocols](../api/nuget-protocols.md)를 구현하는 [nuget.exe v4.9.0 이상](https://www.nuget.org/downloads) 또는 [dotnet.exe v2.2.0 이상](https://www.microsoft.com/net/download/dotnet-core/2.2).

## <a name="creating-a-symbol-package"></a>기호 패키지 만들기

snupkg 기호 패키지는 .nuspec 파일 또는.csproj 파일에서 만들 수 있습니다. NuGet.exe 및 dotnet.exe는 둘 다 지원됩니다. nuget.exe pack 명령에서 ```-Symbols -SymbolPackageFormat snupkg``` 옵션을 사용하면 .nupkg 파일에 .snupkg 파일이 추가로 생성됩니다.

.snupkg 파일을 만드는 명령 예제
```
dotnet pack MyPackage.csproj --include-symbols -p:SymbolPackageFormat=snupkg

nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg

msbuild /t:pack MyPackage.csproj /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
```

`.snupkgs`는 기본적으로 생성되지 않습니다. dotnet.exe의 경우 `-Symbols`와 함께 `SymbolsPackageFormat` 속성을 전달하고, dotnet.exe의 경우 `--include-symbols` 또는 msbuild의 경우 `/p:IncludeSymbols`를 전달해야 합니다.

SymbolsPackageFormat 속성은 `symbols.nupkg`(기본값) 또는 `snupkg`의 두 값 중 하나를 가질 수 있습니다. SymbolsPackageFormat을 지정하지 않으면 기본적으로 `symbols.nupkg`이며 레거시 기호 패키지가 생성됩니다.

> [!Note]
> 레거시 형식 `.symbols.nupkg`는 여전히 호환성 문제에서만 지원됩니다([레거시 기호 패키지](Symbol-Packages.md) 참조). NuGet.org 기호 서버는 새 기호 패키지 형식(`.snupkg`)만 허용합니다.

## <a name="publishing-a-symbol-package"></a>기호 패키지 게시

1. 편의상 먼저 NuGet과 함께 API 키를 저장합니다([패키지 게시](../create-packages/publish-a-package.md) 참조).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. 기본 패키지를 nuget.org에 게시한 후 기호 패키지를 다음과 같이 푸시합니다.

    ```cli
    nuget push MyPackage.snupkg
    ```

1. 아래 명령을 사용하여 기본 패키지 및 기호 패키지를 동시에 푸시할 수도 있습니다. .nupkg 파일 및 .snupkg 파일은 모두 현재 폴더에 있어야 합니다.

    ```cli
    nuget push MyPackage.nupkg
    ```

이 경우 NuGet은 먼저 `MyPackage.nupkg`를 nuget.org에 게시하고 다음에 `MyPackage.snupkg`가 게시됩니다.

## <a name="nugetorg-symbol-server"></a>NuGet.org 기호 서버

NuGet.org는 자체 기호 서버 리포지토리를 지원하며 새 기호 패키지 형식(`.snupkg`)만 허용합니다. 패키지 소비자는 Visual Studio에서 해당 기호 원본에 `https://symbols.nuget.org/download/symbols`를 추가하여 nuget.org 기호 서버에 게시된 기호를 사용할 수 있습니다. 그러면 Visual Studio 디버거에서 코드 패키지를 단계적으로 실행할 수 있습니다. 해당 프로세스에 대한 자세한 내용은 [Visual Studio 디버거에서 기호 파일(.pdb) 및 원본 파일 지정](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017)을 참조하세요.

### <a name="nugetorg-symbol-package-constraints"></a>Nuget.org 기호 패키지 제약 조건

Nuget.org에서 지원되는 기호 패키지에는 다음과 같은 제약 조건이 있습니다.

- 다음 파일 확장명만 기호 패키지에 추가할 수 있습니다. ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- 관리되는 [이식 가능한 pdbs](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md)만 현재 nuget 기호 서버에서 지원됩니다.
- pdbs 및 관련 nupkg dlls는 Visual Studio 버전 15.9 이상의 컴파일러로 빌드해야 합니다([pdb crypto 해시](https://github.com/dotnet/roslyn/issues/24429) 참조).

다른 파일 형식이 .snupkg에 포함된 경우 nuget.org에 게시되는 기호 패키지가 실패합니다.

### <a name="symbol-package-validation-and-indexing"></a>기호 패키지 유효성 검사 및 인덱싱

[NuGet.org](https://www.nuget.org/)에 게시된 기호 패키지는 바이러스 검사와 같은 여러 유효성 검사를 거칩니다.

패키지가 모든 유효성 검사를 통과하면 기호가 인덱싱되고 NuGet.org 기호 서버에서 사용할 수 있게 되는 데 시간이 걸릴 수 있습니다. 패키지가 유효성 검사에 실패하면 .nupkg의 패키지 세부 정보 페이지가 업데이트되어 관련 오류가 표시되고 이를 알리는 이메일도 받게 됩니다.

패키지 유효성 검사 및 인덱싱은 일반적으로 15분이 걸리지 않습니다. 패키지 게시가 예상보다 오래 걸리면 [status.nuget.org](https://status.nuget.org/)를 방문하여 nuget.org에 중단이 발생했는지를 확인합니다. 모든 시스템이 모두 제대로 작동하고 패키지가 한 시간 내에 성공적으로 게시되지 않은 경우 nuget.org에 로그인하여 패키지 세부 정보 페이지에서 지원 문의 링크를 사용하여 문의하세요.

## <a name="symbol-package-structure"></a>기호 패키지 구조

.Nupkg 파일은 현재와 정확히 동일하지만 .snupkg 파일은 다음과 같은 특징이 있습니다.

1) .snupkg는 해당 .nupkg와 동일한 id 및 버전을 갖습니다.
2) .snupkg는 DLL/EXE 대신 해당 PDB가 동일한 폴더 계층 구조에 포함되도록 구분하여 모든 DLL 또는 EXE 파일의 nupkg와 정확히 동일한 폴더 구조를 가집니다. PDB 이외의 확장명을 가진 파일 및 폴더는 snupkg에서 제외됩니다.
3) .snupkg의 .nuspec 파일도 아래와 같이 새 PackageType을 지정합니다. 하나의 PackageType만 지정해야 합니다. 
``` 
<packageTypes>
  <packageType name="SymbolsPackage"/>
</packageTypes>
```
4) 작성자가 nupkg 및 snupkg를 빌드하는 데 사용자 지정 nuspec을 사용하기로 결정한 경우 snupkg는 2)에 자세히 설명된 것과 동일한 계층 구조와 파일을 가져야 합니다.
5) ```authors``` 및 ```owners``` 필드는 snupkg의 nuspec에서 제외됩니다.

## <a name="see-also"></a>참고 항목

[NuGet-Package-Debugging-&-Symbols-Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
