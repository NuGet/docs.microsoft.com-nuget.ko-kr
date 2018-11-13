---
title: 기호 패키지, NuGet API 푸시 | Microsoft Docs
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 게시 서비스에는 새 기호 패키지를 게시 하는 클라이언트 수 있습니다.
keywords: NuGet API 푸시 기호 패키지
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580416"
---
# <a name="push-symbol-packages"></a>기호 패키지 푸시

패키지를 푸시 하려면 기호 수 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) NuGet V3 API를 사용 합니다.
이러한 작업은 기반을 둔 합니다 `SymbolPackagePublish` 에서 리소스를 찾을 합니다 [서비스 인덱스](service-index.md)합니다.

## <a name="versioning"></a>버전 관리

다음 `@type` 값이 사용 됩니다.

@type 값                 | 노트
--------------------        | -----
SymbolPackagePublish/4.9.0  | 초기 릴리스

## <a name="base-url"></a>기준 URL

다음 Api에 대 한 기본 URL의 값은를 `@id` 의 속성을 `SymbolPackagePublish/4.9.0` 패키지 원본에 대 한 리소스 [서비스 인덱스](service-index.md). 아래 설명서 nuget.org의 URL은 사용 합니다. 것이 좋습니다 `https://www.nuget.org/api/v2/symbolpackage` 자리 표시자로는 `@id` 서비스 인덱스에서 찾을 값입니다.

## <a name="http-methods"></a>HTTP 메서드

`PUT` HTTP 메서드는이 리소스에서 지원 합니다. 

## <a name="push-a-symbol-package"></a>기호 패키지를 푸시

nuget.org에 푸시하는 새 기호 패키지 형식 지원 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 다음 API를 사용 하 여 합니다. 

    PUT https://www.nuget.org/api/v2/symbolpackage

기호 패키지는 동일한 ID 및 버전을 사용 하 여 여러 번 제출할 수 있습니다. 기호 패키지는 다음과 같은 경우 거부 됩니다.
- 패키지는 동일한 ID 및 버전을 사용 하 여 존재 하지 않습니다.
- 동일한 ID 및 버전을 사용 하 여 기호 패키지 푸시된 있지만 아직 게시 되지 않습니다.
- 기호 패키지 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 잘못 되었습니다 (참조 [기호 패키지 제약 조건](../create-packages/Symbol-Packages-snupkg.md)).

### <a name="request-parameters"></a>요청 매개 변수

이름           | 입력     | 형식   | 필수 | 노트
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | 헤더 | string | 예      | 예를 들면 `X-NuGet-ApiKey: {USER_API_KEY}`과 같습니다.

API 키는 사용자가 패키지 원본에서 받은 및 클라이언트를 구성 하는 불투명 문자열입니다. 특정 문자열 서식 없음은 위임 하지만 API 키의 길이 HTTP 헤더 값에 대 한 적절 한 크기를 초과할 수 없습니다.

### <a name="request-body"></a>요청 본문

기호 푸시에 대 한 요청 본문은 패키지 푸시 요청의 요청 본문을 사용 하 여 동일 (참조 [패키지 푸시 및 삭제](package-publish-resource.md)). 

### <a name="response"></a>응답

상태 코드 | 의미
----------- | -------
201         | 기호 패키지를 푸시 했습니다.
400         | 제공 된 기호 패키지 올바르지 않습니다.
401         | 사용자는이 작업을 수행할 수 있는 권한이 없습니다.
404         | 제공 된 ID와 버전을 사용 하 여 해당 패키지가 존재 하지 않습니다.
409         | 제공 된 ID와 버전을 사용 하 여 기호 패키지 푸시된 있지만 아직 사용할 수 없는 합니다.
413         | 패키지가 너무 큽니다.

