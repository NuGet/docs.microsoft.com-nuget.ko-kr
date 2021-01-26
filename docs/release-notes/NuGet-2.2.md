---
title: NuGet 2.2 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 2.2에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780435"
---
# <a name="nuget-22-release-notes"></a>NuGet 2.2 릴리스 정보

[NuGet 2.1 릴리스 정보](../release-notes/nuget-2.1.md)  |  [NuGet 2.2.1 릴리스 정보](../release-notes/nuget-2.2.1.md)

NuGet 2.2은 2012 년 12 월 12 일에 출시 되었습니다.

## <a name="visual-studio-quick-launch"></a>Visual Studio 빠른 실행
Visual Studio 2012에 추가 된 새로운 기능 중 하나는 [빠른 실행 대화 상자](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)입니다. NuGet 2.2은이 대화 상자를 확장 하 여 빠른 실행에 입력 된 검색 용어를 사용 하 여 패키지 관리자 대화 상자를 초기화할 수 있도록 합니다. 예를 들어 빠른 실행에서 ' jquery '를 입력 하면 이제 결과에 ' jquery '와 일치 하는 NuGet 패키지를 검색 하는 옵션이 포함 됩니다.

![Visual Studio 빠른 실행의 NuGet](./media/quick-launch.png)

이 옵션을 선택 하면 ' jquery ' 용어에 대 한 표준 NuGet 패키지 관리자 검색 환경이 시작 됩니다.

![미리 채워진 NuGet 패키지 관리자 대화 상자](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>패키지 콘텐츠에 대 한 전체 폴더 지정
이제 NuGet 2.2을 사용 하면 파일의 요소에 전체 폴더를 지정 하 여 `<file>` `.nuspec` 해당 폴더의 모든 내용을 포함할 수 있습니다. 예를 들어 다음은 패키지를 프로젝트에 설치할 때 패키지의 scripts 폴더에 있는 모든 스크립트를 contents\scripts 폴더에 추가 하는 것입니다.

```xml
<file src="scripts\" target="content\scripts"/>
```

**업데이트 6/24/16: 패키지를 설치할 때 "content" 폴더의 빈 폴더는 무시 됩니다.**

## <a name="known-issues"></a>알려진 문제

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>패키지 관리자 콘솔을 사용 하는 경우 F # 프로젝트에 대 한 패키지 설치가 실패 함
패키지 관리자 콘솔을 사용 하 여 F # 프로젝트에 NuGet 패키지를 설치 하려고 하면 InvalidOperationException이 throw 됩니다. 이 문제를 해결 하기 위해 F # 팀과 적극적으로 노력 하 고 있지만, 그 동안에는 nuget 패키지를 콘솔 대신 NuGet의 패키지 관리자 대화 상자를 통해 F # 프로젝트에 설치 하는 것이 해결 방법입니다. [자세한 내용은 CodePlex에서 확인할 수](http://nuget.codeplex.com/workitem/2873)있습니다.


## <a name="bug-fixes"></a>버그 픽스
NuGet 2.2에는 많은 버그 수정이 포함 되어 있습니다. NuGet 2.2에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)를 확인 하세요.
