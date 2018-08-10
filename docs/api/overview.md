---
title: NuGet API 개요
description: NuGet API는 패키지를 다운로드, 메타 데이터를 가져오는 등 새 패키지를 게시 하는 HTTP 끝점의 집합.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fe843a121e2f1aae376f3e30a7b911792057688f
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020533"
---
# <a name="nuget-api"></a>NuGet API

NuGet API는 패키지를 다운로드, 메타 데이터 인출, 새 패키지를 게시 및 공식 NuGet 클라이언트에서 사용할 수 있는 다른 대부분의 작업을 수행 하는 HTTP 끝점의 집합.

이 API는 데.NET CLI, nuget.exe를 Visual Studio에서 NuGet 클라이언트에서와 같이 NuGet 작업을 수행 [ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore), Visual Studio ui에서 검색 하 고 [ `nuget.exe push` ](../tools/cli-ref-push.md)합니다.

Nuget.org에는 추가 요구 사항이 다른 패키지 소스에 의해 적용 되지 않은 경우에 따라 note 합니다. 이러한 차이 문서화 합니다 [nuget.org 프로토콜](nuget-protocols.md)합니다.

## <a name="service-index"></a>서비스 인덱스

API에 대 한 진입점에는 잘 알려진 위치에 JSON 문서입니다. 이 문서 라고 합니다 **서비스 인덱스**합니다. Nuget.org에 대 한 서비스 인덱스 위치가 `https://api.nuget.org/v3/index.json`합니다.

이 JSON 문서 목록이 *리소스* 다양 한 기능을 제공 하며 다양 한 사용 사례를 충족 합니다.

API를 지 원하는 클라이언트는 해당 패키지 원본에 연결 하는 수단으로 이러한 서비스 인덱스 URL 중 하나 이상을 수락 해야 합니다.

서비스 인덱스에 대 한 자세한 내용은 참조 하세요. [해당 API 참조](service-index.md)합니다.

## <a name="versioning"></a>버전 관리

API에는 NuGet의 HTTP 프로토콜의 버전 3입니다. 이 프로토콜은 경우에 따라 "V3 API입니다." 라고 이러한 참조 문서는이 버전의 프로토콜 "API입니다."으로 단순히 참조

서비스 인덱스 스키마 버전으로 표시 됩니다는 `version` 서비스 인덱스의 속성입니다. API 버전 문자열의 주 버전 번호에 규정 `3`합니다. 줄 바꿈하지 않는 서비스 인덱스 스키마를 변경 되는 버전 문자열의 부 버전을 늘릴 수 있습니다.

이전 버전의 클라이언트 (nuget.exe 같은 2.x) V3 API를 지원 하지 않으며 여기서는 설명 하지는 이전 V2 API를 지원 합니다.

NuGet V3 API V2 API의 후속 작업을 설정 하는 공식 NuGet 클라이언트의 2.x 버전에서 구현 하는 OData 기반 프로토콜 된이 있기 때문에 같이 명명 됩니다. V3 API를 처음 3.0 공식 NuGet 클라이언트 버전에서 지원 되었습니다 및 여전히 주요 프로토콜 최신 버전에서 지원 됩니다 4.0 NuGet 클라이언트에 있습니다. 

주요 변경 아님 프로토콜 변경한 API에 첫 번째 릴리스 이후입니다.

## <a name="resources-and-schema"></a>리소스 및 스키마

합니다 **서비스 인덱스** 다양 한 리소스에 설명 합니다. 지원 되는 리소스의 현재 집합은 다음과 같습니다.

리소스 이름                                                          | 필수 | 설명
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | 예      | 푸시 및 삭제 (또는 나열 취소) 패키지 있습니다.
[`SearchQueryService`](search-query-service-resource.md)               | 예      | 필터 및 키워드는 패키지에 대 한 검색 합니다.
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | 예      | 패키지 메타 데이터를 가져옵니다.
[`PackageBaseAddress`](package-base-address-resource.md)               | 예      | 패키지 콘텐츠를 (.nupkg)를 가져옵니다.
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | 아니요       | 부분 문자열에서 패키지 Id 및 버전을 검색 합니다.
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | 아니요       | "신고" 웹 페이지 액세스에 대 한 URL을 생성 합니다.
[`RepositorySignatures`](repository-signatures-resource.md)            | 아니요       | 리포지토리 서명에 사용 되는 인증서를 가져옵니다.
[`Catalog`](catalog-resource.md)                                       | 아니요       | 모든 패키지 이벤트의 전체 레코드입니다.

일반적으로 API 리소스에 의해 반환 되는 모든 이진이 아닌 데이터는 JSON을 사용 하 여 serialize 됩니다. 서비스 인덱스의 각 리소스에서 반환 되는 응답 스키마는 해당 리소스에 대해 개별적으로 정의 됩니다. 각 리소스에 대 한 자세한 내용은 위에 나열 된 항목을 참조 하세요.

> [!Note]
> 원본 구현 하지 않는 경우 `SearchAutocompleteService` 모든 자동 완성 동작을 정상적으로 해제 합니다. 때 `ReportAbuseUriTemplate` 구현 되지 않은 공식 NuGet 클라이언트 대체 되므로 nuget.org의 보고 악성 URL 신고 (에서 추적 [NuGet/Home #4924](https://github.com/NuGet/Home/issues/4924)). 다른 클라이언트는 악성 URL 신고 사용자에 게 표시 하지 않으려면에 간단히 선택할 수 있습니다.

## <a name="timestamps"></a>타임스탬프

API에서 반환 하는 모든 타임 스탬프는 UTC 또는 사용 하 여 지정 된 [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 표현 합니다. 

## <a name="http-methods"></a>HTTP 메서드

동사   | 사용
------ | -----------
가져오기    | 일반적으로 데이터를 검색 하는 읽기 전용 작업을 수행 합니다.
HEAD   | 해당 하는 것에 대 한 응답 헤더를 인출 `GET` 요청 합니다.
PUT    | 존재 하지 않거나 없으면, 업데이트 하는 리소스를 만듭니다. 일부 리소스는 업데이트를 지원 하지 않습니다.
Delete | 삭제 하거나 리소스 목록에서 제거 합니다.

## <a name="http-status-codes"></a>HTTP 상태 코드

코드 | 설명
---- | -----
200  | 성공 하면 응답 본문이 있네요.
201  | 성공 및 리소스를 만들었습니다.
202  | 성공 하면 요청을 받았음을 몇 가지 작업이 있습니다 수 있지만 불완전 하 고 완료 된 비동기적으로.
204  | 성공 하면 응답 본문 없이 이지만 합니다.
301  | 영구 리디렉션입니다.
302  | 임시 리디렉션입니다.
400  | URL 이나 요청 본문에 매개 변수는 유효 하지 않습니다.
401  | 제공 된 자격 증명이 올바르지 않습니다.
403  | 작업을 제공된 된 자격 증명을 지정 하는 것을 허용 되지 않습니다.
404  | 요청한 리소스가 존재 하지 않습니다.
409  | 기존 리소스를 사용 하 여 요청 충돌 합니다.
500  | 서비스에서 예기치 않은 오류가 발생 합니다.
503  | 서비스가 일시적으로 사용할 수 없습니다.

모든 `GET` API 끝점에 대 한 요청에서 HTTP 리디렉션을 (301 또는 302)를 반환할 수 있습니다. 클라이언트를 관찰 하 여 이러한 리디렉션 정상적으로 처리 해야 합니다 `Location` 헤더 및 후속 발급 `GET`합니다. 특정 끝점에 관한 문서가 리디렉션을 사용할 수 있는 아웃 명시적으로 호출 하지 않습니다.

500 수준 상태 코드의 경우 클라이언트는 적절 한 재시도 메커니즘을 구현할 수 있습니다. 공식 NuGet 클라이언트 재시도 500 수준 상태 코드 또는 TCP/DNS 오류가 발생 하는 경우 3 번입니다.

## <a name="http-request-headers"></a>HTTP 요청 헤더

name                     | 설명
------------------------ | -----------
X-NuGet-ApiKey           | 푸시 및 삭제에 대 한 필요한 참조 [ `PackagePublish` 리소스](package-publish-resource.md)
X-NuGet-Client-Version   | **사용 되지 않는** 바뀝니다 `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | Nuget.org에 대해서만 특정 경우에 필요한 참조 [nuget.org 프로토콜](NuGet-Protocols.md)
X-NuGet-Session-Id       | *선택적*합니다. NuGet 클라이언트 v4.7 + 동일한 NuGet 클라이언트 세션의 일부인 HTTP 요청을 식별 합니다. 에 대 한 `PackageReference` 복원 작업 있습니다가 단일 세션 id가, 자동 완성와 같은 다른 시나리오에 대 한 및 `packages.config` 복원 여러 다른 세션 id의 코드는 포함 하는 방법으로 인해 있을 수 있습니다.

## <a name="authentication"></a>인증

인증 정의 하는 패키지 원본 구현을까지 그대로 유지 됩니다. Nuget.org의 경우만 `PackagePublish` 리소스는 특별 한 API 키 헤더를 통해 인증이 필요 합니다. 참조 [ `PackagePublish` 리소스](package-publish-resource.md) 세부 정보에 대 한 합니다.
