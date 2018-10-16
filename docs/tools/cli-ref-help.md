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
| 모두 | 사용 가능한 명령 모두;에 대 한 자세한 도움말을 인쇄 특정 명령을 지정 하는 경우 무시 됩니다. |
| ConfigFile | NuGet 구성 파일을 적용 합니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| ForceEnglishOutput | *(3.5 이상)*  고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말 도움말 명령 자체에 대 한 정보를 표시 합니다. |
| Markdown | 마크 다운 형식으로 사용 하는 경우 자세한 도움말을 인쇄 `-All`합니다. 그렇지 않으면 무시 됩니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다. |
또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
