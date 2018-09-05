---
title: NuGet CLI 푸시 명령
description: Nuget.exe push 명령은 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 125671ca3f695f82bd74f8097e590c3972003e22
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548345"
---
# <a name="push-command-nuget-cli"></a>push 명령은 (NuGet CLI)

**적용 대상:** 게시 패키지 &bullet; **지원 되는 버전:** 모든; nuget.org에 필요한 4.1.0 이상

> [!Important]
> Nuget.org에 패키지를 푸시 하려면 사용 해야 nuget.exe v4.1.0 이상, 필수 구현한 [NuGet 프로토콜](../api/nuget-protocols.md)합니다.

패키지 원본에 패키지를 푸시하고 게시 합니다.

NuGet의 기본 구성을 로드 하 여 가져올 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), 모든 로드 한 다음 `Nuget.Config` 하거나 `.nuget\Nuget.Config` 드라이브의 루트에서 시작 하 고 현재 디렉터리에서 끝나는 파일 (참조 [구성 NuGet 동작](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>사용법

```cli
nuget push <packagePath> [options]
```

여기서 `<packagePath>` 서버로 푸시 하려면 패키지를 식별 합니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| ApiKey | 대상 리포지토리에 대 한 API 키입니다. 없는 경우 구성 파일에 지정 된 사용 됩니다. |
| ConfigFile | NuGet 구성 파일을 적용 합니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| DisableBuffering | 메모리 사용량을 줄이려면 http (s) 서버로 푸시할 때 버퍼링 하는 사용 하지 않도록 설정 합니다. 주의:이 옵션을 사용 하는 통합된 Windows 인증 작동 하지 않을 수 있습니다. |
| ForceEnglishOutput | *(3.5 이상)*  고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| NoSymbols | *(3.5 이상)*  기호 패키지가 있으면 해당 푸시되 지 않습니다 기호 서버에 있습니다. |
| 소스 | 서버 URL을 지정합니다. NuGet은 UNC 또는 로컬 폴더 소스를 식별 하 고 간단히 HTTP를 사용 하 여 푸시하는 대신에 있는 파일을 복사 합니다.  또한 NuGet 3.4.2부터이 않는 필수 매개 변수를 `NuGet.Config` 파일 지정을 *DefaultPushSource* 값 (참조 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)). |
| SymbolSource | *(3.5 이상)*  기호 서버 URL을 지정 합니다. 즉 nuget.org에 푸시할 때 nuget.smbsrc.net는 |
| SymbolApiKey | *(3.5 이상)*  에 지정 된 URL에 대 한 API 키를 지정 `-SymbolSource`합니다. |
| 시간 제한 | 서버에 푸시하기 위한 초 제한 시간을 지정 합니다. 기본값은 300 초 (5 분). |
| 자세한 정도 | 출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
