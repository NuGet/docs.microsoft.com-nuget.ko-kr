---
title: NuGet 1.6 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 1.6에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08b1cb3736e645d6efcc33f920f521c9c0fc7507
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777010"
---
 # <a name="nuget-16-release-notes"></a>NuGet 1.6 릴리스 정보

[NuGet 1.5 릴리스 정보](../release-notes/nuget-1.5.md)  |  [NuGet 1.7 릴리스 정보](../release-notes/nuget-1.7.md)

NuGet 1.6은 2011 년 12 월 13 일에 출시 되었습니다.

## <a name="known-installation-issue"></a>알려진 설치 문제
VS 2010 s p 1을 실행 하는 경우 이전 버전을 설치한 경우 NuGet을 업그레이드 하려고 할 때 설치 오류가 발생할 수 있습니다.

해결 방법은 NuGet을 제거한 후 VS 확장 갤러리에서 설치 하는 것입니다.  자세한 내용은 <https://support.microsoft.com/kb/2581019>를 참조하세요.

참고: Visual Studio에서 확장을 제거 하는 것을 허용 하지 않는 경우 (제거 단추를 사용할 수 없음) "관리자 권한으로 실행"을 사용 하 여 Visual Studio를 다시 시작 해야 할 수도 있습니다.

## <a name="features"></a>기능

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>의미 체계 버전 관리 및 시험판 패키지 지원
NuGet 1.6에는 의미 체계 버전 관리 (SemVer)에 대 한 지원이 도입 되었습니다. SemVer를 사용 하는 방법에 대 한 자세한 내용은 [버전 관리 설명서](../create-packages/prerelease-packages.md)를 참조 하세요.

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>패키지를 체크 인하지 않고 NuGet 사용 (패키지 복원)
이제 NuGet 1.6에는 NuGet 패키지가 소스 제어에 추가 되지 않고 빌드 시에 복원 되는 워크플로를 위한 첫 번째 클래스 지원이 있습니다. 자세한 내용은 [소스 제어에 패키지를 커밋하지 않고 NuGet 사용](../consume-packages/packages-and-source-control.md) 항목을 참조 하세요.

### <a name="item-templates-that-install-nuget-packages"></a>NuGet 패키지를 설치 하는 항목 템플릿
Visual Studio 프로젝트 템플릿에 사전 설치 된 NuGet 패키지를 지원 하기 위한 작업을 기반으로 하는 NuGet 1.6에는 Visual Studio 항목 템플릿에 대 한 지원도 추가 됩니다. 항목 템플릿에는 템플릿이 호출 될 때 설치 되는 관련 NuGet 패키지가 있을 수 있습니다.

NuGet 패키지를 설치 하기 위해 프로젝트/항목 템플릿을 변경 하는 방법에 대 한 자세한 내용은 [Visual Studio 템플릿에서 패키지](../visual-studio-extensibility/visual-studio-templates.md) 항목을 참조 하세요.

### <a name="support-for-disabling-package-sources"></a>패키지 소스를 사용 하지 않도록 설정 지원
여러 패키지 소스가 구성 된 경우 NuGet은 패키지 및 패키지의 종속성을 설치 하는 동안 각 패키지에 대 한 패키지를 확인 합니다. 어떤 이유로 다운 된 패키지 원본의 경우 NuGet이 심각 하 게 느려질 수 있습니다.

NuGet 1.6 이전에는 패키지 원본을 제거할 수 있지만, 다시 추가 하려는 경우에 대 한 세부 정보를 기억할 수 있습니다.

NuGet 1.6은 패키지 원본에 대 한 선택을 취소 하 여 사용 하지 않도록 설정할 수 있습니다.

![패키지 비활성화](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>버그 픽스
NuGet 1.6에는 총 106 개의 작업 항목이 수정 되었습니다. 이러한 중 95는 버그로 분류 되었으며 그 중 10 개는 기능 이었습니다.

NuGet 1.6에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)를 확인 하세요.
