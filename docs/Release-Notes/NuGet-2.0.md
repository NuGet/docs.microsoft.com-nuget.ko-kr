---
title: NuGet 2.0 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 2.0에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0e637a953d9d5d10394857a352be96a7f68dc4e8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-20-release-notes"></a>NuGet 2.0 릴리스 정보

[NuGet 1.8 릴리스 정보](../release-notes/nuget-1.8.md) | [NuGet 2.1 릴리스 정보](../release-notes/nuget-2.1.md)

NuGet 2.0은 2012 년 6 월 19 일에 출시 되었습니다.

## <a name="known-installation-issue"></a>알려진된 설치 문제
VS 2010 s p 1을 실행 하는 경우 이전 버전이 설치 되어 있는 경우 NuGet을 업그레이드 하는 동안 설치 오류에 실행할 수 있습니다.

해결 하려면 NuGet 제거한 다음 VS 확장 갤러리에서 설치 됩니다.  참조 [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) 자세한 내용은 또는 [VS 핫픽스로 직접 이동](http://bit.ly/vsixcertfix)합니다.

참고: Visual Studio 확장 (제거 단추 사용 안 함)을 제거 하도록 허용 하지, 한 후 가능성 하면 "관리자 권한으로 실행"을 사용 하 여 Visual Studio를 다시 시작

## <a name="package-restore-consent-is-now-active"></a>패키지 복원 동의 활성화 되었습니다.

이 항목에 설명 된 대로 [패키지 복원 동의 게시물](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0를 온라인으로 전환 하 고 패키지를 다운로드 패키지 복원을 사용할 수 있도록 동의 지정 필요 합니다. 패키지 관리자 구성 대화 상자 또는 EnableNuGetPackageRestore 환경 변수를 통해 동의 제공한 확인 하십시오.

## <a name="group-dependencies-by-target-frameworks"></a>대상 프레임 워크에 의해 그룹 종속성

패키지 종속성에 따라 달라질 수 있습니다 대상 프로젝트의 프레임 워크 프로필에 따라 버전 2.0 시작 합니다. 이 위해서는 업데이트 된 사용 `.nuspec` 스키마입니다. `<dependencies>` 요소 수는 일련의 포함 이제 `<group>` 요소입니다. 각 그룹에는 0 개 이상의 포함 `<dependency>` 요소와 `targetFramework` 특성입니다. 대상 프레임 워크를 대상 프로젝트 프레임 워크 프로필에 호환 되는 경우 그룹 내의 모든 종속성이 함께 설치 됩니다. 예를 들어:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

그룹에 포함 될 수 있는 참고 **0** 종속성. 위의 예에서 패키지 Silverlight 3.0을 대상으로 하는 프로젝트에 설치 된 이상인 경우 종속성이 없는 설치 됩니다. 패키지는.NET 4.0을 대상으로 하는 프로젝트에 설치 된 이상을, jQuery 및 WebActivator, 두 개의 종속성 설치 됩니다.  이러한 2 프레임 워크 또는 다른 프레임 워크의 초기 버전을 대상으로 하는 프로젝트에 패키지 설치 되어 있으면 RouteMagic 1.1.0 설치 됩니다. 그룹 간의 상속은 없습니다. 프로젝트의 대상 프레임 워크와 일치 하는 경우는 `targetFramework` 특성 그룹, 해당 그룹 내 종속성만 설치 됩니다.

패키지는 두 가지 형식 중 하나로 패키지 종속성을 지정할 수: 이전 형식의의 단순 목록 `<dependency>` 요소나 그룹입니다. 경우는 `<group>` 형식이 사용 됨, 2.0 보다 이전 버전의 NuGet 패키지를 설치할 수 없습니다.

Note는 두 가지 형식 함께 수 없습니다. 예를 들어 다음 코드 조각은 **잘못 된** 및 NuGet에서 거부 됩니다.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>콘텐츠 파일을 분류 하 고 대상 프레임 워크에서 PowerShell 스크립트

어셈블리 참조 외에도 콘텐츠 파일 및 PowerShell 스크립트도 그룹화 할 수 있습니다 대상 프레임 워크입니다. 동일한 폴더 구조에서 찾을 수는 `lib` 대상 프레임 워크를 지정 하는 폴더에 같은 방법으로에서 이제 적용 될 수는 `content` 및 `tools` 폴더입니다. 예를 들어:

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

**참고**: 때문에 `init.ps1` 솔루션 수준에서 실행 되 고 종속 모든 개별 프로젝트에 배치 해야 바로 아래에서 `tools` 폴더입니다. 프레임 워크별 폴더 안에 배치 하는 경우 무시 됩니다.

또한, NuGet 2.0의 새로운 기능에는 프레임 워크 폴더 수 *빈*, 두 가지 경우 NuGet은 없는 어셈블리 참조를 추가, 콘텐츠 파일을 추가 또는 특정 프레임 워크 버전에 대 한 PowerShell 스크립트를 실행 합니다. 폴더 위의 예에서 `content\net40` 비어 있습니다.

## <a name="improved-tab-completion-performance"></a>향상 된 탭 완성 성능
NuGet 패키지 관리자 콘솔의 탭 완성 기능 성능이 대폭 향상에 업데이트 되었습니다. 드롭다운 추천 목록에 나타날 때까지 tab 키를 누를 때부터 훨씬 더 적은 지연이 됩니다.

## <a name="bug-fixes"></a>버그 수정
NuGet 2.0 패키지 복원 동 및 성능에 중점을 두어 많은 버그 수정 포함 되어 있습니다.
작업의 전체 목록은 항목 고정 NuGet 2.0에서 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)합니다.
