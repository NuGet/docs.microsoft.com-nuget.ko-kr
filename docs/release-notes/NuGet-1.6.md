---
title: NuGet 1.6 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 1.6에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08b1cb3736e645d6efcc33f920f521c9c0fc7507
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777010"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="a154e-103">NuGet 1.6 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="a154e-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="a154e-104">[NuGet 1.5 릴리스 정보](../release-notes/nuget-1.5.md)  |  [NuGet 1.7 릴리스 정보](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="a154e-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="a154e-105">NuGet 1.6은 2011 년 12 월 13 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a154e-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="a154e-106">알려진 설치 문제</span><span class="sxs-lookup"><span data-stu-id="a154e-106">Known Installation Issue</span></span>
<span data-ttu-id="a154e-107">VS 2010 s p 1을 실행 하는 경우 이전 버전을 설치한 경우 NuGet을 업그레이드 하려고 할 때 설치 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a154e-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="a154e-108">해결 방법은 NuGet을 제거한 후 VS 확장 갤러리에서 설치 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a154e-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="a154e-109">자세한 내용은 <https://support.microsoft.com/kb/2581019>를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a154e-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="a154e-110">참고: Visual Studio에서 확장을 제거 하는 것을 허용 하지 않는 경우 (제거 단추를 사용할 수 없음) "관리자 권한으로 실행"을 사용 하 여 Visual Studio를 다시 시작 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a154e-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="a154e-111">기능</span><span class="sxs-lookup"><span data-stu-id="a154e-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="a154e-112">의미 체계 버전 관리 및 시험판 패키지 지원</span><span class="sxs-lookup"><span data-stu-id="a154e-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="a154e-113">NuGet 1.6에는 의미 체계 버전 관리 (SemVer)에 대 한 지원이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a154e-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="a154e-114">SemVer를 사용 하는 방법에 대 한 자세한 내용은 [버전 관리 설명서](../create-packages/prerelease-packages.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a154e-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="a154e-115">패키지를 체크 인하지 않고 NuGet 사용 (패키지 복원)</span><span class="sxs-lookup"><span data-stu-id="a154e-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="a154e-116">이제 NuGet 1.6에는 NuGet 패키지가 소스 제어에 추가 되지 않고 빌드 시에 복원 되는 워크플로를 위한 첫 번째 클래스 지원이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a154e-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="a154e-117">자세한 내용은 [소스 제어에 패키지를 커밋하지 않고 NuGet 사용](../consume-packages/packages-and-source-control.md) 항목을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a154e-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="a154e-118">NuGet 패키지를 설치 하는 항목 템플릿</span><span class="sxs-lookup"><span data-stu-id="a154e-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="a154e-119">Visual Studio 프로젝트 템플릿에 사전 설치 된 NuGet 패키지를 지원 하기 위한 작업을 기반으로 하는 NuGet 1.6에는 Visual Studio 항목 템플릿에 대 한 지원도 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a154e-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="a154e-120">항목 템플릿에는 템플릿이 호출 될 때 설치 되는 관련 NuGet 패키지가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a154e-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="a154e-121">NuGet 패키지를 설치 하기 위해 프로젝트/항목 템플릿을 변경 하는 방법에 대 한 자세한 내용은 [Visual Studio 템플릿에서 패키지](../visual-studio-extensibility/visual-studio-templates.md) 항목을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a154e-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="a154e-122">패키지 소스를 사용 하지 않도록 설정 지원</span><span class="sxs-lookup"><span data-stu-id="a154e-122">Support for disabling package sources</span></span>
<span data-ttu-id="a154e-123">여러 패키지 소스가 구성 된 경우 NuGet은 패키지 및 패키지의 종속성을 설치 하는 동안 각 패키지에 대 한 패키지를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a154e-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="a154e-124">어떤 이유로 다운 된 패키지 원본의 경우 NuGet이 심각 하 게 느려질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a154e-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="a154e-125">NuGet 1.6 이전에는 패키지 원본을 제거할 수 있지만, 다시 추가 하려는 경우에 대 한 세부 정보를 기억할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a154e-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="a154e-126">NuGet 1.6은 패키지 원본에 대 한 선택을 취소 하 여 사용 하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a154e-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![패키지 비활성화](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="a154e-128">버그 픽스</span><span class="sxs-lookup"><span data-stu-id="a154e-128">Bug Fixes</span></span>
<span data-ttu-id="a154e-129">NuGet 1.6에는 총 106 개의 작업 항목이 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a154e-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="a154e-130">이러한 중 95는 버그로 분류 되었으며 그 중 10 개는 기능 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="a154e-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="a154e-131">NuGet 1.6에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)를 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="a154e-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
