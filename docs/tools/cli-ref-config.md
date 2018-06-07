---
title: NuGet CLI 구성 명령
description: Nuget.exe config 명령에 대 한 참조
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 9deab9fcca740ea99da61b7d54700a29c1813e88
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818167"
---
# <a name="config-command-nuget-cli"></a>구성 명령 (NuGet CLI)

**적용 대상:** 모든 &bullet; **지원 되는 버전**: 모든

NuGet 구성 값을 가져오거나 설정 합니다. 추가 사용에 대 한 참조 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)합니다. 허용 가능한 키 이름에 대 한 자세한 내용은 참조는 [NuGet config 파일 참조](../reference/nuget-config-file.md)합니다.

## <a name="usage"></a>사용법

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

여기서 `<name>` 및 `<value>` 구성에서 설정할 키-값 쌍을 지정 합니다. 필요에 따라 쌍을 지정할 수 있습니다. 값을 제거 하려면 이름을 지정 및 `=` 기호 있지만 값이 없습니다.

허용 가능한 키 이름에 대 한 참조는 [NuGet config 파일 참조](../reference/nuget-config-file.md)합니다.

NuGet 3.4 +에서 `<value>` צ ְ ײ [환경 변수](cli-ref-environment-variables.md)합니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| AsPath | 경로, 구성 값이 반환 될 때 무시 `-Set` 사용 됩니다. |
| ConfigFile | NuGet 구성 파일 수정입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| ForceEnglishOutput | *(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

### <a name="examples"></a>예제

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
