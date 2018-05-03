---
title: NuGet CLI 목록 표시 명령
description: Nuget.exe 목록 명령에 대 한 참조
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4a44c70937e7cb49e472c53e9857e9f44d269f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="list-command-nuget-cli"></a>목록 표시 명령 (NuGet CLI)

**적용 대상:** 패키지 소비, 게시 &bullet; **지원 되는 버전:** 모든

지정된 된 원본에서 패키지의 목록이 표시 됩니다. 모든 소스에서 글로벌 구성 파일에 정의 된 원본이 지정 된 경우 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config`, 사용 됩니다. 경우 `NuGet.Config` 다음 원본이 없습니다 지정 `list` 기본 피드 (nuget.org)를 사용 하 여 합니다.

## <a name="usage"></a>사용법

```cli
nuget list [search terms] [options]
```

여기서 선택적 검색 단어에 표시 된 목록을 필터링 합니다. 검색어는 nuget.org 방화벽을 사용 하는 경우와 마찬가지로 패키지, 태그 및 패키지 설명의 이름에 적용 됩니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| --- | --- |
| AllVersions | 패키지의 모든 버전을 나열 합니다. 기본적으로는 최신 패키지 버전에만 표시 됩니다. |
| ConfigFile | 적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.|
| ForceEnglishOutput | *(3.5 +)*  고정, 영어 기반 문화권을 사용 하 여 실행할 nuget.exe를 강제로 수행 합니다. |
| 도움말 | 도움말의 명령에 대 한 정보를 표시 합니다. |
| IncludeDelisted | *(3.2 +)*  목록에 없는 패키지를 표시 합니다. |
| 비 대화형 | 사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다. |
| 시험판 | 목록에 시험판 패키지를 포함합니다. |
| 소스 | 검색할 패키지 소스 목록을 지정 합니다. |
| 자세한 정도 | 출력에 표시 되는 세부 정보 수준을 지정: *일반*, *quiet*, *자세한*합니다. |

또한 참조 [환경 변수](cli-ref-environment-variables.md)

## <a name="examples"></a>예제

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
