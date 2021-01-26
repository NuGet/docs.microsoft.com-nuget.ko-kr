---
title: NuGet 1.8 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 1.8에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8dd0fff88424c516d8b894412d07dcc53af19265
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777104"
---
# <a name="nuget-18-release-notes"></a>NuGet 1.8 릴리스 정보

[NuGet 1.7 릴리스 정보](../release-notes/nuget-1.7.md)  |  [NuGet 2.0 릴리스 정보](../release-notes/nuget-2.0.md)

NuGet 1.8은 2012 년 5 월 23 일에 출시 되었습니다.

## <a name="known-installation-issue"></a>알려진 설치 문제
VS 2010 s p 1을 실행 하는 경우 이전 버전을 설치한 경우 NuGet을 업그레이드 하려고 할 때 설치 오류가 발생할 수 있습니다.

해결 방법은 NuGet을 제거한 후 VS 확장 갤러리에서 설치 하는 것입니다.  <https://support.microsoft.com/kb/2581019>자세한 내용은를 참조 하거나 [VS 핫픽스로 직접 이동](http://bit.ly/vsixcertfix)하십시오.

참고: Visual Studio에서 확장을 제거 하는 것을 허용 하지 않는 경우 (제거 단추를 사용할 수 없음) "관리자 권한으로 실행"을 사용 하 여 Visual Studio를 다시 시작 해야 할 수도 있습니다.

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>NuGet 1.8 Windows XP와 호환 되지 않음, 게시 된 핫픽스

NuGet 1.8이 출시 되 고 나면 1.8에서 Windows XP의 사용자를 중단 하는 암호화가 변경 되는 것을 알게 되었습니다.

이후이 문제를 해결 하는 핫픽스를 출시 했습니다.  Visual Studio 확장 갤러리를 통해 NuGet을 업데이트 하면이 핫픽스를 받게 됩니다.

## <a name="features"></a>기능

### <a name="satellite-packages-for-localized-resources"></a>지역화 된 리소스에 대 한 위성 패키지
이제 NuGet 1.8은 .NET Framework의 위성 어셈블리 기능과 비슷하게 지역화 된 리소스에 대 한 별도의 패키지를 만드는 기능을 지원 합니다.  위성 패키지는 다음과 같은 몇 가지 규칙을 추가 하 여 다른 NuGet 패키지와 동일한 방식으로 만들어집니다.

* 위성 패키지 ID 및 파일 이름에는 [.NET Framework에서 사용](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)하는 표준 문화권 문자열 중 하 나와 일치 하는 접미사가 포함 되어야 합니다.
* 해당 `.nuspec` 파일에서 위성 패키지는 ID에 사용 된 것과 동일한 문화권 문자열을 사용 하 여 언어 요소를 정의 해야 합니다.
* 위성 패키지는 해당 파일의 종속성을 해당 `.nuspec` 핵심 패키지에 정의 해야 합니다 .이는 단순히 동일한 ID를 가진 패키지는 언어 접미사를 뺀 것입니다.  설치에 성공 하려면 저장소에서 핵심 패키지를 사용할 수 있어야 합니다.

지역화 된 리소스를 사용 하 여 패키지를 설치 하기 위해 개발자는 리포지토리에서 지역화 된 패키지를 명시적으로 선택 합니다. 현재 NuGet 갤러리는 위성 패키지에 어떠한 종류의 특별 한 처리도 제공 하지 않습니다.

![지역화 된 pacakges가 있는 패키지 관리자 대화 상자](./media/dlg-w-loc-packs.png)

위성 패키지에는 코어 패키지에 대 한 종속성이 나열 되므로 위성 패키지와 핵심 패키지는 모두 NuGet 패키지 폴더로 끌어오고 설치 됩니다.

![지역화 된 패키지가 있는 패키지 폴더](./media/fldr-loc-packs.png)

또한 위성 패키지를 설치 하는 동안 NuGet은 문화권 문자열 명명 규칙도 인식 한 다음 .NET Framework에서 선택할 수 있도록 지역화 된 리소스 어셈블리를 핵심 패키지 내의 올바른 하위 폴더에 복사 합니다.

![복사 된 리소스 폴더를 포함 하는 핵심 패키지 폴더](./media/fldr-copied-loc.png)

위성 패키지를 사용 하는 기존 버그 하나는 NuGet에서 `bin` 웹 사이트 프로젝트의 폴더에 지역화 된 리소스를 복사 하지 않는다는 것입니다.  이 문제는 NuGet의 다음 릴리스에서 수정 될 예정입니다.

위성 패키지를 만들고 사용 하는 방법을 보여 주는 전체 예제는를 참조 하십시오 [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample) .

### <a name="package-restore-consent"></a>패키지 복원 동의
NuGet 1.8에서는 사용자 개인 정보를 보호 하기 위해 패키지 복원에 대 한 중요 한 제약 조건을 지원 하기 위한 토대를 제공 했습니다. 이 제약 조건을 사용 하려면 패키지 복원을 사용 하는 프로젝트와 솔루션을 빌드하는 개발자가 패키지 복원의 온라인에서 패키지를 다운로드 하 여 구성 된 패키지 원본에서 패키지를 다운로드 해야 합니다.

이러한 동의를 제공 하는 방법에는 두 가지가 있습니다. 첫 번째는 아래와 같이 패키지 관리자 구성 대화 상자에서 찾을 수 있습니다.  이 메서드는 주로 개발자 컴퓨터를 대상으로 합니다.

![패키지 관리자 구성 대화 상자](./media/pr-consent-configdlg.png)

두 번째 방법은 환경 변수 "EnableNuGetPackageRestore"를 값 "true"로 설정 하는 것입니다.  이 방법은 CI 또는 빌드 서버와 같은 무인 컴퓨터를 대상으로 합니다.

이제 위에서 설명한 대로 NuGet 1.8에서이 기능에 대 한 토대를 만들었습니다.  즉,이 기능을 사용 하도록 설정 하는 모든 논리를 추가 했지만 현재이 버전에는 적용 되지 않습니다. 그러나 NuGet의 다음 릴리스에서는 사용 하도록 설정 되어 있으므로, 환경을 적절 하 게 구성할 수 있으므로 동의 제약 조건 적용을 시작할 때 영향을 받지 않도록 가능한 한 빨리이를 인식 하고자 합니다.

자세한 내용은이 기능에 대 한 [팀 블로그 게시물](http://blog.nuget.org/20120518/package-restore-and-consent.html) 을 참조 하세요.

### <a name="nugetexe-performance-improvements"></a>nuget.exe 성능 향상
설치 명령을 수정 하 여 동시에 패키지를 다운로드 하 고 설치 하면 NuGet 1.8은 확장 패키지 복원을 통해 nuget.exe 및의 성능을 크게 향상 시킬 수 있습니다.  높은 수준의 테스트는 프로젝트에 6 개의 패키지를 설치 하는 성능이 NuGet 1.8에서 약 35%까지 향상 됨을 보여 줍니다.  패키지 수를 25로 늘려도 약 60%의 성능 향상이 표시 됩니다.

## <a name="bug-fixes"></a>버그 픽스
NuGet 1.8에는 패키지 복원 동의 및 Windows 8 Express 통합과 관련 하 여 특히 패키지 관리자 콘솔과 패키지 복원 워크플로를 강조 하는 몇 가지 버그 수정이 포함 되어 있습니다.
NuGet 1.8에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)를 확인 하세요.