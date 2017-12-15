---
title: "NuGet 1.8 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: e694ee1a-fe4c-4397-8d0a-7336be4dfebe
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 1.8에 대 한 릴리스 정보입니다."
keywords: "NuGet 1.8 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 875cb752fed102c24da255a336d3f16729ca082c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-18-release-notes"></a>NuGet 1.8 릴리스 정보

[NuGet 1.7 릴리스 정보](../release-notes/nuget-1.7.md) | [NuGet 2.0 릴리스 정보](../release-notes/nuget-2.0.md)

NuGet 1.8은 2012 년 5 월 23 일에 출시 되었습니다.

## <a name="known-installation-issue"></a>알려진된 설치 문제
VS 2010 s p 1을 실행 하는 경우 이전 버전이 설치 되어 있는 경우 NuGet을 업그레이드 하는 동안 설치 오류에 실행할 수 있습니다.

해결 하려면 NuGet 제거한 다음 VS 확장 갤러리에서 설치 됩니다.  참조 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) 자세한 내용은 또는 [VS 핫픽스로 직접 이동](http://bit.ly/vsixcertfix)합니다.

참고: Visual Studio 확장 (제거 단추 사용 안 함)을 제거 하도록 허용 하지, 한 후 가능성 하면 "관리자 권한으로 실행"을 사용 하 여 Visual Studio를 다시 시작

## <a name="nuget-18-incompatible-with-windows-xp-hotfix-published"></a>Windows XP와 NuGet 1.8 호환 되지 않는 게시 하는 핫픽스

NuGet 1.8이 출시 된 후에 바로 이전에 배운 것 암호화 변경 1.8에 Windows XP에서 사용자를 중단 합니다.

이 문제를 해결 하는 핫픽스를 릴리스 이후로 했습니다.  NuGet을 통해 Visual Studio 확장 갤러리를 업데이트 하 여이 핫픽스를 받게 됩니다.

## <a name="features"></a>기능

### <a name="satellite-packages-for-localized-resources"></a>지역화 된 리소스에 대 한 위성 패키지
NuGet 1.8는 이제.NET Framework의 위성 어셈블리 기능와 유사한 지역화 된 리소스에 대 한 별도 패키지를 만들 수 있는 기능을 지원 합니다.  위성 패키지는 동일한 방식으로 몇 가지 규칙을 추가 하 여 다른 NuGet 패키지에 만들어집니다.

* 위성 패키지 ID와 파일 이름에는 표준 중 하 나와 일치 하는 접미사 포함 되어 있어야 [.NET Framework에서 사용 되는 문자열을 문화권](http://msdn.microsoft.com/goglobal/bb896001.aspx)합니다.
* 에 해당 `.nuspec` 파일을 위성 패키지 ID에 사용할 동일한 문화권 문자열로 언어 요소를 정의 해야
* 위성 패키지의 종속성을 정의 해야 해당 `.nuspec` 단순히 언어 접미사 뺀 동일한 ID 사용 하 여 패키지의 코어 패키지에는 파일입니다.  코어 패키지 성공적인 설치에 대 한 저장소에 사용할 수 있어야 합니다.

지역화 된 리소스가 포함 된 패키지를 설치 하려면 개발자 저장소에서 지역화 된 패키지 명시적으로 선택 합니다. 현재, NuGet 갤러리는 모든 종류의 위성 패키지에 특별 한 처리를 제공 하지 않습니다.

![지역화 된 pacakges와 패키지 관리자 대화 상자](./media/dlg-w-loc-packs.png)

위성 패키지의 코어 패키지에 대 한 종속성 나열, 위성와 코어 패키지 된 NuGet 패키지 폴더에 포함 되며 설치.

![지역화 된 패키지와 패키지 폴더](./media/fldr-loc-packs.png)

또한 위성 패키지를 설치 하는 동안 NuGet도 문화권 문자열 명명 규칙을 인식 및 지역화 된 리소스 어셈블리는.NET Framework에서 선택할 수 있도록에 코어 패키지 내에서 올바른 하위 폴더에 복사 합니다.

![복사한 리소스 폴더와 코어 패키지 폴더](./media/fldr-copied-loc.png)

위성 패키지와를 하나의 기존 버그는 NuGet을 지역화 된 리소스를 복사 하지 않습니다는 `bin` 웹 사이트 프로젝트에 대 한 폴더입니다.  이 문제는 NuGet의 다음 릴리스에서 수정 될 예정입니다.

만들고 위성 패키지를 사용 하는 방법을 보여 주는 전체 샘플을 참조 하십시오. [https://github.com/NuGet/SatellitePackageSample](https://github.com/NuGet/SatellitePackageSample)합니다.

### <a name="package-restore-consent"></a>패키지 복원 동의
NuGet 1.8에서 म 토대가 패키지 복원 사용자의 개인 정보 보호에 대 한 중요 한 제약 조건을 지원 합니다. 이 제약 조건에서는 프로젝트 및 패키지를 복원 패키지 복원에 명시적으로 동의를 사용 하 여 솔루션을 빌드하는 개발자의 구성 된 패키지 소스에서 패키지를 다운로드 하려면 온라인으로 전환 합니다.

두 가지 방법으로이 동의 제공 합니다. 패키지 관리자 구성 대화 상자에서 아래와 같이 첫 번째를 찾을 수 있습니다.  이 메서드는 개발자 컴퓨터에 대 한 주로 사용 됩니다.

![패키지 관리자 구성 대화 상자](./media/pr-consent-configdlg.png)

두 번째 방법은 환경을 변수 "EnableNuGetPackageRestore" 값 "true 로" 설정 하는 것입니다.  이 메서드를 사용 하 여 CI 또는 빌드 서버와 같이 무인된 컴퓨터에 대 한 합니다.

이제 위에서 설명한 대로 우리는 토대가이 기능에 대 한 NuGet 1.8에서 합니다.  실제로,이 모든 기능을 사용 하려면 논리를 추가 했습니다 동안 적용 되지 않습니다 현재이 버전에서 의미 합니다. 그러나 사용할 수 있게, 동의 제약 조건을 적용 버전의 NuGet 이해 하 고 가능한 한 빨리 따라서 영향을 받지 시작할 때 및 사용자 환경을 적절 하 게 구성할 수 있도록 주고자 하므로 다음에서 합니다.

자세한 내용은 참조 하십시오는 [팀 블로그 게시물](http://blog.nuget.org/20120518/package-restore-and-consent.html) 이 기능에 있습니다.

### <a name="nugetexe-performance-improvements"></a>nuget.exe 성능 향상
다운로드 하 고 동시에 패키지를 설치 하려면 설치 명령줄을 수정 하 여 NuGet 1.8 nuget.exe – 및 확장 패키지를 복원 하 여 성능을 크게 향상을 제공 합니다.  높은 수준의 테스트 NuGet 1.8에서 35 %6 패키지를 프로젝트에 설치를 위한 성능 향상을 보여 줍니다.  25로 패키지 수를 늘리면 약 60%의 성능 향상을 보여 줍니다.

## <a name="bug-fixes"></a>버그 수정
1.8 NuGet 패키지 복원 동 및 Windows 8 Express 통합 관련이 있기 때문에 특히 패키지 관리자 콘솔 및 패키지 복원 워크플로에 중점을 두어 많은 버그 수정 포함 합니다.
작업의 전체 목록은 항목 고정 NuGet 1.8에서 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.8&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)합니다.
