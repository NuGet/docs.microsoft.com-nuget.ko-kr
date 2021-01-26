---
title: 패키지 세부 정보 URL 템플릿, NuGet API
description: 패키지 세부 정보 URL 템플릿을 사용 하면 클라이언트에서 추가 패키지 세부 정보에 대 한 웹 링크를 UI에 표시할 수 있습니다.
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: aaeedea9750c11099b34e927bd8442656839d784
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773950"
---
# <a name="package-details-url-template"></a>패키지 세부 정보 URL 템플릿

클라이언트는 사용자가 웹 브라우저에서 추가 패키지 세부 정보를 볼 때 사용할 수 있는 URL을 작성할 수 있습니다. 이는 NuGet 클라이언트 응용 프로그램에서 표시 하는 범위 내에 적합 하지 않을 수 있는 패키지에 대 한 추가 정보를 패키지 원본에서 표시 하려는 경우에 유용 합니다.

이 URL을 작성 하는 데 사용 되는 리소스는 `PackageDetailsUriTemplate` [서비스 인덱스](service-index.md)에 있는 리소스입니다.

## <a name="versioning"></a>버전 관리

사용 되는 `@type` 값은 다음과 같습니다.

@type 값                     | 메모
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | 초기 릴리스

## <a name="url-template"></a>URL 템플릿

다음 API에 대 한 URL은 `@id` 앞서 언급 한 리소스 값 중 하 나와 연결 된 속성의 값입니다 `@type` .

## <a name="http-methods"></a>HTTP 메서드

클라이언트는 사용자를 대신 하 여 패키지 세부 정보 URL에 대 한 요청을 수행할 수 없지만 웹 페이지는 클릭 된 URL을 `GET` 웹 브라우저에서 쉽게 열도록 허용 하는 메서드를 지원 해야 합니다.

## <a name="construct-the-url"></a>URL 생성

알려진 패키지 ID 및 버전이 제공 되 면 클라이언트 구현에서 웹 인터페이스에 액세스 하는 데 사용 되는 URL을 생성할 수 있습니다. 클라이언트 구현에서는이 생성 된 URL (또는 클릭 가능한 링크)을 사용자에 게 표시 하 여 URL에 대 한 웹 브라우저를 열고 패키지에 대해 자세히 알아볼 수 있습니다. 패키지 세부 정보 페이지의 내용은 서버 구현에 의해 결정 됩니다.

URL은 절대 URL 이어야 하 고 스키마 (프로토콜)는 HTTPS 여야 합니다.

`@id`서비스 인덱스에서의 값은 다음 자리 표시자 토큰 중 하나를 포함 하는 URL 문자열입니다.

### <a name="url-placeholders"></a>URL 자리 표시자

Name        | Type    | 필수 | 메모
----------- | ------- | -------- | -----
`{id}`      | 문자열  | 아니요       | 세부 정보를 가져올 패키지 ID
`{version}` | 문자열  | 아니요       | 세부 정보를 가져올 패키지 버전

서버는 `{id}` `{version}` 대/소문자를 구분 하 여 및 값을 허용 해야 합니다. 또한 서버는 버전이 [정규화](../concepts/package-versioning.md#normalized-version-numbers)되었는지 여부를 구분 하지 않아야 합니다. 즉, 서버에도 정규화 되지 않은 버전이 허용 되어야 합니다.

예를 들어, nuget.exe의 패키지 세부 정보 템플릿은 다음과 같습니다.

```http
https://www.nuget.org/packages/{id}/{version}
```

클라이언트 구현에서 NuGet의 패키지 세부 정보에 대 한 링크를 표시 해야 하는 경우 4.3.0는 다음 URL을 생성 하 여 사용자에 게 제공 합니다.

```http
https://www.nuget.org/packages/NuGet.Versioning/4.3.0
```
