---
title: NuGet 2.2 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 2.2에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cc81d0ff53a5e8ac8b632a08c3cfe0b8b59c9bd7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780435"
---
# <a name="nuget-22-release-notes"></a><span data-ttu-id="f55ac-103">NuGet 2.2 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="f55ac-103">NuGet 2.2 Release Notes</span></span>

<span data-ttu-id="f55ac-104">[NuGet 2.1 릴리스 정보](../release-notes/nuget-2.1.md)  |  [NuGet 2.2.1 릴리스 정보](../release-notes/nuget-2.2.1.md)</span><span class="sxs-lookup"><span data-stu-id="f55ac-104">[NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md) | [NuGet 2.2.1 Release Notes](../release-notes/nuget-2.2.1.md)</span></span>

<span data-ttu-id="f55ac-105">NuGet 2.2은 2012 년 12 월 12 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f55ac-105">NuGet 2.2 was released on December 12, 2012.</span></span>

## <a name="visual-studio-quick-launch"></a><span data-ttu-id="f55ac-106">Visual Studio 빠른 실행</span><span class="sxs-lookup"><span data-stu-id="f55ac-106">Visual Studio Quick Launch</span></span>
<span data-ttu-id="f55ac-107">Visual Studio 2012에 추가 된 새로운 기능 중 하나는 [빠른 실행 대화 상자](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box)입니다.</span><span class="sxs-lookup"><span data-stu-id="f55ac-107">One of the new features that was added in Visual Studio 2012 was the [quick launch dialog](/visualstudio/ide/reference/quick-launch-environment-options-dialog-box).</span></span> <span data-ttu-id="f55ac-108">NuGet 2.2은이 대화 상자를 확장 하 여 빠른 실행에 입력 된 검색 용어를 사용 하 여 패키지 관리자 대화 상자를 초기화할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="f55ac-108">NuGet 2.2 extends this dialog, allowing it to initialize the package manager dialog with the search terms entered in the quick launch.</span></span> <span data-ttu-id="f55ac-109">예를 들어 빠른 실행에서 ' jquery '를 입력 하면 이제 결과에 ' jquery '와 일치 하는 NuGet 패키지를 검색 하는 옵션이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f55ac-109">For example, entering 'jquery' in quick launch now includes an option in the results to search NuGet packages matching 'jquery'.</span></span>

![Visual Studio 빠른 실행의 NuGet](./media/quick-launch.png)

<span data-ttu-id="f55ac-111">이 옵션을 선택 하면 ' jquery ' 용어에 대 한 표준 NuGet 패키지 관리자 검색 환경이 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f55ac-111">Selecting this option will launch the standard NuGet package manager search experience for the term 'jquery'.</span></span>

![미리 채워진 NuGet 패키지 관리자 대화 상자](./media/pkg-mgr-search-from-quick-launch.png)

## <a name="specify-entire-folder-for-package-contents"></a><span data-ttu-id="f55ac-113">패키지 콘텐츠에 대 한 전체 폴더 지정</span><span class="sxs-lookup"><span data-stu-id="f55ac-113">Specify Entire Folder for Package Contents</span></span>
<span data-ttu-id="f55ac-114">이제 NuGet 2.2을 사용 하면 파일의 요소에 전체 폴더를 지정 하 여 `<file>` `.nuspec` 해당 폴더의 모든 내용을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55ac-114">NuGet 2.2 now allows you to specify an entire folder in the `<file>` element of the `.nuspec` file to include all of the contents of that folder.</span></span> <span data-ttu-id="f55ac-115">예를 들어 다음은 패키지를 프로젝트에 설치할 때 패키지의 scripts 폴더에 있는 모든 스크립트를 contents\scripts 폴더에 추가 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f55ac-115">For example, the following will cause all scripts in the package's scripts folder to be added to the contents\scripts folder when the package is installed into a project.</span></span>

```xml
<file src="scripts\" target="content\scripts"/>
```

<span data-ttu-id="f55ac-116">**업데이트 6/24/16: 패키지를 설치할 때 "content" 폴더의 빈 폴더는 무시 됩니다.**</span><span class="sxs-lookup"><span data-stu-id="f55ac-116">**Update 6/24/16: Empty folders in the "content" folder are ignored when installing the package.**</span></span>

## <a name="known-issues"></a><span data-ttu-id="f55ac-117">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="f55ac-117">Known Issues</span></span>

### <a name="package-installation-fails-for-f-projects-when-using-the-package-manager-console"></a><span data-ttu-id="f55ac-118">패키지 관리자 콘솔을 사용 하는 경우 F # 프로젝트에 대 한 패키지 설치가 실패 함</span><span class="sxs-lookup"><span data-stu-id="f55ac-118">Package installation fails for F# projects when using the package manager console</span></span>
<span data-ttu-id="f55ac-119">패키지 관리자 콘솔을 사용 하 여 F # 프로젝트에 NuGet 패키지를 설치 하려고 하면 InvalidOperationException이 throw 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f55ac-119">When attempting to install a NuGet package into an F# project using the package manager console, an InvalidOperationException is thrown.</span></span> <span data-ttu-id="f55ac-120">이 문제를 해결 하기 위해 F # 팀과 적극적으로 노력 하 고 있지만, 그 동안에는 nuget 패키지를 콘솔 대신 NuGet의 패키지 관리자 대화 상자를 통해 F # 프로젝트에 설치 하는 것이 해결 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f55ac-120">We are actively working with the F# team to resolve the issue, but in the meantime, the workaround is to install NuGet packages into F# projects via NuGet's package manager dialog rather than the console.</span></span> <span data-ttu-id="f55ac-121">[자세한 내용은 CodePlex에서 확인할 수](http://nuget.codeplex.com/workitem/2873)있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55ac-121">[More information is available on CodePlex](http://nuget.codeplex.com/workitem/2873).</span></span>


## <a name="bug-fixes"></a><span data-ttu-id="f55ac-122">버그 픽스</span><span class="sxs-lookup"><span data-stu-id="f55ac-122">Bug Fixes</span></span>
<span data-ttu-id="f55ac-123">NuGet 2.2에는 많은 버그 수정이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f55ac-123">NuGet 2.2 includes many bug fixes.</span></span> <span data-ttu-id="f55ac-124">NuGet 2.2에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)를 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="f55ac-124">For a full list of work items fixed in NuGet 2.2, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>
