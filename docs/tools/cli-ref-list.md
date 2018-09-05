---
title: NuGet CLI 목록 표시 명령
description: Nuget.exe 목록 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549803"
---
# <a name="list-command-nuget-cli"></a>목록 표시 명령 (NuGet CLI)

**적용 대상:** 패키지 사용, 게시 &bullet; **지원 되는 버전:** 모든

지정된 된 원본에서 패키지의 목록을 표시합니다. 모든 원본 전역 구성 파일에 정의 된 소스 없음이 지정 된 경우 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config`에 사용 됩니다. 하는 경우 `NuGet.Config` 원본이 없습니다를 다음 지정 `list` 기본 피드 (nuget.org)를 사용 합니다.

## <a name="usage"></a>사용법

```cli
nuget list [search terms] [options]
```

여기서 선택적 검색어에 표시 된 목록 필터링 됩니다. 검색어는 nuget.org에서 사용 하는 경우 처럼 패키지, 태그 및 패키지 설명의 이름에 적용 됩니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| AllVersions | 모든 버전의 패키지를 나열 합니다. 기본적으로 최신 패키지 버전만 표시 됩니다. |
| ConfigFile | NuGet 구성 파일을 적용 합니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| ForceEnglishOutput | *(3.5 이상)*  고정 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| IncludeDelisted | *(3.2 이상)*  제외 된 패키지를 표시 합니다. |
| NonInteractive | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| PreRelease | 목록에 시험판 패키지를 포함합니다. |
| 소스 | 검색할 패키지 소스 목록을 지정 합니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보의 양을 지정: *정상적인*, *quiet*, *자세한*합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
