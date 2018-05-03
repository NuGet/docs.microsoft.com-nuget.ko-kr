---
title: NuGet 2.2.1 릴리스 정보
description: NuGet 2.2.1 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fddeb4e8c9fb2d85ba1876360862461e8ef025af
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-221-release-notes"></a>NuGet 2.2.1 릴리스 정보

[NuGet 2.2 릴리스 정보](../release-notes/nuget-2.2.md) | [NuGet 2.5 릴리스 정보](../release-notes/nuget-2.5.md)

NuGet 2.2.1는 2013 년 2 월 15 일에 출시 되었습니다.  VS 확장 버전 번호가 2.2.40116.9051입니다.

## <a name="localization-refresh"></a>지역화 새로 고침
NuGet은 Visual Studio 2012의 일부로 제공, 완벽 하 게 영어 + 13 다른 언어에 지역화 되었습니다.  그 이후에 NuGet 2.1 및 2.2 제공 되지만 지역화가 새로 고쳐지지 않습니다.  NuGet 2.2.1 릴리스 지역화를 새로 고칩니다.

NuGet의 UI와 PowerShell 콘솔은 다음과 같은 언어로 지역화 되어 있습니다.

1. 및
1. 옵션 대신,
1. 체코어
1. 영어
1. 프랑스어
1. 독일어
1. 이탈리아어
1. 일본어
1. 한국어
1. 폴란드어
1. 포르투갈어(브라질)
1. 러시아어
1. 스페인어
1. 터키어

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Visual Studio 템플릿 여러 사전 설치 된 패키지 저장소를 지원합니다.
Visual Studio 서식 파일을 생성 하는 경우에 NuGet을 사용할 수 있습니다 [패키지를 사전 설치](../visual-studio-extensibility/visual-studio-templates.md) 서식 파일의 일부로 합니다.  지금까지이 기능에는 제한 사항이 동일한 원본에서 제공 하는 데 필요한 모든 패키지 합니다.  그러나 2.2.1 NuGet이 포함 된 서식 파일, 한 VSIX 또는 레지스트리에 정의 된 디스크의 폴더) (내 여러 저장소에서 설치 된 패키지 있을 수 있습니다.

이 기능에 대 한 주요 시나리오 ASP.NET 프로젝트 템플릿 사용자 지정입니다.  기본 제공 ASP.NET 템플릿 로컬 디스크에서 패키지를 풀링 하는 사전 설치 된 패키지를 사용 합니다.  이제 ASP.NET에서 설치 된 기존 패키지를 사용 하는 사용자 지정 ASP.NET 프로젝트 템플릿을 만들 수 있지만 서식 파일에 추가 NuGet 패키지를 추가 합니다.

## <a name="bug-fixes"></a>버그 수정
NuGet 2.2.1 대상으로 지정 된 몇 가지 버그 수정 포함 되어 있습니다. 작업 목록에 대 한 항목에서에서 수정 된 NuGet 2.2.1 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)합니다.


## <a name="known-issues"></a>알려진 문제

모든 사전 설치 된 패키지 저장소에 대 한 동일한 값을 사용 해야 ASP.NET 프로젝트 템플릿을 확장 하는 경우는 `isPreunzipped` 특성입니다.
