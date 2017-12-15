---
title: "NuGet 1.4 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: e4856d0a-b408-4c60-ac51-f80ea06d9f79
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 1.4에 대 한 릴리스 정보입니다."
keywords: "NuGet 1.4 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c4c27861c8697c75a06712b8ca6243b3b206cbb3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="a962f-104">NuGet 1.4의 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="a962f-104">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="a962f-105">[NuGet 1.3 릴리스 정보](../release-notes/nuget-1.3.md) | [NuGet 1.5 릴리스 정보](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="a962f-105">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="a962f-106">NuGet 1.4는 2011 년 6 월 17 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-106">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="a962f-107">기능</span><span class="sxs-lookup"><span data-stu-id="a962f-107">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="a962f-108">업데이트 패키지 향상</span><span class="sxs-lookup"><span data-stu-id="a962f-108">Update-Package improvements</span></span>
<span data-ttu-id="a962f-109">1.4 NuGet 패키지를 솔루션에 여러 프로젝트에서 동일한 버전으로 유지할를 더욱 쉽게 업데이트 패키지 명령의 향상 된 기능을 많이 도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-109">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="a962f-110">예를 들어 패키지를 최신 버전으로 업그레이드할 때 매우 일반적 이기 해당 패키지가 동일한 verision 하도록 업데이트 되어야 설치 된 모든 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-110">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="a962f-111">`Update-Package` 명령 이제 하기가 쉬워집니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-111">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="a962f-112">단일 프로젝트의 모든 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-112">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="a962f-113">모든 프로젝트에서 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-113">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="a962f-114">모든 프로젝트의 모든 패키지를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-114">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="a962f-115">모든 패키지의 "안전한" 업데이트를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-115">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="a962f-116">`-Safe` 플래그 동일한 주 / 부 버전 구성 요소와만 버전 업그레이드를 제한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-116">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="a962f-117">예를 들어 패키지 버전 1.0.0이 설치 되 고 1.0.1, 1.0.2 및 1.1 버전이 피드에서 사용할 수 있는 경우는 `-Safe` 플래그는 패키지를 1.0.2로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-117">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="a962f-118">업그레이드 하지 않고는 `-Safe` 플래그 최신 버전 1.1로 패키지를 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-118">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="a962f-119">솔루션 수준에서 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="a962f-119">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="a962f-120">NuGet 1.4 하기 전에 여러 프로젝트에 패키지를 설치 된 대화 상자를 사용 하 여 복잡 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-120">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="a962f-121">프로젝트 마다 한 번 대화 상자를 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-121">It required launching the dialog once per project.</span></span>

<span data-ttu-id="a962f-122">동시에 여러 프로젝트에 패키지 설치/제거/업데이트에 대 한 지원을 추가 하는 NuGet 1.4 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-122">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="a962f-123">실행 하면는 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 하 여는 **NuGet 패키지 관리** 메뉴 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-123">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![솔루션 수준 NuGet 패키지 관리 대화 상자](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="a962f-125">알림 대화 상자의 제목 표시줄에 솔루션의 이름이 표시 됩니다, 그리고 프로젝트의 이름이 아니라 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-125">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="a962f-126">패키지 작업에는 이제 작업에 적용 해야 하는 프로젝트의 목록 사용 하 여 확인란의 목록을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-126">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![NuGet 패키지 프로젝트 선택 관리](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="a962f-128">자세한 내용은 참조 [솔루션에 대 한 패키지 관리](../tools/package-manager-ui.md#managing-packages-for-the-solution)합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-128">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="a962f-129">허용 버전으로 업그레이드 제한</span><span class="sxs-lookup"><span data-stu-id="a962f-129">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="a962f-130">기본적으로 실행 하는 경우는 `Update-Package` 패키지 (또는 대화 상자를 사용 하 여 패키지를 업데이트) 명령을 피드에 최신 버전으로 업데이트 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-130">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="a962f-131">모든 패키지를 업데이트 하기 위한 새로운 지원, 특정 버전 범위에 패키지를 잠근 경우 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-131">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="a962f-132">예를 들어 알고 있습니다 사전에 응용 프로그램 패키지를 있지만 하지 3.0 이상 버전 2.* 된 에서만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-132">For example, you may know in advance that your application will only work with version 2.* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="a962f-133">실수로 3의 패키지를 업데이트 하는 사용 하지 않도록 NuGet 1.4 패키지를 직접 편집 하 여 업그레이드할 수 있는 버전 범위를 제한 하는 것에 대 한 지원을 추가 하는 `packages.config` 사용 하 여 새 파일 `allowedVersions` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-133">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="a962f-134">예를 들어 다음 예제를 잠그는 방법은 `SomePackage` 패키지 버전 2.0에서 3.0 (제외)의 범위.</span><span class="sxs-lookup"><span data-stu-id="a962f-134">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="a962f-135">`allowedVersions` 특성 변수를 사용 하 여 값의 [버전 범위 형식](../reference/package-versioning.md#version-ranges-and-wildcards)합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-135">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="a962f-136">Note 1.4의 특정 버전 범위를 패키지 잠금 수 있어야 한다는 수동으로 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-136">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="a962f-137">NuGet 1.5에서 배치를 통해이 범위에 대 한 지원을 추가할 계획은 `Install-Package` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-137">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="a962f-138">시각화 도우미 패키지</span><span class="sxs-lookup"><span data-stu-id="a962f-138">Package Visualizer</span></span>
<span data-ttu-id="a962f-139">새 패키지 시각화 도우미를 통해 시작 된 **도구** -> **라이브러리 패키지 관리자** -> **패키지 시각화 도우미** 메뉴 옵션을 수 있습니다. 모든 프로젝트 및 솔루션 내에서 해당 패키지 종속성을 쉽게 시각화할 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-139">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="a962f-140">_**중요 정보:** Visual Studio에서이 기능은 DGML 지원 이용 합니다. Visual Studio Ultimate에 시각화를 만들기만 지원 됩니다. DGML 다이어그램 보기에서 Visual Studio Premium 또는 상위만 지원 됩니다._</span><span class="sxs-lookup"><span data-stu-id="a962f-140">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![시각화 도우미 패키지](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="a962f-142">NuGet 대화에 대 한 자동 업데이트 확인</span><span class="sxs-lookup"><span data-stu-id="a962f-142">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="a962f-143">일부 버전의 NuGet 통해 표현 하는 새로운 기능을 제공할는 `.nuspec` 파일을 이전 버전의 NuGet 대화 상자에서 이해 하기 힘듭니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-143">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="a962f-144">에 대 한 NuGet 1.4에서 소개 하는 예로 [프레임 워크 어셈블리를 지정 하](../release-notes/nuget-1.2.md#framework-assembly-refs)합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-144">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="a962f-145">이 때문에, 그러면 최신 기능을 활용 하는 패키지를 사용할 수 있도록 최신 버전의 NuGet 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-145">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="a962f-146">NuGet 대화 업데이트 NuGet을 보다 편리 하 게, 최신 버전을 사용할 수 있는 강조 표시 하는 논리를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-146">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="a962f-147">_**참고**: 경우에 확인 작업이 수행 된 **온라인** 현재 세션에서 탭을 선택 합니다._</span><span class="sxs-lookup"><span data-stu-id="a962f-147">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![사용 가능한 새 버전으로 대화 NuGet 패키지 관리](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="a962f-149">자동 업데이트 확인을 해제 하려면 NuGet 설정 대화 상자로 이동 하 고의 선택을 취소 **자동으로 업데이트 확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-149">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![NuGet 설정](./media/nuget-settings.png)

<span data-ttu-id="a962f-151">이 기능은 실제로, 추가 되었고 NuGet 1.3에 있지만 보이지 않을 것, 물론, NuGet 1.4와 같은 1.3에 대 한 업데이트 될 때까지 사용 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-151">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="a962f-152">패키지 관리자 대화 상자 개선</span><span class="sxs-lookup"><span data-stu-id="a962f-152">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="a962f-153">**메뉴 이름 향상**: 메뉴 옵션을 대화 상자를 시작 하기 위해 변경 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-153">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="a962f-154">메뉴 옵션은 이제 **NuGet 패키지 관리**합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-154">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="a962f-155">**세부 정보 창 표시 최신 업데이트 날짜**: 패키지에 대 한 세부 정보 창에서 최신 업데이트의 날짜를 표시 하는 NuGet 대화 때는 **온라인** 또는 **업데이트** 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-155">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="a962f-156">**표시 된 태그 목록**: Nuget 대화 태그를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-156">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="a962f-157">향상 된 Powershell</span><span class="sxs-lookup"><span data-stu-id="a962f-157">Powershell Improvements</span></span>
* <span data-ttu-id="a962f-158">**PowerShell 스크립트를 서명**: NuGet 더 제한적인 환경에서 사용을 사용 하도록 설정 하는 서명 된 Powershell 스크립트를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-158">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="a962f-159">**지원 메시지를 표시**: The 패키지 관리자 콘솔을 통해 메시지를 표시 이제 지원는 `$host.ui.Prompt` 및 `$host.ui.PromptForChoice` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-159">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="a962f-160">**패키지 소스 이름**: 사용 하 여 패키지 소스를 지정할 때 사용할 패키지 소스의 이름을 제공 하는 `-Source` 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-160">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="a962f-161">nuget.exe 명령줄 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="a962f-161">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="a962f-162">**사용자 지정 NuGet 명령을**: nuget.exe는 MEF를 사용 하 여 사용자 지정 명령을 통해 확장이 가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-162">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="a962f-163">**간단한 기호 패키지를 만들기 위한 워크플로**:는 `-Symbols` 만 원본을 포함 하 여 기호 패키지를 만드는 일반 규칙 기반 폴더 구조에 플래그를 적용할 수 있습니다 및 `.pdb` 폴더 내의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-163">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="a962f-164">**여러 원본 지정**:는 `NuGet install` 명령에서는 여러 소스를 지정 하 여 또는 구분 기호로 세미콜론으로 구분을 사용 하 여 지정할 수 있으므로 `-Source` 여러 번입니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-164">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="a962f-165">**프록시 인증 지원**: NuGet 1.4 인증이 필요한 프록시 뒤에 있는 NuGet을 사용 하는 경우 사용자 자격 증명에 대 한 메시지를 표시 하는 것에 대 한 지원을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-165">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="a962f-166">**nuget.exe 주요 변경 업데이트**:는 `-Self` 플래그는 이제 nuget.exe 업데이트 되도록 하는 데 필요한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-166">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="a962f-167">`nuget.exe Update`에 대 한 경로에 더 길어진는 `packages.config` 파일 및 패키지를 업데이트 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-167">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="a962f-168">이 업데이트는 제한 됩니다 지 것입니다 한다는 점에서: * * 업데이트, 추가, 프로젝트 파일에서 콘텐츠를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-168">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="a962f-169">* * 패키지 내에서 Powershell 스크립트를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-169">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="a962f-170">Nuget.exe를 사용 하 여 푸시 패키지에 대 한 NuGet 서버 지원</span><span class="sxs-lookup"><span data-stu-id="a962f-170">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="a962f-171">NuGet를 호스트 하는 간단한 방법을 포함 한 [간단한 웹 기반 NuGet 리포지토리](../hosting-packages/NuGet-Server.md) 통해는 `NuGet.Server` NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-171">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/NuGet-Server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="a962f-172">NuGet 1.4와 경량 서버 푸시 및 nuget.exe를 사용 하 여 패키지를 삭제를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-172">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="a962f-173">최신 버전의 `NuGet.Server` 를 새로 추가 `appSetting`명명 된 `apiKey`합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-173">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="a962f-174">키를 생략 하거나 비워 두면, 피드를 패키지에 푸시할 비활성화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-174">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="a962f-175">값 (이상적으로 강력한 암호)에 apiKey를 설정 nuget.exe를 사용 하 여 푸시 패키지 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-175">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="a962f-176">Windows Phone 도구 Mango 버전에 대 한 지원</span><span class="sxs-lookup"><span data-stu-id="a962f-176">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="a962f-177">NuGet은 릴리스 후보 버전의 Windows Phone 도구 Mango에서 이제 지원 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-177">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="a962f-178">현재, Windows Phone 도구는 Windows Phone 도구 NuGet를 설치 해야 하므로 Visual Studio 확장 관리자에 대 한를 지원 하지 않습니다, 그리고 다운로드 하 여 VSIX를 수동으로 실행 해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-178">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="a962f-179">Windows Phone 도구 NuGet를 제거 하려면 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-179">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="a962f-180">버그 수정</span><span class="sxs-lookup"><span data-stu-id="a962f-180">Bug Fixes</span></span>
<span data-ttu-id="a962f-181">NuGet 1.4 88 총 작업 항목을 고정 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-181">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="a962f-182">그 중 71 버그로 표시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-182">71 of those were marked as bugs.</span></span>

<span data-ttu-id="a962f-183">작업의 전체 목록은 항목에서에서 수정 된 NuGet 1.4 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-183">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="a962f-184">주목할 만한 버그가 수정 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-184">Bug fixes worth noting:</span></span>

* <span data-ttu-id="a962f-185">[문제 603](http://nuget.codeplex.com/workitem/603): 특정 패키지 소스를 지정 하는 경우 서로 다른 저장소에서 패키지 종속성 올바르게 해석 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-185">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="a962f-186">[문제 1036](http://nuget.codeplex.com/workitem/1036): 추가 `NuGet Pack SomeProject.csproj` 빌드 후 더 이상 이벤트를에서는 무한 루프가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-186">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="a962f-187">[문제 961](http://nuget.codeplex.com/workitem/961): `-Source` 플래그 상대 경로 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-187">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

# <a name="nuget-14-update"></a><span data-ttu-id="a962f-188">NuGet 1.4 업데이트</span><span class="sxs-lookup"><span data-stu-id="a962f-188">NuGet 1.4 Update</span></span>
<span data-ttu-id="a962f-189">NuGet 1.4의 릴리스 직후 몇 가지 된 문제를 해결 하는 것이 중요 문제를 발견 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-189">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="a962f-190">1.4-이 업데이트의 특정 버전 번호가 1.4.20615.9020입니다.</span><span class="sxs-lookup"><span data-stu-id="a962f-190">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="a962f-191">버그 수정</span><span class="sxs-lookup"><span data-stu-id="a962f-191">Bug Fixes</span></span>
* <span data-ttu-id="a962f-192">[문제 1220](http://nuget.codeplex.com/workitem/1220): 업데이트 패키지를 실행 하지 않습니다 `install.ps1` / `uninstall.ps1` 둘 이상의 프로젝트는 경우 모든 프로젝트에</span><span class="sxs-lookup"><span data-stu-id="a962f-192">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="a962f-193">[문제 1156](http://nuget.codeplex.com/workitem/1156): (Powershell 2가 설치 되지 않음) 하는 경우 패키지 관리자 콘솔 W2K3/XP에서 중단</span><span class="sxs-lookup"><span data-stu-id="a962f-193">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
