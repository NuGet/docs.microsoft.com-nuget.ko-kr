---
title: 2.7.2 NuGet 릴리스 정보
description: NuGet 2.7.2 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3e63944a05f66d5dadf17c5d4b91d3bc4478bb33
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550072"
---
# <a name="nuget-272-release-notes"></a>2.7.2 NuGet 릴리스 정보

[NuGet 2.7.1 릴리스 정보](../release-notes/nuget-2.7.1.md) | [NuGet 2.8 릴리스 정보](../release-notes/nuget-2.8.md)

2.7.2 NuGet은 2013 년 11 월 11에 출시 되었습니다.

## <a name="noteworthy-bug-fixes-and-features"></a>중요 한 버그 수정 및 기능

### <a name="license-text"></a>라이선스 텍스트
상당한 기간 동안 Microsoft가 Visual Studio에서 웹 응용 프로그램 프로젝트에 대 한 기본 템플릿의 일부로 몇 가지 인기 있는 오픈 소스 라이브러리에 대 한 NuGet 패키지를 포함 합니다. jQuery는 라이브러리의이 형식의 가장 잘 알려진 예로 때문일 수 있습니다. 제품을 함께 제공 되는 구성 요소와 관련 된 지원 계약으로 인해 패키지의 스크립트 파일은 공용 nuget.org 갤러리에 동일한 패키지에 스크립트 파일이 아닌 다른 라이선스 텍스트를 포함 합니다. 텍스트의이 차이 다양 한 콘텐츠 해시 값을 스크립트 파일은 다른 라이선스 텍스트 블록의 결과로 계속에서 패키지 업데이트를 방지할 수 있습니다 (및 따라서로 처리할지 프로젝트 내에서 수정).

이 문제를 완화 하려면 NuGet 2.7.2 같습니다는 특별히 표시 된 섹션 내에서 라이선스 텍스트 블록을 포함 하도록 스크립트 작성자를 허용 합니다.

    /************** NUGET: BEGIN LICENSE TEXT **************
     * The following code is licensed under the MIT license
     * Additional license information below is informational
     * only.
     ************** NUGET: END LICENSE TEXT ***************/

콘텐츠를 사용 하 여 패키지를 업데이트 하는 경우이 블록을 포함 하는 파일 NuGet 않습니다 하지 블록의 내용이 NuGet 갤러리에서 버전을 사용 하 여 비교에 영향 수 있으므로 삭제 하 고 원래 복사본에 일치할 것 처럼 콘텐츠 파일을 업데이트 합니다.

이 블록은 text "NUGET:: BEGIN 라이선스는 텍스트" 및 "NUGET:: END 라이선스 텍스트를" 시작 부분에서 아무 곳 이나 발생 하 고 줄 끝으로 식별 됩니다.  이 기능을 언어에 관계 없이 텍스트 파일의 모든 형식에서 사용할 수 있도록 다른 형식 지정 요구 사항이 없습니다 존재 합니다.

### <a name="add-binding-redirects-for-non-framework-assemblies"></a>에 대 한 비-프레임 워크 어셈블리 바인딩 리디렉션을 추가합니다
어셈블리의.NET Framework의 일부인 경우 NuGet 패키지를 업데이트 하는 경우 응용 프로그램의 구성 파일에 바인딩 리디렉션을 추가 건너뜁니다. 이 수정에서는 가능해 집니다 바인딩 리디렉션을 추가 되지 않았습니다 되 고 일부 어셈블리에 대 한 해당 어셈블리에는 없는 경우에 NuGet 2.7 회귀.NET Framework의 일부가 것으로 간주 합니다. NuGet 2.7.2 이전 NuGet 2.5 및 2.6 동작을 복원 및 바인딩 리디렉션을 추가 합니다.

### <a name="installing-portable-libraries-with-xamarin-tools-installed"></a>Xamarin 도구 설치를 사용 하 여 이식 가능한 라이브러리 설치
Xamarin 개발 도구가 컴퓨터에 설치 되 면 이러한 기존 대상 프레임 워크 조합과 Xamarin 프레임 워크 간의 호환성을 지정 하려면 지원 되는 프레임 워크 구성 데이터를 수정 합니다. 2.7.2 버전을 사용 하 여 NuGet은 이러한 암시적 호환성 규칙 알고 이제 있으며 따라서 쉽게 패키지에 따라서 Xamarin 호환 되지만 명시적으로 표시 하는 이식 가능한 라이브러리를 설치 하려면 Xamarin 플랫폼을 대상으로 하는 개발자를 위한 자체 메타 데이터입니다.

### <a name="machine-wide-configuration-settings-honored"></a>시스템 수준의 구성 설정 적용
계층적 Nuget.Config 파일을 사용할 경우 솔루션 루트에 가장 가까운 Nuget.Config 파일에 대 한 따르도록 repositoryPath 키 적용 되지 않았던 합니다. Visual Studio 2013, NuGet "Microsoft 및.NET" 패키지 소스를 추가 하려면 %ProgramData%\NuGet\Config\VisualStudio\12.0\Microsoft.VisualStudio.config에 사용자 지정 Nuget.Config 파일을 설치 합니다. 결과적으로 문제를 해결 하려면 솔루션에서 사용자 지정을 따르도록 repositoryPath 사용에 대 한 극히 일부의 "Microsoft 및.NET" 패키지 소스를 제거 하는 컴퓨터 수준의 Nuget.Config-삭제 했습니다. 이제 NuGet 2.7.2 계층적 Nuget.Config 파일을 사용 하는 경우 따르도록 repositoryPath에 대 한 우선 순위 규칙을 따릅니다.

## <a name="all-changes"></a>모든 변경 내용
작업의 전체 목록은 항목 고정 2.7.2, nuget에서 하세요 보기는 [이 릴리스의 NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.7.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=Fixed)합니다.
