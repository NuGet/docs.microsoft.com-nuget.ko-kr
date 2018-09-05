---
title: NuGet 2.0 릴리스 정보
description: NuGet 2.0 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547577"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="c173d-103">NuGet 2.0 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="c173d-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="c173d-104">[NuGet 1.8 릴리스 정보](../release-notes/nuget-1.8.md) | [NuGet 2.1 릴리스 정보](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="c173d-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="c173d-105">NuGet 2.0은 2012 년 6 월 19 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="c173d-106">알려진된 설치 문제</span><span class="sxs-lookup"><span data-stu-id="c173d-106">Known Installation Issue</span></span>
<span data-ttu-id="c173d-107">VS 2010 SP1을 실행 하는 경우 이전 버전이 설치 되어 있는 경우 NuGet을 업그레이드 하려고 할 때 설치 오류를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="c173d-108">해결 방법은 NuGet 제거한 다음 VS 확장 갤러리에서 설치 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="c173d-109">참조 [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) 대 한 내용은 또는 [VS 핫픽스로 직접 이동](http://bit.ly/vsixcertfix)합니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="c173d-110">참고: Visual Studio (제거 단추 사용 안 함) 확장을 제거할 수 없습니다, 다음 가능성이 높은 경우 "관리자 권한으로 실행"을 사용 하 여 Visual Studio를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="c173d-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="c173d-111">패키지 복원 동의 활성화 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-111">Package restore consent is now active</span></span>

<span data-ttu-id="c173d-112">이 항목에 설명 된 대로 [패키지 복원 동의에 게시](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0를 온라인으로 전환 하 여 패키지를 다운로드 하는 패키지 복원을 사용 하려면 동의 주어 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="c173d-113">패키지 관리자 구성 대화 상자 또는 EnableNuGetPackageRestore 환경 변수를 통해 동의 제공한 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="c173d-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="c173d-114">대상 프레임 워크 종속성 그룹</span><span class="sxs-lookup"><span data-stu-id="c173d-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="c173d-115">패키지 종속성 다를 수 있습니다 버전 2.0 부터는 대상 프로젝트의 프레임 워크 프로필에 기반 합니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="c173d-116">업데이트를 사용 하 여 이렇게 `.nuspec` 스키마입니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="c173d-117">합니다 `<dependencies>` 요소 집합을 이제 포함할 수 있습니다 `<group>` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="c173d-118">각 그룹에는 0 개 이상의 `<dependency>` 요소 및 `targetFramework` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="c173d-119">대상 프레임 워크를 대상 프로젝트 프레임 워크 프로필과 호환 되는 경우 그룹 내의 모든 종속성이 함께 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="c173d-120">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="c173d-120">For example:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<span data-ttu-id="c173d-121">그룹을 포함할 수 있는 참고 **0** 종속성입니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="c173d-122">위의 예제에서는 Silverlight 3.0을 대상으로 하는 프로젝트에 어셈블리를 설치 하거나 나중에 패키지를 종속성이 없는 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="c173d-123">패키지 이상을.NET 4.0을 대상으로 하는 프로젝트에 설치 되어 있으면 두 개의 종속성, jQuery 및 WebActivator에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="c173d-124">이러한 2 프레임 워크 또는 다른 프레임 워크의 초기 버전을 대상으로 하는 프로젝트에 패키지가 설치 되어 있으면 RouteMagic 1.1.0 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="c173d-125">그룹 간 상속은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-125">There is no inheritance between groups.</span></span> <span data-ttu-id="c173d-126">프로젝트의 대상 프레임 워크와 일치 하는 경우는 `targetFramework` 특성 그룹, 해당 그룹 내 종속성만 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="c173d-127">패키지를 두 가지 형식 중 하나에 패키지 종속성을 지정할 수 있습니다: 이전 형식의 플랫 목록 `<dependency>` 요소 또는 그룹.</span><span class="sxs-lookup"><span data-stu-id="c173d-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="c173d-128">경우는 `<group>` 형식이 사용 됩니다, 2.0 보다 이전 버전의 NuGet으로 패키지를 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="c173d-129">Note 두 가지 형식 혼합은 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="c173d-130">예를 들어, 다음 코드 조각은 됩니다 **잘못 된** 않으며 NuGet에서 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="c173d-131">대상 프레임 워크에서 콘텐츠 파일 및 PowerShell 스크립트를 그룹화</span><span class="sxs-lookup"><span data-stu-id="c173d-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="c173d-132">어셈블리 참조 외에도 콘텐츠 파일과 PowerShell 스크립트로 그룹화 할 수 있습니다 대상 프레임 워크입니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="c173d-133">동일한 폴더 구조에는 `lib` 대상 프레임 워크를 지정 하는 것에 대 한 폴더를 동일한 방식으로 적용 될 수 있게 합니다 `content` 및 `tools` 폴더.</span><span class="sxs-lookup"><span data-stu-id="c173d-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="c173d-134">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="c173d-134">For example:</span></span>

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

<span data-ttu-id="c173d-135">**참고**: 때문 `init.ps1` 솔루션 수준에서 실행 되 고 모든 개별 프로젝트에 의존 하지 않는 배치 해야 바로 아래는 `tools` 폴더.</span><span class="sxs-lookup"><span data-stu-id="c173d-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="c173d-136">프레임 워크별 폴더 안에 배치 하는 경우 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="c173d-137">또한 NuGet 2.0의 새로운 기능에는 프레임 워크 폴더 수 있음을 *빈*,이 경우 NuGet은 없는 어셈블리 참조를 추가, 콘텐츠 파일을 추가 또는 특정 프레임 워크 버전에 대 한 PowerShell 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="c173d-138">폴더를 위의 예에서 `content\net40` 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="c173d-139">향상 된 탭 완성 성능</span><span class="sxs-lookup"><span data-stu-id="c173d-139">Improved tab completion performance</span></span>
<span data-ttu-id="c173d-140">NuGet 패키지 관리자 콘솔에서 탭 완성 기능 성능을 크게 개선할 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="c173d-141">제안 드롭다운 표시 될 때까지 tab 키를 누를 때부터 훨씬 적은 지연이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="c173d-142">버그 수정</span><span class="sxs-lookup"><span data-stu-id="c173d-142">Bug Fixes</span></span>
<span data-ttu-id="c173d-143">2.0 NuGet 패키지 복원 동 및 성능에 중점을 두어 많은 버그 수정 프로그램이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="c173d-144">작업의 전체 목록은 항목 고정 NuGet 2.0에서 하세요 보기는 [이 릴리스의 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)합니다.</span><span class="sxs-lookup"><span data-stu-id="c173d-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
