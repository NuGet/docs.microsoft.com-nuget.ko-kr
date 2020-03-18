---
title: NuGet 서버 API 개요
description: NuGet 서버 API는 패키지를 다운로드 하 고, 메타 데이터를 가져오고, 새 패키지를 게시 하는 데 사용할 수 있는 HTTP 끝점 집합입니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: aacf56a5dc5af9abf6f60d42bc7fd530a128d0d8
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428290"
---
# <a name="nuget-server-api"></a>NuGet 서버 API

NuGet 서버 API는 패키지를 다운로드 하 고, 메타 데이터를 가져오고, 새 패키지를 게시 하 고, 공식 NuGet 클라이언트에서 사용할 수 있는 대부분의 다른 작업을 수행 하는 데 사용할 수 있는 HTTP 끝점 집합입니다.

이 API는 Visual Studio, nuget.exe 및 .NET CLI의 NuGet 클라이언트에서 [`dotnet restore`](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)와 같은 nuget 작업을 수행 하 고, VISUAL studio UI에서 검색 하 고, [`nuget.exe push`](../reference/cli-reference/cli-ref-push.md)하는 데 사용 됩니다.

참고 일부의 경우 nuget.org에 다른 패키지 원본에서 적용 하지 않는 추가 요구 사항이 있습니다. 이러한 차이점은 [Nuget.org 프로토콜](nuget-protocols.md)에서 설명 합니다.

사용 가능한 nuget.exe 버전을 간단히 열거 하 고 다운로드 하려면 [tools. json](tools-json.md) 끝점을 참조 하세요.

## <a name="service-index"></a>인덱스 제공

API에 대 한 진입점은 잘 알려진 위치의 JSON 문서입니다. 이 문서를 **서비스 인덱스**라고 합니다. Nuget.org에 대 한 서비스 인덱스의 위치를 `https://api.nuget.org/v3/index.json`합니다.

이 JSON 문서에는 다양 한 기능을 제공 하 고 다양 한 사용 사례를 충족 하는 *리소스* 목록이 포함 되어 있습니다.

API를 지 원하는 클라이언트는 해당 패키지 원본에 연결 하는 수단으로 이러한 서비스 인덱스 URL 중 하나 이상을 수락 해야 합니다.

서비스 인덱스에 대 한 자세한 내용은 [해당 API 참조](service-index.md)를 참조 하세요.

## <a name="versioning"></a>버전 관리

API는 NuGet의 HTTP 프로토콜 버전 3입니다. 이 프로토콜을 "V3 API" 라고도 합니다. 이러한 참조 문서는이 프로토콜 버전을 단순히 "API"로 지칭 합니다.

서비스 인덱스 스키마 버전은 서비스 인덱스의 `version` 속성으로 표시 됩니다. API는 버전 문자열에 `3`의 주 버전 번호가 있음을 요구 합니다. 서비스 인덱스 스키마에 대 한 주요 변경 내용이 적용 되지 않으므로 버전 문자열의 부 버전이 증가 합니다.

이전 클라이언트 (예: nuget.exe 2.x)는 V3 API를 지원 하지 않으며 여기에 설명 되지 않은 이전 V2 API만 지원 합니다.

NuGet V3 API는 V2 API의 후속 작업으로 이름이 지정 됩니다 .이 api는 2.x 버전의 공식 NuGet 클라이언트에서 구현 된 OData 기반 프로토콜입니다. V3 API는 공식 NuGet 클라이언트의 3.0 버전에서 처음으로 지원 되었으며 NuGet 클라이언트, 4.0 및에서 지원 되는 최신 주요 프로토콜 버전입니다. 

API가 처음 출시 된 이후에 중단 된 프로토콜 변경 내용이 적용 되었습니다.

## <a name="resources-and-schema"></a>리소스 및 스키마

**서비스 인덱스** 는 다양 한 리소스를 설명 합니다. 현재 지원 되는 리소스 집합은 다음과 같습니다.

리소스 이름                                                        | 필수 | Description
-------------------------------------------------------------------- | -------- | -----------
[카탈로그](catalog-resource.md)                                       | 아니요       | 모든 패키지 이벤트의 전체 레코드입니다.
[PackageBaseAddress](package-base-address-resource.md)               | 예      | 패키지 콘텐츠 가져오기 (. nupkg)
[PackageDetailsUriTemplate](package-details-template-resource.md)    | 아니요       | 패키지 정보 웹 페이지에 액세스 하기 위한 URL을 생성 합니다.
[PackagePublish](package-publish-resource.md)                        | 예      | 패키지를 푸시 및 삭제 하거나 목록에서 삭제 합니다.
[RegistrationsBaseUrl](registration-base-url-resource.md)            | 예      | 패키지 메타 데이터를 가져옵니다.
[ReportAbuseUriTemplate](report-abuse-resource.md)                   | 아니요       | 보고서 신고 웹 페이지에 액세스 하기 위한 URL을 생성 합니다.
[RepositorySignatures](repository-signatures-resource.md)            | 아니요       | 리포지토리 서명에 사용 되는 인증서를 가져옵니다.
[SearchAutocompleteService](search-autocomplete-service-resource.md) | 아니요       | 하위 문자열로 패키지 Id 및 버전을 검색 합니다.
[SearchQueryService](search-query-service-resource.md)               | 예      | 키워드별로 패키지를 필터링 하 고 검색 합니다.
[기호 Packagepublish](symbol-package-publish-resource.md)           | 아니요       | 기호 패키지를 푸시합니다.

일반적으로 API 리소스에서 반환 하는 이진이 아닌 데이터는 모두 JSON을 사용 하 여 직렬화 됩니다. 서비스 인덱스의 각 리소스에서 반환 하는 응답 스키마는 해당 리소스에 대해 개별적으로 정의 됩니다. 각 리소스에 대 한 자세한 내용은 위에 나열 된 항목을 참조 하십시오.

이후에는 프로토콜이 진화 함에 따라 새 속성이 JSON 응답에 추가 될 수 있습니다. 클라이언트에서 미래를 증명 하려면 구현에서 응답 스키마가 최종 이며 추가 데이터를 포함할 수 없다고 가정 하면 안 됩니다. 구현에서 인식 하지 않는 모든 속성은 무시 해야 합니다.

> [!Note]
> 소스가 `SearchAutocompleteService`를 구현 하지 않는 경우에는 자동 완성 동작을 정상적으로 사용 하지 않도록 설정 해야 합니다. `ReportAbuseUriTemplate`를 구현 하지 않으면 공식 NuGet 클라이언트는 nuget ( [nuget/Home # 4924](https://github.com/NuGet/Home/issues/4924)에서 추적)의 신고 URL로 대체 합니다. 다른 클라이언트는 단순히 사용자에 게 신고 URL을 표시 하지 않도록 선택할 수 있습니다.

### <a name="undocumented-resources-on-nugetorg"></a>Nuget.org의 문서화 되지 않은 리소스

Nuget.org의 V3 서비스 인덱스에는 위에 설명 되지 않은 일부 리소스가 있습니다. 리소스를 문서화 하지 않는 이유는 다음과 같습니다.

먼저 nuget.org의 구현 세부 정보로 사용 되는 리소스를 문서화 하지 않습니다. `SearchGalleryQueryService`는이 범주에 속합니다. [NuGetGallery](https://github.com/NuGet/NuGetGallery) 는이 리소스를 사용 하 여 일부 V2 (OData) 쿼리를 데이터베이스를 사용 하는 대신 검색 인덱스에 위임 합니다. 이 리소스는 확장성을 위해 도입 되었으며 외부에서 사용 하기 위한 것이 아닙니다.

둘째, 공식 클라이언트의 RTM 버전에서 배송 되지 않은 리소스는 문서화 하지 않습니다.
`PackageDisplayMetadataUriTemplate` 및 `PackageVersionDisplayMetadataUriTemplate`이 범주에 속합니다.

Thirdly V2 프로토콜과 긴밀 하 게 결합 된 리소스를 문서화 하지 않습니다. 이러한 리소스 자체는 의도적으로 문서화 되지 않습니다. `LegacyGallery` 리소스는이 범주에 속합니다. 이 리소스를 통해 V3 서비스 인덱스는 해당 V2 원본 URL을 가리킬 수 있습니다. 이 리소스는 `nuget.exe list`을 지원 합니다.

리소스가 여기에 문서화 되어 있지 않은 경우에 *는이에* 대 한 종속성을 사용 하지 않는 것이 좋습니다. 이러한 문서화 되지 않은 리소스의 동작을 제거 하거나 변경 하 여 예기치 않은 방식으로 구현을 중단할 수 있습니다.

## <a name="timestamps"></a>타임스탬프

API에서 반환 되는 모든 타임 스탬프는 UTC 이거나 [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 표현을 사용 하 여 지정 됩니다. 

## <a name="http-methods"></a>HTTP 메서드

동사   | 사용
------ | -----------
GET    | 일반적으로 데이터를 검색 하는 읽기 전용 작업을 수행 합니다.
HEAD   | 해당 `GET` 요청에 대 한 응답 헤더를 페치합니다.
PUT    | 존재 하지 않는 리소스를 만들거나, 존재 하는 경우 업데이트 합니다. 일부 리소스는 업데이트를 지원 하지 않을 수 있습니다.
Delete | 리소스를 삭제 하거나 목록에서 제거 합니다.

## <a name="http-status-codes"></a>HTTP 상태 코드

코드 | Description
---- | -----
200  | 성공 및 응답 본문이 있습니다.
201  | 성공 및 리소스가 생성 되었습니다.
202  | 성공, 요청이 수락 되었지만 일부 작업이 완료 되지 않고 비동기적으로 완료 될 수 있습니다.
204  | 성공 했지만 응답 본문이 없습니다.
301  | 영구 리디렉션입니다.
302  | 임시 리디렉션입니다.
400  | URL 또는 요청 본문의 매개 변수가 유효 하지 않습니다.
401  | 제공 된 자격 증명이 잘못 되었습니다.
403  | 제공 된 자격 증명에 대해 작업을 수행할 수 없습니다.
404  | 요청 된 리소스가 없습니다.
409  | 요청이 기존 리소스와 충돌 합니다.
500  | 서비스에서 예기치 않은 오류가 발생 했습니다.
503  | 서비스를 일시적으로 사용할 수 없습니다.

API 끝점에 대 한 모든 `GET` 요청에서 HTTP 리디렉션 (301 또는 302)을 반환할 수 있습니다. 클라이언트는 `Location` 헤더를 관찰 하 고 후속 `GET`를 실행 하 여 이러한 리디렉션을 정상적으로 처리 해야 합니다. 특정 끝점과 관련 된 설명서는 리디렉션을 사용할 수 있는 경우를 명시적으로 호출 하지 않습니다.

500 수준 상태 코드의 경우 클라이언트는 적절 한 재시도 메커니즘을 구현할 수 있습니다. 공식 NuGet 클라이언트는 500 수준 상태 코드 또는 TCP/DNS 오류가 발생할 때 세 번 다시 시도 합니다.

## <a name="http-request-headers"></a>HTTP 요청 헤더

속성                     | Description
------------------------ | -----------
X-NuGet-ApiKey           | 밀어넣기 및 삭제에 필요 합니다. [`PackagePublish` 리소스](package-publish-resource.md) 를 참조 하세요.
X-NuGet-Client-Version   | **사용 되지** 않으며 `X-NuGet-Protocol-Version`로 대체 됨
X-NuGet-Protocol-Version | Nuget.org의 특정 경우에만 필요 합니다. [nuget.org 프로토콜](NuGet-Protocols.md) 을 참조 하세요.
X-NuGet-Session-Id       | *선택 사항*. NuGet 클라이언트 v 4.7 +는 동일한 NuGet 클라이언트 세션의 일부인 HTTP 요청을 식별 합니다.

`X-NuGet-Session-Id`에는 `PackageReference`의 단일 복원과 관련 된 모든 작업에 대 한 단일 값이 있습니다. 자동 완성 및 `packages.config` 복원과 같은 다른 시나리오의 경우 코드를 팩터링 하는 방법으로 인해 여러 다른 세션 ID가 있을 수 있습니다.

## <a name="authentication"></a>인증

인증은 정의할 패키지 원본 구현에 남아 있습니다. Nuget.org의 경우에는 `PackagePublish` 리소스에만 특수 API 키 헤더를 통한 인증이 필요 합니다. 자세한 내용은 [`PackagePublish` 리소스](package-publish-resource.md) 를 참조 하세요.
