---
title: 속도 제한, NuGet API
description: 속도 제한 남용을 방지 하기 위해 NuGet Api을 강제 적용 됩니다.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548679"
---
# <a name="rate-limits"></a>속도 제한

NuGet.org API 남용을 방지 하기 위해 속도 제한을 적용 합니다. 요청 속도 제한을 초과 하는 다음 오류를 반환 합니다. 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

요청 속도 제한을 사용 하 여 제한 하는 것 외에도 일부 Api도 할당량을 적용 합니다. 다음 오류를 반환 하는 할당량을 초과 하는 요청:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

다음 표에서 NuGet.org API에 대 한 속도 제한 합니다.

## <a name="package-search"></a>패키지 검색

> [!Note]
> NuGet.org의를 사용 하는 것이 좋습니다 [V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource) 현재 검색 성능이 없는 제한 합니다. V1 및 V2에 대 한 검색 Api, followins 제한이 적용 됩니다.


| API | 제한 유형 | 제한 값 | API 사용 |
|:---|:---|:---|:---|
**GET** `/api/v1/Packages` | IP | 1000 / 분 | V1 OData 통해 NuGet 패키지 메타 데이터를 쿼리하여 `Packages` 컬렉션 |
**GET** `/api/v1/Search()` | IP | 3000 / 분 | V1 검색 끝점을 통해 NuGet 패키지 검색 | 
**GET** `/api/v2/Packages` | IP | 20000 / 분 | V2 OData 통해 NuGet 패키지 메타 데이터를 쿼리하여 `Packages` 컬렉션 | 
**GET** `/api/v2/Packages/$count` | IP | 100 / 분 | NuGet 패키지 개수 v2 OData 통해 쿼리 `Packages` 컬렉션 | 

## <a name="package-push-and-unlist"></a>패키지의 나열을 취소 하 고 푸시

| API | 제한 유형 | 제한 값 | API 사용 | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API 키 | 250 / 시간 | V2 푸시 끝점을 통해 새 NuGet 패키지 (버전)를 업로드 합니다. 
**DELETE** `/api/v2/package/{id}/{version}` | API 키 | 250 / 시간 | V2 끝점을 통해 NuGet 패키지 (버전)를 나열 합니다. 
