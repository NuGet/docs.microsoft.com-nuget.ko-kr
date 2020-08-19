---
title: NuGet CLI 구성 명령
description: nuget.exe config 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7d0c1c51f40cba9a5b69f209ffbd995451bfeb9f
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622878"
---
# <a name="config-command-nuget-cli"></a>config 명령 (NuGet CLI)

**적용 대상:** &bullet; **지원 되**는 모든 버전: 모두

NuGet 구성 값을 가져오거나 설정 합니다. 추가 사용에 대해서는 [일반적인 NuGet 구성](../../consume-packages/configuring-nuget-behavior.md)을 참조 하세요. 허용 되는 키 이름에 대 한 자세한 내용은 [NuGet 구성 파일 참조](../nuget-config-file.md)를 참조 하세요.

## <a name="usage"></a>사용량

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

여기서 `<name>` 및는 `<value>` 구성에서 설정할 키-값 쌍을 지정 합니다. 원하는 수 만큼 쌍을 지정할 수 있습니다. 값을 제거 하려면 이름 및 기호를 지정 하 고 값은 지정 `=` 하지 마십시오.

허용 되는 키 이름에 대해서는 [NuGet 구성 파일 참조](../nuget-config-file.md)를 참조 하세요.

NuGet 3.4 이상에서는 `<value>` [환경 변수](cli-ref-environment-variables.md)를 사용할 수 있습니다.

## <a name="options"></a>옵션


- **`AsPath`**

  구성 값을 경로로 반환 하 고가 사용 될 때 무시 됩니다 `-Set` .

- **`-ConfigFile`**

  적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.

- **`-ForceEnglishOutput`**

  *(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.

- **`-?|-help`**

  명령에 대 한 도움말 정보를 표시 합니다.

- **`-NonInteractive`**

  사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.

- **`-Set`**

  구성에 설정할 키-값 쌍이 하나 이상 있습니다.

- **`-Verbosity [normal|quiet|detailed]`**

  출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.

[환경 변수](cli-ref-environment-variables.md) 참조

### <a name="examples"></a>예

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
