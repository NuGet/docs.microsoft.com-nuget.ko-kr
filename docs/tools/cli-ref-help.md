---
title: NuGet CLI help 명령
description: Nuget.exe help 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546565"
---
# <a name="help-or--command-nuget-cli"></a>help or ? 명령(NuGet CLI)

**적용 대상:** 모든 &bullet; **지원 되는 버전**: 모두

일반 표시 도움말 정보 및 특정 명령에 대 한 정보입니다.

## <a name="usage"></a>사용법

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

여기서 [command] 도움말을 표시 하려는 특정 명령을 식별 합니다.

> [!Warning]
> 일부 명령을 사용 하 여 되도록 주의 해야 *도움말* 먼저를 사용 하 여 `nuget help install`nuget.org에서 "도움말" 라는 패키지 중이기 때문입니다. 명령을 제공 하는 경우 `nuget install help`, 설치 명령에서 도움을 받으려면지 않습니다 하지만 대신 도움말 라는 패키지를 설치 합니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| Api 키 | 대상 리포지토리에 대한 API 키입니다. 없는 경우 구성 파일에 지정된 값이 사용됩니다. |
| 구성 파일 | 수정할 NuGet 구성 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| 강제로 영어로 출력 | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| 도움말 | 명령어에 대한 도움말을 표시합니다. |
| 마크다운 | `-All` 인수를 사용하는 경우 상세한 도움말을 마크다운 형식으로 출력합니다. 이외의 경우 이 옵션은 무시됩니다. |
| 대화형 모드 사용하지 않기 | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| 로그 출력 레벨 | 출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참고할 수 있습니다.

## <a name="examples"></a>예제

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
