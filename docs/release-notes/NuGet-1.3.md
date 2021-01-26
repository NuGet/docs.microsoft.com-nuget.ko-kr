---
title: NuGet 1.3 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 1.3에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 54eda149352810eacc1d6340ad16cec1b03194e3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777124"
---
# <a name="nuget-13-release-notes"></a>NuGet 1.3 릴리스 정보

[NuGet 1.2 릴리스 정보](../release-notes/nuget-1.2.md)  |  [NuGet 1.4 릴리스 정보](../release-notes/nuget-1.4.md)

NuGet 1.3은 2011 년 4 월 25 일에 출시 되었습니다.

## <a name="new-features"></a>새로운 기능

### <a name="streamlined-package-creation-with-symbol-server-integration"></a>기호 서버 통합으로 간소화 된 패키지 만들기

NuGet 팀은 [SymbolSource.org](http://www.symbolsource.org/) 의 담당자와 협력 하 여 패키지와 함께 원본 및 PDB를 게시 하는 매우 간단한 방법을 제공 합니다. 이렇게 하면 패키지의 소비자가 디버거에서 패키지에 대 한 소스를 한 단계씩 실행 하도록 할 수 있습니다. 자세한 내용은 [기호 패키지 만들기 및 게시](../create-packages/symbol-packages.md) 를 참조 하세요. 소스를 사용 하 여 NuGet 패키지를 쉽게 게시할 수 있습니다. Mix11에서 심층 통신에서 NuGet의 일부로이 기능의 라이브 데모를 시청 할 수도 있습니다. 이 기능은 비디오의 20 분 표시부터 자세히 설명 합니다.

### <a name="open-packagepage-command"></a>`Open-PackagePage` 명령

이 명령을 사용 하면 패키지 관리자 콘솔 내에서 패키지에 대 한 프로젝트 페이지를 쉽게 가져올 수 있습니다. 또한 패키지에 대 한 라이선스 URL 및 보고서 신고 페이지를 여는 옵션을 제공 합니다.
명령의 구문은 다음과 같습니다.

```
Open-PackagePage -Id <string> [-Version] [-Source] [-License] [-ReportAbuse] [-PassThru]
```

`-PassThru`옵션은 지정 된 URL의 값을 반환 하는 데 사용 됩니다.

예제:

```
PM> Open-PackagePage Ninject
```

Ninject 패키지에 지정 된 프로젝트 URL에 대 한 브라우저를 엽니다.

```
PM> Open-PackagePage Ninject -License
```

Ninject 패키지에 지정 된 라이선스 URL에 대 한 브라우저를 엽니다.

```
PM> Open-PackagePage Ninject -ReportAbuse
```

지정 된 패키지에 대 한 남용을 보고 하는 데 사용 되는 현재 패키지 원본에서 URL에 대 한 브라우저를 엽니다.

```
PM> $url = Open-PackagePage Ninject -License -WhatIf -PassThru
```

브라우저에서 URL을 열지 않고 $url 변수에 라이선스 URL을 할당 합니다.

### <a name="performance-improvements"></a>성능 향상

NuGet 1.3에는 다양 한 성능 향상이 도입 되었습니다. NuGet 1.3은 로컬 사용자별 캐시를 포함 하 여 동일한 버전의 패키지를 여러 번 다운로드 하는 것을 방지 합니다. 캐시는 패키지 관리자 설정 대화 상자를 통해 액세스 하 고 지울 수 있습니다.

![패키지 캐시 설정을 사용 하는 NuGet 옵션 대화 상자](./media/nuget-options.png)

기타 성능 향상으로는 HTTP 압축에 대 한 지원을 추가 하 고 Visual Studio 내에서 패키지 설치 속도를 향상 시킬 수 있습니다.

### <a name="visual-studio-and-nugetexe-uses-the-same-list-of-package-sources"></a>Visual Studio 및 nuget.exe는 동일한 패키지 소스 목록을 사용 합니다.

NuGet 1.3 이전에는 nuget.exe 및 NuGet Visual Studio Add-In에서 사용 하는 패키지 소스 목록이 동일한 장소에 저장 되지 않았습니다. 이제 NuGet 1.3은 두 위치에서 동일한 목록을 사용 합니다. 목록은 AppData 폴더에 저장 되어 `NuGet.Config` 저장 됩니다.

### <a name="nugetexe-ignores-files-and-folders-that-start-with--by-default"></a>nuget.exe은 기본적으로 '. '로 시작 하는 파일 및 폴더를 무시 합니다.

Subversion 및 Mercurial와 같은 소스 제어 시스템에서 NuGet이 잘 작동 하도록 하기 위해 패키지를 만들 때 '. ' 문자로 시작 하는 폴더와 파일은 무시 nuget.exe. 이는 두 개의 새 플래그를 사용 하 여 재정의할 수 있습니다.

* __-NoDefaultExcludes__ 는이 설정을 재정의 하 고 모든 파일을 포함 하는 데 사용 됩니다.
* __-Exclude__ 는 패턴을 사용 하 여 제외할 다른 파일/폴더를 추가 하는 데 사용 됩니다. 예를 들어 ' .bak ' 파일 확장명을 가진 모든 파일을 제외 하려면

```cli
nuget Pack MyPackage.nuspec -Exclude **\*.bak
```  

_참고: 기본적으로이 패턴은 재귀적이 아닙니다._

### <a name="support-for-wix-projects-and-the-net-micro-framework"></a>WiX 프로젝트 및 .NET 마이크로 프레임 워크에 대 한 지원

커뮤니티 참여 덕분에 NuGet은 .NET 마이크로 프레임 워크 뿐만 아니라 WiX 프로젝트 형식에 대 한 지원도 포함 합니다.

## <a name="bug-fixes"></a>버그 픽스

버그 수정의 전체 목록은 [이 릴리스에 대 한 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.3&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)를 확인 하세요.

## <a name="bug-fixes-worth-noting"></a>버그 수정 가치가 있습니다.

* 원본 파일이 포함 된 패키지는 웹 사이트와 웹 응용 프로그램 프로젝트 모두에서 작동 합니다.
웹 사이트의 경우 원본 파일이 폴더로 복사 됩니다. `App_Code`
