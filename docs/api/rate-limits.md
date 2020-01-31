---
title: 요율 한도, NuGet API
description: NuGet Api는 남용을 방지 하기 위해 적용 되는 요금 제한을 적용 합니다.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813197"
---
# <a name="rate-limits"></a>속도 제한

NuGet.org API는 악용을 방지 하기 위해 요금 제한을 적용 합니다. Rate 제한을 초과 하는 요청은 다음 오류를 반환 합니다. 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

요금 제한을 사용 하 여 요청을 제한 하는 것 외에도 일부 Api는 할당량을 적용 합니다. 할당량을 초과 하는 요청은 다음 오류를 반환 합니다.

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

다음 표에서는 NuGet.org API에 대 한 요율 제한을 나열 합니다.

## <a name="package-search"></a>패키지 검색

> [!Note]
> 현재는 전송률이 제한 되지 않으므로 Nuget.exe의 [V3 검색 api](search-query-service-resource.md) 를 사용 하는 것이 좋습니다. V1 및 V2 검색 Api의 경우 다음과 같은 제한이 적용 됩니다.

| API | 제한 유형 | 제한 값 | API 사용 사례 |
|:---|:---|:---|:---|
**GET** `/api/v1/Packages` | IP | 1000/분 | V1 OData `Packages` 컬렉션을 통해 NuGet 패키지 메타 데이터 쿼리 |
**GET** `/api/v1/Search()` | IP | 3000/분 | V1 검색 끝점을 통해 NuGet 패키지 검색 | 
**GET** `/api/v2/Packages` | IP | 2만/분 | V2 OData `Packages` 컬렉션을 통해 NuGet 패키지 메타 데이터 쿼리 | 
**GET** `/api/v2/Packages/$count` | IP | 100/분 | V2 OData `Packages` 컬렉션을 통해 NuGet 패키지 수 쿼리 | 

## <a name="package-push-and-unlist"></a>패키지 푸시 및 목록 제거

| API | 제한 유형 | 제한 값 | API 사용 사례 | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API 키 | 350/시간 | V2 푸시 끝점을 통해 새 NuGet 패키지 (버전) 업로드 
`/api/v2/package/{id}/{version}` **삭제** | API 키 | 250/시간 | V2 끝점을 통해 NuGet 패키지 (버전) 나열 제거 
