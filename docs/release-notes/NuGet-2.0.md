---
title: NuGet 2.0 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 2.0에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6874cbf0404f18ab7007bec1e0f66089c790d08
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776995"
---
# <a name="nuget-20-release-notes"></a>NuGet 2.0 릴리스 정보

[NuGet 1.8 릴리스 정보](../release-notes/nuget-1.8.md)  |  [NuGet 2.1 릴리스 정보](../release-notes/nuget-2.1.md)

NuGet 2.0은 2012 년 6 월 19 일에 출시 되었습니다.

## <a name="known-installation-issue"></a>알려진 설치 문제
VS 2010 s p 1을 실행 하는 경우 이전 버전을 설치한 경우 NuGet을 업그레이드 하려고 할 때 설치 오류가 발생할 수 있습니다.

해결 방법은 NuGet을 제거한 후 VS 확장 갤러리에서 설치 하는 것입니다.  <https://support.microsoft.com/kb/2581019>자세한 내용은를 참조 하거나 [VS 핫픽스로 직접 이동](http://bit.ly/vsixcertfix)하십시오.

참고: Visual Studio에서 확장을 제거 하는 것을 허용 하지 않는 경우 (제거 단추를 사용할 수 없음) "관리자 권한으로 실행"을 사용 하 여 Visual Studio를 다시 시작 해야 할 수도 있습니다.

## <a name="package-restore-consent-is-now-active"></a>이제 패키지 복원 동의가 활성 상태입니다.

이 [게시물의 패키지 복원 동의에](http://blog.nuget.org/20120518/package-restore-and-consent.html)설명 된 대로 NuGet 2.0은 이제 패키지 복원이 온라인으로 전환 되 고 패키지를 다운로드할 수 있도록 동의 해야 합니다. 패키지 관리자 구성 대화 상자 또는 EnableNuGetPackageRestore 환경 변수를 통해 동의를 제공 했는지 확인 하세요.

## <a name="group-dependencies-by-target-frameworks"></a>대상 프레임 워크로 종속성 그룹화

버전 2.0부터 패키지 종속성은 대상 프로젝트의 프레임 워크 프로필에 따라 달라질 수 있습니다. 업데이트 된 스키마를 사용 하 여 수행 됩니다 `.nuspec` . 요소에는 `<dependencies>` 이제 요소 집합이 포함 될 수 있습니다 `<group>` . 각 그룹에는 0 개 이상의 `<dependency>` 요소 및 `targetFramework` 특성이 포함 됩니다. 대상 프레임 워크가 대상 프로젝트 프레임 워크 프로필과 호환 되는 경우 그룹 내의 모든 종속성이 함께 설치 됩니다. 예를 들면 다음과 같습니다.

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

그룹에는 종속성 **이 0 개** 포함 될 수 있습니다. 위의 예제에서 패키지가 Silverlight 3.0 이상을 대상으로 하는 프로젝트에 설치 된 경우 종속성이 설치 되지 않습니다. 패키지가 .NET 4.0 이상을 대상으로 하는 프로젝트에 설치 된 경우에는 jQuery와 WebActivator 라는 두 개의 종속성이 설치 됩니다.  패키지를 이러한 2 프레임 워크의 이전 버전을 대상으로 하는 프로젝트에 설치 하거나 다른 프레임 워크를 대상으로 하는 경우 RouteMagic 1.1.0가 설치 됩니다. 그룹 간에는 상속이 없습니다. 프로젝트의 대상 프레임 워크가 그룹의 특성과 일치 하는 경우 `targetFramework` 해당 그룹 내의 종속성만 설치 됩니다.

패키지는 두 가지 형식 중 하나로 패키지 종속성을 지정할 수 있습니다. 즉, 단순 요소 목록의 이전 형식 `<dependency>` 또는 그룹입니다. `<group>`형식을 사용 하는 경우 패키지를 2.0 이전의 NuGet 버전에 설치할 수 없습니다.

두 형식을 함께 사용할 수는 없습니다. 예를 들어 다음 코드 조각은 **잘못** 되었으며 NuGet에서 거부 됩니다.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>대상 프레임 워크로 콘텐츠 파일 및 PowerShell 스크립트 그룹화

어셈블리 참조 외에도 대상 프레임 워크를 기준으로 콘텐츠 파일 및 PowerShell 스크립트를 그룹화 할 수 있습니다. `lib`대상 프레임 워크를 지정 하기 위해 폴더에 있는 동일한 폴더 구조를 이제 `content` 및 폴더와 동일한 방식으로 적용할 수 있습니다 `tools` . 예를 들면 다음과 같습니다.

```
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
```

**참고**: `init.ps1` 는 솔루션 수준에서 실행 되며 개별 프로젝트에 종속 되지 않기 때문에 폴더 바로 아래에 배치 해야 합니다 `tools` . 프레임 워크 관련 폴더에 배치 된 경우 무시 됩니다.

또한 NuGet 2.0의 새로운 기능은 프레임 워크 폴더가 *비어* 있을 수 있습니다 .이 경우 nuget은 어셈블리 참조를 추가 하거나 콘텐츠 파일을 추가 하거나 특정 프레임 워크 버전에 대해 PowerShell 스크립트를 실행 하지 않습니다. 위의 예제에서 폴더는 `content\net40` 비어 있습니다.

## <a name="improved-tab-completion-performance"></a>향상 된 탭 완성 성능
NuGet 패키지 관리자 콘솔의 탭 완성 기능이 업데이트 되어 성능이 크게 향상 되었습니다. 제안 드롭다운이 나타날 때까지 tab 키를 누르는 시간부터 지연 시간이 훨씬 줄어듭니다.

## <a name="bug-fixes"></a>버그 픽스
NuGet 2.0에는 패키지 복원 동의 및 성능에 중점을 두어 많은 버그 수정이 포함 되어 있습니다.
NuGet 2.0에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)를 확인 하세요.
