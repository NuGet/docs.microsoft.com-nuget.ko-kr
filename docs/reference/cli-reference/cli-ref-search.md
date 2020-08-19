---
title: NuGet CLI 검색 명령
description: nuget.exe 검색 명령에 대 한 참조
author: advay26
ms.author: t-adtand
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 35e4906960534299418cb2a17c190476708b2634
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623256"
---
# <a name="search-command-nuget-cli"></a>검색 명령 (NuGet CLI)

**적용 대상:** 패키지 사용 &bullet; **지원 버전:** 5.8 +

제공 된 쿼리 문자열을 사용 하 여 지정 된 소스를 검색 합니다. 원본을 지정 하지 않으면% AppData% \NuGet\NuGet.config에 정의 된 모든 원본이 사용 됩니다.

## <a name="usage"></a>사용량

```cli
nuget search [search terms] [options]
```

여기서 검색 용어는 nuget.org에서 사용 하는 경우와 마찬가지로 패키지, 태그 및 패키지 설명의 이름에 적용 됩니다.

## <a name="options"></a>옵션

| 속성 | Description | 사용량 |
| ---  |     ---     |  :-:  |
| 시험판 | 시험판 패키지는 기본적으로 포함 되어 있지 않지만이 인수를 사용 하 여 포함할 수 있습니다. | -시험판 |
| 원본 | __nuget.config__ 에서 기본 소스를 쿼리 하는 대신 검색할 특정 패키지 원본 | -원본 `<Source URL>`|
| Take | 반환할 결과의 수입니다. 기본값은 20입니다. | -Take `<positive integer>` |
| 자세한 정도 | 출력에 표시할 세부 정보 수준입니다. 기본값은 _normal_입니다. (아래 참고 참조)  | -자세한 정도 `<quiet\|normal\|detailed>` |
| 도움말 | 명령에 대 한 도움말 정보를 표시 합니다. | -Help |

[환경 변수](cli-ref-environment-variables.md) 참조

__참고__

자세한 표시 수준:

* _자동_ 패키지 ID, 버전
* _일반_ -패키지 ID, 버전, 다운로드, 설명 미리 보기
* _세부_ 정보-패키지 ID, 버전, 다운로드, 전체 설명, 쿼리 URL과 같은 기타 정보

## <a name="examples"></a>예제

기본 원본에서 *로깅*관련 패키지 검색:
```
nuget search logging
```
자세한 자세한 정보 표시를 사용 하 여 *로깅*관련 패키지를 검색 합니다.
```
nuget search logging -Verbosity detailed
```
*로깅*관련 패키지를 검색 하 고 상위 5 개 결과만 표시 합니다.
```
nuget search logging -Take 5
```
지정 된 원본/피드의 시험판 버전을 포함 하 여 *JSON*관련 패키지를 검색 합니다.
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
여러 원본/피드에서 *JSON*관련 패키지 검색:
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
