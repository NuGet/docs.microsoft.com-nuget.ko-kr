---
title: NuGet PackageReference 형식(프로젝트 파일의 패키지 참조)
description: NuGet 4.0 이상, VS2017 및 .NET Core 2.0에서 지원되는 프로젝트 파일에 있는 NuGet PackageReference에 대한 세부 정보
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428506"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="4711c-103">프로젝트 파일의 패키지 참조(PackageReference)</span><span class="sxs-lookup"><span data-stu-id="4711c-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="4711c-104">`PackageReference` 노드를 사용하는 패키지 참조는 별도의 `packages.config` 파일이 아닌 프로젝트 파일 내에서 직접 NuGet 종속성을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="4711c-105">PackageReference를 사용하면 NuGet의 다른 측면이 영향을 받지 않습니다. 예를 들어 `NuGet.config` 파일의 설정(패키지 소스 포함)은 [일반적인 NuGet 구성](configuring-nuget-behavior.md)에 설명된 대로 계속 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="4711c-106">또한 PackageReference를 사용하면 MSBuild 조건을 사용하여 대상 프레임워크 또는 기타 그룹화당 패키지 참조를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="4711c-107">종속성과 콘텐츠 흐름을 세밀하게 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="4711c-108">(자세한 내용은 [MSBuild 대상으로서의 NuGet pack 및 restore](../reference/msbuild-targets.md)를 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="4711c-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="4711c-109">프로젝트 형식 지원</span><span class="sxs-lookup"><span data-stu-id="4711c-109">Project type support</span></span>

<span data-ttu-id="4711c-110">기본적으로 PackageReference는 Windows 10 빌드 15063(크리에이터스 업데이트) 이상을 대상으로 하는 .NET Core 프로젝트, .NET Standard 프로젝트 및 UWP 프로젝트에 사용됩니다(C++ UWP 프로젝트는 제외).</span><span class="sxs-lookup"><span data-stu-id="4711c-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="4711c-111">.NET Framework 프로젝트는 PackageReference를 지원하지만 현재 기본값은 `packages.config`입니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="4711c-112">PackageReference를 사용하려면 종속성을 `packages.config`에서 프로젝트 파일로 [마이그레이션](../consume-packages/migrate-packages-config-to-package-reference.md)한 후 packages.config를 제거하세요.</span><span class="sxs-lookup"><span data-stu-id="4711c-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="4711c-113">전체 .NET Framework를 대상으로 하는 ASP.NET 앱은 PackageReference에 대한 [제한적 지원](https://github.com/NuGet/Home/issues/5877)만 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="4711c-114">C++ 및 JavaScript 프로젝트 형식은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="4711c-115">PackageReference 추가</span><span class="sxs-lookup"><span data-stu-id="4711c-115">Adding a PackageReference</span></span>

<span data-ttu-id="4711c-116">다음 구문을 사용하여 프로젝트 파일에서 종속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="4711c-117">종속성 버전 제어</span><span class="sxs-lookup"><span data-stu-id="4711c-117">Controlling dependency version</span></span>

<span data-ttu-id="4711c-118">패키지의 버전을 지정하는 규칙은 `packages.config`를 사용하는 경우와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="4711c-119">위의 예에서 3.6.0은 [패키지 버전 관리](../concepts/package-versioning.md#version-ranges)에 설명된 대로 가장 낮은 버전의 기본 설정으로 >=3.6.0인 버전을 가르킵니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="4711c-120">PackageReferences가 없는 프로젝트에 대해 PackageReference 사용</span><span class="sxs-lookup"><span data-stu-id="4711c-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="4711c-121">고급: 프로젝트에 설치된 패키지가 없지만(프로젝트 파일에 PackageReferences가 없고 packages.config 파일이 없음) 프로젝트를 PackageReference 스타일로 복원하려는 경우 프로젝트 속성 RestoreProjectStyle을 프로젝트 파일의 PackageReference로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="4711c-122">PackageReference 스타일인 프로젝트(기존 csproj 또는 SDK 스타일 프로젝트)를 참조하는 경우에 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="4711c-123">이렇게 하면 해당 프로젝트가 참조하는 패키지는 프로젝트에서 "전이적으로" 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="4711c-124">PackageReference 및 소스</span><span class="sxs-lookup"><span data-stu-id="4711c-124">PackageReference and sources</span></span>

<span data-ttu-id="4711c-125">PackageReference 프로젝트에서 전이 종속성 버전은 복원 시간에 확인됩니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="4711c-126">따라서 PackageReference 프로젝트에서 모든 복원에 대해 모든 소스를 사용할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="4711c-127">부동 버전</span><span class="sxs-lookup"><span data-stu-id="4711c-127">Floating Versions</span></span>

<span data-ttu-id="4711c-128">[부동 버전](../concepts/dependency-resolution.md#floating-versions)은 `PackageReference`에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="4711c-129">종속성 자산 제어</span><span class="sxs-lookup"><span data-stu-id="4711c-129">Controlling dependency assets</span></span>

<span data-ttu-id="4711c-130">종속성을 개발 도구로서 전적으로 사용하면 패키지를 사용하는 프로젝트에 노출하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="4711c-131">이 시나리오에서는 `PrivateAssets` 메타데이터를 사용하여 이 동작을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="4711c-132">다음 메타데이터 태그는 종속성 자산을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="4711c-133">태그</span><span class="sxs-lookup"><span data-stu-id="4711c-133">Tag</span></span> | <span data-ttu-id="4711c-134">설명</span><span class="sxs-lookup"><span data-stu-id="4711c-134">Description</span></span> | <span data-ttu-id="4711c-135">기본값</span><span class="sxs-lookup"><span data-stu-id="4711c-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4711c-136">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="4711c-136">IncludeAssets</span></span> | <span data-ttu-id="4711c-137">이러한 자산을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-137">These assets will be consumed</span></span> | <span data-ttu-id="4711c-138">모두</span><span class="sxs-lookup"><span data-stu-id="4711c-138">all</span></span> |
| <span data-ttu-id="4711c-139">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="4711c-139">ExcludeAssets</span></span> | <span data-ttu-id="4711c-140">이러한 자산을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-140">These assets will not be consumed</span></span> | <span data-ttu-id="4711c-141">없음</span><span class="sxs-lookup"><span data-stu-id="4711c-141">none</span></span> |
| <span data-ttu-id="4711c-142">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="4711c-142">PrivateAssets</span></span> | <span data-ttu-id="4711c-143">이러한 자산을 사용하지만 부모 프로젝트로 흐르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="4711c-144">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="4711c-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="4711c-145">이러한 태그에 허용 가능한 값은 단독으로 표시해야 하는 `all` 및 `none`를 제외하고 세미콜론으로 구분된 값이 여러 개인 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="4711c-146">값</span><span class="sxs-lookup"><span data-stu-id="4711c-146">Value</span></span> | <span data-ttu-id="4711c-147">설명</span><span class="sxs-lookup"><span data-stu-id="4711c-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="4711c-148">compile</span><span class="sxs-lookup"><span data-stu-id="4711c-148">compile</span></span> | <span data-ttu-id="4711c-149">`lib` 폴더의 콘텐츠이며 프로젝트에서 폴더 내의 어셈블리를 컴파일할 수 있는지 여부 제어</span><span class="sxs-lookup"><span data-stu-id="4711c-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="4711c-150">런타임</span><span class="sxs-lookup"><span data-stu-id="4711c-150">runtime</span></span> | <span data-ttu-id="4711c-151">`lib` 및 `runtimes` 폴더의 콘텐츠이며 이러한 어셈블리가 빌드 출력 디렉터리에 복사되는지 여부 제어</span><span class="sxs-lookup"><span data-stu-id="4711c-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="4711c-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="4711c-152">contentFiles</span></span> | <span data-ttu-id="4711c-153">`contentfiles` 폴더의 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="4711c-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="4711c-154">빌드</span><span class="sxs-lookup"><span data-stu-id="4711c-154">build</span></span> | <span data-ttu-id="4711c-155">`build` 폴더의 `.props` 및 `.targets`</span><span class="sxs-lookup"><span data-stu-id="4711c-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="4711c-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="4711c-156">buildMultitargeting</span></span> | <span data-ttu-id="4711c-157">*(4.0)* 프레임워크 간 타기팅을 위한 `buildMultitargeting` 폴더의 `.props` 및 `.targets`</span><span class="sxs-lookup"><span data-stu-id="4711c-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="4711c-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="4711c-158">buildTransitive</span></span> | <span data-ttu-id="4711c-159">‘(5.0 이상)’ 사용하는 프로젝트로 전이적으로 흐르는 자산을 위한 `buildTransitive` 폴더의 `.props` 및 `.targets` </span><span class="sxs-lookup"><span data-stu-id="4711c-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="4711c-160">[기능](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4711c-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="4711c-161">분석기</span><span class="sxs-lookup"><span data-stu-id="4711c-161">analyzers</span></span> | <span data-ttu-id="4711c-162">.NET 분석기</span><span class="sxs-lookup"><span data-stu-id="4711c-162">.NET analyzers</span></span> |
| <span data-ttu-id="4711c-163">native</span><span class="sxs-lookup"><span data-stu-id="4711c-163">native</span></span> | <span data-ttu-id="4711c-164">`native` 폴더의 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="4711c-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="4711c-165">없음</span><span class="sxs-lookup"><span data-stu-id="4711c-165">none</span></span> | <span data-ttu-id="4711c-166">위의 항목을 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-166">None of the above are used.</span></span> |
| <span data-ttu-id="4711c-167">모두</span><span class="sxs-lookup"><span data-stu-id="4711c-167">all</span></span> | <span data-ttu-id="4711c-168">위 모두 해당(`none` 제외)</span><span class="sxs-lookup"><span data-stu-id="4711c-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="4711c-169">다음 예제에서는 패키지의 콘텐츠 파일을 제외한 모든 항목을 프로젝트에서 사용할 수 있으며 콘텐츠 파일과 분석기를 제외한 모든 항목이 부모 프로젝트로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="4711c-170">`build`가 `PrivateAssets`에 포함되지 않기 때문에 대상 및 props은 부모 프로젝트로 전달되게 *됩니다*.</span><span class="sxs-lookup"><span data-stu-id="4711c-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="4711c-171">예를 들어 위의 참조가 AppLogger라는 NuGet 패키지를 빌드하는 프로젝트에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="4711c-172">프로젝트가 AppLogger를 사용할 수 있는 것처럼 AppLogger는 `Contoso.Utility.UsefulStuff`의 대상 및 props을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="4711c-173">`.nuspec` 파일에서 `developmentDependency`가 `true`로 설정되면 패키지가 개발 전용 종속성으로 표시되므로 해당 패키지가 다른 패키지의 종속성으로 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="4711c-174">PackageReference *(NuGet 4.8 이상)* 를 사용하는 경우 이 플래그는 컴파일 시간 자산을 컴파일에서 제외한다는 의미이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="4711c-175">자세한 내용은 [PackageReference에 대한 DevelopmentDependency 지원](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4711c-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="4711c-176">PackageReference 조건 추가</span><span class="sxs-lookup"><span data-stu-id="4711c-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="4711c-177">조건이 모든 MSBuild 변수 또는 대상이나 props 파일에 정의된 변수를 사용할 수 있는 경우에 패키지가 포함되어 있는지를 제어하는 조건을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="4711c-178">그러나 현재는 `TargetFramework` 변수만이 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="4711c-179">예를 들어 `net452`뿐만 아니라 `netstandard1.4`를 대상으로 지정했지만 `net452`에만 적용할 수 있는 종속성이 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="4711c-180">이 경우에 불필요한 해당 종속성을 추가하는 패키지를 사용하는 `netstandard1.4` 프로젝트를 사용하지 않으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="4711c-181">이를 방지하려면 다음과 같이 `PackageReference`에 대한 조건을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="4711c-182">이 프로젝트를 사용하여 빌드한 패키지는 Newtonsoft.Json이 `net452` 대상에서만 종속성으로 포함되어 있다고 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![VS2017에서 PackageReference에 대한 조건을 적용한 결과](media/PackageReference-Condition.png)

<span data-ttu-id="4711c-184">조건은 `ItemGroup` 수준에도 적용될 수 있고 모든 자식 `PackageReference` 요소에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="4711c-185">GeneratePathProperty</span><span class="sxs-lookup"><span data-stu-id="4711c-185">GeneratePathProperty</span></span>

<span data-ttu-id="4711c-186">이 기능은 NuGet **5.0** 이상 및 Visual Studio 2019 **16.0** 이상에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="4711c-187">경우에 따라 MSBuild 대상의 패키지 파일을 참조하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="4711c-188">`packages.config` 기반 프로젝트에서 패키지는 프로젝트 파일의 상대 폴더에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="4711c-189">그러나 PackageReference에서는 머신마다 다를 수 있는 *global-packages* 폴더의 패키지가 [사용](../concepts/package-installation-process.md)됩니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="4711c-190">이 문제를 해결하기 위해 NuGet은 사용할 패키지의 위치를 가리키는 속성을 도입했습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="4711c-191">예:</span><span class="sxs-lookup"><span data-stu-id="4711c-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="4711c-192">또한 NuGet은 tools 폴더를 포함하는 패키지의 속성을 자동으로 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

<span data-ttu-id="4711c-193">MSBuild 속성과 패키지 ID에는 동일한 제한이 없기 때문에 패키지 ID를 MSBuild 이름으로 변경하고 `Pkg` 단어를 앞에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="4711c-194">생성된 속성의 정확한 이름을 확인하려면 생성된 [nuget.exe](../reference/msbuild-targets.md#restore-outputs) 파일을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="4711c-195">NuGet 경고 및 오류</span><span class="sxs-lookup"><span data-stu-id="4711c-195">NuGet warnings and errors</span></span>

<span data-ttu-id="4711c-196">‘이 기능은 NuGet **4.3** 이상 및 Visual Studio 2017 **15.3** 이상에서 사용할 수 있습니다.’ </span><span class="sxs-lookup"><span data-stu-id="4711c-196">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="4711c-197">많은 패키지 및 복원 시나리오에서는 모든 NuGet 경고 및 오류가 코딩되고 `NU****`로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-197">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="4711c-198">모든 NuGet 경고 및 오류는 [참조](../reference/errors-and-warnings.md) 문서에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-198">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="4711c-199">NuGet은 다음과 같은 경고 속성을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-199">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="4711c-200">`TreatWarningsAsErrors` - 모든 경고를 오류로 처리</span><span class="sxs-lookup"><span data-stu-id="4711c-200">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="4711c-201">`WarningsAsErrors` - 특정 경고를 오류로 처리</span><span class="sxs-lookup"><span data-stu-id="4711c-201">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="4711c-202">`NoWarn` - 프로젝트 수준 또는 패키지 수준에서 특정 경고 숨기기</span><span class="sxs-lookup"><span data-stu-id="4711c-202">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="4711c-203">예:</span><span class="sxs-lookup"><span data-stu-id="4711c-203">Examples:</span></span>

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="4711c-204">NuGet 경고 표시 안 함</span><span class="sxs-lookup"><span data-stu-id="4711c-204">Suppressing NuGet warnings</span></span>

<span data-ttu-id="4711c-205">패키지 및 복원 작업 중에 발생하는 모든 NuGet 경고를 해결하는 것이 좋지만, 특정 상황에서는 경고를 표시하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-205">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="4711c-206">프로젝트 수준에서 경고를 표시하지 않으려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-206">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="4711c-207">경고가 그래프의 특정 패키지에만 적용되는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-207">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="4711c-208">PackageReference 항목에 `NoWarn`을 추가하면 보다 선택적으로 경고 표시를 해제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-208">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="4711c-209">Visual Studio에서 NuGet 패키지 경고 표시 안 함</span><span class="sxs-lookup"><span data-stu-id="4711c-209">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="4711c-210">Visual Studio에서 IDE를 통해 [경고 표시를 해제](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-210">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="4711c-211">종속성 잠금</span><span class="sxs-lookup"><span data-stu-id="4711c-211">Locking dependencies</span></span>

<span data-ttu-id="4711c-212">이 기능은 NuGet **4.9** 이상 및 Visual Studio 2017 **15.9** 이상에서 사용할 수 있습니다. </span><span class="sxs-lookup"><span data-stu-id="4711c-212">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="4711c-213">NuGet 복원의 입력은 프로젝트 파일(최상위 또는 직접 종속성)의 패키지 참조 세트이며, 출력은 전이 종속성을 포함한 모든 패키지 종속성의 전체 클로저입니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-213">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="4711c-214">입력 PackageReference 목록이 변경되지 않은 경우 NuGet은 항상 패키지 종속성의 동일한 전체 클로저를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-214">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="4711c-215">그러나 이렇게 할 수 없는 몇 가지 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-215">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="4711c-216">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="4711c-216">For example:</span></span>

* <span data-ttu-id="4711c-217">`<PackageReference Include="My.Sample.Lib" Version="4.*"/>` 같은 부동 버전을 사용하는 경우.</span><span class="sxs-lookup"><span data-stu-id="4711c-217">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="4711c-218">여기서 의도는 패키지의 모든 복원에서 최신 버전으로 이동하는 것이지만, 사용자가 그래프를 특정 최신 버전으로 잠그고 명시적 제스처에 따라 이후 버전(사용 가능한 경우)으로 이동하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-218">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="4711c-219">PackageReference 버전 요구 사항과 일치하는 패키지의 최신 버전이 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-219">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="4711c-220">예:</span><span class="sxs-lookup"><span data-stu-id="4711c-220">E.g.</span></span> 

  * <span data-ttu-id="4711c-221">1일: `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>`을 지정하지만 NuGet 리포지토리에서 사용 가능한 버전이 4.1.0, 4.2.0, 4.3.0인 경우.</span><span class="sxs-lookup"><span data-stu-id="4711c-221">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="4711c-222">이 경우 NuGet은 4.1.0(가장 가까운 최소 버전)으로 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-222">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="4711c-223">2일: 버전 4.0.0이 게시됩니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-223">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="4711c-224">NuGet은 이제 정확한 일치 항목을 찾고 4.0.0으로 확인을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-224">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="4711c-225">지정된 패키지 버전이 리포지토리에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-225">A given package version is removed from the repository.</span></span> <span data-ttu-id="4711c-226">nuget.org에서는 패키지 삭제를 허용하지 않지만 일부 패키지 리포지토리에는 이 제약 조건이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-226">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="4711c-227">따라서 NuGet은 삭제된 버전으로 확인할 수 없는 경우 가장 일치하는 항목을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-227">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="4711c-228">잠금 파일 사용</span><span class="sxs-lookup"><span data-stu-id="4711c-228">Enabling lock file</span></span>

<span data-ttu-id="4711c-229">패키지 종속성의 전체 클로저를 유지하기 위해 프로젝트의 MSBuild 속성 `RestorePackagesWithLockFile`을 설정하여 잠금 파일 기능을 옵트인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-229">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="4711c-230">이 속성을 설정하면 NuGet 복원은 모든 패키지 종속성을 나열하는 프로젝트 루트 디렉터리에 잠금 파일인 `packages.lock.json` 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-230">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="4711c-231">프로젝트의 루트 디렉터리에 `packages.lock.json` 파일이 있으면 `RestorePackagesWithLockFile` 속성이 설정되지 않은 경우에도 복원에는 항상 잠금 파일이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-231">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="4711c-232">따라서 이 기능을 옵트인하는 또 다른 방법은 프로젝트의 루트 디렉터리에 더미 공백 `packages.lock.json` 파일을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-232">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="4711c-233">잠금 파일을 사용한 `restore` 동작</span><span class="sxs-lookup"><span data-stu-id="4711c-233">`restore` behavior with lock file</span></span>
<span data-ttu-id="4711c-234">프로젝트에 대한 잠금 파일이 있으면 NuGet은 이 잠금 파일을 사용하여 `restore`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-234">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="4711c-235">NuGet은 프로젝트 파일(또는 종속 프로젝트 파일)에 언급된 패키지 종속성에 변경 내용이 있는지 빠르게 확인하고, 변경 내용이 없으면 잠금 파일에 언급된 패키지를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-235">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="4711c-236">패키지 종속성은 다시 평가되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-236">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="4711c-237">NuGet은 프로젝트 파일에 언급된 정의된 종속성에서 변경을 발견하면 패키지 그래프를 다시 평가하고 잠금 파일을 업데이트하여 프로젝트의 새 패키지 클로저를 반영합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-237">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="4711c-238">CI/CD 및 기타 시나리오의 경우 패키지 종속성을 즉시 변경하지 않으려면 `lockedmode`를 `true`로 설정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-238">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="4711c-239">dotnet.exe의 경우 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-239">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="4711c-240">msbuild.exe의 경우 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-240">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="4711c-241">프로젝트 파일에서 이 조건부 MSBuild 속성을 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-241">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="4711c-242">잠김 모드가 `true`인 경우 잠금 파일에 나열된 정확한 패키지가 복원되거나, 잠금 파일이 생성된 후 프로젝트의 정의된 패키지 종속성을 업데이트한 경우 복원에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-242">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="4711c-243">소스 리포지토리의 잠금 파일 파트 만들기</span><span class="sxs-lookup"><span data-stu-id="4711c-243">Make lock file part of your source repository</span></span>
<span data-ttu-id="4711c-244">애플리케이션, 실행 파일을 빌드하는 동안 원하는 프로젝트가 종속성 체인의 시작 부분에 있으면 NuGet이 복원 중에 사용할 수 있도록 소스 코드 리포지토리에 잠금 파일을 체크 인합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-244">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="4711c-245">그러나 프로젝트가 사용자가 제공하지 않는 라이브러리 프로젝트이거나 다른 프로젝트가 사용하는 공통 코드 프로젝트인 경우에는 잠금 파일을 소스 코드의 일부로 체크 인하면 **안 됩니다**.</span><span class="sxs-lookup"><span data-stu-id="4711c-245">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="4711c-246">잠금 파일을 보존해도 문제가 되지 않지만, 공통 코드 프로젝트의 잠긴 패키지 종속성은 이 공통 코드 프로젝트를 사용하는 프로젝트의 복원/빌드 중에 잠금 파일에 나열된 대로 사용되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-246">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="4711c-247">예:</span><span class="sxs-lookup"><span data-stu-id="4711c-247">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="4711c-248">`ProjectA`가 `PackageX` 버전 `2.0.0`에 대한 종속성을 포함하고 `PackageX` 버전 `1.0.0`을 사용하는 `ProjectB`를 참조하는 경우 `ProjectB`의 잠금 파일은 `PackageX` 버전 `1.0.0`에 대한 종속성을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-248">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="4711c-249">그러나 `ProjectA`를 빌드하면 해당 잠금 파일에는 `ProjectB`의 잠금 파일에 나열된 대로 `PackageX` 버전 `1.0.0`이 **아닌** **`2.0.0`** 에 대한 종속성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-249">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="4711c-250">따라서 공통 코드 프로젝트의 잠금 파일에는 이 파일을 사용하는 프로젝트에 대해 확인된 패키지가 거의 언급되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-250">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="4711c-251">잠금 파일 확장성</span><span class="sxs-lookup"><span data-stu-id="4711c-251">Lock file extensibility</span></span>

<span data-ttu-id="4711c-252">다음 설명과 같이 잠금 파일을 사용하여 다양한 복원 동작을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-252">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="4711c-253">NuGet.exe 옵션</span><span class="sxs-lookup"><span data-stu-id="4711c-253">NuGet.exe option</span></span> | <span data-ttu-id="4711c-254">dotnet 옵션</span><span class="sxs-lookup"><span data-stu-id="4711c-254">dotnet option</span></span> | <span data-ttu-id="4711c-255">MSBuild 해당 옵션</span><span class="sxs-lookup"><span data-stu-id="4711c-255">MSBuild equivalent option</span></span> | <span data-ttu-id="4711c-256">설명</span><span class="sxs-lookup"><span data-stu-id="4711c-256">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="4711c-257">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="4711c-257">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="4711c-258">잠금 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-258">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="4711c-259">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="4711c-259">RestoreLockedMode</span></span> | <span data-ttu-id="4711c-260">복원에 잠금 모드를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-260">Enables locked mode for restore.</span></span> <span data-ttu-id="4711c-261">이는 반복 가능한 빌드를 원하는 CI/CD 시나리오에서 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-261">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="4711c-262">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="4711c-262">RestoreForceEvaluate</span></span> | <span data-ttu-id="4711c-263">이 옵션은 프로젝트에 정의된 부동 버전의 패키지에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-263">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="4711c-264">기본적으로 NuGet 복원은 이 옵션으로 복원을 실행하지 않는 한 각 복원에서 패키지 버전을 자동으로 업데이트하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-264">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="4711c-265">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="4711c-265">NuGetLockFilePath</span></span> | <span data-ttu-id="4711c-266">프로젝트의 사용자 지정 잠금 파일 위치를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-266">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="4711c-267">기본적으로 NuGet은 루트 디렉터리에서 `packages.lock.json`을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-267">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="4711c-268">같은 디렉터리에 여러 프로젝트가 있는 경우 NuGet은 프로젝트별 잠금 파일 `packages.<project_name>.lock.json`을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="4711c-268">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
