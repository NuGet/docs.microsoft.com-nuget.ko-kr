---
title: NuGet CLI setapikey 명령
description: Nuget.exe setapikey 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383971"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey 명령 (NuGet CLI)

**적용 대상:** 패키지 사용, 게시 &bullet; **지원 되는 버전:** 모두

지정 된 서버 URL에 대 한 API 키를 `NuGet.Config`에 저장 하 여 후속 명령에 대해 입력이 필요 하지 않도록 합니다.

## <a name="usage"></a>용도

```cli
nuget setapikey <key> -Source <url> [options]
```

여기서 `<source>`은 서버를 식별 하 고 `<key>`는 저장할 키 또는 암호입니다. `<source>` 생략 하면 nuget.org이 가정 됩니다.

> [!NOTE]
> API 키는 개인 피드에 인증 하는 데 사용 되지 않습니다. 원본으로 인증 하기 위한 자격 증명을 관리 하려면 [`nuget sources` 명령을](../cli-reference/cli-ref-sources.md) 참조 하세요.

## <a name="options"></a>Options

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | 수정할 NuGet 구성 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| ForceEnglishOutput | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| 도움말 | 명령어에 대한 도움말을 표시합니다. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="examples"></a>예

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
