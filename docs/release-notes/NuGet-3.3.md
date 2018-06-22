---
title: NuGet 3.3 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 3.3에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: adf193437de237ed32da481e627552a8dba6f656
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821566"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="b0461-103">NuGet 3.3 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="b0461-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="b0461-104">[3.2.1 NuGet 릴리스 정보](../release-notes/nuget-3.2.1.md) | [NuGet 3.4 RC 릴리스 정보](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="b0461-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="b0461-105">NuGet 3.3에 많은 수의 사용자 인터페이스 업데이트 및 명령줄 기능으로는 NuGet 클라이언트에 유용한 수정 프로그램의 모음 2015 년 11 월 30 일에 발표 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b0461-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="b0461-106">새 기능</span><span class="sxs-lookup"><span data-stu-id="b0461-106">New Features</span></span>

* <span data-ttu-id="b0461-107">NuGet 명령줄 클라이언트는 인증 된 피드를 원활 하 게 작업할 수 있게 되기를 허용 하는 자격 증명 공급자 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b0461-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="b0461-108">[Visual Studio Team Services를 설치 하는 방법에 대 한 지침 공급자 자격 증명 ](../api/nuget-exe-credential-providers.md) NuGet 구성 NuGet 문서에서 사용할 수 있는 클라이언트가 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0461-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../api/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="b0461-109">새로운 사용자 인터페이스 기능</span><span class="sxs-lookup"><span data-stu-id="b0461-109">New User Interface Features</span></span>

* <span data-ttu-id="b0461-110">찾아보기, 설치 됨, 및 업데이트를 사용할 수 있는 별도 탭</span><span class="sxs-lookup"><span data-stu-id="b0461-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="b0461-111">사용 가능한 업데이트가 있는 패키지 수를 나타내는 사용할 수 있는 배지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0461-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="b0461-112">패키지를 패키지가 설치 되어 있는지를 나타내는 패키지 목록에 배지 또는 사용 가능한 업데이트가</span><span class="sxs-lookup"><span data-stu-id="b0461-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="b0461-113">개수 및 패키지 목록에 추가 하는 작성자를 다운로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0461-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="b0461-114">사용할 수 있는 버전 번호가 가장 높은 및 패키지 목록에 현재 설치 된 버전 번호</span><span class="sxs-lookup"><span data-stu-id="b0461-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="b0461-115">업데이트 하 고 패키지 목록에서 제거 하는 빠른 설치를 허용 하도록 실행 단추</span><span class="sxs-lookup"><span data-stu-id="b0461-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="b0461-116">패키지 세부 정보 패널에 더 명확 하 게 실행 단추</span><span class="sxs-lookup"><span data-stu-id="b0461-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="b0461-117">패키지 세부 정보 패널에 패키지 업데이트 날짜</span><span class="sxs-lookup"><span data-stu-id="b0461-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="b0461-118">솔루션 뷰 패널 통합</span><span class="sxs-lookup"><span data-stu-id="b0461-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="b0461-119">프로젝트 및 솔루션 뷰에 설치 된 버전 번호의 정렬 가능한 표</span><span class="sxs-lookup"><span data-stu-id="b0461-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="b0461-120">새로운 명령줄 기능</span><span class="sxs-lookup"><span data-stu-id="b0461-120">New Command-line Features</span></span>

<span data-ttu-id="b0461-121">이 버전에서 도입 되었습니다는 `add` 및 `init` 명령에 설명 된 대로 폴더 기반 저장소를 초기화 하는 [nuget.exe 참조](../tools/nuget-exe-cli-reference.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0461-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="b0461-122">생성 되 고이 폴더와 유지 관리 하는 저장소는 구조 [성능을 크게 향상](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) 블로그에서에 설명 된 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b0461-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="b0461-123">콘텐츠 파일</span><span class="sxs-lookup"><span data-stu-id="b0461-123">ContentFiles</span></span>

<span data-ttu-id="b0461-124">콘텐츠를 사용할 수 이제 `project.json` 관리 되는 새로운 프로젝트 `contentFiles` 폴더 및 `.nuspec` `contentFiles` 요소 표기법입니다.</span><span class="sxs-lookup"><span data-stu-id="b0461-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="b0461-125">이 콘텐츠는 프로젝트 시스템과 상호 작용에 대 한 패키지 작성자가 보다 직접 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0461-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="b0461-126">콘텐츠 파일을 구성 하는 방법에 대 한 자세한 정보는 `.nuspec` 문서에서 확인할 수 있습니다는 [.nuspec 참조](../reference/nuspec.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0461-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="b0461-127">NuGet 지역 캐시 관리</span><span class="sxs-lookup"><span data-stu-id="b0461-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="b0461-128">명령줄 NuGet 워크스테이션에서 로컬 캐시를 관리 하는 방법에 대 한 정보를 포함 하도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b0461-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="b0461-129">지역 명령에 대 한 자세한 정보가 표시 됩니다는 [NuGet 명령줄 참조](../tools/cli-ref-locals.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0461-129">More information about the locals command is available in the [NuGet command-line reference](../tools/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="b0461-130">해결 된 문제</span><span class="sxs-lookup"><span data-stu-id="b0461-130">Fixed Issues</span></span>

<span data-ttu-id="b0461-131">**주목할 만한 문제**</span><span class="sxs-lookup"><span data-stu-id="b0461-131">**Notable Issues**</span></span>

* <span data-ttu-id="b0461-132">NuGet 복원에 대 한 명령줄 복원된 지원 모노-에 솔루션 파일이 포함 된 패키지 [1543](https://github.com/NuGet/Home/issues/1543)</span><span class="sxs-lookup"><span data-stu-id="b0461-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="b0461-133">GitHub에서의 전체 목록은 3.3 릴리스에서 해결 된 문제를 찾을 수는 [3.3 마일스 톤](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0461-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="b0461-134">3.3 명령줄 릴리스에서 해결 된 문제 목록에 기록 되는 [3.3 명령줄 마일스 톤](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)합니다.</span><span class="sxs-lookup"><span data-stu-id="b0461-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="b0461-135">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="b0461-135">Known Issues</span></span>

<span data-ttu-id="b0461-136">찾을 수 있는 GitHub 문제 목록에서 문제 추적 계속 합니다. [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="b0461-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>