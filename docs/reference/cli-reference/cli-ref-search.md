---
title: NuGet CLI 검색 명령
description: nuget.exe 검색 명령에 대한 참조
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323663"
---
# <a name="search-command-nuget-cli"></a>search 명령(NuGet CLI)

**적용 대상:** 패키지 사용 &bullet; **지원 버전:** 5.8 이상

제공된 쿼리 문자열을 사용하여 지정된 소스를 검색합니다. 지정된 소스가 없으면 %AppData%\NuGet\NuGet.Config 정의된 모든 원본이 사용됩니다.

## <a name="usage"></a>사용

```cli
nuget search [search terms] [options]
```

여기서 검색 용어는 nuget.org 사용할 때와 마찬가지로 패키지, 태그 및 패키지 설명의 이름에 적용됩니다.

## <a name="options"></a>옵션

| 이름 | Description | 사용 |
| ---  |     ---     |  :-:  |
| 시험판 | 사전 릴리스 패키지는 기본적으로 포함되지 않지만 이 인수를 사용하여 포함할 수 있습니다. | -PreRelease |
| 원본 | 에서 기본 원본을 쿼리하는 대신 검색할 특정 패키지 __원본nuget.config__ | -Source `<Source URL>`|
| Take | 반환할 결과 수입니다. 기본값은 20입니다. | -Take `<positive integer>` |
| 자세한 정도 | 출력에 표시할 세부 정보 수준입니다. 기본값은 _일반_ 입니다. (아래 참고 참조)  | -Verbosity `<quiet|normal|detailed>` |
| 도움말 | 명령에 대한 도움말 정보를 표시합니다. | -Help |

환경 [변수도 참조하세요.](cli-ref-environment-variables.md)

> [!NOTE] 
> 자세한 정도 수준:
> * _quiet_ - 패키지 ID, 버전
> * _normal_ - 패키지 ID, 버전, 다운로드, 설명 미리 보기
> * _detailed_ - 패키지 ID, 버전, 다운로드, 전체 설명, 쿼리 URL과 같은 기타 정보

## <a name="examples"></a>예

기본 원본에서 *로깅* 관련 패키지를 검색합니다.
```
nuget search logging
```
자세한 세부 정보로 *로깅* 관련 패키지를 검색합니다.
```
nuget search logging -Verbosity detailed
```
*로깅* 관련 패키지를 검색하고 상위 5개 결과만 표시합니다.
```
nuget search logging -Take 5
```
지정된 소스/피드에서 *JSON* 관련 패키지(릴리스 전 버전 포함)를 검색합니다.
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
여러 원본/피드에서 *JSON* 관련 패키지를 검색합니다.
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
