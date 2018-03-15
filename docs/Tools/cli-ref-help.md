---
title: "NuGet CLI 도움말 명령을 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 도움말 명령에 대 한 참조"
keywords: "nuget 도움말 참조, 도움말 명령"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 281c6ccc7c58d153280441430be063d9ee89955d
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="help-or--command-nuget-cli"></a>도움말 또는? 명령 (NuGet CLI)

**적용 대상:** 모든 &bullet; **지원 되는 버전**: 모든

일반 표시 도움말 정보 및 특정 명령에 대 한 정보를 지원 합니다.

## <a name="usage"></a>사용법

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

여기서 [command] 도움말을 표시 하려는 특정 명령을 식별 합니다.

> [!Warning]
> 일부 명령으로 지정 하려면 주의 해야 *도움말* 와 함께으로 first `nuget help install`nuget.org에 "help" 라는 패키지 이므로, 합니다. 명령을 제공 하는 경우 `nuget install help`를에 설치 명령을 도움말은 가져올 없지만 대신 도움말 라는 패키지를 설치 합니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| 모두 | 사용 가능한 모든 명령;에 대 한 자세한 도움말이 인쇄 특정 명령을 지정 하는 경우 무시 됩니다. |
| ConfigFile | 적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| ForceEnglishOutput | *(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말 도움말 명령 자체에 대 한 정보를 표시 합니다. |
| Markdown | 마크 다운 형태로 함께 사용할 경우 자세한 도움말을 인쇄 `-All`합니다. 그렇지 않은 경우 무시 됩니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
