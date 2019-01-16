---
title: 패키지 메타 데이터, NuGet API
description: 패키지 등록 기본 URL 허용 패키지에 대 한 메타 데이터를 인출 합니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 19a1f48164f65f1ff805e036e55abb110247aa72
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324866"
---
# <a name="package-metadata"></a>패키지 메타 데이터

NuGet V3 API를 사용 하 여 패키지 원본에 대해 사용 가능한 패키지에 대 한 메타 데이터를 인출 하는 것이 가능 합니다. 사용 하 여이 메타 데이터를 인출할 수 있습니다 합니다 `RegistrationsBaseUrl` 에서 리소스를 찾을 합니다 [서비스 인덱스](service-index.md)합니다.

아래 문서 컬렉션 `RegistrationsBaseUrl` "등록" 또는 "blob 등록" 이라고 합니다. 단일 문서 집합과 `RegistrationsBaseUrl` "등록 하이브" 라고 합니다. 등록 하이브를 패키지 원본에 사용할 수 있는 모든 패키지에 대 한 모든 메타 데이터를 포함합니다.

## <a name="versioning"></a>버전 관리

다음 `@type` 값이 사용 됩니다.

@type 값                     | 노트
------------------------------- | -----
RegistrationsBaseUrl            | 초기 릴리스
RegistrationsBaseUrl/3.0.0-beta | 별칭 `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | 별칭 `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Gzip 압축 된 응답
RegistrationsBaseUrl/3.6.0      | SemVer 2.0.0 패키지를 포함합니다.

다양 한 클라이언트 버전에 사용할 수 있는 세 가지 고유 등록 하이브를 나타냅니다.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

이러한 등록은 압축 되지 않습니다 (사용 하는 암시적인 의미 `Content-Encoding: identity`). SemVer 2.0.0 패키지가 **제외** 이 hive에서.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

사용 하 여 이러한 등록은 압축 `Content-Encoding: gzip`합니다. SemVer 2.0.0 패키지가 **제외** 이 hive에서.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

사용 하 여 이러한 등록은 압축 `Content-Encoding: gzip`합니다. SemVer 2.0.0 패키지가 **포함** 이 하이브에 합니다.
SemVer 2.0.0에 대 한 자세한 내용은 참조 하세요. [nuget.org SemVer 2.0.0 지원을](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)합니다.

## <a name="base-url"></a>기준 URL

다음 Api에 대 한 기본 URL의 값은는 `@id` 앞에서 언급 한 리소스와 연결 된 속성 `@type` 값입니다. 다음 문서에서 자리 표시자 기준 URL `{@id}` 사용 됩니다.

## <a name="http-methods"></a>HTTP 메서드

HTTP 메서드를 등록 리소스 지원에서 발견 한 모든 Url `GET` 고 `HEAD`입니다.

## <a name="registration-index"></a>등록 인덱스

등록 리소스 그룹에 패키지 ID 별 메타 데이터 패키지 한 번에 둘 이상의 패키지 ID에 대 한 데이터를 가져오려는 것이 불가능 합니다. 이 리소스는 패키지 Id를 확인할 수 없으므로 제공 합니다. 클라이언트는을 이미 원하는 패키지 ID를 알고 있다고 가정 하는 대신 각 패키지 버전에 대 한 사용 가능한 메타 데이터 서버 구현에 따라 다릅니다. Blob에 대 한 등록 패키지 같은 계층적 구조를 가집니다.

- **인덱스**: 동일한 패키지 ID 사용 하 여 원본에서 모든 패키지에서 공유할 패키지 메타 데이터에 대 한 진입점
- **페이지**: 패키지 버전을 그룹화 합니다. 페이지에서 패키지 버전 번호는 서버 구현에서 정의 됩니다.
- **리프**: 단일 패키지 버전에 특정 문서입니다.

지정 된 패키지 ID 및 등록 리소스의 클라이언트에서 확인할 수 있습니다 예측 가능한 등록 인덱스의 URL 이며 `@id` 서비스 인덱스의 값입니다. 등록 페이지 및 리프에 대 한 Url 등록 인덱스를 검사 하 여 검색 됩니다.

### <a name="registration-pages-and-leaves"></a>등록 페이지 및 리프

엄밀히 필요한 저장 하기 위한 서버 구현에 대 한 별도 등록 페이지 문서에서 리프 등록 경우 이지만 클라이언트 쪽 메모리를 절약 하는 것이 좋습니다. 대신 인라인 모든 등록 페이지 문서에서 리프를 즉시 저장 하거나 인덱스 유지를 서버 구현은 일부 경험적 접근의 패키지 버전 번호를 기준으로 두 가지 방법 중에서 선택할 수를 정의 하는 것이 좋습니다. 또는 패키지의 누적 크기를 유지합니다.

모든 패키지 버전을 저장 (리프) 등록 인덱스 저장에는 다양 한 HTTP 요청에 패키지 메타 데이터 인출 하지만 더 큰 문서를 다운로드 해야 하 고 더 많은 클라이언트 메모리를 할당 해야 하는 데 필요한 합니다. 반면에 서버 구현은 즉시에 저장 된 경우 등록 리프 별도 페이지 문서에서 클라이언트는 필요한 정보를 가져오려면 자세한 HTTP 요청 수행 해야 합니다.

Nuget.org에서는 아래와 같습니다는 추론: 128 이상 버전의 패키지의 경우 리프 페이지 크기가 64 중단 합니다. 보다 작거나 128 버전의 경우 모든 인라인 등록 인덱스에 유지 합니다.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>요청 매개 변수

이름     | 입력     | 형식    | 필수 | 노트
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | 예      | 소문자를 유지 하는 패키지 ID

`LOWER_ID` 값은 소문자를 유지 하 여 구현 하는 규칙을 사용 하 여 원하는 패키지 ID입니다. NET의 [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) 메서드.

### <a name="response"></a>응답

응답은 다음 속성을 포함 하는 루트 개체에는 JSON 문서.

이름  | 형식             | 필수 | 노트
----- | ---------------- | -------- | -----
count | 정수          | 예      | 인덱스의 등록 페이지 수
항목 | 개체의 배열 | 예      | 등록 페이지의 배열

인덱스 개체의 각 항목 `items` 배열이 등록 페이지를 나타내는 JSON 개체입니다.

#### <a name="registration-page-object"></a>등록 페이지 개체

등록 인덱스에서 찾은 등록 페이지 개체에는 다음 속성이 있습니다.

이름   | 형식             | 필수 | 노트
------ | ---------------- | -------- | -----
@id    | string           | 예      | 등록 페이지 URL
count  | 정수          | 예      | 등록 수가 페이지 유지
항목  | 개체의 배열 | 아니요       | 등록 리프 및 연결 메타 데이터의 배열
낮은  | string           | 예      | (포괄) 페이지에서 가장 낮은 SemVer 2.0.0 버전이
부모 | string           | 아니요       | 등록 인덱스에 대 한 URL
위  | string           | 예      | (포괄) 페이지에서 가장 높은 SemVer 2.0.0 버전이

합니다 `lower` 고 `upper` page 개체의 범위는 특정 페이지 버전에 대 한 메타 데이터가 필요한 경우에 유용 합니다.
필요한 유일한 등록 페이지를 가져오려고 이러한 범위를 사용할 수 있습니다. 버전 문자열을 준수 [NuGet의 버전 규칙](../reference/package-versioning.md)합니다. 버전 문자열은 정규화 및 빌드 메타 데이터를 포함 하지 마세요. NuGet 에코 시스템의 모든 버전을 사용 하 여 버전 문자열의 비교를 사용 하 여 구현 됩니다 [SemVer 2.0.0's 버전 우선 순위 규칙](http://semver.org/spec/v2.0.0.html#spec-item-11)합니다.

합니다 `parent` 등록 페이지 개체에 있는 경우에 속성 나타납니다는 `items` 속성입니다.

경우는 `items` 속성이 인 등록 페이지는 개체에 지정 된 URL을 `@id` 개별 패키지 버전에 대 한 메타 데이터를 페치하는 데 사용할 해야 합니다. `items` 배열은 경우에 따라 최적화 된 페이지 개체에서 제외 됩니다. 단일 패키지 ID의 버전 번호 매우 크면 대규모 및 특정 버전 또는 작은 범위의 버전에 대 한 관심이 하는 클라이언트에 대 한 프로세스에 불필요 등록 인덱스 문서 수 됩니다.

경우는 `items` 속성을 사용할 수 있는지를 `@id` 속성 사용할 필요가, 아니므로 페이지 데이터를 모두 이미에서 인라인는 `items` 속성입니다.

Page 개체의 각 항목 `items` 배열이 등록 리프 나타내는 JSON 개체 및 메타 데이터에 연결 합니다.

#### <a name="registration-leaf-object-in-a-page"></a>페이지의 리프 개체 등록

등록 페이지에서 찾은 등록 리프 개체에는 다음 속성이 있습니다.

이름           | 형식   | 필수 | 노트
-------------- | ------ | -------- | -----
@id            | string | 예      | 등록 리프 URL
catalogEntry   | object | 예      | 패키지 메타 데이터가 포함 된 카탈로그 항목
packageContent | string | 예      | 패키지 콘텐츠 (.nupkg) URL

각 등록 리프 개체를 단일 패키지 버전을 사용 하 여 연결 된 데이터를 나타냅니다.

#### <a name="catalog-entry"></a>카탈로그 항목

`catalogEntry` 등록 리프 개체의 속성에는 다음 속성이 있습니다.

이름                     | 형식                       | 필수 | 노트
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | 예      | 이 개체를 생성 하는 데 사용 되는 문서 URL
authors                  | 문자열 또는 문자열 배열 | 아니요       | 
dependencyGroups         | 개체의 배열           | 아니요       | 대상 프레임 워크 별로 그룹화 된 패키지의 종속성
설명              | string                     | 아니요       | 
iconUrl                  | string                     | 아니요       | 
ID                       | string                     | 예      | 패키지의 ID
licenseUrl               | string                     | 아니요       |
licenseExpression        | string                     | 아니요       | 
나열                   | boolean                    | 아니요       | 없는 경우에 나열 된 것으로 간주 해야
minClientVersion         | string                     | 아니요       | 
projectUrl               | string                     | 아니요       | 
게시                | string                     | 아니요       | 패키지를 게시 하는 경우의 ISO 8601 타임 스탬프를 포함 하는 문자열
requireLicenseAcceptance | boolean                    | 아니요       | 
요약                  | string                     | 아니요       | 
태그                     | 문자열 또는 문자열의 배열  | 아니요       | 
제목                    | string                     | 아니요       | 
버전                  | string                     | 예      | 정규화 후 전체 버전 문자열

패키지 `version` 속성이 정규화 한 후 전체 버전 문자열입니다. 즉,이 SemVer 2.0.0 빌드 데이터를 여기 포함 될 수 있습니다.

`dependencyGroups` 속성은 대상 프레임 워크 별로 그룹화 된 패키지의 종속성을 나타내는 개체의 배열입니다. 패키지에 종속성이 없는 경우는 `dependencyGroups` 속성이 없으면 빈 배열 또는 `dependencies` 모든 그룹의 속성이 비어 있거나 없습니다.

값을 `licenseExpression` 속성을 준수 [NuGet 라이선스 식 구문](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license)합니다.

#### <a name="package-dependency-group"></a>패키지 종속성 그룹

각 종속성 그룹 개체에는 다음 속성이 있습니다.

이름            | 형식             | 필수 | 노트
--------------- | ---------------- | -------- | -----
targetFramework | string           | 아니요       | 이러한 종속성에 적용 되는 대상 프레임 워크
종속성    | 개체의 배열 | 아니요       |

합니다 `targetFramework` 문자열에는 NuGet의.NET 라이브러리에서 구현 형식 사용 [NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/)합니다. 없으면 `targetFramework` 지정, 종속성 그룹을 모든 대상 프레임 워크에 적용 됩니다.

`dependencies` 속성은 각각 현재 패키지의 패키지 종속성을 나타내는 개체의 배열입니다.

#### <a name="package-dependency"></a>패키지 종속성

각 패키지 종속성에 다음 속성이 있습니다.

이름         | 형식   | 필수 | 노트
------------ | ------ | -------- | -----
ID           | string | 예      | 패키지 종속성의 ID
range        | object | 아니요       | 허용 되 [버전 범위](../reference/package-versioning.md#version-ranges-and-wildcards) 종속성
등록 | string | 아니요       | 이 종속성에 대 한 등록 인덱스에 대 한 URL

경우는 `range` 속성은 제외 되거나 빈 문자열인 경우 클라이언트의 버전 범위는 기본값은 `(, )`합니다. 즉, 종속성의 모든 버전이 허용 됩니다.

### <a name="sample-request"></a>샘플 요청

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>샘플 응답

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

이 특정 예제의 등록 인덱스가 있으므로 인라인된 등록 페이지 개별 패키지 버전에 대 한 메타 데이터를 인출 하는 데 필요한 추가 요청이 없습니다.

## <a name="registration-page"></a>등록 페이지

등록 페이지에는 등록 리프 포함 되어 있습니다. 등록 페이지를 가져오려고 URL에 의해 결정 됩니다 합니다 `@id` 속성에는 [등록 페이지 개체](#registration-page-object) 위에서 언급 한 합니다.

경우는 `items` 의 HTTP GET 요청 배열 등록 인덱스를 제공 하지 않으면는 `@id` 값 루트로 개체에는 JSON 문서를 반환 합니다. 개체에는 다음 속성이 있습니다.

이름   | 형식             | 필수 | 노트
------ | ---------------- | -------- | -----
@id    | string           | 예      | 등록 페이지 URL
count  | 정수          | 예      | 등록 수가 페이지 유지
항목  | 개체의 배열 | 예      | 등록 리프 및 연결 메타 데이터의 배열
낮은  | string           | 예      | (포괄) 페이지에서 가장 낮은 SemVer 2.0.0 버전이
부모 | string           | 예      | 등록 인덱스에 대 한 URL
위  | string           | 예      | (포괄) 페이지에서 가장 높은 SemVer 2.0.0 버전이

등록 리프 개체의 모양을 등록 인덱스 동일 [위에](#registration-leaf-object-in-a-page)합니다.

## <a name="sample-request"></a>샘플 요청

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>샘플 응답

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>등록 리프

등록 리프 특정 패키지 ID 및 버전에 대 한 정보를 포함합니다. 이 문서에서 특정 버전에 대 한 메타 데이터를 사용 하지 못할 수도 있습니다. 패키지 메타 데이터에서 인출 되는 [등록 인덱스](#registration-index) 또는 [등록 페이지](#registration-page) (은 검색 된 등록 인덱스를 사용 하 여).

가져온 URL 등록 리프를 인출 하는 `@id` 등록 인덱스 또는 등록 페이지에서 등록 리프 개체의 속성입니다.

등록 리프는 다음 속성을 포함 하는 루트 개체를 사용 하 여 JSON 문서:

이름           | 형식    | 필수 | 노트
-------------- | ------- | -------- | -----
@id            | string  | 예      | 등록 리프 URL
catalogEntry   | string  | 아니요       | 이러한 리프를 생성 하는 카탈로그 항목 URL
나열         | boolean | 아니요       | 없는 경우에 나열 된 것으로 간주 해야
packageContent | string  | 아니요       | 패키지 콘텐츠 (.nupkg) URL
게시      | string  | 아니요       | 패키지를 게시 하는 경우의 ISO 8601 타임 스탬프를 포함 하는 문자열
등록   | string  | 아니요       | 등록 인덱스에 대 한 URL

> [!Note]
> Nuget.org에서는 `published` 값 패키지 나열 되어 있지 않으면 경우 1900 년으로 설정 됩니다.

### <a name="sample-request"></a>샘플 요청

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>샘플 응답

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
