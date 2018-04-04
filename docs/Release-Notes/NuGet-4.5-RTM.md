---
title: NuGet 4.5 RTM 릴리스 정보 | Microsoft Docs
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 12/4/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet 4.5 RTM에 대한 릴리스 정보(알려진 문제, 버그 수정, 추가된 기능 및 DCR 포함)
keywords: NuGet 4.5 RTM 릴리스 정보, 버그 수정, 알려진 문제, 추가된 기능, DCR
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: dbde7256ed5526761107272792d7c7cdc324a3ef
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-45-rtm-release-notes"></a>NuGet 4.5 RTM 릴리스 정보

[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes)는 [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe)과 함께 제공됩니다.

## <a name="known-issues"></a>알려진 문제

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>.NET Framework 및 NuGet이 포함된 .NET Standard 2.0 관련 문제 

.NET Standard 및 해당 도구는 .NET Framework 4.6.1을 대상으로 하는 프로젝트에서 .NET Standard 2.0 또는 이전 버전을 대상으로 하는 NuGet 패키지 및 프로젝트를 사용할 수 있도록 설계되었습니다. [이 문서](https://github.com/dotnet/standard/issues/481)에서는 해당 시나리오와 관련된 문제, 문제를 해결하기 위한 계획 및 현재의 도구 상태로 배포할 수 있는 해결 방법을 요약하고 있습니다.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>NuGet 패키지 관리자를 사용하여 DotNetCLITools를 보거나 추가 또는 업데이트할 수 없음

#### <a name="issue"></a>문제

NuGet 패키지 관리자는 DotNetCLITools 추가/업데이트를 표시하지 않으며 허용하지도 않습니다. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>해결 방법

프로젝트 파일에서 DotNetCLIToolReferences를 수동으로 편집해야 합니다.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>대상 프레임워크 버전의 대상을 변경하면 불완전한 IntelliSense가 발생할 수 있음

#### <a name="issue"></a>문제

Visual Studio에서 대상 프레임워크 버전의 대상을 변경하면 불완전한 IntelliSense가 발생할 수 있습니다. 이 문제는 PackageReferences를 패키지 관리자 형식으로 사용하는 경우에 발생합니다. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>해결 방법

수동 복원을 수행합니다.

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>잘못된 시그니처와 함께 어셈블리가 포함된 .NET Core 프로젝트의 패키지는 무한 복원 루프를 트리거할 수 있음

#### <a name="issue"></a>문제

경우에 따라 잘못된 시그니처와 함께 어셈블리가 포함된 패키지를 사용하거나 패키지 버전이 'DateTime' 표시기로 설정된 경우 패키지 자동 복원이 무한 루프로 실행됩니다([dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457)).

#### <a name="workaround"></a>해결 방법

지금은 해결 방법이 없습니다.

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>NuGet 4.5 RTM 기간에서 수정된 문제

NuGet 4.4 RTM에서 수정된 문제는 [NuGet 4.4 RTM 릴리스 정보](../release-notes/nuget-4.4-RTM.md)를 참조하세요. 

### <a name="features"></a>기능

- 기호 패키지 자동 푸시 사용 안 함 - [#6113](https://github.com/NuGet/Home/issues/6113)

### <a name="bugs"></a>버그

- 15.5p1에서 [재귀]: Portable0.0은 건너뜁니다. - [#6105](https://github.com/NuGet/Home/issues/6105)
- 복원 후 패키지의 자산이 누락되었습니다. - [#5995](https://github.com/NuGet/Home/issues/5995)
- 공백이 포함된 URI를 사용하는 경우 플러그 인 자격 증명 공급자가 작동하지 않습니다. - [#5982](https://github.com/NuGet/Home/issues/5982)
- 패키지를 복원하지 못하면 최소 세부 정보 표시를 ON으로 설정해도 출력에 오류가 출력됩니다. - [#5658](https://github.com/NuGet/Home/issues/5658)
- 솔루션 수준의 dotnet restore에서 ReferenceOutputAssembly가 false인 ProjectReference를 따르지 않아 임의 빌드가 실패합니다. - [#5490](https://github.com/NuGet/Home/issues/5490)
- PMC의 자동 완성이 개체 메서드에서 제대로 작동하지 않습니다. - [#4800](https://github.com/NuGet/Home/issues/4800)
- Visual Studio 2015 도구 집합으로 인해 nuget.exe restore가 실패합니다. - [#4713](https://github.com/NuGet/Home/issues/4713)
- perf - pmc는 VS2017에서 인스턴스화하는 데 비용이 많이 듭니다. - [#4205](https://github.com/NuGet/Home/issues/4205)
- 저속 연결에서 종속성 정보를 가져오는 데 시간이 많이 걸립니다. - [#4089](https://github.com/NuGet/Home/issues/4089)
- 여러 패키지에서 일반적인 종속성을 공유하면 uninstall-package w/ -RemoveDependencies가 실패합니다. - [#4026](https://github.com/NuGet/Home/issues/4026)
- 게시를 위해 NuGet.Core.nupkg를 완료합니다. - [#3581](https://github.com/NuGet/Home/issues/3581)
- csproj + project.json에 -IncludeProjectReferences를 사용하면 NuGet 팩에서 디렉터리 이름의 종속성 ID를 확인합니다. - [#3566](https://github.com/NuGet/Home/issues/3566)
- 'NuGet.ProxyCache'에 대한 형식 이니셜라이저에서 예외를 throw했습니다. - [#3144](https://github.com/NuGet/Home/issues/3144)
- Kudu를 사용한 nuget restore 성능이 저하되는 문제가 있습니다. - [#3087](https://github.com/NuGet/Home/issues/3087)
- 검색이 Blob 등록보다 먼저 수행되면 UI 클라이언트에서 오류 또는 경고를 표시하지 못합니다. - [#2149](https://github.com/NuGet/Home/issues/2149)
- Get-Packages - 업데이트에서 잘못된 쿼리를 생성합니다. - [#2135](https://github.com/NuGet/Home/issues/2135)

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>4.5 RTM에서 수정된 GitHub 문제에 대한 링크

[문제 목록](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
