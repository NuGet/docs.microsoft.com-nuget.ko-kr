---
title: NuGet CLI 소스 명령
description: nuget.exe sources 명령에 대 한 참조
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e9cbdd089c5c0f66d25e7588ece504feae63f2f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780011"
---
# <a name="sources-command-nuget-cli"></a>sources 명령 (NuGet CLI)

**적용 대상:** 패키지 사용, &bullet; **지원 되는 버전 게시:** 모두

사용자 범위 구성 파일 또는 지정 된 구성 파일에 있는 원본 목록을 관리 합니다. 사용자 범위 구성 파일은 `%appdata%\NuGet\NuGet.Config` (Windows) 및 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)에 있습니다.

nuget.org에 대한 원본 URL은 `https://api.nuget.org/v3/index.json`입니다.

## <a name="usage"></a>사용량

```cli
nuget sources <operation> -Name <name> -Source <source>
```

여기서 `<operation>` 는 *목록, 추가, 제거, 사용, 사용 안 함* 또는 *업데이트*, `<name>` 는 원본의 이름, `<source>` 는 소스의 URL입니다. 한 번에 하나의 원본 에서만 작업할 수 있습니다.

## <a name="options"></a>옵션

- **`-ConfigFile`**

  적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.

- **`-ForceEnglishOutput`**

  *(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.

- **`-Format`**

  작업에 적용 `list` 되며 `Detailed` (기본값) 또는 일 수 있습니다 `Short` .

- **`-?|-help`**

  명령에 대 한 도움말 정보를 표시 합니다.

- **`-Name`**

  소스 이름입니다.

- **`-NonInteractive`**

  사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.

- **`-Password`**

  원본으로 인증 하는 데 사용할 암호를 지정 합니다.

- **`-src|-Source`**

  패키지 원본에 대 한 경로입니다.

- **`-StorePasswordInClearText`**

  암호화 된 형식을 저장 하는 기본 동작 대신 암호를 암호화 되지 않은 텍스트로 저장 함을 나타냅니다.

- **`-UserName`**

  원본으로 인증 하는 데 사용할 사용자 이름을 지정 합니다.

- **`-ValidAuthenticationTypes`**

  이 소스에 대한 유효한 인증 형식의 쉼표로 구분된 목록입니다. 기본적으로 모든 인증 유형은 유효 합니다. 예: `basic,negotiate`.

- **`-Verbosity [normal|quiet|detailed]`**

  출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.

> [!Note]
> 나중에 패키지 원본에 액세스 하는 데 사용 되는 nuget.exe 같은 사용자 컨텍스트에서 원본 암호를 추가 해야 합니다. 암호는 구성 파일에 암호화 되어 저장 되며 암호화 된 것과 동일한 사용자 컨텍스트에서 암호를 해독할 수 있습니다. 예를 들어 빌드 서버를 사용 하 여 NuGet 패키지를 복원 하는 경우 암호는 빌드 서버 태스크가 실행 되는 동일한 Windows 사용자로 암호화 되어야 합니다.

[환경 변수](cli-ref-environment-variables.md) 참조

## <a name="examples"></a>예

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
