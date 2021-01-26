---
title: nuget.org 프로토콜
description: NuGet 클라이언트와 상호 작용 하는 진화 하는 nuget.org 프로토콜입니다.
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773980"
---
# <a name="nugetorg-protocols"></a>nuget.org 프로토콜

Nuget.org와 상호 작용 하려면 클라이언트가 특정 프로토콜을 따라야 합니다. 이러한 프로토콜은 계속 진화 하기 때문에 클라이언트는 특정 nuget.org Api를 호출할 때 사용 하는 프로토콜 버전을 식별 해야 합니다. 이렇게 하면 nuget.org가 이전 클라이언트에 대해 중단 되지 않는 방식으로 변경 내용을 적용할 수 있습니다.

> [!Note]
> 이 페이지에서 설명 하는 Api는 nuget.org에만 적용 되며, 다른 NuGet 서버 구현에서 이러한 Api를 도입 하는 것은 아닙니다. 

NuGet 에코 시스템에서 광범위 하 게 구현 된 NuGet API에 대 한 자세한 내용은 [API 개요](overview.md)를 참조 하세요.

이 항목에서는 다양 한 프로토콜의 존재 여부를 나열 합니다.

## <a name="nuget-protocol-version-410"></a>NuGet 프로토콜 버전 4.1.0

4.1.0 프로토콜은 nuget.org 계정에 대해 패키지의 유효성을 검사 하기 위해 nuget.org 이외의 서비스와 상호 작용 하는 verify 범위 키의 사용을 지정 합니다. `4.1.0`버전 번호는 불투명 문자열 이지만이 프로토콜을 지 원하는 공식 NuGet 클라이언트의 첫 번째 버전과 일치 하는 경우에 발생 합니다.

유효성 검사를 통해 사용자가 만든 API 키는 nuget.org 에서만 사용 되 고 타사 서비스의 다른 확인 또는 유효성 검사는 일회성 사용 확인 범위 키를 통해 처리 됩니다. 이러한 검증 범위 키는 패키지가 nuget.org의 특정 사용자 (계정)에 속해 있는지 확인 하는 데 사용할 수 있습니다.

### <a name="client-requirement"></a>클라이언트 요구 사항

클라이언트는 nuget.org에 패키지를 **푸시하** 는 API 호출을 수행할 때 다음 헤더를 전달 해야 합니다.

```
X-NuGet-Protocol-Version: 4.1.0
```

`X-NuGet-Client-Version`헤더의 의미 체계가 유사 하지만 공식 NuGet 클라이언트 에서만 사용 하도록 예약 되어 있습니다. 타사 클라이언트는 헤더 및 값을 사용 해야 합니다 `X-NuGet-Protocol-Version` .

**푸시** 프로토콜 자체는 [ `PackagePublish` 리소스](package-publish-resource.md)에 대 한 설명서에 설명 되어 있습니다.

클라이언트가 외부 서비스와 상호 작용 하 고 패키지가 특정 사용자 (계정)에 속하는지 여부를 확인 해야 하는 경우 다음 프로토콜을 사용 하 고 nuget.org의 API 키가 아닌 확인 범위 키를 사용 해야 합니다.

### <a name="api-to-request-a-verify-scope-key"></a>확인 범위 키를 요청 하는 API

이 API는 nuget.org 작성자가 자신이 소유한 패키지의 유효성을 검사 하기 위한 확인 범위 키를 가져오는 데 사용 됩니다.

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>요청 매개 변수

Name           | In(다음 안에)     | Type   | 필수 | 메모
-------------- | ------ | ------ | -------- | -----
ID             | URL    | 문자열 | 예      | 범위 키 확인이 요청 된 패키지 identidier
VERSION        | URL    | 문자열 | 아니요       | 패키지 버전
X NuGet-ApiKey | 헤더 | 문자열 | 예      | 예를 들어 `X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>응답

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>확인 범위 키를 확인 하는 API

이 API는 nuget.org author에서 소유 하는 패키지에 대 한 확인 범위 키의 유효성을 검사 하는 데 사용 됩니다.

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>요청 매개 변수

Name           | In(다음 안에)     | Type   | 필수 | 메모
-------------  | ------ | ------ | -------- | -----
ID             | URL    | 문자열 | 예      | 범위 키 확인이 요청 된 패키지 식별자입니다.
VERSION        | URL    | 문자열 | 아니요       | 패키지 버전
X NuGet-ApiKey | 헤더 | 문자열 | 예      | 예를 들어 `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> 이 확인 범위 API 키는 하루 중에 만료 되거나 처음 사용 될 때 (어느 쪽이 든 먼저 발생 하는 경우) 만료 됩니다.

#### <a name="response"></a>응답

상태 코드 | 의미
----------- | -------
200         | API 키가 올바릅니다.
403         | API 키가 잘못 되었거나 패키지에 대해 푸시할 수 있는 권한이 없습니다.
404         | `ID`및 `VERSION` (선택 사항)에서 참조 하는 패키지가 없습니다.
