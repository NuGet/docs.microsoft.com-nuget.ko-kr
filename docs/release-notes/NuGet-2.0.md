---
title: NuGet 2.0 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 2.0에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 01fdbfafcaea009cf119dfa880b2b16539c9b088
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383069"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="d48f8-103">NuGet 2.0 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="d48f8-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="d48f8-104">Nuget [1.8 릴리스 정보](../release-notes/nuget-1.8.md) | [Nuget 2.1 릴리스 정보](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="d48f8-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="d48f8-105">NuGet 2.0은 2012 년 6 월 19 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="d48f8-106">알려진 설치 문제</span><span class="sxs-lookup"><span data-stu-id="d48f8-106">Known Installation Issue</span></span>
<span data-ttu-id="d48f8-107">VS 2010 s p 1을 실행 하는 경우 이전 버전을 설치한 경우 NuGet을 업그레이드 하려고 할 때 설치 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="d48f8-108">해결 방법은 NuGet을 제거한 후 VS 확장 갤러리에서 설치 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="d48f8-109">자세한 내용은 <https://support.microsoft.com/kb/2581019>을 참조 하거나 [VS 핫픽스로 직접 이동](http://bit.ly/vsixcertfix)합니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="d48f8-110">참고: Visual Studio에서 확장을 제거 하는 것을 허용 하지 않는 경우 (제거 단추를 사용할 수 없음) "관리자 권한으로 실행"을 사용 하 여 Visual Studio를 다시 시작 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="d48f8-111">이제 패키지 복원 동의가 활성 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-111">Package restore consent is now active</span></span>

<span data-ttu-id="d48f8-112">이 [게시물의 패키지 복원 동의에](http://blog.nuget.org/20120518/package-restore-and-consent.html)설명 된 대로 NuGet 2.0은 이제 패키지 복원이 온라인으로 전환 되 고 패키지를 다운로드할 수 있도록 동의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="d48f8-113">패키지 관리자 구성 대화 상자 또는 EnableNuGetPackageRestore 환경 변수를 통해 동의를 제공 했는지 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="d48f8-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="d48f8-114">대상 프레임 워크로 종속성 그룹화</span><span class="sxs-lookup"><span data-stu-id="d48f8-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="d48f8-115">버전 2.0부터 패키지 종속성은 대상 프로젝트의 프레임 워크 프로필에 따라 달라질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="d48f8-116">업데이트 된 `.nuspec` 스키마를 사용 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="d48f8-117">이제 `<dependencies>` 요소에 `<group>` 요소 집합이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="d48f8-118">각 그룹은 0 개 이상의 `<dependency>` 요소와 `targetFramework` 특성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="d48f8-119">대상 프레임 워크가 대상 프로젝트 프레임 워크 프로필과 호환 되는 경우 그룹 내의 모든 종속성이 함께 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="d48f8-120">예를 들면 다음과 같습니다.:</span><span class="sxs-lookup"><span data-stu-id="d48f8-120">For example:</span></span>

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

<span data-ttu-id="d48f8-121">그룹에는 종속성 **이 0 개** 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="d48f8-122">위의 예제에서 패키지가 Silverlight 3.0 이상을 대상으로 하는 프로젝트에 설치 된 경우 종속성이 설치 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="d48f8-123">패키지가 .NET 4.0 이상을 대상으로 하는 프로젝트에 설치 된 경우에는 jQuery와 WebActivator 라는 두 개의 종속성이 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="d48f8-124">패키지를 이러한 2 프레임 워크의 이전 버전을 대상으로 하는 프로젝트에 설치 하거나 다른 프레임 워크를 대상으로 하는 경우 RouteMagic 1.1.0가 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="d48f8-125">그룹 간에는 상속이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-125">There is no inheritance between groups.</span></span> <span data-ttu-id="d48f8-126">프로젝트의 대상 프레임 워크가 그룹의 `targetFramework` 특성과 일치 하는 경우 해당 그룹 내의 종속성만 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="d48f8-127">패키지는 두 가지 형식 중 하나로 패키지 종속성을 지정할 수 있습니다. `<dependency>` 요소에 대 한 단순 목록 또는 그룹의 이전 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="d48f8-128">`<group>` 형식이 사용 되는 경우 패키지를 2.0 이전 버전의 NuGet에 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="d48f8-129">두 형식을 함께 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="d48f8-130">예를 들어 다음 코드 조각은 **잘못** 되었으며 NuGet에서 거부 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="d48f8-131">대상 프레임 워크로 콘텐츠 파일 및 PowerShell 스크립트 그룹화</span><span class="sxs-lookup"><span data-stu-id="d48f8-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="d48f8-132">어셈블리 참조 외에도 대상 프레임 워크를 기준으로 콘텐츠 파일 및 PowerShell 스크립트를 그룹화 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="d48f8-133">이제 대상 프레임 워크를 지정 하기 위해 `lib` 폴더에 있는 동일한 폴더 구조를 `content` 및 `tools` 폴더와 동일한 방식으로 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="d48f8-134">예를 들면 다음과 같습니다.:</span><span class="sxs-lookup"><span data-stu-id="d48f8-134">For example:</span></span>

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

<span data-ttu-id="d48f8-135">**참고**: `init.ps1` 솔루션 수준에서 실행 되 고 개별 프로젝트에 종속 되지 않기 때문에 `tools` 폴더 바로 아래에 배치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="d48f8-136">프레임 워크 관련 폴더에 배치 된 경우 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="d48f8-137">또한 NuGet 2.0의 새로운 기능은 프레임 워크 폴더가 *비어*있을 수 있습니다 .이 경우 nuget은 어셈블리 참조를 추가 하거나 콘텐츠 파일을 추가 하거나 특정 프레임 워크 버전에 대해 PowerShell 스크립트를 실행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="d48f8-138">위의 예제에서 `content\net40` 폴더는 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="d48f8-139">향상 된 탭 완성 성능</span><span class="sxs-lookup"><span data-stu-id="d48f8-139">Improved tab completion performance</span></span>
<span data-ttu-id="d48f8-140">NuGet 패키지 관리자 콘솔의 탭 완성 기능이 업데이트 되어 성능이 크게 향상 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="d48f8-141">제안 드롭다운이 나타날 때까지 tab 키를 누르는 시간부터 지연 시간이 훨씬 줄어듭니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="d48f8-142">버그 수정</span><span class="sxs-lookup"><span data-stu-id="d48f8-142">Bug Fixes</span></span>
<span data-ttu-id="d48f8-143">NuGet 2.0에는 패키지 복원 동의 및 성능에 중점을 두어 많은 버그 수정이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d48f8-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="d48f8-144">NuGet 2.0에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)를 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="d48f8-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
