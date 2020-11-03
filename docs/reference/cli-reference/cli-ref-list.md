---
title: NuGet CLI 목록 명령
description: nuget.exe list 명령에 대 한 참조
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a6a4ee434c43ad4865dba12f039b5d545a90d3c4
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238168"
---
# <a name="list-command-nuget-cli"></a>list 명령 (NuGet CLI)

**적용 대상:** 패키지 사용, &bullet; **지원 되는 버전 게시:** 모두

지정 된 원본의 패키지 목록을 표시 합니다. 소스를 지정 하지 않으면 전역 구성 파일 (Windows) 또는에 정의 된 모든 소스가 `%AppData%\NuGet\NuGet.Config` `~/.nuget/NuGet/NuGet.Config` 사용 됩니다. `NuGet.Config`에서 소스를 지정 하지 않는 경우는 `list` 기본 피드 (nuget.org)를 사용 합니다.

## <a name="usage"></a>사용량

```cli
nuget list [search terms] [options]
```

여기서 선택적 검색 용어는 표시 된 목록을 필터링 합니다. [검색 용어](../../consume-packages/finding-and-choosing-packages.md#search-syntax) 는 nuget.org에서 사용 하는 경우와 마찬가지로 패키지, 태그 및 패키지 설명의 이름에 적용 됩니다. 

## <a name="options"></a>옵션

- **`-AllVersions`**

  패키지의 모든 버전을 나열 합니다. 기본적으로 최신 패키지 버전만 표시 됩니다.

- **`-ConfigFile`**

  적용할 NuGet 구성 파일입니다. 지정 하지 않으면 `%AppData%\NuGet\NuGet.Config` (Windows) 또는 `~/.nuget/NuGet/NuGet.Config` 또는 `~/.config/NuGet/NuGet.Config` (Mac/Linux)가 사용 됩니다.

- **`-ForceEnglishOutput`**

  *(3.5 +)* 고정 된 영어 기반 문화권을 사용 하 여 nuget.exe을 강제로 실행 합니다.

- **`-?|-help`**

  명령에 대 한 도움말 정보를 표시 합니다.

- **`-IncludeDelisted`**

  *(3.2 이상)* 나열 되지 않은 패키지를 표시 합니다.

- **`-NonInteractive`**

  사용자 입력 또는 확인에 대 한 프롬프트를 표시 하지 않습니다.

- **`-PreRelease`**

  목록에 시험판 패키지를 포함 합니다.

- **`-Source`**

  검색할 패키지 원본 목록을 지정 합니다.

- **`-Verbosity [normal|quiet|detailed]`**

  출력에 표시 되는 세부 정보의 양을 지정 합니다. `normal` (기본값), `quiet` 또는 `detailed` 입니다.

[환경 변수](cli-ref-environment-variables.md) 참조

## <a name="examples"></a>예제

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