---
title: NuGet CLI 명령 원본
description: Nuget.exe에 대 한 참조 원본 명령
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610628"
---
# <a name="sources-command-nuget-cli"></a>sources 명령(NuGet CLI)

**적용 대상:** 패키지 사용, 게시 &bullet; **지원 되는 버전:** 모든

사용자 범위 구성 파일 또는 지정된 된 구성 파일에 있는 원본 목록을 관리 합니다. 사용자 범위 구성 파일에 위치한 `%appdata%\NuGet\NuGet.Config` (Windows) 및 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

nuget.org에 대한 원본 URL은 `https://api.nuget.org/v3/index.json`입니다.

## <a name="usage"></a>사용법

```cli
nuget sources <operation> -Name <name> -Source <source>
```

여기서 `<operation>` 중 하나인 *나열, 추가, 제거, 설정, 해제* 또는 *업데이트*를 `<name>` 원본의 이름 및 `<source>` 소스의 URL입니다. 한 번에 하나의 원본에서 작동할 수 있습니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | 적용할 NuGet 설정 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| ForceEnglishOutput | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| 형식 | 에 적용 합니다 `list` 작업 수 `Detailed` (기본값) 또는 `Short`합니다. |
| Help | 명령어에 대한 도움말을 표시합니다. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| 암호 | 소스를 사용 하 여 인증 하기 위한 암호를 지정 합니다. |
| StorePasswordInClearText | 암호화 된 폼을 저장 하는 기본 동작 대신 암호화 되지 않은 텍스트에서 암호를 저장 하려면이 옵션을 나타냅니다. |
| UserName | 소스를 사용 하 여 인증에 대 한 사용자 이름을 지정 합니다. |
| Verbosity | 출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다. |

> [!Note]
> 패키지 원본에 액세스 하려면 nuget.exe를 나중에 사용 되는 동일한 사용자 컨텍스트에서 소스를 암호를 추가 해야 합니다. 암호 구성 파일에 암호화 되어 저장 될 하며만 해독할 수 동일한 사용자 컨텍스트에서 암호화 되었습니다. 예를 들어 사용 하는 경우 빌드 서버에 빌드 서버 작업이 실행 될 동일한 Windows 사용자를 사용 하 여 암호를 암호화 해야 하는 NuGet 패키지를 복원 합니다.

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="examples"></a>예제

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
