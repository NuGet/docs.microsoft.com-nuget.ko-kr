---
title: NuGet CLI 도움말 명령
description: nuget.exe 도움말 명령에 대 한 참조
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5d91638c4a6f167ea8a04e5dfa2905cb55084ddd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779356"
---
# <a name="help-or--command-nuget-cli"></a>help or ? command (NuGet CLI)

**적용 대상:** &bullet; **지원 되** 는 모든 버전: 모두

일반 도움말 정보 및 특정 명령에 대 한 도움말 정보를 표시 합니다.

## <a name="usage"></a>사용량

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

여기서 [command]는 도움말을 표시할 특정 명령을 식별 합니다.

> [!Warning]
>  `nuget help install` Nuget.org에 "help" 라는 패키지가 있기 때문에 몇 가지 명령을 사용 하 여에 대 한 도움말을 먼저 지정 하는 것에 유의 해야 합니다. 명령을 지정 하면 `nuget install help` install 명령에 대 한 도움말을 볼 수 없지만 대신 help 라는 이름의 패키지를 설치 합니다.

## <a name="options"></a>옵션

- **`-All`**

  사용 가능한 모든 명령에 대 한 자세한 도움말을 인쇄 합니다. 특정 명령이 지정 된 경우 무시 됩니다.

- **`-ConfigFile`**

  적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.

- **`-ForceEnglishOutput`**

  *(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.

- **`-?|-help`**

  명령에 대 한 도움말 정보를 표시 합니다.

- **`-Markdown`**

  에서 사용 하는 경우 자세한 도움말을 markdown 형식으로 인쇄 `-All` 합니다. 그렇지 않으면 무시 됩니다.

- **`-NonInteractive`**

  사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.

- **`-Verbosity [normal|quiet|detailed]`**

  출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.

[환경 변수](cli-ref-environment-variables.md) 참조

## <a name="examples"></a>예

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
