---
title: "NuGet 1.6 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 1.6에 대 한 릴리스 정보입니다."
keywords: "NuGet 1.6 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 114b03cede24dee520ace1d8aa920a648ad16af1
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
 # <a name="nuget-16-release-notes"></a>NuGet 1.6 릴리스 정보

[NuGet 1.5 릴리스 정보](../release-notes/nuget-1.5.md) | [NuGet 1.7 릴리스 정보](../release-notes/nuget-1.7.md)

NuGet 1.6 2011 년 12 월 13 일에 출시 되었습니다.

## <a name="known-installation-issue"></a>알려진된 설치 문제
VS 2010 s p 1을 실행 하는 경우 이전 버전이 설치 되어 있는 경우 NuGet을 업그레이드 하는 동안 설치 오류에 실행할 수 있습니다.

해결 하려면 NuGet 제거한 다음 VS 확장 갤러리에서 설치 됩니다.  자세한 내용은 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)를 참조하세요.

참고: Visual Studio 확장 (제거 단추 사용 안 함)을 제거 하도록 허용 하지, 한 후 가능성 하면 "관리자 권한으로 실행"을 사용 하 여 Visual Studio를 다시 시작

## <a name="features"></a>기능

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>의미 체계 버전 관리 및 시험판 패키지에 대 한 지원
NuGet 1.6 의미 체계 버전 관리 (SemVer)에 대 한 지원이 도입 되었습니다. SemVer를 사용 하는 방법에 대 한 자세한 내용은 참조는 [버전 관리 설명서](../create-packages/prerelease-packages.md)합니다.

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>NuGet을 사용 하 여 패키지 (패키지 복원)에서 확인 하지 않고
NuGet 1.6에는 NuGet 패키지 소스 제어에 추가 되지 않습니다 되지만 대신은 복원 빌드 시 누락 된 경우 워크플로 위한 최고 수준의 지원도 되었습니다. 자세한 내용은 참조 하세요는 [를 사용 하 여 NuGet 패키지를 소스 제어에 커밋하지 않고](../consume-packages/packages-and-source-control.md) 항목입니다.

### <a name="item-templates-that-install-nuget-packages"></a>NuGet 패키지를 설치 하는 항목 템플릿
Visual Studio 항목 템플릿에 대 한 지원을 NuGet 1.6에서 또한 추가 Visual Studio 프로젝트 템플릿 사전 설치 된 NuGet 패키지를 지원 하도록 작업을 작성 합니다. 항목 템플릿에서 서식 파일에서 호출 될 때 설치 된 NuGet 패키지에 연결할 수 있습니다.

NuGet 패키지를 설치 하는 프로젝트/항목 템플릿을 변경 하는 방법에 대 한 자세한 내용은 참조는 [에서 Visual Studio 템플릿 패키지](../visual-studio-extensibility/visual-studio-templates.md) 항목입니다.

### <a name="support-for-disabling-package-sources"></a>패키지 소스를 사용 하지 않도록 설정 하는 것에 대 한 지원
여러 패키지 소스를 구성 하면 NuGet 패키지 및 해당 종속성을 설치 하는 동안에 각 패키지에 대 한 표시 됩니다. 어떤 이유로 든 느려질 수 있다는 심각 하 게 NuGet에 대 한 아래에 있는 패키지 소스입니다.

NuGet 1.6 이전 패키지 소스를 제거할 수 있지만 기억 추가 하려는 경우에 대 한 세부 정보를 다시 제공 해야 합니다.

NuGet 1.6을 사용 하지 않도록 설정 하 고 유지 한 패키지 소스를 선택 취소 하면 수 있습니다.

![패키지를 사용 하지 않도록 설정](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>버그 수정
NuGet 1.6 106의 총 작업 항목을 고정 했습니다. 그 중 95 버그로 분류 된 되었고 그 중 10 기능.

작업의 전체 목록은 항목에서에서 수정 된 NuGet 1.6 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)합니다.
