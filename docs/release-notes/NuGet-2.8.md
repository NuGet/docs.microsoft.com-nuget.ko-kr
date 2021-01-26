---
title: NuGet 2.8 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 2.8에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cb77cf0f049b5b3cfe1039d83ab58e33457674bf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776716"
---
# <a name="nuget-28-release-notes"></a>NuGet 2.8 릴리스 정보

[NuGet 2.7.2 릴리스 정보](../release-notes/nuget-2.7.2.md)  |  [NuGet 2.8.1 릴리스 정보](../release-notes/nuget-2.8.1.md)

NuGet 2.8은 2014 년 1 월 29 일에 출시 되었습니다.

## <a name="acknowledgements"></a>감사의 말

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ( [@leppie](https://twitter.com/leppie) )
    - [#3466](https://nuget.codeplex.com/workitem/3466) -패키지를 압축 하는 경우 종속성 패키지의 Id를 확인 합니다.
2. [텐 Balliauw](https://www.codeplex.com/site/users/view/maartenba) ( [@maartenballiauw](https://twitter.com/maartenballiauw) )
    - [#2379](https://nuget.codeplex.com/workitem/2379) -피드 자격 증명을 persistening 때 $metadata 접미사를 제거 합니다.
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ( [@foxtricks](https://twitter.com/foxtricks) )
    - [#3538](http://nuget.codeplex.com/workitem/3538) -nuget.exe update 명령에 대 한 프로젝트 파일 지정을 지원 합니다.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -대체 토큰이-IncludeReferencedProjects로 전달 되지 않았습니다.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ( [@Sarkie_Dave](https://twitter.com/Sarkie_Dave) )
    - [#3677](http://nuget.codeplex.com/workitem/3677) -대량 패키지를 푸시할 때 OutOfMemoryException throw를 수정 합니다.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -프로젝트가 다른 CLI/c + + 프로젝트를 참조할 때 잘못 된 대상 경로를 수정 합니다.
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )
    - [#3639](https://nuget.codeplex.com/workitem/3639) -패키지를 기본적으로 개발 종속성으로 설치할 수 있습니다.
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ( [@davidfowl](https://twitter.com/davidfowl) )
    - [#3717](https://nuget.codeplex.com/workitem/3717) -최신 패치 버전에 대 한 암시적 업그레이드 제거
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - NuGet. 서버, nuget.exe 미러 명령 및 기타에 대 한 여러 버그 수정 및 개선 사항
    - 이러한 작업은 몇 달 이내에 수행 되었으며, Gregory를 사용 하 여 2.8에 대 한 마스터에 통합 하는 데 적합 한 타이밍에 대해 노력 하 고 있습니다.

## <a name="patch-resolution-for-dependencies"></a>종속성에 대 한 패치 확인

패키지 종속성을 확인할 때 NuGet은 패키지의 종속성을 충족 하는 가장 낮은 주 및 부 패키지 버전을 선택 하는 전략을 지금 구현 했습니다. 그러나 주 버전과 부 버전이 달리 패치 버전은 항상 가장 높은 버전으로 확인 되었습니다. 이 동작은 잘 악의적 종속성이 포함 된 패키지를 설치 하는 것이 적합 하지 않습니다. 다음 예제를 참조하세요.

```
PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

PackageB@1.0.1 is published

Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1
```

이 예제에서 Developer1 및 Developer2가 설치 된 경우에도 PackageA@1.0.0 각는 다른 버전의 PackageB로 종료 됩니다. NuGet 2.8은 패치 버전에 대 한 종속성 확인 동작이 주 버전 및 부 버전의 동작과 일치 하도록이 기본 동작을 변경 합니다. 위의 예제에서은 PackageB@1.0.0 PackageA@1.0.0 최신 패치 버전에 관계 없이 설치의 결과로 설치 됩니다.

## <a name="-dependencyversion-switch"></a>-DependencyVersion 스위치

NuGet 2.8은 종속성을 확인 하는 _기본_ 동작을 변경 하지만 패키지 관리자 콘솔의-DependencyVersion 스위치를 통해 종속성 확인 프로세스를 보다 정확 하 게 제어할 수 있습니다. 스위치를 사용 하면 가능한 가장 낮은 버전 (기본 동작), 가능한 가장 높은 버전 또는 가장 높은 부 또는 패치 버전으로 종속성을 확인할 수 있습니다.  이 스위치는 powershell 명령에서 설치 패키지에 대해서만 작동 합니다.

![DependencyVersion 스위치](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>DependencyVersion 특성

위에서 자세히 설명 하는-DependencyVersion 스위치 외에도 NuGet은를 호출할 때-DependencyVersion 스위치를 지정 하지 않은 경우 기본값을 정의 하는 Nuget.Config 파일에 새 특성을 설정 하는 기능을 허용 합니다. 이 값은 또한 패키지 설치 작업에 대 한 NuGet 패키지 관리자 대화 상자에서 적용 됩니다. 이 값을 설정 하려면 Nuget.Config 파일에 아래 특성을 추가 합니다.

```xml
<config>
    <add key="dependencyversion" value="Highest" />
</config>
```

## <a name="preview-nuget-operations-with--whatif"></a>-Whatif를 사용 하 여 NuGet 작업 미리 보기

일부 NuGet 패키지에는 심층 종속성 그래프가 있을 수 있으며,이에 따라 설치, 제거 또는 업데이트 작업 중에 수행 되는 작업을 먼저 확인 하는 것이 유용할 수 있습니다. NuGet 2.8은 명령이 적용 되는 패키지의 전체 클로저를 시각화할 수 있도록 표준 PowerShell-whatif 스위치를 설치 패키지, 제거 패키지 및 업데이트 패키지 명령에 추가 합니다. 예를 들어 `install-package Microsoft.AspNet.WebApi -whatif` 빈 ASP.NET 웹 응용 프로그램에서를 실행 하면 다음과 같은 결과가 발생 합니다.

```
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
```

## <a name="downgrade-package"></a>패키지 다운 그레이드

새 기능을 조사 하 여 안정적인 최신 버전으로 롤백하려면 먼저 시험판 버전의 패키지를 설치 하는 것이 일반적입니다. NuGet 2.8 이전 버전은 시험판 패키지와 해당 종속성을 제거한 후 이전 버전을 설치 하는 여러 단계로 이루어진 프로세스 였습니다. 그러나 NuGet 2.8에서 업데이트 패키지는 이제 전체 패키지 닫기 (예: 패키지의 종속성 트리)를 이전 버전으로 롤백합니다.

## <a name="development-dependencies"></a>개발 종속성

개발 프로세스를 최적화 하는 데 사용 되는 도구를 포함 하 여 다양 한 유형의 기능을 NuGet 패키지로 배달할 수 있습니다. 이러한 구성 요소는 새 패키지를 개발 하는 데 사용할 수 있는 반면 나중에 게시 될 때 새 패키지의 종속성으로 간주 되지 않아야 합니다. NuGet 2.8을 사용 하면 패키지에서 파일 자체를 `.nuspec` developmentDependency로 식별할 수 있습니다. 설치 된 경우이 메타 데이터는 `packages.config` 패키지가 설치 된 프로젝트의 파일에도 추가 됩니다. 에서 해당 `packages.config` 파일이 나중에 NuGet 종속성을 분석 하는 경우 `nuget.exe pack` 개발 종속성으로 표시 된 종속성을 제외 합니다.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>각 플랫폼에 대 한 개별 packages.config 파일

여러 대상 플랫폼용 응용 프로그램을 개발 하는 경우 각 빌드 환경에 대해 서로 다른 프로젝트 파일을 포함 하는 것이 일반적입니다. 또한 패키지 마다 다양 한 플랫폼에 대 한 다양 한 지원 수준이 있기 때문에 다양 한 프로젝트 파일에서 다른 NuGet 패키지를 사용 하는 것이 일반적입니다. NuGet 2.8은 플랫폼별 프로젝트 파일 마다 다른 파일을 만들어이 시나리오에 대 한 향상 된 지원을 제공 합니다 `packages.config` .

![여러 package.config 파일](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>로컬 캐시로 대체

NuGet 패키지는 일반적으로 네트워크 연결을 사용 하 여 [nuget 갤러리](http://www.nuget.org/) 와 같은 원격 갤러리에서 사용 되지만 클라이언트가 연결 되지 않은 많은 시나리오가 있습니다. 네트워크에 연결 되지 않은 경우 NuGet 클라이언트는 패키지를 성공적으로 설치할 수 없습니다. 해당 패키지는 로컬 NuGet 캐시의 클라이언트 컴퓨터에 이미 있는 경우에도 마찬가지입니다. NuGet 2.8은 패키지 관리자 콘솔에 자동 캐시 대체를 추가 합니다. 예를 들어 네트워크 어댑터의 연결을 끊고 jQuery를 설치 하면 콘솔에 다음이 표시 됩니다.

```
PM> Install-Package jquery
The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
Installing 'jQuery 2.0.3'.
Successfully installed 'jQuery 2.0.3'.
Adding 'jQuery 2.0.3' to WebApplication18.
Successfully added 'jQuery 2.0.3' to WebApplication18.
```

캐시 대체 (fallback) 기능에는 특정 명령 인수가 필요 하지 않습니다. 또한 cache fallback은 현재 패키지 관리자 콘솔 에서만 작동 합니다 .이 동작은 현재 패키지 관리자 대화 상자에서 작동 하지 않습니다.

## <a name="webmatrix-nuget-client-updates"></a>WebMatrix NuGet 클라이언트 업데이트

Nuget 2.8과 함께 WebMatrix에 대 한 NuGet 확장도 [nuget 2.5](../release-notes/nuget-2.5.md)과 함께 제공 되는 많은 주요 기능을 포함 하도록 업데이트 되었습니다. 새 기능에는 ' 업데이트 모두 ', ' 최소 NuGet 버전 ' 및 콘텐츠 파일 덮어쓰기를 허용 하는 기능이 포함 됩니다.

WebMatrix 3에서 NuGet 패키지 관리자 확장을 업데이트 하려면 다음을 수행 합니다.

1. WebMatrix 3 열기
1. 리본에서 확장 아이콘을 클릭 합니다.
1. 업데이트 탭 선택
1. NuGet 패키지 관리자를 2.5.0로 업데이트 하려면 클릭 하십시오.
1. WebMatrix 3을 닫고 다시 시작 합니다.

WebMatrix 용 nuget 패키지 관리자 확장의 첫 번째 릴리스입니다.  이 코드는 최근에 Microsoft에서 오픈 소스 NuGet 프로젝트에 참여 했습니다. 이전에는 NuGet 통합이 WebMatrix에 내장 되었으며 WebMatrix에서 대역 외로 업데이트 되지 않았습니다.  이제 나머지 NuGet 클라이언트 도구와 함께이를 추가로 업데이트할 수 있는 기능이 있습니다.

## <a name="bug-fixes"></a>버그 픽스

중요 한 버그 수정 사항 중 하나는 업데이트-패키지-다시 설치 명령에서 성능 향상입니다.

이러한 기능 외에도이 NuGet 릴리스에는 기타 많은 버그 수정이 포함 되어 있습니다. 릴리스에서 해결 된 총 181 개의 문제가 있습니다. NuGet 2.8에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)를 확인 하세요.
