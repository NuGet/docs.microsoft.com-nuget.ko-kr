---
title: 서비스 인덱스를 NuGet API
description: NuGet HTTP API의 진입점의 서버 기능을 열거 하는 서비스 인덱스입니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1dcfb87690b728280b494d4434f9c1d7ee7a7e74
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324723"
---
# <a name="service-index"></a>서비스 인덱스

서비스 인덱스에는 NuGet 패키지 원본에 대 한 진입점이 고 패키지 원본의 기능을 검색 하기 위한 클라이언트 구현을 허용 하는 JSON 문서입니다. 서비스 인덱스는 두 개의 필수 속성만 사용 하 여 JSON 개체: `version` (서비스 인덱스의 스키마 버전) 및 `resources` (끝점 또는 패키지 원본의 기능).

nuget.org의 서비스 인덱스에 위치한 `https://api.nuget.org/v3/index.json`합니다.

## <a name="versioning"></a>버전 관리

`version` 값은 서비스 인덱스의 스키마 버전을 나타내는 SemVer 2.0.0 구문 분석할 버전 문자열입니다. API 버전 문자열의 주 버전 번호에 규정 `3`합니다. 줄 바꿈하지 않는 서비스 인덱스 스키마를 변경 되는 버전 문자열의 부 버전을 늘릴 수 있습니다.

서비스 인덱스의 각 리소스는 서비스 인덱스 스키마 버전에서 독립적으로 버전이 있습니다.

현재 스키마 버전은 `3.0.0`합니다. 합니다 `3.0.0` 버전은 기능적으로 이전 `3.0.0-beta.1` 버전 있지만 안정적이 고 정의 된 스키마를 보다 명확 하 게 통신 기본 설정 해야 합니다.

## <a name="http-methods"></a>HTTP 메서드

서비스 인덱스는 HTTP 메서드를 사용 하 여 액세스할 `GET` 고 `HEAD`입니다.

## <a name="resources"></a>자료

`resources` 속성에는이 패키지 원본에서 지 원하는 리소스의 배열을 포함 합니다.

### <a name="resource"></a>리소스

리소스는 개체는 `resources` 배열입니다. 패키지 원본 버전 관리 기능을 나타냅니다. 리소스에는 다음 속성이 있습니다.

이름          | 형식   | 필수 | 노트
------------- | ------ | -------- | -----
@id           | string | 예      | 리소스 URL
@type         | string | 예      | 리소스 종류를 나타내는 문자열 상수
주석       | string | 아니요       | 사람이 읽을 수 있는 설명은 리소스

`@id` 절대 이어야 하며 이어야 하는 URL에는 HTTP 또는 HTTPS 스키마가 됩니다.

`@type` 리소스와 상호 작용할 때 사용 하는 특정 프로토콜을 식별 하는 데 사용 됩니다. 리소스 형식의 불투명 문자열 이지만 형식은 일반적으로:

    {RESOURCE_NAME}/{RESOURCE_VERSION}

하드 코드 해야 클라이언트는 `@type` 이해 하 고 패키지 원본의 서비스 인덱스에서 조회는 값입니다. 정확한 `@type` 에 나열 된 개별 리소스 참조 문서에서 현재 사용 중인 값 열거 되는 [API 개요](overview.md#resources-and-schema)합니다.

이 설명서를 위해 다양 한 리소스에 대 한 설명서는 기본적으로 별로 그룹화 할 수는 `{RESOURCE_NAME}` 그룹화 시나리오에 따라 유사한 서비스 인덱스 검색. 

각 리소스에는 고유한 요구 사항이 없을 `@id` 또는 `@type`합니다. 클라이언트 구현 리소스를 다른 것을 선호할 결정 됩니다. 한 가지 구현은 동일 하거나 호환 가능한 리소스 `@type` 연결 오류 또는 서버 오류 발생 시 라운드 로빈 방식으로 사용할 수 있습니다.

### <a name="sample-request"></a>샘플 요청

    GET https://api.nuget.org/v3/index.json

### <a name="sample-response"></a>샘플 응답

[!code-JSON [service-index.json](./_data/service-index.json)]
