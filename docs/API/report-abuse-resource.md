---
title: "보고서 남용 URL 템플릿, NuGet API | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "보고서 남용 URL 서식 파일에는 클라이언트를 신고 링크는 해당 UI에 표시할 수 있습니다."
keywords: "NuGet API 신고, NuGet API 파일 불만, nuget.org 보고서 URL 서식 파일"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: efbe5704e6e6028f9382fea3fe5ec453f573a2e9
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="report-abuse-url-template"></a>보고서 남용 URL 서식 파일

특정 패키지에 대 한 신고 하기 위해 사용자가 사용할 수 있는 URL을 작성 하는 클라이언트에 대 한 것 같습니다. 패키지 소스에서 패키지 원본에 남용 보고서를 위임 하려면 모든 클라이언트 경험 (도 제 3 자)를 사용 하도록 설정 하려는 경우에 유용 합니다.

패키지 콘텐츠를 가져오기 위해 사용 되는 리소스는는 `ReportAbuseUriTemplate` 에서 리소스를 찾을 [서비스 인덱스](service-index.md)합니다.

## <a name="versioning"></a>버전 관리

다음 `@type` 값이 사용 됩니다.

@type 값                       | 노트
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | 초기 릴리스
ReportAbuseUriTemplate/3.0.0-rc   | 별칭 `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL 템플릿

다음 API에 대 한 URL의 값은 고 `@id` 앞에서 언급 한 리소스 중 하나가 지정 된 연결 된 속성 `@type` 값입니다.

## <a name="http-methods"></a>HTTP 메서드

웹 페이지를 지원 해야 하지는 않지만 클라이언트는 사용자를 위해 보고서 남용 URL로 요청을,는 `GET` 메서드를 쉽게 웹 브라우저에서 열 수를 클릭 한 URL을 허용 합니다.

## <a name="construct-the-url"></a>URL 구성

알려진된 패키지 ID 및 버전을 지정 된, 클라이언트 구현에서 URL을 구성 웹 인터페이스에 액세스 하는 데 사용 합니다. 클라이언트 구현에서 모든 필요한 남용 보고서를 URL에 웹 브라우저를 열고 수 있도록 사용자에 게이 구성 된 URL (또는 클릭할 수 있는 링크) 표시 되어야 합니다. 남용 보고서 양식 구현 서버 구현에 의해 결정 됩니다.

값은 `@id` 다음 자리 표시자 토큰 중 하나를 포함 하는 URL 문자열:

### <a name="url-placeholders"></a>URL 자리 표시자

name        | 형식    | 필수 | 노트
----------- | ------- | -------- | -----
`{id}`      | string  | 아니요       | 패키지 ID를 신고 하기에 대 한
`{version}` | string  | 아니요       | 패키지 버전에 대 한 신고를

`{id}` 및 `{version}` 서버 구현에 의해 해석 하는 값은 대/소문자 구분 및 버전 정규화 되는 여부에 민감한 하지 여야 합니다.

예를 들어 nuget.org의 보고서 남용 서식 파일은 다음과 같습니다.

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

클라이언트 구현에서 NuGet.Versioning 4.3.0에 대 한 링크를 보고서 남용 양식으로 표시 하는 경우 것은 다음 URL을 생성 하 고 사용자에 게 제공 합니다.

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
