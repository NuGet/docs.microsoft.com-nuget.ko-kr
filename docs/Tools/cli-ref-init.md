---
title: NuGet CLI init 명령을 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe 초기화 명령에 대 한 참조
keywords: nuget init 참조, init 명령
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 01a3553622020b5868e33ece09cd7555cb712fd3
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="init-command-nuget-cli"></a>초기화 명령 (NuGet CLI)

**적용 대상:** 패키지 만들기가 &bullet; **지원 되는 버전:** 3.3 +

에 대 한 설명 된 대로 계층 레이아웃을 사용 하 여 대상 폴더를 단일 폴더에서 모든 패키지를 복사는 [명령을 추가](cli-ref-add.md)합니다. 즉, 사용 하 여 `init` 사용 하는 `add` 폴더에 각 패키지에 명령 합니다.

와 마찬가지로 `add`, 대상 로컬 폴더 또는 UNC 경로 여야 합니다 Nuget.org 또는 개인 서버와 같이 HTTP 패키지 저장소는 지원 되지 않습니다.

## <a name="usage"></a>사용법

```cli
nuget init <source> <destination> [options]
```

여기서 `<source>` 는 패키지가 포함 된 폴더 및 `<destination>` 로컬 폴더 인지 패키지 복사 되는 UNC 경로 이름입니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | 적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| ForceEnglishOutput | *(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| Expand | 모든 파일은 패키지 소스에 추가 된 각 패키지에 추가 와 동일 `-Expand` 와 `add` 명령입니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
