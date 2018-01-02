---
title: "WebMatrix 릴리스 정보에 대 한 NuGet 2.6.1 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 119ea65b-b38b-4a8c-a4ed-6ea06f1aad09
description: "2.6.1의 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 WebMatrix 용 NuGet에 대 한 릴리스 정보입니다."
keywords: "NuGet 2.6.1 WebMatrix 릴리스 정보, 버그 수정, 알려진된 문제에 대 한 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f859fd8ef74f3246d997790e40f70ad25aadeb71
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="6064f-104">NuGet 2.6.1 WebMatrix 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="6064f-104">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="6064f-105">[NuGet 2.6 릴리스 정보](../release-notes/nuget-2.6.md) | [NuGet 2.7 릴리스 정보](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="6064f-105">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="6064f-106">NuGet 팀 WebMatrix 용 2014 년 3 월 26 일에 업데이트 된 NuGet 패키지 관리자 확장을 릴리스 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-106">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="6064f-107">이 업데이트에서 설치할 수 있습니다는 [WebMatrix 확장 갤러리](http://extensions.webmatrix.com/packages/NuGetPackageManager/) 다음 단계를 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="6064f-107">This update can be installed from the [WebMatrix Extension Gallery](http://extensions.webmatrix.com/packages/NuGetPackageManager/) using the following steps:</span></span>

1. <span data-ttu-id="6064f-108">열기 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="6064f-108">Open WebMatrix 3</span></span>
2. <span data-ttu-id="6064f-109">홈 리본에서 확장 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-109">Click the Extensions icon in the Home ribbon</span></span>
3. <span data-ttu-id="6064f-110">업데이트 탭을 선택</span><span class="sxs-lookup"><span data-stu-id="6064f-110">Select the Updates tab</span></span>
4. <span data-ttu-id="6064f-111">2.6.1에 NuGet 패키지 관리자를 업데이트 하려면 클릭</span><span class="sxs-lookup"><span data-stu-id="6064f-111">Click to update NuGet Package Manager to 2.6.1</span></span>
6. <span data-ttu-id="6064f-112">닫고 WebMatrix 3을 다시 시작</span><span class="sxs-lookup"><span data-stu-id="6064f-112">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="6064f-113">중요 한 변경 내용</span><span class="sxs-lookup"><span data-stu-id="6064f-113">Notable Changes</span></span>

<span data-ttu-id="6064f-114">가장 큰 문제 사용자가이 확장 업데이트 해결 두 WebMatrix 내에서 사용 중인 NuGet 패키지를 직면 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-114">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="6064f-115">첫 번째 NuGet 스키마 버전 오류 이며 두 번째에 0 바이트 Dll에 버그가 `bin` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-115">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="6064f-116">NuGet 스키마 버전 오류</span><span class="sxs-lookup"><span data-stu-id="6064f-116">NuGet Schema Version Error</span></span>

<span data-ttu-id="6064f-117">WebMatrix 3이 릴리스된 이후 NuGet 패키지에 대 한 새 스키마 버전을 필요로 하는 NuGet에 새로운 기능이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-117">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="6064f-118">를 웹 사이트에서 NuGet 패키지를 관리 하려고 시도할 때 이러한 새 패키지 WebMatrix에서 볼 수 있는 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-118">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you'll see in WebMatrix.</span></span>

![오류가 발생했습니다.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="6064f-122">이 최신 릴리스의 발생이 오류를 방지 하는 최신 NuGet 패키지를와 호환성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-122">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="6064f-123">이제 WebMatrix에서 Microsoft.AspNet.WebPages를 포함 하 여 패키지의 새 버전을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-123">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="6064f-124">이러한 패키지 중 일부 사용한 NuGet 기능와 같은 [XDT 구성 변환](../release-notes/nuget-2.6.md#xdt)는 지금까지 WebMatrix에서 지원 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-124">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="6064f-125">Bin 폴더에서에서 0 바이트 Dll</span><span class="sxs-lookup"><span data-stu-id="6064f-125">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="6064f-126">일부 사용자에 게 보고 하는 NuGet을 설치 하는 bin에 복사 하는 Dll을 포함 하는 WebMatrix에서 Dll 표시를 패키지에서 후의 `bin` 0 바이트 파일과 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-126">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="6064f-127">이 런타임 시 응용 프로그램을 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-127">This breaks the application at runtime.</span></span>

<span data-ttu-id="6064f-128">[이 문제](https://nuget.codeplex.com/workitem/4060) 이제 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-128">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="6064f-129">기타 최근 개선 사항</span><span class="sxs-lookup"><span data-stu-id="6064f-129">Other Recent Improvements</span></span>

<span data-ttu-id="6064f-130">Visual Studio 용 NuGet 패키지 관리자 2.8가 릴리스도 WebMatrix에 대 한 NuGet 패키지 관리자 2.5.0를 릴리스 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-130">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="6064f-131">언급 한 것이 동안는 [NuGet 2.8 릴리스 정보](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), 새로운 기능을 도입 하는 업데이트는 특정 언급 하지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-131">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="6064f-132">모두 업데이트</span><span class="sxs-lookup"><span data-stu-id="6064f-132">Update All</span></span>

<span data-ttu-id="6064f-133">이제 모든 한번에 웹 사이트의 패키지를 업데이트할 수 있습니다!</span><span class="sxs-lookup"><span data-stu-id="6064f-133">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="6064f-134">WebMatrix에서 NuGet 확장을 열 때 갤러리, 등에, 설치 된 업데이트를 사용할 수 있는 모든 패키지의 목록을 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-134">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="6064f-135">이전에 모든 패키지를 개별적으로 업데이트 되어야 할 것 이지만 이제 업데이트 탭에 표시 하는 유용한 "모두 업데이트" 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-135">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![사용 가능한 업데이트로 업데이트 하는 모든 패키지를 모두 업데이트를 클릭합니다](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="6064f-137">기존 파일 덮어쓰기</span><span class="sxs-lookup"><span data-stu-id="6064f-137">Overwrite Existing Files</span></span>

<span data-ttu-id="6064f-138">웹 사이트에 이미 있는 파일이 포함 된 패키지를 설치할 때 NuGet 항상 자동으로 해당 파일 (기존 파일은 그대로 두고)를 무시 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-138">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="6064f-139">인상을 패키지 설치 된 또는 아니 실제로 때 제대로 업데이트 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-139">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="6064f-140">파일을 덮어쓸 수 이제 NuGet를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6064f-140">NuGet will now prompt for files to be overwritten.</span></span>

![파일 충돌 해결](./media/NuGet-2.8/webmatrix-overwrite-file.png)
