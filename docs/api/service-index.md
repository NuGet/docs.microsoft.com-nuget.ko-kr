---
title: 서비스 인덱스, NuGet API
description: 서비스 인덱스는 NuGet HTTP API의 진입점 이며 서버의 기능을 열거 합니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775358"
---
# <a name="service-index"></a>인덱스 제공

서비스 인덱스는 NuGet 패키지 소스에 대 한 진입점인 JSON 문서로, 클라이언트 구현에서 패키지 소스의 기능을 검색할 수 있도록 합니다. 서비스 인덱스는 두 개의 필수 속성 `version` (서비스 인덱스의 스키마 버전) 및 `resources`  (패키지 원본의 끝점 또는 기능)을 포함 하는 JSON 개체입니다.

nuget. org의 서비스 인덱스는에 있습니다 `https://api.nuget.org/v3/index.json` .

## <a name="versioning"></a>버전 관리

`version`값은 서비스 인덱스의 스키마 버전을 나타내는 SemVer 2.0.0 구문 분석할 version 문자열입니다. API는 버전 문자열의 주 버전 번호를 요구 `3` 합니다. 서비스 인덱스 스키마에 대 한 주요 변경 내용이 적용 되지 않으므로 버전 문자열의 부 버전이 증가 합니다.

서비스 인덱스의 각 리소스는 서비스 인덱스 스키마 버전과 독립적으로 버전이 지정 됩니다.

현재 스키마 버전은 `3.0.0` 입니다. `3.0.0`버전은 이전 버전과 기능적으로 동일 `3.0.0-beta.1` 하지만, 안정적이 고 정의 된 스키마를 보다 명확 하 게 전달 하므로 선호 해야 합니다.

## <a name="http-methods"></a>HTTP 메서드

서비스 인덱스는 HTTP 메서드 및를 사용 하 여 액세스할 수 `GET` `HEAD` 있습니다.

## <a name="resources"></a>리소스

속성에는 `resources` 이 패키지 소스에서 지 원하는 리소스 배열이 포함 되어 있습니다.

### <a name="resource"></a>리소스

리소스는 배열의 개체입니다 `resources` . 패키지 소스의 버전이 지정 된 기능을 나타냅니다. 리소스에는 다음과 같은 속성이 있습니다.

Name          | Type   | 필수 | 메모
------------- | ------ | -------- | -----
@id           | 문자열 | 예      | 리소스에 대 한 URL입니다.
@type         | 문자열 | 예      | 리소스 형식을 나타내는 문자열 상수입니다.
주석       | 문자열 | 아니요       | 사람이 읽을 수 있는 리소스에 대 한 설명입니다.

는 `@id` 절대 URL 이어야 하며 HTTP 또는 HTTPS 스키마가 있어야 합니다.

는 `@type` 리소스와 상호 작용할 때 사용할 특정 프로토콜을 식별 하는 데 사용 됩니다. 리소스의 형식은 불투명 문자열 이지만 일반적으로 형식은 다음과 같습니다.

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

클라이언트는 `@type` 이해 하는 값을 하드 코딩 하 고 패키지 소스의 서비스 인덱스에서 조회 합니다. `@type`현재 사용 중인 정확한 값은 [API 개요](overview.md#resources-and-schema)에 나열 된 개별 리소스 참조 문서에 열거 됩니다.

이 설명서의 편의를 위해 다른 리소스에 대 한 설명서는 기본적으로 서비스 인덱스에 있는로 그룹화 되며,이는 `{RESOURCE_NAME}` 시나리오 별로 그룹화 하는 것과 유사 합니다. 

각 리소스에는 고유한 또는가 있어야 `@id` `@type` 합니다. 다른 리소스를 선호 하는 리소스를 결정 하는 것은 클라이언트 구현에 따라 결정 됩니다. 한 가지 가능한 구현은 `@type` 연결 실패 또는 서버 오류 발생 시 라운드 로빈 방식으로 같거나 호환 되는 리소스를 사용할 수 있다는 것입니다.

### <a name="sample-request"></a>샘플 요청

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a>샘플 응답

[!code-JSON [service-index.json](./_data/service-index.json)]
