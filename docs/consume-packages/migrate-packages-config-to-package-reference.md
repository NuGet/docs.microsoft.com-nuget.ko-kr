---
title: packages.config에서 PackageReference 형식으로 마이그레이션
description: 프로젝트를 packages.config 관리 형식에서 NuGet 4.0 이상, VS2017, .NET Core 2.0이 지원하는 PackageReference 형식으로 마이그레이션하는 방법에 대한 세부 정보
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 23bd936707173f49a651a8ba432fa8773fa53881
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237837"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="63f46-103">packages.config를 PackageReference로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="63f46-103">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="63f46-104">Visual Studio 2017 버전 15.7 이상은 프로젝트를 [packages.config](../reference/packages-config.md) 관리 형식에서 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 형식으로 마이그레이션하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-104">Visual Studio 2017 Version 15.7 and later supports migrating a project from the [packages.config](../reference/packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="63f46-105">PackageReference 사용 혜택</span><span class="sxs-lookup"><span data-stu-id="63f46-105">Benefits of using PackageReference</span></span>

* <span data-ttu-id="63f46-106">**모든 프로젝트 종속성을 한 곳에서 관리** : 프로젝트 간 참조나 어셈블리 참조처럼 NuGet 패키지 참조(`PackageReference` 노드 사용)는 별도의 packages.config 파일을 사용하지 않고 프로젝트 파일 내에서 직접 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-106">**Manage all project dependencies in one place** : Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="63f46-107">**최상위 종속성의 정리된 보기** : packages.config와 다르게 PackageReference는 프로젝트에 직접 설치한 NuGet 패키지만 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-107">**Uncluttered view of top-level dependencies** : Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="63f46-108">따라서 NuGet 패키지 관리자 UI 및 프로젝트 파일은 하위 수준 종속성으로 인해 복잡하게 보이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-108">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="63f46-109">**향상된 성능** : PackageReference를 사용하는 경우, 패키지는 솔루션 내 `packages` 폴더에서보다는 *전역 패키지* 폴더( [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)에 대해 설명된 대로)에 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-109">**Performance improvements** : When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="63f46-110">따라서 PackageReference는 처리 속도가 더 빠르고 디스크 공간을 더 적게 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-110">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="63f46-111">**종속성 및 콘텐츠 흐름을 세밀하게 제어** : MSBuild의 기존 기능을 사용하면 [조건부로 NuGet 패키지를 참조](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)하고 대상 프레임워크, 구성, 플랫폼 또는 기타 피벗당 패키지 참조를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-111">**Fine control over dependencies and content flow** : Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="63f46-112">**현재 개발 중인 PackageReference** : [GitHub의 PackageReference 문제](https://aka.ms/nuget-pr-improvements)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63f46-112">**PackageReference is under active development** : See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="63f46-113">packages.config는 더 이상 활발하게 개발하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-113">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="63f46-114">제한 사항</span><span class="sxs-lookup"><span data-stu-id="63f46-114">Limitations</span></span>

* <span data-ttu-id="63f46-115">NuGet PackageReference는 Visual Studio 2015 이하에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-115">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="63f46-116">마이그레이션된 프로젝트는 Visual Studio 2017 이상에서만 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-116">Migrated projects can be opened only in Visual Studio 2017 and later.</span></span>
* <span data-ttu-id="63f46-117">현재 C++ 및 ASP.NET 프로젝트에는 마이그레이션이 제공되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-117">Migration is not currently available for C++ and ASP.NET projects.</span></span>
* <span data-ttu-id="63f46-118">일부 패키지는 PackageReference와 완전히 호환되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-118">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="63f46-119">자세한 내용은 [패키지 호환성 문제](#package-compatibility-issues)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63f46-119">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

<span data-ttu-id="63f46-120">또한 PackageReferences와 packages.config의 작동 방식에는 몇 가지 차이점이 있습니다. 예를 들어 [업그레이드 버전 제한](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)은 PackageReference에서 지원되지 않지만 [부동 버전](../consume-packages/package-references-in-project-files.md#floating-versions) 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-120">In addition, there are some differences in how PackageReferences work compared to packages.config. For example - [constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) is not supprted by PackageReference but add support for [Floating Versions](../consume-packages/package-references-in-project-files.md#floating-versions).</span></span>

### <a name="known-issues"></a><span data-ttu-id="63f46-121">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="63f46-121">Known Issues</span></span>

1. <span data-ttu-id="63f46-122">`Migrate packages.config to PackageReference...` 옵션을 오른쪽 클릭 상황에 맞는 메뉴에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-122">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span> 

#### <a name="issue"></a><span data-ttu-id="63f46-123">문제점</span><span class="sxs-lookup"><span data-stu-id="63f46-123">Issue</span></span> 
 
<span data-ttu-id="63f46-124">프로젝트를 처음 열면 NuGet 작업이 수행될 때까지 NuGet을 초기화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-124">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="63f46-125">이로 인해 마이그레이션 옵션이 `packages.config` 또는 `References`의 오른쪽 클릭 상황에 맞는 메뉴에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-125">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span> 

#### <a name="workaround"></a><span data-ttu-id="63f46-126">해결 방법</span><span class="sxs-lookup"><span data-stu-id="63f46-126">Workaround</span></span> 

<span data-ttu-id="63f46-127">다음 NuGet 작업 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-127">Perform any one of the following NuGet actions:</span></span> 
* <span data-ttu-id="63f46-128">패키지 관리자 UI 열기 - `References`를 마우스 오른쪽 단추로 클릭하고 `Manage NuGet Packages...`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-128">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span> 
* <span data-ttu-id="63f46-129">패키지 관리자 콘솔 열기 - `Tools > NuGet Package Manager`에서 `Package Manager Console`을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-129">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span> 
* <span data-ttu-id="63f46-130">NuGet 복원 실행 - 솔루션 탐색기에서 솔루션 노드를 마우스 오른쪽 단추로 클릭하고 `Restore NuGet Packages`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-130">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span> 
* <span data-ttu-id="63f46-131">NuGet 복원을 트리거하는 프로젝트 빌드</span><span class="sxs-lookup"><span data-stu-id="63f46-131">Build the project which also triggers NuGet restore</span></span> 

<span data-ttu-id="63f46-132">이제 마이그레이션 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-132">You should now be able to see the migration option.</span></span> <span data-ttu-id="63f46-133">이 옵션은 지원되지 않으며 ASP.NET 및 C++ 프로젝트 형식에 대해 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-133">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span> 

## <a name="migration-steps"></a><span data-ttu-id="63f46-134">마이그레이션 단계</span><span class="sxs-lookup"><span data-stu-id="63f46-134">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="63f46-135">마이그레이션을 시작하기 전에 Microsoft Visual Studio는 필요한 경우 [packages.config로 롤백](#how-to-roll-back-to-packagesconfig)할 수 있도록 프로젝트의 백업을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-135">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="63f46-136">`packages.config`를 사용하여 프로젝트가 포함된 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-136">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="63f46-137">**솔루션 탐색기** 에서 **참조** 노드 또는 `packages.config` 파일을 마우스 오른쪽 단추로 클릭하고 **packages.config에서 PackageReference로 마이그레이션** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-137">In **Solution Explorer** , right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="63f46-138">마이그레이터는 프로젝트의 NuGet 패키지 참조를 분석하여 **최상위 종속성** (직접 설치한 NuGet 패키지) 및 **전이적 종속성** (최상위 패키지의 종속성으로 설치된 패키지)으로 분류하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-138">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directly) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="63f46-139">PackageReference는 전이적 패키지 복원을 지원하고 종속성을 동적으로 확인합니다. 즉, 전이적 종속성을 명시적으로 설치할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-139">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="63f46-140">(선택 사항) 패키지의 **최상위 레벨** 옵션을 선택함으로써 전이적 종속성으로 분류된 NuGet 패키지를 최상위 종속성으로 선택하여 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-140">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="63f46-141">이 옵션은 전이적으로 이동하지 않는 자산(`build`, `buildCrossTargeting`, `contentFiles` 또는 `analyzers` 폴더의 자산) 및 개발 종속성(`developmentDependency = "true"`)으로 표시된 자산을 포함하는 패키지에 대해 자동으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-141">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="63f46-142">모든 [패키지 호환성 문제](#package-compatibility-issues)를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-142">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="63f46-143">**확인** 을 선택하여 마이그레이션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-143">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="63f46-144">마이그레이션이 끝나면 Microsoft Visual Studio는 백업 파일 경로, 설치한 패키지 목록(최상위 종속성), 전이적 종속성으로 참조되는 패키지 목록, 마이그레이션 시작 시 식별되는 호환성 문제 목록이 포함된 보고서를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-144">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="63f46-145">보고서는 백업 폴더에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-145">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="63f46-146">솔루션이 빌드되고 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-146">Validate that the solution builds and runs.</span></span> <span data-ttu-id="63f46-147">문제가 발생하는 경우, [GitHub에 문제를 보고](https://github.com/NuGet/Home/issues/)하세요.</span><span class="sxs-lookup"><span data-stu-id="63f46-147">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="63f46-148">packages.config로 롤백하는 방법</span><span class="sxs-lookup"><span data-stu-id="63f46-148">How to roll back to packages.config</span></span>

1. <span data-ttu-id="63f46-149">마이그레이션된 프로젝트를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-149">Close the migrated project.</span></span>

1. <span data-ttu-id="63f46-150">백업한 프로젝트 파일과 `packages.config`(일반적으로 `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`에 위치)를 프로젝트 폴더에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-150">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span> <span data-ttu-id="63f46-151">obj 폴더가 프로젝트 루트 디렉터리에 있으면 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-151">Delete the obj folder if it exists in the project root directory.</span></span>

1. <span data-ttu-id="63f46-152">프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-152">Open the project.</span></span>

1. <span data-ttu-id="63f46-153">**도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 메뉴 명령을 사용하여 패키지 관리자 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-153">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="63f46-154">콘솔에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-154">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a><span data-ttu-id="63f46-155">마이그레이션 후 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="63f46-155">Create a package after migration</span></span>

<span data-ttu-id="63f46-156">마이그레이션이 완료되면 [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) NuGet 패키지에 대한 참조를 추가한 다음 [msbuild -t:pack](../reference/msbuild-targets.md#pack-target)을 사용하여 패키지를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-156">Once the migration is complete, we recommend that you add a reference to the [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget package, and then use [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) to create the package.</span></span> <span data-ttu-id="63f46-157">일부 시나리오에서는 `msbuild -t:pack` 대신 `dotnet.exe pack`을 사용할 수 있지만, 이는 권장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-157">Although in some scenarios you could use `dotnet.exe pack` instead of `msbuild -t:pack`, it is not recommended.</span></span>

## <a name="package-compatibility-issues"></a><span data-ttu-id="63f46-158">패키지 호환성 문제</span><span class="sxs-lookup"><span data-stu-id="63f46-158">Package compatibility issues</span></span>

<span data-ttu-id="63f46-159">packages.config에서 지원되던 일부 요소가 PackageReference에서는 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-159">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="63f46-160">마이그레이터는 이러한 문제를 분석하고 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-160">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="63f46-161">다음 중 하나 이상의 문제가 있는 패키지는 마이그레이션 후 예상대로 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-161">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="63f46-162">패키지가 마이그레이션 후에 설치되면 "install.ps1" 스크립트가 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-162">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="63f46-163">**설명**</span><span class="sxs-lookup"><span data-stu-id="63f46-163">**Description**</span></span> | <span data-ttu-id="63f46-164">PackageReference를 사용하면 패키지를 설치하거나 제거하는 동안 install.ps1 및 uninstall.ps1 PowerShell 스크립트가 실행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-164">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="63f46-165">**잠재적 영향**</span><span class="sxs-lookup"><span data-stu-id="63f46-165">**Potential impact**</span></span> | <span data-ttu-id="63f46-166">대상 프로젝트에서 일부 동작을 구성하기 위해 이러한 스크립트에 의존하는 패키지가 예상대로 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-166">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="63f46-167">패키지가 마이그레이션 후에 설치되면 "콘텐츠" 자산을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-167">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="63f46-168">**설명**</span><span class="sxs-lookup"><span data-stu-id="63f46-168">**Description**</span></span> | <span data-ttu-id="63f46-169">패키지의 `content` 폴더에 있는 자산은 PackageReference를 통해 지원되지 않으며 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-169">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="63f46-170">PackageReference는 `contentFiles`에 대한 지원을 추가하여 더 나은 전이적 지원 및 공유 콘텐츠를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-170">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="63f46-171">**잠재적 영향**</span><span class="sxs-lookup"><span data-stu-id="63f46-171">**Potential impact**</span></span> | <span data-ttu-id="63f46-172">`content`의 자산은 프로젝트에 복사되지 않고, 이러한 자산의 존재에 영향을 받는 프로젝트 코드에는 리팩터링이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-172">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="63f46-173">패키지가 업그레이드 후에 설치되면 XDT 변환이 적용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-173">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="63f46-174">**설명**</span><span class="sxs-lookup"><span data-stu-id="63f46-174">**Description**</span></span> | <span data-ttu-id="63f46-175">PackageReference는 XDT 변환을 지원하지 않으며 패키지를 설치하거나 제거하는 경우 `.xdt` 파일이 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-175">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="63f46-176">**잠재적 영향**</span><span class="sxs-lookup"><span data-stu-id="63f46-176">**Potential impact**</span></span> | <span data-ttu-id="63f46-177">XDT 변환은 모든 프로젝트 XML 파일(가장 일반적으로 `web.config.install.xdt` 및 `web.config.uninstall.xdt`)에 적용되지 않습니다. 즉, 패키지를 설치하거나 제거할 때 프로젝트의 ` web.config` 파일이 업데이트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-177">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="63f46-178">패키지가 마이그레이션 후에 설치되면 lib 루트의 어셈블리가 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-178">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="63f46-179">**설명**</span><span class="sxs-lookup"><span data-stu-id="63f46-179">**Description**</span></span> | <span data-ttu-id="63f46-180">PackageReference를 사용하면 대상 프레임워크 특정 하위 폴더가 없는 `lib` 폴더의 루트에 있는 어셈블리가 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-180">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="63f46-181">NuGet은 프로젝트의 대상 프레임워크에 해당하는 TFM(대상 프레임워크 모니커)과 일치하는 하위 폴더를 찾은 다음, 프로젝트에 일치하는 어셈블리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-181">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="63f46-182">**잠재적 영향**</span><span class="sxs-lookup"><span data-stu-id="63f46-182">**Potential impact**</span></span> | <span data-ttu-id="63f46-183">프로젝트의 대상 프레임워크에 해당하는 TFM(대상 프레임워크 모니커)과 일치하는 하위 폴더가 없는 패키지는 전환 후 예상대로 작동하지 않거나 마이그레이션 도중 설치에 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63f46-183">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="63f46-184">문제를 발견했나요?</span><span class="sxs-lookup"><span data-stu-id="63f46-184">Found an issue?</span></span> <span data-ttu-id="63f46-185">그렇다면 보고해주세요.</span><span class="sxs-lookup"><span data-stu-id="63f46-185">Report it!</span></span>

<span data-ttu-id="63f46-186">마이그레이션 환경에 문제가 발생하는 경우 [NuGet GitHub 리포지토리에 문제를 보고](https://github.com/NuGet/Home/issues/)하세요.</span><span class="sxs-lookup"><span data-stu-id="63f46-186">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
