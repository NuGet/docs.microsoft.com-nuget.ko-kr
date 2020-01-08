---
title: NuGet 1.7 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 1.7에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a98da76038582202396c8da96f8eae166e6096f6
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383321"
---
# <a name="nuget-17-release-notes"></a>NuGet 1.7 릴리스 정보

Nuget [1.6 릴리스 정보](../release-notes/nuget-1.6.md) | [Nuget 1.8 릴리스 정보](../release-notes/nuget-1.8.md)

NuGet 1.7은 2012 4 월 4 일에 출시 되었습니다.

## <a name="known-installation-issue"></a>알려진 설치 문제
VS 2010 s p 1을 실행 하는 경우 이전 버전을 설치한 경우 NuGet을 업그레이드 하려고 할 때 설치 오류가 발생할 수 있습니다.

해결 방법은 NuGet을 제거한 후 VS 확장 갤러리에서 설치 하는 것입니다.  자세한 내용은 <https://support.microsoft.com/kb/2581019>를 참조하세요.

참고: Visual Studio에서 확장을 제거 하는 것을 허용 하지 않는 경우 (제거 단추를 사용할 수 없음) "관리자 권한으로 실행"을 사용 하 여 Visual Studio를 다시 시작 해야 할 수도 있습니다.

## <a name="features"></a>기능

### <a name="support-opening-readmetxt-file-after-installation"></a>설치 후 readme.txt 파일 열기 지원
1\.7의 새로운 기능으로, 패키지의 루트에 `readme.txt` 파일을 포함 하는 경우 NuGet은 패키지 설치를 완료 한 후이 파일을 자동으로 엽니다.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>NuGet 패키지 관리 대화 상자에 시험판 패키지 표시
이제 NuGet 패키지 관리 대화 상자에는 시험판 패키지를 표시 하는 옵션을 제공 하는 드롭다운이 포함 되어 있습니다.

![시험판 패키지 표시](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>패키지 파일이 없는 경우 패키지 복원 단추 표시
패키지 관리자 콘솔 또는 관리자 NuGet 패키지 대화 상자를 열면 NuGet은 현재 솔루션이 패키지 복원 모드를 사용 하도록 설정 했는지 여부와 `packages` 폴더에 패키지 파일이 누락 되었는지 확인 합니다. 이러한 두 조건이 충족 되는 경우 NuGet은 사용자에 게 알리고 편리한 복원 단추를 표시 합니다. 이 단추를 클릭 하면 누락 된 모든 패키지를 복원 하는 NuGet이 트리거됩니다.

![대화 상자의 패키지 복원 단추](./media/packagerestore-dialog.png)

![콘솔의 패키지 복원 단추](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>솔루션 수준 패키지 .config 파일 추가
이전 버전의 NuGet에서 각 프로젝트에는 해당 프로젝트에 설치 된 NuGet 패키지를 추적 하는 `packages.config` 파일이 있습니다. 그러나 솔루션 수준 패키지를 추적할 수 있는 유사한 파일이 솔루션 수준에 없습니다. 따라서 솔루션 수준 패키지를 복원할 수 있는 방법이 없습니다.
이 기능은 이제 NuGet 1.7에서 구현 됩니다. 솔루션 수준 `packages.config` 파일은 솔루션 루트의 `.nuget` 폴더 아래에 배치 되며 솔루션 수준 패키지만 저장 합니다.

### <a name="remove-new-package-command"></a>새 패키지 제거 명령
낮은 사용량으로 인해 새 패키지 명령이 제거 되었습니다. 개발자는 nuget.exe 또는 편리한 NuGet 패키지 탐색기를 사용 하 여 패키지를 만드는 것이 좋습니다.

## <a name="bug-fixes"></a>버그 수정
NuGet 1.7은 패키지 복원 워크플로 및 네트워크/원본 제어 시나리오에 대 한 많은 버그를 수정 했습니다.

NuGet 1.7에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)를 확인 하세요.
