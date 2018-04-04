---
title: Package.config에서 PackageReference 형식으로 마이그레이션 | Microsoft Docs
author: karann-msft
ms.author: karann
manager: unniravindranathan
ms.date: 03/27/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet 4.0 이상 및 VS2017 및.NET Core 2.0에서 지 원하는 대로 PackageReference를 package.config 관리 형식에서 프로젝트를 마이그레이션하는 방법에 대 한 세부 정보
keywords: NuGet migrator 마이그레이션, 참조 패키지 파일을 PackageReference, packages.config 프로젝트 VS2017, Visual Studio 2017, NuGet 4,.NET Core 2.0
ms.reviewer:
- karann
- unnir
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 10bd2fe95a6af11806a7edd7a43eaa497486fd80
ms.sourcegitcommit: ecb598c790d4154366bc92757ec7db1a51c34faf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/03/2018
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="dac2d-104">Packages.config에서 PackageReference로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="dac2d-104">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="dac2d-105">Visual Studio 2017 버전 15.7 미리 보기 3 및 이상에서는에서 프로젝트를 마이그레이션하는 [packages.config](./packages-config.md) 관리 형식에는 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-105">Visual Studio 2017 Version 15.7 Preview 3 and later supports migrating a project from the [packages.config](./packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="dac2d-106">PackageReference 사용의 이점</span><span class="sxs-lookup"><span data-stu-id="dac2d-106">Benefits of using PackageReference</span></span>

* <span data-ttu-id="dac2d-107">**한 곳에서 모든 프로젝트 종속성을 관리**: 프로젝트 간 참조 및 어셈블리 참조와 마찬가지로 NuGet 패키지에서 참조 (사용 하는 `PackageReference` 노드) 프로젝트 파일 내에서 직접 관리 되는 별도 사용 하 여 보다는 packages.config 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-107">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="dac2d-108">**깔끔하게 보기의 최상위 종속성**: PackageReference 달리 packages.config을 직접 프로젝트에 설치 된 NuGet 패키지만 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-108">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="dac2d-109">결과적으로, 하위 종속성이 NuGet 패키지 관리자 UI 및 프로젝트 파일 복잡 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-109">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="dac2d-110">**성능 향상**: PackageReference를 사용 하 여 패키지에서 유지 되므로 *전역 패키지* 폴더 (에 설명 된 대로 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md) 대신는 `packages` 솔루션 내에서 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-110">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="dac2d-111">결과적으로, PackageReference는 더 빠르게 수행 하 고 더 적은 디스크 공간만 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-111">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="dac2d-112">**콘텐츠 흐름 및 종속성에 대 한 제어를 미세**: MSBuild의 기존 기능을 사용 하면를 [NuGet 패키지를 참조 하는 조건에 따라](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) 대상 프레임 워크 당 패키지 참조를 선택 하 고 구성, 플랫폼 또는 다른 피벗 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-112">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="dac2d-113">**현재 개발 중 PackageReference**: 참조 [PackageReference GitHub에 대 한 문제](https://aka.ms/nuget-pr-improvements)합니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-113">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="dac2d-114">packages.config를 더 이상 현재 개발에 포함.</span><span class="sxs-lookup"><span data-stu-id="dac2d-114">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="dac2d-115">제한 사항</span><span class="sxs-lookup"><span data-stu-id="dac2d-115">Limitations</span></span>

* <span data-ttu-id="dac2d-116">Visual Studio 2015에서 사용할 수 있는 및 이전 NuGet PackageReference 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-116">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="dac2d-117">Visual Studio 2017 에서만에서 마이그레이션된 프로젝트를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-117">Migrated projects can be opened only in Visual Studio 2017.</span></span>
* <span data-ttu-id="dac2d-118">마이그레이션에 c + + 및 ASP.NET 프로젝트에 대 한 현재 사용할 수 없는 경우</span><span class="sxs-lookup"><span data-stu-id="dac2d-118">Migration is not currently available for C++ and ASP.NET project.</span></span>
* <span data-ttu-id="dac2d-119">일부 패키지는 PackageReference 완벽 하 게 호환 일 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-119">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="dac2d-120">자세한 내용은 참조 [패키지 호환성 문제](#package-compatibility-issues)합니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-120">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

## <a name="migration-steps"></a><span data-ttu-id="dac2d-121">마이그레이션 단계</span><span class="sxs-lookup"><span data-stu-id="dac2d-121">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="dac2d-122">Visual Studio 수 있도록 프로젝트의 백업을 만듭니다 마이그레이션을 시작 하기 전에 [롤백 packages.config](#how-to-roll-back-to-packagesconfig) 필요한 경우.</span><span class="sxs-lookup"><span data-stu-id="dac2d-122">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="dac2d-123">사용 하 여 프로젝트를 포함 하는 솔루션을 열고 `packages.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-123">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="dac2d-124">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭는 **참조** 노드 또는 `packages.config` 파일을 선택 **packages.config PackageReference로 마이그레이션 중...** .</span><span class="sxs-lookup"><span data-stu-id="dac2d-124">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="dac2d-125">migrator 프로젝트의 NuGet 패키지 참조를 분석 하 고 분류로을 **최상위 종속성** (NuGet 패키지를 해당 설치 디렉터리) 및 **전이 종속성**(최상위 패키지의 종속성으로 설치 된 패키지).</span><span class="sxs-lookup"><span data-stu-id="dac2d-125">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directory) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="dac2d-126">PackageReference 전이적 패키지 복원이 지원 하 고 종속성을 동적으로 확인 하 여 전이 종속성 필요를 설치 하지 않도록 명시적으로 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-126">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="dac2d-127">(선택 사항) 선택 하 여 최상위 종속성으로 전이적 종속성으로 분류 하는 NuGet 패키지를 처리 하도록 선택할 수 있습니다는 **최상위** 패키지에 대 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-127">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="dac2d-128">이 옵션은 전이적으로 전달 하지 않는 자산을 포함 하는 패키지에 대 한 자동으로 설정 됩니다 (에 `build`, `buildCrossTargeting`, `contentFiles`, 또는 `analyzers` 폴더) 및 개발 종속성으로 표시 된 것 (`developmentDependency = "true"`).</span><span class="sxs-lookup"><span data-stu-id="dac2d-128">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="dac2d-129">모든 검토 [패키지 호환성 문제](#package-compatibility-issues)합니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-129">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="dac2d-130">선택 **확인** 마이그레이션을 시작 하려면.</span><span class="sxs-lookup"><span data-stu-id="dac2d-130">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="dac2d-131">백업, 설치 된 패키지 (최상위 종속성) 목록, 전이적 종속성으로 참조 패키지 목록 및 시작 될 때 식별 하는 호환성 문제 목록은에 Visual Studio 제공 경로 사용 하 여 보고서 마이그레이션 후에 마이그레이션입니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-131">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="dac2d-132">보고서는 백업 폴더에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-132">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="dac2d-133">솔루션 빌드 및 실행 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-133">Validate that the solution builds and runs.</span></span> <span data-ttu-id="dac2d-134">문제가 발생 하는 경우 [GitHub에서 문제를 제출](https://github.com/NuGet/Home/issues/)합니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-134">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="dac2d-135">Packages.config를 롤백해야 하는 방법</span><span class="sxs-lookup"><span data-stu-id="dac2d-135">How to roll back to packages.config</span></span>

1. <span data-ttu-id="dac2d-136">마이그레이션된 프로젝트를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-136">Close the migrated project.</span></span>

1. <span data-ttu-id="dac2d-137">프로젝트 파일을 복사 하 고 `packages.config` 백업에서 (일반적으로 `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) 프로젝트 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-137">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span>

1. <span data-ttu-id="dac2d-138">프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-138">Open the project.</span></span>

1. <span data-ttu-id="dac2d-139">사용 하 여 패키지 관리자 콘솔을 열고는 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 메뉴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-139">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="dac2d-140">콘솔에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-140">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a><span data-ttu-id="dac2d-141">패키지 호환성 문제</span><span class="sxs-lookup"><span data-stu-id="dac2d-141">Package compatibility issues</span></span>

<span data-ttu-id="dac2d-142">Packages.config에서 지원 되 던 일부 측면 PackageReference에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-142">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="dac2d-143">migrator를 분석 하 고 이러한 문제를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-143">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="dac2d-144">다음 문제 중 하나 이상을 포함 하는 모든 패키지 마이그레이션 후 예상 대로 동작 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-144">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="dac2d-145">마이그레이션 후 패키지를 설치할 때 "install.ps1" 스크립트가 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-145">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dac2d-146">**설명**</span><span class="sxs-lookup"><span data-stu-id="dac2d-146">**Description**</span></span> | <span data-ttu-id="dac2d-147">PackageReference와 install.ps1 / uninstall.ps1 PowerShell 스크립트는 설치 하거나 패키지를 제거 하는 동안 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-147">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="dac2d-148">**잠재적인 영향**</span><span class="sxs-lookup"><span data-stu-id="dac2d-148">**Potential impact**</span></span> | <span data-ttu-id="dac2d-149">대상 프로젝트에 몇 가지 동작을 구성 하는 이러한 스크립트에 종속 된 패키지 예상 대로 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-149">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="dac2d-150">마이그레이션 후 패키지를 설치할 때 "콘텐츠" 자산 사용할 수 없는</span><span class="sxs-lookup"><span data-stu-id="dac2d-150">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dac2d-151">**설명**</span><span class="sxs-lookup"><span data-stu-id="dac2d-151">**Description**</span></span> | <span data-ttu-id="dac2d-152">패키지의 자산 `content` 폴더 PackageReference와 지원 되지 않으며 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-152">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="dac2d-153">에 대 한 지원을 추가 하는 PackageReference `contentFiles` 더 잘 전이적 지원 및 공유 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-153">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="dac2d-154">**잠재적인 영향**</span><span class="sxs-lookup"><span data-stu-id="dac2d-154">**Potential impact**</span></span> | <span data-ttu-id="dac2d-155">자산에 `content` 복사 되지 않습니다 프로젝트와 프로젝트에 이러한 자산의 존재 여부에 종속 된 코드가 리팩터링 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-155">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="dac2d-156">업그레이드 후 패키지를 설치 하는 경우 XDT 변환은 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-156">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dac2d-157">**설명**</span><span class="sxs-lookup"><span data-stu-id="dac2d-157">**Description**</span></span> | <span data-ttu-id="dac2d-158">PackageReference XDT 변환은 지원 되지 않습니다 및 `.xdt` 설치 하거나 패키지를 제거 하는 경우 파일은 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-158">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="dac2d-159">**잠재적인 영향**</span><span class="sxs-lookup"><span data-stu-id="dac2d-159">**Potential impact**</span></span> | <span data-ttu-id="dac2d-160">XDT 변환에 적용 되지 않은 모든 프로젝트 XML 파일을 사용 하 여 가장 일반적으로 `web.config.install.xdt` 및 `web.config.uninstall.xdt`, 즉, 프로젝트의` web.config` 패키지 설치 하거나 제거 하는 경우 파일이 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-160">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="dac2d-161">Lib 루트의 어셈블리는 마이그레이션 후 패키지를 설치할 때 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-161">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="dac2d-162">**설명**</span><span class="sxs-lookup"><span data-stu-id="dac2d-162">**Description**</span></span> | <span data-ttu-id="dac2d-163">루트에 있는 어셈블리와 PackageReference, `lib` 대상 프레임 워크 특정 하위 폴더 제외 하 고 폴더는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-163">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="dac2d-164">NuGet에 해당 하는 프로젝트의 대상 프레임 워크 대상 프레임 워크 모니커 (TFM)와 일치 하는 하위 폴더를 찾아 프로젝트에는 일치 하는 어셈블리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-164">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="dac2d-165">**잠재적인 영향**</span><span class="sxs-lookup"><span data-stu-id="dac2d-165">**Potential impact**</span></span> | <span data-ttu-id="dac2d-166">패키지에 해당 하는 프로젝트의 대상 프레임 워크 대상 프레임 워크 모니커 (TFM)와 일치 하는 하위 폴더를 갖지 않는 전환 된 후 예상 대로 작동 없거나 마이그레이션하는 동안 설치 실패</span><span class="sxs-lookup"><span data-stu-id="dac2d-166">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="dac2d-167">문제를 찾을 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="dac2d-167">Found an issue?</span></span> <span data-ttu-id="dac2d-168">이 보고!</span><span class="sxs-lookup"><span data-stu-id="dac2d-168">Report it!</span></span>

<span data-ttu-id="dac2d-169">마이그레이션 experience와 함께 문제가 발생 실행 하는 경우 다음 문의 [NuGet GitHub 리포지토리에서 문제를 제출](https://github.com/NuGet/Home/issues/)합니다.</span><span class="sxs-lookup"><span data-stu-id="dac2d-169">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
