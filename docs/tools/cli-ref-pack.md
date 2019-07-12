---
title: NuGet CLI pack 명령
description: Nuget.exe pack 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c3a01b7747be96f02f7b93b3bf66f5d1783ceed7
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842548"
---
# <a name="pack-command-nuget-cli"></a>pack 명령(NuGet CLI)

**적용 대상:** 패키지 만들기 &bullet; **지원 되는 버전:** 2.7+

지정한 NuGet 패키지를 만들어 `.nuspec` 또는 프로젝트 파일입니다. 합니다 `dotnet pack` 명령 (참조 [dotnet 명령](dotnet-Commands.md)) 및 `msbuild -t:pack` (참조 [MSBuild 대상](../reference/msbuild-targets.md)) 대체 항목으로 사용할 수 있습니다.

> [!Important]
> Mono에서 프로젝트 파일에서 패키지를 만들 수 없습니다. 로컬이 아닌 경로 조정 해야 합니다 `.nuspec` Unix 스타일 경로로 파일로 nuget.exe 자체 Windows 경로 이름으로 변환 하지 않습니다.

## <a name="usage"></a>사용법

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

여기서 `<nuspecPath>` 하 고 `<projectPath>` 지정는 `.nuspec` 또는 프로젝트 파일을 각각.

## <a name="options"></a>변수

| 옵션 | Description |
| --- | --- |
| BasePath | 설정에서 정의 된 파일의 기본 경로 `.nuspec` 파일입니다. |
| 빌드 | 프로젝트 패키지를 빌드하기 전에 빌드해야 함을 지정 합니다. |
| 제외 | 패키지를 만들 때를 제외 하려면 와일드 카드 패턴을 하나 이상 지정 합니다. 둘 이상의 패턴을 지정 하려면 반복-제외 플래그입니다. 아래 예제를 참조 하세요. |
| ExcludeEmptyDirectories | 패키지를 작성 하는 경우 빈 디렉터리를 포함을 하지 않습니다. |
| ForceEnglishOutput | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| ConfigFile | Pack 명령에 대 한 구성 파일을 지정 합니다. |
| Help | 명령어에 대한 도움말을 표시합니다. |
| IncludeReferencedProjects | 종속성 또는 패키지의 일부로 작성된 된 패키지에서 참조 된 프로젝트를 포함 해야 함을 나타냅니다. 참조 된 프로젝트에 해당 하는 경우 `.nuspec` 파일 이름이 같은 프로젝트와 해당 참조 된 프로젝트를 종속성으로 추가 됩니다. 그렇지 않으면 참조 된 프로젝트는 패키지의 일부로 추가 됩니다. |
| MinClientVersion | 설정 된 *minClientVersion* 만든된 패키지에 대 한 특성입니다. 이 값은 기존 값을 재정의 *minClientVersion* 특성 (있는 경우)에 `.nuspec` 파일입니다. |
| MSBuildPath | *(4.0 이상)*  보다 우선함 명령으로 사용 하는 MSBuild의 경로 지정 `-MSBuildVersion`합니다. |
| MSBuildVersion | *(3.2 이상)*  이 명령을 사용 하 여 사용할 MSBuild의 버전을 지정 합니다. 지원 되는 값은 4, 12, 14, 15.1, 15.3, 15.4에서 15.5, 15.6, 15.7, 15.8, 15.9. 경로에 MSBuild 선택은 기본적으로 그렇지 않은 경우 기본값은 MSBuild의 설치 된 가장 높은 버전으로 합니다. |
| NoDefaultExcludes | NuGet의 기본 예외 방지 패키지 파일 및 파일 및 폴더와 같은 점부터 `.svn` 고 `.gitignore`입니다. |
| NoPackageAnalysis | 패키지를 빌드한 후 팩에서 패키지 분석을 실행하지 않아야 함을 지정합니다. |
| OutputDirectory | 생성된 된 패키지 저장 되는 폴더를 지정 합니다. 폴더는 지정 하지 않으면 현재 폴더가 사용 됩니다. |
| 속성 | 뒤에 있어야 마지막 명령줄에서 다른 옵션입니다. 프로젝트 파일의 값을 재정의 하는 속성의 목록을 지정 합니다. 참조 [일반적인 MSBuild 프로젝트 속성](/visualstudio/msbuild/common-msbuild-project-properties) 속성 이름에 대 한 합니다. 속성 인수 여기은 토큰의 목록 = 값 쌍을 세미콜론으로 구분 된 여기서 각 `$token$` 에 `.nuspec` 파일을 지정된 된 값으로 바뀝니다. 값은 따옴표로 묶인 문자열일 수 있습니다. "구성" 속성에 대 한 기본값은 "Debug" note 합니다. 릴리스 구성으로 변경 하려면 사용 `-Properties Configuration=Release`합니다. |
| 접미사 | *(3.4.4+)*  빌드 또는 기타 시험판 버전 식별자를 추가 하기 위해 일반적으로 사용 되는 내부적으로 생성 된 버전 번호에 접미사를 추가 합니다. 예를 들어,를 사용 하 여 `-suffix nightly` 버전 번호 like를 사용 하 여 패키지를 만들기는 `1.2.3-nightly`합니다. 접미사는 경고, 오류 및 다른 버전의 NuGet 및 NuGet 패키지 관리자를 사용 하 여 호환성 문제를 방지 하려면 문자로 시작 해야 합니다. |
| 기호 | 소스 및 기호 패키지에 포함 되도록 지정 합니다. 와 함께 사용할 경우는 `.nuspec` 파일인이 일반 NuGet 패키지 파일을 만들고 해당 기호 패키지가 있습니다. 기본적으로 만듭니다는 [레거시 기호 패키지](../create-packages/Symbol-Packages.md)합니다. 기호 패키지에 대한 새 권장 형식은 .snupkg입니다. [기호 패키지(.snupkg) 만들기](../create-packages/Symbol-Packages-snupkg.md)를 참조하세요. |
| SymbolPackageFormat | 기호 패키지의 형식을 지정 합니다. *symbols.nupkg* (레거시) 또는 *snupkg* (권장). 기본적으로 만듭니다는 [레거시 기호 패키지](../create-packages/Symbol-Packages.md)합니다. [기호 패키지(.snupkg) 만들기](../create-packages/Symbol-Packages-snupkg.md)를 참조하세요. |
| 도구 | 프로젝트의 출력 파일에 배치 해야 함을 지정 합니다 `tool` 폴더입니다. |
| Verbosity | 출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다. |
| 버전 | 버전 번호를 재정의 합니다 `.nuspec` 파일입니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="excluding-development-dependencies"></a>개발 종속성 제외

일부 NuGet 패키지는 고유한 라이브러리를 작성 하는 데 도움이 되지만 실제 패키지가 종속성으로 반드시 필요 하지는 개발 종속성으로 유용 합니다.

`pack` 명령을 무시 합니다 `package` 항목에서 `packages.config` 있는 합니다 `developmentDependency` 특성이로 설정 `true`합니다. 이러한 항목을 만든된 패키지의 종속성으로 포함 되지 않습니다.

예를 들어, 다음 사항을 고려 `packages.config` 원본 프로젝트의 파일:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

이 프로젝트에 패키지 하 여 만든 `nuget pack` 종속성을 갖습니다 `jQuery` 하 고 `microsoft-web-helpers` 아닌 `netfx-Guard`합니다.

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
