---
title: NuGet CLI 목록 명령
description: Nuget.exe 목록 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813340"
---
# <a name="list-command-nuget-cli"></a>list 명령 (NuGet CLI)

**적용 대상:** 패키지 사용, 게시 &bullet; **지원 되는 버전:** 모두

지정 된 원본의 패키지 목록을 표시 합니다. 원본을 지정 하지 않으면 전역 구성 파일 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config`에 정의 된 모든 소스가 사용 됩니다. `NuGet.Config`에서 소스를 지정 하지 않으면 `list` 기본 피드 (nuget.org)를 사용 합니다.

## <a name="usage"></a>용도

```cli
nuget list [search terms] [options]
```

여기서 선택적 검색 용어는 표시 된 목록을 필터링 합니다. 검색 용어는 nuget.org에서 사용 하는 경우와 마찬가지로 패키지, 태그 및 패키지 설명의 이름에 적용 됩니다.

## <a name="options"></a>Options

| 옵션 | 설명 |
| --- | --- |
| AllVersions | 패키지의 모든 버전을 나열 합니다. 기본적으로 최신 패키지 버전만 표시 됩니다. |
| ConfigFile | 수정할 NuGet 구성 파일입니다. 지정하지 않으면 기본적으로 Windows에서는 `%AppData%\NuGet\NuGet.Config`, Mac이나 Linux에서는 `~/.nuget/NuGet/NuGet.Config`가 사용됩니다.|
| ForceEnglishOutput | *(3.5 이상)*  현재 언어 설정을 무시하고 영어를 기반으로 nuget.exe를 강제로 실행합니다. |
| 도움말 | 명령어에 대한 도움말을 표시합니다. |
| IncludeDelisted | *(3.2 이상)* 나열 되지 않은 패키지를 표시 합니다. |
| NonInteractive | 사용자 입력이나 확인에 대한 프롬프트를 표시하지 않습니다. |
| PreRelease | 목록에 시험판 패키지를 포함 합니다. |
| 소스 | 검색할 패키지 원본 목록을 지정 합니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다. |

또한 [환경 변수](cli-ref-environment-variables.md)에 대한 정보를 참조할 수 있습니다.

## <a name="examples"></a>예

구성 된 피드의 모든 패키지 나열:
```
nuget list
```
자세한 자세한 정보 표시를 포함 하는 Azure 관련 패키지를 나열 합니다.
```
nuget list Azure -Verbosity detailed
```
구성 된 피드의 모든 버전의 Azure 관련 패키지를 나열 합니다.
```
nuget list Azure -AllVersions
```
지정 된 원본/피드에서 JSON 관련 패키지의 모든 버전을 나열 합니다.
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
여러 원본/피드에서 JSON 관련 패키지 나열:
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

