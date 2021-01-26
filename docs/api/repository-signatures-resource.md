---
title: 리포지토리 서명, NuGet API | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: 리포지토리 서명 리소스를 사용 하면 클라이언트 패키지 원본에서 리포지토리 서명 기능을 알릴 수 있습니다.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775332"
---
# <a name="repository-signatures"></a>리포지토리 서명

패키지 원본에서 게시 된 패키지에 리포지토리 서명 추가를 지 원하는 경우 클라이언트는 패키지 원본에서 사용 하는 서명 인증서를 확인할 수 있습니다. 이 리소스를 통해 클라이언트는 리포지토리의 서명 된 패키지가 변조 되었거나 예기치 않은 서명 인증서가 있는지 여부를 검색할 수 있습니다.

이 리포지토리 서명 정보를 인출 하는 데 사용 되는 리소스는 `RepositorySignatures` [서비스 인덱스](service-index.md)에 있는 리소스입니다.

## <a name="versioning"></a>버전 관리

사용 되는 `@type` 값은 다음과 같습니다.

@type 값                | 메모
-------------------------- | -----
RepositorySignatures/4.7.0 | 초기 릴리스
RepositorySignatures/4.9.0 | NuGet v 4.9 + 클라이언트에서 지원
RepositorySignatures/5.0.0 | 사용 `allRepositorySigned` 을 허용 합니다. NuGet v 5.0 이상 클라이언트에서 지원 됨

## <a name="base-url"></a>기준 URL

다음 Api에 대 한 진입점 URL은 `@id` 앞서 언급 한 리소스 값과 연결 된 속성의 값입니다 `@type` . 이 항목에서는 자리 표시자 URL을 사용 `{@id}` 합니다.

다른 리소스와 달리 `{@id}` URL은 HTTPS를 통해 제공 해야 합니다.

## <a name="http-methods"></a>HTTP 메서드

리포지토리 서명 리소스에서 찾은 모든 Url은 HTTP 메서드 및만 지원 `GET` 합니다 `HEAD` .

## <a name="repository-signatures-index"></a>리포지토리 서명 인덱스

리포지토리 서명 인덱스에는 다음과 같은 두 가지 정보가 포함 됩니다.

1. 원본에 있는 모든 패키지가이 패키지 소스에서 서명한 리포지토리입니다 여부입니다.
1. 패키지에 서명 하기 위해 패키지 원본에서 사용 하는 인증서 목록입니다.

대부분의 경우 인증서 목록은에만 추가 됩니다. 이전 서명 인증서가 만료 되 고 패키지 원본이 새 서명 인증서를 사용 하 여 시작 해야 하는 경우 새 인증서가 목록에 추가 됩니다. 인증서가 목록에서 제거 되 면 제거 된 서명 인증서를 사용 하 여 만든 모든 패키지 서명이 더 이상 클라이언트에서 유효한 것으로 간주 되지 않습니다. 이 경우 패키지 서명 (반드시 패키지는 아님)이 유효 하지 않습니다. 클라이언트 정책을 사용 하면 패키지를 unsigned로 설치할 수 있습니다.

인증서 해지 (예: 키 손상)의 경우 패키지 원본에서 영향을 받는 인증서로 서명 된 모든 패키지를 다시 서명 해야 합니다. 또한 패키지 원본은 서명 인증서 목록에서 영향을 받는 인증서를 제거 해야 합니다.

다음 요청은 리포지토리 서명 인덱스를 인출 합니다.

```
GET {@id}
```

리포지토리 서명 인덱스는 다음 속성을 포함 하는 개체를 포함 하는 JSON 문서입니다.

Name                | Type             | 필수 | 메모
------------------- | ---------------- | -------- | -----
allRepositorySigned | boolean          | 예      | `false`4.7.0 및 4.9.0 리소스에 있어야 합니다.
signingCertificates | 개체의 배열 | 예      | 

`allRepositorySigned`패키지 원본에 리포지토리 서명이 없는 일부 패키지가 있는 경우 부울이 false로 설정 됩니다. 부울이 true로 설정 된 경우 원본에서 사용할 수 있는 모든 패키지에는에 설명 된 서명 인증서 중 하나에서 생성 한 리포지토리 서명이 있어야 합니다 `signingCertificates` .

> [!Warning]
> `allRepositorySigned`부울은 4.7.0 및 4.9.0 리소스에 대해 false 여야 합니다. NuGet v 4.7, v 4.8 및 v 4.9 클라이언트는가 true로 설정 된 원본에서 패키지를 설치할 수 없습니다 `allRepositorySigned` .

`signingCertificates` `allRepositorySigned` 부울이 true로 설정 된 경우 배열에 하나 이상의 서명 인증서가 있어야 합니다. 배열이 비어 있고 `allRepositorySigned` 이 true로 설정 된 경우에도 클라이언트 정책에서 패키지 사용을 허용할 수 있지만 원본의 모든 패키지는 유효 하지 않은 것으로 간주 됩니다. 이 배열의 각 요소는 다음 속성을 포함 하는 JSON 개체입니다.

Name         | Type   | 필수 | 메모
------------ | ------ | -------- | -----
contentUrl   | 문자열 | 예      | DER로 인코딩된 공용 인증서의 절대 URL
지문 | 개체 | 예      |
subject      | 문자열 | 예      | 인증서의 주체 고유 이름
발급자       | 문자열 | 예      | 인증서 발급자의 고유 이름입니다.
notBefore    | 문자열 | 예      | 인증서 유효 기간의 시작 타임 스탬프입니다.
notAfter     | 문자열 | 예      | 인증서 유효 기간의 끝 타임 스탬프입니다.

는 HTTPS를 `contentUrl` 통해 제공 해야 합니다. 이 URL에는 특정 URL 패턴이 없으며이 리포지토리 서명 인덱스 문서를 사용 하 여 동적으로 검색 해야 합니다. 

이 개체의 모든 속성 (제외 `contentUrl` )은에 있는 인증서에서 파생 가능한 해야 합니다 `contentUrl` .
이러한 파생 가능한 속성은 라운드트립을 최소화 하기 위해 편리 하 게 제공 됩니다.

`fingerprints` 개체의 속성은 다음과 같습니다.

Name                   | Type   | 필수 | 메모
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | 문자열 | 예      | SHA-256 지문

키 이름은 `2.16.840.1.101.3.4.2.1` SHA-256 해시 알고리즘의 OID입니다.

모든 해시 값은 해시 다이제스트의 소문자, 16 진수로 인코딩된 문자열 표현 이어야 합니다.

### <a name="sample-request"></a>샘플 요청

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a>샘플 응답

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
