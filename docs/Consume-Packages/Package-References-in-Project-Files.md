---
title: "Visual Studio 프로젝트 파일의 NuGet PackageReference | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "NuGet 4.0+ 및 VS2017에서 지원되는 프로젝트 파일에 있는 NuGet PackageReference에 대한 세부 정보"
keywords: "NuGet 패키지 종속성, 패키지 참조, 프로젝트 파일, PackageReference, packages.config, project.json, VS2017, Visual Studio 2017, NuGet 4"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 275957c94e4a4bb45f359cd48816acf4f286ebad
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/05/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="318ab-104">프로젝트 파일의 패키지 참조(PackageReference)</span><span class="sxs-lookup"><span data-stu-id="318ab-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="318ab-105">`PackageReference` 노드를 사용하는 패키지 참조를 사용하면 별도 `packages.config` 또는 `project.json` 파일을 필요로 하지 않고 프로젝트 파일 내에서 직접 NuGet 종속성을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-105">Package references, using the `PackageReference` node, allow you to manage NuGet dependencies directly within project files, rather than needing a separate `packages.config` or `project.json` file.</span></span> <span data-ttu-id="318ab-106">이 메서드는 NuGet의 다른 측면에 영향을 주지 않습니다. 예를 들어 `NuGet.Config` 파일의 설정(패키지 소스 포함)은 [NuGet 동작 구성](Configuring-NuGet-Behavior.md)에 설명된 대로 계속 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-106">This method doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](Configuring-NuGet-Behavior.md).</span></span>

> [!Important]
> <span data-ttu-id="318ab-107">현재 패키지 참조는 Windows 10 빌드 15063(작성자 업데이트)를 대상으로 하는 .NET Core 프로젝트, .NET Standard 프로젝트 및 UWP 프로젝트용 Visual Studio 2017에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-107">At present, package references are supported in Visual Studio 2017 only, for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update).</span></span>

<span data-ttu-id="318ab-108">`PackageReference` 접근 방식을 사용하면 MSBuild 조건을 사용하여 대상 프레임워크, 구성, 플랫폼 또는 기타 그룹화당 패키지 참조를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-108">The `PackageReference` approach allows you to use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="318ab-109">종속성과 콘텐츠 흐름을 세밀하게 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-109">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="318ab-110">동작 및 [종속성 확인](Dependency-Resolution.md) 면에서 `project.json`을 사용하는 방법과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-110">In terms of behavior and [dependency resolution](Dependency-Resolution.md), it's the same as using `project.json`.</span></span>

<span data-ttu-id="318ab-111">프로젝트 파일에서 패키지 참조와 MSBuild의 통합에 대한 자세한 내용은 [NuGet 팩 및 MSBuild 대상으로 복원](../schema/msbuild-targets.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="318ab-111">For more details on the integration of MSBuild with package references in project files, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="318ab-112">PackageReference 추가</span><span class="sxs-lookup"><span data-stu-id="318ab-112">Adding a PackageReference</span></span>

<span data-ttu-id="318ab-113">다음 구문을 사용하여 프로젝트 파일에서 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />    
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="318ab-114">종속성 버전 제어</span><span class="sxs-lookup"><span data-stu-id="318ab-114">Controlling dependency version</span></span>

<span data-ttu-id="318ab-115">패키지의 버전을 지정하는 규칙은 `packages.config` 또는 `project.json`을 사용하는 경우와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-115">The convention for specifying the version of a package is the same as when using `packages.config` or `project.json`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="318ab-116">위의 예에서 3.6.0은 [패키지 버전 관리](../reference/package-versioning.md#version-ranges-and-wildcards)에 설명된 대로 가장 낮은 버전의 기본 설정으로 >=3.6.0인 버전을 가르킵니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="318ab-117">부동 버전</span><span class="sxs-lookup"><span data-stu-id="318ab-117">Floating Versions</span></span>

<span data-ttu-id="318ab-118">[부동 버전](../consume-packages/dependency-resolution.md#floating-versions)은 `PackageReference`에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="318ab-119">종속성 자산 제어</span><span class="sxs-lookup"><span data-stu-id="318ab-119">Controlling dependency assets</span></span>

<span data-ttu-id="318ab-120">종속성을 개발 도구로서 전적으로 사용하면 패키지를 사용하는 프로젝트에 노출하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="318ab-121">이 시나리오에서는 `PrivateAssets` 메타데이터를 사용하여 이 동작을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="318ab-122">다음 메타데이터 태그는 종속성 자산을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="318ab-123">태그</span><span class="sxs-lookup"><span data-stu-id="318ab-123">Tag</span></span> | <span data-ttu-id="318ab-124">설명</span><span class="sxs-lookup"><span data-stu-id="318ab-124">Description</span></span> | <span data-ttu-id="318ab-125">기본값</span><span class="sxs-lookup"><span data-stu-id="318ab-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="318ab-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="318ab-126">IncludeAssets</span></span> | <span data-ttu-id="318ab-127">이러한 자산을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-127">These assets will be consumed</span></span> | <span data-ttu-id="318ab-128">모두</span><span class="sxs-lookup"><span data-stu-id="318ab-128">all</span></span> |
| <span data-ttu-id="318ab-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="318ab-129">ExcludeAssets</span></span> | <span data-ttu-id="318ab-130">이러한 자산을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-130">These assets will not be consumed</span></span> | <span data-ttu-id="318ab-131">없음</span><span class="sxs-lookup"><span data-stu-id="318ab-131">none</span></span> | 
| <span data-ttu-id="318ab-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="318ab-132">PrivateAssets</span></span> | <span data-ttu-id="318ab-133">이러한 자산을 사용하지만 부모 프로젝트로 흐르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="318ab-134">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="318ab-134">contentfiles;analyzers;build</span></span> |


<span data-ttu-id="318ab-135">이러한 태그에 허용 가능한 값은 단독으로 표시해야 하는 `all` 및 `none`를 제외하고 세미콜론으로 구분된 값이 여러 개인 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="318ab-136">값</span><span class="sxs-lookup"><span data-stu-id="318ab-136">Value</span></span> | <span data-ttu-id="318ab-137">설명</span><span class="sxs-lookup"><span data-stu-id="318ab-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="318ab-138">compile</span><span class="sxs-lookup"><span data-stu-id="318ab-138">compile</span></span> | <span data-ttu-id="318ab-139">`lib` 폴더의 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="318ab-139">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="318ab-140">런타임(runtime)</span><span class="sxs-lookup"><span data-stu-id="318ab-140">runtime</span></span> | <span data-ttu-id="318ab-141">`runtime` 폴더의 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="318ab-141">Contents of the `runtime` folder</span></span> |
| <span data-ttu-id="318ab-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="318ab-142">contentFiles</span></span> | <span data-ttu-id="318ab-143">`contentfiles` 폴더의 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="318ab-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="318ab-144">빌드</span><span class="sxs-lookup"><span data-stu-id="318ab-144">build</span></span> | <span data-ttu-id="318ab-145">`build` 폴더의 prop 및 대상</span><span class="sxs-lookup"><span data-stu-id="318ab-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="318ab-146">분석기</span><span class="sxs-lookup"><span data-stu-id="318ab-146">analyzers</span></span> | <span data-ttu-id="318ab-147">.NET 분석기</span><span class="sxs-lookup"><span data-stu-id="318ab-147">.NET analyzers</span></span> |
| <span data-ttu-id="318ab-148">native</span><span class="sxs-lookup"><span data-stu-id="318ab-148">native</span></span> | <span data-ttu-id="318ab-149">`native` 폴더의 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="318ab-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="318ab-150">없음</span><span class="sxs-lookup"><span data-stu-id="318ab-150">none</span></span> | <span data-ttu-id="318ab-151">위의 항목을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-151">None of the above are used.</span></span> |
| <span data-ttu-id="318ab-152">모두</span><span class="sxs-lookup"><span data-stu-id="318ab-152">all</span></span> | <span data-ttu-id="318ab-153">위 모두 해당(`none` 제외)</span><span class="sxs-lookup"><span data-stu-id="318ab-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="318ab-154">다음 예제에서는 패키지의 콘텐츠 파일을 제외한 모든 항목을 프로젝트에서 사용할 수 있으며 콘텐츠 파일과 분석기를 제외한 모든 항목이 부모 프로젝트로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="318ab-155">`build`가 `PrivateAssets`에 포함되지 않기 때문에 대상 및 props은 부모 프로젝트로 전달되게 *됩니다*.</span><span class="sxs-lookup"><span data-stu-id="318ab-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="318ab-156">예를 들어 위의 참조가 AppLogger라는 NuGet 패키지를 빌드하는 프로젝트에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="318ab-157">프로젝트가 AppLogger를 사용할 수 있는 것처럼 AppLogger는 `Contoso.Utility.UsefulStuff`의 대상 및 props을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="318ab-158">PackageReference 조건 추가</span><span class="sxs-lookup"><span data-stu-id="318ab-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="318ab-159">조건이 모든 MSBuild 변수 또는 대상이나 props 파일에 정의된 변수를 사용할 수 있는 경우에 패키지가 포함되어 있는지를 제어하는 조건을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="318ab-160">그러나 현재는 `TargetFramework` 변수만이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="318ab-161">예를 들어 `net452`뿐만 아니라 `netstandard1.4`를 대상으로 지정했지만 `net452`에만 적용할 수 있는 종속성이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="318ab-162">이 경우에 불필요한 해당 종속성을 추가하는 패키지를 사용하는 `netstandard1.4` 프로젝트를 사용하지 않으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="318ab-163">이를 방지하려면 다음과 같이 `PackageReference`에 대한 조건을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="318ab-164">이 프로젝트를 사용하여 빌드한 패키지는 Newtonsoft.json이 `net452` 대상에서만 종속성으로 포함되어 있다고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![VS2017에서 PackageReference에 대한 조건을 적용한 결과](media/PackageReference-Condition.png)

<span data-ttu-id="318ab-166">조건은 `ItemGroup` 수준에도 적용될 수 있고 모든 자식 `PackageReference` 요소에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="318ab-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
