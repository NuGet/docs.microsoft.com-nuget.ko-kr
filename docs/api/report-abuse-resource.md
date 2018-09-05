---
title: 보고서 남용 URL 템플릿을 NuGet API
description: 보고서 남용 URL 템플릿은 클라이언트를 UI에 신고 링크를 표시할 수 있습니다.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d0ff41b08eeba5a6e4bc7c44722b6bc57f502047
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549341"
---
# <a name="report-abuse-url-template"></a>보고서 남용 URL 템플릿

특정 패키지에 대 한 신고 하기 위해 사용자가 사용할 수 있는 URL을 작성 하는 클라이언트는 것이 가능 합니다. 패키지 소스를 남용 보고서 패키지 원본에 위임 하려면 모든 클라이언트 환경을 (도 제 3 자)를 사용 하도록 설정 하려는 경우에 유용 합니다.

이 URL을 작성에 사용 되는 리소스를 `ReportAbuseUriTemplate` 에서 리소스를 찾을 합니다 [서비스 인덱스](service-index.md)합니다.

## <a name="versioning"></a>버전 관리

다음 `@type` 값이 사용 됩니다.

@type 값                       | 노트
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | 초기 릴리스
ReportAbuseUriTemplate/3.0.0-rc   | 별칭 `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL 템플릿

다음 API에 대 한 URL의 값은는 `@id` 앞에서 언급 한 리소스 중 하나를 사용 하 여 연결 된 속성 `@type` 값입니다.

## <a name="http-methods"></a>HTTP 메서드

웹 페이지를 지원 해야 하지는 않지만 클라이언트는 사용자 대신 보고서 남용 URL로 요청을를 `GET` 쉽게 웹 브라우저에서 열 수를 클릭 한 URL을 허용 하는 방법입니다.

## <a name="construct-the-url"></a>URL 생성

알려진된 패키지 ID 및 버전을 지정 하 여 클라이언트 구현 웹 인터페이스에 액세스 하는 데 사용 하는 URL을 생성할 수 있습니다. 클라이언트 구현 선택 수 있게 하는 사용자가 URL로 웹 브라우저를 열고 필요한 남용 보고서에이 구성 된 URL (또는 클릭 가능한 링크가) 표시 됩니다. 남용 보고서 양식 구현의 서버 구현에 의해 결정 됩니다.

값은 `@id` 다음 자리 표시자 토큰 중 하나를 포함 하는 URL 문자열:

### <a name="url-placeholders"></a>URL 자리 표시자

이름        | 형식    | 필수 | 노트
----------- | ------- | -------- | -----
`{id}`      | string  | 아니요       | 패키지 ID에 대해 신고
`{version}` | string  | 아니요       | 패키지 버전에 대해 신고를

합니다 `{id}` 고 `{version}` 서버 구현에 의해 해석 되는 값은 대/소문자 구분 및 버전 정규화 되 고 있는지 여부에 민감 하지 이어야 합니다.

예를 들어, nuget.org의 보고서 남용 서식 파일은 다음과 같습니다.

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

클라이언트 구현 NuGet.Versioning 4.3.0에 대 한 보고서 남용 폼에 링크를 표시 하는 경우는 다음 URL을 생성 하 고 사용자에 게 제공:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
