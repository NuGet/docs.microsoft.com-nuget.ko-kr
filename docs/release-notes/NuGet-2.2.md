---
title: NuGet 2.2 릴리스 정보
description: NuGet 2.2의 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545994"
---
# <a name="nuget-22-release-notes"></a>NuGet 2.2 릴리스 정보

[NuGet 2.1 릴리스 정보](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 릴리스 정보](../release-notes/nuget-2.2.1.md)

NuGet 2.2는 2012 년 12 월 12 일에 출시 되었습니다.

## <a name="visual-studio-quick-launch"></a>Visual Studio 빠른 실행
Visual Studio 2012에 추가 된 새로운 기능 중 하나는 [빠른 시작 대화](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)합니다. NuGet 2.2는 빠른 시작에서 입력 된 검색 용어를 사용 하 여 패키지 관리자 대화 상자를 초기화할 수 있도록이 대화 상자를 확장 합니다. 예를 들어, 이제 빠른 시작에서 'jquery' 입력 'jquery'와 일치 하는 NuGet 패키지를 검색 결과에서 옵션을 포함 합니다.

![Visual Studio 빠른 시작의 NuGet](./media/quick-launch.png)

이 옵션을 선택 하면 'jquery' 용어는 표준 NuGet 패키지 관리자 검색 환경을 시작 됩니다.

![미리 채워진된 NuGet 패키지 관리자 대화 상자](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a>패키지 내용에 대 한 전체 폴더를 지정 합니다.
NuGet 2.2 이제 지정할 수 있습니다에 전체 폴더를 `<file>` 요소의 `.nuspec` 해당 폴더의 내용을 모두 포함 하 여 파일. 예를 들어, 다음 하면 모든 스크립트 프로젝트에 패키지를 설치할 때 contents\scripts 폴더에 추가할 패키지의 스크립트 폴더에 있습니다.

```xml
<file src="scripts\" target="content\scripts"/>
```

**6 월 24/16을 업데이트 합니다: 패키지를 설치할 때 "콘텐츠" 폴더에 빈 폴더는 무시 됩니다.**

## <a name="known-issues"></a>알려진 문제

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a>패키지 관리자 콘솔을 사용 하는 경우 F # 프로젝트에 대 한 패키지 설치 실패
패키지 관리자 콘솔을 사용 하 여 F # 프로젝트에 NuGet 패키지를 설치 하려고 시도할 때, InvalidOperationException이 throw 됩니다. 적극적으로 노력 하 고 문제를 해결 하려면 F # 팀과 하지만 그동안 콘솔 대신 NuGet의 패키지 관리자 대화 상자를 통해 F # 프로젝트에 NuGet 패키지를 설치 하려면이 문제를 해결 합니다. [자세한 정보는 CodePlex에서 사용 가능한](http://nuget.codeplex.com/workitem/2873)합니다.


## <a name="bug-fixes"></a>버그 수정
NuGet 2.2에는 여러 버그 수정을 포함 합니다. 작업의 전체 목록은 항목 고정 NuGet 2.2에서 하세요 보기는 [이 릴리스의 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)합니다.
