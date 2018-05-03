---
title: NuGet 3.0 RC 릴리스 정보
description: NuGet 3.0 RC 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 28ac49d9e9071d16d20b24808abb0acaab214ffd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="75233-103">NuGet 3.0 RC 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="75233-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="75233-104">[NuGet 3.0 베타 릴리스 정보](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 릴리스 정보](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="75233-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="75233-105">NuGet 3.0 RC와 Visual Studio 2015 RC 릴리스 2015 년 4 월 29 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="75233-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="75233-106">이 릴리스에 다양 한 중요 한 버그 수정, 성능 향상 및 새 프레임 워크를 지 원하는 업데이트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75233-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="75233-107">Visual Studio 2015 용만 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="75233-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="75233-108">성능에 계속된 포커스가</span><span class="sxs-lookup"><span data-stu-id="75233-108">Continued Focus on Performance</span></span>

<span data-ttu-id="75233-109">NuGet 쿼리의 안정성과 성능을 계속에 집중 하는 활성 항목 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="75233-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="75233-110">이 릴리스에서 NuGet UI와 웹 사이트에서 매우 빠른 검색 작업을 보려면 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="75233-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="75233-111">서비스와 이러한 작업을 튜닝에 도움이 될 수 있도록 서비스 사용을 모니터링 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="75233-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="75233-112">중요 한 문제 해결</span><span class="sxs-lookup"><span data-stu-id="75233-112">Significant Issues Resolved</span></span>

<span data-ttu-id="75233-113">NuGet 클라이언트가 안정화 하기 위해이 릴리스의 일부로 서 다양 한 문제 해결.</span><span class="sxs-lookup"><span data-stu-id="75233-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="75233-114">간략 한 목록만 더 중요 한 문제를 해결 중 일부는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="75233-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="75233-115">ASP.NET 5에 대 한 K 프레임 워크의 이름 바꾸기의 일환으로, 프레임 워크 모니커 하도록 업데이트 되었습니다 dnx 및 dnxcore 처리 [링크](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="75233-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="75233-116">Visual Studio UI에서 링크에서 도움말 문서 추가 [링크](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="75233-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="75233-117">복잡 한 참조를 더 잘 처리 `.nuspec` 쉼표로 구분 된 프레임 워크 참조와 [링크](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="75233-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="75233-118">일본어 culture에 대 한 지원 고정 [링크](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="75233-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="75233-119">ASP.NET 5 프로젝트에서 새 v3 끝점을 사용 하려면 업데이트 된 클라이언트 [링크](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="75233-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="75233-120">소스 제어와 핸들을 보다 잘 업데이트 된 패키지 폴더 [링크](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="75233-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="75233-121">위성 패키지에 대 한 지원 고정 [링크](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="75233-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="75233-122">프레임 워크 관련 콘텐츠 파일에 대 한 지원을 수정 [링크](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="75233-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="75233-123">GitHub 존재 정비</span><span class="sxs-lookup"><span data-stu-id="75233-123">GitHub presence overhaul</span></span>

<span data-ttu-id="75233-124">일부 변경 내용을 만들었고 우리의 [GitHub에서 코드 저장소를 원본](http://github.com/nuget/home)합니다.</span><span class="sxs-lookup"><span data-stu-id="75233-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="75233-125">Visual Studio 클라이언트, Powershell 명령 또는 명령줄 문제가 있는 경우 실행 문제 별로 로그 있고에서 진행 상황을 모니터링 우리의 [홈 GitHub 리포지토리 문제 목록](http://github.com/nuget/home/issues)합니다.</span><span class="sxs-lookup"><span data-stu-id="75233-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="75233-126">갤러리에 대 한 문제를 추적 하는 것이 [GitHub NuGetGallery 리포지토리](http://github.com/nuget/NuGetGallery/issues)합니다.</span><span class="sxs-lookup"><span data-stu-id="75233-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="75233-127">기대</span><span class="sxs-lookup"><span data-stu-id="75233-127">Stay Tuned</span></span>

<span data-ttu-id="75233-128">에 유의 하십시오 [블로그에서](http://blog.nuget.org) 자세한 진행률 및 NuGet 3.0에 대 한 공지 사항!</span><span class="sxs-lookup"><span data-stu-id="75233-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>