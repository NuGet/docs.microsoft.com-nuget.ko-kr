---
title: NuGet CLI setapikey 명령
description: nuget.exe setapikey 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b84d4257c580f6e734c26ebfc589be27bea10c82
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622813"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey 명령 (NuGet CLI)

**적용 대상:** 패키지 사용, &bullet; **지원 되는 버전 게시:** 모두

지정 된 서버 URL에 대 한 API 키를에 저장 하 여 `NuGet.Config` 후속 명령에 대해 입력이 필요 하지 않도록 합니다.

## <a name="usage"></a>사용량

```cli
nuget setapikey <key> -Source <url> [options]
```

여기서는 `<source>` 서버를 식별 하 고 `<key>` 는 저장할 키입니다. `<source>`을 생략 하면 nuget.org이 가정 됩니다. 

> [!NOTE]
> API 키는 개인 피드에 인증 하는 데 사용 되지 않습니다. 원본으로 인증 하기 위한 자격 증명을 관리 하려면 [ `nuget sources` 명령을](../cli-reference/cli-ref-sources.md) 참조 하세요.
> API 키는 개별 NuGet 서버에서 가져올 수 있습니다. Nuget.org에 대 한 APIKeys를 만들고 관리 하려면- [api 키](../../nuget-org/scoped-api-keys.md#acquire-an-api-key) 를 참조 하세요.

## <a name="options"></a>옵션

- **`-ConfigFile`**

  적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.

- **`-ForceEnglishOutput`**

  *(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.

- **`-?|-help`**

  명령에 대 한 도움말 정보를 표시 합니다.

- **`-NonInteractive`**

  사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.

- **`-src|-Source`**

  API 키가 유효한 서버 URL입니다.

- **`-Verbosity [normal|quiet|detailed]`**

  출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.

[환경 변수](cli-ref-environment-variables.md) 참조

## <a name="examples"></a>예

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
