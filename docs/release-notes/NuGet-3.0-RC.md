---
title: NuGet 3.0 RC 릴리스 정보
description: NuGet 3.0 RC 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551721"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="d81fc-103">NuGet 3.0 RC 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="d81fc-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="d81fc-104">[NuGet 3.0 베타 릴리스 정보](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 릴리스 정보](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="d81fc-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="d81fc-105">NuGet 3.0 RC는 Visual Studio 2015 RC 릴리스를 사용 하 여 2015 년 4 월 29 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d81fc-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="d81fc-106">이 릴리스에 다양 한 중요 한 버그 수정, 성능 향상 및 새로운 프레임 워크를 지원 하도록 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="d81fc-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="d81fc-107">만 Visual Studio 2015 용 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d81fc-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="d81fc-108">성능에 계속된 집중</span><span class="sxs-lookup"><span data-stu-id="d81fc-108">Continued Focus on Performance</span></span>

<span data-ttu-id="d81fc-109">NuGet 쿼리의 성능과 안정성에 집중 하는 활성 항목 수를 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="d81fc-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="d81fc-110">이 릴리스에서 NuGet UI 및 웹 사이트에서 매우 빠른 검색 작업을 보려면 보아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d81fc-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="d81fc-111">서비스 및 이러한 작업을 튜닝할 계속 수 있도록 서비스를 사용 하는 방법을 모니터링 합니다.</span><span class="sxs-lookup"><span data-stu-id="d81fc-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="d81fc-112">중요 한 문제 해결</span><span class="sxs-lookup"><span data-stu-id="d81fc-112">Significant Issues Resolved</span></span>

<span data-ttu-id="d81fc-113">NuGet 클라이언트를 안정화를 하기 위해이 릴리스의 일환으로 다양 한 문제를 해결 했습니다.</span><span class="sxs-lookup"><span data-stu-id="d81fc-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="d81fc-114">방금 간략 한 목록을 확인 하는 더 중요 한 문제 중 일부는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d81fc-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="d81fc-115">ASP.NET 5 K 프레임 워크의 이름 바꾸기의 일환으로, 프레임 워크 모니커 하도록 업데이트 되었습니다 dnx 및 dnxcore 처리 [링크](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="d81fc-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="d81fc-116">Visual Studio UI의 링크 도움말 설명서가 추가 [링크](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="d81fc-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="d81fc-117">더 복잡 한 참조 처리 `.nuspec` 쉼표로 구분 된 프레임 워크 참조를 사용 하 여 [링크](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="d81fc-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="d81fc-118">일본어 culture에 대 한 지원을 고정 [링크](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="d81fc-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="d81fc-119">ASP.NET 5 프로젝트에서 새 v3 끝점을 사용 하려면 업데이트 된 클라이언트 [링크](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="d81fc-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="d81fc-120">소스 제어를 사용 하 여 핸들을 업데이트 된 패키지 폴더 [링크](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="d81fc-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="d81fc-121">위성 패키지에 대 한 지원을 고정 [링크](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="d81fc-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="d81fc-122">프레임 워크별 콘텐츠 파일에 대 한 지원 수정 [링크](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="d81fc-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="d81fc-123">GitHub 있는지 점검</span><span class="sxs-lookup"><span data-stu-id="d81fc-123">GitHub presence overhaul</span></span>

<span data-ttu-id="d81fc-124">일부 변경 내용을 만들었습니다 우리의 [GitHub에서 코드 리포지토리를 원본](http://github.com/nuget/home)합니다.</span><span class="sxs-lookup"><span data-stu-id="d81fc-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="d81fc-125">NuGet Visual Studio 클라이언트에서 Powershell 명령 또는 명령줄을 사용 하 여 문제가 발생 하는 경우 실행 이러한 문제를 로그 하에서 진행률을 모니터링할 우리의 [홈 GitHub 리포지토리 문제 목록](http://github.com/nuget/home/issues)합니다.</span><span class="sxs-lookup"><span data-stu-id="d81fc-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="d81fc-126">갤러리에 대 한 문제를 추적 하는 것이 [GitHub NuGetGallery 리포지토리](http://github.com/nuget/NuGetGallery/issues)합니다.</span><span class="sxs-lookup"><span data-stu-id="d81fc-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="d81fc-127">계속 주목해 주세요</span><span class="sxs-lookup"><span data-stu-id="d81fc-127">Stay Tuned</span></span>

<span data-ttu-id="d81fc-128">에 유의 하세요 [블로그에서](http://blog.nuget.org) 자세한 진행률 및 NuGet 3.0에 대 한 알림!</span><span class="sxs-lookup"><span data-stu-id="d81fc-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>