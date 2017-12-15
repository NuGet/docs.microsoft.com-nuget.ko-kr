---
title: "자동 완성, NuGet API | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: ead5cf7a-e51e-4cbb-8798-58226f4c853f
description: "검색 자동 완성 서비스 패키지 Id의 대화형 검색 및 버전을 지원합니다."
keywords: "NuGet 자동 완성 API, NuGet 패키지 ID, 패키지 ID 부분 문자열을 검색합니다."
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 313ceb630947b46c34b98e14044ecf121b725087
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="autocomplete"></a>자동 완성

V3 API를 사용 하 여 패키지 ID 및 버전 자동 완성 환경을 구축 하는 것이 불가능 합니다. 자동 완성 쿼리를 만드는 데 사용 되는 리소스는는 `SearchAutocompleteService` 에서 리소스를 찾을 [서비스 인덱스](service-index.md)합니다.

## <a name="versioning"></a>버전 관리

다음 `@type` 값이 사용 됩니다.

@type 값                          | 참고
------------------------------------ | -----
SearchAutocompleteService            | 초기 릴리스
SearchAutocompleteService/3.0.0-beta | 별칭`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | 별칭`SearchAutocompleteService`

## <a name="base-url"></a>기준 URL

다음 Api에 대 한 기본 URL의 값은는 `@id` 앞에서 언급 한 리소스 중 하나가 지정 된 연결 된 속성 `@type` 값입니다. 다음 문서에서 자리 표시자 기준 URL `{@id}` 사용 됩니다.

## <a name="http-methods"></a>HTTP 메서드

HTTP 메서드를 등록 리소스 지원에 있는 모든 Url `GET` 및 `HEAD`합니다.

## <a name="search-for-package-ids"></a>패키지 Id에 대 한 검색

첫 번째 자동 완성 API 패키지 ID 문자열의 일부에 대 한 검색 기능을 지원 합니다. NuGet 패키지 소스와 통합 하 여 사용자 인터페이스에서 패키지 typeahead 기능을 제공 하려는 경우에 유용 합니다.

목록에 없는 버전에만 사용 하 여 패키지 결과에 나타나지 않습니다.

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a>요청 매개 변수

이름        | 입력     | 형식    | 필수 | 참고
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | no       | 패키지 Id와 비교할 문자열
skip        | URL    | 정수 | no       | 페이지 매김 건너뛸 결과의 수
take        | URL    | 정수 | no       | 페이지 매김 반환할 결과의 수
시험판  | URL    | boolean | no       | `true`또는 `false` 포함할지 여부를 결정 [시험판 패키지](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | no       | SemVer 1.0.0 버전 문자열 

자동 완성 쿼리 `q` 서버 구현에 의해 정의 된 방식으로 구문 분석 됩니다. nuget.org 카멜식 대/소문자 및 기호 문자만 여 원래를 접두사 부분인 spliting에서 생성 된 ID의 패키지 ID 토큰에 대 한 쿼리를 지원 합니다.

`skip` 매개 변수 기본값은 0입니다.

`take` 매개 변수는 0 보다 큰 정수 여야 합니다. 서버 구현에는 최대 값을 설정할 수 있습니다.

경우 `prerelease` 을 제공 하지 않으면 시험판 패키지 제외 됩니다.

`semVerLevel` 쿼리 매개 변수를 사용에 동의 [SemVer 2.0.0 패키지](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)합니다.
이 쿼리 매개 변수가 제외 되 면 SemVer 1.0.0 호환 되는 버전을 사용 하 여 유일한 패키지 Id가 반환 됩니다 (으로 [표준 NuGet 버전 관리](../reference/package-versioning.md) 4 정수 부분을 사용 하 여 버전 문자열 등의 제한 사항).
경우 `semVerLevel=2.0.0` 제공 1.0.0 SemVer와 호환 패키지가 SemVer 2.0.0 반환 됩니다. 참조는 [nuget.org에 대 한 SemVer 2.0.0 지원](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 자세한 정보에 대 한 합니다.

### <a name="response"></a>응답

응답은 최대에 포함 된 JSON 문서 `take` 자동 완성 결과입니다.

루트 JSON 개체에 다음 속성이 있습니다.

이름      | 형식             | 필수 | 참고
--------- | ---------------- | -------- | -----
totalHits | 정수          | 예      | 총 수에 관계 없이 일치 `skip` 및`take`
데이터      | 문자열의 배열 | 예      | 요청에서 일치 하는 패키지 Id

### <a name="sample-request"></a>샘플 요청

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a>샘플 응답

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>패키지 버전을 열거 합니다.

이전 API를 사용 하 여 패키지 ID가 검색, 되 면 클라이언트가 제공 된 패키지 ID에 대해 패키지 버전을 열거 하 자동 완성 API를 사용할 수 있습니다.

패키지 버전이 나열 되지 않은 결과에 나타나지 않습니다.

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a>요청 매개 변수

이름        | 입력     | 형식    | 필수 | 참고
----------- | ------ | ------- | -------- | -----
ID          | URL    | string  | 예      | 에 대 한 버전을 인출 하는 패키지 ID
시험판  | URL    | boolean | no       | `true`또는 `false` 포함할지 여부를 결정 [시험판 패키지](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | no       | SemVer 2.0.0 버전 문자열 

경우 `prerelease` 을 제공 하지 않으면 시험판 패키지 제외 됩니다.

`semVerLevel` 쿼리 매개 변수는 SemVer 2.0.0 패키지에 옵트인 하는 데 사용 됩니다. 이 쿼리 매개 변수가 제외 되 면 SemVer 1.0.0 버전에만 반환 됩니다. 경우 `semVerLevel=2.0.0` 제공 SemVer 1.0.0 및 SemVer 2.0.0 버전을 모두 반환 됩니다. 참조는 [nuget.org에 대 한 SemVer 2.0.0 지원](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 자세한 정보에 대 한 합니다.

### <a name="response"></a>응답

응답에는 지정 된 쿼리 매개 변수에 의해 필터링 된 제공 된 패키지 ID의 모든 패키지 버전을 포함 하는 JSON 문서입니다.

루트 JSON 개체에 다음 속성이 있습니다.

이름      | 형식             | 필수 | 참고
--------- | ---------------- | -------- | -----
데이터      | 문자열의 배열 | 예      | 패키지 버전 요청에 의해 일치

패키지 버전은 `data` 배열 SemVer 2.0.0 빌드 메타 데이터를 포함할 수 (예: `1.0.0+metadata`) 하는 경우는 `semVerLevel=2.0.0` 쿼리 문자열에 제공 되었습니다.

### <a name="sample-request"></a>샘플 요청

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a>샘플 응답

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
