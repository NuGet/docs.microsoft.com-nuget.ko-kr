---
title: 패키지 콘텐츠를 NuGet API
description: 패키지 기준 주소에는 패키지 자체를 가져오기 위해 간단한 인터페이스입니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2f0f93e0cee78ea03cbd53194cdc2a10871fd7e1
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426761"
---
# <a name="package-content"></a>패키지 콘텐츠

V3 API를 사용 하는 임의의 패키지의 콘텐츠 (.nupkg 파일)를 가져올 URL을 생성 하는 것이 가능 합니다. 패키지 콘텐츠를 가져오는 중에 사용 되는 리소스를 `PackageBaseAddress` 에서 리소스를 찾을 합니다 [서비스 인덱스](service-index.md)합니다. 이 리소스에 나열 된 패키지의 모든 버전의 검색도 사용 하도록 설정 또는 비공개입니다.

이 리소스 일반적으로 라고 "플랫 컨테이너" 또는 "패키지 기본 주소가"으로 합니다.

## <a name="versioning"></a>버전 관리

다음 `@type` 값이 사용 됩니다.

@type 값              | 노트
------------------------ | -----
PackageBaseAddress/3.0.0 | 초기 릴리스

## <a name="base-url"></a>기준 URL

다음 Api에 대 한 기본 URL의 값은는 `@id` 앞에서 언급 한 리소스와 연결 된 속성 `@type` 값입니다. 다음 문서에서 자리 표시자 기준 URL `{@id}` 사용 됩니다.

## <a name="http-methods"></a>HTTP 메서드

HTTP 메서드를 등록 리소스 지원에서 발견 한 모든 Url `GET` 고 `HEAD`입니다.

## <a name="enumerate-package-versions"></a>패키지 버전을 열거 합니다.

클라이언트 패키지 ID를 알고 있는 패키지 버전 패키지를 검색 하려는 경우 원본에서 사용할 수 있는, 클라이언트가 모든 패키지 버전을 열거 하는 예측 가능한 URL을 생성할 수 있습니다. 이 목록은 아래에 설명 된 패키지 콘텐츠 API에 대 한 "디렉터리 목록" 할 것입니다.

> [!Note]
> 이 목록에 나열 되며 목록에 없는 패키지 버전을 모두 포함 되어 있습니다.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>요청 매개 변수

이름     | 입력     | 형식    | 필수 | 노트
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | 예      | 소문자의 패키지 ID

`LOWER_ID` 값은 소문자를 유지 하 여 구현 하는 규칙을 사용 하 여 원하는 패키지 ID입니다. NET의 [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) 메서드.

### <a name="response"></a>응답

패키지 소스에 제공 된 패키지 ID의 버전 없음, 404 상태 코드가 반환 됩니다.

패키지 원본 하나 또는 여러 버전에 200 상태 코드가 반환 됩니다. 응답 본문은 다음 속성과 함께 JSON 개체:

이름     | 형식             | 필수 | 노트
-------- | ---------------- | -------- | -----
버전 | 문자열의 배열 | 예      | 패키지 Id 제공

문자열을 `versions` 배열의 모든 소문자 [NuGet 버전 문자열을 정규화](../reference/package-versioning.md#normalized-version-numbers)합니다. 버전 문자열에는 SemVer 2.0.0 빌드 메타 데이터가 포함 되지 않습니다.

의도이 배열에서 찾은 버전 문자열에 대 한 정확 하 게 사용할 수 있는지를 `LOWER_VERSION` 다음 끝점에서 토큰을 찾을.

### <a name="sample-request"></a>샘플 요청

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>샘플 응답

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>패키지 콘텐츠 (.nupkg) 다운로드

클라이언트 패키지 ID 및 버전을 알고 패키지 콘텐츠 다운로드 하려는 경우 다음 URL을 생성 하려면만 필요 합니다.

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>요청 매개 변수

이름          | 입력     | 형식   | 필수 | 노트
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | 예      | 소문자의 패키지 ID
LOWER_VERSION | URL    | string | 예      | 패키지 버전을 표준화 하 고 소문자를 유지

둘 다 `LOWER_ID` 고 `LOWER_VERSION` 구현한 규칙을 사용 하 여 소문자를 유지 됩니다. NET의 [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
메서드를 재정의합니다.

합니다 `LOWER_VERSION` 원하는 패키지 버전 정규화 된 NuGet의 버전을 사용 하 여 [정규화 규칙](../reference/package-versioning.md#normalized-version-numbers)합니다. 즉, SemVer 2.0.0 사양에서 허용 되는 빌드 메타 데이터는이 경우 제외 해야 합니다.

### <a name="response-body"></a>응답 본문

패키지를 패키지 원본에 있는 경우에 200 상태 코드가 반환 됩니다. 응답 본문에 패키지 콘텐츠 자체 됩니다.

패키지는 패키지 원본에 없는 경우, 404 상태 코드가 반환 됩니다.

### <a name="sample-request"></a>샘플 요청

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>샘플 응답

Newtonsoft.Json 9.0.1에 대 한.nupkg 있는 이진 스트림.

## <a name="download-package-manifest-nuspec"></a>패키지 매니페스트 (.nuspec) 다운로드

클라이언트 패키지 ID 및 버전을 알고 있습니다. 패키지 매니페스트를 다운로드 하려는 경우 다음 URL을 생성 하려면만 필요 합니다.

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>요청 매개 변수

이름          | 입력     | 형식   | 필수 | 노트
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | 예      | 소문자의 패키지 ID
LOWER_VERSION | URL    | string | 예      | 패키지 버전을 표준화 하 고 소문자를 유지

둘 다 `LOWER_ID` 고 `LOWER_VERSION` 구현한 규칙을 사용 하 여 소문자를 유지 됩니다. NET의 [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) 메서드.

합니다 `LOWER_VERSION` 원하는 패키지 버전 정규화 된 NuGet의 버전을 사용 하 여 [정규화 규칙](../reference/package-versioning.md#normalized-version-numbers)합니다. 즉, SemVer 2.0.0 사양에서 허용 되는 빌드 메타 데이터는이 경우 제외 해야 합니다.

### <a name="response-body"></a>응답 본문

패키지를 패키지 원본에 있는 경우에 200 상태 코드가 반환 됩니다. 응답 본문에는 해당.nupkg에 포함 된.nuspec 패키지 매니페스트를 수 있습니다. .Nuspec는 XML 문서입니다.

패키지는 패키지 원본에 없는 경우, 404 상태 코드가 반환 됩니다.

### <a name="sample-request"></a>샘플 요청

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>샘플 응답

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
