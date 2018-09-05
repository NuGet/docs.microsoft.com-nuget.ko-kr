---
title: NuGet CLI 구성 명령
description: Nuget.exe config 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 376b69186ad22d4d94a1df51146b833a1f6f9bd9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546480"
---
# <a name="config-command-nuget-cli"></a>구성 명령 (NuGet CLI)

**적용 대상:** 모든 &bullet; **지원 되는 버전**: 모두

NuGet 구성 값을 가져오거나 설정 합니다. 추가 사용량에 대 한 참조 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md)합니다. 허용 되는 키 이름에 대 한 자세한 내용은 참조는 [NuGet 구성 파일 참조](../reference/nuget-config-file.md)합니다.

## <a name="usage"></a>사용법

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

여기서 `<name>` 고 `<value>` 구성에서 설정할 키-값 쌍을 지정 합니다. 필요에 따라 쌍을 지정할 수 있습니다. 값을 제거 하려면 이름을 지정 하며 `=` 로그인 하지만 값이 없습니다.

허용 되는 키 이름에 대 한 참조를 [NuGet 구성 파일 참조](../reference/nuget-config-file.md)합니다.

NuGet 3.4 이상에서는 `<value>` 사용할 수 있습니다 [환경 변수](cli-ref-environment-variables.md)합니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| AsPath | 경로로 구성 값이 반환 될 때 무시 `-Set` 사용 됩니다. |
| ConfigFile | NuGet 구성 파일을 수정 합니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| ForceEnglishOutput | *(3.5 이상)*  고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

### <a name="examples"></a>예제

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
