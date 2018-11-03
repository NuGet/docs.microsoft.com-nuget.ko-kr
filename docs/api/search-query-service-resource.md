---
title: NuGet API 검색
description: 검색 서비스는 클라이언트가 특정 패키지 필드에서 결과 필터링 하는 키워드는 패키지에 대 한 쿼리를 허용합니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: cfcb52ba7689f1b392c782b4ad42ba820a76c8bf
ms.sourcegitcommit: 09107c5092050f44a0c6abdfb21db73878f78bd0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2018
ms.locfileid: "50981134"
---
# <a name="search"></a>검색

V3 API를 사용 하 여 패키지 원본에 사용할 수 있는 패키지를 검색 하는 것이 가능 합니다. 검색에 사용 되는 리소스를 `SearchQueryService` 에서 리소스를 찾을 합니다 [서비스 인덱스](service-index.md)합니다.

## <a name="versioning"></a>버전 관리

다음 `@type` 값이 사용 됩니다.

@type 값                   | 노트
----------------------------- | -----
SearchQueryService            | 초기 릴리스
SearchQueryService/3.0.0-beta | 별칭 `SearchQueryService`
SearchQueryService/3.0.0-rc   | 별칭 `SearchQueryService`

## <a name="base-url"></a>기준 URL

다음 API에 대 한 기본 URL의 값은는 `@id` 앞에서 언급 한 리소스 중 하나를 사용 하 여 연결 된 속성 `@type` 값입니다. 다음 문서에서 자리 표시자 기준 URL `{@id}` 사용 됩니다.

## <a name="http-methods"></a>HTTP 메서드

HTTP 메서드를 등록 리소스 지원에서 발견 한 모든 Url `GET` 고 `HEAD`입니다.

## <a name="search-for-packages"></a>패키지 검색

검색 API는 지정 된 검색 쿼리와 일치 하는 패키지의 페이지에 대 한 클라이언트를 쿼리를 수 있습니다. 서버 구현에 의해 검색 쿼리 (예: 검색 용어의 토큰화)의 해석이 결정 됩니다 있지만 일반적인 검색 쿼리는 패키지 Id, 제목, 설명 및 태그와 일치 하는 데 합니다. 또한 다른 패키지 메타 데이터 필드를 고려할 수 있습니다.

제외 된 패키지인 검색 결과에 나타나지 않아야 합니다.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>요청 매개 변수

이름        | 입력     | 형식    | 필수 | 노트
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | 아니요       | 검색 단어가 필터 패키지 하는 데 사용된
skip        | URL    | 정수 | 아니요       | 페이지 매김 건너뛸 결과 수
Take        | URL    | 정수 | 아니요       | 페이지 매김 반환할 결과 수
시험판  | URL    | boolean | 아니요       | `true` 또는 `false` 포함할지 여부를 결정 [시험판 패키지](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | 아니요       | SemVer 1.0.0 버전 문자열 

검색 쿼리 `q` 서버 구현에 의해 정의 된 방식으로 구문 분석 됩니다. nuget.org에 기본 필터링이 지원 되는 [다양 한 필드가](../consume-packages/finding-and-choosing-packages.md#search-syntax)합니다. 없으면 `q` 를 반환할 모든 패키지, skip 및 take 따른 경계 내에서 제공 됩니다. 이 통해 NuGet Visual Studio 환경에서 "찾아보기" 탭.

`skip` 매개 변수의 기본값은 0입니다.

`take` 매개 변수는 0 보다 큰 정수 이어야 합니다. 서버 구현은 최대 값을 설정할 수 있습니다.

경우 `prerelease` 을 제공 하지 않으면 시험판 패키지 제외 됩니다.

합니다 `semVerLevel` 쿼리 매개 변수를 사용 하도록 옵트인 [SemVer 2.0.0 패키지](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)합니다.
패키지만 1.0.0 SemVer 호환 되는 버전을 사용 하 여이 쿼리 매개 변수를 제외 하는 경우 반환 됩니다 (사용 하 여 합니다 [표준 NuGet 버전 지정](../reference/package-versioning.md) 4 정수 부분을 사용 하 여 버전 문자열과 같은 주의).
경우 `semVerLevel=2.0.0` 제공 SemVer 1.0.0 및 2.0.0 SemVer 호환 패키지 모두 반환 됩니다. 참조를 [nuget.org SemVer 2.0.0 지원을](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 자세한 내용은 합니다.

### <a name="response"></a>응답

응답은 최대 담긴 JSON 문서가 `take` 결과 검색 합니다. 검색 결과 패키지 ID 별 그룹화

루트 JSON 개체의 속성이 있습니다.

이름      | 형식             | 필수 | 노트
--------- | ---------------- | -------- | -----
totalHits | 정수          | 예      | 총 개수에 관계 없이 일치 `skip` 및 `take`
데이터      | 개체의 배열 | 예      | 요청에서 일치 하는 검색 결과

### <a name="search-result"></a>검색 결과

각 항목에는 `data` 배열이 동일한 패키지 ID를 공유 하는 패키지 버전의 그룹으로 구성 하는 JSON 개체
개체에는 다음 속성이 있습니다.

이름           | 형식                       | 필수 | 노트
-------------- | -------------------------- | -------- | -----
ID             | string                     | 예      | 일치 하는 패키지의 ID
버전        | string                     | 예      | (빌드 메타 데이터를 포함할 수 없습니다) 패키지의 전체 SemVer 2.0.0 버전 문자열
설명    | string                     | 아니요       | 
버전       | 개체의 배열           | 예      | 모든 일치 하는 패키지의 버전을 `prerelease` 매개 변수
authors        | 문자열 또는 문자열 배열 | 아니요       | 
iconUrl        | string                     | 아니요       | 
licenseUrl     | string                     | 아니요       | 
owners         | 문자열 또는 문자열 배열 | 아니요       | 
projectUrl     | string                     | 아니요       | 
등록   | string                     | 아니요       | 연결 된 절대 URL [등록 인덱스](registration-base-url-resource.md#registration-index)
요약        | string                     | 아니요       | 
태그           | 문자열 또는 문자열 배열 | 아니요       | 
제목          | string                     | 아니요       | 
totalDownloads | 정수                    | 아니요       | 이 값에는 다운로드의 합으로 유추할 수는 `versions` 배열
확인       | boolean                    | 아니요       | 패키지 인지 여부를 나타내는 JSON 부울 [확인](../reference/id-prefix-reservation.md)

Nuget.org에서 확인 된 패키지는 예약된 된 ID 접두사를 일치 하는 패키지 ID를 포함 하며 예약 된 접두사의 소유자 중 한 명이 소유한 하나. 자세한 내용은 참조는 [ID 접두사 예약에 대 한 설명서](../reference/id-prefix-reservation.md)합니다.

검색 결과 개체에 포함 된 메타 데이터를 최신 패키지 버전에서 수행 됩니다. 각 항목에는 `versions` 배열이 다음 속성을 사용 하 여 JSON 개체:

이름      | 형식    | 필수 | 노트
--------- | ------- | -------- | -----
@id       | string  | 예      | 연결 된 절대 URL [등록 리프](registration-base-url-resource.md#registration-leaf)
버전   | string  | 예      | (빌드 메타 데이터를 포함할 수 없습니다) 패키지의 전체 SemVer 2.0.0 버전 문자열
다운로드 | 정수 | 예      | 이 특정 패키지 버전에 대 한 다운로드 수

### <a name="sample-request"></a>샘플 요청

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>샘플 응답

[!code-JSON [search-result.json](./_data/search-result.json)]
