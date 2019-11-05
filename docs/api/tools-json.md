---
title: nuget.exe 버전을 검색 하기 위한 도구입니다.
description: 의 끝점
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: a186db9727bdfd1b55bf73a1f29283352555dede
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611026"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a>nuget.exe 버전을 검색 하기 위한 도구입니다.

현재는 스크립트 가능한 방식으로 컴퓨터에서 최신 버전의 nuget.exe를 가져오는 몇 가지 방법이 있습니다. 예를 들어 nuget.org에서 [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) 패키지를 다운로드 하 여 추출할 수 있습니다. 이는 이미 nuget.exe (`nuget.exe install`)를 사용 하거나, 기본 압축 풀기 도구를 사용 하 여 nupkg의 압축을 풀고 내부에서 이진 파일을 찾아야 하기 때문에 다소 복잡 합니다.

이미 nuget.exe를 사용 하 고 있는 경우에는 `nuget.exe update -self`를 사용할 수도 있지만이 경우에는 nuget.exe의 기존 복사본도 필요 합니다. 이 방법은 사용자를 최신 버전으로 업데이트 하기도 합니다. 특정 버전을 사용할 수 없습니다.

`tools.json` 끝점은 부트스트래핑 문제를 해결 하 고 다운로드 하는 nuget.exe 버전을 제어 하는 데 사용할 수 있습니다. 이를 CI/CD 환경 또는 사용자 지정 스크립트에서 사용 하 여 모든 릴리스 버전의 nuget.exe를 검색 하 고 다운로드할 수 있습니다.

`tools.json` 끝점은 인증 되지 않은 HTTP 요청 (예: PowerShell 또는 `wget``Invoke-WebRequest`)을 사용 하 여 페치할 수 있습니다. JSON 역직렬 변환기를 사용 하 여 구문 분석할 수 있으며 후속 nuget .exe 다운로드 Url은 인증 되지 않은 HTTP 요청을 사용 하 여 페치할 수도 있습니다.

`GET` 메서드를 사용 하 여 끝점을 페치할 수 있습니다.

    GET https://dist.nuget.org/tools.json

끝점에 대 한 [JSON 스키마](https://json-schema.org/) 는 여기에서 사용할 수 있습니다.

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a>응답

응답은 사용 가능한 모든 버전의 nuget.exe를 포함 하는 JSON 문서입니다.

루트 JSON 개체에는 다음과 같은 속성이 있습니다.

name      | Type             | 필요한 공간
--------- | ---------------- | --------
nuget.exe | 개체의 배열 | 예

`nuget.exe` 배열에 있는 각 개체에는 다음과 같은 속성이 있습니다.

name     | Type   | 필요한 공간 | 노트
-------- | ------ | -------- | -----
version  | string | 예      | SemVer 2.0.0 문자열
url      | string | 예      | 이 버전의 nuget.exe를 다운로드 하는 데 사용할 절대 URL입니다.
단계    | string | 예      | 열거형 문자열
함 | string | 예      | 버전을 사용 가능 하 게 설정한 경우의 대략적인 ISO 8601 타임 스탬프

배열의 항목은 내림차순 (SemVer 2.0.0 order)으로 정렬 됩니다. 이러한 보장은 가장 높은 버전 번호에 관심이 있는 클라이언트의 부담을 줄이기 위한 것입니다. 그러나이는 목록이 시간순으로 정렬 되지 않음을 의미 합니다. 예를 들어 더 낮은 주 버전이 더 높은 주 버전 보다 나중에 서비스 되는 경우이 서비스 버전은 목록 맨 위에 나타나지 않습니다. *타임 스탬프로*최신 버전을 해제 하려면 `uploaded` 문자열을 기준으로 배열을 정렬 하면 됩니다. 이는 `uploaded` 타임 스탬프가 [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 형식이 기 때문에 작동 합니다 .이는 사전순 정렬 (즉, 간단한 문자열 정렬)을 사용 하 여 시간순으로 정렬할 수 있습니다.

`stage` 속성은이 도구 버전의 점검 되었다는 방법을 나타냅니다. 

단계              | 의미
------------------ | ------
EarlyAccessPreview | [다운로드 웹 페이지](https://www.nuget.org/downloads) 에 아직 표시 되지 않으며 파트너가 유효성을 검사 해야 합니다.
Released           | 다운로드 사이트에서 사용할 수 있지만, 광범위 한 사용량에는 아직 권장 되지 않습니다.
ReleasedAndBlessed | 다운로드 사이트에서 사용할 수 있으며 소비에 권장 됩니다.

최신 권장 버전을 사용 하는 간단한 방법 중 하나는 `stage` 값이 `ReleasedAndBlessed`인 목록의 첫 번째 버전을 사용 하는 것입니다. 이는 버전이 SemVer 2.0.0 order로 정렬 되기 때문에 작동 합니다.

Nuget.org의 `NuGet.CommandLine` 패키지는 일반적으로 `ReleasedAndBlessed` 버전 으로만 업데이트 됩니다.

### <a name="sample-request"></a>샘플 요청

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a>샘플 응답

[!code-JSON [tools-json.json](./_data/tools-json.json)]
