---
title: 자동 완성, NuGet API
description: 검색 자동 완성 서비스 패키지 Id의 대화형 검색 버전을 지원 합니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fdc3ad8aa239a42d8a4c169a757715e856bdcb41
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911051"
---
# <a name="autocomplete"></a>자동 완성

V3 API를 사용 하는 패키지 ID 및 버전 자동 완성 환경을 빌드하는 것이 가능 합니다. 자동 완성 쿼리를 만드는 데 사용할 리소스를 `SearchAutocompleteService` 에서 리소스를 찾을 합니다 [서비스 인덱스](service-index.md)합니다.

## <a name="versioning"></a>버전 관리

다음 `@type` 값이 사용 됩니다.

@type 값                          | 노트
------------------------------------ | -----
SearchAutocompleteService            | 초기 릴리스
SearchAutocompleteService/3.0.0-beta | 별칭 `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | 별칭 `SearchAutocompleteService`

## <a name="base-url"></a>기준 URL

다음 Api에 대 한 기본 URL의 값은는 `@id` 앞에서 언급 한 리소스 중 하나를 사용 하 여 연결 된 속성 `@type` 값입니다. 다음 문서에서 자리 표시자 기준 URL `{@id}` 사용 됩니다.

## <a name="http-methods"></a>HTTP 메서드

HTTP 메서드를 등록 리소스 지원에서 발견 한 모든 Url `GET` 고 `HEAD`입니다.

## <a name="search-for-package-ids"></a>패키지 Id 검색

첫 번째 자동 완성 API 패키지 ID 문자열의 부분에 대 한 검색 기능을 지원 합니다. NuGet 패키지 소스를 통합 하는 사용자 인터페이스에서 패키지 미리 입력 기능을 제공 하려는 경우에 유용 합니다.

목록에 없는 버전만 사용 하 여 패키지 결과에 나타나지 않습니다.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>요청 매개 변수

이름        | 입력     | 형식    | 필수 | 노트
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | 아니요       | 패키지 Id와 비교할 문자열
skip        | URL    | 정수 | 아니요       | 페이지 매김 건너뛸 결과 수
Take        | URL    | 정수 | 아니요       | 페이지 매김 반환할 결과 수
시험판  | URL    | boolean | 아니요       | `true` 또는 `false` 포함할지 여부를 결정 [시험판 패키지](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | 아니요       | SemVer 1.0.0 버전 문자열 

자동 완성 쿼리 `q` 서버 구현에 의해 정의 된 방식으로 구문 분석 됩니다. nuget.org에 카멜식 대/소문자 및 기호 문자는 원래를 조각을 페이지 분할에서 생성 된 ID의 패키지 ID 토큰의 접두사에 대 한 쿼리를 지원 합니다.

`skip` 매개 변수의 기본값은 0입니다.

`take` 매개 변수는 0 보다 큰 정수 이어야 합니다. 서버 구현은 최대 값을 설정할 수 있습니다.

경우 `prerelease` 을 제공 하지 않으면 시험판 패키지 제외 됩니다.

합니다 `semVerLevel` 쿼리 매개 변수를 사용 하도록 옵트인 [SemVer 2.0.0 패키지](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)합니다.
이 쿼리 매개 변수를 제외 하는 경우 1.0.0 SemVer 호환 되는 버전을 사용 하 여 패키지 Id만 반환 됩니다 (사용 하 여는 [표준 NuGet 버전 관리](../reference/package-versioning.md) 4 정수 부분을 사용 하 여 버전 문자열과 같은 주의).
경우 `semVerLevel=2.0.0` 제공 SemVer 1.0.0 및 2.0.0 SemVer 호환 패키지 모두 반환 됩니다. 참조를 [nuget.org SemVer 2.0.0 지원을](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 자세한 내용은 합니다.

### <a name="response"></a>응답

응답은 최대 담긴 JSON 문서가 `take` 자동 완성 결과입니다.

루트 JSON 개체의 속성이 있습니다.

이름      | 형식             | 필수 | 노트
--------- | ---------------- | -------- | -----
totalHits | 정수          | 예      | 총 개수에 관계 없이 일치 `skip` 및 `take`
데이터      | 문자열의 배열 | 예      | 요청에서 일치 하는 패키지 Id

### <a name="sample-request"></a>샘플 요청

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>샘플 응답

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>패키지 버전을 열거 합니다.

이전 API를 사용 하 여 패키지 ID가 검색 되 면 클라이언트는 제공 된 패키지 ID의 패키지 버전을 열거 하려면 자동 완성 API를 사용할 수 있습니다.

나열 되지 않은 패키지 버전을 결과에 나타나지 않습니다.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>요청 매개 변수

이름        | 입력     | 형식    | 필수 | 노트
----------- | ------ | ------- | -------- | -----
ID          | URL    | string  | 예      | 에 대 한 버전을 가져올 패키지 ID
시험판  | URL    | boolean | 아니요       | `true` 또는 `false` 포함할지 여부를 결정 [시험판 패키지](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | 아니요       | SemVer 2.0.0 버전 문자열 

경우 `prerelease` 을 제공 하지 않으면 시험판 패키지 제외 됩니다.

`semVerLevel` 쿼리 매개 변수는 SemVer 2.0.0 패키지에 옵트인 하는 데 사용 됩니다. 이 쿼리 매개 변수를 제외 하는 경우 SemVer 1.0.0 버전에만 반환 됩니다. 경우 `semVerLevel=2.0.0` 제공 SemVer 1.0.0 및 SemVer 2.0.0 버전이 모두 반환 됩니다. 참조를 [nuget.org SemVer 2.0.0 지원을](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 자세한 내용은 합니다.

### <a name="response"></a>응답

응답에는 지정 된 쿼리 매개 변수에 의해 필터링 제공 된 패키지 ID의 모든 패키지 버전을 포함 하는 JSON 문서입니다.

루트 JSON 개체에는 다음과 같은 속성이 있습니다.

이름      | 형식             | 필수 | 노트
--------- | ---------------- | -------- | -----
데이터      | 문자열의 배열 | 예      | 요청에서 일치 하는 패키지 버전

패키지 버전을 `data` 배열 SemVer 2.0.0 빌드 메타 데이터를 포함할 수 있습니다 (예: `1.0.0+metadata`) 하는 경우는 `semVerLevel=2.0.0` 쿼리 문자열에 제공 됩니다.

### <a name="sample-request"></a>샘플 요청

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>샘플 응답

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
