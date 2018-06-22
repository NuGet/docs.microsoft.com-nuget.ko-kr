---
title: NuGet 1.6 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 1.6에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0345e180893a56302385d27792c4e15ba5d96989
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820601"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="97d42-103">NuGet 1.6 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="97d42-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="97d42-104">[NuGet 1.5 릴리스 정보](../release-notes/nuget-1.5.md) | [NuGet 1.7 릴리스 정보](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="97d42-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="97d42-105">NuGet 1.6 2011 년 12 월 13 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="97d42-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="97d42-106">알려진된 설치 문제</span><span class="sxs-lookup"><span data-stu-id="97d42-106">Known Installation Issue</span></span>
<span data-ttu-id="97d42-107">VS 2010 s p 1을 실행 하는 경우 이전 버전이 설치 되어 있는 경우 NuGet을 업그레이드 하는 동안 설치 오류에 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97d42-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="97d42-108">해결 하려면 NuGet 제거한 다음 VS 확장 갤러리에서 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97d42-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="97d42-109">자세한 내용은 [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="97d42-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="97d42-110">참고: Visual Studio 확장 (제거 단추 사용 안 함)을 제거 하도록 허용 하지, 한 후 가능성 하면 "관리자 권한으로 실행"을 사용 하 여 Visual Studio를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="97d42-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="97d42-111">기능</span><span class="sxs-lookup"><span data-stu-id="97d42-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="97d42-112">의미 체계 버전 관리 및 시험판 패키지에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="97d42-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="97d42-113">NuGet 1.6 의미 체계 버전 관리 (SemVer)에 대 한 지원이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="97d42-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="97d42-114">SemVer를 사용 하는 방법에 대 한 자세한 내용은 참조는 [버전 관리 설명서](../create-packages/prerelease-packages.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="97d42-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="97d42-115">NuGet을 사용 하 여 패키지 (패키지 복원)에서 확인 하지 않고</span><span class="sxs-lookup"><span data-stu-id="97d42-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="97d42-116">NuGet 1.6에는 NuGet 패키지 소스 제어에 추가 되지 않습니다 되지만 대신은 복원 빌드 시 누락 된 경우 워크플로 위한 최고 수준의 지원도 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="97d42-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="97d42-117">자세한 내용은 참조 하세요는 [를 사용 하 여 NuGet 패키지를 소스 제어에 커밋하지 않고](../consume-packages/packages-and-source-control.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="97d42-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="97d42-118">NuGet 패키지를 설치 하는 항목 템플릿</span><span class="sxs-lookup"><span data-stu-id="97d42-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="97d42-119">Visual Studio 항목 템플릿에 대 한 지원을 NuGet 1.6에서 또한 추가 Visual Studio 프로젝트 템플릿 사전 설치 된 NuGet 패키지를 지원 하도록 작업을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="97d42-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="97d42-120">항목 템플릿에서 서식 파일에서 호출 될 때 설치 된 NuGet 패키지에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97d42-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="97d42-121">NuGet 패키지를 설치 하는 프로젝트/항목 템플릿을 변경 하는 방법에 대 한 자세한 내용은 참조는 [에서 Visual Studio 템플릿 패키지](../visual-studio-extensibility/visual-studio-templates.md) 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="97d42-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="97d42-122">패키지 소스를 사용 하지 않도록 설정 하는 것에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="97d42-122">Support for disabling package sources</span></span>
<span data-ttu-id="97d42-123">여러 패키지 소스를 구성 하면 NuGet 패키지 및 해당 종속성을 설치 하는 동안에 각 패키지에 대 한 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="97d42-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="97d42-124">어떤 이유로 든 느려질 수 있다는 심각 하 게 NuGet에 대 한 아래에 있는 패키지 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="97d42-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="97d42-125">NuGet 1.6 이전 패키지 소스를 제거할 수 있지만 기억 추가 하려는 경우에 대 한 세부 정보를 다시 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="97d42-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="97d42-126">NuGet 1.6을 사용 하지 않도록 설정 하 고 유지 한 패키지 소스를 선택 취소 하면 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="97d42-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![패키지를 사용 하지 않도록 설정](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="97d42-128">버그 수정</span><span class="sxs-lookup"><span data-stu-id="97d42-128">Bug Fixes</span></span>
<span data-ttu-id="97d42-129">NuGet 1.6 106의 총 작업 항목을 고정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="97d42-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="97d42-130">그 중 95 버그로 분류 된 되었고 그 중 10 기능.</span><span class="sxs-lookup"><span data-stu-id="97d42-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="97d42-131">작업의 전체 목록은 항목에서에서 수정 된 NuGet 1.6 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)합니다.</span><span class="sxs-lookup"><span data-stu-id="97d42-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
