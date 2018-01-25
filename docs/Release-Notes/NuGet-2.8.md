---
title: "NuGet 2.8 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 2.8에 대 한 릴리스 정보입니다."
keywords: "NuGet 2.8 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 39b885adc9e23eb815f65639875c4a4c27d61a4c
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-28-release-notes"></a><span data-ttu-id="99c37-104">NuGet 2.8 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="99c37-104">NuGet 2.8 Release Notes</span></span>

<span data-ttu-id="99c37-105">[NuGet 2.7.2 릴리스 정보](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 릴리스 정보](../release-notes/nuget-2.8.1.md)</span><span class="sxs-lookup"><span data-stu-id="99c37-105">[NuGet 2.7.2 Release Notes](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md)</span></span>

<span data-ttu-id="99c37-106">NuGet 2.8 2014 년 1 월 29 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-106">NuGet 2.8 was released on January 29, 2014.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="99c37-107">감사의 글</span><span class="sxs-lookup"><span data-stu-id="99c37-107">Acknowledgements</span></span>

1. <span data-ttu-id="99c37-108">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span><span class="sxs-lookup"><span data-stu-id="99c37-108">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span></span>
    - <span data-ttu-id="99c37-109">[#3466](https://nuget.codeplex.com/workitem/3466) -압축 된 패키지, 종속성 패키지의 Id를 확인 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="99c37-109">[#3466](https://nuget.codeplex.com/workitem/3466) - When packing packages, verifying Id of dependency packages.</span></span>
1. <span data-ttu-id="99c37-110">[Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span><span class="sxs-lookup"><span data-stu-id="99c37-110">[Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span></span>
    - <span data-ttu-id="99c37-111">[#2379](https://nuget.codeplex.com/workitem/2379) -persistening 피드 자격 증명 때 $metadata 접미사를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-111">[#2379](https://nuget.codeplex.com/workitem/2379) - Remove the $metadata suffix when persistening feed credentials.</span></span>
1. <span data-ttu-id="99c37-112">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span><span class="sxs-lookup"><span data-stu-id="99c37-112">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span></span>
    - <span data-ttu-id="99c37-113">[#3538](http://nuget.codeplex.com/workitem/3538) -nuget.exe 업데이트 명령에 대 한 프로젝트 파일을 지정 하는 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-113">[#3538](http://nuget.codeplex.com/workitem/3538) - Support specifying project file for the nuget.exe update command.</span></span>
1. [<span data-ttu-id="99c37-114">Juan Gonzalez</span><span class="sxs-lookup"><span data-stu-id="99c37-114">Juan Gonzalez</span></span>](https://www.codeplex.com/site/users/view/jjgonzalez)
    - <span data-ttu-id="99c37-115">[#3536](http://nuget.codeplex.com/workitem/3536) --IncludeReferencedProjects 함께 전달 되지 않은 교체 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-115">[#3536](http://nuget.codeplex.com/workitem/3536) - Replacement tokens not passed with -IncludeReferencedProjects.</span></span>
1. <span data-ttu-id="99c37-116">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span><span class="sxs-lookup"><span data-stu-id="99c37-116">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span></span>
    - <span data-ttu-id="99c37-117">[#3677](http://nuget.codeplex.com/workitem/3677) -해결 nuget.push 큰 패키지를 적용할 때 발생 한 OutOfMemoryException를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-117">[#3677](http://nuget.codeplex.com/workitem/3677) - Fix nuget.push throwing OutOfMemoryException when pushing large package.</span></span>
1. [<span data-ttu-id="99c37-118">Wouter Ouwens</span><span class="sxs-lookup"><span data-stu-id="99c37-118">Wouter Ouwens</span></span>](https://www.codeplex.com/site/users/view/Despotes)
    - <span data-ttu-id="99c37-119">[#3666](http://nuget.codeplex.com/workitem/3666) -다른 CLI/c + + 프로젝트를 참조 하는 프로젝트에 잘못 된 대상 경로 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-119">[#3666](http://nuget.codeplex.com/workitem/3666) - Fix incorrect target path when project references another CLI/C++ project.</span></span>
1. <span data-ttu-id="99c37-120">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="99c37-120">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="99c37-121">[#3639](https://nuget.codeplex.com/workitem/3639) -패키지 개발 종속성 기본적으로 설치 되도록 허용</span><span class="sxs-lookup"><span data-stu-id="99c37-121">[#3639](https://nuget.codeplex.com/workitem/3639) - Allow packages to be installed as development dependencies by default</span></span>
1. <span data-ttu-id="99c37-122">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="99c37-122">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="99c37-123">[#3717](https://nuget.codeplex.com/workitem/3717) -최신 패치 버전에 대 한 암시적 업그레이드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-123">[#3717](https://nuget.codeplex.com/workitem/3717) - Remove implicit upgrades to the latest patch version</span></span>
1. [<span data-ttu-id="99c37-124">Gregory Vandenbrouck</span><span class="sxs-lookup"><span data-stu-id="99c37-124">Gregory Vandenbrouck</span></span>](https://www.codeplex.com/site/users/view/vdbg)
    - <span data-ttu-id="99c37-125">여러 버그 수정 및 NuGet.Server, nuget.exe 미러 명령 등에 대 한 향상 된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-125">Several bug fixes and improvements for NuGet.Server, the nuget.exe mirror command, and others.</span></span>
    - <span data-ttu-id="99c37-126">2.8 마스터에 통합 하는 오른쪽 타이밍에 협력해 Gregory와 몇 개월 동안 수행 된이 작업의이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-126">This work was done over several months, with Gregory working with us on the right timing to integrate into master for 2.8.</span></span>

## <a name="patch-resolution-for-dependencies"></a><span data-ttu-id="99c37-127">종속성에 대 한 패치 확인</span><span class="sxs-lookup"><span data-stu-id="99c37-127">Patch Resolution for Dependencies</span></span>

<span data-ttu-id="99c37-128">패키지 종속성을 확인할 때에 지금까지 NuGet 패키지의 종속성을 만족 하는 가장 낮은 주 및 부 패키지 버전을 선택 하는 전략을 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-128">When resolving package dependencies, NuGet has historically implemented a strategy of selecting the lowest major and minor package version which satisfies the dependencies on the package.</span></span> <span data-ttu-id="99c37-129">그러나 주 및 부 버전을 달리 패치 버전 항상 해결 된 가장 높은 버전으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-129">Unlike the major and minor version, however, the patch version was always resolved to the highest version.</span></span> <span data-ttu-id="99c37-130">또한 악의적 동작 이지만 패키지 종속성이 설치를 위한 결정성이 부족 한 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-130">Though the behavior was well-intentioned, it created a lack of determinism for installing packages with dependencies.</span></span> <span data-ttu-id="99c37-131">다음 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="99c37-131">Consider the following example:</span></span>

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

<span data-ttu-id="99c37-132">이 예제에서는 경우에 Developer1 및 Developer2 설치 PackageA@1.0.0각 결국 PackageB의 다른 버전으로, 합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-132">In this example, even though Developer1 and Developer2 installed PackageA@1.0.0, each ended up with a different version of PackageB.</span></span> <span data-ttu-id="99c37-133">NuGet 2.8 패치 버전에 대 한 종속성 확인 하는 동작은 주 버전과 부 버전에 대 한 동작과 일치 되도록이 기본 동작을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-133">NuGet 2.8 changes this default behavior such that the dependency resolution behavior for patch versions is consistent with the behavior for major and minor versions.</span></span> <span data-ttu-id="99c37-134">그런 다음 위의 예에 PackageB@1.0.0 설치 설치할 PackageA@1.0.0최신 패치 버전에 관계 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-134">In the above example, then, PackageB@1.0.0 would be installed as a result of installing PackageA@1.0.0, regardless of the newer patch version.</span></span>

## <a name="-dependencyversion-switch"></a><span data-ttu-id="99c37-135">-DependencyVersion 스위치</span><span class="sxs-lookup"><span data-stu-id="99c37-135">-DependencyVersion Switch</span></span>

<span data-ttu-id="99c37-136">NuGet 2.8 변경 하지만 _기본_ 동작 종속성을 확인 하는 것에 대 한 추가-DependencyVersion 스위치를 통해 종속성 확인 프로세스를 보다 자세히 제어 패키지 관리자 콘솔에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-136">Though NuGet 2.8 changes the _default_ behavior for resolving dependencies, it also adds more precise control over dependency resolution process via the -DependencyVersion switch in the package manager console.</span></span> <span data-ttu-id="99c37-137">스위치 가능한 가장 낮은 버전 (기본 동작), 가능한 최상 버전 또는 부 가장 높은 또는 패치 버전을 확인 하 고 종속성을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-137">The switch enables resolving dependencies to the lowest possible version (default behavior), the highest possible version, or the highest minor or patch version.</span></span>  <span data-ttu-id="99c37-138">이 스위치는 powershell 명령에서 설치 패키지에 대 한 에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-138">This switch only works for install-package in the powershell command.</span></span>

![DependencyVersion 스위치](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a><span data-ttu-id="99c37-140">DependencyVersion 특성</span><span class="sxs-lookup"><span data-stu-id="99c37-140">DependencyVersion Attribute</span></span>

<span data-ttu-id="99c37-141">위에서 설명한, 기능에 대 한 NuGet도 있었습니다 Nuget.Config 파일에서 새 특성을 설정 하는-DependencyVersion 스위치 외에도 정의 기본값은 어떤-DependencyVersion 스위치의 호출에 지정 되지 않은 경우 설치 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-141">In addition to the -DependencyVersion switch detailed above, NuGet has also allowed for the ability to set a new attribute in the Nuget.Config file defining what the default value is, if the -DependencyVersion switch is not specified in an invocation of install-package.</span></span> <span data-ttu-id="99c37-142">이 값 NuGet 패키지 관리자 대화 상자 설치 패키지는 모든 작업에도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-142">This value will also be respected by the NuGet Package Manager Dialog for any install package operations.</span></span> <span data-ttu-id="99c37-143">이 값을 설정 하려면 아래 특성 Nuget.Config 파일을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-143">To set this value, add the attribute below to your Nuget.Config file:</span></span>

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a><span data-ttu-id="99c37-144">미리 보기 NuGet 작업과-whatif를 지원함</span><span class="sxs-lookup"><span data-stu-id="99c37-144">Preview NuGet Operations With -whatif</span></span>

<span data-ttu-id="99c37-145">일부 NuGet 패키지가 상세한 종속성 그래프를 포함할 수 있으며 따라서 것 수는 설치 중에 도움이 될, 제거 또는 업데이트 작업을 먼저 실행 되는 작업을 확인 하려면.</span><span class="sxs-lookup"><span data-stu-id="99c37-145">Some NuGet packages can have deep dependency graphs, and as such, it can be helpful during an install, uninstall, or update operation to first see what will happen.</span></span> <span data-ttu-id="99c37-146">NuGet 2.8 패키지 설치, 제거 패키지 및 업데이트 패키지 명령의 명령을 적용 하는 패키지의 전체 closure 시각화를 사용 하도록 설정 하려면 표준 PowerShell-whatif 스위치를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-146">NuGet 2.8 adds the standard PowerShell -whatif switch to the install-package, uninstall-package, and update-package commands to enable visualizing the entire closure of packages to which the command will be applied.</span></span> <span data-ttu-id="99c37-147">예를 들면 `install-package Microsoft.AspNet.WebApi -whatif` 에 빈 ASP.NET 웹 응용 프로그램은 다음을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-147">For example, running `install-package Microsoft.AspNet.WebApi -whatif` in an empty ASP.NET Web application yields the following.</span></span>

    PM> install-package Microsoft.AspNet.WebApi -whatif
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.WebHost (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Core (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Client (≥ 5.0.0)'.
    Attempting to resolve dependency 'Newtonsoft.Json (≥ 4.5.11)'.
    Install Newtonsoft.Json 4.5.11
    Install Microsoft.AspNet.WebApi.Client 5.0.0
    Install Microsoft.AspNet.WebApi.Core 5.0.0
    Install Microsoft.AspNet.WebApi.WebHost 5.0.0
    Install Microsoft.AspNet.WebApi 5.0.0

## <a name="downgrade-package"></a><span data-ttu-id="99c37-148">다운 그레이드 패키지</span><span class="sxs-lookup"><span data-stu-id="99c37-148">Downgrade Package</span></span>

<span data-ttu-id="99c37-149">안정적인 최신 버전으로 롤백할로 결정 한 새 기능을 검토 하려면 패키지의 시험판 버전을 설치 하는 일반적이 지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-149">It is not uncommon to install a prerelease version of a package in order to investigate new features and then decide to roll back to the last stable version.</span></span> <span data-ttu-id="99c37-150">NuGet 2.8 하기 전에이 시험판 패키지 및 해당 종속성을 제거한 다음 이전 버전을 설치의 여러 단계 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-150">Prior to NuGet 2.8, this was a multi-step process of uninstalling the prerelease package and its dependencies, and then installing the earlier version.</span></span> <span data-ttu-id="99c37-151">그러나 NuGet 2.8와 업데이트 패키지는 이제 롤백할 전체 패키지 클로저 (예: 패키지의 종속성 트리) 이전 버전으로.</span><span class="sxs-lookup"><span data-stu-id="99c37-151">With NuGet 2.8, however, the update-package will now roll back the entire package closure (e.g. the package's dependency tree) to the previous version.</span></span>

## <a name="development-dependencies"></a><span data-ttu-id="99c37-152">개발 종속성</span><span class="sxs-lookup"><span data-stu-id="99c37-152">Development Dependencies</span></span>

<span data-ttu-id="99c37-153">개발 프로세스를 최적화 하는 데 사용 되는 도구를 포함 하 여 NuGet 패키지로-다양 한 유형의 기능을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-153">Many different types of capabilities can be delivered as NuGet packages - including tools that are used for optimizing the development process.</span></span> <span data-ttu-id="99c37-154">이러한 구성 요소를 새 패키지를 개발에 도움이 될 수 있지만 간주 되지 않아야 새 패키지의 종속성 나중에 게시할 때.</span><span class="sxs-lookup"><span data-stu-id="99c37-154">These components, while they can be instrumental in developing a new package, should not be considered a dependency of the new package when it's later published.</span></span> <span data-ttu-id="99c37-155">NuGet 2.8를 사용 하면 패키지에서 자신을 식별 하는 `.nuspec` 는 developmentDependency 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-155">NuGet 2.8 enables a package to identify itself in the `.nuspec` file as a developmentDependency.</span></span> <span data-ttu-id="99c37-156">설치 되 면이 메타 데이터도에 추가할는 `packages.config` 패키지가 설치 된 프로젝트의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-156">When installed, this metadata will also be added to the `packages.config` file of the project into which the package was installed.</span></span> <span data-ttu-id="99c37-157">경우는 `packages.config` 파일이 중 NuGet 종속성에 대 한 나중에 분석 된 `nuget.exe pack`, 개발 종속성으로 표시 하는 해당 종속성을 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-157">When that `packages.config` file is later analyzed for NuGet dependencies during `nuget.exe pack`, it will exclude those dependencies marked as development dependencies.</span></span>

## <a name="individual-packagesconfig-files-for-different-platforms"></a><span data-ttu-id="99c37-158">다른 플랫폼에 대해 개별 packages.config 파일</span><span class="sxs-lookup"><span data-stu-id="99c37-158">Individual packages.config Files for Different Platforms</span></span>

<span data-ttu-id="99c37-159">여러 대상 플랫폼에 대 한 응용 프로그램을 개발할 경우 일반적으로 각 해당 빌드 환경에 대 한 여러 프로젝트 파일에는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-159">When developing applications for multiple target platforms, it's common to have different project files for each of the respective build environments.</span></span> <span data-ttu-id="99c37-160">것도 다른 프로젝트 파일에서 다른 NuGet 패키지를 사용 하도록 패키지에 다양 한 플랫폼에 대 한 지원 수준이 다양 한 대로 합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-160">It is also common to consume different NuGet packages in different project files, as packages have varying levels of support for different platforms.</span></span> <span data-ttu-id="99c37-161">NuGet 2.8 다른 만들어이 시나리오에 대 한 향상 된 지원을 제공 `packages.config` 여러 플랫폼 관련 프로젝트 파일에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-161">NuGet 2.8 provides improved support for this scenario by creating different `packages.config` files for different platform-specific project files.</span></span>

![여러 package.config 파일](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a><span data-ttu-id="99c37-163">로컬 캐시에 대체 (fallback)</span><span class="sxs-lookup"><span data-stu-id="99c37-163">Fallback to Local Cache</span></span>

<span data-ttu-id="99c37-164">NuGet 패키지는 일반적으로 사용 된 원격 갤러리에서와 같은 경우 [은 NuGet 갤러리](http://www.nuget.org/) 는 네트워크 연결을 사용 하 여 다양 한 시나리오는 클라이언트가 연결 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-164">Though NuGet packages are typically consumed from a remote gallery such as [the NuGet gallery](http://www.nuget.org/) using a network connection, there are many scenarios where the client is not connected.</span></span> <span data-ttu-id="99c37-165">네트워크 연결 없이 NuGet 클라이언트에서 이러한 패키지는 로컬 캐시 NuGet의에서 클라이언트 컴퓨터에 이미 있던 경우에 패키지-설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-165">Without a network connection, the NuGet client was not able to successfully install packages - even when those packages were already on the client's machine in the local NuGet cache.</span></span> <span data-ttu-id="99c37-166">NuGet 2.8 패키지 관리자 콘솔에 대체 (fallback) 자동 캐시를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-166">NuGet 2.8 adds automatic cache fallback to the package manager console.</span></span> <span data-ttu-id="99c37-167">예를 들어 표시 되 면 네트워크 어댑터의 연결을 끊고 jQuery 설치, 콘솔 다음:</span><span class="sxs-lookup"><span data-stu-id="99c37-167">For example, when disconnecting the network adapter and installing jQuery, the console shows the following:</span></span>

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

<span data-ttu-id="99c37-168">캐시 대체 기능에는 특정 명령 인수 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-168">The cache fallback feature does not require any specific command arguments.</span></span> <span data-ttu-id="99c37-169">또한 캐시 대체 현재 패키지 관리자 콘솔 에서만에서 작동 함-동작 패키지 관리자 대화 상자에서 현재 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-169">Additionally, cache fallback currently works only in the package manager console - the behavior does not currently work in the package manager dialog.</span></span>

## <a name="webmatrix-nuget-client-updates"></a><span data-ttu-id="99c37-170">WebMatrix NuGet 클라이언트 업데이트</span><span class="sxs-lookup"><span data-stu-id="99c37-170">WebMatrix NuGet Client Updates</span></span>

<span data-ttu-id="99c37-171">NuGet 2.8 함께 WebMatrix 용 NuGet 확장 하도록 업데이트 되었습니다 포함 된 주요 기능을 많이 포함 [NuGet 2.5](../release-notes/nuget-2.5.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-171">Along with NuGet 2.8, the NuGet extension for WebMatrix was also updated to include many of the major features delivered with [NuGet 2.5](../release-notes/nuget-2.5.md).</span></span> <span data-ttu-id="99c37-172">' 업데이트 All', ' 최소 NuGet 버전 ' 및 콘텐츠 파일의 덮어쓰기를 허용 범위를 같은 새로운 기능이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-172">New capabilities include those such as 'Update All', 'Minimum NuGet Version', and allowing for overwriting of content files.</span></span>

<span data-ttu-id="99c37-173">WebMatrix 3에서 NuGet 패키지 관리자 확장을 업데이트.</span><span class="sxs-lookup"><span data-stu-id="99c37-173">To update your NuGet Package Manager extension in WebMatrix 3:</span></span>

1. <span data-ttu-id="99c37-174">열기 WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="99c37-174">Open WebMatrix 3</span></span>
1. <span data-ttu-id="99c37-175">리본 메뉴에서 확장 아이콘을 클릭</span><span class="sxs-lookup"><span data-stu-id="99c37-175">Click the Extensions icon in the ribbon</span></span>
1. <span data-ttu-id="99c37-176">업데이트 탭을 선택</span><span class="sxs-lookup"><span data-stu-id="99c37-176">Select the Updates tab</span></span>
1. <span data-ttu-id="99c37-177">NuGet 패키지 관리자 2.5.0를 업데이트 하려면 클릭</span><span class="sxs-lookup"><span data-stu-id="99c37-177">Click to update NuGet Package Manager to 2.5.0</span></span>
1. <span data-ttu-id="99c37-178">닫고 WebMatrix 3을 다시 시작</span><span class="sxs-lookup"><span data-stu-id="99c37-178">Close and restart WebMatrix 3</span></span>

<span data-ttu-id="99c37-179">WebMatrix 용 NuGet 패키지 관리자 확장의 NuGet 팀의 첫 번째 릴리스에서입니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-179">This is the NuGet team's first release of the NuGet Package Manager extension for WebMatrix.</span></span>  <span data-ttu-id="99c37-180">코드는 오픈 소스 NuGet 프로젝트에 Microsoft에서 최근에 제공 했습니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-180">The code was recently contributed by Microsoft into the open-source NuGet project.</span></span> <span data-ttu-id="99c37-181">이전에 NuGet 통합 WebMatrix에 빌드된 및 WebMatrix에서 대역 외에서 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-181">Previously, the NuGet integration was built into WebMatrix, and it could not be updated out of band from WebMatrix.</span></span>  <span data-ttu-id="99c37-182">이제는 기능을 추가로 나머지 NuGet의 클라이언트 도구와 함께 업데이트 했습니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-182">We now have the capability to further update it alongside the rest of NuGet's client tools.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="99c37-183">버그 수정</span><span class="sxs-lookup"><span data-stu-id="99c37-183">Bug Fixes</span></span>

<span data-ttu-id="99c37-184">업데이트 패키지의 성능 향상 된 만든 주요 버그 수정 중 하나-명령을 다시 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-184">One of the major bug fixes made was performance improvement in the  update-package -reinstall    command.</span></span>

<span data-ttu-id="99c37-185">이러한 기능과 앞에서 언급 한 성능 수정 외에이 버전의 NuGet 다른 많은 버그 수정 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-185">In addition to these features and the aforementioned performance fix, this release of NuGet also includes many other bug fixes.</span></span> <span data-ttu-id="99c37-186">181 총 문제는 릴리스에서 해결 했습니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-186">There were 181 total issues addressed in the release.</span></span> <span data-ttu-id="99c37-187">작업의 전체 목록에 대 한 항목에서에서 수정 된 NuGet 2.8 하십시오 보기는 [이 릴리스에 대 한 NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)합니다.</span><span class="sxs-lookup"><span data-stu-id="99c37-187">For a full list of the work items fixed in NuGet 2.8, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).</span></span>
