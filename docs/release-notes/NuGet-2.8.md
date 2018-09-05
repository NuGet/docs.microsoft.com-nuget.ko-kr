---
title: NuGet 2.8 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함 하 여 NuGet 2.8에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547461"
---
# <a name="nuget-28-release-notes"></a>NuGet 2.8 릴리스 정보

[2.7.2 NuGet 릴리스 정보](../release-notes/nuget-2.7.2.md) | [2.8.1 NuGet 릴리스 정보](../release-notes/nuget-2.8.1.md)

NuGet 2.8은 2014 년 1 월 29 일에 출시 되었습니다.

## <a name="acknowledgements"></a>감사의 글

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) -종속성 패키지의 Id를 확인 하는 패키지를 압축 합니다.
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -persistening 피드를 자격 증명 때 $metadata 접미사를 제거 합니다.
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) -지원 nuget.exe 업데이트 명령에 대 한 프로젝트 파일을 지정 합니다.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -교체 토큰-IncludeReferencedProjects를 사용 하 여 전달 되지 않습니다.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -해결 nuget.push 큰 패키지를 푸시할 때 OutOfMemoryException를 throw 합니다.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -프로젝트가 다른 CLI/c + + 프로젝트를 참조 하는 경우에 잘못 된 대상 경로 수정 합니다.
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -개발 종속성으로 기본적으로 설치 되도록 패키지를 허용 합니다.
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -최신 패치 버전에 대 한 암시적 업그레이드를 제거 합니다.
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - 여러 버그 수정 및 NuGet.Server, nuget.exe 미러 명령 및 기타 향상 된 기능입니다.
    - 이 작업은 몇 개월에 걸쳐 2.8에 대 한 마스터 통합할 Gregory 오른쪽 타이밍에 함께 작업을 사용 하 여 수행 되었습니다.

## <a name="patch-resolution-for-dependencies"></a>종속성에 대 한 패치 확인

패키지 종속성을 해결 하는 경우 NuGet 패키지에서 종속성을 충족 하는 가장 낮은 주 및 부 패키지 버전을 선택 하는 전략을 구현 지금까지 했습니다. 그러나 주 및 부 버전을 달리 패치 버전을 항상 해결 된 가장 높은 버전으로 합니다. 좋은 의도로 동작 이지만 종속성을 사용 하 여 패키지를 설치 하는 것에 대 한 결정성이 부족을 만들었습니다. 다음 예제를 참조하세요.

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

이 예에서 Developer1 및 Developer2 설치 PackageA@1.0.0, 각 결국 PackageB의 다른 버전으로 합니다. NuGet 2.8 패치 버전에 대 한 종속성 확인 동작이 주 버전과 부 버전에 대 한 동작을 사용 하 여 일관 되는이 기본 동작을 변경 합니다. 그런 다음 위의 예제에서는 PackageB@1.0.0 설치의 결과로 설치할 PackageA@1.0.0최신 패치 버전에 관계 없이 합니다.

## <a name="-dependencyversion-switch"></a>-DependencyVersion 스위치

NuGet 2.8 변경 하지만 합니다 _기본_ 동작 종속성을 해결 하는 것에 대 한 추가-DependencyVersion 스위치를 통해 종속성 확인 프로세스를 보다 정밀 하 게 제어 패키지 관리자 콘솔에서. 스위치를 통해 가능한 가장 낮은 버전 (기본 동작), 가능한 최상 버전을 가장 높은 부 또는 패치 버전에 대 한 종속성을 확인할 수 있습니다.  이 스위치는 powershell 명령에서 설치 패키지 에서만 작동합니다.

![DependencyVersion 스위치](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>DependencyVersion 특성

위에서 설명한, NuGet에도 기능에 대 한 허용 Nuget.Config 파일에서 새 특성을 설정 하려면-DependencyVersion 스위치 외에도 정의 기본값은 어떤 호출-DependencyVersion 스위치를 지정 하지 않은 경우 설치 패키지입니다. 이 값이 모든 설치 패키지 작업에 대 한 NuGet 패키지 관리자 대화 상자도 적용 됩니다. 이 값을 설정 하려면 아래 특성 Nuget.Config 파일에 추가 합니다.

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>-Whatif를 사용 하 여 미리 보기 NuGet 작업

일부 NuGet 패키지 전체 종속성 그래프를 포함할 수 있으며 따라서이 수를 설치 하는 동안 유용할 제거 또는 업데이트 작업을 먼저 발생 하는 결과 확인 하려면. NuGet 2.8 패키지 설치, 제거 패키지 및 패키지 업데이트 명령을 적용 되는 패키지의 완전 한 클로저 시각화를 활성화 하는 명령을 표준 PowerShell-whatif 스위치를 추가 합니다. 예를 들어 실행 `install-package Microsoft.AspNet.WebApi -whatif` 에서 빈 ASP.NET 웹 응용 프로그램에는 다음이 생성 됩니다.

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

새로운 기능을 조사 하기 위해 패키지의 시험판 버전을 설치 하 고 마지막 안정적인 버전으로 롤백하려면 다음 결정을 일반적이 지 않은 것입니다. NuGet 2.8 이전에이 시험판 패키지 및 해당 종속성을 제거 하 고 다음 이전 버전을 설치 하는 여러 단계의 프로세스가 이었습니다. 그러나 NuGet 2.8을 사용 하 여 업데이트 패키지를 이제 롤백됩니다 전체 패키지 클로저 (예: 패키지의 종속성 트리) 이전 버전으로 합니다.

## <a name="development-dependencies"></a>개발 종속성

개발 프로세스를 최적화 하는 데 사용 되는 도구를 포함 하는 NuGet 패키지로-다양 한 기능을 제공할 수 있습니다. 이러한 구성 요소를 새 패키지를 개발 하는 데 도움이 될 수 있지만 이러한 간주 되지 않아야 새 패키지의 종속성 나중에 게시 될 때입니다. NuGet 2.8에 자신을 식별 하는 패키지를 사용 하도록 설정 된 `.nuspec` 는 developmentDependency 파일로. 설치 하는 경우이 메타 데이터는도 추가할 수는 `packages.config` 패키지가 설치 된 프로젝트의 파일입니다. 경우는 `packages.config` 파일이 중 NuGet 종속성에 대 한 나중에 분석 된 `nuget.exe pack`, 개발 종속성으로 표시 하는 이러한 종속성을 제외 됩니다.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>다양 한 플랫폼에 대 한 개별 packages.config 파일

여러 대상 플랫폼에 대 한 응용 프로그램을 개발 하는 경우 각 해당 빌드 환경에 대해 다른 프로젝트 파일을 저장 하는 일반적인 것입니다. 패키지에 다양 한 플랫폼에 대 한 지원 수준이 다양 한 대로도 여러 프로젝트 파일에서 다른 NuGet 패키지 사용에 일반적입니다. NuGet 2.8 다른 만들어이 시나리오에 대 한 향상 된 지원을 제공 `packages.config` 다양 한 플랫폼 관련 프로젝트 파일에 대 한 파일입니다.

![여러 package.config 파일](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>로컬 캐시에 대체 (fallback)

NuGet 패키지는 일반적으로 사용 된 원격 갤러리에서와 같은 있지만 [NuGet 갤러리](http://www.nuget.org/) 는 네트워크 연결을 사용 하 여, 다양 한 시나리오는 클라이언트가 연결 되지 않았습니다. 네트워크 연결 없이 NuGet 클라이언트에서 해당 패키지는 로컬 NuGet 캐시에서 클라이언트 컴퓨터에 이미 있던 경우에-패키지를 설치할 수 없습니다. 2.8 NuGet 패키지 관리자 콘솔에 대체 (fallback) 자동 캐시를 추가합니다. 예를 들어, 표시 되는 경우 네트워크 어댑터 연결을 끊고 jQuery 설치, 콘솔 다음:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

캐시 대체 (fallback) 기능에는 특정 명령 인수를 사용할 필요가 없습니다. 또한 대체 (fallback) 캐시는 현재 패키지 관리자 콘솔 에서만에서 작동-동작 패키지 관리자 대화 상자에서 현재 작동 하지 않습니다.

## <a name="webmatrix-nuget-client-updates"></a>WebMatrix NuGet 클라이언트 업데이트

NuGet 2.8 함께 WebMatrix 용 NuGet 확장은 포함 된 주요 기능을 많이 포함 하도록 업데이트도 되었으며 [NuGet 2.5](../release-notes/nuget-2.5.md)합니다. ' 업데이트 All', ' 최소 NuGet 버전 ' 및 콘텐츠 파일을 덮어쓸 수 있습니다와 같은 새로운 기능 포함 됩니다.

WebMatrix 3에서 NuGet 패키지 관리자 확장을 업데이트 합니다.

1. WebMatrix 3를 열려면
1. 리본에서 확장 아이콘을 클릭
1. [업데이트] 탭을 선택 합니다.
1. 2.5.0에 NuGet 패키지 관리자를 업데이트 하려면 클릭
1. 닫고 WebMatrix 3를 다시 시작

이것은 WebMatrix에 대 한 NuGet 패키지 관리자 확장의 NuGet 팀의 첫 번째 릴리스입니다.  코드는 최근에 Microsoft에서 오픈 소스 NuGet 프로젝트에 기여 했습니다. 이전에 NuGet 통합 WebMatrix에 빌드된 및 WebMatrix에서 대역 외에서 업데이트할 수 없습니다.  이제 추가로 나머지 NuGet의 클라이언트 도구와 함께 업데이트 하는 기능.

## <a name="bug-fixes"></a>버그 수정

업데이트 패키지의 성능 향상 된 만든 주요 버그 수정 중-명령을 다시 설치 합니다.

이 릴리스의 NuGet에는 이러한 기능 및 앞에서 언급 한 성능 문제를 해결 하는 것 외에도 다른 많은 버그 수정도 포함 됩니다. 릴리스에서 해결 181 총 문제가 있었습니다. 작업의 전체 목록은 항목에서에서 수정 된 NuGet 2.8 하세요 보기는 [이 릴리스의 NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)합니다.
