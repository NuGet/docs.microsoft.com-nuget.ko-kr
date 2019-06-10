---
title: PackageReference 형식을 package.config에서 마이그레이션
description: NuGet 4.0 이상, VS2017 및.NET Core 2.0에서 지원 되는 PackageReference로 package.config 관리 형식에서 프로젝트를 마이그레이션하는 방법에 대 한 세부 정보
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 09d132aeaf00d2a1d095b9638b455cc23de91f2c
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812882"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="1bb2b-103">Packages.config를 PackageReference로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="1bb2b-103">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="1bb2b-104">Visual Studio 2017 버전 15.7 및 이상에서는 지원에서 프로젝트를 마이그레이션하는 [packages.config](./packages-config.md) 관리 형식을 합니다 [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-104">Visual Studio 2017 Version 15.7 and later supports migrating a project from the [packages.config](./packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="1bb2b-105">PackageReference를 사용할 때의 이점</span><span class="sxs-lookup"><span data-stu-id="1bb2b-105">Benefits of using PackageReference</span></span>

* <span data-ttu-id="1bb2b-106">**한 곳에서 모든 프로젝트 종속성을 관리**: 프로젝트 간 참조 및 어셈블리 참조와 마찬가지로 NuGet 패키지 참조 (사용 하 여는 `PackageReference` 노드) 별도 packages.config 파일을 사용 하는 것이 아니라 프로젝트 파일 내에서 직접 관리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-106">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="1bb2b-107">**최상위 종속성 깔끔하게 보기**: 달리 packages.config를 PackageReference 프로젝트에 직접 설치 하는 NuGet 패키지만 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-107">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="1bb2b-108">결과적으로, 하위 수준 종속성을 사용 하 여 NuGet 패키지 관리자 UI 및 프로젝트 파일 복잡 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-108">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="1bb2b-109">**성능 향상**: PackageReference를 사용 하 여 패키지에서 유지 됩니다 합니다 *전역 패키지* 폴더 (에 설명 된 대로 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md) 대신는 `packages` 내의 폴더를 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-109">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="1bb2b-110">결과적으로 PackageReference는 더 빠르게 수행 하 고 더 적은 디스크 공간만 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-110">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="1bb2b-111">**세부적으로 종속성과 콘텐츠 흐름 제어**: MSBuild의 기존 기능을 사용 하면 [NuGet 패키지를 조건부로 참조할](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) 대상 프레임 워크, 구성, 플랫폼 또는 다른 피벗 당 패키지 참조를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-111">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="1bb2b-112">**PackageReference는 활성 개발 중**: 참조 [PackageReference github 문제](https://aka.ms/nuget-pr-improvements)합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-112">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="1bb2b-113">packages.config는 더 이상 활성 개발 중입니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-113">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="1bb2b-114">제한 사항</span><span class="sxs-lookup"><span data-stu-id="1bb2b-114">Limitations</span></span>

* <span data-ttu-id="1bb2b-115">NuGet PackageReference Visual Studio 2015에서 사용할 수 있으며 이전 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-115">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="1bb2b-116">Visual Studio 2017 에서만에서 마이그레이션된 프로젝트를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-116">Migrated projects can be opened only in Visual Studio 2017.</span></span>
* <span data-ttu-id="1bb2b-117">마이그레이션에 대 한 현재 제공 되지 않습니다. C++ 및 ASP.NET 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-117">Migration is not currently available for C++ and ASP.NET projects.</span></span>
* <span data-ttu-id="1bb2b-118">일부 패키지를 PackageReference를 사용 하 여 완벽 하 게 호환 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-118">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="1bb2b-119">자세한 내용은 [패키지 호환성 문제](#package-compatibility-issues)합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-119">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

### <a name="known-issues"></a><span data-ttu-id="1bb2b-120">알려진 문제</span><span class="sxs-lookup"><span data-stu-id="1bb2b-120">Known Issues</span></span>

1. <span data-ttu-id="1bb2b-121">`Migrate packages.config to PackageReference...` 옵션을 오른쪽 클릭 상황에 맞는 메뉴에서 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-121">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span> 

#### <a name="issue"></a><span data-ttu-id="1bb2b-122">문제</span><span class="sxs-lookup"><span data-stu-id="1bb2b-122">Issue</span></span> 
 
<span data-ttu-id="1bb2b-123">프로젝트를 처음 열면 NuGet 작업이 수행될 때까지 NuGet을 초기화할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-123">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="1bb2b-124">이로 인해 마이그레이션 옵션이 `packages.config` 또는 `References`의 오른쪽 클릭 상황에 맞는 메뉴에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-124">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span> 

#### <a name="workaround"></a><span data-ttu-id="1bb2b-125">해결 방법</span><span class="sxs-lookup"><span data-stu-id="1bb2b-125">Workaround</span></span> 

<span data-ttu-id="1bb2b-126">다음 NuGet 작업 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-126">Perform any one of the following NuGet actions:</span></span> 
* <span data-ttu-id="1bb2b-127">패키지 관리자 UI 열기 - `References`를 마우스 오른쪽 단추로 클릭하고 `Manage NuGet Packages...`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-127">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span> 
* <span data-ttu-id="1bb2b-128">패키지 관리자 콘솔 열기 - `Tools > NuGet Package Manager`에서 `Package Manager Console`을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-128">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span> 
* <span data-ttu-id="1bb2b-129">NuGet 복원 실행 - 솔루션 탐색기에서 솔루션 노드를 마우스 오른쪽 단추로 클릭하고 `Restore NuGet Packages`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-129">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span> 
* <span data-ttu-id="1bb2b-130">NuGet 복원을 트리거하는 프로젝트 빌드</span><span class="sxs-lookup"><span data-stu-id="1bb2b-130">Build the project which also triggers NuGet restore</span></span> 

<span data-ttu-id="1bb2b-131">이제 마이그레이션 옵션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-131">You should now be able to see the migration option.</span></span> <span data-ttu-id="1bb2b-132">이 옵션은 지원되지 않으며 ASP.NET 및 C++ 프로젝트 형식에 대해 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-132">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span> 

## <a name="migration-steps"></a><span data-ttu-id="1bb2b-133">마이그레이션 단계</span><span class="sxs-lookup"><span data-stu-id="1bb2b-133">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="1bb2b-134">Visual Studio 수 있도록 프로젝트의 백업을 만듭니다 마이그레이션을 시작 하기 전에 [롤백 packages.config](#how-to-roll-back-to-packagesconfig) 필요한 경우.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-134">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="1bb2b-135">사용 하 여 프로젝트를 포함 하는 솔루션을 열고 `packages.config`합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-135">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="1bb2b-136">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 합니다 **참조** 노드 또는 `packages.config` 파일을 선택 **packages.config를 PackageReference로 마이그레이션 중...** .</span><span class="sxs-lookup"><span data-stu-id="1bb2b-136">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="1bb2b-137">마이 그레이터 프로젝트의 NuGet 패키지 참조를 분석 하 고 가져와서 분류 하려고 **최상위 종속성** (직접 설치한 NuGet 패키지) 및 **전이적 종속성** (최상위 패키지의 종속성으로 설치 된 패키지).</span><span class="sxs-lookup"><span data-stu-id="1bb2b-137">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directly) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="1bb2b-138">PackageReference 전이적 패키지 복원을 지 및 종속성을 동적으로 확인 하 여 전이적 종속성 필요를 설치 하지 않도록 명시적으로 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-138">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="1bb2b-139">(선택 사항) 선택 하 여 최상위 종속성으로 전이적 종속성으로 분류 하는 NuGet 패키지를 처리 하도록 선택할 수 있습니다 합니다 **최상위** 패키지에 대 한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-139">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="1bb2b-140">이 옵션은 전이적으로 이동 하지 마십시오는 자산을 포함 하는 패키지에 대 한 자동으로 설정 됩니다 (에 `build`, `buildCrossTargeting`를 `contentFiles`, 또는 `analyzers` 폴더) 및 개발 종속성으로 표시 된 것 (`developmentDependency = "true"`).</span><span class="sxs-lookup"><span data-stu-id="1bb2b-140">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="1bb2b-141">검토 [패키지 호환성 문제](#package-compatibility-issues)합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-141">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="1bb2b-142">선택 **확인** 마이그레이션을 시작 하려면.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-142">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="1bb2b-143">마이그레이션 후에 Visual Studio 백업, 설치 된 패키지 (최상위 종속성)의 목록, 전이적 종속성으로 참조 하는 패키지 목록을 및 시작할 때 식별 하는 호환성 문제 목록을 경로 사용 하 여 보고서를 제공 마이그레이션입니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-143">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="1bb2b-144">보고서는 백업 폴더에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-144">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="1bb2b-145">솔루션 빌드 및 실행 되는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-145">Validate that the solution builds and runs.</span></span> <span data-ttu-id="1bb2b-146">문제가 발생 하는 경우 [GitHub에서 문제를 제출](https://github.com/NuGet/Home/issues/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-146">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="1bb2b-147">Packages.config를 롤백해야 하는 방법</span><span class="sxs-lookup"><span data-stu-id="1bb2b-147">How to roll back to packages.config</span></span>

1. <span data-ttu-id="1bb2b-148">마이그레이션된 프로젝트를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-148">Close the migrated project.</span></span>

1. <span data-ttu-id="1bb2b-149">프로젝트 파일을 복사 하 고 `packages.config` 백업에서 (일반적으로 `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) 프로젝트 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-149">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span> <span data-ttu-id="1bb2b-150">프로젝트 루트 디렉터리에 있는 경우 obj 폴더를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-150">Delete the obj folder if it exists in the project root directory.</span></span>

1. <span data-ttu-id="1bb2b-151">프로젝트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-151">Open the project.</span></span>

1. <span data-ttu-id="1bb2b-152">사용 하 여 패키지 관리자 콘솔을 엽니다는 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 메뉴 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-152">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="1bb2b-153">콘솔에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-153">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a><span data-ttu-id="1bb2b-154">마이그레이션 후 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="1bb2b-154">Create a package after migration</span></span>

<span data-ttu-id="1bb2b-155">마이그레이션이 완료 되 면에 대 한 참조를 추가 하는 것이 좋습니다는 [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget 패키지를 사용 하 여 선택한 [msbuild 팩](../reference/msbuild-targets.md#pack-target) 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-155">Once the migration is complete, we recommend that you add a reference to the [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget package, and then use [msbuild pack](../reference/msbuild-targets.md#pack-target) to create the package.</span></span> <span data-ttu-id="1bb2b-156">일부 시나리오에서 사용할 수 있지만 `dotnet.exe pack` 대신 `msbuild pack`, 권장 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-156">Although in some scenarios you could use `dotnet.exe pack` instead of `msbuild pack`, it is not recommended.</span></span>

## <a name="package-compatibility-issues"></a><span data-ttu-id="1bb2b-157">패키지 호환성 문제</span><span class="sxs-lookup"><span data-stu-id="1bb2b-157">Package compatibility issues</span></span>

<span data-ttu-id="1bb2b-158">Packages.config에 지원 하 던 일부 측면은 PackageReference에 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-158">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="1bb2b-159">마이 그레이터 분석 하 고 이러한 문제를 감지 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-159">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="1bb2b-160">다음 문제 중 하나 이상을 포함 하는 모든 패키지 마이그레이션 후 예상 대로 동작 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-160">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="1bb2b-161">마이그레이션 후 패키지를 설치할 때 "install.ps1" 스크립트는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-161">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1bb2b-162">**설명**</span><span class="sxs-lookup"><span data-stu-id="1bb2b-162">**Description**</span></span> | <span data-ttu-id="1bb2b-163">Uninstall.ps1 / install.ps1 PowerShell 스크립트는 PackageReference를 사용 하 여 설치 하거나 패키지를 제거 하는 동안 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-163">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="1bb2b-164">**잠재적인 영향**</span><span class="sxs-lookup"><span data-stu-id="1bb2b-164">**Potential impact**</span></span> | <span data-ttu-id="1bb2b-165">대상 프로젝트에서 몇 가지 동작을 구성 하는 이러한 스크립트에 종속 된 패키지가 예상 대로 작동 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-165">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="1bb2b-166">마이그레이션 후 패키지를 설치할 때 "콘텐츠" 자산 사용할 수 없는</span><span class="sxs-lookup"><span data-stu-id="1bb2b-166">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1bb2b-167">**설명**</span><span class="sxs-lookup"><span data-stu-id="1bb2b-167">**Description**</span></span> | <span data-ttu-id="1bb2b-168">패키지의 자산 `content` 폴더는 PackageReference를 사용 하 여 지원 되지 않으며 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-168">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="1bb2b-169">에 대 한 지원을 추가 하는 PackageReference `contentFiles` 전이적 지원 향상 및 공유 콘텐츠입니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-169">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="1bb2b-170">**잠재적인 영향**</span><span class="sxs-lookup"><span data-stu-id="1bb2b-170">**Potential impact**</span></span> | <span data-ttu-id="1bb2b-171">자산 `content` 복사 되지 않습니다 프로젝트 및 프로젝트에 해당 자산에 의존 하는 코드 리팩터링 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-171">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="1bb2b-172">XDT 변환에는 업그레이드 후 패키지를 설치할 때 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-172">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1bb2b-173">**설명**</span><span class="sxs-lookup"><span data-stu-id="1bb2b-173">**Description**</span></span> | <span data-ttu-id="1bb2b-174">XDT 변환 PackageReference를 사용 하 여 지원 되지 않습니다 및 `.xdt` 설치 하거나 패키지를 제거 하는 경우 파일은 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-174">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="1bb2b-175">**잠재적인 영향**</span><span class="sxs-lookup"><span data-stu-id="1bb2b-175">**Potential impact**</span></span> | <span data-ttu-id="1bb2b-176">XDT 변환에 적용 되지 않은 모든 프로젝트 XML 파일을 사용 하 여 가장 일반적으로 `web.config.install.xdt` 하 고 `web.config.uninstall.xdt`, 즉, 프로젝트의` web.config` 패키지를 설치 하거나 제거 하는 경우에 파일이 업데이트 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-176">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="1bb2b-177">마이그레이션 후 패키지를 설치할 때 어셈블리 lib 루트에서 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-177">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="1bb2b-178">**설명**</span><span class="sxs-lookup"><span data-stu-id="1bb2b-178">**Description**</span></span> | <span data-ttu-id="1bb2b-179">PackageReference를 사용 하 여 어셈블리의 루트에 있는 `lib` 대상 프레임 워크 특정 하위 폴더를 제외 하 고 폴더는 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-179">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="1bb2b-180">NuGet은 프로젝트의 대상 프레임 워크에 해당 대상 프레임 워크 모니커 (TFM)와 일치 하는 하위 폴더를 찾아 프로젝트에는 일치 하는 어셈블리를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-180">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="1bb2b-181">**잠재적인 영향**</span><span class="sxs-lookup"><span data-stu-id="1bb2b-181">**Potential impact**</span></span> | <span data-ttu-id="1bb2b-182">프로젝트의 대상 프레임 워크에 해당 대상 프레임 워크 모니커 (TFM)와 일치 하는 하위 폴더에 있지 않은 패키지 있습니다 전환 후 예상 대로 작동 않거나 마이그레이션하는 동안 설치 실패</span><span class="sxs-lookup"><span data-stu-id="1bb2b-182">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="1bb2b-183">문제를 찾을 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="1bb2b-183">Found an issue?</span></span> <span data-ttu-id="1bb2b-184">보고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-184">Report it!</span></span>

<span data-ttu-id="1bb2b-185">마이그레이션 환경 사용 하 여 문제를 실행 하는 경우 하세요 [NuGet GitHub 리포지토리에서 문제를 제출](https://github.com/NuGet/Home/issues/)합니다.</span><span class="sxs-lookup"><span data-stu-id="1bb2b-185">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
