---
title: 새 기호 패키지 형식 '.snupkg'를 사용하여 NuGet 기호 패키지를 게시하는 방법 | Microsoft Docs
author: cristinamanu
ms.author: cristinamanu
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
ms.openlocfilehash: e62d1872497e0e5e703bf7c49a87249ce9a996c7
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959671"
---
# <a name="creating-symbol-packages-snupkg"></a>기호 패키지(.snupkg) 만들기

기호 패키지를 사용하면 NuGet 패키지의 디버깅 환경을 향상시킬 수 있습니다.

## <a name="prerequisites"></a>전제 조건

필수 [NuGet protocols](../api/nuget-protocols.md)를 구현하는 [nuget.exe v4.9.0 이상](https://www.nuget.org/downloads) 또는 [dotnet.exe v2.2.0 이상](https://www.microsoft.com/net/download/dotnet-core/2.2).

## <a name="creating-a-symbol-package"></a>기호 패키지 만들기

dotnet.exe, NuGet.exe 또는 MSBuild를 사용하여 snupkg 기호 패키지를 만들 수 있습니다. NuGet.exe를 사용하는 경우 다음 명령을 사용하여 .nupkg 파일 외에도 .snupkg 파일을 만들 수 있습니다.

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

dotnet.exe 또는 MSBuild를 사용하는 경우 다음 단계에 따라 .nupkg 파일 외에도 .snupkg 파일을 만듭니다.

1. .csproj 파일에 다음 속성을 추가합니다.

    ```xml
    <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
    </PropertyGroup>
    ```

1. `dotnet pack MyPackage.csproj` 또는 `msbuild -t:pack MyPackage.csproj`로 프로젝트를 압축합니다.

[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) 속성은 `symbols.nupkg`(기본값) 또는 `snupkg`의 두 값 중 하나를 가질 수 있습니다. [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) 속성을 지정하지 않으면 레거시 기호 패키지가 생성됩니다.

> [!Note]
> 레거시 형식 `.symbols.nupkg`는 여전히 호환성 문제에서만 지원됩니다([레거시 기호 패키지](Symbol-Packages.md) 참조). NuGet.org의 기호 서버는 새 기호 패키지 형식(`.snupkg`)만 허용합니다.

## <a name="publishing-a-symbol-package"></a>기호 패키지 게시

1. 편의상 먼저 NuGet과 함께 API 키를 저장합니다([패키지 게시](../nuget-org/publish-a-package.md) 참조).

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

NuGet은 두 패키지를 nuget.org에 게시합니다. `MyPackage.nupkg`가 먼저 게시되고 `MyPackage.snupkg`가 그다음으로 게시됩니다.

> [!Note]
> 기호 패키지가 게시되지 않은 경우 NuGet.org 소스를 `https://api.nuget.org/v3/index.json`(으)로 구성했는지 확인합니다. 기호 패키지 게시는 [NuGet V3 API](../api/overview.md#versioning)에서만 지원됩니다.

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

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) 작성자가 nupkg 및 snupkg를 빌드하는 데 사용자 지정 nuspec을 사용하기로 결정한 경우 snupkg는 2)에 자세히 설명된 것과 동일한 계층 구조와 파일을 가져야 합니다.
5) ```authors``` 및 ```owners``` 필드는 snupkg의 nuspec에서 제외됩니다.
6) <license> 요소를 사용하지 마세요. .snupkg에는 해당.nupk와 동일한 라이선스가 적용됩니다.

## <a name="see-also"></a>참고 항목

[NuGet-Package-Debugging-&-Symbols-Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
