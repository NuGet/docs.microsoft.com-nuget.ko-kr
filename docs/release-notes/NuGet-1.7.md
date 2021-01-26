---
title: NuGet 1.7 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 1.7에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777067"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="6626b-103">NuGet 1.7 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="6626b-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="6626b-104">[NuGet 1.6 릴리스 정보](../release-notes/nuget-1.6.md)  |  [NuGet 1.8 릴리스 정보](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="6626b-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="6626b-105">NuGet 1.7은 2012 4 월 4 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6626b-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="6626b-106">알려진 설치 문제</span><span class="sxs-lookup"><span data-stu-id="6626b-106">Known Installation Issue</span></span>
<span data-ttu-id="6626b-107">VS 2010 s p 1을 실행 하는 경우 이전 버전을 설치한 경우 NuGet을 업그레이드 하려고 할 때 설치 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6626b-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="6626b-108">해결 방법은 NuGet을 제거한 후 VS 확장 갤러리에서 설치 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6626b-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="6626b-109">자세한 내용은 <https://support.microsoft.com/kb/2581019>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6626b-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="6626b-110">참고: Visual Studio에서 확장을 제거 하는 것을 허용 하지 않는 경우 (제거 단추를 사용할 수 없음) "관리자 권한으로 실행"을 사용 하 여 Visual Studio를 다시 시작 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6626b-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="6626b-111">기능</span><span class="sxs-lookup"><span data-stu-id="6626b-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="6626b-112">설치 후 readme.txt 파일 열기 지원</span><span class="sxs-lookup"><span data-stu-id="6626b-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="6626b-113">1.7의 새로운 기능으로, 패키지 `readme.txt` 의 루트에 파일이 포함 된 경우 NuGet은 패키지 설치를 완료 한 후이 파일을 자동으로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6626b-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="6626b-114">NuGet 패키지 관리 대화 상자에 시험판 패키지 표시</span><span class="sxs-lookup"><span data-stu-id="6626b-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="6626b-115">이제 NuGet 패키지 관리 대화 상자에는 시험판 패키지를 표시 하는 옵션을 제공 하는 드롭다운이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6626b-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![시험판 패키지 표시](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="6626b-117">패키지 파일이 없는 경우 패키지 복원 단추 표시</span><span class="sxs-lookup"><span data-stu-id="6626b-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="6626b-118">패키지 관리자 콘솔 또는 관리자 NuGet 패키지 대화 상자를 열면 NuGet은 현재 솔루션이 패키지 복원 모드를 사용 하도록 설정 했는지 여부와 폴더에 패키지 파일이 누락 되었는지 확인 합니다 `packages` .</span><span class="sxs-lookup"><span data-stu-id="6626b-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="6626b-119">이러한 두 조건이 충족 되는 경우 NuGet은 사용자에 게 알리고 편리한 복원 단추를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6626b-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="6626b-120">이 단추를 클릭 하면 누락 된 모든 패키지를 복원 하는 NuGet이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="6626b-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![대화 상자의 패키지 복원 단추](./media/packagerestore-dialog.png)

![콘솔의 패키지 복원 단추](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="6626b-123">솔루션 수준 packages.config 파일 추가</span><span class="sxs-lookup"><span data-stu-id="6626b-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="6626b-124">이전 버전의 NuGet에서 각 프로젝트에 `packages.config` 는 해당 프로젝트에 설치 된 NuGet 패키지를 추적 하는 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6626b-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="6626b-125">그러나 솔루션 수준 패키지를 추적할 수 있는 유사한 파일이 솔루션 수준에 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6626b-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="6626b-126">따라서 솔루션 수준 패키지를 복원할 수 있는 방법이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6626b-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="6626b-127">이 기능은 이제 NuGet 1.7에서 구현 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6626b-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="6626b-128">솔루션 수준 파일은 솔루션 `packages.config` 루트의 폴더 아래에 배치 되 `.nuget` 고 솔루션 수준 패키지만 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="6626b-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="6626b-129">New-Package 명령 제거</span><span class="sxs-lookup"><span data-stu-id="6626b-129">Remove New-Package command</span></span>
<span data-ttu-id="6626b-130">낮은 사용량으로 인해 New-Package 명령이 제거 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6626b-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="6626b-131">개발자는 nuget.exe 또는 편리한 NuGet 패키지 탐색기를 사용 하 여 패키지를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6626b-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="6626b-132">버그 픽스</span><span class="sxs-lookup"><span data-stu-id="6626b-132">Bug Fixes</span></span>
<span data-ttu-id="6626b-133">NuGet 1.7은 패키지 복원 워크플로 및 네트워크/원본 제어 시나리오에 대 한 많은 버그를 수정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6626b-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="6626b-134">NuGet 1.7에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)를 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="6626b-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
