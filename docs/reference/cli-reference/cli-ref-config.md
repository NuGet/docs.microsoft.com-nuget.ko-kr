---
title: NuGet CLI 구성 명령
description: Nuget.exe 구성 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433310"
---
# <a name="config-command-nuget-cli"></a>config 명령 (NuGet CLI)

****모든 버전에서 모두 지원됩니다.**

NuGet 구성 값을 불러오거나 설정할 수 있습니다. 추가 사용에 대해서는 [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md)을 참조 하세요. 사용할 수 있는 키 값에 대한 자세한 내용은 [NuGet 구성 파일 참조](../nuget-config-file.md)를 볼 수 있습니다.

## <a name="usage"></a>사용법

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

여기서 `<name>`과 `<value>`는 구성 파일에서 설정할 키-값 쌍을 지정합니다. 원하는 수 만큼 쌍을 지정할 수 있습니다. 값을 제거하려면 이름과 `=`로 해당 키에 빈 값을 지정해주시면 됩니다.

허용되는 키 이름은 [NuGet 구성 파일 참조](../nuget-config-file.md)에서 확인할 수 있습니다.

NuGet 3.4 이상에서 `<value>`는 [환경 변수](cli-ref-environment-variables.md)를 사용할 수 있습니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| AsPath | 구성 파일의 경로를 반환합니다. `-Set`이 사용될 때 옵션은 무시됩니다. |
| ConfigFile | 수정할 NuGet 설정 파일입니다. 지정 하지 않으면 기본 파일이 (Windows) 또는`%AppData%\NuGet\NuGet.Config` `~/.config/NuGet/NuGet.Config` (Mac/Linux) 또는 `~/.nuget/NuGet/NuGet.Config` (OS 배포에 따라 다름) 사용 됩니다.|
| ForceEnglishOutput | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| Help | 명령어에 대한 도움말을 표시합니다. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| Verbosity | 출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

### <a name="examples"></a>예제

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
