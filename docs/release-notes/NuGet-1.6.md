---
title: NuGet 1.6 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함 하 여 NuGet 1.6에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549014"
---
 # <a name="nuget-16-release-notes"></a>NuGet 1.6 릴리스 정보

[NuGet 1.5 릴리스](../release-notes/nuget-1.5.md) | [NuGet 1.7 릴리스 정보](../release-notes/nuget-1.7.md)

NuGet 1.6은 2011 년 12 월 13 일에 출시 되었습니다.

## <a name="known-installation-issue"></a>알려진된 설치 문제
VS 2010 SP1을 실행 하는 경우 이전 버전이 설치 되어 있는 경우 NuGet을 업그레이드 하려고 할 때 설치 오류를 실행할 수 있습니다.

해결 방법은 NuGet 제거한 다음 VS 확장 갤러리에서 설치 하는 것입니다.  자세한 내용은 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)를 참조하세요.

참고: Visual Studio (제거 단추 사용 안 함) 확장을 제거할 수 없습니다, 다음 가능성이 높은 경우 "관리자 권한으로 실행"을 사용 하 여 Visual Studio를 다시 시작

## <a name="features"></a>기능

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>유의 적 버전 및 시험판 패키지에 대 한 지원
NuGet 1.6에는 유의 적 버전 (SemVer)에 대 한 지원이 도입 되었습니다. SemVer를 사용 하는 방법에 대 한 자세한 내용은 참조는 [버전 관리 설명서](../create-packages/prerelease-packages.md)합니다.

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>NuGet을 사용 하 여 패키지 (패키지 복원)를 체크 인하지 않고
이제 NuGet 1.6는 워크플로 nuget에서 패키지를 소스 제어에 추가 되지 않습니다 하지만 대신 복원 됩니다 빌드 시 누락 된 경우 첫 번째 클래스 지원 합니다. 자세한 내용은 참조는 [소스 제어에 패키지를 커밋하지 않고 NuGet을 사용 하 여](../consume-packages/packages-and-source-control.md) 항목.

### <a name="item-templates-that-install-nuget-packages"></a>NuGet 패키지를 설치 하는 항목 템플릿
Visual Studio 프로젝트 템플릿에 미리 설치 된 NuGet 패키지를 지원 하도록 작업을 토대로, NuGet 1.6 추가 Visual Studio 항목 템플릿 지원 합니다. 항목 템플릿을 NuGet 패키지에서 템플릿을 호출할 때 설치 되는 연결 될 수 있습니다.

NuGet 패키지를 설치 하는 프로젝트/항목 템플릿을 변경 하는 방법에 대 한 자세한 내용은 참조는 [Visual Studio 템플릿의 패키지](../visual-studio-extensibility/visual-studio-templates.md) 항목입니다.

### <a name="support-for-disabling-package-sources"></a>패키지 소스를 사용 하지 않도록 설정 하는 것에 대 한 지원
여러 패키지 소스를 구성 하면 패키지 및 해당 종속성의 설치 중 NuGet 패키지에 대 한 각각 살펴보겠습니다. 어떤 이유로 든 느려질 수 있다는 심각 하 게 NuGet에 대 한 아래에 있는 패키지 소스입니다.

NuGet 1.6 이전 패키지 소스를 제거할 수 있습니다 하지만 추가 하려는 경우에 대 한 세부 정보를 다시 저장 해야 합니다.

NuGet 1.6을 사용 하지 않도록 설정 하지만 유지 하는 패키지 원본 선택을 취소를 허용 합니다.

![패키지를 사용 하지 않도록 설정](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>버그 수정
NuGet 1.6 106의 총 작업 항목을 고정 했습니다. 그 중 95 버그 기밀로 분류 된 있었으며 해당 10 개 기능.

작업의 전체 목록은 항목 고정 NuGet 1.6에서 하세요 보기는 [이 릴리스의 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)합니다.
