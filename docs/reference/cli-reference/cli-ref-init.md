---
title: NuGet CLI init 명령
description: nuget.exe init 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3b830d678a473c917b70bd46900bdb0206d3652e
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623086"
---
# <a name="init-command-nuget-cli"></a>init 명령 (NuGet CLI)

**적용 대상:** 패키지 만들기 &bullet; **지원 되는 버전:** 3.3 이상

[추가 명령](cli-ref-add.md)에 설명 된 대로 계층적 레이아웃을 사용 하 여 플랫 폴더의 모든 패키지를 대상 폴더에 복사 합니다. 즉,를 사용 하는 것 `init` 은 `add` 폴더의 각 패키지에 대해 명령을 사용 하는 것과 같습니다.

와 마찬가지로 `add` 대상은 로컬 폴더 또는 UNC 경로 여야 합니다. Nuget.org 또는 private 서버와 같은 HTTP 패키지 리포지토리는 지원 되지 않습니다.

## <a name="usage"></a>사용량

```cli
nuget init <source> <destination> [options]
```

여기서 `<source>` 는 패키지가 포함 된 폴더이 고 `<destination>` 은 패키지가 복사 되는 로컬 폴더 또는 UNC 경로 이름입니다.

## <a name="options"></a>옵션

- **`-ConfigFile`**

  적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.

- **`-Expand`**

  패키지 소스에 추가 된 각 패키지의 모든 파일을 추가 합니다. `-Expand` 명령을 사용 하는 것과 같습니다 `add` .

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
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
