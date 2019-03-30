---
title: 패키지 세부 정보 URL 템플릿을 NuGet API
description: 패키지 세부 정보 URL 템플릿을 한 패키지 세부 정보로 링크 웹 UI에 표시 하는 클라이언트 수
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638080"
---
# <a name="package-details-url-template"></a>패키지 세부 정보 URL 템플릿

웹 브라우저에서 더 많은 패키지 세부 정보를 보려면 사용자가 사용할 수 있는 URL을 작성 하는 클라이언트는 것이 가능 합니다. 패키지 소스를 NuGet 클라이언트 응용 프로그램 표시 범위 내에서 맞지 않을 수 있습니다 하는 패키지에 대 한 추가 정보를 표시 하려고 할 때 유용 합니다.

이 URL을 작성에 사용 되는 리소스를 `PackageDetailsUriTemplate` 에서 리소스를 찾을 합니다 [서비스 인덱스](service-index.md)합니다.

## <a name="versioning"></a>버전 관리

다음 `@type` 값이 사용 됩니다.

@type 값                     | 노트
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | 초기 릴리스

## <a name="url-template"></a>URL 템플릿

다음 API에 대 한 URL의 값은는 `@id` 앞에서 언급 한 리소스 중 하나를 사용 하 여 연결 된 속성 `@type` 값입니다.

## <a name="http-methods"></a>HTTP 메서드

웹 페이지를 지원 해야 클라이언트 사용자를 대신 하 여 패키지 세부 정보 URL 요청을 하려면 없습니다, 있지만 `GET` 쉽게 웹 브라우저에서 열 수를 클릭 한 URL을 허용 하는 방법입니다.

## <a name="construct-the-url"></a>URL 생성

알려진된 패키지 ID 및 버전을 지정 하 여 클라이언트 구현 웹 인터페이스에 액세스 하는 데 사용 하는 URL을 생성할 수 있습니다. 클라이언트 구현에는 URL로 웹 브라우저를 열고을 패키지에 자세히 알아보려면 수 있도록 사용자에 게이 구성 된 URL (또는 클릭 가능한 링크) 표시 됩니다. 패키지 세부 정보 페이지의 내용은 서버 구현에 의해 결정 됩니다.

URL은 절대 URL 이어야 하 고 (프로토콜) 체계는 HTTPS 여야 합니다.

값을 `@id` 서비스에서 인덱스는 다음과 같은 자리 표시자 토큰 중 하나를 포함 하는 URL 문자열:

### <a name="url-placeholders"></a>URL 자리 표시자

이름        | 형식    | 필수 | 노트
----------- | ------- | -------- | -----
`{id}`      | string  | 아니요       | 패키지 ID에 대 한 세부 정보를 가져오려면
`{version}` | string  | 아니요       | 패키지 버전에 대 한 세부 정보를 가져오려면

서버를 승인할지 `{id}` 및 `{version}` 모든 대/소문자를 사용 하 여 값입니다. 서버를 버전 인지는 중요 한 있어야 뿐만 [정규화 된](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers)합니다. 즉, 서버를 승인할지 정규화 되지 않은 버전을 그대로 사용할 수도 있습니다.

예를 들어, nuget.org의 패키지 세부 정보 템플릿을 다음과 같습니다.

    https://www.nuget.org/packages/{id}/{version}

클라이언트 구현 NuGet.Versioning 4.3.0에 대 한 링크 패키지 세부 정보를 표시 하는 경우는 다음 URL을 생성 하 고 사용자에 게 제공:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
