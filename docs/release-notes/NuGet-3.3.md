---
title: NuGet 3.3 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 3.3에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa8290c80cc500b59d1779bf76662c07382fd277
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813782"
---
# <a name="nuget-33-release-notes"></a><span data-ttu-id="f6cde-103">NuGet 3.3 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="f6cde-103">NuGet 3.3 Release Notes</span></span>

<span data-ttu-id="f6cde-104">Nuget [3.2.1 릴리스 정보](../release-notes/nuget-3.2.1.md) | [NUGET 3.4-RC 릴리스 정보](../release-notes/nuget-3.4-RC.md)</span><span class="sxs-lookup"><span data-stu-id="f6cde-104">[NuGet 3.2.1 Release Notes](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md)</span></span>

<span data-ttu-id="f6cde-105">NuGet 3.3는 NuGet 클라이언트에 대 한 유용한 픽스 모음 뿐만 아니라 많은 사용자 인터페이스 업데이트 및 명령줄 기능을 사용 하 여 11 월 30 2015 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f6cde-105">NuGet 3.3 was released November 30, 2015 with a significant number of user interface updates and command-line features as well as a collection of useful fixes to the NuGet clients.</span></span>

## <a name="new-features"></a><span data-ttu-id="f6cde-106">새 기능</span><span class="sxs-lookup"><span data-stu-id="f6cde-106">New Features</span></span>

* <span data-ttu-id="f6cde-107">NuGet 명령줄 클라이언트가 인증 된 피드를 사용 하 여 원활 하 게 작동할 수 있도록 하는 자격 증명 공급자가 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f6cde-107">Credential Providers have been introduced that allow NuGet command-line clients to be able to work seamlessly with an authenticated feed.</span></span> <span data-ttu-id="f6cde-108">[Visual Studio Team Services 자격 증명 공급자를 설치](../reference/extensibility/nuget-exe-credential-providers.md) 하 고 nuget 클라이언트를 사용 하도록 구성 하는 방법에 대 한 지침은 nuget 문서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6cde-108">[Instructions on how to install the Visual Studio Team Services credential provider ](../reference/extensibility/nuget-exe-credential-providers.md) and configure the NuGet clients to use it are available on NuGet Docs.</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="f6cde-109">새 사용자 인터페이스 기능</span><span class="sxs-lookup"><span data-stu-id="f6cde-109">New User Interface Features</span></span>

* <span data-ttu-id="f6cde-110">찾아보기, 설치 및 업데이트 사용 가능 탭 분리</span><span class="sxs-lookup"><span data-stu-id="f6cde-110">Separate Browse, Installed, and Updates Available tabs</span></span>
* <span data-ttu-id="f6cde-111">사용 가능한 업데이트가 있는 패키지 수를 나타내는 사용 가능한 배지 업데이트</span><span class="sxs-lookup"><span data-stu-id="f6cde-111">Updates Available badge indicating the number of packages with available updates</span></span>
* <span data-ttu-id="f6cde-112">패키지가 설치 되어 있거나 업데이트를 사용할 수 있는지 여부를 나타내는 패키지 목록에서 배지 패키지</span><span class="sxs-lookup"><span data-stu-id="f6cde-112">Package badges in the package list to indicate if the package is installed or has an update available</span></span>
* <span data-ttu-id="f6cde-113">패키지 목록에 추가 된 다운로드 수 및 만든이</span><span class="sxs-lookup"><span data-stu-id="f6cde-113">Download count and author added to the package list</span></span>
* <span data-ttu-id="f6cde-114">패키지 목록에서 사용 가능한 가장 높은 버전 번호 및 현재 설치 된 버전 번호</span><span class="sxs-lookup"><span data-stu-id="f6cde-114">Highest available version number and currently installed version number on the package list</span></span>
* <span data-ttu-id="f6cde-115">패키지 목록에서 빠른 설치, 업데이트 및 제거를 허용 하는 작업 단추</span><span class="sxs-lookup"><span data-stu-id="f6cde-115">Action buttons to allow quick install, update, and uninstall from the package list</span></span>
* <span data-ttu-id="f6cde-116">패키지 세부 정보 패널의 보다 선명한 작업 단추</span><span class="sxs-lookup"><span data-stu-id="f6cde-116">Clearer action buttons on the package detail panel</span></span>
* <span data-ttu-id="f6cde-117">패키지 세부 정보 패널의 패키지 업데이트 날짜</span><span class="sxs-lookup"><span data-stu-id="f6cde-117">Package update date on the package detail panel</span></span>
* <span data-ttu-id="f6cde-118">솔루션 보기에서 패널 통합</span><span class="sxs-lookup"><span data-stu-id="f6cde-118">Consolidate panel in Solution view</span></span>
* <span data-ttu-id="f6cde-119">솔루션 보기에서 프로젝트 및 설치 된 버전 번호의 정렬 가능한 표</span><span class="sxs-lookup"><span data-stu-id="f6cde-119">Sortable grid of projects and installed version numbers on the solution view</span></span>

## <a name="new-command-line-features"></a><span data-ttu-id="f6cde-120">새 명령줄 기능</span><span class="sxs-lookup"><span data-stu-id="f6cde-120">New Command-line Features</span></span>

<span data-ttu-id="f6cde-121">이 버전에는 [nuget.exe 참조](../reference/nuget-exe-cli-reference.md)에 설명 된 대로 폴더 기반 리포지토리를 초기화 하는 `add` 및 `init` 명령이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f6cde-121">In this version we introduced the `add` and `init` commands to initialize folder-based repositories as described in the [nuget.exe reference](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="f6cde-122">이 폴더 구조를 사용 하 여 생성 및 유지 관리 되는 리포지토리는 블로그에 설명 된 대로 [상당한 성능 이점을 제공](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) 합니다.</span><span class="sxs-lookup"><span data-stu-id="f6cde-122">Repositories that are constructed and maintained with this folder structure will [deliver significant performance benefits](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) as outlined on our blog.</span></span>

## <a name="contentfiles"></a><span data-ttu-id="f6cde-123">ContentFiles</span><span class="sxs-lookup"><span data-stu-id="f6cde-123">ContentFiles</span></span>

<span data-ttu-id="f6cde-124">이제 새 `contentFiles` 폴더 및 `.nuspec` `contentFiles` 요소 표기법을 통해 관리 되는 프로젝트 `project.json`에서 콘텐츠가 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6cde-124">Content is now supported in `project.json` managed projects through the new `contentFiles` folder and `.nuspec` `contentFiles` element notation.</span></span>  <span data-ttu-id="f6cde-125">이 콘텐츠는 프로젝트 시스템과의 상호 작용을 위해 패키지 작성자가 직접 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6cde-125">This content can be more directly specified by the package author for interactions with project systems.</span></span>  <span data-ttu-id="f6cde-126">`.nuspec` 문서에서 contentFiles를 구성 하는 방법에 대 한 자세한 내용은 [Nuspec 참조](../reference/nuspec.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6cde-126">More information about how to configure contentFiles in a `.nuspec` document can be found in the [.nuspec Reference](../reference/nuspec.md).</span></span>

## <a name="nuget-locals-cache-management"></a><span data-ttu-id="f6cde-127">NuGet 로컬 캐시 관리</span><span class="sxs-lookup"><span data-stu-id="f6cde-127">NuGet Locals Cache Management</span></span>

<span data-ttu-id="f6cde-128">NuGet 명령줄은 워크스테이션에서 로컬 캐시를 관리 하는 방법에 대 한 정보를 포함 하도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f6cde-128">The NuGet command-line has been updated to include information about how to manage the local caches on a workstation.</span></span>  <span data-ttu-id="f6cde-129">로컬 명령에 대 한 자세한 내용은 [NuGet 명령줄 참조](../reference/cli-reference/cli-ref-locals.md)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6cde-129">More information about the locals command is available in the [NuGet command-line reference](../reference/cli-reference/cli-ref-locals.md).</span></span>

## <a name="fixed-issues"></a><span data-ttu-id="f6cde-130">해결 된 문제</span><span class="sxs-lookup"><span data-stu-id="f6cde-130">Fixed Issues</span></span>

<span data-ttu-id="f6cde-131">**주목할 만한 문제**</span><span class="sxs-lookup"><span data-stu-id="f6cde-131">**Notable Issues**</span></span>

* <span data-ttu-id="f6cde-132">NuGet 명령줄 복원- [1543](https://github.com/NuGet/Home/issues/1543) 의 솔루션 파일을 사용 하 여 패키지 복원 지원</span><span class="sxs-lookup"><span data-stu-id="f6cde-132">NuGet command-line restored support for restoring packages with a solution file on Mono - [1543](https://github.com/NuGet/Home/issues/1543)</span></span>

<span data-ttu-id="f6cde-133">3\.3 릴리스에서 해결 된 문제에 대 한 전체 목록은 GitHub의 [3.3 마일스 톤](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f6cde-133">The complete list of issues that were addressed in the 3.3 release can be found on GitHub under the [3.3 milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).</span></span>

<span data-ttu-id="f6cde-134">3\.3 명령줄 릴리스에서 해결 된 문제 목록은 [3.3 명령줄 마일스 톤](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)에 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f6cde-134">The list of issues fixed in the 3.3 command-line release are recorded in the [3.3 Command-Line milestone](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).</span></span>

## <a name="known-issues"></a><span data-ttu-id="f6cde-135">알려진 문제점</span><span class="sxs-lookup"><span data-stu-id="f6cde-135">Known Issues</span></span>

<span data-ttu-id="f6cde-136">Microsoft는 GitHub 문제 목록에서 찾을 수 있는 문제를 계속 추적 합니다. [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="f6cde-136">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>