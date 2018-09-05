---
title: NuGet 2.2.1 릴리스 정보
description: NuGet 2.2.1 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550700"
---
# <a name="nuget-221-release-notes"></a>NuGet 2.2.1 릴리스 정보

[NuGet 2.2 릴리스 정보](../release-notes/nuget-2.2.md) | [NuGet 2.5 릴리스 정보](../release-notes/nuget-2.5.md)

NuGet 2.2.1은 2013 년 2 월 15 년에 출시 되었습니다.  VS 확장 버전 번호가 2.2.40116.9051입니다.

## <a name="localization-refresh"></a>지역화 새로 고침
Visual Studio 2012의 일부로 제공 되는 NuGet을 영어 + 13 다른 언어를 완벽 하 게 지역화 되었습니다.  그 이후로 NuGet 2.1 및 2.2 운송 하지만 지역화가 새로 고쳐지지 않습니다.  NuGet 2.2.1 릴리스 지역화를 새로 고칩니다.

NuGet의 UI 및 PowerShell 콘솔은 다음 언어로 지역화 됩니다.

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

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Visual Studio 템플릿은 여러 사전 설치 된 패키지 리포지토리를 지원합니다.
Visual Studio 서식 파일을 생성 하는 경우에 NuGet을 사용할 수 있습니다 [패키지를 사전 설치](../visual-studio-extensibility/visual-studio-templates.md) 템플릿의 일부로 합니다.  지금까지이 기능은 했습니다 제한 같은 원본에서 가져와야 하는 데 필요한 모든 패키지는 합니다.  그러나 NuGet 2.2.1 사용 하 여 여러 리포지토리 (템플릿, VSIX를 레지스트리에 정의 된 디스크의 폴더 내)에서 설치 된 패키지 있을 수 있습니다.

이 기능에 대 한 기본 시나리오는 사용자 지정 ASP.NET 프로젝트 템플릿.  기본 제공 ASP.NET 템플릿은 미리 설치 된 패키지를 로컬 디스크에서 패키지를 끌어오기를 사용 합니다.  이제 ASP.NET에 의해 설치 된 기존 패키지를 사용 하는 사용자 지정 ASP.NET 프로젝트 템플릿을 만들 수 있지만 추가 NuGet 패키지를 템플릿에 추가 합니다.

## <a name="bug-fixes"></a>버그 수정
NuGet 2.2.1 대상된 몇 가지 버그 수정을 포함합니다. 작업의 목록은 항목 고정 nuget 2.2.1 하세요 보기는 [이 릴리스의 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)합니다.


## <a name="known-issues"></a>알려진 문제

모든 사전 설치 된 패키지 저장소에 대 한 동일한 값을 사용 해야 ASP.NET 프로젝트 템플릿을 확장 하는 경우는 `isPreunzipped` 특성입니다.
