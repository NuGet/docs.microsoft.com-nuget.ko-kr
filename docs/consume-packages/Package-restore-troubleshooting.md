---
title: Visual Studio에서 NuGet 패키지 복원 문제 해결
description: Visual Studio의 일반적인 NuGet 복원 오류 및 해당 오류를 해결하는 방법의 설명입니다.
author: JonDouglas
ms.author: jodou
ms.date: 05/25/2018
ms.topic: conceptual
ms.openlocfilehash: 0bd14104695a15d2e4c65a13b271143809c4ba8a
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323624"
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="5a381-103">패키지 복원 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="5a381-103">Troubleshooting package restore errors</span></span>

<span data-ttu-id="5a381-104">이 아티클에서는 패키지를 복원할 때 일반적인 오류 및 해당 문제를 해결하는 단계를 집중적으로 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-104">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> 

<span data-ttu-id="5a381-105">패키지 복원은 프로젝트 파일( *.csproj*) 또는 *packages.config* 파일에서 패키지 참조와 일치하는 올바른 상태에 대한 모든 패키지 종속성을 설치하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-105">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="5a381-106">(Visual Studio에서 참조는 솔루션 탐색기의 **종속성 \ NuGet** 또는 **참조** 노드 아래에 표시됩니다.) 패키지를 복원하는 데 필요한 단계를 수행하려면 [패키지 복원](../consume-packages/package-restore.md#restore-packages)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a381-106">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.) To follow the required steps to restore packages, see [Restore packages](../consume-packages/package-restore.md#restore-packages).</span></span> <span data-ttu-id="5a381-107">프로젝트 파일( *.csproj*) 또는 *packages.config* 파일의 패키지 참조가 잘못된 경우(패키지 복원 이후 원하는 상태와 일치하지 않는 경우) 패키지 복원을 사용하는 대신 패키지를 설치하거나 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-107">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead of using Package Restore.</span></span>

<span data-ttu-id="5a381-108">이 지침으로 문제가 해결되지 않을 경우 귀하의 시나리오를 더 면밀히 살펴볼 수 있도록 [GitHub에서 문제를 제출](https://github.com/NuGet/docs.microsoft.com-nuget/issues)해 주세요.</span><span class="sxs-lookup"><span data-stu-id="5a381-108">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="5a381-109">이 페이지에 표시되는 "이 페이지가 도움이 되었나요?"</span><span class="sxs-lookup"><span data-stu-id="5a381-109">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="5a381-110">컨트롤은 사용하지 마세요. Microsoft에서 귀하에게 연락하여 자세한 내용을 확인할 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-110">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="5a381-111">Visual Studio 사용자를 위한 빠른 해결책</span><span class="sxs-lookup"><span data-stu-id="5a381-111">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="5a381-112">Visual Studio를 사용하는 경우 먼저 다음과 같이 패키지 복원을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-112">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="5a381-113">그러지 않을 경우 다음에 나오는 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-113">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="5a381-114">**도구 > NuGet 패키지 관리자 > 패키지 관리자 설정** 메뉴 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-114">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="5a381-115">**패키지 복원** 에서 두 옵션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-115">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="5a381-116">**확인** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-116">Select **OK**.</span></span>
1. <span data-ttu-id="5a381-117">프로젝트를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-117">Build your project again.</span></span>

![도구/옵션에서 NuGet 패키지 복원 활성화](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="5a381-119">이러한 설정은 `NuGet.Config` 파일에서도 변경할 수 있습니다. [동의](#consent) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5a381-119">These settings can also be changed in your `NuGet.Config` file; see the [consent](#consent) section.</span></span> <span data-ttu-id="5a381-120">프로젝트가 MSBuild 통합 패키지 복원을 사용하는 이전 프로젝트인 경우 자동 패키지 복원으로 [마이그레이션](package-restore.md#migrate-to-automatic-package-restore-visual-studio)해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-120">If your project is an older project that uses the MSBuild-integrated package restore, you may need to [migrate](package-restore.md#migrate-to-automatic-package-restore-visual-studio) to automatic package restore.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="5a381-121">이 프로젝트는 이 컴퓨터에 없는 NuGet 패키지를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-121">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="5a381-122">전체 오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="5a381-122">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="5a381-123">이 오류는 하나 이상의 NuGet 패키지에 대한 참조를 포함하는 프로젝트를 빌드하려고 시도할 때 해당 패키지가 컴퓨터 또는 프로젝트에 현재 설치되지 않은 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-123">This error occurs when you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently installed on the computer or in the project.</span></span>

- <span data-ttu-id="5a381-124">[PackageReference](package-references-in-project-files.md) 관리 형식을 사용할 경우 이 오류는 packages.config에서 PackageReference로 마이그레이션한 결과일 수 있으며 프로젝트 파일에서 [수동으로 제거](/nuget/resources/nuget-faq#working-with-packages)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-124">When using the [PackageReference](package-references-in-project-files.md) management format, this error might be a leftover from a packages.config to PackageReference migration and needs to be [manually removed](/nuget/resources/nuget-faq#working-with-packages) from the project file.</span></span>
- <span data-ttu-id="5a381-125">[packages.config](../reference/packages-config.md)를 사용할 경우 이 오류는 패키지가 솔루션 루트의 `packages` 폴더에 설치되어 있지 않음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-125">When using [packages.config](../reference/packages-config.md), the error means that the package is not installed in the `packages` folder at the solution root.</span></span>

<span data-ttu-id="5a381-126">이러한 상황은 일반적으로 소스 제어 또는 다른 다운로드에서 프로젝트의 소스 코드를 가져올 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-126">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="5a381-127">패키지는 nuget.org 같은 패키지 피드에서 복원할 수 있으므로 일반적으로 소스 제어 또는 다운로드에는 패키지가 없습니다([패키지 및 소스 제어](Packages-and-Source-Control.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="5a381-127">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="5a381-128">그렇지 않고 이를 포함할 경우 리포지토리가 블로트되거나 불필요하게 큰 .zip 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-128">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="5a381-129">프로젝트 파일에 패키지 위치에 대한 절대 경로를 포함하고 프로젝트를 이동하는 경우에 오류가 발생할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-129">The error can also happen if your project file contains absolute paths to package locations, and you move the project.</span></span>

<span data-ttu-id="5a381-130">패키지를 복원하려면 다음 방법 중 하나를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="5a381-130">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="5a381-131">프로젝트 파일을 이동한 경우 패키지 참조를 업데이트하도록 파일을 직접 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-131">If you've moved the project file, edit the file directly to update the package references.</span></span>
- <span data-ttu-id="5a381-132">[Visual Studio](package-restore.md#restore-using-visual-studio)([자동 복원](package-restore.md#restore-packages-automatically-using-visual-studio) 또는 [수동 복원](package-restore.md#restore-packages-manually-using-visual-studio))</span><span class="sxs-lookup"><span data-stu-id="5a381-132">[Visual Studio](package-restore.md#restore-using-visual-studio) ([automatic restore](package-restore.md#restore-packages-automatically-using-visual-studio) or [manual restore](package-restore.md#restore-packages-manually-using-visual-studio))</span></span>
- [<span data-ttu-id="5a381-133">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="5a381-133">dotnet CLI</span></span>](package-restore.md#restore-using-the-dotnet-cli)
- [<span data-ttu-id="5a381-134">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="5a381-134">nuget.exe CLI</span></span>](package-restore.md#restore-using-the-nugetexe-cli)
- [<span data-ttu-id="5a381-135">MSBuild</span><span class="sxs-lookup"><span data-stu-id="5a381-135">MSBuild</span></span>](package-restore.md#restore-using-msbuild)
- [<span data-ttu-id="5a381-136">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="5a381-136">Azure Pipelines</span></span>](package-restore.md#restore-using-azure-pipelines)
- [<span data-ttu-id="5a381-137">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="5a381-137">Azure DevOps Server</span></span>](package-restore.md#restore-using-azure-devops-server)

<span data-ttu-id="5a381-138">복원되면 패키지가 *global-packages* 폴더에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-138">After a successful restore, the package should be present in the *global-packages* folder.</span></span> <span data-ttu-id="5a381-139">PackageReference를 사용하는 프로젝트의 경우 복원에서 `obj/project.assets.json` 파일을 다시 만들어야 하고, `packages.config`를 사용하는 프로젝트의 경우 패키지가 프로젝트의 `packages` 폴더에 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-139">For projects using PackageReference, a restore should recreate the `obj/project.assets.json` file; for projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="5a381-140">이제 프로젝트가 성공적으로 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-140">The project should now build successfully.</span></span> <span data-ttu-id="5a381-141">그렇지 않을 경우 후속 조치를 위해 [GitHub에서 문제를 제출](https://github.com/NuGet/docs.microsoft.com-nuget/issues)해 주세요.</span><span class="sxs-lookup"><span data-stu-id="5a381-141">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="5a381-142">자산 파일 project.assets.json을 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="5a381-142">Assets file project.assets.json not found</span></span>

<span data-ttu-id="5a381-143">전체 오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="5a381-143">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="5a381-144">`project.assets.json` 파일은 PackageReference 관리 형식을 사용할 때 프로젝트의 종속성 그래프를 유지하며, 필요한 모든 패키지가 컴퓨터에 설치되어 있는지 확인하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-144">The `project.assets.json` file maintains a project's dependency graph when using the PackageReference management format, which is used to make sure that all necessary packages are installed on the computer.</span></span> <span data-ttu-id="5a381-145">이 파일은 패키지 복원을 통해 동적으로 생성되므로 일반적으로 소스 제어에는 추가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-145">Because this file is generated dynamically through package restore, it's typically not added to source control.</span></span> <span data-ttu-id="5a381-146">따라서 이 오류는 패키지를 자동으로 복원하지 않는 `msbuild`와 같은 도구를 사용하여 프로젝트를 빌드할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-146">As a result, this error occurs when building a project with a tool such as `msbuild` that does not automatically restore packages.</span></span>

<span data-ttu-id="5a381-147">이 경우 `msbuild -t:restore` 및 `msbuild`를 차례로 실행하거나 `dotnet build`를 사용합니다(그러면 패키지가 자동으로 복원됨).</span><span class="sxs-lookup"><span data-stu-id="5a381-147">In this case, run `msbuild -t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span> <span data-ttu-id="5a381-148">[이전 섹션](#missing)에서는 원하는 패키지 복원 방법을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-148">You can also use any of the package restore methods in the [previous section](#missing).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="5a381-149">하나 이상의 NuGet 패키지를 복원해야 하지만 동의하지 않았기 때문에 그럴 수 없음</span><span class="sxs-lookup"><span data-stu-id="5a381-149">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="5a381-150">전체 오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="5a381-150">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="5a381-151">이 오류는 NuGet 구성에 패키지 복원이 비활성화되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-151">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="5a381-152">앞서 [Visual Studio 사용자를 위한 빠른 해결책](#quick-solution-for-visual-studio-users)에서 설명한 것처럼 Visual Studio의 해당 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-152">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="5a381-153">또한 해당 `nuget.config` 파일에서 이러한 설정을 바로 편집할 수도 있습니다(일반적으로 Windows의 경우 `%AppData%\NuGet\NuGet.Config`, Mac/Linux의 경우 `~/.nuget/NuGet/NuGet.Config`).</span><span class="sxs-lookup"><span data-stu-id="5a381-153">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="5a381-154">`packageRestore` 아래의 `enabled` 및 `automatic` 키가 True로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-154">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

> [!Important]
> <span data-ttu-id="5a381-155">`nuget.config`에서 `packageRestore` 설정을 바로 편집할 경우 Visual Studio를 다시 시작해야 옵션 대화 상자에 최신 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="5a381-156">다른 잠재적 상태</span><span class="sxs-lookup"><span data-stu-id="5a381-156">Other potential conditions</span></span>

- <span data-ttu-id="5a381-157">파일이 없을 경우 NuGet 복원을 사용하려면 해당 파일을 다운로드하라는 메시지와 함께 빌드 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-157">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="5a381-158">하지만 복원을 실행할 때 "모든 패키지가 이미 설치되어 있으며 복원할 항목이 없습니다"라는 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-158">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="5a381-159">이 경우 `packages` 폴더(`packages.config` 사용 시) 또는 `obj/project.assets.json` 파일(PackageReference 사용 시)을 삭제하고 복원을 다시 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="5a381-159">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span> <span data-ttu-id="5a381-160">그래도 오류가 지속되면 명령줄에서 [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md)(전역 패키지 및 캐시 폴더 관리)에 설명된 대로 `nuget locals all -clear` 또는 `dotnet nuget locals all --clear`를 사용하여 *global-packages* 및 캐시 폴더를 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-160">If the error still persists, use `nuget locals all -clear` or `dotnet nuget locals all --clear` from the command line to clear the *global-packages* and cache folders as described on [Managing the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

- <span data-ttu-id="5a381-161">소스 제어에서 프로젝트를 가져올 때 프로젝트 폴더가 읽기 전용으로 설정되어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-161">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="5a381-162">폴더 사용 권한을 변경하고 패키지를 다시 복원해 보세요.</span><span class="sxs-lookup"><span data-stu-id="5a381-162">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="5a381-163">이전 버전의 NuGet를 사용 중일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-163">You may be using an old version of NuGet.</span></span> <span data-ttu-id="5a381-164">[nuget.org/downloads](https://www.nuget.org/downloads)에서 최신 권장 버전을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="5a381-164">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="5a381-165">Visual Studio 2015의 경우 3.6.0을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="5a381-165">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="5a381-166">다른 문제가 발생할 경우 자세한 내용을 확인할 수 있도록 [GitHub에서 문제를 제출](https://github.com/NuGet/docs.microsoft.com-nuget/issues)해 주세요.</span><span class="sxs-lookup"><span data-stu-id="5a381-166">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>
