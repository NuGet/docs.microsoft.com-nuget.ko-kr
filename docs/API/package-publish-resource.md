---
title: "밀어넣기 및 삭제를 NuGet API | Microsoft Docs"
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
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "게시 서비스에는 클라이언트가 새 패키지를 게시 하 고 unlist 또는 기존 패키지를 삭제할 수 있습니다."
keywords: "NuGet API 푸시 패키지 API NuGet 패키지를 삭제, API NuGet 패키지를 NuGet API 업로드 패키지가 unlist, API NuGet 패키지를 만듭니다."
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 1fa3c0e1698a11208d9ef29fdf26a4980cb60cf5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="push-and-delete"></a>밀어넣기 및 삭제

푸시 및 삭제 (또는 서버 구현에 따라 unlist) 수는 NuGet V3 API를 사용 하 여 패키지 합니다.
두 작업은에 기반을 둔는 `PackagePublish` 에서 리소스를 찾을 [서비스 인덱스](service-index.md)합니다.

## <a name="versioning"></a>버전 관리

다음 `@type` 값이 사용 됩니다.

@type 값          | 참고
-------------------- | -----
PackagePublish/2.0.0 | 초기 릴리스

## <a name="base-url"></a>기준 URL

다음 Api에 대 한 기본 URL의 값은는 `@id` 의 속성은 `PackagePublish/2.0.0` 패키지 소스에서 리소스 [서비스 인덱스](service-index.md)합니다. 아래 설명서에 대 한 nuget.org의 URL이 사용 됩니다. 고려 `https://www.nuget.org/api/v2/package` 에 대 한 자리 표시자로는 `@id` 서비스 인덱스에서 값을 찾을 수 있습니다.

동일한 프로토콜은이 URL의 레거시 V2 푸시 끝점으로 같은 위치를 가리키는지 note 합니다.

## <a name="http-methods"></a>HTTP 메서드

`PUT` 및 `DELETE` HTTP 메서드가이 리소스에서 지원 됩니다. 각 끝점에서 지원 되는 어떤 메서드는, 다음을 참조 합니다.

## <a name="push-a-package"></a>푸시 한 패키지

nuget.org 다음 API를 사용 하 여 푸시 새 패키지를 지원 합니다. 제공 된 ID와 버전을 사용 하 여 패키지에 이미 있으면 nuget.org 푸시를 거부 합니다. 기존 패키지를 대체 합니다. 다른 패키지 원본을 지원할 수 있습니다.

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>요청 매개 변수

이름           | 입력     | 형식   | 필수 | 참고
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Header | string | 예      | 예를 들면 `X-NuGet-ApiKey: {USER_API_KEY}`과 같습니다.

API 키는 사용자가 패키지 소스에서 수신 하 고 클라이언트를 구성 하는 불투명 문자열입니다. 특정 문자열 형식은 없습니다 위임 되는지 있지만 API 키의 길이 HTTP 헤더 값에 대 한 적절 한 크기를 초과할 수 없습니다.

### <a name="request-body"></a>요청 본문

요청 본문에는 다음과 같은 형태로 야 합니다.

#### <a name="multipart-form-data"></a>다중 파트 양식 데이터

요청 헤더 `Content-Type` 은 `multipart/form-data` 및 요청 본문의 첫 번째 항목은 눌렀는지.nupkg의 원시 바이트입니다. 다중 파트 본문에 있는 다음 항목은 무시 됩니다. 파일 이름 또는 다중 항목의 다른 모든 헤더는 무시 됩니다.

### <a name="response"></a>응답

상태 코드 | 의미
----------- | -------
201, 202    | 패키지가는 성공적으로 푸시되 지
400         | 제공 된 패키지가 잘못 되었습니다.
409         | 제공 된 ID와 버전을 사용 하 여 패키지 이미 있습니다.

패키지를 성공적으로 푸시 될 때 반환 되는 성공 상태 코드에 서버 구현은 달라 집니다.

## <a name="delete-a-package"></a>패키지 삭제

nuget.org 패키지 삭제 요청으로 해석 하는 "unlist"입니다. 즉, 패키지를 패키지의 기존 사용자가 계속 사용할 수 있지만 패키지 또는 웹 인터페이스 검색 결과에 더 이상 표시 합니다. 이 연습에 대 한 자세한 내용은 참조는 [패키지 삭제](../policies/deleting-packages.md) 정책입니다. 하드 delete이 신호를 해석 하거나 일시 삭제 하거나 unlist 하는 다른 서버 구현입니다. 예를 들어 [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (만 이전 V2 API를 지 원하는 서버 구현)는 unlist 또는 구성 옵션에 따라 하드 삭제로이 요청을 처리를 지원 합니다.

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>요청 매개 변수

이름           | 입력     | 형식   | 필수 | 참고
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | 예      | 패키지의 ID를 삭제 하려면
VERSION        | URL    | string | 예      | 삭제할 패키지의 버전
X-NuGet-ApiKey | Header | string | 예      | 예를 들면 `X-NuGet-ApiKey: {USER_API_KEY}`과 같습니다.

### <a name="response"></a>응답

상태 코드 | 의미
----------- | -------
204         | 패키지 삭제
404         | 제공 된 패키지가 `ID` 및 `VERSION` 존재
