---
title: NuGet CLI init 명령
description: Nuget.exe init 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327780"
---
# <a name="init-command-nuget-cli"></a>init 명령 (NuGet CLI)

**적용 대상:** 패키지 만들기 &bullet; **지원 되는 버전:** 3.3+

[추가 명령](cli-ref-add.md)에 설명 된 대로 계층적 레이아웃을 사용 하 여 플랫 폴더의 모든 패키지를 대상 폴더에 복사 합니다. 즉,를 사용 `init` 하는 것은 폴더 `add` 의 각 패키지에 대해 명령을 사용 하는 것과 같습니다.

와 `add`마찬가지로 대상은 로컬 폴더 또는 UNC 경로 여야 합니다. Nuget.org 또는 private 서버와 같은 HTTP 패키지 리포지토리는 지원 되지 않습니다.

## <a name="usage"></a>사용법

```cli
nuget init <source> <destination> [options]
```

여기서 `<source>` 는 패키지가 포함 된 폴더이 `<destination>` 고은 패키지가 복사 되는 로컬 폴더 또는 UNC 경로 이름입니다.

## <a name="options"></a>변수

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | 적용할 NuGet 설정 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| ForceEnglishOutput | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| Expand | 패키지 소스에 추가 된 각 패키지의 모든 파일을 추가 합니다. 명령을 사용 `-Expand` 하는 `add` 것과 같습니다. |
| Help | 명령어에 대한 도움말을 표시합니다. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| Verbosity | 출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="examples"></a>예제

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
