---
title: "NuGet 에코시스템 개요 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 소스, 비 Microsoft NuGet 프로젝트, 유틸리티 및 교육 자료를 포함하여 NuGet 에코시스템에 있는 포괄적인 리소스입니다."
keywords: "NuGet 에코시스템, 비 Microsoft NuGet 프로젝트, NuGet 오픈 소스, NuGet 유틸리티, NuGet 교육 자료"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7c1e457c034f239fbea4e75f24851ea38182a294
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>NuGet 에코시스템 개요

2010을 소개하므로 NuGet에서는 개발 프로세스의 다양한 측면을 개선하고 자동화하는 좋은 기회를 제공합니다.

NuGet이 허용 [Apache v2 라이선스](http://choosealicense.com/licenses/apache/) 하의 오픈 소스이기 때문에 다른 프로젝트에서는 NuGet를 활용할 수 있고 회사는 해당 제품에서 지원을 빌드할 수 있습니다. 오픈 소스 프로젝트나 엔터프라이즈 응용 프로그램 개발에서 NuGet 및 NuGet 주위에 빌드되는 다른 응용 프로그램은 소프트웨어 개발 프로세스를 향상시키기 위한 도구의 광범위한 에코시스템을 제공합니다.

이러한 프로젝트는 모두 개발자 기여로 인해 혁신할 수 있습니다. NuGet 자체에 기여한 것처럼 가능한 경우 오류 및 새로운 기능 아이디어를 보고하고, 피드백을 제공하고, 설명서를 작성하고, 코드에 기여하여 이러한 프로젝트에 참여할 수 있습니다.

## <a name="net-foundation-projects"></a>.NET Foundation 프로젝트

NuGet은 Microsoft 개발 플랫폼에 대한 체험용 오픈 소스 패키지 관리 시스템을 제공합니다. [공식 NuGet 갤러리](http://www.nuget.org)를 구성하는 서비스 집합뿐만 아니라 몇 가지 클라이언트 도구로 구성됩니다. 이 항목이 결합되어 [.NET Foundation](http://www.dotnetfoundation.org/)에 의해 제어되는 NuGet 프로젝트를 형성합니다.

NuGet 조직에는 GitHub에 대한 다양한 저장소가 포함됩니다. [https://github.com/Nuget/Home](https://github.com/Nuget/Home)에서는 모든 리포지토리에 대한 개요 및 다양한 NuGet 구성 요소를 찾을 수 있는 위치를 제공합니다.

## <a name="microsoft-projects"></a>Microsoft 프로젝트

Microsoft에서는 NuGet을 개발하는 데 광범위하게 기여했습니다. Microsoft 직원들이 수행한 모든 노력은 오픈 소스이며 .NET Foundation에 제공됩니다(저작권 포함).

## <a name="non-microsoft-projects"></a>타사 프로젝트

다른 개인 및 회사에서도 NuGet 에코시스템에 상당히 기여했습니다. 여기에 나열된 각 프로젝트에서는 주요 NuGet 구성 요소와 다른 라이선스를 사용할 수 있습니다. 따라서 사용하기 전에 사용 약관을 허용할 수 있는지 확인합니다.

- [AppVeyor CI](https://www.appveyor.com/)
- [Artifactory](https://www.jfrog.com/artifactory/)
- [BoxStarter](http://boxstarter.org/)
- [Chocolatey](https://chocolatey.org/)
- [CoApp](http://coapp.org/)
- [JetBrains ReSharper](https://resharper-plugins.jetbrains.com/)
- [JetBrains TeamCity](https://www.jetbrains.com/teamcity/)
- [Klondike](https://github.com/themotleyfool/Klondike)
- [MinimalNugetServer](https://github.com/TanukiSharp/MinimalNugetServer)
- [MyGet(또는 NuGet-as-a-service)](http://www.myget.org/)
- [NuGet 패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [NuGet 서버](http://nugetserver.net/)
- [OctopusDeploy](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet(Inedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [SharpDevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin 및 MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>기타 NuGet 기반 유틸리티

NuGet에 기반한 도구 및 유틸리티는 다음과 같습니다.

- [슬라이드 확장](http://getglimpse.com/Packages)(플러그 인이 패키지)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Orchard](http://www.orchardproject.net/)(Orchard 갤러리에서 호스트되는 v1 NuGet 피드에서 CMS 모듈을 가져옴)
- [NuGet 서버의 Java 구현](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest)(새 패키지 게시를 트윗하는 Twitter 봇)
- [DefinitelyTyped](http://definitelytyped.org/)([자동](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript 형식 [NuGet에 게시된 정의](http://www.nuget.org/packages?q=DefinitelyTyped))

## <a name="training-materials-and-references"></a>교육 자료 및 참조

일반적으로 새로운 도구 또는 기술을 사용하면 학습 곡선이 함께 제공됩니다. 다행히 NuGet의 학습 곡선은 가파르지 않습니다. 실제로 신속하게 [패키지를 사용하기 시작](../quickstart/use-a-package.md)할 수 있습니다.

즉, 자동화된 빌드 및 배포 프로세스에서 NuGet과 함께 패키지를 작성하려면(특히 양호한 패키지) 다음 리소스에 좀 더 많은 시간을 들여야 합니다.

- [NuGet 블로그](http://blog.nuget.org/)
- [Twitter의 NuGet 팀@nuget](http://twitter.com/nuget)
- 서적:
  - [Apress Pro NuGet](http://bit.ly/ProNuGet)
  - [NuGet 2 Essentials](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>개별 패키지에 대한 설명서

[NuDoq](http://nudoq.org)은 NuGet 패키지에 대한 액세스와 업데이트 및 설명서를 간단하게 제공합니다.

NuDoq는 정기적으로 최신 패키지 업데이트에 nuget.org 갤러리 서버를 폴링하고, 라이브러리 설명서 파일을 처리하고, 그에 따라 사이트를 업데이트합니다.

## <a name="adding-your-project"></a>프로젝트 추가

이 페이지에 추가되는 NuGet 에코시스템 프로젝트가 있는 경우 이 페이지를 편집하는 끌어오기 요청을 제출하세요.
