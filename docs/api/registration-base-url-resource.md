---
title: 패키지 메타 데이터, NuGet API
description: 패키지 등록 기준 URL을 사용 하 여 패키지에 대 한 메타 데이터를 가져올 수 있습니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c62e5b7b53d30a1b362e87dbbea26355a36b1274
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813275"
---
# <a name="package-metadata"></a>패키지 메타데이터

NuGet V3 API를 사용 하 여 패키지 원본에서 사용할 수 있는 패키지에 대 한 메타 데이터를 가져올 수 있습니다. 이 메타 데이터는 [서비스 인덱스](service-index.md)에 있는 `RegistrationsBaseUrl` 리소스를 사용 하 여 페치할 수 있습니다.

`RegistrationsBaseUrl` 아래에 있는 문서 컬렉션을 "등록" 또는 "등록 blob" 이라고 하는 경우가 많습니다. 단일 `RegistrationsBaseUrl` 아래의 문서 집합을 "등록 hive" 라고 합니다. 등록 하이브에는 패키지 원본에서 사용할 수 있는 모든 패키지에 대 한 모든 메타 데이터가 포함 됩니다.

## <a name="versioning"></a>버전 관리

사용 되는 `@type` 값은 다음과 같습니다.

@type 값                     | 참고
------------------------------- | -----
RegistrationsBaseUrl            | 초기 릴리스
RegistrationsBaseUrl/3.0.0-beta | `RegistrationsBaseUrl`의 별칭
RegistrationsBaseUrl/3.0.0-rc   | `RegistrationsBaseUrl`의 별칭
RegistrationsBaseUrl/3.4.0      | Gzipped 응답
RegistrationsBaseUrl/3.6.0      | SemVer 2.0.0 패키지 포함

이는 다양 한 클라이언트 버전에 대해 사용할 수 있는 세 가지 고유한 등록 하이브를 나타냅니다.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

이러한 등록은 압축 되지 않습니다 (묵시적 `Content-Encoding: identity`를 사용 한다는 의미). SemVer 2.0.0 패키지는이 hive에서 **제외** 됩니다.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

이러한 등록은 `Content-Encoding: gzip`를 사용 하 여 압축 됩니다. SemVer 2.0.0 패키지는이 hive에서 **제외** 됩니다.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

이러한 등록은 `Content-Encoding: gzip`를 사용 하 여 압축 됩니다. SemVer 2.0.0 패키지는이 하이브에 **포함** 됩니다.
SemVer 2.0.0에 대 한 자세한 내용은 [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)를 참조 하세요.

## <a name="base-url"></a>기준 URL

다음 Api에 대 한 기준 URL은 앞서 언급 한 리소스 `@type` 값에 연결 된 `@id` 속성의 값입니다. 다음 문서에서는 자리 표시자 기준 URL `{@id}` 사용 됩니다.

## <a name="http-methods"></a>HTTP 메서드

등록 리소스에서 찾은 모든 Url은 HTTP 메서드 `GET` 및 `HEAD`를 지원 합니다.

## <a name="registration-index"></a>등록 인덱스

등록 리소스는 패키지 ID 별로 패키지 메타 데이터를 그룹화 합니다. 한 번에 두 개 이상의 패키지 ID에 대 한 데이터를 가져올 수는 없습니다. 이 리소스는 패키지 Id를 검색할 수 있는 방법을 제공 하지 않습니다. 대신 클라이언트는 원하는 패키지 ID를 이미 알고 있는 것으로 간주 됩니다. 각 패키지 버전에 대 한 사용 가능한 메타 데이터는 서버 구현에 따라 달라 집니다. 패키지 등록 blob의 계층 구조는 다음과 같습니다.

- **인덱스**: 원본에 있는 모든 패키지에서 동일한 패키지 ID를 사용 하 여 공유 하는 패키지 메타 데이터의 진입점입니다.
- **Page**: 패키지 버전의 그룹입니다. 페이지의 패키지 버전 수는 서버 구현에 의해 정의 됩니다.
- **리프**: 단일 패키지 버전과 관련 된 문서입니다.

등록 인덱스의 URL은 예측 가능 하며, 서비스 인덱스에서 패키지 ID 및 등록 리소스의 `@id` 값을 지정 하 여 클라이언트에 의해 결정 될 수 있습니다. 등록 페이지 및 리프에 대 한 Url은 등록 인덱스를 검사 하 여 검색 됩니다.

### <a name="registration-pages-and-leaves"></a>등록 페이지 및 리프

서버 구현에서 개별 등록 페이지 문서에 등록 leafs을 저장 하는 데 반드시 필요한 것은 아니지만 클라이언트 쪽 메모리를 절약 하는 것이 좋습니다. 인덱스의 모든 등록 리프를 인라인 하거나 페이지 문서에 리프를 즉시 저장 하는 대신 서버 구현에서 패키지 버전의 수를 기반으로 하는 두 가지 방법 중에서 선택할 수 있는 몇 가지 추론을 정의 하는 것이 좋습니다. 패키지 리프의 누적 크기입니다.

등록 인덱스에 모든 패키지 버전 (리프)을 저장 하면 패키지 메타 데이터를 인출 하는 데 필요한 HTTP 요청 수가 절약 되지만 더 큰 문서를 다운로드 하 여 더 많은 클라이언트 메모리를 할당 해야 함을 의미 합니다. 반면에 서버 구현에서 등록 리프를 별도 페이지 문서에 즉시 저장 하는 경우 클라이언트는 필요한 정보를 얻기 위해 더 많은 HTTP 요청을 수행 해야 합니다.

Nuget.org에서 사용 하는 추론은 다음과 같습니다. 128 이상의 패키지 버전이 있는 경우에는 64 크기의 페이지로 리프를 나눕니다. 128 버전 보다 작은 경우 인라인 모두 등록 인덱스에 그대로 둡니다. 즉, 65 ~ 127 버전의 패키지는 인덱스에 두 페이지를 포함 하지만 두 페이지가 모두 인라인 됩니다.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>요청 매개 변수

이름     | 입력     | 형식    | 필수 | 참고
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | 예      | 패키지 ID, lowercased

`LOWER_ID` 값은에서 구현 된 규칙을 사용 하 여 원하는 패키지 ID lowercased. NET의 [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) 메서드입니다.

### <a name="response"></a>응답

응답은 다음 속성을 포함 하는 루트 개체를 포함 하는 JSON 문서입니다.

이름  | 형식             | 필수 | 참고
----- | ---------------- | -------- | -----
count | 정수          | 예      | 인덱스의 등록 페이지 수
항목 | 개체의 배열 | 예      | 등록 페이지의 배열입니다.

Index 개체 `items` 배열의 각 항목은 등록 페이지를 나타내는 JSON 개체입니다.

#### <a name="registration-page-object"></a>등록 페이지 개체

등록 인덱스에 있는 등록 페이지 개체의 속성은 다음과 같습니다.

이름   | 형식             | 필수 | 참고
------ | ---------------- | -------- | -----
@id    | string           | 예      | 등록 페이지의 URL입니다.
count  | 정수          | 예      | 페이지에 있는 등록의 수입니다.
항목  | 개체의 배열 | no       | 등록의 배열 및 연결 메타 데이터
작을  | string           | 예      | 페이지에서 가장 낮은 SemVer 2.0.0 버전 (포함)
부모(parent) | string           | no       | 등록 인덱스의 URL입니다.
위의  | string           | 예      | 페이지의 최고 SemVer 2.0.0 버전 (포함)

Page 개체의 `lower` 및 `upper` 범위는 특정 페이지 버전에 대 한 메타 데이터가 필요한 경우에 유용 합니다.
이러한 범위는 필요한 유일한 등록 페이지를 인출 하는 데 사용할 수 있습니다. 버전 문자열은 [NuGet의 버전 규칙](../concepts/package-versioning.md)을 따릅니다. 버전 문자열은 정규화 되며 빌드 메타 데이터를 포함 하지 않습니다. NuGet 에코 시스템의 모든 버전과 마찬가지로 버전 문자열의 비교는 [SemVer 2.0.0의 버전 우선 순위 규칙](https://semver.org/spec/v2.0.0.html#spec-item-11)을 사용 하 여 구현 됩니다.

`parent` 속성은 등록 페이지 개체에 `items` 속성이 있는 경우에만 표시 됩니다.

`items` 속성이 등록 페이지 개체에 없는 경우 `@id`에 지정 된 URL을 사용 하 여 개별 패키지 버전에 대 한 메타 데이터를 가져와야 합니다. `items` 배열은 경우에 따라 페이지 개체에서 최적화로 제외 됩니다. 단일 패키지 ID의 버전 수가 매우 큰 경우 등록 인덱스 문서는 특정 버전 또는 작은 버전의 특정 버전에 대해서만 관심이 있는 클라이언트에 대해 처리 하는 데 큰 부담이 됩니다.

`items` 속성이 있는 경우 모든 페이지 데이터가 이미 `items` 속성에 인라인 되어 있으므로 `@id` 속성을 사용할 필요가 없습니다.

페이지 개체 `items` 배열의 각 항목은 등록 리프 및 연결 된 메타 데이터를 나타내는 JSON 개체입니다.

#### <a name="registration-leaf-object-in-a-page"></a>페이지의 등록 리프 개체

등록 페이지에 있는 등록 리프 개체의 속성은 다음과 같습니다.

이름           | 형식   | 필수 | 참고
-------------- | ------ | -------- | -----
@id            | string | 예      | 등록 리프에 대 한 URL입니다.
catalogEntry   | 개체 | 예      | 패키지 메타 데이터를 포함 하는 카탈로그 항목입니다.
packageContent | string | 예      | 패키지 콘텐츠에 대 한 URL (. nupkg)

각 등록 리프 개체는 단일 패키지 버전과 연결 된 데이터를 나타냅니다.

#### <a name="catalog-entry"></a>카탈로그 항목

등록 리프 개체의 `catalogEntry` 속성에는 다음과 같은 속성이 있습니다.

이름                     | 형식                       | 필수 | 참고
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | 예      | 이 개체를 생성 하는 데 사용 되는 문서에 대 한 URL입니다.
authors                  | 문자열 또는 문자열 배열 | no       | 
dependencyGroups         | 개체의 배열           | no       | 대상 프레임 워크를 기준으로 그룹화 된 패키지의 종속성
중단              | 개체                     | no       | 패키지와 연결 된 사용 중단
설명              | string                     | no       | 
iconUrl                  | string                     | no       | 
ID                       | string                     | 예      | 패키지의 ID입니다.
licenseUrl               | string                     | no       |
licenseExpression        | string                     | no       | 
목록                   | boolean                    | no       | 없는 경우 나열 된 것으로 간주 해야 합니다.
minClientVersion         | string                     | no       | 
projectUrl               | string                     | no       | 
published                | string                     | no       | 패키지가 게시 되었을 때의 ISO 8601 타임 스탬프를 포함 하는 문자열입니다.
requireLicenseAcceptance | boolean                    | no       | 
요약                  | string                     | no       | 
태그                     | 문자열 또는 문자열 배열  | no       | 
제목                    | string                     | no       | 
버전                  | string                     | 예      | 정규화 후의 전체 버전 문자열

패키지 `version` 속성은 정규화 후의 전체 버전 문자열입니다. 이는 SemVer 2.0.0 build 데이터가 여기에 포함 될 수 있음을 의미 합니다.

`dependencyGroups` 속성은 패키지의 종속성을 나타내는 개체의 배열입니다. 대상 프레임 워크를 기준으로 그룹화 됩니다. 패키지에 종속성이 없거나, `dependencyGroups` 속성이 없거나, 빈 배열 이거나, 모든 그룹의 `dependencies` 속성이 비어 있거나 누락 된 경우

`licenseExpression` 속성의 값은 [NuGet 라이선스 식 구문을](../reference/nuspec.md#license)준수 합니다.

> [!Note]
> Nuget.org에서 패키지를 나열 하지 않으면 `published` 값이 year 1900로 설정 됩니다.

#### <a name="package-dependency-group"></a>패키지 종속성 그룹

각 종속성 그룹 개체에는 다음과 같은 속성이 있습니다.

이름            | 형식             | 필수 | 참고
--------------- | ---------------- | -------- | -----
targetFramework | string           | no       | 이러한 종속성이 적용 되는 대상 프레임 워크입니다.
종속성    | 개체의 배열 | no       |

`targetFramework` 문자열은 NuGet의 .NET 라이브러리 [nuget. 프레임 워크](https://www.nuget.org/packages/NuGet.Frameworks/)에서 구현 된 형식을 사용 합니다. `targetFramework` 지정 하지 않으면 종속성 그룹이 모든 대상 프레임 워크에 적용 됩니다.

`dependencies` 속성은 각각 현재 패키지의 패키지 종속성을 나타내는 개체의 배열입니다.

#### <a name="package-dependency"></a>패키지 종속성

각 패키지 종속성에는 다음과 같은 속성이 있습니다.

이름         | 형식   | 필수 | 참고
------------ | ------ | -------- | -----
ID           | string | 예      | 패키지 종속성의 ID입니다.
range        | 개체 | no       | 종속성의 허용 되는 [버전 범위](../concepts/package-versioning.md#version-ranges-and-wildcards) 입니다.
등록 | string | no       | 이 종속성에 대 한 등록 인덱스의 URL입니다.

`range` 속성이 제외 되거나 빈 문자열인 경우 클라이언트는 `(, )`버전 범위를 기본값으로 지정 해야 합니다. 즉, 종속성의 모든 버전을 사용할 수 있습니다. `*` 값은 `range` 속성에 사용할 수 없습니다.

#### <a name="package-deprecation"></a>패키지 사용 중단

각 패키지 사용 중단에는 다음과 같은 속성이 있습니다.

이름             | 형식             | 필수 | 참고
---------------- | ---------------- | -------- | -----
이유          | 문자열 배열 | 예      | 패키지가 더 이상 사용 되지 않는 이유
message          | string           | no       | 이 사용 중단에 대 한 추가 세부 정보
alternatePackage | 개체           | no       | 대신 사용 해야 하는 대체 패키지

`reasons` 속성은 하나 이상의 문자열을 포함 해야 하며 다음 표의 문자열만 포함 해야 합니다.

Reason       | 설명             
------------ | -----------
레거시       | 패키지가 더 이상 유지 관리 되지 않습니다.
CriticalBugs | 패키지에 사용 하기에 적합 하지 않은 버그가 있습니다.
기타        | 이 목록에 없는 이유로 인해 패키지가 더 이상 사용 되지 않습니다.

`reasons` 속성에 알려진 집합이 아닌 문자열이 포함 된 경우이를 무시 해야 합니다. 문자열은 대/소문자를 구분 하지 않으므로 `legacy` `Legacy`와 동일 하 게 처리 되어야 합니다. 배열에는 순서 제한이 없으므로 임의의 순서로 문자열을 정렬할 수 있습니다. 또한 속성에 알려진 집합이 아닌 문자열만 포함 된 경우에는 "Other" 문자열만 포함 된 것으로 처리 해야 합니다.

#### <a name="alternate-package"></a>대체 패키지

대체 패키지 개체에는 다음과 같은 속성이 있습니다.

이름         | 형식   | 필수 | 참고
------------ | ------ | -------- | -----
ID           | string | 예      | 대체 패키지의 ID입니다.
range        | 개체 | no       | 허용 되는 [버전 범위](../concepts/package-versioning.md#version-ranges-and-wildcards)이거나, 버전이 허용 되는 경우 `*`입니다.
등록 | string | no       | 이 대체 패키지의 등록 인덱스에 대 한 URL입니다.

### <a name="sample-request"></a>샘플 요청

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>샘플 응답

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

이 특정 경우에 등록 인덱스는 인라인 등록 페이지를 포함 하므로 개별 패키지 버전에 대 한 메타 데이터를 인출 하는 데 필요한 추가 요청은 없습니다.

## <a name="registration-page"></a>등록 페이지

등록 페이지에 등록 나뭇잎이 포함 되어 있습니다. 등록 페이지를 인출 하는 URL은 위에서 언급 한 [등록 페이지 개체](#registration-page-object) 의 `@id` 속성에 의해 결정 됩니다. URL은 예측 가능 하지 않으며 항상 인덱스 문서를 통해 검색 되어야 합니다.

> [!Warning]
> Nuget.org에서 등록 페이지 문서 우연히의 URL에는 페이지의 하 한 및 상한이 포함 됩니다. 그러나 인덱스 문서에 유효한 링크가 있으면 서버 구현에서 URL의 모양을 변경 하는 것이 가능 하므로 클라이언트는이 가정을 하지 말아야 합니다.

`items` 배열을 등록 인덱스에 제공 하지 않으면 `@id` 값의 HTTP GET 요청은 개체가 루트로 포함 된 JSON 문서를 반환 합니다. 개체에는 다음 속성이 있습니다.

이름   | 형식             | 필수 | 참고
------ | ---------------- | -------- | -----
@id    | string           | 예      | 등록 페이지의 URL입니다.
count  | 정수          | 예      | 페이지에 있는 등록의 수입니다.
항목  | 개체의 배열 | 예      | 등록의 배열 및 연결 메타 데이터
작을  | string           | 예      | 페이지에서 가장 낮은 SemVer 2.0.0 버전 (포함)
부모(parent) | string           | 예      | 등록 인덱스의 URL입니다.
위의  | string           | 예      | 페이지의 최고 SemVer 2.0.0 버전 (포함)

등록 리프 개체의 모양은 [위의](#registration-leaf-object-in-a-page)등록 인덱스와 동일 합니다.

## <a name="sample-request"></a>샘플 요청

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>샘플 응답

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>등록 리프

등록 리프는 특정 패키지 ID 및 버전에 대 한 정보를 포함 합니다. 이 문서에서는 특정 버전에 대 한 메타 데이터를 사용 하지 못할 수 있습니다. [등록 인덱스 또는 등록](#registration-index) [페이지](#registration-page) (등록 인덱스를 사용 하 여 검색 됨)에서 패키지 메타 데이터를 가져와야 합니다.

등록 인덱스 또는 등록 페이지에 있는 등록 리프 개체의 `@id` 속성에서 등록 리프를 인출 하는 URL을 가져옵니다. 페이지 문서와 마찬가지로 URL은 예측 가능 하지 않으며 항상 등록 페이지 개체를 통해 검색 되어야 합니다.

> [!Warning]
> Nuget.org에서 등록 리프 문서 우연히의 URL에 패키지 버전이 포함 되어 있습니다. 그러나 부모 문서에 유효한 링크가 있으면 서버 구현에서 URL 셰이프를 자유롭게 변경할 수 있으므로 클라이언트는이 가정을 하지 않아야 합니다. 

등록 리프는 다음 속성을 포함 하는 루트 개체가 포함 된 JSON 문서입니다.

이름           | 형식    | 필수 | 참고
-------------- | ------- | -------- | -----
@id            | string  | 예      | 등록 리프에 대 한 URL입니다.
catalogEntry   | string  | no       | 이러한 리프를 생성 한 카탈로그 항목에 대 한 URL입니다.
목록         | boolean | no       | 없는 경우 나열 된 것으로 간주 해야 합니다.
packageContent | string  | no       | 패키지 콘텐츠에 대 한 URL (. nupkg)
published      | string  | no       | 패키지가 게시 되었을 때의 ISO 8601 타임 스탬프를 포함 하는 문자열입니다.
등록   | string  | no       | 등록 인덱스의 URL입니다.

> [!Note]
> Nuget.org에서 패키지를 나열 하지 않으면 `published` 값이 year 1900로 설정 됩니다.

### <a name="sample-request"></a>샘플 요청

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>샘플 응답

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
