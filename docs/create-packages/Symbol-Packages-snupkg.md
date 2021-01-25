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
ms.openlocfilehash: fbcc035a6b800617f995d3bcebd7e1764aa467b0
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235726"
---
# <a name="creating-symbol-packages-snupkg"></a>기호 패키지(.snupkg) 만들기

디버깅 환경이 제대로 작동하려면 컴파일된 코드와 소스 코드 간의 연결, 지역 변수 이름, 스택 추적 등의 중요한 정보를 제공하는 디버그 기호가 있어야 합니다. 기호 패키지(.snupkg)를 사용하여 이러한 기호를 배포하고 NuGet 패키지의 디버깅 환경을 개선할 수 있습니다.

## <a name="prerequisites"></a>사전 요구 사항

필수 [NuGet 프로토콜](../api/nuget-protocols.md)을 구현하는 [nuget.exe v4.9.0 이상](https://www.nuget.org/downloads) 또는 [dotnet CLI v2.2.0 이상](https://www.microsoft.com/net/download/dotnet-core/2.2)

## <a name="creating-a-symbol-package"></a>기호 패키지 만들기

dotnet CLI 또는 MSBuild를 사용하는 경우 nupkg 파일 외에 .snupkg 파일을 만들도록 `IncludeSymbols` 및 `SymbolPackageFormat` 속성을 설정해야 합니다.

* .csproj 파일에 다음 속성을 추가합니다.

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* 또는 명령줄에서 다음 속성을 지정합니다.

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  또는

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

NuGet.exe를 사용하는 경우 다음 명령을 사용하여 .nupkg 파일 외에도 .snupkg 파일을 만들 수 있습니다.

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

[`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) 속성은 `symbols.nupkg`(기본값) 또는 `snupkg`의 두 값 중 하나를 가질 수 있습니다. 이 속성을 지정하지 않으면 레거시 기호 패키지가 생성됩니다.

> [!Note]
> 레거시 형식 `.symbols.nupkg`는 네이티브 패키지와 같이 여전히 호환성 이유로만 지원됩니다([레거시 기호 패키지](Symbol-Packages.md) 참조). NuGet.org의 기호 서버는 새 기호 패키지 형식(`.snupkg`)만 허용합니다.

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

NuGet.org는 자체 기호 서버 리포지토리를 지원하며 새 기호 패키지 형식(`.snupkg`)만 허용합니다. 패키지 소비자는 Visual Studio에서 해당 기호 원본에 `https://symbols.nuget.org/download/symbols`를 추가하여 nuget.org 기호 서버에 게시된 기호를 사용할 수 있습니다. 그러면 Visual Studio 디버거에서 코드 패키지를 단계적으로 실행할 수 있습니다. 해당 프로세스에 대한 자세한 내용은 [Visual Studio 디버거에서 기호 파일(.pdb) 및 원본 파일 지정](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)을 참조하세요.

### <a name="nugetorg-symbol-package-constraints"></a>NuGet.org 기호 패키지 제약 조건

NuGet.org에는 기호 패키지에 대한 다음과 같은 제약 조건이 있습니다.

- 기호 패키지에는 `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`와 같은 파일 확장명만 사용할 수 있습니다.
- 관리형 [이동식 PDB](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md)만 NuGet.org의 기호 서버에서 지원됩니다.
- PDB 및 관련 .nupkg DLL은 Visual Studio 버전 15.9 이상의 컴파일러로 빌드해야 합니다([PDB crypto 해시](https://github.com/dotnet/roslyn/issues/24429) 참조).

이러한 제약 조건이 충족되지 않으면 NuGet.org에 게시된 기호 패키지가 유효성 검사에 실패합니다. 

> [!NOTE]
> C++ 프로젝트와 같은 네이티브 프로젝트는 이식 가능한 PDB 대신 Windows PDB를 생성합니다. 해당 기능은 NuGet.org의 기호 서버에서 지원되지 않습니다. 대신 [레거시 기호 패키지](Symbol-Packages.md)를 사용하세요.

### <a name="symbol-package-validation-and-indexing"></a>기호 패키지 유효성 검사 및 인덱싱

[NuGet.org](https://www.nuget.org/)에 게시된 기호 패키지는 맬웨어 검색을 포함한 여러 유효성 검사를 거칩니다. 패키지가 유효성 검사에 실패하면 패키지 세부 정보 페이지에 오류 메시지가 표시됩니다. 또한 패키지 소유자는 식별된 문제를 해결하는 방법에 대한 지침이 포함된 전자 메일을 받게 됩니다.

기호 패키지가 모든 유효성 검사를 통과하면 기호는 NuGet.org의 기호 서버에 의해 인덱싱되어 사용할 수 있게 됩니다.

패키지 유효성 검사 및 인덱싱은 일반적으로 15분이 걸리지 않습니다. 패키지 게시가 예상보다 오래 걸리면 [status.nuget.org](https://status.nuget.org/)를 방문하여 NuGet.org에 중단이 발생했는지를 확인합니다. 모든 시스템이 모두 제대로 작동하고 패키지가 한 시간 내에 성공적으로 게시되지 않은 경우 nuget.org에 로그인하여 패키지 세부 정보 페이지에서 지원 문의 링크를 사용하여 문의하세요.

## <a name="symbol-package-structure"></a>기호 패키지 구조

기호 패키지(. snupkg)의 특징은 다음과 같습니다.

1) .snupkg는 해당 NuGet 패키지(.nupkg)와 동일한 ID 및 버전을 갖습니다.
2) .snupkg는 DLL/EXE 대신 해당 PDB가 동일한 폴더 계층 구조에 포함되도록 구분하여 모든 DLL 또는 EXE 파일의 해당 nupkg와 정확히 동일한 폴더 구조를 가집니다. PDB 이외의 확장명을 가진 파일 및 폴더는 snupkg에서 제외됩니다.
3) 기호 패키지의 .nuspec 파일은 `SymbolsPackage` 패키지 유형입니다.

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) 작성자가 nupkg 및 snupkg를 빌드하는 데 사용자 지정 nuspec을 사용하기로 결정한 경우 snupkg는 2)에 자세히 설명된 것과 동일한 계층 구조와 파일을 가져야 합니다.
5) ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl``` 및 ```icon``` 필드는 snupkg의 nuspec에서 제외됩니다.
6) ```<license>``` 요소를 사용하지 마세요. .snupkg에는 해당 .nupkg와 동일한 라이선스가 적용됩니다.

## <a name="see-also"></a>참고 항목

소스 링크를 사용하여 .NET 어셈블리의 소스 코드 디버깅을 사용하도록 설정하는 것이 좋습니다. 자세한 내용은 [소스 링크 지침](/dotnet/standard/library-guidance/sourcelink)을 참조하세요.

기호 패키지에 대한 자세한 내용은 [NuGet 패키지 디버깅 & 기호 향상](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) 디자인 사양을 참조하세요.
