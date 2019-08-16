---
title: 자동 완성, NuGet API
description: 검색 자동 완성 서비스는 패키지 Id 및 버전의 대화형 검색을 지원 합니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488302"
---
# <a name="autocomplete"></a>자동 완성

V3 API를 사용 하 여 패키지 ID 및 버전 자동 완성 환경을 빌드할 수 있습니다. 자동 완성 쿼리를 만드는 데 사용 되는 `SearchAutocompleteService` 리소스는 [서비스 인덱스](service-index.md)에 있는 리소스입니다.

## <a name="versioning"></a>버전 관리

사용 되는 값은 다음과 같습니다. `@type`

@type 값                          | 참고
------------------------------------ | -----
SearchAutocompleteService            | 초기 릴리스
SearchAutocompleteService/3.0.0-beta | 별칭`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | 별칭`SearchAutocompleteService`

## <a name="base-url"></a>기준 URL

다음 api에 대 한 기준 URL은 앞서 언급 한 리소스 `@id` `@type` 값 중 하 나와 연결 된 속성의 값입니다. 다음 문서에서는 자리 표시자 기준 URL `{@id}` 이 사용 됩니다.

## <a name="http-methods"></a>HTTP 메서드

등록 리소스에서 찾은 모든 url은 HTTP 메서드 `GET` 및 `HEAD`를 지원 합니다.

## <a name="search-for-package-ids"></a>패키지 Id 검색

첫 번째 자동 완성 API는 패키지 ID 문자열의 일부 검색을 지원 합니다. 이는 NuGet 패키지 원본과 통합 된 사용자 인터페이스에 패키지 형식 미리 기능을 제공 하려는 경우에 유용 합니다.

목록에 없는 버전만 포함 된 패키지는 결과에 표시 되지 않습니다.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>요청 매개 변수

이름        | 입력     | 형식    | 필수 | 참고
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | no       | 패키지 Id와 비교할 문자열입니다.
skip        | URL    | integer | no       | 페이지를 매길 때 건너뛸 결과의 수입니다.
노트        | URL    | integer | no       | 페이지를 매길 때 반환할 결과의 수입니다.
시험판  | URL    | boolean | no       | `true`또는 `false` [시험판 패키지](../create-packages/prerelease-packages.md) 를 포함할지 여부를 결정 합니다.
semVerLevel | URL    | string  | no       | SemVer 1.0.0 버전 문자열 

자동 완성 쿼리 `q` 는 서버 구현에 정의 된 방식으로 구문 분석 됩니다. nuget.org는 원본에서 카멜식 대/소문자 및 기호 문자를 spliting 하 여 생성 된 ID의 일부인 패키지 ID 토큰의 접두사 쿼리를 지원 합니다.

매개 `skip` 변수의 기본값은 0입니다.

매개 `take` 변수는 0 보다 큰 정수 여야 합니다. 서버 구현에서 최 댓 값을 설정할 수 있습니다.

을 `prerelease` 지정 하지 않으면 시험판 패키지가 제외 됩니다.

Query 매개 변수는 [SemVer 2.0.0 패키지](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)를 옵트인 (opt in) 하는 데 사용 됩니다. `semVerLevel`
이 쿼리 매개 변수가 제외 되 면 SemVer 1.0.0 호환 버전이 포함 된 패키지 Id만 반환 됩니다 (4 개의 정수 부분을 포함 하는 버전 문자열과 같은 [표준 NuGet 버전 관리](../concepts/package-versioning.md) 에 대 한 주의).
가 `semVerLevel=2.0.0` 제공 되는 경우 SemVer 1.0.0 및 SemVer 2.0.0 호환 패키지가 모두 반환 됩니다. 자세한 내용은 [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 를 참조 하세요.

### <a name="response"></a>응답

응답은 최대 자동 완성 결과를 `take` 포함 하는 JSON 문서입니다.

루트 JSON 개체에는 다음과 같은 속성이 있습니다.

이름      | 형식             | 필수 | 참고
--------- | ---------------- | -------- | -----
totalHits | integer          | 예      | 총 일치 항목 수, 무시 `skip` 및`take`
데이터      | 문자열 배열 | 예      | 요청과 일치 하는 패키지 Id

### <a name="sample-request"></a>샘플 요청

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>샘플 응답

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>패키지 버전 열거

이전 API를 사용 하 여 패키지 ID가 검색 되 면 클라이언트는 자동 완성 API를 사용 하 여 제공 된 패키지 ID에 대 한 패키지 버전을 열거할 수 있습니다.

나열 되지 않은 패키지 버전은 결과에 표시 되지 않습니다.

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>요청 매개 변수

이름        | 입력     | 형식    | 필수 | 참고
----------- | ------ | ------- | -------- | -----
id          | URL    | string  | 예      | 버전을 가져올 패키지 ID
시험판  | URL    | boolean | no       | `true`또는 `false` [시험판 패키지](../create-packages/prerelease-packages.md) 를 포함할지 여부를 결정 합니다.
semVerLevel | URL    | string  | no       | SemVer 2.0.0 version 문자열 

을 `prerelease` 지정 하지 않으면 시험판 패키지가 제외 됩니다.

`semVerLevel` Query 매개 변수는 SemVer 2.0.0 패키지를 옵트인 (opt in) 하는 데 사용 됩니다. 이 쿼리 매개 변수가 제외 되 면 SemVer 1.0.0 버전만 반환 됩니다. 가 `semVerLevel=2.0.0` 제공 되 면 SemVer 1.0.0 및 SemVer 2.0.0 버전이 모두 반환 됩니다. 자세한 내용은 [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 를 참조 하세요.

### <a name="response"></a>응답

응답은 지정 된 쿼리 매개 변수를 기준으로 필터링 하 여 제공 된 패키지 ID의 모든 패키지 버전을 포함 하는 JSON 문서입니다.

루트 JSON 개체에는 다음과 같은 속성이 있습니다.

이름      | 형식             | 필수 | 참고
--------- | ---------------- | -------- | -----
데이터      | 문자열 배열 | 예      | 요청과 일치 하는 패키지 버전

가 쿼리 문자열에 제공 `data` 되는 경우 `1.0.0+metadata`배열의 패키지 버전에는 SemVer 2.0.0 build 메타 데이터 (예:)가 포함 될 수 있습니다. `semVerLevel=2.0.0`

### <a name="sample-request"></a>샘플 요청

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>샘플 응답

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
