---
title: 사용자 고유의 NuGet 피드 호스팅 개요
description: 로컬 또는 원격으로 사용자 고유의 NuGet 패키지 피드 또는 갤러리를 호스팅하기 위한 개요입니다.
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 4741d780afa4fbe11001aed49a9f72bf608d96d9
ms.sourcegitcommit: a1846edf70ddb2505d58e536e08e952d870931b0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52303566"
---
# <a name="hosting-your-own-nuget-feeds"></a><span data-ttu-id="5ec7a-103">사용자 고유의 NuGet 피드 호스팅</span><span class="sxs-lookup"><span data-stu-id="5ec7a-103">Hosting your own NuGet feeds</span></span>

<span data-ttu-id="5ec7a-104">패키지를 공개적으로 제공하는 대신 사용자의 조직 또는 작업 그룹 등 제한된 사용자에게만 패키지를 릴리스하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec7a-104">Instead of making packages publicly available, you might want to release packages to only a limited audience, such as your organization or workgroup.</span></span> <span data-ttu-id="5ec7a-105">또한 일부 회사에서는 개발자가 사용할 타사 라이브러리를 제한하고 이에 따라 해당 개발자가 nuget.org가 아닌 제한된 패키지 소스에서 그리도록 지시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ec7a-105">In addition, some companies may want to restrict which third-party libraries their developers may use, and thus direct those developers to draw from a limited package source rather than nuget.org.</span></span>

<span data-ttu-id="5ec7a-106">NuGet은 이러한 모든 용도에서 다음과 같은 방법으로 개인 패키지 소스를 설정하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec7a-106">For all such purposes, NuGet supports setting up private package sources in the following ways:</span></span>

- <span data-ttu-id="5ec7a-107">로컬 피드: 패키지는 계층적 폴더 구조를 만드는 `nuget init` 및 `nuget add`를 사용하여 적합한 네트워크 파일 공유에 배치합니다(NuGet 3.3+).</span><span class="sxs-lookup"><span data-stu-id="5ec7a-107">Local feed: Packages are simply placed on a suitable network file share, ideally using `nuget init` and `nuget add` to create a hierarchical folder structure (NuGet 3.3+).</span></span> <span data-ttu-id="5ec7a-108">자세한 내용은 [로컬 피드](../hosting-packages/local-feeds.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ec7a-108">For details, see [Local Feeds](../hosting-packages/local-feeds.md).</span></span>
- <span data-ttu-id="5ec7a-109">NuGet.Server: 로컬 HTTP 서버를 통해 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ec7a-109">NuGet.Server: Packages are made available through a local HTTP server.</span></span> <span data-ttu-id="5ec7a-110">자세한 내용은 [NuGet.Server](../hosting-packages/nuget-server.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5ec7a-110">For details, see [NuGet.Server](../hosting-packages/nuget-server.md).</span></span>
- <span data-ttu-id="5ec7a-111">NuGet 갤러리: [NuGet 갤러리 프로젝트](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps)를 사용하여 인터넷 서버에서 패키지를 호스트합니다(github.com).</span><span class="sxs-lookup"><span data-stu-id="5ec7a-111">NuGet Gallery: Packages are hosted on an Internet server using the [NuGet Gallery Project](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span></span> <span data-ttu-id="5ec7a-112">NuGet 갤러리에서는 nuget.org와 비슷하게 브라우저 내에서 패키지를 검색하고 탐색할 수 있는 광범위한 웹 UI와 같은 사용자 관리 및 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5ec7a-112">NuGet Gallery provides user management and features such as an extensive web UI that allows searching and exploring packages from within the browser, similar to nuget.org.</span></span>

<span data-ttu-id="5ec7a-113">다음을 포함하여 원격 개인 피드를 지원하는 제품을 호스팅하는 다른 여러 NuGet이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ec7a-113">There are also several other NuGet hosting products that support remote private feeds, including the following:</span></span>

- <span data-ttu-id="5ec7a-114">[Visual Studio Team Services 패키지 관리](https://www.visualstudio.com/docs/package/nuget/publish)는 Team Foundation Server 2017 이상에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ec7a-114">[Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), which is also available on Team Foundation Server 2017 and later.</span></span>
- [<span data-ttu-id="5ec7a-115">MyGet</span><span class="sxs-lookup"><span data-stu-id="5ec7a-115">MyGet</span></span>](http://myget.org)
- <span data-ttu-id="5ec7a-116">Inedo의 [ProGet](http://inedo.com/proget)</span><span class="sxs-lookup"><span data-stu-id="5ec7a-116">[ProGet](http://inedo.com/proget) from Inedo</span></span>
- <span data-ttu-id="5ec7a-117">[NuGet 서버](http://nugetserver.net/), Inedo의 커뮤니티 프로젝트</span><span class="sxs-lookup"><span data-stu-id="5ec7a-117">[NuGet Server](http://nugetserver.net/), a community project from Inedo</span></span>
- <span data-ttu-id="5ec7a-118">[NuGet 서버(오픈 소스)](http://nuget-server.net), Inedo의 NuGet 서버와 비슷한 오픈 소스 구현</span><span class="sxs-lookup"><span data-stu-id="5ec7a-118">[NuGet Server (Open Source)](http://nuget-server.net), an open-source implementation similar to Inedo's NuGet Server</span></span>
- <span data-ttu-id="5ec7a-119">[LiGet](https://github.com/ai-traders/liget), Docker의 kestrel에서 실행되는 NuGet V2 서버의 오픈 소스 구현</span><span class="sxs-lookup"><span data-stu-id="5ec7a-119">[LiGet](https://github.com/ai-traders/liget), an open-source implementation of NuGet V2 server that runs on kestrel in docker</span></span>
- <span data-ttu-id="5ec7a-120">[BaGet](https://github.com/loic-sharma/BaGet), ASP.NET Core에 빌드된 NuGet V3 서버의 오픈 소스 구현</span><span class="sxs-lookup"><span data-stu-id="5ec7a-120">[BaGet](https://github.com/loic-sharma/BaGet), an open-source implementation of NuGet V3 server built on ASP.NET Core</span></span>
- <span data-ttu-id="5ec7a-121">[Sleet](https://github.com/emgarten/sleet), 오픈 소스 NuGet V3 정적 피드 생성기</span><span class="sxs-lookup"><span data-stu-id="5ec7a-121">[Sleet](https://github.com/emgarten/sleet), an open-source NuGet V3 static feed generator</span></span>
- <span data-ttu-id="5ec7a-122">JFrog의 [Artifactory](https://www.jfrog.com/artifactory/)</span><span class="sxs-lookup"><span data-stu-id="5ec7a-122">[Artifactory](https://www.jfrog.com/artifactory/) from JFrog.</span></span>
- <span data-ttu-id="5ec7a-123">Sonatype의 [Nexus](http://www.sonatype.org/nexus/)</span><span class="sxs-lookup"><span data-stu-id="5ec7a-123">[Nexus](http://www.sonatype.org/nexus/) from Sonatype.</span></span>
- <span data-ttu-id="5ec7a-124">JetBrains의 [TeamCity](https://www.jetbrains.com/teamcity/)</span><span class="sxs-lookup"><span data-stu-id="5ec7a-124">[TeamCity](https://www.jetbrains.com/teamcity/) from JetBrains.</span></span>

<span data-ttu-id="5ec7a-125">패키지를 호스팅하는 방법에 관계 없이 `NuGet.Config`에서 사용할 수 있는 원본 목록에 추가하여 액세스할 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ec7a-125">Regardless of how packages are hosted, you access them by adding them to the list of available sources in `NuGet.Config`.</span></span> <span data-ttu-id="5ec7a-126">[패키지 소스](../tools/package-manager-ui.md#package-sources)에 설명된 대로 Visual Studio 또는 [`nuget sources`](../tools/cli-ref-sources.md)를 사용하는 명령줄에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ec7a-126">This can be done in Visual Studio as described in [Package Sources](../tools/package-manager-ui.md#package-sources), or from the command line using [`nuget sources`](../tools/cli-ref-sources.md).</span></span> <span data-ttu-id="5ec7a-127">원본의 경로는 로컬 폴더 경로 이름, 네트워크 이름 또는 URL일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ec7a-127">The path to a source can be a local folder pathname, a network name, or a URL.</span></span>
