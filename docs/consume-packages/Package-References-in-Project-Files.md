---
title: NuGet PackageReference 형식(프로젝트 파일의 패키지 참조)
description: NuGet 4.0 이상, VS2017 및 .NET Core 2.0에서 지원되는 프로젝트 파일에 있는 NuGet PackageReference에 대한 세부 정보
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 48930701f1bb5f13718505b85b293f38d37d19fb
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508350"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="df497-103">프로젝트 파일의 패키지 참조(PackageReference)</span><span class="sxs-lookup"><span data-stu-id="df497-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="df497-104">`PackageReference` 노드를 사용하는 패키지 참조는 별도의 `packages.config` 파일이 아닌 프로젝트 파일 내에서 직접 NuGet 종속성을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="df497-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="df497-105">PackageReference를 사용하면 NuGet의 다른 측면이 영향을 받지 않습니다. 예를 들어 `NuGet.Config` 파일의 설정(패키지 소스 포함)은 [NuGet 동작 구성](configuring-nuget-behavior.md)에 설명된 대로 계속 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="df497-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="df497-106">또한 PackageReference를 사용하면 MSBuild 조건을 사용하여 대상 프레임워크, 구성, 플랫폼 또는 기타 그룹화당 패키지 참조를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df497-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="df497-107">종속성과 콘텐츠 흐름을 세밀하게 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df497-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="df497-108">(자세한 내용은 [MSBuild 대상으로서의 NuGet pack 및 restore](../reference/msbuild-targets.md)를 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="df497-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="df497-109">기본적으로 PackageReference는 Windows 10 빌드 15063(크리에이터스 업데이트) 이상을 대상으로 하는 .NET Core 프로젝트, .NET Standard 프로젝트 및 UWP 프로젝트에 사용됩니다(C++ UWP 프로젝트는 제외).</span><span class="sxs-lookup"><span data-stu-id="df497-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="df497-110">.NET 전체 프레임워크 프로젝트는 PackageReference를 지원하지만 현재 기본값은 `packages.config`입니다.</span><span class="sxs-lookup"><span data-stu-id="df497-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="df497-111">PackageReference를 사용하려면 종속성을 `packages.config`에서 프로젝트 파일로 마이그레이션한 후 packages.config를 제거하세요.</span><span class="sxs-lookup"><span data-stu-id="df497-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="df497-112">PackageReference 추가</span><span class="sxs-lookup"><span data-stu-id="df497-112">Adding a PackageReference</span></span>

<span data-ttu-id="df497-113">다음 구문을 사용하여 프로젝트 파일에서 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="df497-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="df497-114">종속성 버전 제어</span><span class="sxs-lookup"><span data-stu-id="df497-114">Controlling dependency version</span></span>

<span data-ttu-id="df497-115">패키지의 버전을 지정하는 규칙은 `packages.config`를 사용하는 경우와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="df497-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="df497-116">위의 예에서 3.6.0은 [패키지 버전 관리](../reference/package-versioning.md#version-ranges-and-wildcards)에 설명된 대로 가장 낮은 버전의 기본 설정으로 >=3.6.0인 버전을 가르킵니다.</span><span class="sxs-lookup"><span data-stu-id="df497-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="df497-117">PackageReferences가 없는 프로젝트에 대해 PackageReference 사용</span><span class="sxs-lookup"><span data-stu-id="df497-117">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="df497-118">고급: 프로젝트에 설치된 패키지가 없지만(프로젝트 파일에 PackageReferences가 없고 packages.config 파일이 없음) 프로젝트를 PackageReference 스타일로 복원하려는 경우 프로젝트 속성 RestoreProjectStyle을 프로젝트 파일의 PackageReference로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df497-118">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="df497-119">PackageReference 스타일인 프로젝트(기존 csproj 또는 SDK 스타일 프로젝트)를 참조하는 경우에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df497-119">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="df497-120">이렇게 하면 해당 프로젝트가 참조하는 패키지는 프로젝트에서 "전이적으로" 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="df497-120">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="df497-121">부동 버전</span><span class="sxs-lookup"><span data-stu-id="df497-121">Floating Versions</span></span>

<span data-ttu-id="df497-122">[부동 버전](../consume-packages/dependency-resolution.md#floating-versions)은 `PackageReference`에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="df497-122">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="df497-123">종속성 자산 제어</span><span class="sxs-lookup"><span data-stu-id="df497-123">Controlling dependency assets</span></span>

<span data-ttu-id="df497-124">종속성을 개발 도구로서 전적으로 사용하면 패키지를 사용하는 프로젝트에 노출하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df497-124">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="df497-125">이 시나리오에서는 `PrivateAssets` 메타데이터를 사용하여 이 동작을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df497-125">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="df497-126">다음 메타데이터 태그는 종속성 자산을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="df497-126">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="df497-127">태그</span><span class="sxs-lookup"><span data-stu-id="df497-127">Tag</span></span> | <span data-ttu-id="df497-128">설명</span><span class="sxs-lookup"><span data-stu-id="df497-128">Description</span></span> | <span data-ttu-id="df497-129">기본값</span><span class="sxs-lookup"><span data-stu-id="df497-129">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="df497-130">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="df497-130">IncludeAssets</span></span> | <span data-ttu-id="df497-131">이러한 자산을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="df497-131">These assets will be consumed</span></span> | <span data-ttu-id="df497-132">모두</span><span class="sxs-lookup"><span data-stu-id="df497-132">all</span></span> |
| <span data-ttu-id="df497-133">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="df497-133">ExcludeAssets</span></span> | <span data-ttu-id="df497-134">이러한 자산을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df497-134">These assets will not be consumed</span></span> | <span data-ttu-id="df497-135">없음</span><span class="sxs-lookup"><span data-stu-id="df497-135">none</span></span> |
| <span data-ttu-id="df497-136">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="df497-136">PrivateAssets</span></span> | <span data-ttu-id="df497-137">이러한 자산을 사용하지만 부모 프로젝트로 흐르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df497-137">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="df497-138">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="df497-138">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="df497-139">이러한 태그에 허용 가능한 값은 단독으로 표시해야 하는 `all` 및 `none`를 제외하고 세미콜론으로 구분된 값이 여러 개인 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="df497-139">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="df497-140">값</span><span class="sxs-lookup"><span data-stu-id="df497-140">Value</span></span> | <span data-ttu-id="df497-141">설명</span><span class="sxs-lookup"><span data-stu-id="df497-141">Description</span></span> |
| --- | ---
| <span data-ttu-id="df497-142">compile</span><span class="sxs-lookup"><span data-stu-id="df497-142">compile</span></span> | <span data-ttu-id="df497-143">`lib` 폴더의 콘텐츠이며 프로젝트에서 폴더 내의 어셈블리를 컴파일할 수 있는지 여부 제어</span><span class="sxs-lookup"><span data-stu-id="df497-143">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="df497-144">런타임(runtime)</span><span class="sxs-lookup"><span data-stu-id="df497-144">runtime</span></span> | <span data-ttu-id="df497-145">`lib` 및 `runtimes` 폴더의 콘텐츠이며 이러한 어셈블리가 빌드 출력 디렉터리에 복사되는지 여부 제어</span><span class="sxs-lookup"><span data-stu-id="df497-145">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="df497-146">contentFiles</span><span class="sxs-lookup"><span data-stu-id="df497-146">contentFiles</span></span> | <span data-ttu-id="df497-147">`contentfiles` 폴더의 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="df497-147">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="df497-148">빌드</span><span class="sxs-lookup"><span data-stu-id="df497-148">build</span></span> | <span data-ttu-id="df497-149">`build` 폴더의 prop 및 대상</span><span class="sxs-lookup"><span data-stu-id="df497-149">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="df497-150">분석기</span><span class="sxs-lookup"><span data-stu-id="df497-150">analyzers</span></span> | <span data-ttu-id="df497-151">.NET 분석기</span><span class="sxs-lookup"><span data-stu-id="df497-151">.NET analyzers</span></span> |
| <span data-ttu-id="df497-152">native</span><span class="sxs-lookup"><span data-stu-id="df497-152">native</span></span> | <span data-ttu-id="df497-153">`native` 폴더의 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="df497-153">Contents of the `native` folder</span></span> |
| <span data-ttu-id="df497-154">없음</span><span class="sxs-lookup"><span data-stu-id="df497-154">none</span></span> | <span data-ttu-id="df497-155">위의 항목을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="df497-155">None of the above are used.</span></span> |
| <span data-ttu-id="df497-156">모두</span><span class="sxs-lookup"><span data-stu-id="df497-156">all</span></span> | <span data-ttu-id="df497-157">위 모두 해당(`none` 제외)</span><span class="sxs-lookup"><span data-stu-id="df497-157">All of the above (except `none`)</span></span> |

<span data-ttu-id="df497-158">다음 예제에서는 패키지의 콘텐츠 파일을 제외한 모든 항목을 프로젝트에서 사용할 수 있으며 콘텐츠 파일과 분석기를 제외한 모든 항목이 부모 프로젝트로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="df497-158">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="df497-159">`build`가 `PrivateAssets`에 포함되지 않기 때문에 대상 및 props은 부모 프로젝트로 전달되게 *됩니다*.</span><span class="sxs-lookup"><span data-stu-id="df497-159">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="df497-160">예를 들어 위의 참조가 AppLogger라는 NuGet 패키지를 빌드하는 프로젝트에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="df497-160">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="df497-161">프로젝트가 AppLogger를 사용할 수 있는 것처럼 AppLogger는 `Contoso.Utility.UsefulStuff`의 대상 및 props을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df497-161">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="df497-162">PackageReference 조건 추가</span><span class="sxs-lookup"><span data-stu-id="df497-162">Adding a PackageReference condition</span></span>

<span data-ttu-id="df497-163">조건이 모든 MSBuild 변수 또는 대상이나 props 파일에 정의된 변수를 사용할 수 있는 경우에 패키지가 포함되어 있는지를 제어하는 조건을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="df497-163">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="df497-164">그러나 현재는 `TargetFramework` 변수만이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="df497-164">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="df497-165">예를 들어 `net452`뿐만 아니라 `netstandard1.4`를 대상으로 지정했지만 `net452`에만 적용할 수 있는 종속성이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="df497-165">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="df497-166">이 경우에 불필요한 해당 종속성을 추가하는 패키지를 사용하는 `netstandard1.4` 프로젝트를 사용하지 않으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="df497-166">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="df497-167">이를 방지하려면 다음과 같이 `PackageReference`에 대한 조건을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="df497-167">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="df497-168">이 프로젝트를 사용하여 빌드한 패키지는 Newtonsoft.Json이 `net452` 대상에서만 종속성으로 포함되어 있다고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="df497-168">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![VS2017에서 PackageReference에 대한 조건을 적용한 결과](media/PackageReference-Condition.png)

<span data-ttu-id="df497-170">조건은 `ItemGroup` 수준에도 적용될 수 있고 모든 자식 `PackageReference` 요소에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="df497-170">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
