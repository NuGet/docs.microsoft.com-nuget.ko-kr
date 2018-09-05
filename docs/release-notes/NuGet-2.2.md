---
title: NuGet 2.2 릴리스 정보
description: NuGet 2.2의 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a968ced3c58b7187a8bd9a8b14baa92f61f0140f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545994"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="11167-103">NuGet 2.2 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="11167-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="11167-104">[NuGet 2.1 릴리스 정보](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 릴리스 정보](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="11167-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="11167-105">NuGet 2.2는 2012 년 12 월 12 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="11167-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="11167-106">Visual Studio 빠른 실행</span><span class="sxs-lookup"><span data-stu-id="11167-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="11167-107">Visual Studio 2012에 추가 된 새로운 기능 중 하나는 [빠른 시작 대화](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)합니다.</span><span class="sxs-lookup"><span data-stu-id="11167-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="11167-108">NuGet 2.2는 빠른 시작에서 입력 된 검색 용어를 사용 하 여 패키지 관리자 대화 상자를 초기화할 수 있도록이 대화 상자를 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="11167-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="11167-109">예를 들어, 이제 빠른 시작에서 'jquery' 입력 'jquery'와 일치 하는 NuGet 패키지를 검색 결과에서 옵션을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="11167-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![Visual Studio 빠른 시작의 NuGet](./media/quick-launch.png)

<span data-ttu-id="11167-111">이 옵션을 선택 하면 'jquery' 용어는 표준 NuGet 패키지 관리자 검색 환경을 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11167-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![미리 채워진된 NuGet 패키지 관리자 대화 상자](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="11167-113">패키지 내용에 대 한 전체 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="11167-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="11167-114">NuGet 2.2 이제 지정할 수 있습니다에 전체 폴더를 `<file>` 요소의 `.nuspec` 해당 폴더의 내용을 모두 포함 하 여 파일.</span><span class="sxs-lookup"><span data-stu-id="11167-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="11167-115">예를 들어, 다음 하면 모든 스크립트 프로젝트에 패키지를 설치할 때 contents\scripts 폴더에 추가할 패키지의 스크립트 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11167-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="11167-116">**6 월 24/16을 업데이트 합니다: 패키지를 설치할 때 "콘텐츠" 폴더에 빈 폴더는 무시 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="11167-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="11167-117">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="11167-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="11167-118">패키지 관리자 콘솔을 사용 하는 경우 F # 프로젝트에 대 한 패키지 설치 실패</span><span class="sxs-lookup"><span data-stu-id="11167-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="11167-119">패키지 관리자 콘솔을 사용 하 여 F # 프로젝트에 NuGet 패키지를 설치 하려고 시도할 때, InvalidOperationException이 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11167-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="11167-120">적극적으로 노력 하 고 문제를 해결 하려면 F # 팀과 하지만 그동안 콘솔 대신 NuGet의 패키지 관리자 대화 상자를 통해 F # 프로젝트에 NuGet 패키지를 설치 하려면이 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="11167-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="11167-121">[자세한 정보는 CodePlex에서 사용 가능한](http://nuget.codeplex.com/workitem/2873)합니다.</span><span class="sxs-lookup"><span data-stu-id="11167-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="11167-122">버그 수정</span><span class="sxs-lookup"><span data-stu-id="11167-122">Bug Fixes</span></span>
<span data-ttu-id="11167-123">NuGet 2.2에는 여러 버그 수정을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="11167-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="11167-124">작업의 전체 목록은 항목 고정 NuGet 2.2에서 하세요 보기는 [이 릴리스의 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)합니다.</span><span class="sxs-lookup"><span data-stu-id="11167-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
