---
title: 밀어넣기 및 삭제, NuGet API
description: 게시 서비스를 사용 하면 클라이언트가 새 패키지를 게시 하 고 기존 패키지를 목록에서 삭제 하거나 삭제할 수 있습니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773924"
---
# <a name="push-and-delete"></a>밀어넣기 및 삭제

서버 구현에 따라 푸시, 삭제 또는 나열을 취소할 수 있으며 NuGet V3 API를 사용 하 여 패키지를 다시 나열할 수 있습니다. 이러한 작업은 `PackagePublish` [서비스 인덱스](service-index.md)에 있는 리소스를 기반으로 합니다.

## <a name="versioning"></a>버전 관리

사용 되는 `@type` 값은 다음과 같습니다.

@type 값          | 메모
-------------------- | -----
PackagePublish/2.0.0 | 초기 릴리스

## <a name="base-url"></a>기준 URL

다음 Api에 대 한 기준 URL은 `@id` `PackagePublish/2.0.0` 패키지 소스의 [서비스 인덱스](service-index.md)에 있는 리소스의 속성 값입니다. 아래 설명서의 경우에는 nuget.exe의 URL이 사용 됩니다. `https://www.nuget.org/api/v2/package`서비스 인덱스에 있는 값에 대 한 자리 표시자로 간주 `@id` 합니다.

이 URL은 프로토콜이 동일 하기 때문에 레거시 V2 push 끝점과 동일한 위치를 가리킵니다.

## <a name="http-methods"></a>HTTP 메서드

`PUT`, `POST` 및 `DELETE` HTTP 메서드는이 리소스에서 지원 됩니다. 각 끝점에서 지원 되는 메서드는 아래를 참조 하세요.

## <a name="push-a-package"></a>패키지 푸시

> [!Note]
> nuget.org에는 푸시 끝점과 상호 작용 하기 위한 [추가 요구 사항이](NuGet-Protocols.md) 있습니다.

nuget.org은 다음 API를 사용 하 여 새 패키지를 푸시하는 것을 지원 합니다. 제공 된 ID와 버전이 있는 패키지가 이미 있는 경우 nuget.org은 푸시를 거부 합니다. 다른 패키지 원본은 기존 패키지를 바꾸는 것을 지원할 수 있습니다.

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>요청 매개 변수

Name           | In(다음 안에)     | Type   | 필수 | 메모
-------------- | ------ | ------ | -------- | -----
X NuGet-ApiKey | 헤더 | 문자열 | 예      | 예를 들어 `X-NuGet-ApiKey: {USER_API_KEY}`

API 키는 사용자가 패키지 원본에서 가져온 불투명 문자열이 며 클라이언트에 구성 됩니다. 특정 문자열 형식은 지정 되지 않지만 API 키의 길이는 HTTP 헤더 값에 대 한 적절 한 크기를 초과 하면 안 됩니다.

### <a name="request-body"></a>요청 본문

요청 본문은 다음과 같은 형식으로 제공 되어야 합니다.

#### <a name="multipart-form-data"></a>다중 파트 폼 데이터

요청 헤더는 `Content-Type` 이 `multipart/form-data` 고 요청 본문의 첫 번째 항목은 푸시되는 nupkg의 원시 바이트입니다. Multipart 본문의 후속 항목은 무시 됩니다. 파일 이름 또는 multipart 항목의 다른 헤더는 무시 됩니다.

### <a name="response"></a>응답

상태 코드 | 의미
----------- | -------
201, 202    | 패키지를 푸시 했습니다.
400         | 제공 된 패키지가 잘못 되었습니다.
409         | 제공 된 ID 및 버전의 패키지가 이미 있습니다.

서버 구현은 패키지가 성공적으로 푸시되는 경우 반환 되는 성공 상태 코드에 따라 달라 집니다.

## <a name="delete-a-package"></a>패키지 삭제

nuget.org는 패키지 삭제 요청을 "unlist"로 해석 합니다. 즉, 패키지를 기존 소비자에 게 계속 사용할 수 있지만 패키지가 검색 결과 나 웹 인터페이스에 더 이상 표시 되지 않습니다. 이 방법에 대 한 자세한 내용은 삭제 된 [패키지](../nuget-org/policies/deleting-packages.md) 정책을 참조 하세요. 다른 서버 구현에서는이 신호를 하드 삭제, 일시 삭제 또는 unlist로 자유롭게 해석할 수 있습니다. 예를 들어, [NuGet. 서버](https://www.nuget.org/packages/NuGet.Server) (이전 V2 API를 지 원하는 서버 구현)는 구성 옵션에 따라이 요청을 나열 취소 또는 hard delete로 처리 하는 것을 지원 합니다.

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>요청 매개 변수

Name           | In(다음 안에)     | Type   | 필수 | 메모
-------------- | ------ | ------ | -------- | -----
ID             | URL    | 문자열 | 예      | 삭제할 패키지의 ID입니다.
VERSION        | URL    | 문자열 | 예      | 삭제할 패키지의 버전입니다.
X NuGet-ApiKey | 헤더 | 문자열 | 예      | 예를 들어 `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>응답

상태 코드 | 의미
----------- | -------
204         | 패키지가 삭제 되었습니다.
404         | 제공 된 `ID` 및가 있는 패키지가 없습니다. `VERSION`

## <a name="relist-a-package"></a>패키지 다시 나열

패키지가 나열 되지 않은 경우 "relist" 끝점을 사용 하 여 검색 결과에 해당 패키지를 다시 한 번 표시 하 게 할 수 있습니다. 이 끝점은 [delete (unlist) 끝점과](#delete-a-package) 동일한 셰이프를 갖지만 `POST` 메서드 대신 HTTP 메서드를 사용 합니다 `DELETE` .

패키지가 이미 나열 되어 있으면 여전히 요청이 성공 합니다.

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>요청 매개 변수

Name           | In(다음 안에)     | Type   | 필수 | 메모
-------------- | ------ | ------ | -------- | -----
ID             | URL    | 문자열 | 예      | 다시 나열할 패키지의 ID입니다.
VERSION        | URL    | 문자열 | 예      | 다시 나열할 패키지의 버전입니다.
X NuGet-ApiKey | 헤더 | 문자열 | 예      | 예를 들어 `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>응답

상태 코드 | 의미
----------- | -------
200         | 이제 패키지가 나열 됩니다.
404         | 제공 된 `ID` 및가 있는 패키지가 없습니다. `VERSION`
