---
title: NuGet CLI 도움말 명령
description: Nuget.exe 도움말 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327800"
---
# <a name="help-or--command-nuget-cli"></a>help or ? 명령(NuGet CLI)

****모든 버전에서 모두 지원됩니다.**

일반 도움말 정보 및 특정 명령에 대 한 도움말 정보를 표시 합니다.

## <a name="usage"></a>사용법

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

여기서 [command]는 도움말을 표시할 특정 명령을 식별 합니다.

> [!Warning]
> Nuget.org에 "help" 라는 패키지가 있기  때문에 몇 가지 명령을 `nuget help install`사용 하 여에 대 한 도움말을 먼저 지정 하는 것에 유의 해야 합니다. 명령을 `nuget install help`지정 하면 install 명령에 대 한 도움말을 볼 수 없지만 대신 help 라는 이름의 패키지를 설치 합니다.

## <a name="options"></a>변수

| 옵션 | Description |
| --- | --- |
| 모두 | 사용 가능한 모든 명령에 대 한 자세한 도움말을 인쇄 합니다. 특정 명령이 지정 된 경우 무시 됩니다. |
| ConfigFile | 적용할 NuGet 설정 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| ForceEnglishOutput | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| Help | 도움말 명령 자체에 대 한 도움말 정보를 표시 합니다. |
| Markdown | 에서 사용 하 `-All`는 경우 자세한 도움말을 markdown 형식으로 인쇄 합니다. 그렇지 않으면 무시 됩니다. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| Verbosity | 출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="examples"></a>예제

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
