---
title: NuGet 패키지 다시 설치 및 업데이트 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Visual Studio에서 손상된 패키지 참조와 같이 패키지를 다시 설치하고 업데이트해야 하는 경우에 대해 자세히 설명합니다.
keywords: NuGet 패키지 설치, NuGet 패키지 다시 설치, NuGet 패키지 복원, 패키지 업데이트, 패키지 복원, 손상된 참조 수정
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9da385f51abf5877589c29ebdeffefc9a1a20a2e
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="how-to-reinstall-and-update-packages"></a><span data-ttu-id="ba454-104">패키지를 다시 설치하고 업데이트하는 방법</span><span class="sxs-lookup"><span data-stu-id="ba454-104">How to reinstall and update packages</span></span>

<span data-ttu-id="ba454-105">아래에서 설명하는 [패키지를 다시 설치하는 경우](#when-to-reinstall-a-package)에는 패키지에 대한 참조가 Visual Studio 프로젝트에서 손상될 수 있는 여러 가지 상황이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-105">There are a number of situations, described below under [When to Reinstall a Package](#when-to-reinstall-a-package), where references to a package might get broken within a Visual Studio project.</span></span> <span data-ttu-id="ba454-106">이러한 경우 동일한 버전의 패키지를 제거한 다음 다시 설치하면 해당 참조가 작업 순서에 맞게 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-106">In these cases, uninstalling and then reinstalling the same version of the package will restore those references to working order.</span></span> <span data-ttu-id="ba454-107">패키지 업데이트는 업데이트된 버전을 설치하는 것이며, 이 경우 패키지를 작업 순서에 맞게 복원하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-107">Updating a package simply means installing an updated version, which often restores a package to working order.</span></span>

<span data-ttu-id="ba454-108">패키지 업데이트 및 다시 설치는 다음과 같이 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-108">Updating and reinstalling packages is accomplished as follows:</span></span>

| <span data-ttu-id="ba454-109">메서드</span><span class="sxs-lookup"><span data-stu-id="ba454-109">Method</span></span> | <span data-ttu-id="ba454-110">업데이트</span><span class="sxs-lookup"><span data-stu-id="ba454-110">Update</span></span> | <span data-ttu-id="ba454-111">다시 설치</span><span class="sxs-lookup"><span data-stu-id="ba454-111">Reinstall</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba454-112">패키지 관리자 콘솔([Update-Package 사용](#using-update-package)에서 설명)</span><span class="sxs-lookup"><span data-stu-id="ba454-112">Package Manager console (described in [Using Update-Package](#using-update-package))</span></span> | <span data-ttu-id="ba454-113">`Update-Package` 명령</span><span class="sxs-lookup"><span data-stu-id="ba454-113">`Update-Package` command</span></span> | <span data-ttu-id="ba454-114">`Update-Package -reinstall` 명령</span><span class="sxs-lookup"><span data-stu-id="ba454-114">`Update-Package -reinstall` command</span></span> |
| <span data-ttu-id="ba454-115">패키지 관리자 UI</span><span class="sxs-lookup"><span data-stu-id="ba454-115">Package Manager UI</span></span> | <span data-ttu-id="ba454-116">**업데이트** 탭에서 패키지를 하나 이상 선택하고 **업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-116">On the **Updates** tab, select one or more packages and select **Update**</span></span> | <span data-ttu-id="ba454-117">**설치됨** 탭에서 패키지를 선택하고, 이름을 기록한 다음, **제거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-117">On the **Installed** tab, select a package, record its name, then select **Uninstall**.</span></span> <span data-ttu-id="ba454-118">**찾아보기** 탭으로 전환하고, 패키지 이름을 검색하여 선택한 다음, **설치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-118">Switch to the **Browse** tab, search for the package name, select it, then select **Install**).</span></span> |
| <span data-ttu-id="ba454-119">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="ba454-119">nuget.exe CLI</span></span> | <span data-ttu-id="ba454-120">`nuget update` 명령</span><span class="sxs-lookup"><span data-stu-id="ba454-120">`nuget update` command</span></span> | <span data-ttu-id="ba454-121">모든 패키지의 경우 패키지 폴더를 삭제한 다음 `nuget install`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-121">For all packages, delete the package folder, then run `nuget install`.</span></span> <span data-ttu-id="ba454-122">단일 패키지의 경우 패키지 폴더를 삭제하고 `nuget install <id>`를 사용하여 동일한 패키지를 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-122">For a single package, delete the package folder and use `nuget install <id>` to reinstall the same one.</span></span> |

<span data-ttu-id="ba454-123">이 문서의 내용</span><span class="sxs-lookup"><span data-stu-id="ba454-123">In this article:</span></span>

- [<span data-ttu-id="ba454-124">패키지를 다시 설치하는 경우</span><span class="sxs-lookup"><span data-stu-id="ba454-124">When to Reinstall a Package</span></span>](#when-to-reinstall-a-package)
- [<span data-ttu-id="ba454-125">업그레이드 버전 제한</span><span class="sxs-lookup"><span data-stu-id="ba454-125">Constraining upgrade versions</span></span>](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a><span data-ttu-id="ba454-126">패키지를 다시 설치하는 경우</span><span class="sxs-lookup"><span data-stu-id="ba454-126">When to Reinstall a Package</span></span>

1. <span data-ttu-id="ba454-127">**패키지 복원 후 손상된 참조**: 프로젝트를 열고 NuGet 패키지를 복원했지만 손상된 참조가 계속 표시되는 경우 해당 패키지 각각을 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-127">**Broken references after package restore**: If you've opened a project and restored NuGet packages, but still see broken references, try reinstalling each of those packages.</span></span>
1. <span data-ttu-id="ba454-128">**삭제된 파일로 인해 중단된 프로젝트**: NuGet은 패키지에서 추가된 항목을 제거할 수 있도록 하므로 실수로 패키지에서 설치된 내용을 수정하고 프로젝트를 중단할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-128">**Project is broken due to deleted files**: NuGet does not prevent you from removing items added from packages, so it's easy to inadvertently modify contents installed from a package and break your project.</span></span> <span data-ttu-id="ba454-129">프로젝트를 복원하려면 영향을 받은 패키지를 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-129">To restore the project, reinstall the affected packages.</span></span>
1. <span data-ttu-id="ba454-130">**패키지 업데이트로 인해 중단된 프로젝트**: 패키지 업데이트로 인해 프로젝트가 중단되는 경우 일반적으로 업데이트되었을 수도 있는 종속성 패키지로 인해 실패가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-130">**Package update broke the project**: If an update to a package breaks a project, the failure is generally caused by a dependency package which may have also been updated.</span></span> <span data-ttu-id="ba454-131">종속성 상태를 복원하려면 특정 패키지를 다시 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-131">To restore the state of the dependency, reinstall that specific package.</span></span>
1. <span data-ttu-id="ba454-132">**프로젝트 대상 변경 또는 업그레이드**: 프로젝트 대상이 변경되거나 프로젝트가 업그레이드된 경우 및 대상 프레임워크의 변경으로 인해 패키지를 다시 설치해야 하는 경우에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-132">**Project retargeting or upgrade**: This can be useful when a project has been retargeted or upgraded and if the package requires reinstallation due to the change in target framework.</span></span> <span data-ttu-id="ba454-133">NuGet에서는 프로젝트 대상을 변경하는 직후 빌드 오류가 표시되며, 뒤이은 빌드 경고에서 패키지를 다시 설치해야 할 수 있음을 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-133">NuGet shows a build error in such cases immediately after project retargeting, and subsequent build warnings let you know that the package may need to be reinstalled.</span></span> <span data-ttu-id="ba454-134">프로젝트를 업그레이드하는 경우 NuGet은 프로젝트 업그레이드 로그에 오류를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-134">For project upgrade, NuGet shows an error in the Project Upgrade Log.</span></span>
1. <span data-ttu-id="ba454-135">**개발 중에 패키지 다시 설치**: 패키지 작성자는 동작을 테스트하기 위해 개발 중인 패키지와 동일한 버전을 다시 설치해야 하는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-135">**Reinstalling a package during its development**: Package authors often need to reinstall the same version of package they're developing to test the behavior.</span></span> <span data-ttu-id="ba454-136">`Install-Package` 명령은 강제로 다시 설치하는 옵션을 제공하지 않으므로 `Update-Package -reinstall`을 대신 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-136">The `Install-Package` command does not provide an option to force a reinstall, so use `Update-Package -reinstall` instead.</span></span>

## <a name="constraining-upgrade-versions"></a><span data-ttu-id="ba454-137">업그레이드 버전 제한</span><span class="sxs-lookup"><span data-stu-id="ba454-137">Constraining upgrade versions</span></span>

<span data-ttu-id="ba454-138">기본적으로 패키지를 다시 설치하거나 업데이트하는 경우 *항상* 패키지 원본에서 사용 가능한 최신 버전이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-138">By default, reinstalling or updating a package *always* installs the latest version available from the package source.</span></span>

<span data-ttu-id="ba454-139">그러나 `packages.config` 관리 형식을 사용하는 프로젝트에서는 버전 범위를 구체적으로 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-139">In projects using the `packages.config` management format, however, you can specifically constrain the version range.</span></span> <span data-ttu-id="ba454-140">예를 들어 패키지 API의 주요 변경으로 인해 응용 프로그램이 패키지 버전 1.x에서만 작동하고 2.0 이상에서는 작동하지 않는 것으로 알고 있는 경우 업그레이드를 1.x 버전으로 제한하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-140">For example, if you know that your application works only with version 1.x of a package but not 2.0 and above, perhaps due to a major change in the package API, then you'd want to constrain upgrades to 1.x versions.</span></span> <span data-ttu-id="ba454-141">이렇게 하면 우발적인 업데이트로 인해 응용 프로그램이 중단되는 것을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-141">This prevents accidental updates that would break the application.</span></span>

<span data-ttu-id="ba454-142">제한 조건을 설정하려면 텍스트 편집기에서 `packages.config`를 열고, 문제의 종속성을 찾고, 버전 범위가 있는 `allowedVersions` 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-142">To set a constraint, open `packages.config` in a text editor, locate the dependency in question, and add the `allowedVersions` attribute with a version range.</span></span> <span data-ttu-id="ba454-143">예를 들어 업데이트를 1.x 버전으로 제한하려면 `allowedVersions`를 `[1,2)`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-143">For example, to constrain updates to version 1.x, set `allowedVersions` to `[1,2)`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

<span data-ttu-id="ba454-144">모든 경우에 [패키지 버전 관리](../reference/package-versioning.md#version-ranges-and-wildcards)에서 설명한 표기법을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="ba454-144">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-update-package"></a><span data-ttu-id="ba454-145">Update-Package 사용</span><span class="sxs-lookup"><span data-stu-id="ba454-145">Using Update-Package</span></span>

<span data-ttu-id="ba454-146">아래에 설명된 [고려 사항](#considerations)에 유념하여 Visual Studio 패키지 관리자 콘솔(**도구** > **NuGet 패키지 관리자** > **패키지 관리자 콘솔**)에서 [Update-Package 명령](../Tools/ps-ref-update-package.md)을 통해 모든 패키지를 쉽게 다시 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-146">Being mindful of the [Considerations](#considerations) described below, you can easily reinstall any package using the [Update-Package command](../Tools/ps-ref-update-package.md) in the Visual Studio Package Manager Console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

```ps
Update-Package -Id <package_name> –reinstall
```

<span data-ttu-id="ba454-147">이 명령을 사용하면 패키지를 제거한 다음 NuGet 갤러리에서 동일한 버전의 동일한 패키지를 찾으려고 하는 것보다 훨씬 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-147">Using this command is much easier than removing a package and then trying to locate the same package in the NuGet gallery with the same version.</span></span> <span data-ttu-id="ba454-148">`-Id` 스위치는 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-148">Note that the `-Id` switch is optional.</span></span>

<span data-ttu-id="ba454-149">해당되는 경우 `-reinstall`이 없는 동일한 명령으로 패키지를 최신 버전으로 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-149">The same command without `-reinstall` updates a package to a newer version, if applicable.</span></span> <span data-ttu-id="ba454-150">문제의 패키지가 프로젝트에 아직 설치되지 않은 경우 이 명령에서는 오류가 발생합니다. 즉 `Update-Package`에서 패키지를 직접 설치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-150">The command gives an error if the package in question is not already installed in a project; that is, `Update-Package` does not install packages directly.</span></span>

```ps
Update-Package <package_name>
```

<span data-ttu-id="ba454-151">기본적으로 `Update-Package`는 솔루션의 모든 패키지에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-151">By default, `Update-Package` affects all packages in a solution.</span></span> <span data-ttu-id="ba454-152">작업을 특정 프로젝트로 제한하려면 [솔루션 탐색기]에 표시된 대로 프로젝트 이름을 사용하는 `-ProjectName` 스위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-152">To limit the action to a specific project, use the `-ProjectName` switch, using the name of the project as it appears in Solution Explorer:</span></span>

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

<span data-ttu-id="ba454-153">프로젝트의 모든 패키지를 *업데이트*(또는 `-reinstall`을 사용하여 다시 설치)하려면 특정 패키지를 지정하지 않은 `-ProjectName`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-153">To *update* all packages in a project (or reinstall using `-reinstall`), use `-ProjectName` without specifying any particular package:</span></span>

```ps
Update-Package -ProjectName MyProject
```

<span data-ttu-id="ba454-154">솔루션의 모든 패키지를 업데이트하려면 다른 인수 또는 스위치 없이 `Update-Package`만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-154">To update all packages in a solution, just use `Update-Package` by itself with no other arguments or switches.</span></span> <span data-ttu-id="ba454-155">모든 업데이트를 수행하는 데 상당한 시간이 걸릴 수 있으므로 이 형식은 신중하게 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-155">Use this form carefully, because it can take considerable time to perform all the updates:</span></span>

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

<span data-ttu-id="ba454-156">[PackageReference](../Consume-Packages/Package-References-in-Project-Files.md)를 사용하여 프로젝트 또는 솔루션에서 패키지를 업데이트하면 항상 최신 버전의 패키지(시험판 패키지 제외)로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-156">Updating packages in a project or solution using [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md) always updates to the latest version of the package (excluding pre-release packages).</span></span> <span data-ttu-id="ba454-157">원하는 경우 [업그레이드 버전 제한](#constraining-upgrade-versions)에서 설명한 대로 `packages.config`를 사용하는 프로젝트에서 업데이트 버전을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-157">Projects that use `packages.config` can, if desired, limit update versions as described below in [Constraining upgrade versions](#constraining-upgrade-versions).</span></span>

<span data-ttu-id="ba454-158">명령에 대한 자세한 내용은 [Update-Package](../Tools/ps-ref-update-package.md) 참조를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ba454-158">For full details on the command, see the [Update-Package](../Tools/ps-ref-update-package.md) reference.</span></span>

### <a name="considerations"></a><span data-ttu-id="ba454-159">고려 사항</span><span class="sxs-lookup"><span data-stu-id="ba454-159">Considerations</span></span>

<span data-ttu-id="ba454-160">패키지를 다시 설치할 때 다음과 같은 영향을 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-160">The following may be affected when reinstalling a package:</span></span>

1. <span data-ttu-id="ba454-161">**프로젝트 대상 프레임워크의 대상 변경에 따라 패키지 다시 설치**</span><span class="sxs-lookup"><span data-stu-id="ba454-161">**Reinstalling packages according to project target framework retargeting**</span></span>
    - <span data-ttu-id="ba454-162">간단한 경우에만 `Update-Package –reinstall <package_name>`을 사용하여 패키지를 다시 설치하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-162">In a simple case, just reinstalling a package using `Update-Package –reinstall <package_name>` works.</span></span> <span data-ttu-id="ba454-163">이전 대상 프레임워크에 대해 설치된 패키지가 제거되고, 프로젝트의 현재 대상 프레임워크에 대해 동일한 패키지가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-163">A package that is installed against an old target framework gets uninstalled and the same package gets installed against the current target framework of the project.</span></span>
    - <span data-ttu-id="ba454-164">경우에 따라 새 대상 프레임워크를 지원하지 않는 패키지가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-164">In some cases, there may be a package that does not support the new target framework.</span></span>
        - <span data-ttu-id="ba454-165">패키지에서 PCL(이식 가능한 클래스 라이브러리)을 지원하고 프로젝트 대상이 해당 패키지에서 더 이상 지원하지 않는 플랫폼의 조합으로 변경된 경우 다시 설치하면 패키지에 대한 참조가 누락됩니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-165">If a package supports portable class libraries (PCLs) and the project is retargeted to a combination of platforms no longer supported by the package, references to the package will be missing after reinstalling.</span></span>
        - <span data-ttu-id="ba454-166">이는 직접 사용하는 패키지 또는 종속성으로 설치된 패키지에 대해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-166">This can surface for packages you're using directly or for packages installed as dependencies.</span></span> <span data-ttu-id="ba454-167">해당 종속성이 없는 경우에도 직접 사용하는 패키지에서 새 대상 프레임워크를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-167">It's possible for the package you're using directly to support the new target framework while its dependency does not.</span></span>
        - <span data-ttu-id="ba454-168">응용 프로그램을 대상으로 변경한 후 패키지를 다시 설치할 때 빌드 또는 런타임 오류가 발생하는 경우 대상 프레임워크를 되돌리거나 새 대상 프레임워크를 제대로 지원하는 대체 패키지를 검색해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-168">If reinstalling packages after retargeting your application results in build or runtime errors, you may need to revert your target framework or search for alternative packages that properly support your new target framework.</span></span>

1. <span data-ttu-id="ba454-169">**프로젝트 대상 변경 또는 프로젝트 업그레이드 후 requireReinstallation 특성이 packages.config에 추가됨**</span><span class="sxs-lookup"><span data-stu-id="ba454-169">**requireReinstallation attribute added in packages.config after project retargeting or upgrade**</span></span>
    - <span data-ttu-id="ba454-170">NuGet은 프로젝트 대상을 변경하거나 프로젝트를 업그레이드함으로써 패키지에서 영향을 받았다고 감지하면 `packages.config`의 `requireReinstallation="true"` 특성을 영향을 받은 모든 패키지 참조에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-170">If NuGet detects that packages were affected by retargeting or upgrading a project, it adds a `requireReinstallation="true"` attribute in  `packages.config` to all affected package references.</span></span> <span data-ttu-id="ba454-171">이로 인해 Visual Studio의 각 후속 빌드에서 다시 설치해야 한다는 것을 기억할 수 있도록 해당 패키지에 대한 빌드 경고를 발생시킵니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-171">Because of this, each subsequent build in Visual Studio raises build warnings for those packages so you can remember to reinstall them.</span></span>

1. <span data-ttu-id="ba454-172">**종속성이 있는 패키지 다시 설치**</span><span class="sxs-lookup"><span data-stu-id="ba454-172">**Reinstalling packages with dependencies**</span></span>
    - <span data-ttu-id="ba454-173">`Update-Package –reinstall`은 동일한 버전의 원래 패키지를 다시 설치하지만, 특정 버전 제한 조건이 제공되지 않는 한 최신 버전의 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-173">`Update-Package –reinstall` reinstalls the same version of the original package, but installs the latest version of dependencies unless specific version constraints are provided.</span></span> <span data-ttu-id="ba454-174">이렇게 하면 문제를 해결하는 데 필요한 종속성만 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-174">This allows you to update only the dependencies as required to fix an issue.</span></span> <span data-ttu-id="ba454-175">그러나 종속성을 이전 버전으로 롤백하는 경우 종속 패키지에 영향을 주지 않고 `Update-Package <dependency_name>`을 사용하여 해당 종속성을 다시 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-175">However, if this rolls a dependency back to an earlier version, you can use `Update-Package <dependency_name>` to reinstall that one dependency without affecting the dependent package.</span></span>
    - <span data-ttu-id="ba454-176">`Update-Package –reinstall <packageName> -ignoreDependencies`는 동일한 버전의 원래 패키지를 다시 설치하지만, 종속성은 다시 설치하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-176">`Update-Package –reinstall <packageName> -ignoreDependencies` reinstalls the same version of the original package but does not reinstall dependencies.</span></span> <span data-ttu-id="ba454-177">패키지 종속성을 업데이트하면 상태가 손상될 수 있는 경우에 이 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-177">Use this when updating package dependencies might result in a broken state</span></span>

1. <span data-ttu-id="ba454-178">**종속 버전이 포함된 경우 패키지 다시 설치**</span><span class="sxs-lookup"><span data-stu-id="ba454-178">**Reinstalling packages when dependent versions are involved**</span></span>
    - <span data-ttu-id="ba454-179">위에서 설명한 대로 패키지를 다시 설치해도 설치된 다른 패키지의 버전은 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-179">As explained above, reinstalling a package does not change versions of any other installed packages that depend on it.</span></span> <span data-ttu-id="ba454-180">따라서 종속성을 다시 설치하면 종속성 패키지가 손상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ba454-180">It's possible, then, that reinstalling a dependency could break the dependent package.</span></span>
