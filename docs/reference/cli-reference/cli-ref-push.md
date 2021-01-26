---
title: NuGet CLI push 명령
description: nuget.exe push 명령에 대 한 참조
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 54a09361173ae10040433b05fcfae7304e39452e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779192"
---
# <a name="push-command-nuget-cli"></a>push 명령 (NuGet CLI)

**적용 대상:** 패키지 게시 &bullet; **지원 버전:** 모두, 4.1.0 + nuget.org에 필요 합니다.

> [!Important]
> Nuget.org에 패키지를 푸시 하려면 필요한 [nuget 프로토콜](../../api/nuget-protocols.md)을 구현 하는 nuget.exe v 4.1.0 +를 사용 해야 합니다.

패키지 소스에 패키지를 푸시하고 게시 합니다.

NuGet의 기본 구성은 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)를 로드 한 다음 `Nuget.Config` `.nuget\Nuget.Config` 드라이브의 루트에서 시작 하 여 현재 디렉터리에서 끝나는 또는 파일을 로드 하 여 가져옵니다 ( [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md)참조).

## <a name="usage"></a>사용량

```cli
nuget push <packagePath> [options]
```

여기서는 `<packagePath>` 서버에 푸시할 패키지를 식별 합니다.

## <a name="options"></a>옵션

- **`-ApiKey`**

  대상 리포지토리의 API 키입니다. 존재 하지 않는 경우 구성 파일에 지정 된 항목을 사용 합니다.

- **`-ConfigFile`**

  적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.

- **`-DisableBuffering`**

  메모리 사용을 줄이기 위해 HTTP (s) 서버로 푸시할 때 버퍼링을 사용 하지 않습니다. 주의:이 옵션을 사용 하는 경우 Windows 통합 인증이 작동 하지 않을 수 있습니다.

- **`-ForceEnglishOutput`**

  *(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.

- **`-?|-help`**

  명령에 대 한 도움말 정보를 표시 합니다.

- **`-NonInteractive`**

  사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.

- **`-NoServiceEndpoint`**

  `api/v2/packages`원본 URL에를 추가 하지 않습니다.

- **`-NoSymbols`**

  *(3.5 +)* 기호 패키지가 있으면 기호 서버에 푸시되 지 않습니다.

- **`-src|-Source`**

  서버 URL을 지정합니다. NuGet은 UNC 또는 로컬 폴더 소스를 식별하며, HTTP를 사용하여 파일을 푸시하는 대신 단순히 파일을 복사합니다.  또한 NuGet 3.4.2 부터는이 `NuGet.Config` 파일이 *Defaultpushsource* 값을 지정 하지 않는 한 필수 매개 변수입니다 ( [NuGet 동작 구성](../../consume-packages/configuring-nuget-behavior.md)참조).

- **`-SkipDuplicate`**

  *(5.1 이상)* 패키지와 버전이 이미 있는 경우이를 건너뛰고 밀어넣기 (있는 경우)에서 다음 패키지를 계속 합니다.

- **`-SymbolSource`**

  *(3.5 +)* 기호 서버 URL을 지정 합니다. nuget.smbsrc.net는 nuget.org에 푸시할 때 사용 됩니다.

- **`-SymbolApiKey`**

  *(3.5 +)* 에 지정 된 URL에 대 한 API 키를 지정 합니다 `-SymbolSource` .

- **`-Timeout`**

  서버에 푸시하는 제한 시간 (초)을 지정 합니다.  기본값은 300초(5분)입니다.

- **`-Verbosity [normal|quiet|detailed]`**

  출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.


[환경 변수](cli-ref-environment-variables.md) 참조

## <a name="examples"></a>예

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
