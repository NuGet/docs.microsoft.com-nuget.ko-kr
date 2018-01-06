---
title: "nuget.org 프로토콜 | Microsoft Docs"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba1d9742-9f1c-42ff-8c30-8e953e23c501
description: "NuGet 클라이언트와 상호 작용할 수 발전 nuget.org 프로토콜입니다."
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 0bc71795d120256b9eb14ca64141f0b69f01e620
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/05/2018
---
# <a name="nugetorg-protocols"></a>nuget.org 프로토콜

Nuget.org를 상호작용 하려면 클라이언트를 특정 프로토콜을 수행 해야 합니다. 이러한 프로토콜 진화 유지 하기 때문에 클라이언트가 특정 nuget.org Api를 호출할 때 사용 하 여 프로토콜 버전을 식별 해야 합니다. 이렇게 하면 이전 클라이언트에 대 한 줄 바꿈하지 않는 방식으로 변경 내용을 소개 하기 위한 nuget.org가 있습니다.

> [!Note]
> 이 페이지에서 설명 하는 Api nuget.org 관련이 이며 이러한 Api를 소개 하기 위한 다른 NuGet 서버 구현에 없는 기대 합니다. 

NuGet 에코 시스템에서 광범위 하 게 구현 하는 NuGet API에 대 한 정보를 참조 하십시오.는 [API 개요](overview.md)합니다.

이 항목으로 다양 한 프로토콜 및 존재에 나올 때 나열 합니다.

## <a name="nuget-protocol-version-410"></a>NuGet 프로토콜 버전 4.1.0

4.1.0 프로토콜 확인 범위 nuget.org nuget.org 계정에 대해 패키지의 유효성 검사를 제외한 다른 서비스와 상호 작용 하는 키의 사용을 지정 합니다. `4.1.0` 버전 번호는 불투명 문자열 이지만이 프로토콜을 지원 하는 공식 NuGet 클라이언트의 첫 번째 버전과 일치 하 게 발생 합니다.

유효성 검사를 수행 하면 사용자가 만든 API 키, nuget.org에만 사용 됩니다이 다른 확인 또는 제 3 자 서비스에서 유효성 검사 일회용 범위 확인 키를 통해 처리 됩니다. 패키지 nuget.org에 있는 특정 사용자 (계정)에 속해 있는지 확인 하 이러한 범위 확인 키를 사용할 수 있습니다.

### <a name="client-requirement"></a>클라이언트 요구 사항

클라이언트에 대 한 API 호출을 할 때 다음 헤더를 전달 하는 데 필요한 **푸시** nuget.org 패키지:

```
X-NuGet-Protocol-Version: 4.1.0
```

`X-NuGet-Client-Version` 헤더와 유사한 의미 체계를 갖지만 공식 NuGet 클라이언트 에서만 사용 하도록 예약 되어 있습니다. 제 3 자 클라이언트를 사용 해야는 `X-NuGet-Protocol-Version` 헤더와 값입니다.

**푸시** 프로토콜 자체에 대 한 설명서에서 설명 된 [ `PackagePublish` 리소스](package-publish-resource.md)합니다.

외부 서비스 및 패키지 특정 사용자 (계정)에 속하는지 여부를 확인 하는 요구와 클라이언트 상호 작용을 하는 경우 다음 프로토콜을 사용 하 고 확인 범위 키 및 하지 nuget.org에서 API 키를 사용 합니다.

### <a name="api-to-request-a-verify-scope-key"></a>범위 확인 키를 요청 하는 API

이 API는 즉 사용자가 소유 하는 패키지의 유효성 검사에 nuget.org 작성자에 대 한 범위 확인 키를 가져오는 데 사용 됩니다.

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>요청 매개 변수

name           | 입력     | 형식   | 필수 | 노트
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | 예      | 범위 확인 키를 요청한 대상 패키지 identidier
VERSION        | URL    | string | 아니요       | 패키지 버전
X-NuGet-ApiKey | Header | string | 예      | 예를 들면 `X-NuGet-ApiKey: {USER_API_KEY}`과 같습니다.

#### <a name="response"></a>응답

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>범위 확인 키를 확인 하는 API

이 API는 사용 하 여을 nuget.org 작성자가 소유 하는 패키지에 대 한 범위 확인 키를 검사 합니다.

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>요청 매개 변수

name           | 입력     | 형식   | 필수 | 노트
-------------  | ------ | ------ | -------- | -----
ID             | URL    | string | 예      | 범위 확인 키를 요청한 대상 패키지 식별자
VERSION        | URL    | string | 아니요       | 패키지 버전
X-NuGet-ApiKey | Header | string | 예      | 예를 들면 `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`과 같습니다.

> [!Note]
> 이 확인 범위 API 키 날의 시간에 만료 됩니다. 또는 처음 사용할 때 중 먼저 발생 합니다.

#### <a name="response"></a>응답

상태 코드 | 의미
----------- | -------
200         | API 키가 유효
403         | API 키가 잘못 되었거나 패키지에 대해 적용할 인증 되지 않았습니다.
404         | 패키지에서 참조 `ID` 및 `VERSION` (선택 사항) 존재 하지 않는
