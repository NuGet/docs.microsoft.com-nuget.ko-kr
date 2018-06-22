---
title: 속도 제한을 NuGet API
description: NuGet Api 남용 하지 않으려면 속도 제한을 강제 적용 됩니다.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: c5d3cf68ac6a96a6c14eb5e652bcf72698b6a8e8
ms.sourcegitcommit: 8f0bb8bb9cb91d27d660963ed9b0f32642f420fe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34225946"
---
# <a name="rate-limits"></a>속도 제한

NuGet.org API 남용 하지 않으려면 속도 제한 적용 합니다. 요청 속도 제한을 초과 하는 다음 오류를 반환 합니다. 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

다음 표에서 NuGet.org API에 대 한 속도 제한입니다.

## <a name="package-search"></a>패키지 검색

> [!Note]
> NuGet.org의를 사용 하는 것이 좋습니다 [V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource) 고성능 이며가 없는 있는 검색에 대 한 현재를 제한 합니다. V1 및 V2 검색 Api, followins 제한이 적용:


| API | 제한 유형 | 제한 값 | API 사용 |
|:---|:---|:---|:---|
**GET** `/api/v1/Packages` | IP | 1000 / 분 | OData v 1 통해 NuGet 패키지 메타 데이터를 쿼리 `Packages` 컬렉션 |
**GET** `/api/v1/Search()` | IP | 3000 / 분 | V1 검색 끝점을 통해 NuGet 패키지에 대 한 검색 | 
**GET** `/api/v2/Packages` | IP | 20000 / 분 | OData v 2 통해 NuGet 패키지 메타 데이터 쿼리 `Packages` 컬렉션 | 
**GET** `/api/v2/Packages/$count` | IP | 100 / 분 | NuGet 패키지 개수 v2 OData 통해 쿼리 `Packages` 컬렉션 | 

## <a name="package-push-and-unlist"></a>패키지 푸시하고 Unlist

| API | 제한 유형 | 제한 값 | API 사용 | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API 키 | 250 / 시간 | V2 푸시 끝점을 통해 새 NuGet 패키지 (버전)를 업로드 합니다. 
**삭제** `/api/v2/package/{id}/{version}` | API 키 | 250 / 시간 | Unlist v2 끝점을 통해 NuGet 패키지 (버전) 
