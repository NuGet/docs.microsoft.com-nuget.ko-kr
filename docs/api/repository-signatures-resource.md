---
title: 리포지토리 서명, NuGet API | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: 리포지토리 서명을 리소스 클라이언트 기능을 서명 하는 리포지토리의 기쁘게 패키지 소스를 수 있습니다.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: ea318446c41a0d85d3fbf959dd38c929a0d0e9a1
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2019
ms.locfileid: "59509024"
---
# <a name="repository-signatures"></a>리포지토리 서명

패키지 원본에서 게시 된 패키지에 추가 리포지토리 서명의 지 원하는 경우 패키지 원본에서 사용 되는 서명 인증서를 확인 하려면 클라이언트에 대 한 합니다. 이 리소스에 클라이언트를 패키지 변조 또는 예기치 않은 서명 인증서가 포함 된 리포지토리를 서명할지 여부를 검색할 수 있습니다.

이 리포지토리 서명 정보를 가져오는 중에 사용 되는 리소스를 `RepositorySignatures` 에서 리소스를 찾을 합니다 [서비스 인덱스](service-index.md)합니다.

## <a name="versioning"></a>버전 관리

다음 `@type` 값이 사용 됩니다.

@type 값                | 노트
-------------------------- | -----
RepositorySignatures/4.7.0 | 초기 릴리스
RepositorySignatures/4.9.0 | NuGet v4.9 + 클라이언트 지원
RepositorySignatures/5.0.0 | 사용 하도록 설정 하면 허용 `allRepositorySigned`합니다. NuGet v5.0 + 클라이언트 지원

## <a name="base-url"></a>기준 URL

다음 Api에 대 한 항목 지점 URL의 값인 합니다 `@id` 앞에서 언급 한 리소스와 연결 된 속성 `@type` 값입니다. 자리 표시자 URL을 사용 하 여이 항목에서는 `{@id}`합니다.

다른 리소스와 달리는 `{@id}` URL은 HTTPS를 통해 제공 해야 합니다.

## <a name="http-methods"></a>HTTP 메서드

리포지토리 서명 리소스 지원만 HTTP 메서드에서 발견 한 모든 Url `GET` 고 `HEAD`입니다.

## <a name="repository-signatures-index"></a>저장소 서명 인덱스

저장소 서명을 인덱스는 두 가지 정보를 포함합니다.

1. 이 패키지 원본에서 서명 하는 리포지토리는 여부를 모든 패키지에 원본입니다.
1. 패키지를 패키지 원본에서 사용 되는 인증서의 목록입니다.

대부분의 경우에서 인증서 목록에 추가 됩니다. 새 인증서 이전 서명 인증서가 만료 및 패키지 원본에서 새 서명 인증서를 사용 하 여 시작 해야 하는 경우 목록에 추가할 수는 있습니다. 경우는 인증서는 제거 서명 인증서를 사용 하 여 만든 모든 패키지 서명을 해야 더 이상 유효 하지 클라이언트에서 의미 하는 목록에서 제거 됩니다. 이 경우 패키지 서명을 (반드시 패키지) 올바르지 않습니다. 클라이언트 정책으로 서명 되지 않은 패키지를 설치 하 수 있습니다.

인증서 해지 (예: 키 손상)의 경우 패키지 소스는 영향을 받는 인증서로 서명 된 모든 패키지를 다시 서명 해야 합니다. 또한 패키지 원본을 서명 인증서 목록에서 영향을 받는 인증서를 제거 해야 합니다.

다음 요청은 리포지토리 서명을 인덱스를 페치합니다.

    GET {@id}

저장소 서명 인덱스는 다음 속성을 가진 개체를 포함 하는 JSON 문서:

이름                | 형식             | 필수 | 노트
------------------- | ---------------- | -------- | -----
allRepositorySigned | boolean          | 예      | 해야 `false` 4.7.0 및 4.9.0 리소스
signingCertificates | 개체의 배열 | 예      | 

`allRepositorySigned` 패키지 원본 리포지토리 서명이 있는 일부 패키지가 있으면 부울 false로 설정 됩니다. 원본에서 언급 한 서명 인증서 중 하나에서 생성 된 리포지토리 서명이 있어야 부울에서 사용 가능한 모든 패키지를 true로 설정 된 경우 `signingCertificates`합니다.

> [!Warning]
> `allRepositorySigned` 부울 4.7.0 및 4.9.0 리소스에 false 여야 합니다. NuGet v4.7, v4.8, 및 v4.9 클라이언트가 있는 원본에서 패키지를 설치할 수 없습니다 `allRepositorySigned` true로 설정 합니다.

서명 인증서를 하나 이상 있어야 합니다 `signingCertificates` 배열을 `allRepositorySigned` 부울 설정 되어 true로 합니다. 배열이 비어 있는 경우 및 `allRepositorySigned` 로 설정 된 true 이면 모든 패키지 소스에서 고려해 야 잘못 된 경우에 클라이언트 정책을 여전히 패키지의 사용을 허용 하지만 합니다. 이 배열의 각 요소에는 다음 속성을 사용 하 여 JSON 개체입니다.

이름         | 형식   | 필수 | 노트
------------ | ------ | -------- | -----
contentUrl   | string | 예      | DER로 인코딩된 공용 인증서에 절대 URL
지문 | object | 예      |
제목      | string | 예      | 인증서의 주체 고유 이름
issuer       | string | 예      | 인증서의 발급자의 고유 이름
notBefore    | string | 예      | 인증서의 유효 기간의 시작 타임 스탬프
notAfter     | string | 예      | 인증서의 유효 기간의 끝 타임 스탬프

`contentUrl` 는 HTTPS를 통해 제공 해야 합니다. 이 URL 없는 특정 URL 패턴과 있으며이 저장소 서명을 인덱스 문서를 사용 하 여 동적으로 검색 되어야 합니다. 

이 개체의 모든 속성 (보인다는 `contentUrl`)에 있는 인증서에서 결과 해야 `contentUrl`합니다.
이러한 결과 속성 왕복을 최소화 하기 위해 편의상 제공 됩니다.

`fingerprints` 개체에는 다음 속성이 있습니다.

이름                   | 형식   | 필수 | 노트
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | string | 예      | SHA-256 지문

키 이름 `2.16.840.1.101.3.4.2.1` 는 SHA-256 해시 알고리즘의 OID입니다.

모든 해시 값에는 해시 다이제스트의 소문자 16 진수로 인코딩된 문자열 표현 이어야 합니다.

### <a name="sample-request"></a>샘플 요청

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a>샘플 응답

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
