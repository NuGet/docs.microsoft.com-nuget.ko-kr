---
title: "NuGet 패키지 복원 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "복원을 사용하지 않도록 설정하고 버전을 제한하는 방법을 포함하여 NuGet에서 프로젝트가 종속된 패키지를 복원하는 방법을 설명합니다."
keywords: "NuGet 패키지 복원, NuGet 패키지 설치, 패키지 설치, 패키지 복원, 종속성 버전, 자동 복원 사용 해제, 패키지 버전 제한"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4e819a2bb34bbe70f0f11d5adeed82b976a8cb65
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/05/2018
---
# <a name="package-restore"></a><span data-ttu-id="490be-104">패키지 복원</span><span class="sxs-lookup"><span data-stu-id="490be-104">Package Restore</span></span>

<span data-ttu-id="490be-105">더 깨끗한 개발 환경을 촉진하고 리포지토리 크기를 줄이기 위해 NuGet **패키지 복원**은 프로젝트가 빌드되기 전에 참조된 모든 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="490be-106">널리 사용되는 이 기능은 패키지를 원본 제어에 저장하지 않고도 프로젝트에서 모든 종속성을 사용할 수 있게 합니다(패키지 이진 파일을 제외하도록 리포지토리를 구성하는 방법은 [패키지 및 원본 제어](../consume-packages/packages-and-source-control.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="490be-106">This widely-used feature ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span>

<span data-ttu-id="490be-107">항목 내용:</span><span class="sxs-lookup"><span data-stu-id="490be-107">In this topic:</span></span>
- [<span data-ttu-id="490be-108">패키지 복원에 대한 빠른 지침</span><span class="sxs-lookup"><span data-stu-id="490be-108">Quick guide to package restore</span></span>](#quick-guide-to-package-restore)
- [<span data-ttu-id="490be-109">패키지 복원 개요</span><span class="sxs-lookup"><span data-stu-id="490be-109">Package restore overview</span></span>](#package-restore-overview)
- [<span data-ttu-id="490be-110">패키지 복원 사용 설정/해제</span><span class="sxs-lookup"><span data-stu-id="490be-110">Enabling and disabling package restore</span></span>](#enabling-and-disabling-package-restore)
- [<span data-ttu-id="490be-111">복원을 사용하여 패키지 버전 제한</span><span class="sxs-lookup"><span data-stu-id="490be-111">Constraining package versions with restore</span></span>](#constraining-package-versions-with-restore)
- <span data-ttu-id="490be-112">[명령줄 복원](#command-line-restore)(모든 NuGet 버전)</span><span class="sxs-lookup"><span data-stu-id="490be-112">[Command-line restore](#command-line-restore), for all versions of NuGet</span></span>
- <span data-ttu-id="490be-113">[Visual Studio에서 자동 복원](#automatic-restore-in-visual-studio)(NuGet 2.7 이상)</span><span class="sxs-lookup"><span data-stu-id="490be-113">[Automatic restore in Visual Studio](#automatic-restore-in-visual-studio), for NuGet 2.7 and later.</span></span>
- <span data-ttu-id="490be-114">[Visual Studio에서 MSBuild 통합 복원](#msbuild-integrated-restore)(NuGet 2.6 및 이전 버전)</span><span class="sxs-lookup"><span data-stu-id="490be-114">[MSBuild-integrated restore in Visual Studio](#msbuild-integrated-restore), for NuGet 2.6 and earlier.</span></span>
- [<span data-ttu-id="490be-115">Team Foundation 빌드를 사용하여 패키지 복원</span><span class="sxs-lookup"><span data-stu-id="490be-115">Package restore with Team Foundation Build</span></span>](#package-restore-with-team-foundation-build)

<span data-ttu-id="490be-116">복원 동작은 버전에 따라 다릅니다. NuGet 버전을 확인하려면 명령줄에서 `nuget.exe`를 실행하여 첫 번째 출력 줄을 살펴보기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="490be-116">Restore behavior does vary by version; to check your NuGet version, simply run `nuget.exe` on the command line and look at the first line of output.</span></span>

<span data-ttu-id="490be-117">빌드 서버의 패키지 복원에 대한 자세한 내용은 [TFBuild를 사용하여 패키지 복원](../consume-packages/team-foundation-build.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="490be-117">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

> [!Note]
> <span data-ttu-id="490be-118">패키지 복원에 대해 구성된 프로젝트는 Mono의 xbuild에서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-118">Projects configured for package restore also work with xbuild on Mono.</span></span>

## <a name="quick-guide-to-package-restore"></a><span data-ttu-id="490be-119">패키지 복원에 대한 빠른 지침</span><span class="sxs-lookup"><span data-stu-id="490be-119">Quick guide to package restore</span></span>

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> <span data-ttu-id="490be-120">"이 프로젝트는 이 컴퓨터에 없는 NuGet 패키지를 참조합니다." 또는 "하나 이상의 NuGet 패키지를 복원해야 하지만 동의하지 않아 복원할 수 없습니다."라는 오류 메시지가 표시되면 [패키지 복원 사용 설정/해제](#enabling-and-disabling-package-restore)의 지침에 따라 자동 복원을 설정하세요.</span><span class="sxs-lookup"><span data-stu-id="490be-120">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="490be-121">패키지 복원 개요</span><span class="sxs-lookup"><span data-stu-id="490be-121">Package restore overview</span></span>

<span data-ttu-id="490be-122">먼저, 패키지 참조는 프로젝트 형식 및 NuGet 버전에 따라 다음 패키지 관리 형식 중 하나로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="490be-122">First, package references are maintained in one of the following package management formats, depending on project type and NuGet version.</span></span> <span data-ttu-id="490be-123">(NuGet 4 및 MSBuild 15.1은 Visual Studio 2017과 함께 설치됩니다.)</span><span class="sxs-lookup"><span data-stu-id="490be-123">(Note that NuGet 4 and MSBuild 15.1 are installed with Visual Studio 2017.)</span></span>

| <span data-ttu-id="490be-124">메서드</span><span class="sxs-lookup"><span data-stu-id="490be-124">Method</span></span> | <span data-ttu-id="490be-125">NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="490be-125">NuGet Version</span></span> | <span data-ttu-id="490be-126">설명</span><span class="sxs-lookup"><span data-stu-id="490be-126">Description</span></span> | 
| --- | --- | --- |
| `packages.config` | <span data-ttu-id="490be-127">2.x 이상</span><span class="sxs-lookup"><span data-stu-id="490be-127">2.x+</span></span> | <span data-ttu-id="490be-128">종속성의 완전한 전체 집합을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-128">Lists the complete deep set of dependencies.</span></span> <span data-ttu-id="490be-129">`packages.config`에 추가된 Packages도 프로젝트 파일에 추가해야 하며, Targets 및 Props도 프로젝트 파일에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-129">Packages added to `packages.config` must also be added to the project file, and Targets and Props must also be added to the project file.</span></span> <span data-ttu-id="490be-130">이는 모든 NuGet 버전에 대한 기준 메서드이지만 다른 옵션에 비해 성능이 떨어집니다.</span><span class="sxs-lookup"><span data-stu-id="490be-130">This is the baseline method for all versions of NuGet, but has slower performance compared with the other options.</span></span> <span data-ttu-id="490be-131">[packages.config 스키마](../schema/packages-config.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="490be-131">(See [packages.config schema](../schema/packages-config.md).)</span></span> | 
| `project.json` | <span data-ttu-id="490be-132">3.x 이상</span><span class="sxs-lookup"><span data-stu-id="490be-132">3.x+</span></span> | <span data-ttu-id="490be-133">UWP 프로젝트에서는 기본적으로 사용되지만, 프로젝트는 `packages.config`에서 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="490be-133">Used only by default with UWP projects, but projects can be converted from `packages.config`.</span></span> <span data-ttu-id="490be-134">`project.json`은 최상위 종속성만 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-134">`project.json` lists only top-level dependencies.</span></span> <span data-ttu-id="490be-135">References, Targets 및 Props는 빌드하는 동안 프로젝트에 동적으로 추가되며, 이에 따라 `packages.config`에 비해 성능이 향상됩니다.</span><span class="sxs-lookup"><span data-stu-id="490be-135">References, Targets, and Props are added dynamically to the project during build, resulting in better performance compared with `packages.config`.</span></span> <span data-ttu-id="490be-136">[project.json 스키마](../schema/project-json.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="490be-136">(See [project.json schema](../schema/project-json.md).)</span></span>|
| <span data-ttu-id="490be-137">PackageReference</span><span class="sxs-lookup"><span data-stu-id="490be-137">PackageReference</span></span> | <span data-ttu-id="490be-138">4.x 이상</span><span class="sxs-lookup"><span data-stu-id="490be-138">4.x+</span></span> | <span data-ttu-id="490be-139">`<PackageReference>` 노드의 프로젝트 파일에 `<Reference>` 및 `<ProjectReference>`와 함께 종속성을 직접 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-139">Lists dependencies directly in the project file in the `<PackageReference>` node, alongside `<Reference>` and `<ProjectReference>`.</span></span> <span data-ttu-id="490be-140">`project.json`과 비슷하게 작동합니다. [프로젝트 파일의 패키지 참조](../Consume-Packages/Package-References-in-Project-Files.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="490be-140">Works similarly to `project.json`; see [Package references in project files](../Consume-Packages/Package-References-in-Project-Files.md).</span></span> |

<span data-ttu-id="490be-141">다음으로, 다양한 방법으로 참조 목록을 사용하여 복원을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-141">Second, you start a restore using the reference list in a variety of ways:</span></span>

<span data-ttu-id="490be-142">명령줄 또는 [패키지 관리자 콘솔](../tools/Package-Manager-Console.md)에서 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-142">From the command line or [Package Manager Console](../tools/Package-Manager-Console.md):</span></span>

| <span data-ttu-id="490be-143">명령</span><span class="sxs-lookup"><span data-stu-id="490be-143">Command</span></span> | <span data-ttu-id="490be-144">적용 가능한 시나리오</span><span class="sxs-lookup"><span data-stu-id="490be-144">Applicable scenarios</span></span> |
| --- | --- | 
| `nuget restore` | <span data-ttu-id="490be-145">모든 NuGet 버전 및 모든 참조 형식에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="490be-145">All versions of NuGet and all reference types.</span></span> <span data-ttu-id="490be-146">아래의 [명령줄 복원](#command-line-restore)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="490be-146">See [Command-line restore](#command-line-restore) below.</span></span> | 
| `dotnet restore` | <span data-ttu-id="490be-147">.NET Core 프로젝트에 대한 `nuget restore`와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-147">Same as `nuget restore` for .NET Core projects.</span></span> <span data-ttu-id="490be-148">[dotnet restore](/dotnet/articles/core/tools/dotnet-restore)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="490be-148">See [dotnet restore](/dotnet/articles/core/tools/dotnet-restore).</span></span> |
| `msbuild /t:restore` | <span data-ttu-id="490be-149">[프로젝트 파일의 패키지 참조](../Consume-Packages/Package-References-in-Project-Files.md)만 있는 Nuget 4.x 이상 및 MSBuild 15.1 이상에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="490be-149">Nuget 4.x+ and MSBuild 15.1+ with [package references in project files](../Consume-Packages/Package-References-in-Project-Files.md) only.</span></span> <span data-ttu-id="490be-150">`nuget restore` 및 `dotnet restore`는 모두 해당 프로젝트에 대해 이 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-150">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span> <span data-ttu-id="490be-151">[MSBuild 대상으로서의 NuGet pack 및 restore - restore 대상](../schema/msbuild-targets.md#restore-target)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="490be-151">See [NuGet pack and restore as MSBuild targets- restore target](../schema/msbuild-targets.md#restore-target).</span></span>|

<span data-ttu-id="490be-152">Visual Studio 자체에서도 다른 시간에 패키지를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-152">Visual Studio itself also restores packages at different times:</span></span>

| <span data-ttu-id="490be-153">형식</span><span class="sxs-lookup"><span data-stu-id="490be-153">Type</span></span> | <span data-ttu-id="490be-154">복원이 수행되는 시간</span><span class="sxs-lookup"><span data-stu-id="490be-154">When restore happens</span></span> |
| --- | --- |
| <span data-ttu-id="490be-155">템플릿 복원</span><span class="sxs-lookup"><span data-stu-id="490be-155">Template restore</span></span> | <span data-ttu-id="490be-156">새 프로젝트를 만드는 동안(일부 템플릿이 외부 패키지에 종속되기 때문)</span><span class="sxs-lookup"><span data-stu-id="490be-156">During creation of a new project, as some templates depend on external packages.</span></span> |
| <span data-ttu-id="490be-157">빌드 복원</span><span class="sxs-lookup"><span data-stu-id="490be-157">Build restore</span></span> | <span data-ttu-id="490be-158">빌드의 첫 번째 단계로 수행</span><span class="sxs-lookup"><span data-stu-id="490be-158">As the first step of a build.</span></span> |
| <span data-ttu-id="490be-159">솔루션 복원</span><span class="sxs-lookup"><span data-stu-id="490be-159">Solution restore</span></span> | <span data-ttu-id="490be-160">사용자가 솔루션을 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 복원**을 선택할 때</span><span class="sxs-lookup"><span data-stu-id="490be-160">When user right-clicks a solution and selects **Restore NuGet Packages**.</span></span> |
| <span data-ttu-id="490be-161">프로젝트 변경 시 복원</span><span class="sxs-lookup"><span data-stu-id="490be-161">Restore on project change</span></span> | <span data-ttu-id="490be-162">*(NuGet 4.x만 해당)* .NET Core SDK 기반 프로젝트를 사용할 때(프로젝트 상태를 변경할 때 포함)</span><span class="sxs-lookup"><span data-stu-id="490be-162">*(NuGet 4.x only)* When a .NET Core SDK-based project is used, including when project state changes.</span></span> |

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="490be-163">패키지 복원 사용 설정/해제</span><span class="sxs-lookup"><span data-stu-id="490be-163">Enabling and disabling package restore</span></span>

<span data-ttu-id="490be-164">패키지 복원은 주로 Visual Studio에서 **도구 > 옵션 > NuGet 패키지 관리자**를 통해 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="490be-164">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![NuGet 패키지 관리자 옵션을 통한 패키지 복원 동작 제어](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="490be-166">**NuGet이 누락된 패키지를 다운로드하도록 허용**: `%AppData%\NuGet\NuGet.Config` 파일의 `packageRestore/enabled` 설정을 아래와 같이 변경하여 모든 형태의 패키지 복원을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-166">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  <span data-ttu-id="490be-167">Visual Studio를 시작하거나 빌드를 시작하기 전에 **EnableNuGetPackageRestore**이라는 환경 변수를 TRUE 또는 FALSE 값으로 설정하여 `packageRestore/enabled` 설정을 전역으로 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="490be-167">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>
    

- <span data-ttu-id="490be-168">**Visual Studio에서 빌드 시 누락된 패키지를 자동으로 확인**: `%AppData%\NuGet\NuGet.Config` 파일의 `packageRestore/automatic` 설정을 아래와 같이 변경하여 NuGet 2.7 이상에 대한 자동 복원을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-168">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore for NuGet 2.7 and later by changing the `packageRestore/automatic` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>
            
    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

<span data-ttu-id="490be-169">해당 참조는 [NuGet.Config 파일 - packageRestore 섹션](../Schema/nuget-config-file.md#packagerestore-section)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="490be-169">For reference, see the [NuGet config file - packageRestore section](../Schema/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="490be-170">경우에 따라 개발자 또는 회사에서 모든 사용자에 대해 기본적으로 컴퓨터에서 패키지 복원을 사용하거나 사용하지 않도록 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="490be-170">In some cases, a developer or company might want to enable or disable package restore on a machine by default for all users.</span></span> <span data-ttu-id="490be-171">이렇게 하려면 위의 동일한 설정을 `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`에 있는 전역 NuGet 구성 파일에 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="490be-171">This can be done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="490be-172">개별 사용자는 프로젝트 수준에서 필요에 따라 선택적으로 복원을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="490be-172">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="490be-173">NuGet에서 여러 config 파일의 우선 순위를 정확히 지정하는 방법에 대한 자세한 내용은 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="490be-173">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="490be-174">복원을 사용하여 패키지 버전 제한</span><span class="sxs-lookup"><span data-stu-id="490be-174">Constraining package versions with restore</span></span>

<span data-ttu-id="490be-175">어떤 방법으로든 NuGet에서 패키지를 복원하는 경우 `packages.config`, `project.json` 또는 프로젝트 파일에 지정된 제약 조건을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-175">When NuGet restores packages through any method, it will honor any constraints specified in `packages.config`, `project.json`, or the project file:</span></span>

- <span data-ttu-id="490be-176">`packages.config`: 종속성의 `allowedVersion` 속성에서 버전 범위를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-176">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="490be-177">[패키지 다시 설치 및 업데이트](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="490be-177">See [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="490be-178">예:</span><span class="sxs-lookup"><span data-stu-id="490be-178">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="490be-179">`project.json`: 종속성의 버전 번호를 사용하여 버전 범위를 직접 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-179">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="490be-180">예:</span><span class="sxs-lookup"><span data-stu-id="490be-180">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- <span data-ttu-id="490be-181">프로젝트 파일의 패키지 참조: 종속성의 버전 번호를 사용하여 버전 범위를 직접 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-181">Package references in project files: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="490be-182">예:</span><span class="sxs-lookup"><span data-stu-id="490be-182">For example:</span></span>
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

<span data-ttu-id="490be-183">모든 경우에 [패키지 버전 관리](../reference/package-versioning.md)에서 설명한 표기법을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="490be-183">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="command-line-restore"></a><span data-ttu-id="490be-184">명령줄 복원</span><span class="sxs-lookup"><span data-stu-id="490be-184">Command-line restore</span></span>

<span data-ttu-id="490be-185">NuGet 2.7 이상의 경우 [Restore](../tools/cli-ref-restore.md) 명령을 사용하여 솔루션의 모든 패키지를 복원합니다(`packages.config`, `project.json` 또는 프로젝트 파일의 패키지 참조를 사용하는지 여부에 관계없이).</span><span class="sxs-lookup"><span data-stu-id="490be-185">For NuGet 2.7 and above, use the [Restore](../tools/cli-ref-restore.md) command to restore all packages in a solution (whether it uses `packages.config`, `project.json`, or package references in project files).</span></span> <span data-ttu-id="490be-186">지정된 프로젝트 폴더(예: `c:\proj\app`)의 경우 아래의 일반적인 변형 각각에서 패키지를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-186">For a given project folder such as `c:\proj\app`, the common variations below each restore the packages:</span></span>

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

<span data-ttu-id="490be-187">또한 NuGet 4.0 이상 및 MSBuild 15.1 이상의 경우 [MSBuild 대상으로서의 NuGet pack 및 restore](../schema/msbuild-targets.md)에서 설명한 대로 `MSBuild /t:restore`를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="490be-187">For NuGet 4.0+ and MSBuild 15.1+, you can also use `MSBuild /t:restore` as described on [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="build-time-restore-in-visual-studio"></a><span data-ttu-id="490be-188">Visual Studio에서 빌드 시간 복원</span><span class="sxs-lookup"><span data-stu-id="490be-188">Build-time restore in Visual Studio</span></span>

<span data-ttu-id="490be-189">Visual Studio는 기본적으로 빌드를 시작할 때 누락된 패키지를 자동으로 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-189">Visual Studio automatically restores missing packages by default at the beginning of a build.</span></span> <span data-ttu-id="490be-190">이 동작은 **도구 > 옵션 > NuGet 패키지 관리자 > 일반 > Visual Studio에서 빌드 시 누락된 패키지를 자동으로 확인**을 선택 취소하여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="490be-190">This behavior can be changed by clearing **Tools > Options > NuGet Package Manager > General > Automatically check for missing packages during build in Visual Studio**.</span></span>

<span data-ttu-id="490be-191">사용하도록 설정되는 경우 자동 복원은 다음과 같이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-191">When enabled, automatic restore works as follows:</span></span>

1. <span data-ttu-id="490be-192">빌드가 시작되면 Visual Studio에서 패키지를 복원하도록 NuGet에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-192">When a build begins, Visual Studio instructs NuGet to restore packages.</span></span>
1. <span data-ttu-id="490be-193">NuGet은 재귀적으로 솔루션의 모든 `packages.config` 파일을 찾거나, `project.json`를 찾거나, 프로젝트 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="490be-193">NuGet recursively looks for all `packages.config` files in the solution, looks for `project.json`, or looks in the project file.</span></span>
1. <span data-ttu-id="490be-194">참조 파일에 나열된 각 패키지에 대해 NuGet은 이미 솔루션에 있는지 확인합니다(프로젝트에서 `packages.config`, `project.json` 또는 프로젝트 파일의 패키지 참조를 사용하는지 여부에 따라 `packages` 폴더, `project.lock.json` 또는 `project.assets.json`).</span><span class="sxs-lookup"><span data-stu-id="490be-194">For each packages listed in the reference files, NuGet checks if it already exists in the solution (the `packages` folder, `project.lock.json`, or `project.assets.json` depending on whether the project is using `packages.config`, `project.json`, or package references in project files).</span></span>
1. <span data-ttu-id="490be-195">패키지가 없으면 NuGet은 먼저 캐시에서 해당 패키지를 검색하려고 합니다([NuGet 캐시 관리](../consume-packages/managing-the-nuget-cache.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="490be-195">If the package is not found, NuGet attempts to retrieve the package from its cache first (see [Managing the NuGet cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="490be-196">패키지가 캐시에 없으면 NuGet은 **도구 > 옵션 > NuGet 패키지 관리자 > 패키지 원본**에서 나열한 대로 활성화된 원본에서 표시된 순서대로 해당 패키지를 다운로드하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-196">If the package is not in the cache, NuGet attempts to download the package from the enabled sources as listed in **Tools > Options > NuGet Package Manager > Package Sources**, in the order that the sources appear.</span></span> <span data-ttu-id="490be-197">이 경우 모든 원본을 확인한 후에 NuGet에서 패키지를 찾지 못했음을 나타내며, 목록의 마지막 원본에 대한 실패만 보고합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-197">In this case, NuGet does not indicate a failure to find the package until all the sources have been checked, at which time it reports the failure only for the last source in the list.</span></span> <span data-ttu-id="490be-198">이러한 오류는 해당 원본에 대한 오류가 개별적으로 표시되지 않았더라도 패키지가 다른 원본에 존재하지 않음을 함축적으로 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-198">By implication such an error also means that the package wasn't present on any of the other sources either, even though errors were not shown for those sources individually.</span></span>
1. <span data-ttu-id="490be-199">다운로드가 성공하면 NuGet에서 패키지를 캐시하고 솔루션(즉 `packages` 폴더, `project.lock.json` 또는 `project.assets.json`)에 설치합니다. 그렇지 않으면 NuGet이 실패하고 빌드도 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-199">If the download is successful, NuGet caches the package and installs it into the solution (again, into either the `packages` folder, `project.lock.json`, or `project.assets.json`); otherwise NuGet fails and the build fails.</span></span>

<span data-ttu-id="490be-200">이 프로세스에는 패키지 복원을 취소하는 옵션이 있는 진행률 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="490be-200">During this process, you see a progress dialog with the option to cancel package restore.</span></span>

## <a name="package-restore-with-team-foundation-build"></a><span data-ttu-id="490be-201">Team Foundation 빌드를 사용하여 패키지 복원</span><span class="sxs-lookup"><span data-stu-id="490be-201">Package Restore with Team Foundation Build</span></span>

<span data-ttu-id="490be-202">패키지 복원은 TFS(Team Foundation Server) 및 Visual Studio Team Services(여기서 다루지 않는 다른 빌드 시스템도 포함)와 마찬가지로 빌드 서버에서 프로젝트를 빌드할 때 주로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="490be-202">Package restore is commonly used when building projects on build servers, as with Team Foundation Server (TFS) and Visual Studio Team Services (as well as other build systems, which are not covered here).</span></span>

### <a name="visual-studio-team-services"></a><span data-ttu-id="490be-203">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="490be-203">Visual Studio Team Services</span></span>

<span data-ttu-id="490be-204">Team Services에서 빌드 정의를 만들 때 빌드 작업 이전에 NuGet 패키지 복원 작업을 정의에 포함하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="490be-204">When creating a build definition on Team Services, simply include the Restore NuGet Packages task in the definition before any build task.</span></span> <span data-ttu-id="490be-205">이 작업은 여러 빌드 템플릿에 기본적으로 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="490be-205">This task is included by default in a number of build templates.</span></span>

![Visual Studio Team Service 빌드 정의의 NuGet 패키지 복원 작업](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a><span data-ttu-id="490be-207">Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="490be-207">Team Foundation Server</span></span>

<span data-ttu-id="490be-208">Team Foundation Server 2013 이상용 팀 빌드 템플릿을 사용하는 경우, TFS 2013 이상에서는 기본적으로 빌드하는 동안 패키지가 자동으로 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="490be-208">With TFS 2013 and later, packages are automatically restored by default during build, provided that you're using a Team Build Template for Team Foundation Server 2013 or later.</span></span>

<span data-ttu-id="490be-209">또한 이전 버전의 빌드 템플릿(예: 이전 버전의 TFS에서 마이그레이션한 프로젝트)을 사용하는 경우, 해당 빌드 템플릿을 TFS 2013으로 마이그레이션해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="490be-209">If you're using a previous version of build templates (such as in a project that's been migrated from earlier versions of TFS), you'll need to also migrate those build templates to TFS 2013.</span></span> <span data-ttu-id="490be-210">즉 기본적으로 원본 제어(TFVC 또는 Git)에 적합한 템플릿을 사용하여 빌드 템플릿의 사용자 지정 부분을 다시 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="490be-210">This essentially means recreating the custom parts of the Build Templates using the appropriate template for your source control (TFVC or Git).</span></span>

<span data-ttu-id="490be-211">이전 버전의 TFS에서는 앞에서 설명한 대로 [명령줄 복원](#command-line-restore)을 호출하는 빌드 단계를 포함하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="490be-211">For earlier version of TFS, you can simply include a build step to invoke [command-line restore](#command-line-restore) as described earlier.</span></span>

<span data-ttu-id="490be-212">자세한 내용은 [Team Foundation 빌드를 사용하여 패키지 복원 연습](../consume-packages/team-foundation-build.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="490be-212">For more details see then [Walkthrough of Package Restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>    
