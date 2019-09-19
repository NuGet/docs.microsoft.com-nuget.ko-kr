---
title: 패키지 콘텐츠, NuGet API
description: 패키지 기본 주소는 패키지 자체를 인출 하기 위한 간단한 인터페이스입니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 7aea28d6224a89149aa33be035c82a45db3058f0
ms.sourcegitcommit: 1eda83ab537c86cc27316e7bc67f95a358766e63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/18/2019
ms.locfileid: "71094123"
---
# <a name="package-content"></a>패키지 콘텐츠

V3 API를 사용 하 여 임의의 패키지의 콘텐츠 (nupkg 파일)를 인출 하는 URL을 생성할 수 있습니다. 패키지 콘텐츠를 가져오는 데 사용 되는 리소스 `PackageBaseAddress` 는 [서비스 인덱스](service-index.md)에 있는 리소스입니다. 또한이 리소스는 나열 되거나 나열 되지 않은 패키지의 모든 버전을 검색할 수 있도록 합니다.

이 리소스를 일반적으로 "패키지 기본 주소" 또는 "플랫 컨테이너" 라고 합니다.

## <a name="versioning"></a>버전 관리

사용 되는 값은 다음과 같습니다. `@type`

@type 값              | 참고
------------------------ | -----
PackageBaseAddress/3.0.0 | 초기 릴리스

## <a name="base-url"></a>기준 URL

다음 api에 대 한 기준 URL은 앞서 언급 한 리소스 `@id` `@type` 값과 연결 된 속성의 값입니다. 다음 문서에서는 자리 표시자 기준 URL `{@id}` 이 사용 됩니다.

## <a name="http-methods"></a>HTTP 메서드

등록 리소스에서 찾은 모든 url은 HTTP 메서드 `GET` 및 `HEAD`를 지원 합니다.

## <a name="enumerate-package-versions"></a>패키지 버전 열거

클라이언트에서 패키지 ID를 알고 있고 패키지 원본에서 사용할 수 있는 패키지 버전을 검색 하려는 경우 클라이언트는 예측 가능한 URL을 생성 하 여 모든 패키지 버전을 열거할 수 있습니다. 이 목록은 아래에 설명 된 패키지 콘텐츠 API에 대 한 "디렉터리 목록"입니다.

> [!Note]
> 이 목록에는 나열 되거나 나열 되지 않은 패키지 버전이 모두 포함 되어 있습니다.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>요청 매개 변수

이름     | 입력     | 형식    | 필수 | 참고
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | 예      | 패키지 ID, lowercased

`LOWER_ID` 값은에 의해 구현 된 규칙을 사용 하 여 원하는 패키지 ID lowercased. NET의 [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) 메서드입니다.

### <a name="response"></a>응답

패키지 원본에 제공 된 패키지 ID 버전이 없으면 404 상태 코드가 반환 됩니다.

패키지 원본에 하나 이상의 버전이 있는 경우 200 상태 코드가 반환 됩니다. 응답 본문은 다음 속성을 포함 하는 JSON 개체입니다.

이름     | 형식             | 필수 | 참고
-------- | ---------------- | -------- | -----
버전 | 문자열 배열 | 예      | 사용 가능한 버전

`versions` 배열의 문자열은 [정규화 된 NuGet 버전 문자열](../concepts/package-versioning.md#normalized-version-numbers)lowercased입니다. 버전 문자열에는 SemVer 2.0.0 build 메타 데이터가 포함 되지 않습니다.

이 배열에 있는 버전 문자열을 다음 끝점에 있는 `LOWER_VERSION` 토큰에 대해 약어를 사용 하 여 사용할 수 있습니다.

### <a name="sample-request"></a>샘플 요청

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>샘플 응답

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>패키지 콘텐츠 다운로드 (. nupkg)

클라이언트에서 패키지 ID 및 버전을 인식 하 고 패키지 콘텐츠를 다운로드 하려는 경우 다음 URL을 생성 하기만 하면 됩니다.

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>요청 매개 변수

이름          | 입력     | 형식   | 필수 | 참고
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | 예      | 패키지 ID, 소문자
LOWER_VERSION | URL    | string | 예      | 패키지 버전, 정규화 및 lowercased

`LOWER_ID` 및`LOWER_VERSION` 는 모두에서 구현 된 규칙을 사용 하 여 lowercased 됩니다. 네트워크[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
메서드를 재정의합니다.

는 `LOWER_VERSION` NuGet의 버전 [정규화 규칙](../concepts/package-versioning.md#normalized-version-numbers)을 사용 하 여 정규화 된 패키지 버전을 정규화 합니다. 즉,이 경우 SemVer 2.0.0 사양에서 허용 하는 빌드 메타 데이터를 제외 해야 합니다.

### <a name="response-body"></a>응답 본문

패키지가 패키지 원본에 있으면 200 상태 코드가 반환 됩니다. 응답 본문은 패키지 콘텐츠 자체가 됩니다.

패키지가 패키지 원본에 없으면 404 상태 코드가 반환 됩니다.

### <a name="sample-request"></a>샘플 요청

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>샘플 응답

Newtonsoft.json 9.0.1에 대 한. nupkg 이진 스트림입니다.

## <a name="download-package-manifest-nuspec"></a>패키지 매니페스트 (. nuspec) 다운로드

클라이언트에서 패키지 ID 및 버전을 인식 하 고 패키지 매니페스트를 다운로드 하려는 경우 다음 URL을 생성 하기만 하면 됩니다.

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>요청 매개 변수

이름          | 입력     | 형식   | 필수 | 참고
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | 예      | 패키지 ID, 소문자
LOWER_VERSION | URL    | string | 예      | 패키지 버전, 정규화 및 lowercased

`LOWER_ID` 및`LOWER_VERSION` 는 모두에서 구현 된 규칙을 사용 하 여 lowercased 됩니다. NET의 [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) 메서드입니다.

는 `LOWER_VERSION` NuGet의 버전 [정규화 규칙](../concepts/package-versioning.md#normalized-version-numbers)을 사용 하 여 정규화 된 패키지 버전을 정규화 합니다. 즉,이 경우 SemVer 2.0.0 사양에서 허용 하는 빌드 메타 데이터를 제외 해야 합니다.

### <a name="response-body"></a>응답 본문

패키지가 패키지 원본에 있으면 200 상태 코드가 반환 됩니다. 응답 본문은 해당. nupkg에 포함 된 nuspec 패키지 매니페스트입니다. . Nuspec은 XML 문서입니다.

패키지가 패키지 원본에 없으면 404 상태 코드가 반환 됩니다.

### <a name="sample-request"></a>샘플 요청

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>샘플 응답

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
