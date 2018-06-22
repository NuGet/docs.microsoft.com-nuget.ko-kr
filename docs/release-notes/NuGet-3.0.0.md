---
title: NuGet 3.0 릴리스 정보
description: NuGet 3.0.0 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 26236c2db0e1a6be9c660905db567d9ebbbbe377
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820292"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="54597-103">NuGet 3.0 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="54597-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="54597-104">[NuGet 3.0 RC2 릴리스 정보](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 릴리스 정보](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="54597-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="54597-105">NuGet 3.0 2015 년 7 월 20 일에 Visual Studio 2015에 대 한 번들 확장으로 릴리스 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="54597-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="54597-106">Visual Studio와 함께이 릴리스를 전체 업데이트 된 NuGet 3.0 환경을 새 Visual Studio 사용자에 대해 사용할 수 있도록 제공 푸시되.</span><span class="sxs-lookup"><span data-stu-id="54597-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="54597-107">이 NuGet 확장 버전은 Visual Studio 2015에 사용할 수만 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54597-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="54597-108">Windows 10 개발에 대 한 지원을 포함 하는 Visual Studio 2015 릴리스 직후 게시 업데이트 하는 것 처럼 사용할 수 있는 최신 버전에 대 한 Visual Studio 갤러리 업데이트에 액세스할 수 있는 개발자가 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="54597-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="54597-109">전체적으로 우리 3.0 버전에서 240 문제 닫히고 검토할 수 있습니다는 [문제 GitHub에서의 전체 목록은](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)합니다.</span><span class="sxs-lookup"><span data-stu-id="54597-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="54597-110">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="54597-110">Known Issues</span></span>

<span data-ttu-id="54597-111">여러 가지 알려진된 문제가이 릴리스에서 제공 했으며 이러한 항목을 모두 해결 우리의 예약 된 3.1 릴리스의 Windows 10 29th 년 7 월에 일치 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="54597-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="54597-112">이러한 알려진된 문제를 해결 하려면 해당 날짜 또는 그 이후에 갤러리에서 Visual Studio 확장 프로그램을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54597-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="54597-113">미리 보기 창에 "이를 다시 표시 안" 레이블 및 패키지 설명 창에 "작성자" 레이블에 대 한 번역을 제공 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="54597-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="54597-114">TFS를 사용 하 여 프로젝트에서 작업 하면 소스 제어, NuGet 없습니다 제시 패키지 관리자 사용자 인터페이스 Nuget.Config 파일은 읽기 전용으로 표시 된 경우.</span><span class="sxs-lookup"><span data-stu-id="54597-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="54597-115">**해결 방법** TFS에서 파일을 체크 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="54597-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="54597-116">Visual Studio 어두운 테마를 사용 하는 경우에 노란색 "다시 시작 막대" NuGet Powershell 창에서 텍스트 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="54597-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="54597-117">**해결 방법** Visual Studio 밝은 테마를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="54597-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="54597-118">주요 문제 해결의 요약</span><span class="sxs-lookup"><span data-stu-id="54597-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="54597-119">패키지 관리자 창을 새로 고칠 때 자주 네트워크 업데이트 호출</span><span class="sxs-lookup"><span data-stu-id="54597-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="54597-120">패키지 관리자에 보기를 설치를 변경 하면 스크롤 지연</span><span class="sxs-lookup"><span data-stu-id="54597-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="54597-121">백그라운드 스레드에서 네트워크 호출을 실행 해야</span><span class="sxs-lookup"><span data-stu-id="54597-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="54597-122">'미리 보기 창 표시 안 함' 확인란을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="54597-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="54597-123">추가 된 프로세스 프로세서 사용량을 줄이기 위해 조절</span><span class="sxs-lookup"><span data-stu-id="54597-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="54597-124">쉽게 이식 가능한 클래스 라이브러리 참조 처리</span><span class="sxs-lookup"><span data-stu-id="54597-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="54597-125">자동 완성 서비스에서 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="54597-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="54597-126">기본 인증 자격 증명을 다시 삽입 하는 업데이트</span><span class="sxs-lookup"><span data-stu-id="54597-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="54597-127">향상 된 오류 로깅</span><span class="sxs-lookup"><span data-stu-id="54597-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="54597-128">업데이트 패키지를 호출할 때 향상 된 powershell 오류 메시지</span><span class="sxs-lookup"><span data-stu-id="54597-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="54597-129">Windows 10에서 충돌을 방지 하기 위해 '옵션에 대 한 자세한 정보' 링크를 고정 합니다.</span><span class="sxs-lookup"><span data-stu-id="54597-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="54597-130">시험판 확인란 설정을 기억 합니다.</span><span class="sxs-lookup"><span data-stu-id="54597-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="54597-131">솔루션의 프로젝트에서 결과 캐시 하 여 향상 된 수집 성능</span><span class="sxs-lookup"><span data-stu-id="54597-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="54597-132">동시에 여러 패키지를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54597-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="54597-133">설치 패키지를 제거-강제로 명령</span><span class="sxs-lookup"><span data-stu-id="54597-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="54597-134">에 유의 하십시오 [블로그에서](http://blog.nuget.org) 자세한 진행률 및 공지에 대 한 대로 Windows 10 개발에 대 한 지원을 제공 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="54597-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>