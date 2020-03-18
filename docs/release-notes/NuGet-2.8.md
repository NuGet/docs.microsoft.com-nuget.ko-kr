---
title: NuGet 2.8 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 2.8에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428356"
---
# <a name="nuget-28-release-notes"></a><span data-ttu-id="6b71d-103">NuGet 2.8 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="6b71d-103">NuGet 2.8 Release Notes</span></span>

<span data-ttu-id="6b71d-104">Nuget [2.7.2 릴리스 정보](../release-notes/nuget-2.7.2.md) | [Nuget 2.8.1 릴리스 정보](../release-notes/nuget-2.8.1.md)</span><span class="sxs-lookup"><span data-stu-id="6b71d-104">[NuGet 2.7.2 Release Notes](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md)</span></span>

<span data-ttu-id="6b71d-105">NuGet 2.8은 2014 년 1 월 29 일에 출시 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-105">NuGet 2.8 was released on January 29, 2014.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="6b71d-106">감사의 말</span><span class="sxs-lookup"><span data-stu-id="6b71d-106">Acknowledgements</span></span>

1. <span data-ttu-id="6b71d-107">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span><span class="sxs-lookup"><span data-stu-id="6b71d-107">[Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))</span></span>
    - <span data-ttu-id="6b71d-108">[#3466](https://nuget.codeplex.com/workitem/3466) -패키지를 압축 하는 경우 종속성 패키지의 Id를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-108">[#3466](https://nuget.codeplex.com/workitem/3466) - When packing packages, verifying Id of dependency packages.</span></span>
2. <span data-ttu-id="6b71d-109">[텐 Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span><span class="sxs-lookup"><span data-stu-id="6b71d-109">[Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))</span></span>
    - <span data-ttu-id="6b71d-110">[#2379](https://nuget.codeplex.com/workitem/2379) -피드 자격 증명을 persistening 때 $metadata 접미사를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-110">[#2379](https://nuget.codeplex.com/workitem/2379) - Remove the $metadata suffix when persistening feed credentials.</span></span>
3. <span data-ttu-id="6b71d-111">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span><span class="sxs-lookup"><span data-stu-id="6b71d-111">[Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))</span></span>
    - <span data-ttu-id="6b71d-112">[#3538](http://nuget.codeplex.com/workitem/3538) -nuget.exe 업데이트 명령에 대 한 프로젝트 파일 지정을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-112">[#3538](http://nuget.codeplex.com/workitem/3538) - Support specifying project file for the nuget.exe update command.</span></span>
4. [<span data-ttu-id="6b71d-113">Juan Gonzalez</span><span class="sxs-lookup"><span data-stu-id="6b71d-113">Juan Gonzalez</span></span>](https://www.codeplex.com/site/users/view/jjgonzalez)
    - <span data-ttu-id="6b71d-114">[#3536](http://nuget.codeplex.com/workitem/3536) -대체 토큰이-IncludeReferencedProjects로 전달 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-114">[#3536](http://nuget.codeplex.com/workitem/3536) - Replacement tokens not passed with -IncludeReferencedProjects.</span></span>
5. <span data-ttu-id="6b71d-115">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span><span class="sxs-lookup"><span data-stu-id="6b71d-115">[David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))</span></span>
    - <span data-ttu-id="6b71d-116">[#3677](http://nuget.codeplex.com/workitem/3677) -대량 패키지를 푸시할 때 OutOfMemoryException throw를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-116">[#3677](http://nuget.codeplex.com/workitem/3677) - Fix nuget.push throwing OutOfMemoryException when pushing large package.</span></span>
6. [<span data-ttu-id="6b71d-117">Wouter Ouwens</span><span class="sxs-lookup"><span data-stu-id="6b71d-117">Wouter Ouwens</span></span>](https://www.codeplex.com/site/users/view/Despotes)
    - <span data-ttu-id="6b71d-118">[#3666](http://nuget.codeplex.com/workitem/3666) -프로젝트가 다른 CLI/C++ 프로젝트를 참조할 때 잘못 된 대상 경로를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-118">[#3666](http://nuget.codeplex.com/workitem/3666) - Fix incorrect target path when project references another CLI/C++ project.</span></span>
7. <span data-ttu-id="6b71d-119">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span><span class="sxs-lookup"><span data-stu-id="6b71d-119">[Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))</span></span>
    - <span data-ttu-id="6b71d-120">[#3639](https://nuget.codeplex.com/workitem/3639) -패키지를 기본적으로 개발 종속성으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-120">[#3639](https://nuget.codeplex.com/workitem/3639) - Allow packages to be installed as development dependencies by default</span></span>
8. <span data-ttu-id="6b71d-121">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span><span class="sxs-lookup"><span data-stu-id="6b71d-121">[David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))</span></span>
    - <span data-ttu-id="6b71d-122">[#3717](https://nuget.codeplex.com/workitem/3717) -최신 패치 버전에 대 한 암시적 업그레이드 제거</span><span class="sxs-lookup"><span data-stu-id="6b71d-122">[#3717](https://nuget.codeplex.com/workitem/3717) - Remove implicit upgrades to the latest patch version</span></span>
9. [<span data-ttu-id="6b71d-123">Gregory Vandenbrouck</span><span class="sxs-lookup"><span data-stu-id="6b71d-123">Gregory Vandenbrouck</span></span>](https://www.codeplex.com/site/users/view/vdbg)
    - <span data-ttu-id="6b71d-124">NuGet. Server, nuget.exe 미러 명령 및 기타에 대 한 여러 버그 수정 및 개선 사항</span><span class="sxs-lookup"><span data-stu-id="6b71d-124">Several bug fixes and improvements for NuGet.Server, the nuget.exe mirror command, and others.</span></span>
    - <span data-ttu-id="6b71d-125">이러한 작업은 몇 달 이내에 수행 되었으며, Gregory를 사용 하 여 2.8에 대 한 마스터에 통합 하는 데 적합 한 타이밍에 대해 노력 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-125">This work was done over several months, with Gregory working with us on the right timing to integrate into master for 2.8.</span></span>

## <a name="patch-resolution-for-dependencies"></a><span data-ttu-id="6b71d-126">종속성에 대 한 패치 확인</span><span class="sxs-lookup"><span data-stu-id="6b71d-126">Patch Resolution for Dependencies</span></span>

<span data-ttu-id="6b71d-127">패키지 종속성을 확인할 때 NuGet은 패키지의 종속성을 충족 하는 가장 낮은 주 및 부 패키지 버전을 선택 하는 전략을 지금 구현 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-127">When resolving package dependencies, NuGet has historically implemented a strategy of selecting the lowest major and minor package version which satisfies the dependencies on the package.</span></span> <span data-ttu-id="6b71d-128">그러나 주 버전과 부 버전이 달리 패치 버전은 항상 가장 높은 버전으로 확인 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-128">Unlike the major and minor version, however, the patch version was always resolved to the highest version.</span></span> <span data-ttu-id="6b71d-129">이 동작은 잘 악의적 종속성이 포함 된 패키지를 설치 하는 것이 적합 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-129">Though the behavior was well-intentioned, it created a lack of determinism for installing packages with dependencies.</span></span> <span data-ttu-id="6b71d-130">다음과 같은 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6b71d-130">Consider the following example:</span></span>

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

<span data-ttu-id="6b71d-131">이 예제에서는 Developer1 및 Developer2가 PackageA@1.0.0설치 된 경우에도 각각 다른 버전의 PackageB로 종료 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-131">In this example, even though Developer1 and Developer2 installed PackageA@1.0.0, each ended up with a different version of PackageB.</span></span> <span data-ttu-id="6b71d-132">NuGet 2.8은 패치 버전에 대 한 종속성 확인 동작이 주 버전 및 부 버전의 동작과 일치 하도록이 기본 동작을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-132">NuGet 2.8 changes this default behavior such that the dependency resolution behavior for patch versions is consistent with the behavior for major and minor versions.</span></span> <span data-ttu-id="6b71d-133">위의 예에서는 최신 패치 버전에 관계 없이 PackageA@1.0.0를 설치한 결과로 PackageB@1.0.0를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-133">In the above example, then, PackageB@1.0.0 would be installed as a result of installing PackageA@1.0.0, regardless of the newer patch version.</span></span>

## <a name="-dependencyversion-switch"></a><span data-ttu-id="6b71d-134">-DependencyVersion 스위치</span><span class="sxs-lookup"><span data-stu-id="6b71d-134">-DependencyVersion Switch</span></span>

<span data-ttu-id="6b71d-135">NuGet 2.8은 종속성을 확인 하는 _기본_ 동작을 변경 하지만 패키지 관리자 콘솔의-DependencyVersion 스위치를 통해 종속성 확인 프로세스를 보다 정확 하 게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-135">Though NuGet 2.8 changes the _default_ behavior for resolving dependencies, it also adds more precise control over dependency resolution process via the -DependencyVersion switch in the package manager console.</span></span> <span data-ttu-id="6b71d-136">스위치를 사용 하면 가능한 가장 낮은 버전 (기본 동작), 가능한 가장 높은 버전 또는 가장 높은 부 또는 패치 버전으로 종속성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-136">The switch enables resolving dependencies to the lowest possible version (default behavior), the highest possible version, or the highest minor or patch version.</span></span>  <span data-ttu-id="6b71d-137">이 스위치는 powershell 명령에서 설치 패키지에 대해서만 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-137">This switch only works for install-package in the powershell command.</span></span>

![DependencyVersion 스위치](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a><span data-ttu-id="6b71d-139">DependencyVersion 특성</span><span class="sxs-lookup"><span data-stu-id="6b71d-139">DependencyVersion Attribute</span></span>

<span data-ttu-id="6b71d-140">위에서 설명 하는-DependencyVersion 스위치 외에도 NuGet은의 호출에-DependencyVersion 스위치가 지정 되지 않은 경우 기본값을 정의 하는 Nuget 파일에 새 특성을 설정 하는 기능을 허용 합니다. 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-140">In addition to the -DependencyVersion switch detailed above, NuGet has also allowed for the ability to set a new attribute in the Nuget.Config file defining what the default value is, if the -DependencyVersion switch is not specified in an invocation of install-package.</span></span> <span data-ttu-id="6b71d-141">이 값은 또한 패키지 설치 작업에 대 한 NuGet 패키지 관리자 대화 상자에서 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-141">This value will also be respected by the NuGet Package Manager Dialog for any install package operations.</span></span> <span data-ttu-id="6b71d-142">이 값을 설정 하려면 아래 특성을 Nuget.exe 파일에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-142">To set this value, add the attribute below to your Nuget.Config file:</span></span>

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a><span data-ttu-id="6b71d-143">-Whatif를 사용 하 여 NuGet 작업 미리 보기</span><span class="sxs-lookup"><span data-stu-id="6b71d-143">Preview NuGet Operations With -whatif</span></span>

<span data-ttu-id="6b71d-144">일부 NuGet 패키지에는 심층 종속성 그래프가 있을 수 있으며,이에 따라 설치, 제거 또는 업데이트 작업 중에 수행 되는 작업을 먼저 확인 하는 것이 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-144">Some NuGet packages can have deep dependency graphs, and as such, it can be helpful during an install, uninstall, or update operation to first see what will happen.</span></span> <span data-ttu-id="6b71d-145">NuGet 2.8은 명령이 적용 되는 패키지의 전체 클로저를 시각화할 수 있도록 표준 PowerShell-whatif 스위치를 설치 패키지, 제거 패키지 및 업데이트 패키지 명령에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-145">NuGet 2.8 adds the standard PowerShell -whatif switch to the install-package, uninstall-package, and update-package commands to enable visualizing the entire closure of packages to which the command will be applied.</span></span> <span data-ttu-id="6b71d-146">예를 들어 빈 ASP.NET 웹 응용 프로그램에서 `install-package Microsoft.AspNet.WebApi -whatif`를 실행 하면 다음과 같은 결과가 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-146">For example, running `install-package Microsoft.AspNet.WebApi -whatif` in an empty ASP.NET Web application yields the following.</span></span>

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

## <a name="downgrade-package"></a><span data-ttu-id="6b71d-147">패키지 다운 그레이드</span><span class="sxs-lookup"><span data-stu-id="6b71d-147">Downgrade Package</span></span>

<span data-ttu-id="6b71d-148">새 기능을 조사 하 여 안정적인 최신 버전으로 롤백하려면 먼저 시험판 버전의 패키지를 설치 하는 것이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-148">It is not uncommon to install a prerelease version of a package in order to investigate new features and then decide to roll back to the last stable version.</span></span> <span data-ttu-id="6b71d-149">NuGet 2.8 이전 버전은 시험판 패키지와 해당 종속성을 제거한 후 이전 버전을 설치 하는 여러 단계로 이루어진 프로세스 였습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-149">Prior to NuGet 2.8, this was a multi-step process of uninstalling the prerelease package and its dependencies, and then installing the earlier version.</span></span> <span data-ttu-id="6b71d-150">그러나 NuGet 2.8에서 업데이트 패키지는 이제 전체 패키지 닫기 (예: 패키지의 종속성 트리)를 이전 버전으로 롤백합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-150">With NuGet 2.8, however, the update-package will now roll back the entire package closure (e.g. the package's dependency tree) to the previous version.</span></span>

## <a name="development-dependencies"></a><span data-ttu-id="6b71d-151">개발 종속성</span><span class="sxs-lookup"><span data-stu-id="6b71d-151">Development Dependencies</span></span>

<span data-ttu-id="6b71d-152">개발 프로세스를 최적화 하는 데 사용 되는 도구를 포함 하 여 다양 한 유형의 기능을 NuGet 패키지로 배달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-152">Many different types of capabilities can be delivered as NuGet packages - including tools that are used for optimizing the development process.</span></span> <span data-ttu-id="6b71d-153">이러한 구성 요소는 새 패키지를 개발 하는 데 사용할 수 있는 반면 나중에 게시 될 때 새 패키지의 종속성으로 간주 되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-153">These components, while they can be instrumental in developing a new package, should not be considered a dependency of the new package when it's later published.</span></span> <span data-ttu-id="6b71d-154">NuGet 2.8을 사용 하면 `.nuspec` 파일에서 패키지 자체를 developmentDependency으로 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-154">NuGet 2.8 enables a package to identify itself in the `.nuspec` file as a developmentDependency.</span></span> <span data-ttu-id="6b71d-155">설치 된 경우이 메타 데이터는 패키지가 설치 된 프로젝트의 `packages.config` 파일에도 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-155">When installed, this metadata will also be added to the `packages.config` file of the project into which the package was installed.</span></span> <span data-ttu-id="6b71d-156">이 `packages.config` 파일이 `nuget.exe pack`동안 NuGet 종속성에 대해 나중에 분석 되는 경우 개발 종속성으로 표시 된 종속성을 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-156">When that `packages.config` file is later analyzed for NuGet dependencies during `nuget.exe pack`, it will exclude those dependencies marked as development dependencies.</span></span>

## <a name="individual-packagesconfig-files-for-different-platforms"></a><span data-ttu-id="6b71d-157">다른 플랫폼용 개별 패키지 .config 파일</span><span class="sxs-lookup"><span data-stu-id="6b71d-157">Individual packages.config Files for Different Platforms</span></span>

<span data-ttu-id="6b71d-158">여러 대상 플랫폼용 응용 프로그램을 개발 하는 경우 각 빌드 환경에 대해 서로 다른 프로젝트 파일을 포함 하는 것이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-158">When developing applications for multiple target platforms, it's common to have different project files for each of the respective build environments.</span></span> <span data-ttu-id="6b71d-159">또한 패키지 마다 다양 한 플랫폼에 대 한 다양 한 지원 수준이 있기 때문에 다양 한 프로젝트 파일에서 다른 NuGet 패키지를 사용 하는 것이 일반적입니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-159">It is also common to consume different NuGet packages in different project files, as packages have varying levels of support for different platforms.</span></span> <span data-ttu-id="6b71d-160">NuGet 2.8은 플랫폼별 프로젝트 파일 마다 다른 `packages.config` 파일을 만들어이 시나리오에 대 한 향상 된 지원을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-160">NuGet 2.8 provides improved support for this scenario by creating different `packages.config` files for different platform-specific project files.</span></span>

![여러 패키지 .config 파일](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a><span data-ttu-id="6b71d-162">로컬 캐시로 대체</span><span class="sxs-lookup"><span data-stu-id="6b71d-162">Fallback to Local Cache</span></span>

<span data-ttu-id="6b71d-163">NuGet 패키지는 일반적으로 네트워크 연결을 사용 하 여 [nuget 갤러리](http://www.nuget.org/) 와 같은 원격 갤러리에서 사용 되지만 클라이언트가 연결 되지 않은 많은 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-163">Though NuGet packages are typically consumed from a remote gallery such as [the NuGet gallery](http://www.nuget.org/) using a network connection, there are many scenarios where the client is not connected.</span></span> <span data-ttu-id="6b71d-164">네트워크에 연결 되지 않은 경우 NuGet 클라이언트는 패키지를 성공적으로 설치할 수 없습니다. 해당 패키지는 로컬 NuGet 캐시의 클라이언트 컴퓨터에 이미 있는 경우에도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-164">Without a network connection, the NuGet client was not able to successfully install packages - even when those packages were already on the client's machine in the local NuGet cache.</span></span> <span data-ttu-id="6b71d-165">NuGet 2.8은 패키지 관리자 콘솔에 자동 캐시 대체를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-165">NuGet 2.8 adds automatic cache fallback to the package manager console.</span></span> <span data-ttu-id="6b71d-166">예를 들어 네트워크 어댑터의 연결을 끊고 jQuery를 설치 하면 콘솔에 다음이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-166">For example, when disconnecting the network adapter and installing jQuery, the console shows the following:</span></span>

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

<span data-ttu-id="6b71d-167">캐시 대체 (fallback) 기능에는 특정 명령 인수가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-167">The cache fallback feature does not require any specific command arguments.</span></span> <span data-ttu-id="6b71d-168">또한 cache fallback은 현재 패키지 관리자 콘솔 에서만 작동 합니다 .이 동작은 현재 패키지 관리자 대화 상자에서 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-168">Additionally, cache fallback currently works only in the package manager console - the behavior does not currently work in the package manager dialog.</span></span>

## <a name="webmatrix-nuget-client-updates"></a><span data-ttu-id="6b71d-169">WebMatrix NuGet 클라이언트 업데이트</span><span class="sxs-lookup"><span data-stu-id="6b71d-169">WebMatrix NuGet Client Updates</span></span>

<span data-ttu-id="6b71d-170">Nuget 2.8과 함께 WebMatrix에 대 한 NuGet 확장도 [nuget 2.5](../release-notes/nuget-2.5.md)과 함께 제공 되는 많은 주요 기능을 포함 하도록 업데이트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-170">Along with NuGet 2.8, the NuGet extension for WebMatrix was also updated to include many of the major features delivered with [NuGet 2.5](../release-notes/nuget-2.5.md).</span></span> <span data-ttu-id="6b71d-171">새 기능에는 ' 업데이트 모두 ', ' 최소 NuGet 버전 ' 및 콘텐츠 파일 덮어쓰기를 허용 하는 기능이 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-171">New capabilities include those such as 'Update All', 'Minimum NuGet Version', and allowing for overwriting of content files.</span></span>

<span data-ttu-id="6b71d-172">WebMatrix 3에서 NuGet 패키지 관리자 확장을 업데이트 하려면 다음을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-172">To update your NuGet Package Manager extension in WebMatrix 3:</span></span>

1. <span data-ttu-id="6b71d-173">WebMatrix 3 열기</span><span class="sxs-lookup"><span data-stu-id="6b71d-173">Open WebMatrix 3</span></span>
1. <span data-ttu-id="6b71d-174">리본에서 확장 아이콘을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-174">Click the Extensions icon in the ribbon</span></span>
1. <span data-ttu-id="6b71d-175">업데이트 탭 선택</span><span class="sxs-lookup"><span data-stu-id="6b71d-175">Select the Updates tab</span></span>
1. <span data-ttu-id="6b71d-176">NuGet 패키지 관리자를 2.5.0로 업데이트 하려면 클릭 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6b71d-176">Click to update NuGet Package Manager to 2.5.0</span></span>
1. <span data-ttu-id="6b71d-177">WebMatrix 3을 닫고 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-177">Close and restart WebMatrix 3</span></span>

<span data-ttu-id="6b71d-178">WebMatrix 용 nuget 패키지 관리자 확장의 첫 번째 릴리스입니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-178">This is the NuGet team's first release of the NuGet Package Manager extension for WebMatrix.</span></span>  <span data-ttu-id="6b71d-179">이 코드는 최근에 Microsoft에서 오픈 소스 NuGet 프로젝트에 참여 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-179">The code was recently contributed by Microsoft into the open-source NuGet project.</span></span> <span data-ttu-id="6b71d-180">이전에는 NuGet 통합이 WebMatrix에 내장 되었으며 WebMatrix에서 대역 외로 업데이트 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-180">Previously, the NuGet integration was built into WebMatrix, and it could not be updated out of band from WebMatrix.</span></span>  <span data-ttu-id="6b71d-181">이제 나머지 NuGet 클라이언트 도구와 함께이를 추가로 업데이트할 수 있는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-181">We now have the capability to further update it alongside the rest of NuGet's client tools.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="6b71d-182">버그 수정</span><span class="sxs-lookup"><span data-stu-id="6b71d-182">Bug Fixes</span></span>

<span data-ttu-id="6b71d-183">중요 한 버그 수정 사항 중 하나는 업데이트-패키지-다시 설치 명령에서 성능 향상입니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-183">One of the major bug fixes made was performance improvement in the  update-package -reinstall    command.</span></span>

<span data-ttu-id="6b71d-184">이러한 기능 외에도이 NuGet 릴리스에는 기타 많은 버그 수정이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-184">In addition to these features and the aforementioned performance fix, this release of NuGet also includes many other bug fixes.</span></span> <span data-ttu-id="6b71d-185">릴리스에서 해결 된 총 181 개의 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b71d-185">There were 181 total issues addressed in the release.</span></span> <span data-ttu-id="6b71d-186">NuGet 2.8에서 수정 된 작업 항목의 전체 목록은 [이 릴리스에 대 한 Nuget 문제 추적기](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all)를 확인 하세요.</span><span class="sxs-lookup"><span data-stu-id="6b71d-186">For a full list of the work items fixed in NuGet 2.8, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).</span></span>
