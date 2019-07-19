---
title: NuGet CLI add 명령
description: Nuget.exe add 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327860"
---
# <a name="add-command-nuget-cli"></a>add 명령(NuGet CLI)

**적용 대상**: 패키지 게시 &bullet; **지원 버전**: 3.3+

특정한 패키지를 폴더나 UNC 경로와 같은 비 HTTP 패키지 소스에 패키지 이름과 버전 번호로 된 폴더 내부에 계층 레이아웃으로 추가합니다. 예를 들어:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

해당 패키지에 대한 복원이나 업데이트를 할 때, 위와 같은 계층 레이아웃은 더 나은 성능을 제공합니다.

원하는 패키지 소스 폴더 내부의 모든 파일을 확장하려면 `-Expand`를 사용하여 전환합니다. 일반적으로 `tools` 와 `lib`이라는 추가적인 하위폴더가 목적지 폴더 내부에 보일 수 있습니다.

## <a name="usage"></a>사용법

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

여기서 `<packagePath>`는 추가하고자 하는 패키지의 위치를, `<sourcePath>`는 추가할 패키지 소스의 위치를 의미합니다. HTTP 소스는 지원되지 않습니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| ConfigFile | 적용할 NuGet 설정 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| Expand | 패키지의 원본에 있는 모든 파일을 추가합니다. |
| ForceEnglishOutput | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| Help | 명령어에 대한 도움말을 표시합니다. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| Verbosity | 출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="examples"></a>예제

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
