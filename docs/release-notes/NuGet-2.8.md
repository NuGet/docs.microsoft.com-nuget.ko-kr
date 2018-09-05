---
title: NuGet 2.8 릴리스 정보
description: 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함 하 여 NuGet 2.8에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547461"
---
# <a name="nuget-28-release-notes"></a><span data-ttu-id="51da5-103">NuGet 2.8 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="51da5-103">NuGet 2.8 Release Notes</span></span>

<span data-ttu-id="51da5-104">[2.7.2 NuGet 릴리스 정보](../release-notes/nuget-2.7.2.md) | [2.8.1 NuGet 릴리스 정보](../release-notes/nuget-2.8.1.md)</span><span class="sxs-lookup"><span data-stu-id="51da5-104">[NuGet 2.7.2 Release Notes](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md)</span></span>

<span data-ttu-id="51da5-105">NuGet 2.8은 2014 년 1 월 29 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-105">NuGet 2.8 was released on January 29, 2014.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="51da5-106">감사의 글</span><span class="sxs-lookup"><span data-stu-id="51da5-106">Acknowledgements</span></span>

1. <span data-ttu-id="51da5-107">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span><span class="sxs-lookup"><span data-stu-id="51da5-107">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span></span>
    - <span data-ttu-id="51da5-108">[#3466](https://nuget.codeplex.com/workitem/3466) -종속성 패키지의 Id를 확인 하는 패키지를 압축 합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-108">[#3466](https://nuget.codeplex.com/workitem/3466) - When packing packages, verifying Id of dependency packages.</span></span>
2. <span data-ttu-id="51da5-109">[Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span><span class="sxs-lookup"><span data-stu-id="51da5-109">[Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span></span>
    - <span data-ttu-id="51da5-110">[#2379](https://nuget.codeplex.com/workitem/2379) -persistening 피드를 자격 증명 때 $metadata 접미사를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-110">[#2379](https://nuget.codeplex.com/workitem/2379) - Remove the $metadata suffix when persistening feed credentials.</span></span>
3. <span data-ttu-id="51da5-111">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span><span class="sxs-lookup"><span data-stu-id="51da5-111">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span></span>
    - <span data-ttu-id="51da5-112">[#3538](http://nuget.codeplex.com/workitem/3538) -지원 nuget.exe 업데이트 명령에 대 한 프로젝트 파일을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-112">[#3538](http://nuget.codeplex.com/workitem/3538) - Support specifying project file for the nuget.exe update command.</span></span>
4. [<span data-ttu-id="51da5-113">Juan Gonzalez</span><span class="sxs-lookup"><span data-stu-id="51da5-113">Juan Gonzalez</span></span>](https://www.codeplex.com/site/users/view/jjgonzalez)
    - <span data-ttu-id="51da5-114">[#3536](http://nuget.codeplex.com/workitem/3536) -교체 토큰-IncludeReferencedProjects를 사용 하 여 전달 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-114">[#3536](http://nuget.codeplex.com/workitem/3536) - Replacement tokens not passed with -IncludeReferencedProjects.</span></span>
5. <span data-ttu-id="51da5-115">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span><span class="sxs-lookup"><span data-stu-id="51da5-115">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span></span>
    - <span data-ttu-id="51da5-116">[#3677](http://nuget.codeplex.com/workitem/3677) -해결 nuget.push 큰 패키지를 푸시할 때 OutOfMemoryException를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-116">[#3677](http://nuget.codeplex.com/workitem/3677) - Fix nuget.push throwing OutOfMemoryException when pushing large package.</span></span>
6. [<span data-ttu-id="51da5-117">Wouter Ouwens</span><span class="sxs-lookup"><span data-stu-id="51da5-117">Wouter Ouwens</span></span>](https://www.codeplex.com/site/users/view/Despotes)
    - <span data-ttu-id="51da5-118">[#3666](http://nuget.codeplex.com/workitem/3666) -프로젝트가 다른 CLI/c + + 프로젝트를 참조 하는 경우에 잘못 된 대상 경로 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-118">[#3666](http://nuget.codeplex.com/workitem/3666) - Fix incorrect target path when project references another CLI/C++ project.</span></span>
7. <span data-ttu-id="51da5-119">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="51da5-119">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="51da5-120">[#3639](https://nuget.codeplex.com/workitem/3639) -개발 종속성으로 기본적으로 설치 되도록 패키지를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-120">[#3639](https://nuget.codeplex.com/workitem/3639) - Allow packages to be installed as development dependencies by default</span></span>
8. <span data-ttu-id="51da5-121">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="51da5-121">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="51da5-122">[#3717](https://nuget.codeplex.com/workitem/3717) -최신 패치 버전에 대 한 암시적 업그레이드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-122">[#3717](https://nuget.codeplex.com/workitem/3717) - Remove implicit upgrades to the latest patch version</span></span>
9. [<span data-ttu-id="51da5-123">Gregory Vandenbrouck</span><span class="sxs-lookup"><span data-stu-id="51da5-123">Gregory Vandenbrouck</span></span>](https://www.codeplex.com/site/users/view/vdbg)
    - <span data-ttu-id="51da5-124">여러 버그 수정 및 NuGet.Server, nuget.exe 미러 명령 및 기타 향상 된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-124">Several bug fixes and improvements for NuGet.Server, the nuget.exe mirror command, and others.</span></span>
    - <span data-ttu-id="51da5-125">이 작업은 몇 개월에 걸쳐 2.8에 대 한 마스터 통합할 Gregory 오른쪽 타이밍에 함께 작업을 사용 하 여 수행 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-125">This work was done over several months, with Gregory working with us on the right timing to integrate into master for 2.8.</span></span>

## <a name="patch-resolution-for-dependencies"></a><span data-ttu-id="51da5-126">종속성에 대 한 패치 확인</span><span class="sxs-lookup"><span data-stu-id="51da5-126">Patch Resolution for Dependencies</span></span>

<span data-ttu-id="51da5-127">패키지 종속성을 해결 하는 경우 NuGet 패키지에서 종속성을 충족 하는 가장 낮은 주 및 부 패키지 버전을 선택 하는 전략을 구현 지금까지 했습니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-127">When resolving package dependencies, NuGet has historically implemented a strategy of selecting the lowest major and minor package version which satisfies the dependencies on the package.</span></span> <span data-ttu-id="51da5-128">그러나 주 및 부 버전을 달리 패치 버전을 항상 해결 된 가장 높은 버전으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-128">Unlike the major and minor version, however, the patch version was always resolved to the highest version.</span></span> <span data-ttu-id="51da5-129">좋은 의도로 동작 이지만 종속성을 사용 하 여 패키지를 설치 하는 것에 대 한 결정성이 부족을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-129">Though the behavior was well-intentioned, it created a lack of determinism for installing packages with dependencies.</span></span> <span data-ttu-id="51da5-130">다음 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="51da5-130">Consider the following example:</span></span>

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

<span data-ttu-id="51da5-131">이 예에서 Developer1 및 Developer2 설치 PackageA@1.0.0, 각 결국 PackageB의 다른 버전으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-131">In this example, even though Developer1 and Developer2 installed PackageA@1.0.0, each ended up with a different version of PackageB.</span></span> <span data-ttu-id="51da5-132">NuGet 2.8 패치 버전에 대 한 종속성 확인 동작이 주 버전과 부 버전에 대 한 동작을 사용 하 여 일관 되는이 기본 동작을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-132">NuGet 2.8 changes this default behavior such that the dependency resolution behavior for patch versions is consistent with the behavior for major and minor versions.</span></span> <span data-ttu-id="51da5-133">그런 다음 위의 예제에서는 PackageB@1.0.0 설치의 결과로 설치할 PackageA@1.0.0최신 패치 버전에 관계 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-133">In the above example, then, PackageB@1.0.0 would be installed as a result of installing PackageA@1.0.0, regardless of the newer patch version.</span></span>

## <a name="-dependencyversion-switch"></a><span data-ttu-id="51da5-134">-DependencyVersion 스위치</span><span class="sxs-lookup"><span data-stu-id="51da5-134">-DependencyVersion Switch</span></span>

<span data-ttu-id="51da5-135">NuGet 2.8 변경 하지만 합니다 _기본_ 동작 종속성을 해결 하는 것에 대 한 추가-DependencyVersion 스위치를 통해 종속성 확인 프로세스를 보다 정밀 하 게 제어 패키지 관리자 콘솔에서.</span><span class="sxs-lookup"><span data-stu-id="51da5-135">Though NuGet 2.8 changes the _default_ behavior for resolving dependencies, it also adds more precise control over dependency resolution process via the -DependencyVersion switch in the package manager console.</span></span> <span data-ttu-id="51da5-136">스위치를 통해 가능한 가장 낮은 버전 (기본 동작), 가능한 최상 버전을 가장 높은 부 또는 패치 버전에 대 한 종속성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-136">The switch enables resolving dependencies to the lowest possible version (default behavior), the highest possible version, or the highest minor or patch version.</span></span>  <span data-ttu-id="51da5-137">이 스위치는 powershell 명령에서 설치 패키지 에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-137">This switch only works for install-package in the powershell command.</span></span>

![DependencyVersion 스위치](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a><span data-ttu-id="51da5-139">DependencyVersion 특성</span><span class="sxs-lookup"><span data-stu-id="51da5-139">DependencyVersion Attribute</span></span>

<span data-ttu-id="51da5-140">위에서 설명한, NuGet에도 기능에 대 한 허용 Nuget.Config 파일에서 새 특성을 설정 하려면-DependencyVersion 스위치 외에도 정의 기본값은 어떤 호출-DependencyVersion 스위치를 지정 하지 않은 경우 설치 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-140">In addition to the -DependencyVersion switch detailed above, NuGet has also allowed for the ability to set a new attribute in the Nuget.Config file defining what the default value is, if the -DependencyVersion switch is not specified in an invocation of install-package.</span></span> <span data-ttu-id="51da5-141">이 값이 모든 설치 패키지 작업에 대 한 NuGet 패키지 관리자 대화 상자도 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-141">This value will also be respected by the NuGet Package Manager Dialog for any install package operations.</span></span> <span data-ttu-id="51da5-142">이 값을 설정 하려면 아래 특성 Nuget.Config 파일에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-142">To set this value, add the attribute below to your Nuget.Config file:</span></span>

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a><span data-ttu-id="51da5-143">-Whatif를 사용 하 여 미리 보기 NuGet 작업</span><span class="sxs-lookup"><span data-stu-id="51da5-143">Preview NuGet Operations With -whatif</span></span>

<span data-ttu-id="51da5-144">일부 NuGet 패키지 전체 종속성 그래프를 포함할 수 있으며 따라서이 수를 설치 하는 동안 유용할 제거 또는 업데이트 작업을 먼저 발생 하는 결과 확인 하려면.</span><span class="sxs-lookup"><span data-stu-id="51da5-144">Some NuGet packages can have deep dependency graphs, and as such, it can be helpful during an install, uninstall, or update operation to first see what will happen.</span></span> <span data-ttu-id="51da5-145">NuGet 2.8 패키지 설치, 제거 패키지 및 패키지 업데이트 명령을 적용 되는 패키지의 완전 한 클로저 시각화를 활성화 하는 명령을 표준 PowerShell-whatif 스위치를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-145">NuGet 2.8 adds the standard PowerShell -whatif switch to the install-package, uninstall-package, and update-package commands to enable visualizing the entire closure of packages to which the command will be applied.</span></span> <span data-ttu-id="51da5-146">예를 들어 실행 `install-package Microsoft.AspNet.WebApi -whatif` 에서 빈 ASP.NET 웹 응용 프로그램에는 다음이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-146">For example, running `install-package Microsoft.AspNet.WebApi -whatif` in an empty ASP.NET Web application yields the following.</span></span>

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

## <a name="downgrade-package"></a><span data-ttu-id="51da5-147">다운 그레이드 패키지</span><span class="sxs-lookup"><span data-stu-id="51da5-147">Downgrade Package</span></span>

<span data-ttu-id="51da5-148">새로운 기능을 조사 하기 위해 패키지의 시험판 버전을 설치 하 고 마지막 안정적인 버전으로 롤백하려면 다음 결정을 일반적이 지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-148">It is not uncommon to install a prerelease version of a package in order to investigate new features and then decide to roll back to the last stable version.</span></span> <span data-ttu-id="51da5-149">NuGet 2.8 이전에이 시험판 패키지 및 해당 종속성을 제거 하 고 다음 이전 버전을 설치 하는 여러 단계의 프로세스가 이었습니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-149">Prior to NuGet 2.8, this was a multi-step process of uninstalling the prerelease package and its dependencies, and then installing the earlier version.</span></span> <span data-ttu-id="51da5-150">그러나 NuGet 2.8을 사용 하 여 업데이트 패키지를 이제 롤백됩니다 전체 패키지 클로저 (예: 패키지의 종속성 트리) 이전 버전으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-150">With NuGet 2.8, however, the update-package will now roll back the entire package closure (e.g. the package's dependency tree) to the previous version.</span></span>

## <a name="development-dependencies"></a><span data-ttu-id="51da5-151">개발 종속성</span><span class="sxs-lookup"><span data-stu-id="51da5-151">Development Dependencies</span></span>

<span data-ttu-id="51da5-152">개발 프로세스를 최적화 하는 데 사용 되는 도구를 포함 하는 NuGet 패키지로-다양 한 기능을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-152">Many different types of capabilities can be delivered as NuGet packages - including tools that are used for optimizing the development process.</span></span> <span data-ttu-id="51da5-153">이러한 구성 요소를 새 패키지를 개발 하는 데 도움이 될 수 있지만 이러한 간주 되지 않아야 새 패키지의 종속성 나중에 게시 될 때입니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-153">These components, while they can be instrumental in developing a new package, should not be considered a dependency of the new package when it's later published.</span></span> <span data-ttu-id="51da5-154">NuGet 2.8에 자신을 식별 하는 패키지를 사용 하도록 설정 된 `.nuspec` 는 developmentDependency 파일로.</span><span class="sxs-lookup"><span data-stu-id="51da5-154">NuGet 2.8 enables a package to identify itself in the `.nuspec` file as a developmentDependency.</span></span> <span data-ttu-id="51da5-155">설치 하는 경우이 메타 데이터는도 추가할 수는 `packages.config` 패키지가 설치 된 프로젝트의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-155">When installed, this metadata will also be added to the `packages.config` file of the project into which the package was installed.</span></span> <span data-ttu-id="51da5-156">경우는 `packages.config` 파일이 중 NuGet 종속성에 대 한 나중에 분석 된 `nuget.exe pack`, 개발 종속성으로 표시 하는 이러한 종속성을 제외 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-156">When that `packages.config` file is later analyzed for NuGet dependencies during `nuget.exe pack`, it will exclude those dependencies marked as development dependencies.</span></span>

## <a name="individual-packagesconfig-files-for-different-platforms"></a><span data-ttu-id="51da5-157">다양 한 플랫폼에 대 한 개별 packages.config 파일</span><span class="sxs-lookup"><span data-stu-id="51da5-157">Individual packages.config Files for Different Platforms</span></span>

<span data-ttu-id="51da5-158">여러 대상 플랫폼에 대 한 응용 프로그램을 개발 하는 경우 각 해당 빌드 환경에 대해 다른 프로젝트 파일을 저장 하는 일반적인 것입니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-158">When developing applications for multiple target platforms, it's common to have different project files for each of the respective build environments.</span></span> <span data-ttu-id="51da5-159">패키지에 다양 한 플랫폼에 대 한 지원 수준이 다양 한 대로도 여러 프로젝트 파일에서 다른 NuGet 패키지 사용에 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-159">It is also common to consume different NuGet packages in different project files, as packages have varying levels of support for different platforms.</span></span> <span data-ttu-id="51da5-160">NuGet 2.8 다른 만들어이 시나리오에 대 한 향상 된 지원을 제공 `packages.config` 다양 한 플랫폼 관련 프로젝트 파일에 대 한 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-160">NuGet 2.8 provides improved support for this scenario by creating different `packages.config` files for different platform-specific project files.</span></span>

![여러 package.config 파일](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a><span data-ttu-id="51da5-162">로컬 캐시에 대체 (fallback)</span><span class="sxs-lookup"><span data-stu-id="51da5-162">Fallback to Local Cache</span></span>

<span data-ttu-id="51da5-163">NuGet 패키지는 일반적으로 사용 된 원격 갤러리에서와 같은 있지만 [NuGet 갤러리](http://www.nuget.org/) 는 네트워크 연결을 사용 하 여, 다양 한 시나리오는 클라이언트가 연결 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-163">Though NuGet packages are typically consumed from a remote gallery such as [the NuGet gallery](http://www.nuget.org/) using a network connection, there are many scenarios where the client is not connected.</span></span> <span data-ttu-id="51da5-164">네트워크 연결 없이 NuGet 클라이언트에서 해당 패키지는 로컬 NuGet 캐시에서 클라이언트 컴퓨터에 이미 있던 경우에-패키지를 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-164">Without a network connection, the NuGet client was not able to successfully install packages - even when those packages were already on the client's machine in the local NuGet cache.</span></span> <span data-ttu-id="51da5-165">2.8 NuGet 패키지 관리자 콘솔에 대체 (fallback) 자동 캐시를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-165">NuGet 2.8 adds automatic cache fallback to the package manager console.</span></span> <span data-ttu-id="51da5-166">예를 들어, 표시 되는 경우 네트워크 어댑터 연결을 끊고 jQuery 설치, 콘솔 다음:</span><span class="sxs-lookup"><span data-stu-id="51da5-166">For example, when disconnecting the network adapter and installing jQuery, the console shows the following:</span></span>

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

<span data-ttu-id="51da5-167">캐시 대체 (fallback) 기능에는 특정 명령 인수를 사용할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-167">The cache fallback feature does not require any specific command arguments.</span></span> <span data-ttu-id="51da5-168">또한 대체 (fallback) 캐시는 현재 패키지 관리자 콘솔 에서만에서 작동-동작 패키지 관리자 대화 상자에서 현재 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-168">Additionally, cache fallback currently works only in the package manager console - the behavior does not currently work in the package manager dialog.</span></span>

## <a name="webmatrix-nuget-client-updates"></a><span data-ttu-id="51da5-169">WebMatrix NuGet 클라이언트 업데이트</span><span class="sxs-lookup"><span data-stu-id="51da5-169">WebMatrix NuGet Client Updates</span></span>

<span data-ttu-id="51da5-170">NuGet 2.8 함께 WebMatrix 용 NuGet 확장은 포함 된 주요 기능을 많이 포함 하도록 업데이트도 되었으며 [NuGet 2.5](../release-notes/nuget-2.5.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-170">Along with NuGet 2.8, the NuGet extension for WebMatrix was also updated to include many of the major features delivered with [NuGet 2.5](../release-notes/nuget-2.5.md).</span></span> <span data-ttu-id="51da5-171">' 업데이트 All', ' 최소 NuGet 버전 ' 및 콘텐츠 파일을 덮어쓸 수 있습니다와 같은 새로운 기능 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-171">New capabilities include those such as 'Update All', 'Minimum NuGet Version', and allowing for overwriting of content files.</span></span>

<span data-ttu-id="51da5-172">WebMatrix 3에서 NuGet 패키지 관리자 확장을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-172">To update your NuGet Package Manager extension in WebMatrix 3:</span></span>

1. <span data-ttu-id="51da5-173">WebMatrix 3를 열려면</span><span class="sxs-lookup"><span data-stu-id="51da5-173">Open WebMatrix 3</span></span>
1. <span data-ttu-id="51da5-174">리본에서 확장 아이콘을 클릭</span><span class="sxs-lookup"><span data-stu-id="51da5-174">Click the Extensions icon in the ribbon</span></span>
1. <span data-ttu-id="51da5-175">[업데이트] 탭을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-175">Select the Updates tab</span></span>
1. <span data-ttu-id="51da5-176">2.5.0에 NuGet 패키지 관리자를 업데이트 하려면 클릭</span><span class="sxs-lookup"><span data-stu-id="51da5-176">Click to update NuGet Package Manager to 2.5.0</span></span>
1. <span data-ttu-id="51da5-177">닫고 WebMatrix 3를 다시 시작</span><span class="sxs-lookup"><span data-stu-id="51da5-177">Close and restart WebMatrix 3</span></span>

<span data-ttu-id="51da5-178">이것은 WebMatrix에 대 한 NuGet 패키지 관리자 확장의 NuGet 팀의 첫 번째 릴리스입니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-178">This is the NuGet team's first release of the NuGet Package Manager extension for WebMatrix.</span></span>  <span data-ttu-id="51da5-179">코드는 최근에 Microsoft에서 오픈 소스 NuGet 프로젝트에 기여 했습니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-179">The code was recently contributed by Microsoft into the open-source NuGet project.</span></span> <span data-ttu-id="51da5-180">이전에 NuGet 통합 WebMatrix에 빌드된 및 WebMatrix에서 대역 외에서 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-180">Previously, the NuGet integration was built into WebMatrix, and it could not be updated out of band from WebMatrix.</span></span>  <span data-ttu-id="51da5-181">이제 추가로 나머지 NuGet의 클라이언트 도구와 함께 업데이트 하는 기능.</span><span class="sxs-lookup"><span data-stu-id="51da5-181">We now have the capability to further update it alongside the rest of NuGet's client tools.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="51da5-182">버그 수정</span><span class="sxs-lookup"><span data-stu-id="51da5-182">Bug Fixes</span></span>

<span data-ttu-id="51da5-183">업데이트 패키지의 성능 향상 된 만든 주요 버그 수정 중-명령을 다시 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-183">One of the major bug fixes made was performance improvement in the  update-package -reinstall    command.</span></span>

<span data-ttu-id="51da5-184">이 릴리스의 NuGet에는 이러한 기능 및 앞에서 언급 한 성능 문제를 해결 하는 것 외에도 다른 많은 버그 수정도 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-184">In addition to these features and the aforementioned performance fix, this release of NuGet also includes many other bug fixes.</span></span> <span data-ttu-id="51da5-185">릴리스에서 해결 181 총 문제가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-185">There were 181 total issues addressed in the release.</span></span> <span data-ttu-id="51da5-186">작업의 전체 목록은 항목에서에서 수정 된 NuGet 2.8 하세요 보기는 [이 릴리스의 NuGet 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)합니다.</span><span class="sxs-lookup"><span data-stu-id="51da5-186">For a full list of the work items fixed in NuGet 2.8, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).</span></span>
