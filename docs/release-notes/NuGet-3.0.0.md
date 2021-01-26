---
title: NuGet 3.0 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 3.0.0를 포함 하는 NuGet에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4d4ce17c33dc38df5504a77d9cc3530d466d70af
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776556"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="33dec-103">NuGet 3.0 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="33dec-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="33dec-104">[NuGet 3.0 RC2 릴리스 정보](../release-notes/nuget-3.0-RC2.md)  |  [NuGet 3.1 릴리스 정보](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="33dec-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="33dec-105">NuGet 3.0는 Visual Studio 2015의 번들 확장으로 7 월 20 2015 일에 릴리스 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="33dec-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="33dec-106">새로운 Visual Studio 사용자에 게 업데이트 된 NuGet 3.0 환경을 완벽 하 게 사용할 수 있도록 Visual Studio에서이 릴리스를 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="33dec-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="33dec-107">이 NuGet 확장 버전은 Visual Studio 2015 에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33dec-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="33dec-108">Windows 10 개발에 대 한 지원이 포함 된 Visual Studio 2015 릴리스 직후 업데이트를 게시할 때 사용 가능한 최신 버전에 대 한 Visual Studio 갤러리 업데이트에 액세스할 수 있는 개발자를 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="33dec-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="33dec-109">총 240 3.0 릴리스에서 문제가 종결 되었으며 [GitHub에서 전체 문제 목록을](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33dec-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="33dec-110">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="33dec-110">Known Issues</span></span>

<span data-ttu-id="33dec-111">이 릴리스와 함께 제공 되는 알려진 문제에는 여러 가지가 있으며, 이러한 모든 항목은 7 월 29 일에 Windows 10 릴리스와 일치 하도록 예약 된 3.1 릴리스에서 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="33dec-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="33dec-112">이러한 알려진 문제를 해결 하기 위해 해당 날짜 또는 이후 갤러리에서 Visual Studio 확장을 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33dec-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="33dec-113">미리 보기 창에는 "다시 표시 안 함" 레이블과 패키지 설명 창에 "Authors" 레이블이 제공 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33dec-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="33dec-114">TFS 원본 제어를 사용 하 여 프로젝트에서 작업 하는 경우 Nuget.Config 파일이 읽기 전용으로 표시 된 경우 NuGet은 패키지 관리자 사용자 인터페이스를 표시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="33dec-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="33dec-115">**해결 방법** TFS에서 파일을 체크 아웃 합니다.</span><span class="sxs-lookup"><span data-stu-id="33dec-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="33dec-116">Visual Studio 어두운 테마를 사용 하는 경우 NuGet Powershell 창의 노란색 "다시 시작 표시줄" 텍스트는 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="33dec-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="33dec-117">**해결 방법** Visual Studio light 테마를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="33dec-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="33dec-118">해결 된 주요 문제 요약</span><span class="sxs-lookup"><span data-stu-id="33dec-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="33dec-119">패키지 관리자 창이 새로 고쳐질 때 네트워크 업데이트 호출이 자주 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="33dec-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="33dec-120">패키지 관리자에서 설치 된 뷰로 변경할 때 지연 된 스크롤</span><span class="sxs-lookup"><span data-stu-id="33dec-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="33dec-121">네트워크 호출은 백그라운드 스레드에서 실행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="33dec-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="33dec-122">' 미리 보기 창 표시 안 함 ' 확인란 추가 됨</span><span class="sxs-lookup"><span data-stu-id="33dec-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="33dec-123">프로세서 사용량을 줄이기 위해 프로세스 제한을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="33dec-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="33dec-124">이식 가능한 클래스 라이브러리 참조 처리 향상</span><span class="sxs-lookup"><span data-stu-id="33dec-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="33dec-125">자동 완성 서비스의 대/소문자 구분</span><span class="sxs-lookup"><span data-stu-id="33dec-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="33dec-126">기본 인증 자격 증명을 새로 소개할 업데이트</span><span class="sxs-lookup"><span data-stu-id="33dec-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="33dec-127">오류 로깅이 개선되었습니다.</span><span class="sxs-lookup"><span data-stu-id="33dec-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="33dec-128">업데이트 패키지를 호출할 때 향상 된 powershell 오류 메시지</span><span class="sxs-lookup"><span data-stu-id="33dec-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="33dec-129">Windows 10에서 충돌을 방지 하는 ' 옵션 정보 ' 링크를 수정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="33dec-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="33dec-130">시험판 확인란 설정 고려</span><span class="sxs-lookup"><span data-stu-id="33dec-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="33dec-131">솔루션의 프로젝트 간에 결과를 캐싱하여 수집 성능 향상</span><span class="sxs-lookup"><span data-stu-id="33dec-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="33dec-132">여러 패키지를 동시에 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="33dec-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="33dec-133">제거 되는 설치-패키지-force 명령</span><span class="sxs-lookup"><span data-stu-id="33dec-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="33dec-134">Windows 10 개발에 대 한 지원을 제공할 준비가 되 면 [블로그](http://blog.nuget.org) 에서 더 많은 진행률과 공지 사항을 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="33dec-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>