---
title: NuGet CLI setapikey 명령
description: Nuget.exe setapikey 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231229"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey 명령 (NuGet CLI)

**적용 대상:** 패키지 사용, 게시 &bullet; **지원 되는 버전:** 모두

지정 된 서버 URL에 대 한 API 키를 `NuGet.Config`에 저장 하 여 후속 명령에 대해 입력이 필요 하지 않도록 합니다.

## <a name="usage"></a>사용

```cli
nuget setapikey <key> -Source <url> [options]
```

여기서 `<source>`은 서버를 식별 하 고 `<key>`는 저장할 키입니다. `<source>` 생략 하면 nuget.org이 가정 됩니다. 

> [!NOTE]
> API 키는 개인 피드에 인증 하는 데 사용 되지 않습니다. 원본으로 인증 하기 위한 자격 증명을 관리 하려면 [`nuget sources` 명령을](../cli-reference/cli-ref-sources.md) 참조 하세요.
> API 키는 개별 NuGet 서버에서 가져올 수 있습니다. Nuget.org에 대 한 APIKeys를 만들고 관리 하려면 [publish-key](../../quickstart/includes/publish-api-key.md) 를 참조 하세요.

## <a name="options"></a>옵션

| 옵션 | Description |
| --- | --- |
| ConfigFile | 수정할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| ForceEnglishOutput | *(3.5 +)* 고정 영어 기반 문화권을 사용 하 여 nuget.exe를 실행 합니다. |
| 도움말 | 명령어에 대한 도움말을 표시합니다. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보의 양을 지정 합니다. *보통*, *자동*, *자세히*입니다. |

[환경 변수](cli-ref-environment-variables.md) 참조

## <a name="examples"></a>예

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
