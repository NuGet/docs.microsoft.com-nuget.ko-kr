---
title: NuGet CLI add 명령
description: nuget.exe add 명령에 대 한 참조
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 096d2f7a61a3c861ce2084368500ab8e8b21f212
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776098"
---
# <a name="add-command-nuget-cli"></a>add 명령 (NuGet CLI)

**적용 대상**: 패키지 게시 &bullet; **지원 버전**: 3.3 이상

패키지 ID 및 버전 번호에 대 한 폴더를 만드는 계층적 레이아웃에서 HTTP가 아닌 패키지 원본 (폴더 또는 UNC 경로)에 지정 된 패키지를 추가 합니다. 예를 들면 다음과 같습니다.

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

패키지 원본에 대해 복원 하거나 업데이트 하는 경우 계층적 레이아웃을 통해 성능이 크게 향상 됩니다.

패키지의 모든 파일을 대상 패키지 원본으로 확장 하려면 스위치를 사용 `-Expand` 합니다. 이 경우 일반적으로 및와 같은 추가 하위 폴더가 대상에 나타납니다 `tools` `lib` .

## <a name="usage"></a>사용량

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

여기서 `<packagePath>` 는 추가할 패키지의 경로 이름 이며,는 `<sourcePath>` 패키지를 추가할 폴더 기반 패키지 원본을 지정 합니다. HTTP 원본은 지원 되지 않습니다.

## <a name="options"></a>옵션

- **`-ConfigFile`**

  적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.

- **`-Expand`**

  패키지 소스에 패키지의 모든 파일을 추가 합니다.

- **`-ForceEnglishOutput`**

  *(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.
고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.

- **`-?|-help`**

  명령에 대 한 도움말 정보를 표시 합니다.

- **`-NonInteractive`**

  사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.

- **`-src|-Source`**

   Nupkg이 추가 될 폴더 또는 UNC 공유 인 패키지 원본을 지정 합니다. Http 원본은 지원 되지 않습니다.

- **`-Verbosity [normal|quiet|detailed]`**

  출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.

[환경 변수](cli-ref-environment-variables.md) 참조

## <a name="examples"></a>예

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
