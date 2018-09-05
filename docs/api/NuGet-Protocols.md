---
title: nuget.org 프로토콜
description: NuGet 클라이언트와 상호 작용을 발전 nuget.org 프로토콜입니다.
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547275"
---
# <a name="nugetorg-protocols"></a>nuget.org 프로토콜

Nuget.org를 사용 하 여 상호 작용, 클라이언트를 특정 프로토콜을 수행 해야 합니다. 이러한 프로토콜 진화 하는, 때문에 클라이언트가 특정 nuget.org Api를 호출할 때 사용할 프로토콜 버전을 식별 해야 합니다. 따라서 nuget.org 이전 버전의 클라이언트에 대 한 변경 내용을 줄 바꿈하지 않는 방식으로 소개 합니다.

> [!Note]
> 이 페이지에서 설명 하는 Api nuget.org에 특정 되며 다른 NuGet 서버 구현에서 이러한 Api를 도입 하기 위한으로 예상할 수 없습니다. 

NuGet 에코 시스템에서 광범위 하 게 구현 하는 NuGet API에 대 한 내용은 참조는 [API 개요](overview.md)합니다.

이 항목에서는 다양 한 프로토콜 및 존재 여부에 나올 때를 나열 합니다.

## <a name="nuget-protocol-version-410"></a>NuGet 프로토콜 버전 4.1.0

4.1.0 프로토콜 이외의 nuget.org에서 패키지를 nuget.org 계정에 대해 유효성을 검사 하는 서비스와 상호 작용 하는 범위 확인 키의 사용법을 지정 합니다. `4.1.0` 버전 번호는 불투명 문자열 이지만이 프로토콜을 지원 되는 공식 NuGet 클라이언트의 첫 번째 버전에 맞추어 발생 합니다.

유효성 검사 하면 사용자가 만든 API 키를 사용 하 여 nuget.org에만 되는 다른 확인 또는 타사 서비스에서 유효성 검사는 일회용으로 사용 범위 확인 키를 통해 처리 됩니다. 패키지를 nuget.org에서 특정 사용자 (계정)에 속해 있는지 유효성을 검사 하려면 이러한 범위 확인 키를 사용할 수 있습니다.

### <a name="client-requirement"></a>클라이언트 요구 사항

클라이언트 API를 호출 하는 경우 다음 헤더를 전달 하는 데 필요한 **푸시** nuget.org에 패키지 합니다.

    X-NuGet-Protocol-Version: 4.1.0

`X-NuGet-Client-Version` 헤더와 유사한 의미 체계를 갖지만 공식 NuGet 클라이언트 에서만 사용 하도록 예약 되어 있습니다. 제 3 자 클라이언트가 사용 해야 합니다 `X-NuGet-Protocol-Version` 헤더 및 값입니다.

**푸시** 프로토콜 자체에 대 한 설명서에서 설명 합니다 [ `PackagePublish` 리소스](package-publish-resource.md)합니다.

외부 서비스와 패키지를 특정 사용자 (계정)에 속해 있는지 여부를 확인 해야 클라이언트 상호 작용을 다음 프로토콜을 사용 하며 확인 범위 키 및 nuget.org에서 API 키는 하지 사용 합니다.

### <a name="api-to-request-a-verify-scope-key"></a>범위 확인 키를 요청 하는 API

이 API는 nuget.org 작성자도 소유 패키지 유효성 검사에 대 한 범위 확인 키를 가져오는 데 사용 됩니다.

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>요청 매개 변수

이름           | 입력     | 형식   | 필수 | 노트
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | 예      | 범위 확인 키가 요청 되는 패키지 identidier
VERSION        | URL    | string | 아니요       | 패키지 버전
X-NuGet-ApiKey | 헤더 | string | 예      | 예를 들면 `X-NuGet-ApiKey: {USER_API_KEY}`과 같습니다.

#### <a name="response"></a>응답

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API 범위 확인 키를 확인 하려면

이 API는 nuget.org 작성자가 소유 하는 패키지에 대 한 확인 범위 키 유효성 검사에 사용 됩니다.

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>요청 매개 변수

이름           | 입력     | 형식   | 필수 | 노트
-------------  | ------ | ------ | -------- | -----
ID             | URL    | string | 예      | 범위 확인 키가 요청 되는 패키지 식별자
VERSION        | URL    | string | 아니요       | 패키지 버전
X-NuGet-ApiKey | 헤더 | string | 예      | 예를 들면 `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`과 같습니다.

> [!Note]
> 이 확인 범위 API 키 만료 날짜의 시간 또는 처음 사용할 때 중 먼저 발생 합니다.

#### <a name="response"></a>응답

상태 코드 | 의미
----------- | -------
200         | API 키가 유효한
403         | API 키가 잘못 되었거나 패키지에 대해 적용할 권하지 없음
404         | 패키지 참조 `ID` 고 `VERSION` (선택 사항)가 없습니다
