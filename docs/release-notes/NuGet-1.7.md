---
title: NuGet 버전 1.7 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함 하 여 NuGet 1.7에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 07cd541ef215d2a1bacc45995a22dadb6dfeac6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551469"
---
# <a name="nuget-17-release-notes"></a>NuGet 버전 1.7 릴리스 정보

[NuGet 1.6 릴리스 정보](../release-notes/nuget-1.6.md) | [NuGet 1.8 릴리스 정보](../release-notes/nuget-1.8.md)

NuGet 1.7은 2012 년 4 월 4 일에 출시 되었습니다.

## <a name="known-installation-issue"></a>알려진된 설치 문제
VS 2010 SP1을 실행 하는 경우 이전 버전이 설치 되어 있는 경우 NuGet을 업그레이드 하려고 할 때 설치 오류를 실행할 수 있습니다.

해결 방법은 NuGet 제거한 다음 VS 확장 갤러리에서 설치 하는 것입니다.  자세한 내용은 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)를 참조하세요.

참고: Visual Studio (제거 단추 사용 안 함) 확장을 제거할 수 없습니다, 다음 가능성이 높은 경우 "관리자 권한으로 실행"을 사용 하 여 Visual Studio를 다시 시작

## <a name="features"></a>기능

### <a name="support-opening-readmetxt-file-after-installation"></a>설치 후 readme.txt 파일을 열고 지원
패키지에 포함 된 경우 1.7의 새로운는 `readme.txt` NuGet 패키지의 루트에 있는 파일 패키지를 설치한 완료 된 후이 파일을 엽니다 자동으로 됩니다.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>시험판 패키지를 관리 하는 NuGet 패키지 대화 상자에서 표시
이제 NuGet 패키지 관리 대화 상자에는 시험판 패키지를 표시 하는 옵션을 제공 하는 드롭다운 포함 됩니다.

![시험판 패키지 표시](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>패키지 파일이 없는 경우 패키지 복원 단추를 표시 합니다.
패키지 관리자 콘솔을 열면 또는 Manager NuGet 패키지 대화 상자, NuGet 패키지 복원 모드를 현재 솔루션에 설정한 경우 확인 하 고 모든 패키지 파일에서 누락 된 경우는 `packages` 폴더입니다. 이러한 두 조건이 충족 될 경우 NuGet 알려 고 편리 하 게 복원 단추가 표시 됩니다. 이 단추를 클릭 하면 누락 된 모든 패키지를 복원 하도록 NuGet에 트리거할 수 있습니다.

![대화 상자에서 패키지 복원 단추](./media/packagerestore-dialog.png)

![콘솔에서 패키지 복원 단추](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>솔루션 수준 packages.config 파일 추가
각 프로젝트에 NuGet의 이전 버전을 `packages.config` 파일 추적 하는 NuGet 패키지는 해당 프로젝트에 설치 됩니다. 그러나 솔루션 수준 패키지를 추적 하는 솔루션 수준에서 비슷한 파일이 없는 했습니다. 결과적으로 솔루션 수준 패키지를 복원 하려면 방법이 없었습니다.
이 기능은 NuGet 1.7에서 구현 됩니다. 솔루션 수준의 `packages.config` 파일 아래에 배치 됩니다는 `.nuget` 솔루션 아래에 폴더 루트 및 솔루션 수준 패키지를 저장 합니다.

### <a name="remove-new-package-command"></a>새로 만들기-Package 명령 제거
낮은 사용량으로 인 한 새 패키지 명령을 제거 되었습니다. 개발자는 nuget.exe 또는 유용한 NuGet 패키지 탐색기 패키지를 만드는 데 사용 하는 것이 좋습니다.

## <a name="bug-fixes"></a>버그 수정
NuGet 1.7은 워크플로 패키지 복원 및 네트워크/소스 제어 시나리오에 대 한 많은 버그가 수정 합니다.

작업의 전체 목록은 항목에서에서 수정 된 NuGet 1.7 하세요 보기는 [이 릴리스의 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)합니다.
