---
title: "NuGet 2.7.2 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: c775d1d7-de26-476c-bf9e-0cf95986a22f
description: "NuGet 2.7.2 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다."
keywords: "NuGet 2.7.2 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5bb1eb346666c5d5ee790fcdcd7d844bfd37b22e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-272-release-notes"></a>NuGet 2.7.2 릴리스 정보

[NuGet 2.7.1 릴리스 정보](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 릴리스 정보](../release-notes/nuget-2.8.md)

2.7.2 NuGet는 2013 년 11 월 11 일에 출시 되었습니다.

## <a name="noteworthy-bug-fixes-and-features"></a>주목할 만한 버그 수정 및 기능

### <a name="license-text"></a>라이선스 텍스트
상당한 기간 동안 Microsoft가 Visual Studio에서 웹 응용 프로그램 프로젝트에 대 한 기본 서식 파일의 일부로 여러 개의 인기 있는 오픈 소스 라이브러리에 대 한 NuGet 패키지를 포함 합니다. jQuery는 라이브러리에이 유형의 잘 알려진 예 때문일 수 있습니다. 제품을 함께 배달 되는 구성 요소와 관련 된 지원 계약으로 인해 패키지의 스크립트 파일이 동일한 패키지에는 공용 nuget.org 갤러리에서 확인할 스크립트 파일 보다 다른 라이선스 텍스트를 포함 합니다. 이러한 차이 텍스트에이 따라 다양 한 콘텐츠 해시 값을 스크립트 파일을 일으키는 다른 라이선스 텍스트 블록의 결과에서 패키지 업데이트를 방지할 수 (및 따라서 형태로 처리 되는 프로젝트 내에서 수정).

이 문제를 해결 하려면 NuGet 2.7.2 다음과 같이 표시 되는 특별히 표시 된 섹션 내에서 라이선스 텍스트 블록을 포함 하도록 스크립트 작성자를 수 있습니다.

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

패키지 내용으로 업데이트할 때이 블록을 포함 하는 파일 NuGet 않습니다 하지 블록의 내용을에 NuGet 갤러리에 있는 버전으로 비교 하 고 수 따라서 삭제 모아 놓은 원래 복사본 일치 인 것 처럼 콘텐츠 파일을 업데이트 합니다.

이 블록은 텍스트 "NUGET:: BEGIN 라이선스 텍스트" 및 "NUGET:: 라이선스 텍스트 끝" 시작 부분에서 아무 곳 이나 발생 및 줄 끝으로 식별 됩니다.  이 기능을 모든 종류의 언어에 관계 없이 텍스트 파일에 사용할 수 있도록 다른 서식 요구 존재 합니다.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>프레임 워크 아닌 어셈블리에 대 한 바인딩 리디렉션을 추가합니다
어셈블리의.NET Framework의 일부인 경우 NuGet 패키지를 업데이트할 때 응용 프로그램의 구성 파일에 바인딩 리디렉션을 추가 건너뜁니다. 이 수정 프로그램에서는 표현의 바인딩 리디렉션을 추가 되지 않았습니다 되 고 일부 어셈블리에 대 한 이러한 어셈블리 하지 않더라도 NuGet 2.7에서의 문제 재발에.NET Framework의 일부분으로 간주 합니다. NuGet 2.7.2 이전 NuGet 2.5 및 2.6 동작을 복원 하 고 바인딩 리디렉션을 추가 합니다.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Xamarin 도구가 설치 된 휴대용 라이브러리 설치
Xamarin 개발 도구는 컴퓨터에 설치 되 면 기존 대상 프레임 워크 조합 및 Xamarin 프레임 워크 간의 호환성을 지정 하려면 지원 되는 프레임 워크 구성 데이터 수정 합니다. 2.7.2 버전으로 NuGet은 이러한 암시적 호환성 규칙을 알고 이제 있으며 따라서 쉽게 패키지에 따라서 Xamarin 호환 되는 하지만 명시적으로 표시 하는 이식 가능한 라이브러리를 설치 하려면 Xamarin 플랫폼을 대상으로 하는 개발자를 위한 자체 메타 데이터입니다.

### <a name="machine-wide-configuration-settings-honored"></a>시스템 수준의 구성 설정 적용
Nuget.Config 파일 계층을 사용할 경우 repositoryPath 키 적용 되지 않은 것 되 고 솔루션의 루트에 가장 가까운 Nuget.Config 파일에 대 한 합니다. Visual Studio 2013에서 NuGet "Microsoft 및.NET" 패키지 소스를 추가 하기 위해 %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config에 사용자 지정 Nuget.Config 파일을 설치 합니다. 결과적으로, 해결 하는 솔루션에서 사용자 지정 repositoryPath 사용에 대 한도 제거 하는 "Microsoft 및.NET" 패키지 소스를 의미 하는 컴퓨터 수준 Nuget.Config-삭제할 했습니다. Nuget.Config 파일 계층 구조를 사용 하는 경우 NuGet 2.7.2 이제 repositoryPath에 대 한 우선 순위 규칙을 준수 합니다.

## <a name="all-changes"></a>모든 변경 내용
작업의 전체 목록은 항목에서에서 수정 된 NuGet 2.7.2, 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)합니다.
