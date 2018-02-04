---
title: "NuGet 2.8 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 2.8에 대 한 릴리스 정보입니다."
keywords: "NuGet 2.8 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 39b885adc9e23eb815f65639875c4a4c27d61a4c
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-28-release-notes"></a>NuGet 2.8 릴리스 정보

[NuGet 2.7.2 릴리스 정보](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 릴리스 정보](../release-notes/nuget-2.8.1.md)

NuGet 2.8 2014 년 1 월 29 일에 출시 되었습니다.

## <a name="acknowledgements"></a>감사의 글

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) -압축 된 패키지, 종속성 패키지의 Id를 확인 하는 경우.
1. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -persistening 피드 자격 증명 때 $metadata 접미사를 제거 합니다.
1. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) -nuget.exe 업데이트 명령에 대 한 프로젝트 파일을 지정 하는 지원 합니다.
1. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) --IncludeReferencedProjects 함께 전달 되지 않은 교체 토큰입니다.
1. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -해결 nuget.push 큰 패키지를 적용할 때 발생 한 OutOfMemoryException를 throw 합니다.
1. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -다른 CLI/c + + 프로젝트를 참조 하는 프로젝트에 잘못 된 대상 경로 수정 합니다.
1. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -패키지 개발 종속성 기본적으로 설치 되도록 허용
1. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -최신 패치 버전에 대 한 암시적 업그레이드를 제거 합니다.
1. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - 여러 버그 수정 및 NuGet.Server, nuget.exe 미러 명령 등에 대 한 향상 된 기능입니다.
    - 2.8 마스터에 통합 하는 오른쪽 타이밍에 협력해 Gregory와 몇 개월 동안 수행 된이 작업의이 있습니다.

## <a name="patch-resolution-for-dependencies"></a>종속성에 대 한 패치 확인

패키지 종속성을 확인할 때에 지금까지 NuGet 패키지의 종속성을 만족 하는 가장 낮은 주 및 부 패키지 버전을 선택 하는 전략을 구현 했습니다. 그러나 주 및 부 버전을 달리 패치 버전 항상 해결 된 가장 높은 버전으로 합니다. 또한 악의적 동작 이지만 패키지 종속성이 설치를 위한 결정성이 부족 한 만들어집니다. 다음 예제를 참조하세요.

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

이 예제에서는 경우에 Developer1 및 Developer2 설치 PackageA@1.0.0각 결국 PackageB의 다른 버전으로, 합니다. NuGet 2.8 패치 버전에 대 한 종속성 확인 하는 동작은 주 버전과 부 버전에 대 한 동작과 일치 되도록이 기본 동작을 변경 합니다. 그런 다음 위의 예에 PackageB@1.0.0 설치 설치할 PackageA@1.0.0최신 패치 버전에 관계 없이 합니다.

## <a name="-dependencyversion-switch"></a>-DependencyVersion 스위치

NuGet 2.8 변경 하지만 _기본_ 동작 종속성을 확인 하는 것에 대 한 추가-DependencyVersion 스위치를 통해 종속성 확인 프로세스를 보다 자세히 제어 패키지 관리자 콘솔에 있습니다. 스위치 가능한 가장 낮은 버전 (기본 동작), 가능한 최상 버전 또는 부 가장 높은 또는 패치 버전을 확인 하 고 종속성을 수 있습니다.  이 스위치는 powershell 명령에서 설치 패키지에 대 한 에서만 작동합니다.

![DependencyVersion 스위치](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>DependencyVersion 특성

위에서 설명한, 기능에 대 한 NuGet도 있었습니다 Nuget.Config 파일에서 새 특성을 설정 하는-DependencyVersion 스위치 외에도 정의 기본값은 어떤-DependencyVersion 스위치의 호출에 지정 되지 않은 경우 설치 패키지입니다. 이 값 NuGet 패키지 관리자 대화 상자 설치 패키지는 모든 작업에도 적용 됩니다. 이 값을 설정 하려면 아래 특성 Nuget.Config 파일을 추가 합니다.

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>미리 보기 NuGet 작업과-whatif를 지원함

일부 NuGet 패키지가 상세한 종속성 그래프를 포함할 수 있으며 따라서 것 수는 설치 중에 도움이 될, 제거 또는 업데이트 작업을 먼저 실행 되는 작업을 확인 하려면. NuGet 2.8 패키지 설치, 제거 패키지 및 업데이트 패키지 명령의 명령을 적용 하는 패키지의 전체 closure 시각화를 사용 하도록 설정 하려면 표준 PowerShell-whatif 스위치를 추가 합니다. 예를 들면 `install-package Microsoft.AspNet.WebApi -whatif` 에 빈 ASP.NET 웹 응용 프로그램은 다음을 생성 합니다.

    PM> install-package Microsoft.AspNet.WebApi -whatif
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.WebHost (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Core (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Client (≥ 5.0.0)'.
    Attempting to resolve dependency 'Newtonsoft.Json (≥ 4.5.11)'.
    Install Newtonsoft.Json 4.5.11
    Install Microsoft.AspNet.WebApi.Client 5.0.0
    Install Microsoft.AspNet.WebApi.Core 5.0.0
    Install Microsoft.AspNet.WebApi.WebHost 5.0.0
    Install Microsoft.AspNet.WebApi 5.0.0

## <a name="downgrade-package"></a>다운 그레이드 패키지

안정적인 최신 버전으로 롤백할로 결정 한 새 기능을 검토 하려면 패키지의 시험판 버전을 설치 하는 일반적이 지 않습니다. NuGet 2.8 하기 전에이 시험판 패키지 및 해당 종속성을 제거한 다음 이전 버전을 설치의 여러 단계 프로세스입니다. 그러나 NuGet 2.8와 업데이트 패키지는 이제 롤백할 전체 패키지 클로저 (예: 패키지의 종속성 트리) 이전 버전으로.

## <a name="development-dependencies"></a>개발 종속성

개발 프로세스를 최적화 하는 데 사용 되는 도구를 포함 하 여 NuGet 패키지로-다양 한 유형의 기능을 제공할 수 있습니다. 이러한 구성 요소를 새 패키지를 개발에 도움이 될 수 있지만 간주 되지 않아야 새 패키지의 종속성 나중에 게시할 때. NuGet 2.8를 사용 하면 패키지에서 자신을 식별 하는 `.nuspec` 는 developmentDependency 파일입니다. 설치 되 면이 메타 데이터도에 추가할는 `packages.config` 패키지가 설치 된 프로젝트의 파일입니다. 경우는 `packages.config` 파일이 중 NuGet 종속성에 대 한 나중에 분석 된 `nuget.exe pack`, 개발 종속성으로 표시 하는 해당 종속성을 제외 합니다.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>다른 플랫폼에 대해 개별 packages.config 파일

여러 대상 플랫폼에 대 한 응용 프로그램을 개발할 경우 일반적으로 각 해당 빌드 환경에 대 한 여러 프로젝트 파일에는 있습니다. 것도 다른 프로젝트 파일에서 다른 NuGet 패키지를 사용 하도록 패키지에 다양 한 플랫폼에 대 한 지원 수준이 다양 한 대로 합니다. NuGet 2.8 다른 만들어이 시나리오에 대 한 향상 된 지원을 제공 `packages.config` 여러 플랫폼 관련 프로젝트 파일에 대 한 파일입니다.

![여러 package.config 파일](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>로컬 캐시에 대체 (fallback)

NuGet 패키지는 일반적으로 사용 된 원격 갤러리에서와 같은 경우 [은 NuGet 갤러리](http://www.nuget.org/) 는 네트워크 연결을 사용 하 여 다양 한 시나리오는 클라이언트가 연결 되지 않았습니다. 네트워크 연결 없이 NuGet 클라이언트에서 이러한 패키지는 로컬 캐시 NuGet의에서 클라이언트 컴퓨터에 이미 있던 경우에 패키지-설치할 수 없습니다. NuGet 2.8 패키지 관리자 콘솔에 대체 (fallback) 자동 캐시를 추가합니다. 예를 들어 표시 되 면 네트워크 어댑터의 연결을 끊고 jQuery 설치, 콘솔 다음:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

캐시 대체 기능에는 특정 명령 인수 필요 하지 않습니다. 또한 캐시 대체 현재 패키지 관리자 콘솔 에서만에서 작동 함-동작 패키지 관리자 대화 상자에서 현재 작동 하지 않습니다.

## <a name="webmatrix-nuget-client-updates"></a>WebMatrix NuGet 클라이언트 업데이트

NuGet 2.8 함께 WebMatrix 용 NuGet 확장 하도록 업데이트 되었습니다 포함 된 주요 기능을 많이 포함 [NuGet 2.5](../release-notes/nuget-2.5.md)합니다. ' 업데이트 All', ' 최소 NuGet 버전 ' 및 콘텐츠 파일의 덮어쓰기를 허용 범위를 같은 새로운 기능이 포함 됩니다.

WebMatrix 3에서 NuGet 패키지 관리자 확장을 업데이트.

1. 열기 WebMatrix 3
1. 리본 메뉴에서 확장 아이콘을 클릭
1. 업데이트 탭을 선택
1. NuGet 패키지 관리자 2.5.0를 업데이트 하려면 클릭
1. 닫고 WebMatrix 3을 다시 시작

WebMatrix 용 NuGet 패키지 관리자 확장의 NuGet 팀의 첫 번째 릴리스에서입니다.  코드는 오픈 소스 NuGet 프로젝트에 Microsoft에서 최근에 제공 했습니다. 이전에 NuGet 통합 WebMatrix에 빌드된 및 WebMatrix에서 대역 외에서 업데이트할 수 없습니다.  이제는 기능을 추가로 나머지 NuGet의 클라이언트 도구와 함께 업데이트 했습니다.

## <a name="bug-fixes"></a>버그 수정

업데이트 패키지의 성능 향상 된 만든 주요 버그 수정 중 하나-명령을 다시 설치 합니다.

이러한 기능과 앞에서 언급 한 성능 수정 외에이 버전의 NuGet 다른 많은 버그 수정 포함 되어 있습니다. 181 총 문제는 릴리스에서 해결 했습니다. 작업의 전체 목록에 대 한 항목에서에서 수정 된 NuGet 2.8 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)합니다.
