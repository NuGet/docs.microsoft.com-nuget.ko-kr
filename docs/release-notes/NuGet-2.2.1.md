---
title: NuGet 2.2.1 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 2.2.1를 포함 하는 NuGet에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776807"
---
# <a name="nuget-221-release-notes"></a>NuGet 2.2.1 릴리스 정보

[NuGet 2.2 릴리스 정보](../release-notes/nuget-2.2.md)  |  [NuGet 2.5 릴리스 정보](../release-notes/nuget-2.5.md)

NuGet 2.2.1는 2013 년 2 월 15 일에 출시 되었습니다.  VS 확장 버전 번호는 2.2.40116.9051입니다.

## <a name="localization-refresh"></a>지역화 새로 고침
NuGet은 Visual Studio 2012의 일부로 제공 될 때 영어 + 13 기타 언어로 완전히 지역화 되었습니다.  그 이후에는 NuGet 2.1 및 2.2이 제공 되었지만 지역화를 새로 고치지 않았습니다.  NuGet 2.2.1 릴리스는 지역화를 새로 고칩니다.

NuGet의 UI 및 PowerShell 콘솔은 다음 언어로 지역화 됩니다.

1. 중국어(간체)
1. 중국어(번체)
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

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Visual Studio 템플릿은 미리 설치 된 여러 패키지 리포지토리를 지원 합니다.
Visual Studio 템플릿을 생성 하는 경우 NuGet을 사용 하 여 템플릿의 일부로 [패키지를 사전 설치할](../visual-studio-extensibility/visual-studio-templates.md) 수 있습니다.  지금 까지는이 기능에 모든 패키지가 동일한 소스에서 제공 되어야 한다는 제한이 있었습니다.  그러나 NuGet 2.2.1을 사용 하면 템플릿, VSIX 또는 레지스트리에 정의 된 디스크의 폴더에 있는 여러 리포지토리에서 패키지를 설치할 수 있습니다.

이 기능의 주요 시나리오는 사용자 지정 ASP.NET 프로젝트 템플릿입니다.  기본 제공 ASP.NET 템플릿은 미리 설치 된 패키지를 사용 하 여 로컬 디스크에서 패키지를 끌어옵니다.  이제 ASP.NET에 의해 설치 된 기존 패키지를 사용 하지만 템플릿에 추가 NuGet 패키지를 추가 하는 사용자 지정 ASP.NET 프로젝트 템플릿을 만들 수 있습니다.

## <a name="bug-fixes"></a>버그 픽스
NuGet 2.2.1에는 몇 가지 대상 버그 수정이 포함 되어 있습니다. NuGet 2.2.1에서 수정 된 작업 항목 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)를 확인 하세요.


## <a name="known-issues"></a>알려진 문제

ASP.NET 프로젝트 템플릿을 확장 하는 경우 사전 설치 된 모든 패키지 리포지토리는 특성에 대해 동일한 값을 사용 해야 합니다 `isPreunzipped` .
