---
title: WebMatrix 릴리스 정보에 대 한 NuGet 2.6.1
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 포함 하 여 WebMatrix 용 NuGet 2.6.1에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780421"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="a9e0b-103">WebMatrix 릴리스 정보에 대 한 NuGet 2.6.1</span><span class="sxs-lookup"><span data-stu-id="a9e0b-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="a9e0b-104">[NuGet 2.6 릴리스 정보](../release-notes/nuget-2.6.md)  |  [NuGet 2.7 릴리스 정보](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="a9e0b-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="a9e0b-105">NuGet 팀은 2014 년 3 월 26 일에 WebMatrix 용 업데이트 된 NuGet 패키지 관리자 확장을 릴리스 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="a9e0b-106">이 업데이트는 [WebMatrix 확장 갤러리](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) 에서 다음 단계를 사용 하 여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="a9e0b-107">WebMatrix 3 열기</span><span class="sxs-lookup"><span data-stu-id="a9e0b-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="a9e0b-108">홈 리본에서 확장 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="a9e0b-109">업데이트 탭 선택</span><span class="sxs-lookup"><span data-stu-id="a9e0b-109">Select the Updates tab</span></span>
1. <span data-ttu-id="a9e0b-110">NuGet 패키지 관리자를 2.6.1로 업데이트 하려면 클릭 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="a9e0b-111">WebMatrix 3을 닫고 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="a9e0b-112">주목할 만한 변경 내용</span><span class="sxs-lookup"><span data-stu-id="a9e0b-112">Notable Changes</span></span>

<span data-ttu-id="a9e0b-113">이 확장 업데이트는 사용자가 WebMatrix 내에서 NuGet 패키지를 사용 하는 가장 큰 두 가지 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="a9e0b-114">첫 번째는 NuGet 스키마 버전 오류이 고, 두 번째는 폴더에서 0 바이트 Dll로 이어지는 버그 였습니다 `bin` .</span><span class="sxs-lookup"><span data-stu-id="a9e0b-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="a9e0b-115">NuGet 스키마 버전 오류</span><span class="sxs-lookup"><span data-stu-id="a9e0b-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="a9e0b-116">WebMatrix 3이 출시 되었으므로 nuget 패키지에 대 한 새 스키마 버전을 필요로 하는 새로운 기능이 NuGet에 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="a9e0b-117">웹 사이트에서 NuGet 패키지를 관리 하려고 할 때 이러한 새 패키지를 통해 WebMatrix에 표시 되는 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![오류가 발생했습니다.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="a9e0b-121">이 최신 릴리스는 최신 NuGet 패키지와의 호환성을 제공 하 여이 오류가 발생 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="a9e0b-122">이제 Microsoft 웹 페이지를 포함 하는 패키지의 새 버전을 WebMatrix에 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="a9e0b-123">이러한 패키지 중 일부는 현재까지 WebMatrix에서 지원 되지 않는 [XDT config 변환과](../release-notes/nuget-2.6.md#xdt)같은 NuGet 기능을 사용 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="a9e0b-124">Bin 폴더의 Zero-Byte Dll</span><span class="sxs-lookup"><span data-stu-id="a9e0b-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="a9e0b-125">일부 사용자는 WebMatrix에 복사 된 Dll이 포함 된 NuGet 패키지를 설치 하 고 나면 해당 Dll이 `bin` 폴더에 0 바이트 파일로 표시 되는 것을 보고 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="a9e0b-126">이렇게 하면 런타임에 응용 프로그램이 중단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="a9e0b-127">이제 [이 문제가](https://nuget.codeplex.com/workitem/4060) 해결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="a9e0b-128">기타 최신 개선 사항</span><span class="sxs-lookup"><span data-stu-id="a9e0b-128">Other Recent Improvements</span></span>

<span data-ttu-id="a9e0b-129">Visual Studio 용 NuGet 패키지 관리자 2.8가 릴리스되면 WebMatrix 용 NuGet 패키지 관리자 2.5.0 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="a9e0b-130">이 내용은 [NuGet 2.8 릴리스 정보](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)에 설명 되어 있지만 업데이트에서 도입 된 특정 새 기능에 대해서는 언급 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="a9e0b-131">모두 업데이트</span><span class="sxs-lookup"><span data-stu-id="a9e0b-131">Update All</span></span>

<span data-ttu-id="a9e0b-132">이제 모든 웹 사이트의 패키지를 한 번에 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="a9e0b-133">WebMatrix에서 NuGet 확장을 열면 갤러리의 모든 패키지 목록, 설치 된 패키지 및 업데이트를 사용할 수 있는 패키지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="a9e0b-134">이전에는 모든 패키지가 개별적으로 업데이트 되어야 하지만 이제 업데이트 탭에 표시 되는 유용한 "모두 업데이트" 단추가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![사용 가능한 업데이트가 있는 모든 패키지를 업데이트 하려면 모두 업데이트를 클릭 합니다.](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="a9e0b-136">기존 파일 덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="a9e0b-136">Overwrite Existing Files</span></span>

<span data-ttu-id="a9e0b-137">웹 사이트에 이미 있는 파일을 포함 하는 패키지를 설치할 때 NuGet은 항상 해당 파일을 자동으로 무시 했습니다 (기존 파일만 남기고 있음).</span><span class="sxs-lookup"><span data-stu-id="a9e0b-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="a9e0b-138">이로 인해 실제로 패키지가 설치 또는 업데이트 되지 않은 것 처럼 보일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="a9e0b-139">이제 NuGet에서 파일을 덮어쓸지 묻는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9e0b-139">NuGet will now prompt for files to be overwritten.</span></span>

![파일 충돌 해결](./media/NuGet-2.8/webmatrix-overwrite-file.png)
