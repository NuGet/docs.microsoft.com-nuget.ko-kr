---
title: NuGet 2.2 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 2.2에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 21f212de53da5faf1ec0762f97a840968b615b19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-22-release-notes"></a>NuGet 2.2 릴리스 정보

[NuGet 2.1 릴리스 정보](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 릴리스 정보](../release-notes/nuget-2.2.1.md)

NuGet 2.2는 2012 년 12 월 12 일에 출시 되었습니다.

## <a name="visual-studio-quick-launch"></a>Visual Studio 빠른 실행
Visual Studio 2012에서 추가 된 새로운 기능 중 하나인는 [빠른 실행 대화](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)합니다. NuGet 2.2 하므로 검색어를 빠른 실행에서 입력 한 패키지 관리자 대화 상자를 초기화 하는이 대화 상자에서을 확장 합니다. 예를 들어, 빠른 실행에서 이제 'jquery'를 입력 'jquery'와 일치 하는 NuGet 패키지를 검색 하 고 결과에 옵션을 포함 합니다.

![Visual Studio 빠른 실행에서 NuGet](./media/quick-launch.png)

이 옵션을 선택 하면 표준 NuGet 패키지 관리자 검색 환경을 'jquery' 용어에 대 한 시작 됩니다.

![미리 채워진된 NuGet 패키지 관리자 대화 상자](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>패키지 내용에 대 한 전체 폴더를 지정 합니다.
NuGet 2.2 이제 지정할 수 있습니다에 전체 폴더는 `<file>` 의 요소는 `.nuspec` 파일의 모든 해당 폴더의 내용을 포함 하도록 합니다. 예를 들어 다음로 인해 모든 스크립트의 패키지의 스크립트 폴더를 프로젝트에 패키지를 설치할 때 contents\scripts 폴더에 추가할 수 있습니다.

```xml
<file src="scripts\" target="content\scripts"/>
```

**업데이트 6/24/16: 패키지를 설치 하는 경우 "content" 폴더에 빈 폴더는 무시 됩니다.**

## <a name="known-issues"></a>알려진 문제

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>F # 프로젝트에 대 한 패키지 관리자 콘솔을 사용 하는 경우 패키지 설치에 실패
패키지 관리자 콘솔을 사용 하 여 F # 프로젝트에 NuGet 패키지 설치을 시도할 때 InvalidOperationException 발생 throw 됩니다. 문제를 해결 하려면 F # 팀과 함께 최선을 다 하지만 해결 방법은 콘솔 대신 NuGet 패키지 관리자 대화 상자를 통해 F # 프로젝트에 NuGet 패키지를 설치 하는 한편, 합니다. [자세한 정보는 CodePlex에서 사용 가능한](http://nuget.codeplex.com/workitem/2873)합니다.


## <a name="bug-fixes"></a>버그 수정
NuGet 2.2에는 많은 버그 수정 포함 되어 있습니다. 작업의 전체 목록은 항목 고정 NuGet 2.2에서 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)합니다.
