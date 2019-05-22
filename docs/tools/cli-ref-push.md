---
title: NuGet CLI 푸시 명령
description: Nuget.exe push 명령은 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bce04864224a66019a52cdfff8355f68dc424204
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65974997"
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
| ApiKey | 대상 리포지토리에 대한 API 키입니다. 없는 경우 구성 파일에 지정 된 사용 됩니다. |
| ConfigFile | 적용할 NuGet 설정 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| DisableBuffering | 메모리 사용량을 줄이려면 http (s) 서버로 푸시할 때 버퍼링 하는 사용 하지 않도록 설정 합니다. 주의:이 옵션을 사용 하는 통합된 Windows 인증 작동 하지 않을 수 있습니다. |
| ForceEnglishOutput | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| Help | 명령어에 대한 도움말을 표시합니다. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| NoSymbols | *(3.5 이상)*  기호 패키지가 있으면 해당 푸시되 지 않습니다 기호 서버에 있습니다. |
| Source | 서버 URL을 지정합니다. NuGet은 UNC 또는 로컬 폴더 소스를 식별 하 고 간단히 HTTP를 사용 하 여 푸시하는 대신에 있는 파일을 복사 합니다.  또한 NuGet 3.4.2부터이 않는 필수 매개 변수를 `NuGet.Config` 파일 지정을 *DefaultPushSource* 값 (참조 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)). |
| SkipDuplicate | 패키지 및 버전이 이미 있는 경우 해당 건너뛰고 있는 경우 푸시에서 다음 패키지를 사용 하 여 계속 합니다. |
| SymbolSource | *(3.5 이상)*  기호 서버 URL을 지정 합니다. 즉 nuget.org에 푸시할 때 nuget.smbsrc.net는 |
| SymbolApiKey | *(3.5 이상)*  에 지정 된 URL에 대 한 API 키를 지정 `-SymbolSource`합니다. |
| 제한 시간 | 서버에 푸시하기 위한 초 제한 시간을 지정 합니다. 기본값은 300 초 (5 분). |
| Verbosity | 출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="examples"></a>예제

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
