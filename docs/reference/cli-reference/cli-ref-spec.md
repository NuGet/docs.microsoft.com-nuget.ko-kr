---
title: NuGet CLI 사양 명령
description: nuget.exe spec 명령에 대 한 참조
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b7780ee5d2e722da5e1623f44709059dd9aa3d45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779142"
---
# <a name="spec-command-nuget-cli"></a>spec 명령 (NuGet CLI)

**적용 대상:** 패키지 만들기 &bullet; **지원 되는 버전:** 모두

`.nuspec`새 패키지에 대 한 파일을 생성 합니다. 프로젝트 파일 (,,)과 동일한 폴더에서 실행 `.csproj` 되는 경우 `.vbproj` `.fsproj` `spec` 토큰화 된 파일을 만듭니다 `.nuspec` . 자세한 내용은 [패키지 만들기](../../create-packages/creating-a-package.md)를 참조 하세요.

## <a name="usage"></a>사용량

```cli
nuget spec [<packageID>] [options]
```

여기서 `<packageID>` 은 파일에 저장할 선택적 패키지 식별자입니다 `.nuspec` .

## <a name="options"></a>옵션

- **`-AssemblyPath`**

  메타 데이터에 사용할 어셈블리의 경로를 지정 합니다.

- **`-Force`**

  기존 `.nuspec` 파일을 덮어씁니다.


- **`-ForceEnglishOutput`**

  *(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.

- **`-?|-help`**

  명령에 대 한 도움말 정보를 표시 합니다.

- **`-NonInteractive`**

  사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.

- **`-Verbosity [normal|quiet|detailed]`**

  출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.

[환경 변수](cli-ref-environment-variables.md) 참조

## <a name="examples"></a>예

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
