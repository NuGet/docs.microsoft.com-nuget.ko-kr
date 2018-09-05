---
title: NuGet 2.6.1 WebMatrix 릴리스 정보
description: 2.6.1의 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함 하 여 WebMatrix 용 NuGet에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550319"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="b1ddf-103">NuGet 2.6.1 WebMatrix 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="b1ddf-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="b1ddf-104">[NuGet 2.6 릴리스 정보](../release-notes/nuget-2.6.md) | [NuGet 2.7 릴리스 정보](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="b1ddf-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="b1ddf-105">NuGet 팀 WebMatrix 용 2014 년 3 월 26에 NuGet 패키지 관리자 확장을 업데이트를 릴리스 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="b1ddf-106">이 업데이트에서 설치할 수 있습니다 합니다 [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) 다음 단계를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="b1ddf-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="b1ddf-107">WebMatrix 3를 열려면</span><span class="sxs-lookup"><span data-stu-id="b1ddf-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="b1ddf-108">홈 리본에서 확장 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="b1ddf-109">[업데이트] 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-109">Select the Updates tab</span></span>
1. <span data-ttu-id="b1ddf-110">2.6.1에 NuGet 패키지 관리자를 업데이트 하려면 클릭</span><span class="sxs-lookup"><span data-stu-id="b1ddf-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="b1ddf-111">닫고 WebMatrix 3를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="b1ddf-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="b1ddf-112">주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="b1ddf-112">Notable Changes</span></span>

<span data-ttu-id="b1ddf-113">이 확장 업데이트 주소의 두 가장 큰 문제 사용자 WebMatrix 내에서 사용 중인 NuGet 패키지에 직면 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="b1ddf-114">NuGet 스키마 버전 오류가 발생 한 첫 번째 및 두 번째 앞에 0 바이트 Dll에 버그가 있었습니다는 `bin` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="b1ddf-115">NuGet 스키마 버전 오류</span><span class="sxs-lookup"><span data-stu-id="b1ddf-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="b1ddf-116">WebMatrix 3이 릴리스된 이후 NuGet 패키지에 대 한 새 스키마 버전을 필요로 하는 NuGet에 새로운 기능이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="b1ddf-117">를 웹 사이트에서 NuGet 패키지를 관리 하려고 시도할 때 이러한 새 패키지 WebMatrix에서 표시 되는 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![오류가 발생했습니다.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="b1ddf-121">이 최신 릴리스의 발생이 오류를 방지 하 고 최신 NuGet 패키지와 호환성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="b1ddf-122">이제 WebMatrix에서 Microsoft.AspNet.WebPages를 포함 하 여 패키지의 새 버전을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="b1ddf-123">이러한 패키지 중 일부를 사용한 NuGet 기능 같은 [XDT 구성 변환](../release-notes/nuget-2.6.md#xdt)을 지금까지 WebMatrix에서 지원 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="b1ddf-124">Bin 폴더에서에서 0 바이트 Dll</span><span class="sxs-lookup"><span data-stu-id="b1ddf-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="b1ddf-125">일부 사용자에 게 보고 하는 NuGet을 설치 패키지는 bin으로 복사 하는 Dll을 포함 하는 WebMatrix에서 Dll 표시 후는 `bin` 0 바이트 파일 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="b1ddf-126">이 런타임 시 응용 프로그램을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="b1ddf-127">[이 문제](https://nuget.codeplex.com/workitem/4060) 이제 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="b1ddf-128">기타 최근 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="b1ddf-128">Other Recent Improvements</span></span>

<span data-ttu-id="b1ddf-129">Visual Studio 용 NuGet 패키지 관리자 2.8 릴리스 되었을 수도 WebMatrix 용 NuGet 패키지 관리자 2.5.0를 발표 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="b1ddf-130">언급 한 것이 동안 합니다 [NuGet 2.8 릴리스 정보](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates),에서는 특정 도입 업데이트를 새로운 기능을 언급 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="b1ddf-131">모든 업데이트</span><span class="sxs-lookup"><span data-stu-id="b1ddf-131">Update All</span></span>

<span data-ttu-id="b1ddf-132">이제 모든 웹 사이트의 패키지를 한 번에 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="b1ddf-133">WebMatrix에서 NuGet 확장을 열면 갤러리, 설치 된 및 사용 가능한 업데이트를 사용 하 여 항목에 모든 패키지 목록에 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="b1ddf-134">이전에 모든 패키지를 개별적으로 업데이트 해야 할 것 이지만 이제 [업데이트] 탭에 표시 되는 유용한 "모두 업데이트" 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![사용 가능한 업데이트를 사용 하 여 모든 패키지 업데이트를 모두 업데이트 클릭](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="b1ddf-136">기존 파일 덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="b1ddf-136">Overwrite Existing Files</span></span>

<span data-ttu-id="b1ddf-137">웹 사이트에 이미 있는 파일이 포함 된 패키지를 설치할 때 NuGet 항상 자동으로 해당 파일 (기존 파일을 단독으로 @)를 무시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="b1ddf-138">이 패키지를 설치한 또는 않았습니다 사실 경우 제대로 업데이트는 인상을 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="b1ddf-139">이제 NuGet 파일을 덮어쓸 수 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="b1ddf-139">NuGet will now prompt for files to be overwritten.</span></span>

![파일 충돌 해결](./media/NuGet-2.8/webmatrix-overwrite-file.png)
