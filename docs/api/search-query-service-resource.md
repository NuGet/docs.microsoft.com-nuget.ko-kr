---
title: 검색, NuGet API
description: 검색 서비스에는 키워드로 패키지에 대 한 쿼리를 특정 패키지 필드에서 필터 결과를 클라이언트 수 있습니다.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 76600ee916305ee01ddfb675c83c184e980c5a42
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821085"
---
# <a name="search"></a>검색

V3 API를 사용 하 여 패키지 원본에서 사용할 수 있는 패키지를 검색할 수는 있습니다. 검색에 사용 되는 리소스는는 `SearchQueryService` 에서 리소스를 찾을 [서비스 인덱스](service-index.md)합니다.

## <a name="versioning"></a>버전 관리

다음 `@type` 값이 사용 됩니다.

@type 값                   | 노트
----------------------------- | -----
SearchQueryService            | 초기 릴리스
SearchQueryService/3.0.0-beta | 별칭 `SearchQueryService`
SearchQueryService/3.0.0-rc   | 별칭 `SearchQueryService`

## <a name="base-url"></a>기준 URL

다음 API에 대 한 기본 URL의 값은는 `@id` 앞에서 언급 한 리소스 중 하나가 지정 된 연결 된 속성 `@type` 값입니다. 다음 문서에서 자리 표시자 기준 URL `{@id}` 사용 됩니다.

## <a name="http-methods"></a>HTTP 메서드

HTTP 메서드를 등록 리소스 지원에 있는 모든 Url `GET` 및 `HEAD`합니다.

## <a name="search-for-packages"></a>패키지에 대 한 검색

검색 API에 지정 된 검색 쿼리와 일치 하는 패키지의 페이지에 대 한 쿼리 클라이언트 수 있습니다. 검색 쿼리 (예: 검색 용어의 토큰화)의 해석 서버 구현에 의해 결정 됩니다 되지만 일반가 검색 쿼리는 패키지 Id, 제목, 설명 및 태그 일치에 사용 됩니다. 다른 패키지 메타 데이터 필드도 간주 될 수 있습니다.

목록에 없는 패키지 검색 결과에 표시 되지 않습니다 됩니다.

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>요청 매개 변수

이름        | 입력     | 형식    | 필수 | 노트
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | 아니요       | 필터 패키지에 사용 되는 검색 단어가
skip        | URL    | 정수 | 아니요       | 페이지 매김 건너뛸 결과의 수
take        | URL    | 정수 | 아니요       | 페이지 매김 반환할 결과의 수
시험판  | URL    | boolean | 아니요       | `true` 또는 `false` 포함할지 여부를 결정 [시험판 패키지](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | 아니요       | SemVer 1.0.0 버전 문자열 

검색 쿼리 `q` 서버 구현에 의해 정의 된 방식으로 구문 분석 됩니다. nuget.org에 기본 필터링이 지원 되는 [다양 한 필드가](../consume-packages/finding-and-choosing-packages.md#search-syntax)합니다. 하지 않으면 `q` 모든 패키지를 반환할지, skip 및 take에 따른 경계 내에서 제공 됩니다. 이 통해 Visual Studio 환경에서 "찾아보기" 탭 합니다.

`skip` 매개 변수 기본값은 0입니다.

`take` 매개 변수는 0 보다 큰 정수 여야 합니다. 서버 구현에는 최대 값을 설정할 수 있습니다.

경우 `prerelease` 을 제공 하지 않으면 시험판 패키지 제외 됩니다.

`semVerLevel` 쿼리 매개 변수를 사용에 동의 [SemVer 2.0.0 패키지](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)합니다.
SemVer 1.0.0 호환 되는 버전 있는 패키지만이 쿼리 매개 변수를 제외 하는 경우 반환 됩니다 (으로 [표준 NuGet 버전 관리](../reference/package-versioning.md) 4 정수 부분을 사용 하 여 버전 문자열 등의 제한 사항).
경우 `semVerLevel=2.0.0` 제공 1.0.0 SemVer와 호환 패키지가 SemVer 2.0.0 반환 됩니다. 참조는 [nuget.org에 대 한 SemVer 2.0.0 지원](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 자세한 정보에 대 한 합니다.

### <a name="response"></a>응답

응답은 최대에 포함 된 JSON 문서 `take` 결과 검색 합니다. 검색 결과 패키지 id입니다. 별로 그룹화 됩니다.

루트 JSON 개체에 다음 속성이 있습니다.

이름      | 형식             | 필수 | 노트
--------- | ---------------- | -------- | -----
totalHits | 정수          | 예      | 총 수에 관계 없이 일치 `skip` 및 `take`
데이터      | 개체의 배열 | 예      | 요청에 의해 일치 검색 결과

### <a name="search-result"></a>검색 결과

각 항목에는 `data` 배열이 같은 패키지 ID를 공유 하는 패키지 버전의 그룹으로 구성 하는 JSON 개체
개체에 다음 속성이 있습니다.

이름           | 형식                       | 필수 | 노트
-------------- | -------------------------- | -------- | -----
ID             | string                     | 예      | 일치 하는 패키지의 ID
버전        | string                     | 예      | (빌드 메타 데이터를 포함할 수 없습니다) 패키지의 전체 SemVer 2.0.0 버전 문자열
description    | string                     | 아니요       | 
버전       | 개체의 배열           | 예      | 모든 일치 하는 패키지의 버전은 `prerelease` 매개 변수
authors        | 문자열 또는 문자열의 배열 | 아니요       | 
iconUrl        | string                     | 아니요       | 
licenseUrl     | string                     | 아니요       | 
owners         | 문자열 또는 문자열의 배열 | 아니요       | 
projectUrl     | string                     | 아니요       | 
등록   | string                     | 아니요       | 연결 된 절대 URL [등록 인덱스](registration-base-url-resource.md#registration-index)
요약        | string                     | 아니요       | 
태그           | 문자열 또는 문자열의 배열 | 아니요       | 
제목          | string                     | 아니요       | 
totalDownloads | 정수                    | 아니요       | 다운로드에 의해이 값을 유추할 수는 `versions` 배열
확인       | boolean                    | 아니요       | 패키지 인지를 나타내는 JSON 부울 [확인](../reference/id-prefix-reservation.md)

Nuget.org, 확인 된 패키지는 예약 된 ID 접두사와 일치 하는 패키지 ID를 포함 하 고 예약 된 네임 스페이스 소유자 중 하나가 소유 하나는입니다. 자세한 내용은 참조는 [ID 접두사 예약에 대 한 설명서](../reference/id-prefix-reservation.md)합니다.

검색 결과 개체에 포함 된 메타 데이터는 최신 패키지 버전에서 가져온 것입니다. 각 항목에는 `versions` 배열이 다음 속성을 가진 JSON 개체:

이름      | 형식    | 필수 | 노트
--------- | ------- | -------- | -----
@id       | string  | 예      | 연결 된 절대 URL [등록 리프](registration-base-url-resource.md#registration-leaf)
버전   | string  | 예      | (빌드 메타 데이터를 포함할 수 없습니다) 패키지의 전체 SemVer 2.0.0 버전 문자열
다운로드 | 정수 | 예      | 이 특정 패키지 버전에 대 한 다운로드 수

### <a name="sample-request"></a>샘플 요청

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>샘플 응답

[!code-JSON [search-result.json](./_data/search-result.json)]
