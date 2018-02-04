---
title: "개요, NuGet API | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "NuGet API는 패키지를 다운로드, 메타 데이터 인출, 새로운 패키지 등 게시를 사용할 수 있는 HTTP 끝점의 집합입니다."
keywords: "NuGet V3 API, NuGet V2 API, NuGet JSON, NuGet 등록 API를 NuGet API 플랫 컨테이너, NuGet nupkg API, NuGet 메타 데이터 API, NuGet 검색 API, NuGet 푸시 API NuGe API를 게시, NuGet API를 삭제, NuGet unlist API, NuGet 프로토콜"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c28b0912be6dbccab06078100cb71821c3658e08
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-api"></a>NuGet API

NuGet API는 패키지를 다운로드, 메타 데이터 인출, 새로운 패키지를 게시 및 공식 NuGet 클라이언트에서 사용할 수 있는 다른 대부분 작업을 수행 하는 데 사용할 수 있는 HTTP 끝점의 집합입니다.

이 API는 데 Visual Studio, nuget.exe,.NET CLI에는 NuGet 클라이언트와 같은 NuGet 작업을 수행 [ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore), Visual Studio UI에서 검색 하 고 [ `nuget.exe push` ](../tools/cli-ref-push.md)합니다.

Nuget.org의 다른 패키지 소스에 적용 되지 않은 다른 요구 사항이 있을 경우에 따라 note 합니다. 이러한 차이 단계의 유형별로 설명 되어는 [nuget.org 프로토콜](nuget-protocols.md)합니다.

## <a name="service-index"></a>서비스 인덱스

API에 대 한 진입점에는 잘 알려진 위치에 JSON 문서입니다. 이 문서는 라고는 **서비스 인덱스**합니다.
Nuget.org에 대 한 서비스 인덱스의 위치는 `https://api.nuget.org/v3/index.json`합니다.

이 JSON 문서 목록이 포함 되어 *리소스* 다른 기능을 제공 하 고 다른 사용 사례를 수행 합니다.

API를 지 원하는 클라이언트는 해당 패키지 소스에 연결 하는 수단으로 이러한 서비스 인덱스 URL 중 하나 이상을 사용 해야 합니다.

서비스 인덱스에 대 한 자세한 내용은 참조 [해당 API 참조](service-index.md)합니다.

## <a name="versioning"></a>버전 관리

API에는 NuGet의 HTTP 프로토콜의 버전 3입니다. 이 프로토콜 때때로 이라고 "V3 API입니다." 이러한 참조 문서에서는 "API입니다." 처럼 간단 하 게이 버전의 프로토콜을 나타냅니다.

서비스 인덱스 스키마 버전으로 표시 됩니다는 `version` 서비스 인덱스에서 속성입니다. API 버전 문자열의 주 버전 번호에 보내도록 규정 `3`합니다. 서비스 인덱스 스키마에 사소한 변경, 버전 문자열의 부 버전을 늘릴 수 있습니다.

이전 버전의 클라이언트 (nuget.exe 같은 2.x) V3 API를 지원 하지 않으며 여기에 문서화 되지 않은 이전 V2 API를 지원 합니다.

NuGet V3 API V2 API의 후속 작업을 설정 하는 공식 NuGet 클라이언트 2.x 버전에서 구현 하는 OData 기반 프로토콜을 임이 있기 때문에 따라서 라고 합니다. V3 API 공식 NuGet 클라이언트 버전 3.0에서 처음 지원 되었습니다 및 여전히 주요 프로토콜 최신 버전에서 지원 됩니다 4.0 NuGet 클라이언트에 있습니다. 

주요 변경 아님 프로토콜 변경이 이루어진 API에 첫 번째 릴리스 이후입니다.

## <a name="resources-and-schema"></a>리소스 및 스키마

**서비스 인덱스** 다양 한 리소스에 설명 합니다. 지원 되는 리소스의 현재 집합은 다음과 같습니다.

리소스 이름                                                          | 필수 | 설명
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | 예      | 푸시 및 삭제 (또는 unlist) 패키지 합니다.
[`SearchQueryService`](search-query-service-resource.md)               | 예      | 필터 및 키워드로 패키지에 대 한 검색 합니다.
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | 예      | 패키지 메타 데이터를 가져옵니다.
[`PackageBaseAddress`](package-base-address-resource.md)               | 예      | 패키지 콘텐츠를 (.nupkg)를 가져옵니다.
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | 아니요       | 부분 문자열이 패키지 Id 및 버전을 검색 합니다.
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | 아니요       | "신고" 웹 페이지에 액세스 하는 URL을 구성 합니다.
[`Catalog`](catalog-resource.md)                                       | 아니요       | 모든 패키지 이벤트의 전체 레코드입니다.

일반적으로 API 리소스에 의해 반환 되는 모든 이진이 아닌 데이터는 JSON을 사용 하 여 serialize 됩니다. 서비스 인덱스의 각 리소스에서 반환 된 응답 스키마는 해당 리소스에 대해 개별적으로 정의 됩니다. 각 리소스에 대 한 자세한 내용은 위에 나열 된 항목을 참조 하십시오.

> [!Note]
> 원본 구현 하지 않는 `SearchAutocompleteService` 모든 자동 완성 동작을 적절 하 게 해제 되어야 합니다. 때 `ReportAbuseUriTemplate` 구현 되지 않은 nuget.org의로 공식 NuGet 클라이언트 변경 보고서 남용 URL (에서 추적 [NuGet/홈 #4924](https://github.com/NuGet/Home/issues/4924)). 다른 클라이언트를 보고서 남용 URL을 사용자에 게 표시 되지 않도록에 간단히 선택할 수 있습니다.

## <a name="timestamps"></a>타임스탬프

API에서 반환 하는 모든 타임 스탬프는 UTC 또는 사용 하 여 별도로 지정 [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 표현 합니다. 

## <a name="http-methods"></a>HTTP 메서드

동사   | 사용
------ | -----------
가져오기    | 일반적으로 데이터를 검색 하는 읽기 전용 작업을 수행 합니다.
HEAD   | 응답 헤더에는 해당 인출 `GET` 요청 합니다.
PUT    | 존재 하지 않거나 파일이 존재 하는 경우 업데이트 하는 리소스를 만듭니다. 일부 리소스는 업데이트를 지원 하지 않을 수 있습니다.
Delete | 삭제 하거나 리소스 unlists 합니다.

## <a name="http-status-codes"></a>HTTP 상태 코드

코드 | 설명
---- | -----
200  | 성공할 경우 응답 본문은 및입니다.
201  | 성공 및 리소스를 만들었습니다.
202  | 성공, 요청이 승인 된 되지만 몇 가지 작업 수 불완전 한 시간 및 완료 된 비동기적으로.
204  | 성공 하지만 응답 본문이 없습니다.
301  | 영구 리디렉션입니다.
302  | 임시 리디렉션입니다.
400  | 매개 변수는 URL에 또는 요청 본문에서 유효 하지 않습니다.
401  | 제공 된 자격 증명이 올바르지 않습니다.
403  | 작업이 제공 된 자격 증명이 제공 하는 것을 허용 되지 않습니다.
404  | 요청 된 리소스는 존재 하지 않습니다.
409  | 기존 리소스와 함께 요청 충돌 합니다.
500  | 서비스에 예기치 않은 오류가 발생 했습니다.
503  | 서비스를 일시적으로 사용할 수 없습니다.

모든 `GET` API 끝점에 대 한 요청에 HTTP 리디렉션을 (301 또는 302) 반환할 수 있습니다. 관찰 하 여 클라이언트가 이러한 리디렉션을 적절히 처리 해야는 `Location` 헤더 및 후속 내림 `GET`합니다. 특정 끝점에 관한 설명서 리디렉션을 사용할 수 있습니다. 아웃 명시적으로 호출 하지 않습니다.

500 수준 상태 코드의 경우 클라이언트는 적절 한 재시도 메커니즘을 구현 수 있습니다. 공식 NuGet 클라이언트 다시 시도가 3 번 500 수준 상태 코드 또는 TCP/DNS 오류를 발견할 때.

## <a name="http-request-headers"></a>HTTP 요청 헤더

name                     | 설명
------------------------ | -----------
X-NuGet-ApiKey           | 필수 푸시 및 삭제를 참조 하십시오 [ `PackagePublish` 리소스](package-publish-resource.md)
X-NuGet-Client-Version   | **사용 되지 않는** 대체`X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | Nuget.org에 대해서만 특정 경우에 필요한 참조 [nuget.org 프로토콜](NuGet-Protocols.md)

## <a name="authentication"></a>인증

인증을 정의 하는 패키지 원본 구현을 몫입니다. 만 nuget.org에 대 한는 `PackagePublish` 리소스는 특별 한 API 키 헤더를 통해 인증이 필요 합니다. 참조 [ `PackagePublish` 리소스](package-publish-resource.md) 대 한 자세한 내용은 합니다.
