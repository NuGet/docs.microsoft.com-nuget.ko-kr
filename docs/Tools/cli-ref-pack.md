---
title: "NuGet CLI 팩 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 55e9e4d2-8039-4e9b-bdd9-c8b3eb0e894b
description: "Nuget.exe 팩 명령에 대 한 참조"
keywords: "nuget 팩 참조 팩 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 22643ee4c7d5f858da728ba9d9d2886d600d20f0
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/05/2018
---
# <a name="pack-command-nuget-cli"></a>팩 명령 (NuGet CLI)

**적용 대상:** 패키지 만들기가 &bullet; **지원 되는 버전:** 2.7 +

지정 된 기준 NuGet 패키지를 만들어 `.nuspec` 또는 프로젝트 파일입니다. `dotnet pack` 명령 (참조 [dotnet 명령을](dotnet-Commands.md)) 및 `msbuild /t:pack` (참조 [MSBuild 대상](../schema/msbuild-targets.md)) 안으로 사용할 수 있습니다.

> [!Important]
> 모노, 아래에서 프로젝트 파일에서 패키지를 만드는 지원 되지 않습니다. 로컬이 아닌 경로 조정 해야 할 수도 있습니다는 `.nuspec` Unix 스타일 경로 파일 nuget.exe Windows 경로 이름 자체를 변환 하지 않습니다.

## <a name="usage"></a>사용법

```
nuget pack <nuspecPath | projectPath> [options]
```

여기서 `<nuspecPath>` 및 `<projectPath>` 지정는 `.nuspec` 또는 프로젝트 파일을 각각.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| BasePath | 에 정의 된 파일의 기본 경로 설정의 `.nuspec` 파일입니다. |
| 빌드 | 패키지를 빌드하기 전에 프로젝트를 빌드해야 함을 지정 합니다. |
| 제외 | 패키지를 만들 때를 제외 하려면 와일드 카드 패턴을 하나 이상 지정 합니다. |
| ExcludeEmptyDirectories | 패키지를 작성 하는 경우 빈 디렉터리를 포함을 하지 않습니다. |
| ForceEnglishOutput | *(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| IncludeReferencedProjects | 종속성으로 또는 패키지의 일부로 서 빌드된 패키지에서 참조 된 프로젝트를 포함 해야 함을 나타냅니다. 참조 된 프로젝트에 해당 하는 경우 `.nuspec` 참조 된 프로젝트는 종속성으로 추가 됩니다 한 다음 프로젝트와 동일한 이름을 가진 파일을 합니다. 그렇지 않은 경우 참조 된 프로젝트는 패키지의 일부로 추가 됩니다. |
| MinClientVersion | 설정의 *minClientVersion* 생성된 된 패키지에 대 한 특성입니다. 이 값은 기존 값을 재정의 하는 것 *minClientVersion* 특성 (있는 경우)에 `.nuspec` 파일입니다. |
| MSBuildPath | *(4.0 이상)*  우선 순위를 차지 명령으로 사용 하는 MSBuild의 경로 지정 `-MSBuildVersion`합니다. |
| MSBuildVersion | *(3.2 +)*  이 명령과 함께 사용할 MSBuild의 버전을 지정 합니다. 지원 되는 값은 4, 12, 14, 15입니다. 경로에 MSBuild 선택은 기본적으로 그렇지 않은 경우 기본값이 가장 높은 설치 된 버전의 MSBuild 됩니다. |
| NoDefaultExcludes | NuGet의 기본 예외 방지 패키지 파일 및 파일 및 폴더와 같은 점으로 시작 `.svn` 및 `.gitignore`합니다. |
| NoPackageAnalysis | 패키지를 빌드한 후 팩에서 패키지 분석을 실행하지 않아야 함을 지정합니다. |
| OutputDirectory | 생성된 된 패키지 저장 된 폴더를 지정 합니다. 없는 폴더를 지정 하는 경우 현재 폴더가 사용 됩니다. |
| 속성 | 프로젝트 파일;의 값을 재정의 하는 속성의 목록을 지정 합니다. 참조 [일반적인 MSBuild 프로젝트 속성](/visualstudio/msbuild/common-msbuild-project-properties) 속성 이름에 대 한 합니다. 여기에 속성 인수는 토큰의 목록 = 값 쌍을 세미콜론으로 구분 하 여기서 발생할 때마다 `$token$` 에 `.nuspec` 파일이 지정된 된 값으로 바뀝니다. 따옴표로 문자열 일 수 있습니다. "구성" 속성에 대 한 기본값은 "Debug" note 합니다. 릴리스 구성으로 변경 하려면 사용 `-Properties Configuration=Release`합니다. |
| 접미사 | *(3.4.4+)*  빌드 또는 기타 시험판 버전 식별자를 추가 하기 위한 일반적으로 사용 되는 내부적으로 생성 된 버전 번호에 접미사를 추가 합니다. 예를 들어,를 사용 하 여 `-suffix nightly` 버전 번호 like 패키지를 만듭니다 `1.2.3-nightly`합니다. 접미사는 경고, 오류 및 다른 버전의 NuGet과 NuGet 패키지 관리자 잠재적인 호환성 문제를 방지 하기 위해 문자로 시작 해야 합니다. |
| 기호 | 소스 및 기호 패키지에 포함 되도록 지정 합니다. 와 함께 사용할 경우는 `.nuspec` 해당 기호 패키지 하 고 파일을 일반 NuGet 패키지 파일이 만들어집니다. |
| 도구 | 프로젝트의 출력 파일에 배치할를 지정 된 `tool` 폴더입니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *세부 (2.5 이상)*합니다. |
| 버전 | 버전 번호를 재정의 `.nuspec` 파일입니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>개발 종속성을 제외

일부 NuGet 패키지가 라이브러리를 작성 하는 데 도움이 되지만 반드시 실제 패키지 종속성으로 필요 하지 않은 개발 종속 항목으로 유용 합니다.

`pack` 명령에서 무시 `package` 항목 `packages.config` 있는 `developmentDependency` 특성이로 설정 `true`합니다. 이러한 항목을 만든된 패키지에서 종속성으로 포함 되지 않습니다.

예를 들어, 다음 사항을 고려 `packages.config` 소스 프로젝트 파일에에서:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

이 프로젝트에 대 한 패키지에서 만든 `nuget pack` 한 종속성을 설정한 `jQuery` 및 `microsoft-web-helpers` 아닌 `netfx-Guard`합니다.

## <a name="examples"></a>예제

```
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5
```
