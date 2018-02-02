---
title: "NuGet 1.7 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 1.7에 대 한 릴리스 정보입니다."
keywords: "NuGet 1.7 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7b16bea8c6bcc77f814dd32a43b895b5e656c95d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-17-release-notes"></a>NuGet 1.7 릴리스 정보

[NuGet 1.6 릴리스 정보](../release-notes/nuget-1.6.md) | [NuGet 1.8 릴리스 정보](../release-notes/nuget-1.8.md)

NuGet 1.7은 2012 년 4 월 4 일에 출시 되었습니다.

## <a name="known-installation-issue"></a>알려진된 설치 문제
VS 2010 s p 1을 실행 하는 경우 이전 버전이 설치 되어 있는 경우 NuGet을 업그레이드 하는 동안 설치 오류에 실행할 수 있습니다.

해결 하려면 NuGet 제거한 다음 VS 확장 갤러리에서 설치 됩니다.  자세한 내용은 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)를 참조하세요.

참고: Visual Studio 확장 (제거 단추 사용 안 함)을 제거 하도록 허용 하지, 한 후 가능성 하면 "관리자 권한으로 실행"을 사용 하 여 Visual Studio를 다시 시작

## <a name="features"></a>기능

### <a name="support-opening-readmetxt-file-after-installation"></a>설치 후 readme.txt 파일 열기만 지원
패키지에 포함 된 경우 1.7의 새로운는 `readme.txt` 패키지 설치를 완료 한 후 파일 NuGet 패키지의 루트에서이 파일은 자동으로 열립니다.

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a>시험판 패키지를 관리 하는 NuGet 패키지 대화 상자 표시
NuGet 패키지 관리 대화 상자에 시험판 패키지를 표시 하려면 옵션을 제공 하는 드롭다운 이제 포함 됩니다.

![시험판 패키지를 표시합니다.](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a>패키지 파일이 없는 경우 패키지를 복원 단추를 표시 합니다.
패키지 관리자 콘솔을 열면 또는 관리자 NuGet 패키지 대화 상자, NuGet은 현재 솔루션 패키지 복원 모드를 활성화 하는 경우를 확인 하 고 패키지 파일에서 누락 된 경우는 `packages` 폴더입니다. 이러한 두 조건이 충족 되 면 NuGet에서 알려 고 편리 하 게 복원 단추가 표시 됩니다. 이 단추를 클릭 하면 NuGet이 누락 된 모든 패키지를 복원 하도록 트리거할 수 있습니다.

![대화 상자에서 패키지 복원 단추](./media/packagerestore-dialog.png)

![콘솔에서 패키지 복원 단추](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a>솔루션 수준 packages.config 파일 추가
NuGet의 이전 버전에서는 각 프로젝트에는 `packages.config` 파일 추적 하는 NuGet 패키지는 해당 프로젝트에 설치 됩니다. 그러나 솔루션 수준의 패키지를 추적 하기 위해 솔루션 수준에서 비슷한 파일이 없습니다. 했습니다. 결과적으로, 방법이 수준 솔루션 패키지를 복원 했습니다.
이 기능은 NuGet 1.7에서 구현 됩니다. 솔루션 수준 `packages.config` 아래 파일에 저장 됩니다는 `.nuget` 솔루션 아래에 폴더 루트 및는 솔루션 수준의 패키지를 저장 합니다.

### <a name="remove-new-package-command"></a>새 패키지 명령 제거
낮은 사용으로 인해 새 패키지 명령이 제거 되었습니다. 개발자는 nuget.exe 또는 편리한 NuGet 패키지 탐색기 패키지를 만드는 데 사용 하는 것이 좋습니다.

## <a name="bug-fixes"></a>버그 수정
NuGet 1.7는 패키지를 복원 하는 워크플로 및 네트워크/소스 제어 시나리오 많은 버그를 수정 합니다.

작업의 전체 목록은 항목에서에서 수정 된 NuGet 1.7 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)합니다.
