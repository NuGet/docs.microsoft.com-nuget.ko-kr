---
title: "NuGet 1.3 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 1.3에 대 한 릴리스 정보입니다."
keywords: "NuGet 1.3 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 59169be5b39ba4436e13e0935a0ad6efa724e08e
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-13-release-notes"></a>NuGet 1.3 릴리스 정보

[NuGet 1.2 릴리스 정보](../release-notes/nuget-1.2.md) | [NuGet 1.4 릴리스 정보](../release-notes/nuget-1.4.md)

NuGet 1.3 2011 년 4 월 25 일에 출시 되었습니다.

## <a name="new-features"></a>새 기능

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>기호 서버 통합 된 간편한 패키지 만들기

NuGet 팀에서 협력 [SymbolSource.org](http://www.symbolsource.org/) 원본과 PDB의 패키지와 함께 게시 하는 매우 간단한 방법을 제공 합니다. 그러면 디버거에서 패키지에 대 한 소스 한 단계씩 패키지의 소비자가 있습니다. 자세한 내용은 참조 하세요 [만들기 및 게시 기호 패키지](../create-packages/symbol-packages.md) 소스와 NuGet 패키지를 게시 하는 쉬운 방법입니다. 라이브 데모는이 기능의 심층에서 NuGet의 일부로 Mix11에 통신도 볼 수 있습니다. 이 기능을 완벽 하 게 비디오의 20 분 지점부터 보여 줍니다.

### <a name="open-packagepage-command"></a>`Open-PackagePage`명령

이 명령을 사용 하면 쉽게 패키지 관리자 콘솔 내에서 패키지에 대 한 프로젝트 페이지에 액세스할 수 있습니다. 또한 라이선스 URL 및 패키지에 대 한 보고서 남용 페이지를 열려면 옵션을 제공 합니다.
명령 구문은 다음과 같습니다.

    Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]

`-PassThru` 옵션이 지정된 된 URL의 값을 반환 하는 데 사용 됩니다.

예를 들면 다음과 같습니다.

    PM> Open-PackagePage Ninject

Ninject 패키지에 지정 된 프로젝트 URL로 브라우저를 엽니다.

    PM> Open-PackagePage Ninject -License

Ninject 패키지에 지정 된 라이선스 URL에 대 한 브라우저를 엽니다.

    PM> Open-PackagePage Ninject -ReportAbuse

지정된 된 패키지에 대 한 신고 하는 데 사용 되는 현재 패키지 소스에서 URL로 브라우저를 엽니다.

    PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru

변수에 $url, 브라우저에서 URL을 열지 않고 라이선스 URL을 할당 합니다.

### <a name="performance-improvements"></a>성능 향상

NuGet 1.3 많은 성능 향상을 소개합니다. NuGet 1.3 사용자 단위 로컬 캐시를 포함 하 여 동일한 버전의 패키지를 여러 번 다운로드를 방지 합니다. 캐시를 액세스 하 고 패키지 관리자 설정 대화 상자를 통해 지울 수 있습니다.:

![패키지 캐시 설정 사용 하 여 NuGet 옵션 대화 상자](./media/nuget-options.png)

기타 성능 향상 등이 HTTP 압축에 대 한 지원을 추가 하기 위한 Visual Studio 내에서 패키지 설치 속도 향상 합니다.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio 및 nuget.exe 같은 패키지 소스 목록을 사용 하 여

NuGet 1.3 전에 nuget.exe와 NuGet Visual Studio 추가 기능에서 사용 하는 패키지 소스 목록 같은 위치에 저장 되지 않았습니다. 이제 NuGet 1.3 양쪽 모두에서 동일한 목록을 사용합니다. 목록에 저장 됩니다 `NuGet.Config` 응용 프로그램 데이터 폴더에 저장 합니다.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe 무시 파일 및 폴더로 시작 하는 '.' 기본적으로

NuGet Subversion, Mercurial 등의 소스 제어 시스템에서 제대로 작동 하려면 nuget.exe 무시로 시작 하는 파일과 폴더는 '.' 패키지를 만들 때 문자입니다. 두 개의 새로운 플래그를 사용 하 여 재정의할 수 있습니다.

* __-NoDefaultExcludes__ 이 설정을 무시 하 고 모든 파일을 포함 하는 데 사용 됩니다.
* __-제외__ 패턴을 사용 하 여 제외할 다른 파일/폴더를 추가 하는 데 사용 됩니다. 예를 들어, '_db_' 파일 확장명을 가진 모든 파일을 제외 하려면

```
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_참고: 패턴은 기본적으로 재귀적입니다._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>WiX 프로젝트 및.NET 마이크로 프레임 워크에 대 한 지원

커뮤니티 기여 덕분에 NuGet에 WiX 프로젝트 형식 뿐만 아니라.NET 마이크로 프레임 워크에 대 한 지원이 포함 됩니다.

## <a name="bug-fixes"></a>버그 수정

버그 수정 사항의 전체 목록을 보십시오는 [이 릴리스에 대 한 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)합니다.

## <a name="bug-fixes-worth-noting"></a>주목할 만한 버그 수정

* 소스 파일을 사용 하 여 패키지에 두 웹 사이트 및 웹 응용 프로그램 프로젝트에서 작업합니다.
웹 사이트의 경우 소스 파일에 복사 되는 `App_Code` 폴더
