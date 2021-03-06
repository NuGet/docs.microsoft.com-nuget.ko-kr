---
title: 카탈로그 리소스, NuGet V3 API
description: 카탈로그는 nuget.org에서 만들어지고 삭제 된 모든 패키지의 인덱스입니다.
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6c04453fec9beb7b0998953384ec60694e1213c1
ms.sourcegitcommit: af059dc776cfdcbad20baab2919b5d6dc1e9022d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2021
ms.locfileid: "99990146"
---
# <a name="catalog"></a>카탈로그

**카탈로그** 는 생성 및 삭제와 같은 패키지 원본에 대 한 모든 패키지 작업을 기록 하는 리소스입니다. 카탈로그 리소스의 `Catalog` 형식은 [서비스 인덱스](service-index.md)에 있습니다. 이 리소스를 사용 하 여 [게시 된 모든 패키지를 쿼리할](../guides/api/query-for-all-published-packages.md)수 있습니다.

> [!Note]
> 카탈로그는 공식 NuGet 클라이언트에서 사용 되지 않으므로 모든 패키지 원본이 카탈로그를 구현 하는 것은 아닙니다.

> [!Note]
> 현재 nuget.org 카탈로그는 중국에서 사용할 수 없습니다. 자세한 내용은 [NuGet/NuGetGallery # 4949](https://github.com/NuGet/NuGetGallery/issues/4949)를 참조 하세요.

## <a name="versioning"></a>버전 관리

사용 되는 `@type` 값은 다음과 같습니다.

@type 값   | 참고
------------- | -----
Catalog/3.0.0 | 초기 릴리스

## <a name="base-url"></a>기준 URL

다음 Api에 대 한 진입점 URL은 `@id` 앞서 언급 한 리소스 값과 연결 된 속성의 값입니다 `@type` . 이 항목에서는 자리 표시자 URL을 사용 `{@id}` 합니다.

## <a name="http-methods"></a>HTTP 메서드

카탈로그 리소스에 있는 모든 Url은 HTTP 메서드 및만 지원 `GET` 합니다 `HEAD` .

## <a name="catalog-index"></a>카탈로그 인덱스

카탈로그 인덱스는 카탈로그 항목 목록이 시간순으로 정렬 된 잘 알려진 위치에 있는 문서입니다. 카탈로그 리소스의 진입점입니다.

인덱스는 카탈로그 페이지로 구성 됩니다. 각 카탈로그 페이지에는 카탈로그 항목이 포함 되어 있습니다. 각 카탈로그 항목은 특정 시점의 단일 패키지와 관련 된 이벤트를 나타냅니다. 카탈로그 항목은 패키지 원본에서 생성, 나열 되지 않음, 다시 나열 또는 삭제 된 패키지를 나타낼 수 있습니다. 클라이언트는 시간 순서로 카탈로그 항목을 처리 하 여 V3 패키지 원본에 있는 모든 패키지의 최신 뷰를 작성할 수 있습니다.

간단히 말해서 카탈로그 blob의 계층 구조는 다음과 같습니다.

- **Index**: 카탈로그의 진입점입니다.
- **Page**: 카탈로그 항목의 그룹입니다.
- **리프**: 단일 패키지 상태의 스냅숏의 카탈로그 항목을 나타내는 문서입니다.

각 카탈로그 개체에는 `commitTimeStamp` 항목이 카탈로그에 추가 된 경우를 나타내는 라는 속성이 있습니다. 카탈로그 항목은 커밋 이라는 일괄 처리에서 카탈로그 페이지에 추가 됩니다. 동일한 커밋의 모든 카탈로그 항목은 커밋 타임 스탬프 ( `commitTimeStamp` )와 커밋 ID ()가 동일 합니다 `commitId` . 동일한 커밋에 배치 된 카탈로그 항목은 패키지 원본에서 동일한 시점에 발생 한 이벤트를 나타냅니다. 카탈로그 커밋 내에는 순서가 없습니다.

각 패키지 ID 및 버전은 고유 하므로 커밋에는 둘 이상의 카탈로그 항목이 없습니다. 이렇게 하면 커밋 타임 스탬프에 대해 단일 패키지에 대 한 카탈로그 항목이 항상 명확 하 게 정렬 될 수 있습니다.

에는 카탈로그에 대 한 커밋이 두 개 이상 있을 수 없습니다 `commitTimeStamp` . 즉,는 `commitId` 와 중복 됩니다 `commitTimeStamp` .

패키지 ID로 인덱싱되는 [패키지 메타 데이터 리소스](registration-base-url-resource.md)와 달리 카탈로그는 시간에 의해서만 인덱싱되어 쿼리 가능 합니다.

카탈로그 항목은 항상 일정 한 시간 순서에 따라 카탈로그에 추가 됩니다. 즉, 카탈로그 커밋이 X 시간에 추가 되는 경우 카탈로그 커밋이 X 보다 작거나 같은 시간으로 추가 되지 않습니다.

다음 요청은 카탈로그 인덱스를 인출 합니다.

```
GET {@id}
```

카탈로그 인덱스는 다음 속성을 포함 하는 개체를 포함 하는 JSON 문서입니다.

이름            | Type             | 필수 | 참고
--------------- | ---------------- | -------- | -----
commitId        | 문자열           | 예      | 가장 최근 커밋에 연결 된 고유 ID입니다.
commitTimeStamp | 문자열           | 예      | 가장 최근 커밋의 타임 스탬프입니다.
count           | integer          | 예      | 인덱스의 페이지 수입니다.
items           | 개체의 배열 | 예      | 개체의 배열입니다. 각 개체는 페이지를 나타냅니다.

배열의 각 요소 `items` 는 각 페이지에 대 한 최소한의 세부 정보를 포함 하는 개체입니다. 이러한 페이지 개체는 카탈로그 리프 (항목)을 포함 하지 않습니다. 이 배열에 있는 요소의 순서는 정의 되지 않습니다. 클라이언트는 해당 속성을 사용 하 여 페이지를 메모리에 정렬할 수 있습니다 `commitTimeStamp` .

새 페이지가 도입 되 면이 `count` 증가 하 고 배열에 새 개체가 표시 됩니다 `items` .

항목이 카탈로그에 추가 되 면 인덱스는 `commitId` 변경 되 고가 `commitTimeStamp` 증가 합니다. 이러한 두 속성은 기본적으로 배열에 있는 모든 페이지와 값에 대 한 요약 `commitId` `commitTimeStamp` `items` 입니다.

### <a name="catalog-page-object-in-the-index"></a>인덱스의 카탈로그 페이지 개체

카탈로그 인덱스의 속성에 있는 카탈로그 페이지 개체의 `items` 속성은 다음과 같습니다.

이름            | Type    | 필수 | 참고
--------------- | ------- | -------- | -----
@id             | 문자열  | 예      | 카탈로그를 가져올 URL 페이지
commitId        | 문자열  | 예      | 이 페이지의 가장 최근 커밋에 연결 된 고유 ID입니다.
commitTimeStamp | 문자열  | 예      | 이 페이지에서 가장 최근의 커밋 타임 스탬프
count           | integer | 예      | 카탈로그 페이지의 항목 수

일부 경우에는 인덱스에 inlines 된 [패키지 메타 데이터 리소스](registration-base-url-resource.md) 와 달리 카탈로그 리프는 인덱스에 인라인되지 않으며 항상 페이지 URL을 사용 하 여 인출 되어야 합니다 `@id` .

### <a name="sample-request"></a>샘플 요청

```
GET https://api.nuget.org/v3/catalog0/index.json
```

### <a name="sample-response"></a>샘플 응답

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>카탈로그 페이지

카탈로그 페이지는 카탈로그 항목의 컬렉션입니다. 카탈로그 인덱스에 있는 값 중 하나를 사용 하 여 인출 된 문서입니다 `@id` . 카탈로그 페이지에 대 한 URL은 예측 하기 위한 것이 아니며 카탈로그 인덱스만 사용 하 여 검색 해야 합니다.

새 카탈로그 항목은 가장 높은 커밋 타임 스탬프 또는 새 페이지로만 카탈로그 인덱스의 페이지에 추가 됩니다. 커밋 타임 스탬프가 더 높은 페이지가 카탈로그에 추가 되 면 이전 페이지가 추가 되거나 변경 되지 않습니다.

카탈로그 페이지 문서는 다음 속성을 포함 하는 JSON 개체입니다.

이름            | Type             | 필수 | 참고
--------------- | ---------------- | -------- | -----
commitId        | 문자열           | 예      | 이 페이지의 가장 최근 커밋에 연결 된 고유 ID입니다.
commitTimeStamp | 문자열           | 예      | 이 페이지에서 가장 최근의 커밋 타임 스탬프
count           | integer          | 예      | 페이지의 항목 수입니다.
items           | 개체의 배열 | 예      | 이 페이지의 카탈로그 항목
부모(parent)          | 문자열           | 예      | 카탈로그 인덱스에 대 한 URL입니다.

배열의 각 요소 `items` 는 카탈로그 항목에 대 한 최소한의 세부 정보를 포함 하는 개체입니다. 이러한 항목 개체에는 카탈로그 항목의 모든 데이터가 포함 되어 있지 않습니다. 페이지 배열의 항목 순서는 `items` 정의 되지 않습니다. 클라이언트는 해당 속성을 사용 하 여 항목을 메모리로 정렬할 수 있습니다 `commitTimeStamp` .

페이지의 카탈로그 항목 수는 서버 구현에 의해 정의 됩니다. Nuget.org의 경우 각 페이지에는 최대 550 개의 항목이 있지만 특정 시점에서 다음 커밋 일괄 처리의 크기에 따라 일부 페이지의 경우 실제 숫자가 작을 수 있습니다.

새 항목이 도입 되 면 `count` 이 증가 하 고 새 카탈로그 항목 개체가 배열에 표시 됩니다 `items` .

항목이 페이지에 추가 되 면 `commitId` 변경 내용과가 `commitTimeStamp` 늘어납니다. 이러한 두 속성은 기본적으로 배열의 모든 및 값에 대 한 요약 `commitId` `commitTimeStamp` `items` 입니다.

### <a name="catalog-item-object-in-a-page"></a>페이지의 카탈로그 항목 개체

카탈로그 페이지의 속성에 있는 카탈로그 항목 개체의 `items` 속성은 다음과 같습니다.

이름            | Type    | 필수 | 참고
--------------- | ------- | -------- | -----
@id             | 문자열  | 예      | 카탈로그 항목을 페치할 URL입니다.
@type           | 문자열  | 예      | 카탈로그 항목의 유형입니다.
commitId        | 문자열  | 예      | 이 카탈로그 항목과 연결 된 커밋 ID입니다.
commitTimeStamp | 문자열  | 예      | 이 카탈로그 항목의 커밋 타임 스탬프입니다.
nuget: id        | 문자열  | 예      | 이 리프가 관련 된 패키지 ID입니다.
nuget: 버전   | 문자열  | 예      | 이 리프가 관련 된 패키지 버전입니다.

`@type`값은 다음 두 값 중 하나가 됩니다.

1. `nuget:PackageDetails`: `PackageDetails` 카탈로그 리프 문서의 형식에 해당 합니다.
1. `nuget:PackageDelete`: `PackageDelete` 카탈로그 리프 문서의 형식에 해당 합니다.

각 형식의 의미에 대 한 자세한 내용은 아래의 [해당 항목 형식](#item-types) 을 참조 하세요.

### <a name="sample-request"></a>샘플 요청

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

### <a name="sample-response"></a>샘플 응답

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>카탈로그 리프

카탈로그 리프는 특정 시점의 특정 패키지 ID 및 버전에 대 한 메타 데이터를 포함 합니다. 카탈로그 페이지에 있는 값을 사용 하 여 인출 된 문서입니다 `@id` . 카탈로그 리프에 대 한 URL은 예측 하기 위한 것이 아니며 카탈로그 페이지만 사용 하 여 검색 해야 합니다.

카탈로그 리프 문서는 다음 속성을 포함 하는 JSON 개체입니다.

이름                    | Type                       | 필수 | 참고
----------------------- | -------------------------- | -------- | -----
@type                   | 문자열 또는 문자열 배열 | 예      | 카탈로그 항목의 유형입니다.
카탈로그: commitId        | 문자열                     | 예      | 이 카탈로그 항목과 연결 된 커밋 ID입니다.
카탈로그: commitTimeStamp | 문자열                     | 예      | 이 카탈로그 항목의 커밋 타임 스탬프입니다.
id                      | 문자열                     | 예      | 카탈로그 항목의 패키지 ID
published               | 문자열                     | 예      | 패키지 카탈로그 항목의 게시 된 날짜입니다.
버전                 | 문자열                     | 예      | 카탈로그 항목의 패키지 버전입니다.

### <a name="item-types"></a>항목 유형

`@type`속성은 문자열 또는 문자열 배열입니다. 편의상 `@type` 값이 문자열이 면 크기 1의 배열로 처리 되어야 합니다. 의 모든 가능한 값 `@type` 이 문서화 된 것은 아닙니다. 그러나 각 카탈로그 항목에는 다음 두 문자열 형식 값 중 하나만 포함 됩니다.

1. `PackageDetails`: 패키지 메타 데이터의 스냅숏을 나타냅니다.
1. `PackageDelete`: 삭제 된 패키지를 나타냅니다.

### <a name="package-details-catalog-items"></a>패키지 정보 카탈로그 항목

유형이 있는 카탈로그 항목 `PackageDetails` 에는 특정 패키지에 대 한 패키지 메타 데이터의 스냅숏 (ID 및 버전 조합)이 포함 됩니다. 패키지 정보 카탈로그 항목은 패키지 원본에서 다음 시나리오 중 하나가 발생할 때 생성 됩니다.

1. 패키지가 **푸시됩니다**.
1. 패키지가 **나열** 됩니다.
1. 패키지는 **나열** 되지 않습니다.
1. 패키지는 **reflowed** 입니다.

패키지 리플로우는 기본적으로 패키지 자체를 변경 하지 않고 기존 패키지의 가짜 푸시를 생성 하는 관리 제스처입니다. Nuget.org에서 카탈로그를 사용 하는 백그라운드 작업 중 하나에서 버그를 수정 하 고 나 서 리플로우를 사용 합니다.

카탈로그 항목을 사용 하는 클라이언트는 카탈로그 항목을 생성 하는 시나리오를 결정 하려고 하지 않아야 합니다. 대신, 클라이언트는 카탈로그 항목에 포함 된 메타 데이터를 사용 하 여 유지 관리 된 뷰나 인덱스를 업데이트 해야 합니다. 또한 중복 되거나 중복 된 카탈로그 항목을 정상적으로 처리 해야 합니다 (idempotently).

패키지 정보 카탈로그 항목에는 [모든 카탈로그에 포함 된](#catalog-leaf)항목 외에 다음과 같은 속성이 있습니다.

이름                    | Type                       | 필수 | 참고
----------------------- | -------------------------- | -------- | -----
authors                 | 문자열                     | 아니요       |
created                 | 문자열                     | 아니요       | 패키지를 처음 만들 때의 타임 스탬프입니다. 대체 `published` (Fallback) 속성:
dependencyGroups        | 개체의 배열           | 아니요       | 대상 프레임 워크를 기준으로 그룹화 된 패키지의 종속성 ([패키지 메타 데이터 리소스와 동일한 형식](registration-base-url-resource.md#package-dependency-group))
중단             | object                     | 아니요       | 패키지와 관련 된 사용 중단 ([패키지 메타 데이터 리소스와 동일한 형식](registration-base-url-resource.md#package-deprecation))
description             | 문자열                     | 아니요       |
iconUrl                 | 문자열                     | 아니요       |
isPrerelease            | boolean                    | 아니요       | 패키지 버전이 시험판 인지 여부입니다. 에서 검색할 수 있습니다 `version` .
언어                | 문자열                     | 아니요       |
licenseUrl              | 문자열                     | 아니요       |
나열                  | boolean                    | 아니요       | 패키지가 나열 되는지 여부
minClientVersion        | 문자열                     | 아니요       |
packageHash             | 문자열                     | 예      | 패키지의 해시, [표준 기본 64](https://tools.ietf.org/html/rfc4648#section-4) 를 사용 하 여 인코딩
packageHashAlgorithm    | 문자열                     | 예      |
packageSize             | integer                    | 예      | Nupkg의 크기 (바이트)입니다.
packageTypes            | 개체의 배열           | 아니요       | 작성자가 지정한 패키지 유형입니다.
projectUrl              | 문자열                     | 아니요       |
releaseNotes            | 문자열                     | 아니요       |
requireLicenseAgreement | boolean                    | 아니요       | `false`제외 된 경우 가정
요약                 | 문자열                     | 아니요       |
tags                    | 문자열 배열           | 아니요       |
title                   | 문자열                     | 아니요       |
verbatimVersion         | 문자열                     | 아니요       | 원래 nuspec에 있는 버전 문자열입니다.
취약성         | 개체의 배열           | 아니요       | 패키지의 보안 취약점

Package `version` 속성은 정규화 후의 전체 버전 문자열입니다. 이는 SemVer 2.0.0 build 데이터가 여기에 포함 될 수 있음을 의미 합니다.

`created`타임 스탬프는 패키지 원본에서 패키지를 처음 받을 때 이며 일반적으로 카탈로그 항목의 커밋 타임 스탬프 보다 짧은 시간입니다.

는를 `packageHashAlgorithm` 생성 하는 데 사용 되는 해시 알고리즘을 나타내는 서버 구현에 의해 정의 된 문자열입니다 `packageHash` . nuget.org는 항상 `packageHashAlgorithm` 값을 사용 `SHA512` 합니다.

`packageTypes`속성은 패키지 형식이 작성자에 의해 지정 된 경우에만 표시 됩니다. 존재 하는 경우 항상 하나 이상의 (1) 항목이 있어야 합니다. 배열의 각 항목 `packageTypes` 은 다음 속성을 포함 하는 JSON 개체입니다.

이름      | Type    | 필수 | 참고
--------- | ------- | -------- | -----
name      | 문자열  | 예      | 패키지 형식의 이름입니다.
버전    | 문자열  | 아니요       | 패키지 유형의 버전입니다. 작성자가 nuspec의 버전을 명시적으로 지정한 경우에만 존재 합니다.

`published`타임 스탬프는 패키지가 마지막으로 나열 된 시간입니다.

> [!Note]
> Nuget.org에서 패키지를 `published` 나열 하지 않으면 값이 1900 년으로 설정 됩니다.

#### <a name="vulnerabilities"></a>취약점

`vulnerability` 개체의 배열입니다. 각 취약점에는 다음과 같은 속성이 있습니다.

이름         | Type   | 필수 | 참고
------------ | ------ | -------- | -----
advisoryUrl  | 문자열 | 예      | 패키지에 대 한 보안 권고의 위치
severity     | 문자열 | 예      | 권고 심각도: "0" = 낮음, "1" = 보통, "2" = 높음, "3" = 위험

속성에 `severity` 여기에 나열 된 값 이외의 값이 포함 되어 있는 경우에는이 권고의 심각도가 Low로 처리 됩니다.

#### <a name="sample-request"></a>샘플 요청

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

#### <a name="sample-response"></a>샘플 응답

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>패키지 삭제 카탈로그 항목

유형의 카탈로그 항목에는 패키지가 `PackageDelete` 패키지 원본에서 삭제 되었으며 패키지 작업 (예: 복원)에 더 이상 사용할 수 없다는 것을 나타내는 최소한의 정보 집합이 포함 되어 있습니다.

> [!NOTE]
> 패키지를 삭제 하 고 나중에 동일한 패키지 ID 및 버전을 사용 하 여 다시 게시할 수 있습니다. Nuget.org에서는 패키지 ID와 버전이 특정 패키지 콘텐츠를 암시 한다고 가정 하 여 공식 클라이언트의 가정이 중단 되는 경우가 매우 드뭅니다. Nuget.org에서 패키지를 삭제 하는 방법에 대 한 자세한 내용은 [정책](../nuget-org/policies/deleting-packages.md)을 참조 하세요.

패키지 삭제 카탈로그 항목에는 [모든 카탈로그에 포함 된](#catalog-leaf)항목 이외에 추가 속성이 없습니다.

`version`속성은 nuspec에 있는 원래 버전 문자열입니다.

`published`속성은 패키지가 삭제 된 시간입니다. 일반적으로 카탈로그 항목의 커밋 타임 스탬프 보다 짧은 시간입니다.

#### <a name="sample-request"></a>샘플 요청

```
GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json
```

#### <a name="sample-response"></a>샘플 응답

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>커서

### <a name="overview"></a>개요

이 섹션에서는 프로토콜에 의해 반드시 지정 되는 것은 아니지만 실제 카탈로그 클라이언트 구현에 포함 되어야 하는 클라이언트 개념에 대해 설명 합니다.

카탈로그는 시간별로 인덱싱되는 추가 전용 데이터 구조 이므로 클라이언트는 **커서** 를 로컬로 저장 하 여 클라이언트가 카탈로그 항목을 처리 한 시점까지 표시 합니다. 이 커서 값은 클라이언트의 컴퓨터 클록을 사용 하 여 생성 하면 안 됩니다. 대신 카탈로그 개체의 값에서 값을 가져와야 합니다 `commitTimestamp` .

클라이언트는 패키지 원본에서 새 이벤트를 처리 하려고 할 때마다 커밋 타임 스탬프가 저장 된 커서 보다 큰 모든 카탈로그 항목에 대해 카탈로그를 쿼리해야 합니다. 클라이언트는 모든 새 카탈로그 항목을 성공적으로 처리 한 후 새 커서 값으로 처리 된 카탈로그 항목의 최신 커밋 타임 스탬프를 기록 합니다.

클라이언트는이 방법을 사용 하 여 패키지 원본에서 발생 한 패키지 이벤트를 놓치지 않도록 할 수 있습니다.
또한 클라이언트는 커서의 기록 된 커밋 타임 스탬프 전에 이전 이벤트를 다시 처리할 필요가 없습니다.

이러한 강력한 커서 개념은 많은 nuget.org 백그라운드 작업에 사용 되며 V3 API 자체를 최신 상태로 유지 하는 데 사용 됩니다. 

### <a name="initial-value"></a>초기 값

카탈로그 클라이언트를 처음부터 시작 하 여 커서 값이 없는 경우의 기본 커서 값을 사용 해야 합니다. NET의 `System.DateTimeOffset.MinValue` 표현 가능한 최소 타임 스탬프에 대 한 이러한 유사한 개념입니다.

### <a name="iterating-over-catalog-items"></a>카탈로그 항목 반복

처리할 다음 카탈로그 항목 집합을 쿼리하려면 클라이언트는 다음을 수행 해야 합니다.

1. 로컬 저장소에서 기록 된 커서 값을 페치합니다.
1. 카탈로그 인덱스를 다운로드 하 고 deserialize 합니다.
1. 커밋 타임 스탬프가 커서 *보다 큰* 모든 카탈로그 페이지를 찾습니다.
1. 처리할 카탈로그 항목의 빈 목록을 선언 합니다.
1. 3 단계에서 일치 하는 각 카탈로그 페이지에 대해 다음을 수행 합니다.
   1. 카탈로그 페이지를 다운로드 하 고 역직렬화 합니다.
   1. 커밋 타임 스탬프가 커서 *보다 큰* 모든 카탈로그 항목을 찾습니다.
   1. 4 단계에서 선언 된 목록에 일치 하는 모든 카탈로그 항목을 추가 합니다.
1. 커밋 타임 스탬프를 기준으로 카탈로그 항목 목록을 정렬 합니다.
1. 각 카탈로그 항목을 순서 대로 처리 합니다.
   1. 카탈로그 항목을 다운로드 하 고 deserialize 합니다.
   1. 카탈로그 항목의 형식에 맞게 적절 하 게 대응 합니다.
   1. 클라이언트 관련 방식으로 카탈로그 항목 문서를 처리 합니다.
1. 마지막 카탈로그 항목의 커밋 타임 스탬프를 새 커서 값으로 기록 합니다.

이 기본 알고리즘을 사용 하면 클라이언트 구현에서 패키지 원본에서 사용할 수 있는 모든 패키지의 전체 뷰를 작성할 수 있습니다. 클라이언트는 항상 패키지 원본에 대 한 최신 변경 내용을 인식 하도록이 알고리즘을 정기적으로 실행 해야 합니다.

> [!Note]
> 이 알고리즘은 [패키지 메타 데이터](registration-base-url-resource.md), [패키지 콘텐츠](package-base-address-resource.md), [검색](search-query-service-resource.md) 및 [자동 완성](search-autocomplete-service-resource.md) 리소스를 최신 상태로 유지 하기 위해 nuget.org에서 사용 하는 알고리즘입니다.

### <a name="dependent-cursors"></a>종속 커서

한 클라이언트의 출력이 다른 클라이언트의 출력에 종속 되는 고유 종속성이 있는 두 개의 카탈로그 클라이언트가 있다고 가정 합니다. 

#### <a name="example"></a>예제

예를 들어 nuget.org에서 새로 게시 된 패키지는 패키지 메타 데이터 리소스에 표시 되기 전에 검색 리소스에 표시 되어서는 안 됩니다. 이는 공식 NuGet 클라이언트에서 수행 하는 "복원" 작업이 패키지 메타 데이터 리소스를 사용 하기 때문입니다. 고객이 검색 서비스를 사용 하 여 패키지를 검색 하는 경우 패키지 메타 데이터 리소스를 사용 하 여 해당 패키지를 성공적으로 복원할 수 있어야 합니다. 즉, 검색 리소스는 패키지 메타 데이터 리소스에 따라 달라 집니다. 각 리소스에는 해당 리소스를 업데이트 하는 카탈로그 클라이언트 백그라운드 작업이 있습니다. 각 클라이언트에는 고유한 커서가 있습니다.

두 리소스가 모두 카탈로그에서 빌드되기 때문에 검색 리소스를 업데이트 하는 카탈로그 클라이언트의 커서는 패키지 메타 데이터 카탈로그 클라이언트의 커서를 *벗어나지 않아야 합니다* .

#### <a name="algorithm"></a>알고리즘

이 제한을 구현 하려면 위의 알고리즘을 다음과 같이 수정 하면 됩니다.

1. 로컬 저장소에서 기록 된 커서 값을 페치합니다.
1. 카탈로그 인덱스를 다운로드 하 고 deserialize 합니다.
1. 커밋 타임 스탬프가 커서 보다 **작거나 같은** 커서 *보다 큰* 모든 카탈로그 페이지를 찾습니다.
1. 처리할 카탈로그 항목의 빈 목록을 선언 합니다.
1. 3 단계에서 일치 하는 각 카탈로그 페이지에 대해 다음을 수행 합니다.
   1. 카탈로그 페이지를 다운로드 하 고 역직렬화 합니다.
   1. 커밋 타임 스탬프를 포함 하는 모든 카탈로그 항목 **을 종속성의 커서 보다 작거나 같은** 커서 보다 *크게* 찾습니다.
   1. 4 단계에서 선언 된 목록에 일치 하는 모든 카탈로그 항목을 추가 합니다.
1. 커밋 타임 스탬프를 기준으로 카탈로그 항목 목록을 정렬 합니다.
1. 각 카탈로그 항목을 순서 대로 처리 합니다.
   1. 카탈로그 항목을 다운로드 하 고 deserialize 합니다.
   1. 카탈로그 항목의 형식에 맞게 적절 하 게 대응 합니다.
   1. 클라이언트 관련 방식으로 카탈로그 항목 문서를 처리 합니다.
1. 마지막 카탈로그 항목의 커밋 타임 스탬프를 새 커서 값으로 기록 합니다.

이 수정 된 알고리즘을 사용 하 여 고유한 특정 인덱스, 아티팩트 등을 생성 하는 종속 카탈로그 클라이언트 시스템을 빌드할 수 있습니다.
