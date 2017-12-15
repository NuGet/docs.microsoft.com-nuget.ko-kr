---
title: "카탈로그, NuGet V3 API | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/30/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: cfd338b5-6253-48c0-88ba-17c6b98fc935
description: "카탈로그는 모든 패키지를 만들고 삭제할 nuget.org에의 한 인덱스입니다."
keywords: "NuGet V3 API 카탈로그, nuget.org 트랜잭션 로그를 NuGet.org 복제, NuGet.org, 추가 전용 레코드 NuGet.org의 복제"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 50e329680c5527d2a69d9c2b1421dc3aa609b478
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="catalog"></a>Catalog

**카탈로그** 은 작성과 삭제와 같은 패키지 소스에 대 한 모든 패키지 작업을 기록 하는 리소스입니다. 카탈로그 리소스에는 `Catalog` 에 입력 된 [서비스 인덱스](service-index.md)합니다.

> [!Note]
> 공식 NuGet 클라이언트에서 카탈로그를 사용 하지 않으므로 모든 패키지 소스 카탈로그를 구현 합니다.

> [!Note]
> 현재, nuget.org 카탈로그는 중국에서 사용할 수 없습니다. 자세한 내용은 참조 하십시오. [NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949)합니다.

## <a name="versioning"></a>버전 관리

다음 `@type` 값이 사용 됩니다.

@type 값   | 참고
------------- | -----
Catalog/3.0.0 | 초기 릴리스

## <a name="base-url"></a>기준 URL

다음 Api에 대 한 항목 지점 URL의 값은 고 `@id` 앞에서 언급 한 리소스와 연결 된 속성 `@type` 값입니다. 이 항목의 자리 표시자 URL을 사용 하 여 `{@id}`합니다.

## <a name="http-methods"></a>HTTP 메서드

카탈로그 리소스 지원 HTTP 방법만 있는 모든 Url `GET` 및 `HEAD`합니다.

## <a name="catalog-index"></a>카탈로그의 인덱스

카탈로그의 인덱스는 cronologically 정렬 카탈로그 항목의 목록이 있는 잘 알려진 위치에 문서. 카탈로그 리소스의 진입점은

인덱스는 카탈로그 페이지의 구성 됩니다. 각 카탈로그 페이지는 카탈로그 항목을 포함 합니다. 카탈로그 항목에 각 시간에서 지점에서 단일 패키지에 관한 이벤트를 나타냅니다. 카탈로그 항목은 생성 된 목록에 없는 relisted, 또는 삭제 된 패키지 소스에서 패키지를 나타낼 수 있습니다. 시간 순서에 따라 카탈로그 항목을 처리 하 여 클라이언트 V3 패키지 소스에 있는 모든 패키지의 최신 상태 보기를 빌드할 수 있습니다.

즉, 카탈로그 blob은 다음 계층 구조:

- **인덱스**: 카탈로그에 대 한 진입점입니다.
- **페이지**: 카탈로그 항목의 그룹입니다.
- **리프**: 단일 패키지의 상태 스냅숏을 카탈로그 항목을 나타내는 문서입니다.

각 카탈로그 개체에 라는 속성이 `commitTimeStamp` 카탈로그에 항목이 추가 된 때를 나타내는입니다. 카탈로그 항목은 일괄 처리로 커밋 호출 카탈로그 페이지에 추가 됩니다. 모든 카탈로그 항목 동일한 커밋에는 동일한 커밋 타임 스탬프 (`commitTimeStamp`) 및 커밋 ID (`commitId`). 동일한 커밋에 배치 되는 카탈로그 항목에 일어난 같은 지정 시간으로 패키지 소스에서 이벤트를 나타냅니다. 카탈로그 커밋 내에서 순서가 있지 않습니다.

각 패키지 ID와 버전은 고유 하므로 될 수 없으므로 둘 이상의 카탈로그 항목이 경우 커밋에서입니다. 이렇게 하면 단일 패키지에 대 한 카탈로그 항목 순서 수 있도록 항상 될 명확 하 게 커밋 타임 스탬프를 기준으로 합니다.

일 수 없습니다. 둘 이상의 커밋 당 카탈로그에는 `commitTimeStamp`합니다. 즉,는 `commitId` 중복 되는 `commitTimeStamp`합니다.

달리는 [패키지 메타 데이터 리소스](registration-base-url-resource.md), 패키지 ID 기준으로 인덱싱되어 있으면 있는,이 카탈로그는 인덱싱된 (및 쿼리할 수) 시간에 의해서만 합니다.

카탈로그 항목은 일정 하 게 증가 하는 시간 순서로 카탈로그에 항상 추가 됩니다. 이 카탈로그 커밋 시간 X에 추가 되 면 다음 카탈로그 커밋 안 함은 현재까지 추가 의미 X 적은 시간을 사용 합니다.

다음 요청 카탈로그의 인덱스를 인출합니다.

```
GET {@id}
```

카탈로그의 인덱스는 다음 속성을 가진 개체가 포함 된 JSON 문서:

이름            | 형식             | 필수 | 참고
--------------- | ---------------- | -------- | -----
commitId        | string           | 예      | 가장 최근의 커밋와 연결 된 고유 ID
commitTimeStamp | string           | 예      | 가장 최근의 커밋 타임 스탬프
count           | 정수          | 예      | 인덱스의 페이지 수
항목           | 개체의 배열 | 예      | 각 개체는 페이지를 나타내는 개체 배열

각 요소에는 `items` 배열에는 각 페이지에 대 한 최소한의 몇 가지 세부 정보를 가진 개체입니다. 이러한 페이지 개체 카탈로그 leaves (항목)를 포함 하지 않습니다. 이 배열에 있는 요소의 순서는 정의 되지 않았습니다. 클라이언트가 사용 하 여 메모리에서 페이지를 정렬할 수 자신의 `commitTimeStamp` 속성입니다.

새 페이지 도입 되는 `count` 증가 하 고 새 개체에 표시 됩니다는 `items` 배열입니다.

카탈로그와 인덱스의 항목을 추가할 때 `commitId` 바뀝니다 및 `commitTimeStamp` 증가 합니다. 이러한 속성은 두 가지 요약 기본적으로 모든 페이지를 덮어쓰며 `commitId` 및 `commitTimeStamp` 값에 `items` 배열입니다.

### <a name="catalog-page-object-in-the-index"></a>인덱스의 카탈로그 페이지 개체

카탈로그의 인덱스에서 카탈로그 페이지 개체 찾을 수 `items` 속성에는 다음과 같은 속성이 있어야 합니다.

이름            | 형식    | 필수 | 참고
--------------- | ------- | -------- | -----
@id             | string  | 예      | Fetch 카탈로그 페이지의 URL
commitId        | string  | 예      | 이 페이지에서 가장 최근의 커밋와 연결 된 고유 ID
commitTimeStamp | string  | 예      | 이 페이지에서 가장 최근의 커밋 타임 스탬프
count           | 정수 | 예      | 카탈로그 페이지의 항목 수

달리는 [패키지 메타 데이터 리소스](registration-base-url-resource.md) 인라인 사례 중 일부는 인덱스에 유지, 카탈로그 리프 인덱스에 인라이닝 된 전혀 없는 및 페이지를 사용 하 여 가져올 수는 항상 `@id` URL입니다.

### <a name="sample-request"></a>샘플 요청

```
GET https://api.nuget.org/v3/catalog0/index.json
```

### <a name="sample-response"></a>샘플 응답

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>카탈로그 페이지

카탈로그 페이지는 카탈로그 항목의 컬렉션입니다. 가 중 하나를 사용 하 여 인출 된 문서는 `@id` 카탈로그의 인덱스 값을 찾을 수 있습니다. 카탈로그 페이지의 URL은 예측 가능 하 게 없으며 카탈로그 인덱스만 사용 하 여 검색 해야 합니다.

새 카탈로그 항목이 가장 높은 커밋 타임 스탬프에만 카탈로그 인덱스에서 페이지 또는 새 페이지에 추가 됩니다. 더 높은 커밋 타임 스탬프가 있는 페이지를 카탈로그에 추가 되 면 오래 된 페이지는 추가 되거나 변경 되지 않습니다.

카탈로그 페이지 문서는 다음 속성을 가진 JSON 개체:

이름            | 형식             | 필수 | 참고
--------------- | ---------------- | -------- | -----
commitId        | string           | 예      | 이 페이지에서 가장 최근의 커밋와 연결 된 고유 ID
commitTimeStamp | string           | 예      | 이 페이지에서 가장 최근의 커밋 타임 스탬프
count           | 정수          | 예      | 페이지의 항목 수
항목           | 개체의 배열 | 예      | 이 페이지의 카탈로그 항목
부모          | string           | 예      | 카탈로그의 인덱스에 대 한 URL

각 요소에는 `items` 배열은 카탈로그 항목에 대 한 최소한의 몇 가지 세부 정보를 가진 개체입니다. 이러한 항목 개체의 모든 카탈로그 항목의 데이터를 포함 되지 않습니다. 페이지의 항목 순서 `items` 배열 정의 되어 있지 않습니다. 클라이언트가 사용 하 여 메모리에 항목을 정렬할 수 자신의 `commitTimeStamp` 속성입니다.

페이지에서 카탈로그 항목의 수는 서버 구현에 의해 정의 됩니다. Nuget.org에 대 한 항목이 최대 550 각 페이지에서 시간에 실제 수는 일부 페이지 dependong 지점에서 다음 커밋 일괄 처리의 크기에 대 한 더 작은 수 있지만.

새 항목 도입 되는 `count` 에 증가 하 고 새 카탈로그 항목 개체 표시 되는 `items` 배열입니다.

페이지에 항목이 추가 되는 `commitId` 변경 내용 및 `commitTimeStamp` 증가 합니다. 이 두 속성 모두 기본적으로 요약은 `commitId` 및 `commitTimeStamp` 값에 `items` 배열입니다.

### <a name="catalog-item-object-in-a-page"></a>카탈로그 항목 페이지에는 개체

카탈로그 페이지에서 카탈로그 항목 개체를 찾을 `items` 속성에는 다음과 같은 속성이 있어야 합니다.

이름            | 형식    | 필수 | 참고
--------------- | ------- | -------- | -----
@id             | string  | 예      | 카탈로그 항목을 인출 하는 URL
@type           | string  | 예      | 카탈로그 항목의 형식
commitId        | string  | 예      | 이 카탈로그 항목에 연결 된 커밋 ID
commitTimeStamp | string  | 예      | 이 카탈로그 항목의 커밋 타임 스탬프
nuget:id        | string  | 예      | 이 리프 관련이 있는 패키지 ID
nuget:version   | string  | 예      | 이 리프 관련이 패키지 버전

`@type` 값은 다음 두 값 중 하나로 설정 됩니다.

1. `nuget:PackageDetails`:이에 해당 `PackageDetails` 카탈로그 리프 문서를 입력 합니다.
1. `nuget:PackageDelete`:이에 해당는 `PackageDelete` 카탈로그 리프 문서를 입력 합니다.

각 종류를 의미 하는 방법에 대 한 자세한 내용은 [형식 항목에 해당](#item-types) 아래 합니다.

### <a name="sample-request"></a>샘플 요청

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

### <a name="sample-response"></a>샘플 응답

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>리프 카탈로그

카탈로그 리프 시간에 특정 패키지 ID 및 특정 시점에는 버전에 대 한 메타 데이터를 포함합니다. 가 사용 하 여 인출 된 문서는 `@id` 카탈로그 페이지에서 값을 찾을 수 있습니다. 카탈로그 리프 URL predictedable 수 없습니다 및 카탈로그 페이지에만 사용 하 여 검색 해야 합니다.

카탈로그 리프 문서는 다음 속성을 가진 JSON 개체:

이름                    | 형식                       | 필수 | 참고
----------------------- | -------------------------- | -------- | -----
@type                   | 문자열 또는 문자열의 배열 | 예      | 카탈로그 항목의 형식
카탈로그: commitId        | string                     | 예      | 이 카탈로그 항목에 연결 된 커밋 ID
카탈로그: commitTimeStamp | string                     | 예      | 이 카탈로그 항목의 커밋 타임 스탬프
ID                      | string                     | 예      | 카탈로그 항목의 패키지 ID
게시               | string                     | 예      | 패키지 카탈로그 항목의 게시 된 날짜
version                 | string                     | 예      | 카탈로그 항목의 패키지 버전

### <a name="item-types"></a>항목 형식

`@type` 속성은 문자열 또는 문자열 배열입니다. 편의 위해 하는 경우는 `@type` 값은 문자열, 배열입니다. 하나는 크기 것으로 처리 해야 합니다. 에 대 한 모든 가능한 값 `@type` 설명 되어 있습니다. 그러나 각 카탈로그 항목에는 다음 두 개의 문자열 형식 값 중 하나만.

1. `PackageDetails`: 패키지 메타 데이터의 스냅숏을 나타냅니다.
1. `PackageDelete`: 삭제 된 패키지를 나타냅니다

### <a name="package-details-catalog-items"></a>패키지 세부 정보 카탈로그 항목

카탈로그 항목 형식과 `PackageDetails` 특정 패키지 (ID 및 버전 조합)에 대 한 패키지 메타 데이터의 스냅숏을 포함 합니다. 패키지 소스에서 다음과 같은 시나리오 중 하나를 발견 한 경우 패키지 세부 정보 카탈로그 항목이 생성 됩니다.

1. 패키지는 **푸시**합니다.
1. 패키지는 **나열**합니다.
1. 패키지는 **목록에 없는**합니다.
1. 패키지는 **리플로우되면서**합니다.

패키지 다시 흐름에는 기본적으로 패키지 자체를 변경 하지 않고 기존 패키지의 가짜 밀어넣기를 생성 하는 관리 밀기입니다. Nuget.org에 다시 흐름 카탈로그를 사용 하는 백그라운드 작업 중 하나에 버그를 해결 한 후 사용 됩니다.

카탈로그 항목을 사용 하는 클라이언트는 카탈로그 항목을 생성 하는 이러한 시나리오를 결정 하려고 해서는 안 됩니다. 대신, 클라이언트 단순히 업데이트 해야 유지 관리 되는 뷰나 인덱스 카탈로그 항목에 포함 된 메타 데이터를 사용 합니다. 또한 중복 되었습니다. 카탈로그 항목의 처리 정상적으로 (멱).

패키지 세부 정보 카탈로그 항목 외에 다음 속성이 [모든 카탈로그 리프에 포함 된](#catalog-leaf)합니다.

이름                    | 형식                       | 필수 | 참고
----------------------- | -------------------------- | -------- | -----
authors                 | string                     | no       |
created                 | string                     | 예      | 패키지를 처음 만들 때의 타임 스탬프
dependencyGroups        | 개체의 배열           | no       | 동일한 형식으로 [패키지 메타 데이터 리소스](registration-base-url-resource.md#package-dependency-group)
설명             | string                     | no       |
iconUrl                 | string                     | no       |
isPrerelease            | boolean                    | 예      | 패키지 버전은 시험판 여부
language                | string                     | no       |
licenseUrl              | string                     | no       |
나열                  | boolean                    | no       | 패키지가 나열 되는 여부
Minclientversion이        | string                     | no       |
packageHash             | string                     | 예      | 인코딩을 사용 하 여 패키지의 해시가 [표준 base 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | string                     | 예      |
packageSize             | 정수                    | 예      | 패키지.nupkg 바이트 크기
projectUrl              | string                     | no       |
releaseNotes            | string                     | no       |
requireLicenseAgreement | boolean                    | no       | 가정 `false` 제외 하는 경우
요약                 | string                     | no       |
태그                    | 문자열의 배열           | no       |
제목                   | string                     | no       |
verbatimVersion         | string                     | no       | 그대로 버전 문자열이 고.nuspec에 있는 원래

패키지 `version` 속성은 전체, 정규화 된 버전 문자열입니다. 즉,는 SemVer 2.0.0 빌드 데이터를 여기 포함 될 수 있습니다.

`created` 타임 스탬프는 패키지는 일반적으로 짧은 시간 카탈로그 항목의 커밋 타임 스탬프 이전의 패키지 소스에서 먼저 수신 되었을 때.

`packageHashAlgorithm` 서버 구현 represeting에서 정의 문자열 해시 알고리즘을 생성 하는 데 사용 되는 `packageHash`합니다. 항상 사용 nuget.org는 `packageHashAlgorithm` 값 `SHA512`합니다.

`published` 타임 스탬프는 패키지가 마지막으로 나열 된 시간입니다.

> [!Note]
> Nuget.org에 `published` 값 패키지 나열 되어 있지 않으면 경우 1900 년으로 설정 됩니다.

#### <a name="sample-request"></a>샘플 요청

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

#### <a name="sample-response"></a>샘플 응답

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>패키지 카탈로그 항목 삭제

카탈로그 항목 형식과 `PackageDelete` 나타내는 카탈로그 클라이언트에 패키지 패키지 소스에서 삭제 되었습니다 (예: 복원)의 패키지 작업에 대해 사용할 수 없는 정보의 최소 집합을 포함 합니다.

> [!Note]
> 패키지 삭제 하 고 동일한 패키지 ID와 버전에는 나중에 다시 게시를 사용 하 여에 대 한 것 같습니다. Nuget.org를 패키지 ID와 버전 의미 특정 패키지 콘텐츠는 공식 클라이언트의 가정을 나누는 것 매우 드문 경우입니다. Nuget.org에 패키지 삭제에 대 한 자세한 내용은 참조 [보호 정책](../policies/deleting-packages.md)합니다.

패키지 카탈로그 항목 삭제 하는 것 외에도 추가 속성이 있어야 [모든 카탈로그 리프에 포함 된](#catalog-leaf)합니다.

`version` 속성은 패키지.nuspec에 있는 원래 버전 문자열입니다.

`published` 속성은 패키지를 삭제 하는 시기는 일반적으로 카탈로그 항목의 커밋 타임 스탬프 이전의 짧은 시간으로 시간입니다.

#### <a name="sample-request"></a>샘플 요청

```
GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json
```

#### <a name="sample-response"></a>샘플 응답

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Cursor

### <a name="overview"></a>개요

이 섹션에는 프로토콜에서 위임 되지 않는 있지만 모든 실질적인 카탈로그 클라이언트 구현의 일부를 기준으로 여야 하는 클라이언트 개념을 설명 합니다.

카탈로그는 추가 전용 데이터 구조 시간으로 인덱싱된 이기 때문에 클라이언트를 저장 해야는 **커서** 로컬에 클라이언트가 있는 시점까지 나타내는 처리 카탈로그 항목입니다. 이 커서 값은 생성 되지 않고 수 클라이언트의 컴퓨터 시계를 사용 하 여 참고 합니다. 값은 카탈로그 개체의에서 가져와야 하는 대신, `commitTimestamp` 값입니다.

클라이언트가 패키지 소스에서 새 이벤트를 처리할 때마다 할 카탈로그 쿼리 커밋 타임 스탬프를 갖는 모든 카탈로그 항목에 대 한 해당 저장된 커서 보다 큽니다. 클라이언트가 새 카탈로그 항목은 모두를 성공적으로 처리만 새 커서 값으로 처리 하는 카탈로그 항목의 최신 커밋 타임 스탬프를 기록 합니다.

이 방법을 사용 하면 클라이언트 하지 패키지 소스에서 발생 한 모든 패키지 이벤트를 놓칠 되도록 할 수 있습니다.
또한 클라이언트에 다시 커서의 기록 된 커밋 타임 스탬프 이전의 이전 이벤트를 처리할 수 없습니다.

이 강력한 개념 커서의 다양 한 nuget.org 백그라운드 작업에 사용 되 고 V3 API 자체를 최신 상태로 유지 하는 데 사용 됩니다. 

### <a name="initial-value"></a>초기 값

카탈로그 클라이언트 맨 처음에 대 한 시작 (및 따라서 값이 없는 커서) 하는 경우의 기본값 커서를 사용 해야 합니다. NET의 `System.DateTimeOffset.MinValue` 또는 일부 이러한 유사한 개념 표현할 수 있는 최소 타임 스탬프입니다.

### <a name="iterating-over-catalog-items"></a>카탈로그 항목을 반복

처리 하는 카탈로그 항목의 다음 집합을 쿼리하려면 클라이언트는 다음을 수행 해야 합니다.

1. 로컬 저장소에서 기록 된 커서 값을 인출 합니다.
1. 다운로드 한 카탈로그의 인덱스를 deserialize 합니다.
1. 모든 카탈로그 커밋 타임 스탬프를 사용 하 여 페이지 찾기 *보다 큰* 커서입니다.
1. 빈 목록을 처리할 카탈로그 항목을 선언 합니다.
1. 각 카탈로그 페이지에 대해 3 단계에서 일치 합니다.
   1. 다운로드 하 고 카탈로그 페이지를 역직렬화 합니다.
   1. 모든 카탈로그 항목 커밋 타임 스탬프가 찾기 *보다 큰* 커서입니다.
   1. 4 단계에서 선언 된 변수에 일치 하는 모든 카탈로그 항목을 추가 합니다.
1. 카탈로그 항목 목록 커밋 타임 스탬프 순으로 정렬 합니다.
1. 순서로 각 카탈로그 항목을 처리 합니다.
   1. 다운로드 한 카탈로그 항목을 deserialize 합니다.
   1. 카탈로그 항목의 형식에 적절 하 게 동작 합니다.
   1. 클라이언트 관련 방식에서으로 카탈로그 항목 문서를 처리 합니다.
1. 새 커서 값으로 마지막 카탈로그 항목의 커밋 타임 스탬프를 기록 합니다.

이 기본 알고리즘 클라이언트 구현에서 패키지 원본에서 사용할 수 있는 모든 패키지의 전체 보기를 구축할 수 있습니다. 클라이언트는 주기적으로 항상 알아야 할 패키지 원본에 대 한 최신 변경 내용을이 알고리즘을 실행만 필요 합니다.

> [!Note]
> 알고리즘은이 해당 nuget.org 유지를 사용 하 여는 [패키지 메타 데이터](registration-base-url-resource.md), [패키지 콘텐츠](package-base-address-resource.md), [검색](search-query-service-resource.md) 및 [자동 완성](search-autocomplete-service-resource.md) 최신 리소스입니다.

### <a name="dependent-cursors"></a>종속 커서

클라이언트의 출력 다른 클라이언트의 출력에 따라 달라 집니다 inherant 종속성이 있는 있는 두 명의 카탈로그 클라이언트가 가정 합니다. 

#### <a name="example"></a>예제

예를 들어 nuget.org 새로 게시 된 패키지 해야에 나타나지 검색 리소스 패키지 메타 데이터 리소스에 표시 되기 전에 합니다. 패키지 메타 데이터 리소스를 사용 하는 공식 NuGet 클라이언트가 수행한 "복원" 작업 때문입니다. 고객 검색 서비스를 사용 하 여 패키지를 발견 패키지 메타 데이터 리소스를 사용 하 여 해당 패키지를 성공적으로 복원할 수 있습니다. 즉, 검색 리소스 패키지 메타 데이터 리소스에 따라 달라 집니다. 각 리소스에 해당 리소스를 업데이트 하는 카탈로그 클라이언트 백그라운드 작업이 됩니다. 각 클라이언트는 자체 커서를 있습니다.

두 리소스가 검색 리소스를 업데이트 하는 카탈로그 클라이언트의 커서 카탈로그에서 작성 된 이후 *이상 사용해 서는 안* 패키지 메타 데이터 카탈로그 클라이언트 커서입니다.

#### <a name="algorithm"></a>알고리즘

를 구현 하기 위해이 제한을 단순 되도록 위의 알고리즘을 수정 합니다.

1. 로컬 저장소에서 기록 된 커서 값을 인출 합니다.
1. 다운로드 한 카탈로그의 인덱스를 deserialize 합니다.
1. 모든 카탈로그 커밋 타임 스탬프를 사용 하 여 페이지 찾기 *보다 큰* 커서 **종속성의 커서 보다 작습니다.**
1. 빈 목록을 처리할 카탈로그 항목을 선언 합니다.
1. 각 카탈로그 페이지에 대해 3 단계에서 일치 합니다.
   1. 다운로드 하 고 카탈로그 페이지를 역직렬화 합니다.
   1. 모든 카탈로그 항목 커밋 타임 스탬프가 찾기 *보다 큰* 커서 **종속성의 커서 보다 작습니다.**
   1. 4 단계에서 선언 된 변수에 일치 하는 모든 카탈로그 항목을 추가 합니다.
1. 카탈로그 항목 목록 커밋 타임 스탬프 순으로 정렬 합니다.
1. 순서로 각 카탈로그 항목을 처리 합니다.
   1. 다운로드 한 카탈로그 항목을 deserialize 합니다.
   1. 카탈로그 항목의 형식에 적절 하 게 동작 합니다.
   1. 클라이언트 관련 방식에서으로 카탈로그 항목 문서를 처리 합니다.
1. 새 커서 값으로 마지막 카탈로그 항목의 커밋 타임 스탬프를 기록 합니다.

이 수정 된 알고리즘을 사용 하 여 빌드할 수 종속 카탈로그는 클라이언트의 시스템 자신의 특정 인덱스, 아티팩트 등 모든를 생성 합니다.
