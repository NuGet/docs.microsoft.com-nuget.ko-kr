---
title: NuGet CLI 목록 명령
description: Nuget.exe 목록 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327740"
---
# <a name="list-command-nuget-cli"></a>list 명령 (NuGet CLI)

**적용 대상:** 패키지 사용, &bullet; **지원 되는 버전 게시:** 모두

지정 된 원본의 패키지 목록을 표시 합니다. 소스를 지정 하지 않으면 전역 구성 파일 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config`에 정의 된 모든 소스가 사용 됩니다. 에서 소스를 지정 하지 않는 경우 `NuGet.Config` 는 기본 피드 (nuget.org)를 사용합니다.`list`

## <a name="usage"></a>사용

```cli
nuget list [search terms] [options]
```

여기서 선택적 검색 용어는 표시 된 목록을 필터링 합니다. 검색 용어는 nuget.org에서 사용 하는 경우와 마찬가지로 패키지, 태그 및 패키지 설명의 이름에 적용 됩니다.

## <a name="options"></a>변수

| 옵션 | Description |
| --- | --- |
| Allversions) | 패키지의 모든 버전을 나열 합니다. 기본적으로 최신 패키지 버전만 표시 됩니다. |
| ConfigFile | 적용할 NuGet 설정 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| ForceEnglishOutput | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| Help | 명령어에 대한 도움말을 표시합니다. |
| IncludeDelisted | *(3.2 이상)* 나열 되지 않은 패키지를 표시 합니다. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| PreRelease | 목록에 시험판 패키지를 포함 합니다. |
| Source | 검색할 패키지 원본 목록을 지정 합니다. |
| Verbosity | 출력에 표시되는 세부정보의 양을 지정합니다: *정상적인*, *조용한*, *자세한*합니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="examples"></a>예제

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
