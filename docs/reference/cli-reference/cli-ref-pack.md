---
title: NuGet CLI pack 명령
description: nuget.exe pack 명령에 대 한 참조
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e2906d53119cb8c922df7d177cd686836ac50a5a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780047"
---
# <a name="pack-command-nuget-cli"></a>pack 명령 (NuGet CLI)

**적용 대상:** 패키지 만들기 &bullet; **지원 버전:** 2.7 +

지정 된 [nuspec](../nuspec.md) 또는 프로젝트 파일을 기반으로 하는 NuGet 패키지를 만듭니다. `dotnet pack`명령 ( [dotnet 명령](../dotnet-Commands.md)참조) 및 `msbuild -t:pack` ( [MSBuild 대상](../msbuild-targets.md)참조)을 대체 항목으로 사용할 수 있습니다.

> [!Important]
> [`dotnet pack`](../dotnet-Commands.md) [`msbuild -t:pack`](../msbuild-targets.md) [PackageReference](../../consume-packages/package-references-in-project-files.md) 기반 프로젝트의 경우 또는를 사용 합니다.
> Mono에서는 프로젝트 파일에서 패키지를 만들 수 없습니다. 또한 `.nuspec` Windows 경로 이름을 변환 하지 않으므로 파일의 비로컬 경로를 Unix 스타일 경로로 조정 해야 합니다 nuget.exe.

## <a name="usage"></a>사용량

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

여기서 `<nuspecPath>` 및 `<projectPath>` 은 `.nuspec` 각각 또는 프로젝트 파일을 지정 합니다.

## <a name="options"></a>옵션
- **`-BasePath`**

   [Nuspec](../nuspec.md) 파일에 정의 된 파일의 기본 경로를 설정 합니다.

- **`-Build`**

  패키지를 빌드하기 전에 프로젝트를 빌드해야 함을 지정 합니다.

- **`-ConfigFile`**

  적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.

- **`-Exclude`**

  패키지를 만들 때 제외할 와일드 카드 패턴을 하나 이상 지정 합니다. 둘 이상의 패턴을 지정 하려면-Exclude 플래그를 반복 합니다. 아래 예제를 참조하세요.

- **`-ExcludeEmptyDirectories`**

  패키지를 빌드할 때 빈 디렉터리가 포함 되지 않도록 합니다.

- **`-ForceEnglishOutput`**

  *(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.

- **`-?|-help`**

  명령에 대 한 도움말 정보를 표시 합니다.

- **`-IncludeReferencedProjects`**

  빌드된 패키지에 종속성 또는 패키지의 일부로 참조 된 프로젝트를 포함 해야 함을 나타냅니다. 참조 된 프로젝트에 `.nuspec` 프로젝트와 이름이 같은 해당 파일이 있는 경우 참조 된 프로젝트가 종속성으로 추가 됩니다. 그렇지 않으면 참조 된 프로젝트가 패키지의 일부로 추가 됩니다.

- **`-InstallPackageToOutputPath`**

  명령이 공유 피드를 지원 하도록 패키지 출력 디렉터리를 준비 해야 하는지 여부를 지정 합니다.

- **`-MinClientVersion`**

  만든 패키지에 대 한 *minClientVersion* 특성을 설정 합니다. 이 값은 파일의 기존 *minClientVersion* 특성 (있는 경우)의 값을 재정의 합니다 `.nuspec` .

- **`-MSBuildPath`**

  *(4.0 이상)* 명령에 사용할 MSBuild의 경로를 지정 합니다 `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2 이상)* 이 명령에 사용할 MSBuild의 버전을 지정 합니다. 지원 되는 값은 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9입니다. 기본적으로 경로에 MSBuild가 선택 되어 있으며, 그렇지 않은 경우 기본적으로 설치 되어 있는 MSBuild의 가장 높은 버전으로 설정 됩니다.

- **`-NoDefaultExcludes`**

  및와 같이 점으로 시작 하는 NuGet 패키지 파일 및 파일 및 폴더의 기본 제외를 `.svn` 방지 `.gitignore` 합니다.

- **`-NonInteractive`**

  사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.

- **`-NoPackageAnalysis`**

  패키지를 빌드한 후 팩에서 패키지 분석을 실행하지 않아야 함을 지정합니다.

- **`-OutputDirectory`**

  만들어진 패키지가 저장 되는 폴더를 지정 합니다. 폴더를 지정 하지 않으면 현재 폴더가 사용 됩니다.

- **`-OutputFileNamesWithoutVersion`**

  명령에서 버전 없이 패키지 출력 이름을 준비 해야 하는지 여부를 지정 합니다.

- **`-PackagesDirectory`**

  패키지 폴더를 지정 합니다.

- **`-p|-Properties`**

  다른 옵션 다음에 오는 명령줄에서 마지막에 표시 되어야 합니다. 프로젝트 파일의 값을 재정의 하는 속성의 목록을 지정 합니다. 속성 이름에 대 한 [일반적인 MSBuild 프로젝트 속성](/visualstudio/msbuild/common-msbuild-project-properties) 을 참조 하세요. 여기에 있는 Properties 인수는 세미콜론으로 구분 된 토큰 = 값 쌍의 목록이 며,이 목록은 파일의 각 항목이 `$token$` `.nuspec` 지정 된 값으로 대체 됩니다. 값은 따옴표로 묶인 문자열일 수 있습니다. "구성" 속성의 경우 기본값은 "Debug"입니다. 릴리스 구성으로 변경 하려면를 사용 `-Properties Configuration=Release` 합니다. **일반적** 으로 이러한 속성은 비정상적인 동작을 방지 하기 위해 해당 프로젝트 빌드 중에 사용 된 것과 동일 해야 합니다.

- **`-SolutionDirectory`**

  솔루션 디렉터리를 지정 합니다.

- **`-Suffix`**

  *(3.4.4 +)* 일반적으로 빌드 또는 기타 시험판 식별자를 추가 하는 데 사용 되는 내부적으로 생성 된 버전 번호에 접미사를 추가 합니다. 예를 들어를 사용 하면 `-suffix nightly` 와 같은 버전 번호를 사용 하 여 패키지를 만듭니다 `1.2.3-nightly` . 서로 다른 버전의 NuGet 및 NuGet 패키지 관리자와의 경고, 오류 및 잠재적 비 호환성을 방지 하려면 접미사를 문자로 시작 해야 합니다.

- **`-SymbolPackageFormat`**

  기호 패키지를 만들 때에서 및 형식을 선택할 수 있습니다 `snupkg` `symbols.nupkg` .

- **`-Symbols`**

  패키지에 원본 및 기호가 포함 되도록 지정 합니다. 파일에 사용 되는 경우 `.nuspec` 일반 NuGet 패키지 파일 및 해당 기호 패키지를 만듭니다. 기본적으로 [레거시 기호 패키지](../../create-packages/Symbol-Packages.md)를 만듭니다. 기호 패키지에 대한 새 권장 형식은 .snupkg입니다. [기호 패키지(.snupkg) 만들기](../../create-packages/Symbol-Packages-snupkg.md)를 참조하세요.

- **`-Tool`**

   프로젝트의 출력 파일을 폴더에 배치 하도록 지정 합니다 `tool` .

- **`-Verbosity [normal|quiet|detailed]`**

  출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.

- **`-Version`**

  파일의 버전 번호를 재정의 `.nuspec` 합니다.

[환경 변수](cli-ref-environment-variables.md) 참조

## <a name="excluding-development-dependencies"></a>개발 종속성 제외

일부 NuGet 패키지는 사용자 고유의 라이브러리를 작성 하는 데 도움이 되는 개발 종속성으로 유용 하지만 실제 패키지 종속성으로 반드시 필요한 것은 아닙니다.

`pack`이 명령은 `package` `packages.config` `developmentDependency` 특성이로 설정 된에서 항목을 무시 `true` 합니다. 이러한 항목은 생성 된 패키지에 종속성으로 포함 되지 않습니다.

예를 들어 `packages.config` 소스 프로젝트에서 다음 파일을 고려 합니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

이 프로젝트의 경우에서 만든 패키지는 `nuget pack` 및에 대 한 종속성을 갖지 `jQuery` `microsoft-web-helpers` 않습니다 `netfx-Guard` .

## <a name="suppressing-pack-warnings"></a>Pack 경고 표시 안 함

Pack 작업 중에 모든 NuGet 경고를 해결 하는 것이 좋지만 특정 한 경우에는이를 억제 하는 것이 좋습니다.

이렇게 하려면 다음과 같은 방법을 사용할 수 있습니다. 

> nuget.exe pack nuspec NoWarn = NU5104

## <a name="examples"></a>예

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
