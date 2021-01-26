---
title: 신고 URL 템플릿, NuGet API 보고
description: 보고서 신고 URL 템플릿을 사용 하면 클라이언트는 자신의 UI에 신고 링크를 표시할 수 있습니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775234"
---
# <a name="report-abuse-url-template"></a>신고 URL 템플릿 신고

클라이언트는 사용자가 특정 패키지에 대 한 불건전 사용자를 보고 하는 데 사용할 수 있는 URL을 작성할 수 있습니다. 이 기능은 패키지 원본에서 모든 클라이언트 환경 (타사)을 사용 하도록 설정 하 여 불건전 보고서를 패키지 원본에 위임 하려는 경우에 유용 합니다.

이 URL을 작성 하는 데 사용 되는 리소스는 `ReportAbuseUriTemplate` [서비스 인덱스](service-index.md)에 있는 리소스입니다.

## <a name="versioning"></a>버전 관리

사용 되는 `@type` 값은 다음과 같습니다.

@type 값                       | 메모
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | 초기 릴리스
ReportAbuseUriTemplate/3.0.0   | 별칭 `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL 템플릿

다음 API에 대 한 URL은 `@id` 앞서 언급 한 리소스 값 중 하 나와 연결 된 속성의 값입니다 `@type` .

## <a name="http-methods"></a>HTTP 메서드

클라이언트가 사용자를 대신 하 여 신고 URL에 대 한 요청을 수행 하기 위한 것은 아니지만 웹 페이지는 `GET` 클릭 된 URL을 웹 브라우저에서 쉽게 열도록 허용 하는 메서드를 지원 해야 합니다.

## <a name="construct-the-url"></a>URL 생성

알려진 패키지 ID 및 버전이 제공 되 면 클라이언트 구현에서 웹 인터페이스에 액세스 하는 데 사용 되는 URL을 생성할 수 있습니다. 클라이언트 구현에서는이 생성 된 URL (또는 클릭 가능한 링크)을 사용자에 게 표시 하 여 URL에 대 한 웹 브라우저를 열고 필요한 불건전 보고서를 만들 수 있도록 합니다. 불건전 보고서 양식의 구현은 서버 구현에 의해 결정 됩니다.

의 값은 `@id` 다음 자리 표시자 토큰 중 하나를 포함 하는 URL 문자열입니다.

### <a name="url-placeholders"></a>URL 자리 표시자

Name        | Type    | 필수 | 메모
----------- | ------- | -------- | -----
`{id}`      | 문자열  | 아니요       | 신고를 보고할 패키지 ID
`{version}` | 문자열  | 아니요       | 신고를 보고할 패키지 버전

`{id}` `{version}` 서버 구현에서 해석 되는 및 값은 대/소문자를 구분 하지 않고 버전이 정규화 되었는지 여부를 구분 하지 않아야 합니다.

예를 들어, nuget.exe의 신고는 다음과 같습니다.

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

클라이언트 구현에서 NuGet에 대 한 보고서 불건전 폼의 링크를 표시 해야 하는 경우 다음 URL을 생성 하 여 사용자에 게 제공 합니다. 4.3.0.

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
