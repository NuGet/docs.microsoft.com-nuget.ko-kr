---
title: "사용자 고유의 NuGet 피드 호스팅 개요 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/25/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 97577ddd-c294-432d-81a7-b4aebe88bd1c
description: "로컬 또는 원격으로 사용자 고유의 NuGet 패키지 피드 또는 갤러리를 호스팅하기 위한 개요입니다."
keywords: "NuGet 피드, NuGet 갤러리, 패키지 피드 사용자 지정, NuGet.Server"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: c3c6b17cdeb4fe959adbc56bdc6ace73202a98fc
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="hosting-your-own-nuget-feeds"></a><span data-ttu-id="704b7-104">사용자 고유의 NuGet 피드 호스팅</span><span class="sxs-lookup"><span data-stu-id="704b7-104">Hosting your own NuGet feeds</span></span>

<span data-ttu-id="704b7-105">패키지를 공개적으로 제공하는 대신 사용자의 조직 또는 작업 그룹 등 제한된 사용자에게만 패키지를 릴리스하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="704b7-105">Instead of making packages publicly available, you might want to release packages to only a limited audience, such as your organization or workgroup.</span></span> <span data-ttu-id="704b7-106">또한 일부 회사에서는 개발자가 사용할 타사 라이브러리를 제한하고 이에 따라 해당 개발자가 nuget.org가 아닌 제한된 패키지 소스에서 그리도록 지시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="704b7-106">In addition, some companies may want to restrict which third-party libraries their developers may use, and thus direct those developers to draw from a limited package source rather than nuget.org.</span></span>

<span data-ttu-id="704b7-107">NuGet은 이러한 모든 용도에서 다음과 같은 방법으로 개인 패키지 소스를 설정하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="704b7-107">For all such purposes, NuGet supports setting up private package sources in the following ways:</span></span>

- <span data-ttu-id="704b7-108">로컬 피드: 패키지는 계층적 폴더 구조를 만드는 `nuget init` 및 `nuget add`를 사용하여 적합한 네트워크 파일 공유에 배치합니다(NuGet 3.3+).</span><span class="sxs-lookup"><span data-stu-id="704b7-108">Local feed: Packages are simply placed on a suitable network file share, ideally using `nuget init` and `nuget add` to create a hierarchical folder structure (NuGet 3.3+).</span></span> <span data-ttu-id="704b7-109">자세한 내용은 [로컬 피드](../hosting-packages/local-feeds.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="704b7-109">For details, see [Local Feeds](../hosting-packages/local-feeds.md).</span></span>
- <span data-ttu-id="704b7-110">NuGet.Server: 로컬 HTTP 서버를 통해 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="704b7-110">NuGet.Server: Packages are made available through a local HTTP server.</span></span> <span data-ttu-id="704b7-111">자세한 내용은 [NuGet.Server](../hosting-packages/NuGet-Server.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="704b7-111">For details, see [NuGet.Server](../hosting-packages/NuGet-Server.md).</span></span>
- <span data-ttu-id="704b7-112">NuGet 갤러리: [NuGet 갤러리 프로젝트](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps)를 사용하여 인터넷 서버에서 패키지를 호스트합니다(github.com).</span><span class="sxs-lookup"><span data-stu-id="704b7-112">NuGet Gallery: Packages are hosted on an Internet server using the [NuGet Gallery Project](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com).</span></span> <span data-ttu-id="704b7-113">NuGet 갤러리에서는 nuget.org와 비슷하게 브라우저 내에서 패키지를 검색하고 탐색할 수 있는 광범위한 웹 UI와 같은 사용자 관리 및 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="704b7-113">NuGet Gallery provides user management and features such as an extensive web UI that allows searching and exploring packages from within the browser, similar to nuget.org.</span></span>

<span data-ttu-id="704b7-114">다음을 포함하여 원격 개인 피드를 지원하는 제품을 호스팅하는 다른 여러 NuGet이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="704b7-114">There are also several other NuGet hosting products that support remote private feeds, including the following:</span></span>

- <span data-ttu-id="704b7-115">[Visual Studio Team Services 패키지 관리](https://www.visualstudio.com/docs/package/nuget/publish)는 Team Foundation Server 2017 이상에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="704b7-115">[Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), which is also available on Team Foundation Server 2017 and later.</span></span>
- [<span data-ttu-id="704b7-116">MyGet</span><span class="sxs-lookup"><span data-stu-id="704b7-116">MyGet</span></span>](http://myget.org)
- <span data-ttu-id="704b7-117">Inedo의 [ProGet](http://inedo.com/proget)</span><span class="sxs-lookup"><span data-stu-id="704b7-117">[ProGet](http://inedo.com/proget) from Inedo</span></span>
- <span data-ttu-id="704b7-118">[NuGet 서버](http://nugetserver.net/), Inedo의 커뮤니티 프로젝트</span><span class="sxs-lookup"><span data-stu-id="704b7-118">[NuGet Server](http://nugetserver.net/), a community project from Inedo</span></span>
- <span data-ttu-id="704b7-119">[NuGet 서버(오픈 소스)](http://nuget-server.net), Inedo의 NuGet 서버와 비슷한 오픈 소스 구현</span><span class="sxs-lookup"><span data-stu-id="704b7-119">[NuGet Server (Open Source)](http://nuget-server.net), an open-source implementation similar to Inedo's NuGet Server</span></span>
- <span data-ttu-id="704b7-120">JFrog의 [Artifactory](https://www.jfrog.com/artifactory/)</span><span class="sxs-lookup"><span data-stu-id="704b7-120">[Artifactory](https://www.jfrog.com/artifactory/) from JFrog.</span></span>
- <span data-ttu-id="704b7-121">Sonatype의 [Nexus](http://www.sonatype.org/nexus/)</span><span class="sxs-lookup"><span data-stu-id="704b7-121">[Nexus](http://www.sonatype.org/nexus/) from Sonatype.</span></span>
- <span data-ttu-id="704b7-122">JetBrains의 [TeamCity](https://www.jetbrains.com/teamcity/)</span><span class="sxs-lookup"><span data-stu-id="704b7-122">[TeamCity](https://www.jetbrains.com/teamcity/) from JetBrains.</span></span>

<span data-ttu-id="704b7-123">패키지를 호스팅하는 방법에 관계 없이 `NuGet.Config`에서 사용할 수 있는 원본 목록에 추가하여 액세스할 있습니다.</span><span class="sxs-lookup"><span data-stu-id="704b7-123">Regardless of how packages are hosted, you access them by adding them to the list of available sources in `NuGet.Config`.</span></span> <span data-ttu-id="704b7-124">[패키지 소스](../tools/package-manager-ui.md#package-sources)에 설명된 대로 Visual Studio 또는 [`nuget sources`](../tools/cli-ref-sources.md)를 사용하는 명령줄에서 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="704b7-124">This can be done in Visual Studio as described in [Package Sources](../tools/package-manager-ui.md#package-sources), or from the command line using [`nuget sources`](../tools/cli-ref-sources.md).</span></span> <span data-ttu-id="704b7-125">원본의 경로는 로컬 폴더 경로 이름, 네트워크 이름 또는 URL일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="704b7-125">The path to a source can be a local folder pathname, a network name, or a URL.</span></span>