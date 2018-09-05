---
title: 푸시 및 삭제, NuGet API
description: 게시 서비스에는 클라이언트가 새 패키지를 게시 및 나열을 취소 하거나 기존 패키지를 삭제할 수 있습니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: ad66d8e0ffda13aaef744104c213863b0e111e0e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547523"
---
# <a name="push-and-delete"></a>푸시 및 삭제

푸시, 삭제 (또는 서버 구현에 따라 나열 취소) 수 및 NuGet V3 API를 사용 하 여 패키지를 다시 나열 합니다. 이러한 작업은 기반을 둔 합니다 `PackagePublish` 에서 리소스를 찾을 합니다 [서비스 인덱스](service-index.md)합니다.

## <a name="versioning"></a>버전 관리

다음 `@type` 값이 사용 됩니다.

@type 값          | 노트
-------------------- | -----
PackagePublish/2.0.0 | 초기 릴리스

## <a name="base-url"></a>기준 URL

다음 Api에 대 한 기본 URL의 값은를 `@id` 의 속성을 `PackagePublish/2.0.0` 패키지 원본에 대 한 리소스 [서비스 인덱스](service-index.md). 아래 설명서 nuget.org의 URL은 사용 합니다. 것이 좋습니다 `https://www.nuget.org/api/v2/package` 자리 표시자로는 `@id` 서비스 인덱스에서 찾을 값입니다.

동일한 프로토콜은이 URL의 레거시 V2 푸시 끝점으로 동일한 위치를 가리키는지 note 합니다.

## <a name="http-methods"></a>HTTP 메서드

합니다 `PUT`, `POST` 및 `DELETE` HTTP 메서드는이 리소스에 의해 지원 됩니다. 각 끝점에 어떤 방법이 지원, 아래 참조 하세요.

## <a name="push-a-package"></a>패키지 푸시

> [!Note]
> nuget.org에 [추가 요구 사항](NuGet-Protocols.md) 푸시 끝점과 상호 작용 합니다.

nuget.org는 다음 API를 사용 하 여 푸시 새 패키지를 지원 합니다. 제공 된 ID와 버전을 사용 하 여 패키지에 이미 있으면 nuget.org에서 푸시를 거부 합니다. 다른 패키지 원본이 기존 패키지를 대체 지원할 수 있습니다.

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a>요청 매개 변수

이름           | 입력     | 형식   | 필수 | 노트
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | 헤더 | string | 예      | 예를 들면 `X-NuGet-ApiKey: {USER_API_KEY}`과 같습니다.

API 키는 사용자가 패키지 원본에서 받은 및 클라이언트를 구성 하는 불투명 문자열입니다. 특정 문자열 서식 없음은 위임 하지만 API 키의 길이 HTTP 헤더 값에 대 한 적절 한 크기를 초과할 수 없습니다.

### <a name="request-body"></a>요청 본문

요청 본문에 다음 형식 이어야 합니다.

#### <a name="multipart-form-data"></a>다중 파트 양식 데이터

요청 헤더 `Content-Type` 는 `multipart/form-data` 및 요청 본문의 첫째 항목 푸시되.nupkg의 원시 바이트입니다. 다중 파트 본문의 후속 항목은 무시 됩니다. 파일 이름 또는 다중 항목의 다른 모든 헤더는 무시 됩니다.

### <a name="response"></a>응답

상태 코드 | 의미
----------- | -------
201, 202    | 패키지를 푸시 했습니다.
400         | 제공 된 패키지가 잘못 되었습니다.
409         | 제공 된 ID와 버전을 사용 하 여 패키지를 이미 있습니다.

패키지를 성공적으로 푸시 될 때 반환 된 성공 상태 코드에 서버 구현이 달라 집니다.

## <a name="delete-a-package"></a>패키지 삭제

nuget.org에서 패키지 삭제 요청으로 해석 "나열" 발생 합니다. 즉, 패키지는 패키지의 기존 소비자에 대 한 계속 사용할 수 있지만 패키지 또는 웹 인터페이스에서 검색 결과에서 더 이상 표시 합니다. 이 연습에 대 한 자세한 내용은 참조는 [패키지 삭제](../policies/deleting-packages.md) 정책입니다. 다른 서버 구현은 하드 삭제이 신호를 해석 하거나 일시 삭제 하거나 나열을 취소 하는 무료입니다. 예를 들어 [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (만 이전 V2 API를 지 원하는 서버 구현)이이 요청을 처리 하는 나열 취소 또는 구성 옵션에 따라 하드 삭제를 지원 합니다.

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>요청 매개 변수

이름           | 입력     | 형식   | 필수 | 노트
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | 예      | 삭제할 패키지의 ID
VERSION        | URL    | string | 예      | 삭제할 패키지의 버전
X-NuGet-ApiKey | 헤더 | string | 예      | 예를 들면 `X-NuGet-ApiKey: {USER_API_KEY}`과 같습니다.

### <a name="response"></a>응답

상태 코드 | 의미
----------- | -------
204         | 패키지 삭제
404         | 제공 된 패키지가 없는 `ID` 고 `VERSION` 존재

## <a name="relist-a-package"></a>패키지를 다시 나열

패키지 나열 되어 있지 않으면 경우 해당 패키지를 다시 한 번 "버전 다시 나열" 끝점을 사용 하 여 검색 결과에 표시 되도록 합니다. 이 끝점으로 동일한 셰이프가 [삭제 (나열) 끝점](#delete-a-package) 같지만 합니다 `POST` 대신 HTTP 메서드를 `DELETE` 메서드.

패키지가 이미 나열 되 고, 요청은 성공 합니다.

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>요청 매개 변수

이름           | 입력     | 형식   | 필수 | 노트
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | 예      | 패키지의 ID를 다시 나열
VERSION        | URL    | string | 예      | 다시 나열 하는 패키지의 버전
X-NuGet-ApiKey | 헤더 | string | 예      | 예를 들면 `X-NuGet-ApiKey: {USER_API_KEY}`과 같습니다.

### <a name="response"></a>응답

상태 코드 | 의미
----------- | -------
200         | 패키지는 이제 나열 되어 있습니다.
404         | 제공 된 패키지가 없는 `ID` 고 `VERSION` 존재
