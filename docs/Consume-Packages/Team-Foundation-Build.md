---
title: "Team Foundation 빌드를 사용하여 NuGet 패키지 복원 연습 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3113cccd-35f7-4980-8a6e-fc06556b5064
description: "Team Foundation Build(TFS 및 Visual Studio Team Services)에서 NuGet 패키지를 복원하는 방법의 연습입니다."
keywords: "NuGet 패키지 복원, NuGet 및 TFS, NuGet 및 VSTS, NuGet 빌드 시스템, Team Foundation 빌드, MSBuild 프로젝트 사용자 지정, 클라우드 빌드, 연속 통합"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4be1bb83549958897a15d690439cac073c9683d1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="setting-up-package-restore-with-team-foundation-build"></a><span data-ttu-id="324ba-104">Team Foundation 빌드를 사용하여 패키지 복원 설정</span><span class="sxs-lookup"><span data-stu-id="324ba-104">Setting up package restore with Team Foundation Build</span></span>

> <span data-ttu-id="324ba-105">적용 대상:</span><span class="sxs-lookup"><span data-stu-id="324ba-105">Applies To:</span></span>
>  - <span data-ttu-id="324ba-106">TFS의 모든 버전에서 실행되는 MSBuild 프로젝트 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="324ba-106">Custom MSBuild projects running on any version of TFS</span></span>
>  - <span data-ttu-id="324ba-107">Team Foundation Server 2012 이전</span><span class="sxs-lookup"><span data-stu-id="324ba-107">Team Foundation Server 2012 or earlier</span></span>
>  - <span data-ttu-id="324ba-108">TFS 2013 이상으로 마이그레이션된 Team Foundation 빌드 프로세스 템플릿 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="324ba-108">Custom Team Foundation Build Process Templates migrated to TFS 2013 or later</span></span>
>  - <span data-ttu-id="324ba-109">Nuget 복원 기능이 제거된 프로세스 템플릿 빌드</span><span class="sxs-lookup"><span data-stu-id="324ba-109">Build Process Templates With Nuget Restore functionality removed</span></span>
>
> <span data-ttu-id="324ba-110">해당 빌드 프로세스 템플릿에서 Visual Studio Team Services 또는 온-프레미스 Team Foundation Server 2013을 사용하는 경우 빌드 프로세스의 일부로 자동 패키지가 복원됩니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-110">If you're using Visual Studio Team Services or on-premises Team Foundation Server 2013 with its build process templates, Automatic Package Restore happens as part of the build process.</span></span>

<span data-ttu-id="324ba-111">이 섹션은 [Team Foundation 빌드](http://msdn.microsoft.com/library/ms181710(v=VS.90).aspx)의 일환으로 [git](http://en.wikipedia.org/wiki/Git_(software)) 및 [TF 버전 제어](http://msdn.microsoft.com/library/ms181237(v=vs.120).aspx)에서 패키지를 복원하는 방법에 대한 자세한 연습을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-111">This section will provide a detailed walkthrough on how to restore packages as part of the [Team Foundation Build](http://msdn.microsoft.com/library/ms181710(v=VS.90).aspx) both, for [git](http://en.wikipedia.org/wiki/Git_(software)) as well as [TF Version Control](http://msdn.microsoft.com/library/ms181237(v=vs.120).aspx).</span></span>

<span data-ttu-id="324ba-112">[Team Foundation Service](http://tfs.visualstudio.com/)를 사용하는 시나리오에 이 연습이 지정되지만 개념은 다른 버전 제어에도 적용되고 시스템을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-112">Although this walkthrough is specific for the scenario of using [Team Foundation Service](http://tfs.visualstudio.com/), the concepts also apply to other version control- and build systems.</span></span>

## <a name="the-general-approach"></a><span data-ttu-id="324ba-113">일반적인 접근 방법</span><span class="sxs-lookup"><span data-stu-id="324ba-113">The general approach</span></span>

<span data-ttu-id="324ba-114">NuGet을 사용하는 경우의 이점은 버전 제어 시스템에 대한 이진 파일을 검사하지 않도록 방지하기 위해 사용할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-114">An advantage of using NuGet is that you can use it to avoid checking in binaries to your version control system.</span></span>

<span data-ttu-id="324ba-115">개발자가 로컬로 작업을 시작하기 전에 전체 기록을 포함하여 전체 리포지토리를 복제해야 하기 때문에 Git과 같은 [분산 버전 제어](http://en.wikipedia.org/wiki/Distributed_revision_control) 시스템을 사용 중인 경우에 특히 흥미롭습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-115">This is especially interesting if you are using a [distributed version control](http://en.wikipedia.org/wiki/Distributed_revision_control) system like git because developers need to clone the entire repository, including the full history, before they can start working locally.</span></span> <span data-ttu-id="324ba-116">이진 파일을 체크 인하면 이진 파일이 델타 압축 없이 일반적으로 저장되므로 상당한 리포지토리 블로트가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-116">Checking in binaries can cause significant repository bloat as binary files are typically stored without delta compression.</span></span>

<span data-ttu-id="324ba-117">NuGet은 오랜 시간 동안 빌드의 일부로 [패키지를 복원](../consume-packages/package-restore.md)하도록 지원했습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-117">NuGet has supported [restoring packages](../consume-packages/package-restore.md) as part of the build for a long time now.</span></span> <span data-ttu-id="324ba-118">프로젝트를 빌드하는 동안 NuGet이 패키지를 복원했기 때문에 이전 구현은 빌드 프로세스 확장하려는 패키지에서 '닭이 먼저냐, 달걀이 먼저냐'와 같은 문제가 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-118">The previous implementation had a chicken-and-egg problem for packages that want to extend the build process because NuGet restored packages while building the project.</span></span> <span data-ttu-id="324ba-119">그러나 MSBuild는 빌드 중에 빌드를 확장할 수 없습니다. 따라서 MSBuild에 문제가 있다고 주장할 수 있지만 근본적인 문제라고 생각합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-119">However, MSBuild doesn't allow extending the build during the build; one could argue that this an issue in MSBuild but I would argue that this is an inherent problem.</span></span> <span data-ttu-id="324ba-120">확장해야 하는 측면에 따라 패키지를 복원할 때에는 등록하기가 너무 늦을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-120">Depending on which aspect you need to extend it might be too late to register by the time your package is restored.</span></span>

<span data-ttu-id="324ba-121">이 문제를 수정하려면 빌드 프로세스에서 첫 번째 단계로 패키지를 복원했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-121">The cure to this problem is making sure that packages are restored as the first step in the build process.</span></span> <span data-ttu-id="324ba-122">NuGet 2.7 이상에서는 간소화된 명령줄을 통해 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-122">NuGet 2.7+ makes this easy via a simplified command line:</span></span>

```
nuget restore path\to\solution.sln
```

<span data-ttu-id="324ba-123">코드를 빌드하기 전에 프로세스 복원 패키지를 빌드하는 경우 `.targets` 파일을 체크 인할 필요가 없습니다</span><span class="sxs-lookup"><span data-stu-id="324ba-123">When your build process restores packages before building the code, you don't need to check-in `.targets` files</span></span>

> [!Note]
> <span data-ttu-id="324ba-124">Visual Studio에서 로드를 허용하도록 패키지를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-124">Packages must be authored to allow loading in Visual Studio.</span></span> <span data-ttu-id="324ba-125">그렇지 않으면 다른 개발자가 먼저 패키지를 복원하지 않고도 쉽게 솔루션을 열 수 있도록 `.targets` 파일을 체크 인하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-125">Otherwise, you may still want to check in `.targets` files so that other developers can simply open the solution without having to restore packages first.</span></span>

<span data-ttu-id="324ba-126">다음 데모 프로젝트는 `packages` 폴더 및 `.targets` 파일을 체크 인할 필요가 없는 방식으로 빌드를 설정하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-126">The following demo project shows how to set up the build in such a way that the `packages` folders and `.targets` files don't need to be checked-in.</span></span> <span data-ttu-id="324ba-127">또한 이 샘플 프로젝트에서 Team Foundation Service에 자동화된 빌드를 설정하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-127">It also shows how to set up an automated build on the Team Foundation Service for this sample project.</span></span>

## <a name="repository-structure"></a><span data-ttu-id="324ba-128">리포지토리 구조</span><span class="sxs-lookup"><span data-stu-id="324ba-128">Repository structure</span></span>

<span data-ttu-id="324ba-129">이 데모 프로젝트는 Bing을 쿼리하는 데 명령줄 인수를 사용하는 간단한 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-129">Our demo project is a simple command line tool that uses the command line argument to query Bing.</span></span> <span data-ttu-id="324ba-130">.NET Framework 4를 대상으로 지정하고 [BCL 패키지](http://www.nuget.org/profiles/dotnetframework/)를 사용합니다([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async) 및 [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span><span class="sxs-lookup"><span data-stu-id="324ba-130">It targets the .NET Framework 4 and uses many of the [BCL packages](http://www.nuget.org/profiles/dotnetframework/) ([Microsoft.Net.Http](http://www.nuget.org/packages/Microsoft.Net.Http), [Microsoft.Bcl](http://www.nuget.org/packages/Microsoft.Bcl), [Microsoft.Bcl.Async](http://www.nuget.org/packages/Microsoft.Bcl.Async), and [Microsoft.Bcl.Build](http://www.nuget.org/packages/Microsoft.Bcl.Build)).</span></span>

<span data-ttu-id="324ba-131">리포지토리의 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-131">The structure of the repository looks as follows:</span></span>

    <Project>
        │   .gitignore
        │   .tfignore
        │   build.proj
        │
        ├───src
        │   │   BingSearcher.sln
        │   │
        │   └───BingSearcher
        │       │   App.config
        │       │   BingSearcher.csproj
        │       │   packages.config
        │       │   Program.cs
        │       │
        │       └───Properties
        │               AssemblyInfo.cs
        │
        └───tools
            └───NuGet
                    nuget.exe

<span data-ttu-id="324ba-132">`packages` 폴더나 `.targets` 파일을 아직 체크 인하지 않은 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-132">You can see that we haven't checked-in the `packages` folder nor any `.targets` files.</span></span>

<span data-ttu-id="324ba-133">그러나 빌드 중에 필요한 경우 `nuget.exe`을 체크 인했습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-133">We have, however, checked-in the `nuget.exe` as it's needed during the build.</span></span> <span data-ttu-id="324ba-134">다음은 공유 `tools` 폴더 아래에서 체크 인한 규칙을 광범위하게 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-134">Following widely used conventions we've checked it in under a shared `tools` folder.</span></span>

<span data-ttu-id="324ba-135">소스 코드는 `src` 폴더 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-135">The source code is under the `src` folder.</span></span> <span data-ttu-id="324ba-136">데모에서 단일 솔루션만을 사용하지만 이 폴더에 하나 이상의 솔루션이 포함되어 있다고 쉽게 상상할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-136">Although our demo only uses a single solution, you can easily imagine that this folder contains more than one solution.</span></span>

### <a name="ignore-files"></a><span data-ttu-id="324ba-137">파일 무시</span><span class="sxs-lookup"><span data-stu-id="324ba-137">Ignore files</span></span>

> [!Note]
> <span data-ttu-id="324ba-138">현재 클라이언트를 버전 제어에 대한 `packages` 폴더에 추가하는 [NuGet 클라이언트의 알려진 버그](https://nuget.codeplex.com/workitem/4072)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-138">There is currently a [known bug in the NuGet client](https://nuget.codeplex.com/workitem/4072) that causes the client to still add the `packages` folder to version control.</span></span> <span data-ttu-id="324ba-139">해결 방법은 소스 제어 통합을 사용하지 않도록 설정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-139">A workaround is to disable the source control integration.</span></span> <span data-ttu-id="324ba-140">이를 수행하려면 솔루션에 병렬되는 `.nuget` 폴더에 `Nuget.Config ` 파일이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-140">In order to do that, you'll need a `Nuget.Config ` file in the  `.nuget` folder that is parallel to your solution.</span></span> <span data-ttu-id="324ba-141">이 폴더가 아직 존재하지 않으면 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-141">If this folder doesn't exist yet, you'll need to create it.</span></span> <span data-ttu-id="324ba-142">[`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md)에서 다음 콘텐츠를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-142">In [`Nuget.Config`](../consume-packages/configuring-nuget-behavior.md), add the following content:</span></span>

```xml
<configuration>
    <solution>
        <add key="disableSourceControlIntegration" value="true" />
    </solution>
</configuration>
```


<span data-ttu-id="324ba-143">**패키지** 폴더를 체크 인하지 않으려는 버전 제어에 통신하기 위해 TF 버전 제어(`.tfignore`)뿐만 아니라 두 Git(`.gitignore`)에 무시 파일을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-143">In order to communicate to the version control that we don’t intent to check-in the **packages** folders, we've also added ignore files for both git (`.gitignore`) as well as TF version control (`.tfignore`).</span></span> <span data-ttu-id="324ba-144">이러한 파일은 체크 인하지 않으려는 파일의 패턴을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-144">These files describes patterns of files you don't want to check-in.</span></span>

<span data-ttu-id="324ba-145">`.gitignore` 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-145">The `.gitignore` file looks as follows:</span></span>

    syntax: glob
    *.user
    *.suo
    bin
    obj
    packages

<span data-ttu-id="324ba-146">`.gitignore` 파일은 [매우 강력](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-146">The `.gitignore` file is [quite powerful](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html).</span></span> <span data-ttu-id="324ba-147">예를 들어, 일반적으로 `packages` 폴더의 콘텐츠를 체크 인하지 않지만 `.targets` 파일을 체크인하는 이전 지침으로 이동하려는 경우 대신 다음 규칙이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-147">For example, if you want to generally not check-in the contents of the `packages` folder but want to go with previous guidance of checking in the `.targets` files you could have the following rule instead:</span></span>

    packages
    !packages/**/*.targets

<span data-ttu-id="324ba-148">이렇게 하면 모든 `packages` 폴더를 제외하지만 포함된 모든 `.targets` 파일을 다시 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-148">This will exclude all `packages` folders but will re-include all contained `.targets` files.</span></span> <span data-ttu-id="324ba-149">Visual Studio 개발자의 요구를 위해 특별히 조정된 `.gitignore` 파일의 템플릿을 [여기](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-149">By the way, you can find a template for `.gitignore` files that is specifically tailored for the needs of Visual Studio developers [here](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>

<span data-ttu-id="324ba-150">TF 버전 제어는 [.tfignore](http://msdn.microsoft.com/library/ms245454.aspx) 파일을 통해 매우 유사한 메커니즘을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-150">TF version control supports a very similar mechanism via the [.tfignore](http://msdn.microsoft.com/library/ms245454.aspx) file.</span></span> <span data-ttu-id="324ba-151">구문은 거의 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-151">The syntax is virtually the same:</span></span>

    *.user
    *.suo
    bin
    obj
    packages

## <a name="buildproj"></a><span data-ttu-id="324ba-152">build.proj</span><span class="sxs-lookup"><span data-stu-id="324ba-152">build.proj</span></span>

<span data-ttu-id="324ba-153">이 데모에서는 빌드 프로세스 매우 단순합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-153">For our demo, we keep the build process fairly simple.</span></span> <span data-ttu-id="324ba-154">솔루션을 빌드하기 전에 패키지가 복원되었는지 확인하는 동안 모든 솔루션을 빌드하는 MSBuild 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-154">We'll create an MSBuild project that builds all solutions while making sure that packages are restored before building the solutions.</span></span>

<span data-ttu-id="324ba-155">이 프로젝트에는 기존의 세 가지 대상인 `Clean`, `Build` 및 `Rebuild`뿐만 아니라 새 대상 `RestorePackages`가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-155">This project will have the three conventional targets `Clean`, `Build` and `Rebuild` as well as a new target `RestorePackages`.</span></span>

- <span data-ttu-id="324ba-156">`Build` 및 `Rebuild` 대상은 둘 다 `RestorePackages`에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-156">The `Build` and `Rebuild` targets both depend on `RestorePackages`.</span></span> <span data-ttu-id="324ba-157">이렇게 하면 `Build` 및 `Rebuild` 둘 다를 실행하고 복원되는 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-157">This makes sure that you can both run `Build` and `Rebuild` and rely on packages being restored.</span></span>
- <span data-ttu-id="324ba-158">`Clean`, `Build` 및 `Rebuild`는 모든 솔루션 파일에서 해당하는 MSBuild 대상을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-158">`Clean`, `Build` and `Rebuild` invoke the corresponding MSBuild target on all solution files.</span></span>
- <span data-ttu-id="324ba-159">`RestorePackages` 대상은 각 솔루션 파일의 `nuget.exe`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-159">The `RestorePackages` target invokes `nuget.exe` for each solution file.</span></span> <span data-ttu-id="324ba-160">[MSBuild 일괄 처리 기능](http://msdn.microsoft.com/library/ms171473.aspx)을 사용하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-160">This is accomplished by using [MSBuild's batching functionality](http://msdn.microsoft.com/library/ms171473.aspx).</span></span>

<span data-ttu-id="324ba-161">결과는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-161">The result looks as follows:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="4.0"
            DefaultTargets="Build"
            xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
    <OutDir Condition=" '$(OutDir)'=='' ">$(MSBuildThisFileDirectory)bin\</OutDir>
    <Configuration Condition=" '$(Configuration)'=='' ">Release</Configuration>
    <SourceHome Condition=" '$(SourceHome)'=='' ">$(MSBuildThisFileDirectory)src\</SourceHome>
    <ToolsHome Condition=" '$(ToolsHome)'=='' ">$(MSBuildThisFileDirectory)tools\</ToolsHome>
    </PropertyGroup>

    <ItemGroup>
    <Solution Include="$(SourceHome)*.sln">
        <AdditionalProperties>OutDir=$(OutDir);Configuration=$(Configuration)</AdditionalProperties>
    </Solution>
    </ItemGroup>

    <Target Name="RestorePackages">
    <Exec Command="&quot;$(ToolsHome)NuGet\nuget.exe&quot; restore &quot;%(Solution.Identity)&quot;" />
    </Target>

    <Target Name="Clean">
    <MSBuild Targets="Clean"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Build" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Build"
                Projects="@(Solution)" />
    </Target>

    <Target Name="Rebuild" DependsOnTargets="RestorePackages">
    <MSBuild Targets="Rebuild"
                Projects="@(Solution)" />
    </Target>
</Project>
```

## <a name="configuring-team-build"></a><span data-ttu-id="324ba-162">팀 빌드 구성</span><span class="sxs-lookup"><span data-stu-id="324ba-162">Configuring Team Build</span></span>

<span data-ttu-id="324ba-163">팀 빌드에서는 다양한 프로세스 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-163">Team Build offers various process templates.</span></span> <span data-ttu-id="324ba-164">이 데모에서는 Team Foundation Service를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-164">For this demonstration, we're using the Team Foundation Service.</span></span> <span data-ttu-id="324ba-165">하지만 TFS의 온-프레미스 설치는 매우 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-165">On-premises installations of TFS will be very similar though.</span></span>

<span data-ttu-id="324ba-166">Git 및 TF 버전 제어에는 다른 팀 빌드 템플릿이 있으므로 다음 단계는 사용하는 버전 제어 시스템에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-166">Git and TF Version Control have different Team Build templates, so the following steps will vary depending on which version control system you are using.</span></span> <span data-ttu-id="324ba-167">두 경우에 빌드하려는 프로젝트로 build.proj를 선택하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-167">In both cases, all you need is selecting the build.proj as the project you want to build.</span></span>

<span data-ttu-id="324ba-168">먼저 Git에 대한 프로세스 템플릿을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-168">First, let's look at the process template for git.</span></span> <span data-ttu-id="324ba-169">Git 기반 템플릿에서 `Solution to build` 속성을 통해 빌드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-169">In the git based template the build is selected via the property `Solution to build`:</span></span>

![Git의 빌드 프로세스](media/PackageRestoreTeamBuildGit.png)

<span data-ttu-id="324ba-171">이 속성은 리포지토리에 위치합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-171">Please note that this property is a location in your repository.</span></span> <span data-ttu-id="324ba-172">`build.proj`가 루트에 있으므로 `build.proj`를 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-172">Since our `build.proj` is in the root, we simply used `build.proj`.</span></span> <span data-ttu-id="324ba-173">`tools`이라는 폴더 아래에서 빌드 파일을 배치하는 경우 값은 `tools\build.proj`입니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-173">If you place the build file under a folder called `tools`, the value would be `tools\build.proj`.</span></span>

<span data-ttu-id="324ba-174">TF 버전 컨트롤 템플릿에서 `Projects` 속성을 통해 프로젝트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-174">In the TF version control template the project is selected via the property `Projects`:</span></span>

![TFVC의 빌드 프로세스](media/PackageRestoreTeamBuildTFVC.png)

<span data-ttu-id="324ba-176">Git 기반 템플릿과 달리 TF 버전 제어는 선택기(세 개의 점이 있는 오른쪽의 단추)를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-176">In contrast to the git based template the TF version control supports pickers (the button on the right hand side with the three dots).</span></span> <span data-ttu-id="324ba-177">따라서 입력 오류를 방지하기 위해 프로젝트를 선택하는 데 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="324ba-177">So in order to avoid any typing errors we suggest you use them to select the project.</span></span>