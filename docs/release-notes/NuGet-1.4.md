---
title: NuGet 1.4 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 1.4에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b31c02b9251d6d45d952fdf8b111493495d57ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230709"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="15d47-103">NuGet 1.4 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="15d47-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="15d47-104">Nuget [1.3 릴리스 정보](../release-notes/nuget-1.3.md) | [Nuget 1.5 릴리스 정보](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="15d47-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="15d47-105">NuGet 1.4은 2011 년 6 월 17 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="15d47-106">기능</span><span class="sxs-lookup"><span data-stu-id="15d47-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="15d47-107">업데이트-패키지 개선 사항</span><span class="sxs-lookup"><span data-stu-id="15d47-107">Update-Package improvements</span></span>
<span data-ttu-id="15d47-108">NuGet 1.4은 업데이트 패키지 명령에 대해 많은 향상 된 기능을 제공 하 여 솔루션의 여러 프로젝트에서 패키지를 동일한 버전으로 쉽게 유지할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="15d47-109">예를 들어 패키지를 최신 버전으로 업그레이드 하는 경우 해당 패키지를 설치 하는 모든 프로젝트를 동일한 verision 업데이트 하는 것이 매우 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="15d47-110">이제 `Update-Package` 명령을 사용 하면 다음과 같은 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="15d47-111">단일 프로젝트의 모든 패키지 업데이트</span><span class="sxs-lookup"><span data-stu-id="15d47-111">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="15d47-112">모든 프로젝트의 패키지 업데이트</span><span class="sxs-lookup"><span data-stu-id="15d47-112">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="15d47-113">모든 프로젝트의 모든 패키지 업데이트</span><span class="sxs-lookup"><span data-stu-id="15d47-113">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="15d47-114">모든 패키지에서 "안전" 업데이트 수행</span><span class="sxs-lookup"><span data-stu-id="15d47-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="15d47-115">`-Safe` 플래그는 주 버전 및 부 버전 구성 요소가 같은 버전으로 업그레이드를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="15d47-116">예를 들어 패키지의 버전 1.0.0을 설치 하 고 피드에서 1.0.1, 1.0.2 및 1.1 버전을 사용할 수 있는 경우 `-Safe` 플래그는 패키지를 1.0.2로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="15d47-117">`-Safe` 플래그 없이 업그레이드 하면 패키지가 최신 버전인 1.1로 업그레이드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="15d47-118">솔루션 수준에서 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="15d47-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="15d47-119">NuGet 1.4 이전에는 대화 상자를 사용 하 여 여러 프로젝트에 패키지를 설치 하는 것이 복잡 했습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="15d47-120">프로젝트 마다 한 번씩 대화를 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="15d47-121">NuGet 1.4은 동시에 여러 프로젝트에서 패키지를 설치/제거/업데이트 하기 위한 지원을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="15d47-122">솔루션을 마우스 오른쪽 단추로 클릭 하 고 **NuGet 패키지 관리** 메뉴 옵션을 선택 하 여를 시작 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![솔루션 수준 NuGet 패키지 관리 대화 상자](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="15d47-124">이 대화 상자의 제목 표시줄에는 프로젝트 이름이 아니라 솔루션 이름이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="15d47-125">이제 패키지 작업은 작업을 적용 해야 하는 프로젝트 목록과 함께 확인란 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![NuGet 패키지 관리 프로젝트 선택](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="15d47-127">자세한 내용은 [솔루션에 대 한 패키지 관리](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution)항목을 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="15d47-127">For more details, see the topic on [Managing Packages for the Solution](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="15d47-128">허용 되는 버전으로 업그레이드 제한</span><span class="sxs-lookup"><span data-stu-id="15d47-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="15d47-129">기본적으로 패키지에서 `Update-Package` 명령을 실행 하거나 대화 상자를 사용 하 여 패키지를 업데이트 하는 경우 피드의 최신 버전으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="15d47-130">모든 패키지를 업데이트 하는 새로운 지원 기능을 사용 하 여 패키지를 특정 버전 범위로 잠그는 경우가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="15d47-131">예를 들어 응용 프로그램은 패키지의 버전 2. \* 에서만 작동 하지만 3.0 이상에서는 작동 하지 않는 것을 미리 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="15d47-132">패키지를 실수로 업데이트 하는 것을 방지 하기 위해 NuGet 1.4은 새 `allowedVersions` 특성을 사용 하 여 `packages.config` 파일을 직접 편집 하 여 패키지를 업그레이드할 수 있는 버전 범위를 제한 하기 위한 지원을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="15d47-133">예를 들어 다음 예제에서는 2.0-3.0 (제외) 버전 범위의 `SomePackage` 패키지를 잠그는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="15d47-134">`allowedVersions` 특성은 [버전 범위 형식을](../concepts/package-versioning.md#version-ranges)사용 하 여 값을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-134">The `allowedVersions` attribute accepts values using the [version range format](../concepts/package-versioning.md#version-ranges).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="15d47-135">1.4에서는 특정 버전 범위에 대 한 패키지 잠금을 직접 편집 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="15d47-136">NuGet 1.5에서는 `Install-Package` 명령을 통해이 범위를 배치 하는 지원을 추가할 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="15d47-137">패키지 시각화 도우미</span><span class="sxs-lookup"><span data-stu-id="15d47-137">Package Visualizer</span></span>
<span data-ttu-id="15d47-138">**도구** -> **라이브러리 패키지 관리자** -> **패키지 시각화 도우미** 메뉴 옵션을 통해 시작 된 새 패키지 시각화 도우미를 사용 하면 솔루션 내에서 모든 프로젝트 및 해당 패키지 종속성을 쉽게 시각화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="15d47-139">_**중요 정보:** 이 기능은 Visual Studio의 DGML 지원을 활용 합니다. 시각화 만들기는 Visual Studio Ultimate 에서만 지원 됩니다. DGML 다이어그램 보기는 Visual Studio Premium 이상 에서만 지원 됩니다._</span><span class="sxs-lookup"><span data-stu-id="15d47-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![패키지 시각화 도우미](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="15d47-141">NuGet 대화 상자에 대 한 자동 업데이트 확인</span><span class="sxs-lookup"><span data-stu-id="15d47-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="15d47-142">일부 NuGet 버전은 NuGet 대화 상자의 이전 버전에서는 인식 되지 않는 `.nuspec` 파일을 통해 표현 되는 새로운 기능을 소개 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="15d47-143">한 가지 예는 [프레임 워크 어셈블리를 지정](../release-notes/nuget-1.2.md#framework-assembly-refs)하기 위한 NuGet 1.4에 대 한 소개입니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="15d47-144">따라서 최신 버전의 NuGet을 사용 하 여 최신 기능을 활용 하는 패키지를 사용할 수 있도록 하는 것이 중요 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="15d47-145">NuGet에 대 한 업데이트를 더 표시 하기 위해 NuGet 대화 상자에는 최신 버전을 사용할 수 있는 경우를 강조 표시 하는 논리가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="15d47-146">_**참고**: 현재 세션에서 **온라인** 탭을 선택한 경우에만 확인이 수행 됩니다._</span><span class="sxs-lookup"><span data-stu-id="15d47-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![새 버전을 사용할 수 있는 NuGet 패키지 관리 대화 상자](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="15d47-148">자동 업데이트 확인을 해제 하려면 NuGet 설정 대화 상자로 이동 하 여 **자동으로 업데이트 확인**을 선택 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![NuGet 설정](./media/nuget-settings.png)

<span data-ttu-id="15d47-150">이 기능은 NuGet 1.3에 실제로 추가 되었지만 NuGet 1.4와 같은 1.3 업데이트를 사용할 수 있게 되었을 때까지 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="15d47-151">패키지 관리자 대화 상자 개선</span><span class="sxs-lookup"><span data-stu-id="15d47-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="15d47-152">**메뉴 이름 개선**: 대화 상자를 시작 하는 메뉴 옵션의 이름을 명확 하 게 변경 했습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="15d47-153">이제 메뉴 옵션이 **NuGet 패키지를 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="15d47-154">**최신 업데이트 날짜를 표시 하는 세부 정보 창**: NuGet 대화 상자는 **온라인** 또는 **업데이트** 탭을 선택한 경우 패키지에 대 한 세부 정보 창에 최신 업데이트 날짜를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="15d47-155">**표시 되는 태그 목록**: Nuget 대화 상자에 태그가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="15d47-156">Powershell 개선 사항</span><span class="sxs-lookup"><span data-stu-id="15d47-156">Powershell Improvements</span></span>
* <span data-ttu-id="15d47-157">**서명 된 powershell 스크립트**: NuGet에는 더 제한적인 환경에서 사용 하도록 설정 된 서명 된 powershell 스크립트가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="15d47-158">**지원 요청**: 이제 패키지 관리자 콘솔에서 `$host.ui.Prompt` 및 `$host.ui.PromptForChoice` 명령을 통해 메시지를 표시 하도록 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="15d47-159">패키지 원본 **이름**: `-Source` 플래그를 사용 하 여 패키지 원본을 지정할 때 패키지 원본 이름을 제공 하는 것이 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="15d47-160">nuget.exe 명령줄 개선 사항</span><span class="sxs-lookup"><span data-stu-id="15d47-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="15d47-161">**Nuget 사용자 지정 명령**: NUGET.EXE는 MEF를 사용 하 여 사용자 지정 명령을 통해 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="15d47-162">**기호 패키지를 만들기 위한 워크플로 간소화**: `-Symbols` 플래그는 폴더 내의 원본 및 `.pdb` 파일만 포함 하 여 기호 패키지를 만드는 일반적인 규칙 기반 폴더 구조에 적용 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="15d47-163">**여러 소스 지정**: `NuGet install` 명령은 세미콜론을 구분 기호로 사용 하거나 `-Source`을 여러 번 지정 하 여 여러 소스를 지정 하도록 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="15d47-164">**프록시 인증 지원**: nuget 1.4는 인증을 필요로 하는 프록시 뒤에서 nuget을 사용할 때 사용자 자격 증명을 묻는 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="15d47-165">**Nuget.exe 업데이트 중단 변경**: 이제 nuget.exe를 업데이트 하기 위해 `-Self` 플래그가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="15d47-166">`nuget.exe Update`는 이제 `packages.config` 파일에 대 한 경로를 사용 하 여 패키지 업데이트를 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="15d47-167">이 업데이트는 \* \* 프로젝트 파일의 콘텐츠를 업데이트, 추가, 제거 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-167">Note that this update is limited in that it will not: \*\* Update, add, remove content in the project file.</span></span>
<span data-ttu-id="15d47-168">\* \* 패키지 내에서 Powershell 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-168">\*\* Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="15d47-169">Nuget.exe를 사용 하 여 패키지를 푸시하는 NuGet 서버 지원</span><span class="sxs-lookup"><span data-stu-id="15d47-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="15d47-170">NuGet에는 `NuGet.Server` NuGet 패키지를 통해 간단한 [웹 기반 NuGet 리포지토리](../hosting-packages/nuget-server.md) 를 호스트 하는 간단한 방법이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="15d47-171">NuGet 1.4를 사용 하는 경량 서버는 nuget.exe를 사용 하 여 패키지 밀어넣기 및 삭제를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="15d47-172">최신 버전의 `NuGet.Server`은 `apiKey`라는 새 `appSetting`를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="15d47-173">키를 생략 하거나 비워 두면 피드에 패키지를 푸시할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="15d47-174">ApiKey를 값 (이상적으로는 강력한 암호)으로 설정 하면 nuget.exe를 사용 하 여 패키지를 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="15d47-175">Windows Phone Tools 망고 Edition에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="15d47-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="15d47-176">이제 NuGet은 망고 용 Windows Phone Tools의 릴리스 후보 버전에서 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="15d47-177">현재 Windows Phone 도구에는 Visual Studio 확장 관리자가 지원 되지 않으므로 Windows Phone 도구에 대 한 NuGet을 설치 하기 위해 VSIX를 수동으로 다운로드 하 여 실행 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="15d47-178">Windows Phone Tools에 대 한 NuGet을 제거 하려면 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="15d47-179">버그 수정</span><span class="sxs-lookup"><span data-stu-id="15d47-179">Bug Fixes</span></span>
<span data-ttu-id="15d47-180">NuGet 1.4에는 총 88 개의 작업 항목이 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="15d47-181">71는 버그로 표시 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="15d47-182">NuGet 1.4에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)를 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="15d47-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="15d47-183">버그가 수정 될 만한 문제:</span><span class="sxs-lookup"><span data-stu-id="15d47-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="15d47-184">[문제 603](http://nuget.codeplex.com/workitem/603): 특정 패키지 원본을 지정할 때 서로 다른 리포지토리의 패키지 종속성이 제대로 확인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="15d47-185">[문제 1036](http://nuget.codeplex.com/workitem/1036): 빌드 후 이벤트에 `NuGet Pack SomeProject.csproj`를 추가 하면 무한 루프가 발생 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="15d47-186">[문제 961](http://nuget.codeplex.com/workitem/961): `-Source` 플래그는 상대 경로를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="15d47-187">NuGet 1.4 업데이트</span><span class="sxs-lookup"><span data-stu-id="15d47-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="15d47-188">NuGet 1.4이 출시 되는 즉시 해결 해야 하는 몇 가지 문제가 발견 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="15d47-189">1.4에 대 한이 업데이트의 특정 버전 번호는 1.4.20615.9020입니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="15d47-190">버그 수정</span><span class="sxs-lookup"><span data-stu-id="15d47-190">Bug Fixes</span></span>
* <span data-ttu-id="15d47-191">[문제 1220](http://nuget.codeplex.com/workitem/1220): 업데이트가 두 개 이상 있는 경우 모든 프로젝트에서 패키지 `install.ps1`/`uninstall.ps1` 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15d47-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="15d47-192">[문제 1156](http://nuget.codeplex.com/workitem/1156): W2K3/XP에서 패키지 관리자 콘솔 중단 되었습니다 (Powershell 2가 설치 되지 않은 경우).</span><span class="sxs-lookup"><span data-stu-id="15d47-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
