---
title: 검색, NuGet API
description: 검색 서비스를 사용 하면 클라이언트가 키워드별로 패키지를 쿼리하고 특정 패키지 필드에서 결과를 필터링 할 수 있습니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b898b389ee6c962831ce789a7c304c75e6bd8774
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488206"
---
# <a name="search"></a>검색

V3 API를 사용 하 여 패키지 원본에서 사용할 수 있는 패키지를 검색할 수 있습니다. 검색 `SearchQueryService` 에 사용 되는 리소스는 [서비스 인덱스](service-index.md)에 있는 리소스입니다.

## <a name="versioning"></a>버전 관리

사용 되는 값은 다음과 같습니다. `@type`

@type 값                   | 참고
----------------------------- | -----
SearchQueryService            | 초기 릴리스
SearchQueryService/3.0.0-beta | 별칭`SearchQueryService`
SearchQueryService/3.0.0-rc   | 별칭`SearchQueryService`

## <a name="base-url"></a>기준 URL

다음 API에 대 한 기준 URL은 앞서 언급 한 리소스 `@id` `@type` 값 중 하 나와 연결 된 속성의 값입니다. 다음 문서에서는 자리 표시자 기준 URL `{@id}` 이 사용 됩니다.

## <a name="http-methods"></a>HTTP 메서드

등록 리소스에서 찾은 모든 url은 HTTP 메서드 `GET` 및 `HEAD`를 지원 합니다.

## <a name="search-for-packages"></a>패키지 검색

검색 API를 통해 클라이언트는 지정 된 검색 쿼리와 일치 하는 패키지 페이지를 쿼리할 수 있습니다. 검색 쿼리 (예: 검색 용어의 토큰화)의 해석은 서버 구현에 따라 결정 되지만, 일반적으로 검색 쿼리는 패키지 Id, 제목, 설명 및 태그 일치에 사용 됩니다. 다른 패키지 메타 데이터 필드도 고려할 수 있습니다.

나열 되지 않은 패키지는 검색 결과에 표시 되지 않습니다.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>요청 매개 변수

이름        | 입력     | 형식    | 필수 | 참고
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | no       | 패키지를 필터링 하는 데 사용 되는 검색 용어
skip        | URL    | integer | no       | 페이지를 매길 때 건너뛸 결과의 수입니다.
노트        | URL    | integer | no       | 페이지를 매길 때 반환할 결과의 수입니다.
시험판  | URL    | boolean | no       | `true`또는 `false` [시험판 패키지](../create-packages/prerelease-packages.md) 를 포함할지 여부를 결정 합니다.
semVerLevel | URL    | string  | no       | SemVer 1.0.0 버전 문자열 

검색 쿼리 `q` 는 서버 구현에 정의 된 방식으로 구문 분석 됩니다. nuget.org는 [다양 한 필드](../consume-packages/finding-and-choosing-packages.md#search-syntax)에 대 한 기본 필터링을 지원 합니다. 을 제공 `q` 하지 않으면 skip 및 take에 의해 적용 되는 경계 내에서 모든 패키지가 반환 됩니다. 이렇게 하면 NuGet Visual Studio 환경에서 "찾아보기" 탭을 사용할 수 있습니다.

매개 `skip` 변수의 기본값은 0입니다.

매개 `take` 변수는 0 보다 큰 정수 여야 합니다. 서버 구현에서 최 댓 값을 설정할 수 있습니다.

을 `prerelease` 지정 하지 않으면 시험판 패키지가 제외 됩니다.

Query 매개 변수는 [SemVer 2.0.0 패키지](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)를 옵트인 (opt in) 하는 데 사용 됩니다. `semVerLevel`
이 쿼리 매개 변수가 제외 되 면 SemVer 1.0.0 호환 버전이 포함 된 패키지만 반환 됩니다 (4 개의 정수 부분을 포함 하는 버전 문자열과 같은 [표준 NuGet 버전 관리](../concepts/package-versioning.md) 에 대 한 주의).
가 `semVerLevel=2.0.0` 제공 되는 경우 SemVer 1.0.0 및 SemVer 2.0.0 호환 패키지가 모두 반환 됩니다. 자세한 내용은 [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 를 참조 하세요.

### <a name="response"></a>응답

응답은 검색 결과를 `take` 포함 하는 JSON 문서입니다. 검색 결과는 패키지 ID를 기준으로 그룹화 됩니다.

루트 JSON 개체에는 다음과 같은 속성이 있습니다.

이름      | 형식             | 필수 | 참고
--------- | ---------------- | -------- | -----
totalHits | integer          | 예      | 총 일치 항목 수, 무시 `skip` 및`take`
데이터      | 개체의 배열 | 예      | 요청과 일치 하는 검색 결과입니다.

### <a name="search-result"></a>검색 결과

`data` 배열의 각 항목은 동일한 패키지 ID를 공유 하는 패키지 버전 그룹으로 구성 된 JSON 개체입니다.
개체에는 다음과 같은 속성이 있습니다.

이름           | 형식                       | 필수 | 참고
-------------- | -------------------------- | -------- | -----
id             | string                     | 예      | 일치 하는 패키지의 ID입니다.
version        | string                     | 예      | 패키지의 full SemVer 2.0.0 version 문자열 (빌드 메타 데이터를 포함할 수 있음)
description    | string                     | no       | 
버전       | 개체의 배열           | 예      | `prerelease` 매개 변수와 일치 하는 패키지의 모든 버전
authors        | 문자열 또는 문자열 배열 | no       | 
iconUrl        | string                     | no       | 
licenseUrl     | string                     | no       | 
owners         | 문자열 또는 문자열 배열 | no       | 
projectUrl     | string                     | no       | 
등록   | string                     | no       | 연결 된 [등록 인덱스](registration-base-url-resource.md#registration-index) 의 절대 URL입니다.
요약        | string                     | no       | 
태그           | 문자열 또는 문자열 배열 | no       | 
title          | string                     | no       | 
totalDownloads | integer                    | no       | `versions` 배열의 다운로드 합으로이 값을 유추할 수 있습니다.
확인       | boolean                    | no       | 패키지가 [확인](../nuget-org/id-prefix-reservation.md) 되었는지 여부를 나타내는 JSON 부울입니다.

Nuget.org에서 확인 된 패키지는 예약 된 ID 접두사와 일치 하 고 예약 된 접두사 소유자 중 하나가 소유 하 고 있는 패키지 ID입니다. 자세한 내용은 [ID 접두사 예약에 대 한 설명서](../reference/id-prefix-reservation.md)를 참조 하세요.

검색 결과 개체에 포함 된 메타 데이터는 최신 패키지 버전에서 가져옵니다. `versions` 배열의 각 항목은 다음 속성을 포함 하는 JSON 개체입니다.

이름      | 형식    | 필수 | 참고
--------- | ------- | -------- | -----
@id       | string  | 예      | 연결 된 [등록 리프](registration-base-url-resource.md#registration-leaf) 에 대 한 절대 URL입니다.
version   | string  | 예      | 패키지의 full SemVer 2.0.0 version 문자열 (빌드 메타 데이터를 포함할 수 있음)
다운로드 | integer | 예      | 이 특정 패키지 버전에 대 한 다운로드 수

### <a name="sample-request"></a>샘플 요청

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>샘플 응답

[!code-JSON [search-result.json](./_data/search-result.json)]
