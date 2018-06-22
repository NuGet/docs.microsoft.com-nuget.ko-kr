---
title: NuGet 2.6.1 WebMatrix 릴리스 정보
description: 2.6.1의 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 WebMatrix 용 NuGet에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3d767788d348553cbb5cb82c6f70aac1894628c3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31818407"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="5f381-103">NuGet 2.6.1 WebMatrix 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="5f381-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="5f381-104">[NuGet 2.6 릴리스 정보](../release-notes/nuget-2.6.md) | [NuGet 2.7 릴리스 정보](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="5f381-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="5f381-105">NuGet 팀 WebMatrix 용 2014 년 3 월 26 일에 업데이트 된 NuGet 패키지 관리자 확장을 릴리스 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="5f381-106">이 업데이트에서 설치할 수 있습니다는 [WebMatrix 확장 갤러리](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) 다음 단계를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="5f381-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="5f381-107">열기 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="5f381-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="5f381-108">홈 리본에서 확장 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="5f381-109">업데이트 탭을 선택</span><span class="sxs-lookup"><span data-stu-id="5f381-109">Select the Updates tab</span></span>
1. <span data-ttu-id="5f381-110">2.6.1에 NuGet 패키지 관리자를 업데이트 하려면 클릭</span><span class="sxs-lookup"><span data-stu-id="5f381-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="5f381-111">닫고 WebMatrix 3을 다시 시작</span><span class="sxs-lookup"><span data-stu-id="5f381-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="5f381-112">중요 한 변경 내용</span><span class="sxs-lookup"><span data-stu-id="5f381-112">Notable Changes</span></span>

<span data-ttu-id="5f381-113">가장 큰 문제 사용자가이 확장 업데이트 해결 두 WebMatrix 내에서 사용 중인 NuGet 패키지를 직면 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="5f381-114">첫 번째 NuGet 스키마 버전 오류 이며 두 번째에 0 바이트 Dll에 버그가 `bin` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="5f381-115">NuGet 스키마 버전 오류</span><span class="sxs-lookup"><span data-stu-id="5f381-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="5f381-116">WebMatrix 3이 릴리스된 이후 NuGet 패키지에 대 한 새 스키마 버전을 필요로 하는 NuGet에 새로운 기능이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="5f381-117">를 웹 사이트에서 NuGet 패키지를 관리 하려고 시도할 때 이러한 새 패키지 WebMatrix에서 볼 수 있는 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![오류가 발생했습니다.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="5f381-121">이 최신 릴리스의 발생이 오류를 방지 하는 최신 NuGet 패키지를와 호환성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="5f381-122">이제 WebMatrix에서 Microsoft.AspNet.WebPages를 포함 하 여 패키지의 새 버전을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="5f381-123">이러한 패키지 중 일부 사용한 NuGet 기능와 같은 [XDT 구성 변환](../release-notes/nuget-2.6.md#xdt)는 지금까지 WebMatrix에서 지원 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="5f381-124">Bin 폴더에서에서 0 바이트 Dll</span><span class="sxs-lookup"><span data-stu-id="5f381-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="5f381-125">일부 사용자에 게 보고 하는 NuGet을 설치 하는 bin에 복사 하는 Dll을 포함 하는 WebMatrix에서 Dll 표시를 패키지에서 후의 `bin` 0 바이트 파일과 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="5f381-126">이 런타임 시 응용 프로그램을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="5f381-127">[이 문제](https://nuget.codeplex.com/workitem/4060) 이제 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="5f381-128">기타 최근 개선 사항</span><span class="sxs-lookup"><span data-stu-id="5f381-128">Other Recent Improvements</span></span>

<span data-ttu-id="5f381-129">Visual Studio 용 NuGet 패키지 관리자 2.8가 릴리스도 WebMatrix에 대 한 NuGet 패키지 관리자 2.5.0를 릴리스 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="5f381-130">언급 한 것이 동안는 [NuGet 2.8 릴리스 정보](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), 새로운 기능을 도입 하는 업데이트는 특정 언급 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="5f381-131">모두 업데이트</span><span class="sxs-lookup"><span data-stu-id="5f381-131">Update All</span></span>

<span data-ttu-id="5f381-132">이제 모든 한번에 웹 사이트의 패키지를 업데이트할 수 있습니다!</span><span class="sxs-lookup"><span data-stu-id="5f381-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="5f381-133">WebMatrix에서 NuGet 확장을 열 때 갤러리, 등에, 설치 된 업데이트를 사용할 수 있는 모든 패키지의 목록을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="5f381-134">이전에 모든 패키지를 개별적으로 업데이트 되어야 할 것 이지만 이제 업데이트 탭에 표시 하는 유용한 "모두 업데이트" 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![사용 가능한 업데이트로 업데이트 하는 모든 패키지를 모두 업데이트를 클릭합니다](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="5f381-136">기존 파일 덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="5f381-136">Overwrite Existing Files</span></span>

<span data-ttu-id="5f381-137">웹 사이트에 이미 있는 파일이 포함 된 패키지를 설치할 때 NuGet 항상 자동으로 해당 파일 (기존 파일은 그대로 두고)를 무시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="5f381-138">인상을 패키지 설치 된 또는 아니 실제로 때 제대로 업데이트 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="5f381-139">파일을 덮어쓸 수 이제 NuGet를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f381-139">NuGet will now prompt for files to be overwritten.</span></span>

![파일 충돌 해결](./media/NuGet-2.8/webmatrix-overwrite-file.png)
