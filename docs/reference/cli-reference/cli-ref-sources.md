---
title: NuGet CLI 소스 명령
description: Nuget.exe 소스 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327600"
---
# <a name="sources-command-nuget-cli"></a>sources 명령(NuGet CLI)

**적용 대상:** 패키지 사용, &bullet; **지원 되는 버전 게시:** 모두

사용자 범위 구성 파일 또는 지정 된 구성 파일에 있는 원본 목록을 관리 합니다. 사용자 범위 구성 파일은 (Windows) `%appdata%\NuGet\NuGet.Config` 및 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)에 있습니다.

nuget.org에 대한 원본 URL은 `https://api.nuget.org/v3/index.json`입니다.

## <a name="usage"></a>사용

```cli
nuget sources <operation> -Name <name> -Source <source>
```

여기서 `<operation>` 는 *목록, 추가, 제거, 사용, 사용 안 함* 또는 *업데이트*, `<name>` 는 원본의 `<source>` 이름,는 소스의 URL입니다. 한 번에 하나의 원본 에서만 작업할 수 있습니다.

## <a name="options"></a>변수

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | 적용할 NuGet 설정 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| ForceEnglishOutput | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| 형식 | `list` 작업에 적용 되며 (기본값) `Detailed` 또는 `Short`일 수 있습니다. |
| Help | 명령어에 대한 도움말을 표시합니다. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| 암호 | 원본으로 인증 하는 데 사용할 암호를 지정 합니다. |
| StorePasswordInClearText | 암호화 된 형식을 저장 하는 기본 동작 대신 암호를 암호화 되지 않은 텍스트로 저장 함을 나타냅니다. |
| UserName | 원본으로 인증 하는 데 사용할 사용자 이름을 지정 합니다. |
| Verbosity | 출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다. |

> [!Note]
> 나중에 nuget.exe를 사용 하 여 패키지 원본에 액세스 하는 것과 같은 사용자 컨텍스트에서 소스의 암호를 추가 해야 합니다. 암호는 구성 파일에 암호화 되어 저장 되며 암호화 된 것과 동일한 사용자 컨텍스트에서 암호를 해독할 수 있습니다. 예를 들어 빌드 서버를 사용 하 여 NuGet 패키지를 복원 하는 경우 암호는 빌드 서버 태스크가 실행 되는 동일한 Windows 사용자로 암호화 되어야 합니다.

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="examples"></a>예제

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
