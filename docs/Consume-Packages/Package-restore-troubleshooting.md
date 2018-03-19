---
title: "Visual Studio에서 NuGet 패키지 복원 문제 해결 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Visual Studio의 일반적인 NuGet 복원 오류 및 해당 오류를 해결하는 방법의 설명입니다."
keywords: "NuGet 패키지 복원, 패키지 복원, 문제 해결, 문제 해결"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8efaed497a596921af3c73ab919831c73bf598e0
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="troubleshooting-package-restore-errors"></a><span data-ttu-id="94bb5-104">패키지 복원 오류 문제 해결</span><span class="sxs-lookup"><span data-stu-id="94bb5-104">Troubleshooting package restore errors</span></span>

<span data-ttu-id="94bb5-105">이 아티클에서는 패키지를 복원할 때 일반적인 오류 및 해당 문제를 해결하는 단계를 집중적으로 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-105">This article focuses on common errors when restoring packages and steps to resolve them.</span></span> <span data-ttu-id="94bb5-106">패키지 복원에 대한 자세한 내용은 [패키지 복원](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="94bb5-106">For complete details on restoring packages, see [Package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="94bb5-107">이 지침으로 문제가 해결되지 않을 경우 귀하의 시나리오를 더 면밀히 살펴볼 수 있도록 [GitHub에서 문제를 제출](https://github.com/NuGet/docs.microsoft.com-nuget/issues)해 주세요.</span><span class="sxs-lookup"><span data-stu-id="94bb5-107">If the instructions here do not work for you, [please file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so that we can examine your scenario more carefully.</span></span> <span data-ttu-id="94bb5-108">이 페이지에 표시되는 "이 페이지가 도움이 되었나요?"</span><span class="sxs-lookup"><span data-stu-id="94bb5-108">Do not use the "Is this page helpful?"</span></span> <span data-ttu-id="94bb5-109">컨트롤은 사용하지 마세요. Microsoft에서 귀하에게 연락하여 자세한 내용을 확인할 수 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-109">control that may appear on this page because it doesn't give us the ability to contact you for more information.</span></span>

## <a name="quick-solution-for-visual-studio-users"></a><span data-ttu-id="94bb5-110">Visual Studio 사용자를 위한 빠른 해결책</span><span class="sxs-lookup"><span data-stu-id="94bb5-110">Quick solution for Visual Studio users</span></span>

<span data-ttu-id="94bb5-111">Visual Studio를 사용하는 경우 먼저 다음과 같이 패키지 복원을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-111">If you're using Visual Studio, first enable package restore as follows.</span></span> <span data-ttu-id="94bb5-112">그러지 않을 경우 다음에 나오는 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-112">Otherwise continue to the sections that follow.</span></span>

1. <span data-ttu-id="94bb5-113">**도구 > NuGet 패키지 관리자 > 패키지 관리자 설정** 메뉴 명령을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-113">Select the **Tools > NuGet Package Manager > Package Manager Settings** menu command.</span></span>
1. <span data-ttu-id="94bb5-114">**패키지 복원**에서 두 옵션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-114">Set both options under **Package Restore**.</span></span>
1. <span data-ttu-id="94bb5-115">**확인**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-115">Select **OK**.</span></span>
1. <span data-ttu-id="94bb5-116">프로젝트를 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-116">Build your project again.</span></span>

![도구/옵션에서 NuGet 패키지 복원 활성화](../consume-packages/media/restore-01-autorestoreoptions.png)

<span data-ttu-id="94bb5-118">이러한 설정은 `NuGet.config` 파일에서도 변경할 수 있습니다. [동의](#consent) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="94bb5-118">These settings can also be changed in your `NuGet.config` file; see the [consent](#consent) section.</span></span>

<a name="missing"></a>

## <a name="this-project-references-nuget-packages-that-are-missing-on-this-computer"></a><span data-ttu-id="94bb5-119">이 프로젝트는 이 컴퓨터에 없는 NuGet 패키지를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-119">This project references NuGet package(s) that are missing on this computer</span></span>

<span data-ttu-id="94bb5-120">전체 오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="94bb5-120">Complete error message:</span></span>

```output
This project references NuGet package(s) that are missing on this computer.
Use NuGet Package Restore to download them. The missing file is {name}.
```

<span data-ttu-id="94bb5-121">이 오류는 하나 이상의 NuGet 패키지에 대한 참조를 포함하는 프로젝트를 빌드하려고 시도할 때 해당 패키지가 프로젝트에 현재 캐시되지 않은 경우에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-121">This error occurs you attempt to build a project that contains references to one or more NuGet packages, but those packages are not presently cached in the project.</span></span> <span data-ttu-id="94bb5-122">(패키지는 프로젝트가 `packages.config`를 사용하는 경우 솔루션 루트의 `packages` 폴더에, 프로젝트가 PackageReference 형식을 사용하는 경우 `obj/project.assets.json` 파일에 캐시됩니다.)</span><span class="sxs-lookup"><span data-stu-id="94bb5-122">(Packages are cached in a `packages` folder at the solution root if the project uses `packages.config`, or in the `obj/project.assets.json` file if the project uses the PackageReference format.)</span></span>

<span data-ttu-id="94bb5-123">이러한 상황은 일반적으로 소스 제어 또는 다른 다운로드에서 프로젝트의 소스 코드를 가져올 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-123">This situation commonly occurs when you obtain the project's source code from source control or another download.</span></span> <span data-ttu-id="94bb5-124">패키지는 nuget.org 같은 패키지 피드에서 복원할 수 있으므로 일반적으로 소스 제어 또는 다운로드에는 패키지가 없습니다([패키지 및 소스 제어](Packages-and-Source-Control.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="94bb5-124">Packages are typically omitted from source control or downloads because they can be restored from package feeds like nuget.org (see [Packages and source control](Packages-and-Source-Control.md)).</span></span> <span data-ttu-id="94bb5-125">그렇지 않고 이를 포함할 경우 리포지토리가 블로트되거나 불필요하게 큰 .zip 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-125">Including them would otherwise bloat the repository or create unnecessarily large .zip files.</span></span>

<span data-ttu-id="94bb5-126">패키지를 복원하려면 다음 방법 중 하나를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="94bb5-126">Use one of the following methods to restore the packages:</span></span>

- <span data-ttu-id="94bb5-127">Visual Studio에서 **도구 > NuGet 패키지 관리자 > 패키지 관리자 설정** 메뉴 명령을 선택하고 **패키지 복원**에서 두 옵션을 설정하고 **확인**을 선택하여 패키지 복원을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-127">In Visual Studio, enable package restore by selecting the **Tools > NuGet Package Manager > Package Manager Settings** menu command, setting both options under **Package Restore**, and selecting **OK**.</span></span> <span data-ttu-id="94bb5-128">그런 다음, 솔루션을 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-128">Then build the solution again.</span></span>
- <span data-ttu-id="94bb5-129">.NET Core 프로젝트의 경우 `dotnet restore` 또는 `dotnet build`를 실행합니다(복원이 자동으로 실행됨).</span><span class="sxs-lookup"><span data-stu-id="94bb5-129">For .NET Core projects, run `dotnet restore` or `dotnet build` (which automatically runs restore).</span></span>
- <span data-ttu-id="94bb5-130">명령줄에서 `nuget restore`를 실행합니다(단, `dotnet`을 사용하여 만든 프로젝트의 경우에는 `dotnet restore` 사용).</span><span class="sxs-lookup"><span data-stu-id="94bb5-130">On the command line, run `nuget restore` (except for projects created with `dotnet`, in which case use `dotnet restore`).</span></span>
- <span data-ttu-id="94bb5-131">PackageReference 형식을 사용하는 프로젝트의 경우 명령줄에서 `msbuild /t:restore`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-131">On the command line with projects using the PackageReference format, run `msbuild /t:restore`.</span></span>

<span data-ttu-id="94bb5-132">복원에 성공하면 `packages` 폴더(`packages.config` 사용 시) 또는 `obj/project.assets.json` 파일(PackageReference 사용 시)이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-132">After a successful restore, you should see either a `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference).</span></span> <span data-ttu-id="94bb5-133">이제 프로젝트가 성공적으로 빌드됩니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-133">The project should now build successfully.</span></span> <span data-ttu-id="94bb5-134">그렇지 않을 경우 후속 조치를 위해 [GitHub에서 문제를 제출](https://github.com/NuGet/docs.microsoft.com-nuget/issues)해 주세요.</span><span class="sxs-lookup"><span data-stu-id="94bb5-134">If not, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can follow up with you.</span></span>

<a name="assets"></a>

## <a name="assets-file-projectassetsjson-not-found"></a><span data-ttu-id="94bb5-135">자산 파일 project.assets.json을 찾을 수 없음</span><span class="sxs-lookup"><span data-stu-id="94bb5-135">Assets file project.assets.json not found</span></span>

<span data-ttu-id="94bb5-136">전체 오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="94bb5-136">Complete error message:</span></span>

```output
Assets file '<path>\project.assets.json' not found. Run a NuGet package restore to generate this file.
```

<span data-ttu-id="94bb5-137">이 오류는 [이전 섹션](#missing)에 설명된 것과 같은 이유로 발생하며 해결책도 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-137">This error occurs for the same reasons as explained in the [previous section](#missing), and has the same remedies.</span></span> <span data-ttu-id="94bb5-138">예를 들어 소스 제어에서 가져온 .NET Core 프로젝트에 대해 `msbuild`를 실행하면 패키지가 자동으로 복원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-138">For example, running `msbuild` on a .NET Core project that's been obtained from source control won't automatically restore packages.</span></span> <span data-ttu-id="94bb5-139">이 경우 `msbuild /t:restore` 및 `msbuild`를 차례로 실행하거나 `dotnet build`를 사용합니다(그러면 패키지가 자동으로 복원됨).</span><span class="sxs-lookup"><span data-stu-id="94bb5-139">In this case, run `msbuild /t:restore` followed by `msbuild`, or use `dotnet build` (which restores packages automatically).</span></span>

<a name="consent"></a>

## <a name="one-or-more-nuget-packages-need-to-be-restored-but-couldnt-be-because-consent-has-not-been-granted"></a><span data-ttu-id="94bb5-140">하나 이상의 NuGet 패키지를 복원해야 하지만 동의하지 않았기 때문에 그럴 수 없음</span><span class="sxs-lookup"><span data-stu-id="94bb5-140">One or more NuGet packages need to be restored but couldn't be because consent has not been granted</span></span>

<span data-ttu-id="94bb5-141">전체 오류 메시지:</span><span class="sxs-lookup"><span data-stu-id="94bb5-141">Complete error message:</span></span>

```output
One or more NuGet packages need to be restored but couldn't be because consent has
not been granted. To give consent, open the Visual Studio Options dialog, click on
the NuGet Package Manager node and check 'Allow NuGet to download missing packages
during build.' You can also give consent by setting the environment variable
'EnableNuGetPackageRestore' to 'true'. Missing packages: {name}
```

<span data-ttu-id="94bb5-142">이 오류는 NuGet 구성에 패키지 복원이 비활성화되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-142">This error indicates that package restore is disabled in your NuGet configuration.</span></span>

<span data-ttu-id="94bb5-143">앞서 [Visual Studio 사용자를 위한 빠른 해결책](#quick-solution-for-visual-studio-users)에서 설명한 것처럼 Visual Studio의 해당 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-143">You can change the applicable settings in Visual Studio as described earlier under [Quick solution for Visual Studio users](#quick-solution-for-visual-studio-users).</span></span>

<span data-ttu-id="94bb5-144">또한 해당 `nuget.config` 파일에서 이러한 설정을 바로 편집할 수도 있습니다(일반적으로 Windows의 경우 `%AppData%\NuGet\NuGet.Config`, Mac/Linux의 경우 `~/.nuget/NuGet/NuGet.Config`).</span><span class="sxs-lookup"><span data-stu-id="94bb5-144">You can also edit these settings directly in the applicable `nuget.config` file (typically `%AppData%\NuGet\NuGet.Config` on Windows and `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="94bb5-145">`packageRestore` 아래의 `enabled` 및 `automatic` 키가 True로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-145">Make sure the `enabled` and `automatic` keys under `packageRestore` are set to True:</span></span>

```xml
<!-- Package restore is enabled -->
<configuration>
    <packageRestore>
        <add key="enabled" value="True" />
        <add key="automatic" value="True" />
    </packageRestore>
</configuration>
```

<span data-ttu-id="94bb5-146">`nuget.config`에서 `packageRestore` 설정을 바로 편집할 경우 Visual Studio를 다시 시작해야 옵션 대화 상자에 최신 값이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-146">Note that if you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio so that the options dialog box shows the current values.</span></span>

## <a name="other-potential-conditions"></a><span data-ttu-id="94bb5-147">다른 잠재적 상태</span><span class="sxs-lookup"><span data-stu-id="94bb5-147">Other potential conditions</span></span>

- <span data-ttu-id="94bb5-148">파일이 없을 경우 NuGet 복원을 사용하려면 해당 파일을 다운로드하라는 메시지와 함께 빌드 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-148">You may encounter build errors due to missing files, with a message saying to use NuGet restore to download them.</span></span> <span data-ttu-id="94bb5-149">하지만 복원을 실행할 때 "모든 패키지가 이미 설치되어 있으며 복원할 항목이 없습니다"라는 메시지가 나타날 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-149">However, running a restore might say, "All packages are already installed and there is nothing to restore."</span></span> <span data-ttu-id="94bb5-150">이 경우 `packages` 폴더(`packages.config` 사용 시) 또는 `obj/project.assets.json` 파일(PackageReference 사용 시)을 삭제하고 복원을 다시 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="94bb5-150">In this case, delete the `packages` folder (when using `packages.config`) or the `obj/project.assets.json` file (when using PackageReference) and run restore again.</span></span>

- <span data-ttu-id="94bb5-151">소스 제어에서 프로젝트를 가져올 때 프로젝트 폴더가 읽기 전용으로 설정되어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-151">When obtaining a project from source control, your project folders may be set to read-only.</span></span> <span data-ttu-id="94bb5-152">폴더 사용 권한을 변경하고 패키지를 다시 복원해 보세요.</span><span class="sxs-lookup"><span data-stu-id="94bb5-152">Change the folder permissions and try restoring packages again.</span></span>

- <span data-ttu-id="94bb5-153">이전 버전의 NuGet를 사용 중일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-153">You may be using an old version of NuGet.</span></span> <span data-ttu-id="94bb5-154">[nuget.org/downloads](https://www.nuget.org/downloads)에서 최신 권장 버전을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="94bb5-154">Check [nuget.org/downloads](https://www.nuget.org/downloads) for the latest recommended versions.</span></span> <span data-ttu-id="94bb5-155">Visual Studio 2015의 경우 3.6.0을 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="94bb5-155">For Visual Studio 2015, we recommend 3.6.0.</span></span>

<span data-ttu-id="94bb5-156">다른 문제가 발생할 경우 자세한 내용을 확인할 수 있도록 [GitHub에서 문제를 제출](https://github.com/NuGet/docs.microsoft.com-nuget/issues)해 주세요.</span><span class="sxs-lookup"><span data-stu-id="94bb5-156">If you encounter other problems, [file an issue on GitHub](https://github.com/NuGet/docs.microsoft.com-nuget/issues) so we can get more details from you.</span></span>