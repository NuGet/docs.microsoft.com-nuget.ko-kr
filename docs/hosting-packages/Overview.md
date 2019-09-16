---
title: 사용자 고유의 NuGet 피드 호스팅 개요
description: 로컬 또는 원격으로 사용자 고유의 NuGet 패키지 피드 또는 갤러리를 호스팅하기 위한 개요입니다.
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 10651e2cc26f7df4115e4de5dac8c91c93af7374
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815297"
---
# <a name="hosting-your-own-nuget-feeds"></a>사용자 고유의 NuGet 피드 호스팅

패키지를 공개적으로 제공하는 대신 사용자의 조직 또는 작업 그룹 등 제한된 사용자에게만 패키지를 릴리스하려고 합니다. 또한 일부 회사에서는 개발자가 사용할 타사 라이브러리를 제한하고 이에 따라 해당 개발자가 nuget.org가 아닌 제한된 패키지 소스에서 그리도록 지시할 수 있습니다.

NuGet은 이러한 모든 용도에서 다음과 같은 방법으로 개인 패키지 소스를 설정하도록 지원합니다.

- 로컬 피드: 패키지는 계층적 폴더 구조를 만드는 `nuget init` 및 `nuget add`를 사용하여 적합한 네트워크 파일 공유에 배치합니다(NuGet 3.3+). 자세한 내용은 [로컬 피드](../hosting-packages/local-feeds.md)를 참조하세요.
- NuGet.Server: 로컬 HTTP 서버를 통해 패키지를 사용할 수 있습니다. 자세한 내용은 [NuGet.Server](../hosting-packages/nuget-server.md)를 참조하세요.
- NuGet 갤러리: [NuGet 갤러리 프로젝트](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps)를 사용하여 인터넷 서버에서 패키지를 호스트합니다(github.com). NuGet 갤러리에서는 nuget.org와 비슷하게 브라우저 내에서 패키지를 검색하고 탐색할 수 있는 광범위한 웹 UI와 같은 사용자 관리 및 기능을 제공합니다.

또한 원격 프라이빗 피드를 지원하는 [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) 및 [GitHub 패키지 레지스트리](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)와 같은 몇 가지 다른 NuGet 호스팅 제품이 있습니다. 다음은 이와 같은 제품의 목록입니다.

- JFrog의 [Artifactory](https://www.jfrog.com/artifactory/)
- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish): Team Foundation Server 2017 이상에서도 사용할 수 있습니다.
- [BaGet](https://github.com/loic-sharma/BaGet), ASP.NET Core에 빌드된 NuGet V3 서버의 오픈 소스 구현
- [Cloudsmith](https://cloudsmith.io/l/nuget-feed/), 완전 관리형 패키지 관리 SaaS
- [GitHub 패키지 레지스트리](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [LiGet](https://github.com/ai-traders/liget), Docker의 kestrel에서 실행되는 NuGet V2 서버의 오픈 소스 구현
- [MyGet](http://myget.org)
- Sonatype의 [Nexus](http://www.sonatype.org/nexus/)
- [NuGet 서버(오픈 소스)](http://nuget-server.net), Inedo의 NuGet 서버와 비슷한 오픈 소스 구현
- [NuGet 서버](http://nugetserver.net/), Inedo의 커뮤니티 프로젝트
- Inedo의 [ProGet](http://inedo.com/proget)
- [Sleet](https://github.com/emgarten/sleet), 오픈 소스 NuGet V3 정적 피드 생성기
- JetBrains의 [TeamCity](https://www.jetbrains.com/teamcity/)

패키지를 호스팅하는 방법에 관계 없이 `NuGet.Config`에서 사용할 수 있는 원본 목록에 추가하여 액세스할 있습니다. [패키지 소스](../consume-packages/install-use-packages-visual-studio.md#package-sources)에 설명된 대로 Visual Studio 또는 [`nuget sources`](../reference/cli-reference/cli-ref-sources.md)를 사용하는 명령줄에서 수행할 수 있습니다. 원본의 경로는 로컬 폴더 경로 이름, 네트워크 이름 또는 URL일 수 있습니다.
