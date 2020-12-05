---
title: 푸시 기호 패키지, NuGet API | Microsoft Docs
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 게시 서비스를 사용 하면 클라이언트가 새 기호 패키지를 게시할 수 있습니다.
keywords: NuGet API 푸시 기호 패키지
ms.reviewer: karann
ms.openlocfilehash: bd4a10cc976c9d0775a63cfe61c35327c196065c
ms.sourcegitcommit: e39e5a5ddf68bf41e816617e7f0339308523bbb3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96738879"
---
# <a name="push-symbol-packages"></a>기호 패키지 푸시

NuGet V3 API를 사용 하 여 기호 패키지 ([snupkg](../create-packages/Symbol-Packages-snupkg.md))를 푸시할 수 있습니다.
이러한 작업은 `SymbolPackagePublish` [서비스 인덱스](service-index.md)에 있는 리소스를 기반으로 합니다.

## <a name="versioning"></a>버전 관리

사용 되는 `@type` 값은 다음과 같습니다.

@type 값                 | 메모
--------------------        | -----
기호 Packagepublish/4.9.0  | 초기 릴리스

## <a name="base-url"></a>기준 URL

다음 Api에 대 한 기준 URL은 `@id` `SymbolPackagePublish/4.9.0` 패키지 소스의 [서비스 인덱스](service-index.md)에 있는 리소스의 속성 값입니다. 아래 설명서의 경우에는 nuget.exe의 URL이 사용 됩니다. `https://www.nuget.org/api/v2/symbolpackage`서비스 인덱스에 있는 값에 대 한 자리 표시자로 간주 `@id` 합니다.

## <a name="http-methods"></a>HTTP 메서드

`PUT`이 리소스에서 HTTP 메서드가 지원 됩니다. 

## <a name="push-a-symbol-package"></a>기호 패키지 푸시

nuget.org은 다음 API를 사용 하 여 새 기호 패키지 형식 ([snupkg](../create-packages/Symbol-Packages-snupkg.md))을 푸시하는 것을 지원 합니다. 

    PUT https://www.nuget.org/api/v2/symbolpackage

ID와 버전이 같은 기호 패키지는 여러 번 제출할 수 있습니다. 기호 패키지는 다음과 같은 경우에 거부 됩니다.
- ID와 버전이 같은 패키지가 없습니다.
- ID와 버전이 동일한 기호 패키지를 푸시 했지만 아직 게시 하지 않았습니다.
- 기호 패키지 ([snupkg](../create-packages/Symbol-Packages-snupkg.md))가 잘못 되었습니다 ( [기호 패키지 제약 조건](../create-packages/Symbol-Packages-snupkg.md)참조).

### <a name="request-parameters"></a>요청 매개 변수

이름           | In(다음 안에)     | 형식   | 필수 | 메모
-------------- | ------ | ------ | -------- | -----
X NuGet-ApiKey | 헤더 | 문자열 | 예      | 예, `X-NuGet-ApiKey: {USER_API_KEY}`

API 키는 사용자가 패키지 원본에서 가져온 불투명 문자열이 며 클라이언트에 구성 됩니다. 특정 문자열 형식은 지정 되지 않지만 API 키의 길이는 HTTP 헤더 값에 대 한 적절 한 크기를 초과 하면 안 됩니다.

### <a name="request-body"></a>요청 본문

기호 푸시에 대 한 요청 본문은 패키지 푸시 요청의 요청 본문을 사용 하는 것과 같습니다. [패키지 푸시 및 삭제](package-publish-resource.md)를 참조 하세요. 

### <a name="response"></a>응답

상태 코드 | 의미
----------- | -------
201         | 기호 패키지를 푸시 했습니다.
400         | 제공 된 기호 패키지가 잘못 되었습니다.
401         | 사용자에 게이 작업을 수행할 수 있는 권한이 없습니다.
404         | 제공 된 ID 및 버전의 해당 패키지가 없습니다.
409         | 제공 된 ID와 버전을 포함 하는 기호 패키지를 푸시 했지만 아직 사용할 수 없습니다.
413         | 패키지가 너무 깁니다.

