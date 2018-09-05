---
title: NuGet 2.0 릴리스 정보
description: NuGet 2.0 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547577"
---
# <a name="nuget-20-release-notes"></a>NuGet 2.0 릴리스 정보

[NuGet 1.8 릴리스 정보](../release-notes/nuget-1.8.md) | [NuGet 2.1 릴리스 정보](../release-notes/nuget-2.1.md)

NuGet 2.0은 2012 년 6 월 19 일에 출시 되었습니다.

## <a name="known-installation-issue"></a>알려진된 설치 문제
VS 2010 SP1을 실행 하는 경우 이전 버전이 설치 되어 있는 경우 NuGet을 업그레이드 하려고 할 때 설치 오류를 실행할 수 있습니다.

해결 방법은 NuGet 제거한 다음 VS 확장 갤러리에서 설치 하는 것입니다.  참조 [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) 대 한 내용은 또는 [VS 핫픽스로 직접 이동](http://bit.ly/vsixcertfix)합니다.

참고: Visual Studio (제거 단추 사용 안 함) 확장을 제거할 수 없습니다, 다음 가능성이 높은 경우 "관리자 권한으로 실행"을 사용 하 여 Visual Studio를 다시 시작

## <a name="package-restore-consent-is-now-active"></a>패키지 복원 동의 활성화 되었습니다.

이 항목에 설명 된 대로 [패키지 복원 동의에 게시](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0를 온라인으로 전환 하 여 패키지를 다운로드 하는 패키지 복원을 사용 하려면 동의 주어 필요 합니다. 패키지 관리자 구성 대화 상자 또는 EnableNuGetPackageRestore 환경 변수를 통해 동의 제공한 확인 하세요.

## <a name="group-dependencies-by-target-frameworks"></a>대상 프레임 워크 종속성 그룹

패키지 종속성 다를 수 있습니다 버전 2.0 부터는 대상 프로젝트의 프레임 워크 프로필에 기반 합니다. 업데이트를 사용 하 여 이렇게 `.nuspec` 스키마입니다. 합니다 `<dependencies>` 요소 집합을 이제 포함할 수 있습니다 `<group>` 요소입니다. 각 그룹에는 0 개 이상의 `<dependency>` 요소 및 `targetFramework` 특성입니다. 대상 프레임 워크를 대상 프로젝트 프레임 워크 프로필과 호환 되는 경우 그룹 내의 모든 종속성이 함께 설치 됩니다. 예를 들어:

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

그룹을 포함할 수 있는 참고 **0** 종속성입니다. 위의 예제에서는 Silverlight 3.0을 대상으로 하는 프로젝트에 어셈블리를 설치 하거나 나중에 패키지를 종속성이 없는 설치 됩니다. 패키지 이상을.NET 4.0을 대상으로 하는 프로젝트에 설치 되어 있으면 두 개의 종속성, jQuery 및 WebActivator에 설치 됩니다.  이러한 2 프레임 워크 또는 다른 프레임 워크의 초기 버전을 대상으로 하는 프로젝트에 패키지가 설치 되어 있으면 RouteMagic 1.1.0 설치 됩니다. 그룹 간 상속은 없습니다. 프로젝트의 대상 프레임 워크와 일치 하는 경우는 `targetFramework` 특성 그룹, 해당 그룹 내 종속성만 설치 됩니다.

패키지를 두 가지 형식 중 하나에 패키지 종속성을 지정할 수 있습니다: 이전 형식의 플랫 목록 `<dependency>` 요소 또는 그룹. 경우는 `<group>` 형식이 사용 됩니다, 2.0 보다 이전 버전의 NuGet으로 패키지를 설치할 수 없습니다.

Note 두 가지 형식 혼합은 허용 되지 않습니다. 예를 들어, 다음 코드 조각은 됩니다 **잘못 된** 않으며 NuGet에서 거부 됩니다.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>대상 프레임 워크에서 콘텐츠 파일 및 PowerShell 스크립트를 그룹화

어셈블리 참조 외에도 콘텐츠 파일과 PowerShell 스크립트로 그룹화 할 수 있습니다 대상 프레임 워크입니다. 동일한 폴더 구조에는 `lib` 대상 프레임 워크를 지정 하는 것에 대 한 폴더를 동일한 방식으로 적용 될 수 있게 합니다 `content` 및 `tools` 폴더. 예를 들어:

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

**참고**: 때문 `init.ps1` 솔루션 수준에서 실행 되 고 모든 개별 프로젝트에 의존 하지 않는 배치 해야 바로 아래는 `tools` 폴더. 프레임 워크별 폴더 안에 배치 하는 경우 무시 됩니다.

또한 NuGet 2.0의 새로운 기능에는 프레임 워크 폴더 수 있음을 *빈*,이 경우 NuGet은 없는 어셈블리 참조를 추가, 콘텐츠 파일을 추가 또는 특정 프레임 워크 버전에 대 한 PowerShell 스크립트를 실행 합니다. 폴더를 위의 예에서 `content\net40` 비어 있습니다.

## <a name="improved-tab-completion-performance"></a>향상 된 탭 완성 성능
NuGet 패키지 관리자 콘솔에서 탭 완성 기능 성능을 크게 개선할 업데이트 되었습니다. 제안 드롭다운 표시 될 때까지 tab 키를 누를 때부터 훨씬 적은 지연이 됩니다.

## <a name="bug-fixes"></a>버그 수정
2.0 NuGet 패키지 복원 동 및 성능에 중점을 두어 많은 버그 수정 프로그램이 포함 되어 있습니다.
작업의 전체 목록은 항목 고정 NuGet 2.0에서 하세요 보기는 [이 릴리스의 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)합니다.
