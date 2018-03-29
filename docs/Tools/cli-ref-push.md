---
title: NuGet CLI 푸시 명령을 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe 푸시 명령에 대 한 참조
keywords: nuget 푸시 참조, 푸시 명령
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 832f7aeb2b485acbb83e5213916fc3423df961ab
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="push-command-nuget-cli"></a>푸시 명령 (NuGet CLI)

**적용 대상:** 게시 패키지 &bullet; **지원 되는 버전:** 모든; 4.1.0+ nuget.org에 필요한

> [!Important]
> Nuget.org를 패키지를 강제를 사용 해야 nuget.exe v4.1.0 +에서 구현 하는 필수는 [NuGet 프로토콜](../api/nuget-protocols.md)합니다.

패키지를 패키지 원본에 푸시합니다를 게시 합니다.

NuGet의 기본 구성을 로드 하 여 가져온 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), 다음 모든 로드 `Nuget.Config` 또는 `.nuget\Nuget.Config` 드라이브의 루트에서 시작 하 고 현재 디렉터리에서 끝나는 파일 (참조 [구성 NuGet 동작](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>사용법

```cli
nuget push <packagePath> [options]
```

여기서 `<packagePath>` 패키지는 서버에 대 한 푸시를 식별 합니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| apiKey | 대상 저장소에 대 한 API 키입니다. 래퍼가 없는 경우 구성 파일에 지정 된 사용 됩니다. |
| ConfigFile | 적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| DisableBuffering | 메모리 사용량을 줄이기 위해 http (s) 서버에 적용할 때 버퍼링 하는 데 사용 하지 않습니다. 주의:이 옵션을 사용 Windows 통합된 인증 작동 하지 않을 수 있습니다. |
| ForceEnglishOutput | *(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| NoSymbols | *(3.5 +)*  기호 패키지 있으면 해당 기호 서버에 푸시되 지 것입니다. |
| 소스 | 서버 URL을 지정합니다. NuGet은 UNC 또는 로컬 폴더 소스를 식별 하 고 간단히 HTTP를 사용 하 여 푸시하는 대신 거기 파일을 복사 합니다.  또한 NuGet 3.4.2 부터는이 표시 되지 않으면 필수 매개 변수는 `NuGet.Config` 파일 지정는 *DefaultPushSource* 값 (참조 [NuGet 구성 동작](../consume-packages/configuring-nuget-behavior.md)). |
| SymbolSource | *(3.5 +)*  기호 서버 URL을 지정 합니다. 즉 nuget.smbsrc.net nuget.org를 푸시할 때 사용 됩니다 |
| SymbolApiKey | *(3.5 +)*  에 지정 된 URL에 대 한 API 키 지정 `-SymbolSource`합니다. |
| 시간 제한 | 서버에 밀어 넣는 초 제한 시간을 지정 합니다. 기본값은 300 초 (5 분)입니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다. |

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
