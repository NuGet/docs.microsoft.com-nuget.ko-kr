---
title: NuGet project.json 보관 콘텐츠
description: project.json 콘텐츠의 기타 비트는 NuGet 설명서의 다른 영역에서 제거됩니다.
author: karann-msft
ms.author: karann
ms.date: 01/17/2018
ms.topic: conceptual
ms.openlocfilehash: 8d732e87f01c55bde87da0a2e382fd6d509886a3
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317009"
---
# <a name="projectjson-archive"></a><span data-ttu-id="c6180-103">project.json 보관 파일</span><span class="sxs-lookup"><span data-stu-id="c6180-103">project.json archive</span></span>

<span data-ttu-id="c6180-104">`project.json` 관리 형식은 NuGet 3.x와 함께 도입되었으며 특정 프로젝트 유형에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-104">The `project.json` management format was introduced with NuGet 3.x and used for certain project types.</span></span> <span data-ttu-id="c6180-105">이 참조 형식은 종속성이 프로젝트 파일에 직접 나열되는 PackageReference 형식이 도입되면서 더 이상 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-105">It was deprecated with the introduction of the PackageReference format, in which dependencies are listed directly in a project file.</span></span>

<span data-ttu-id="c6180-106">또한 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6180-106">Also see:</span></span>

- [<span data-ttu-id="c6180-107">project.json 스키마</span><span class="sxs-lookup"><span data-stu-id="c6180-107">project.json schema</span></span>](project-json.md)
- [<span data-ttu-id="c6180-108">project.json이 패키지 작성자에 미치는 영향</span><span class="sxs-lookup"><span data-stu-id="c6180-108">project.json impact on package authors</span></span>](project-json-impact.md)
- [<span data-ttu-id="c6180-109">project.json 및 UWP</span><span class="sxs-lookup"><span data-stu-id="c6180-109">project.json and UWP</span></span>](project-json-and-uwp.md)

## <a name="projectjson-management-format"></a><span data-ttu-id="c6180-110">project.json 관리 형식</span><span class="sxs-lookup"><span data-stu-id="c6180-110">project.json management format</span></span>

<span data-ttu-id="c6180-111">*원래 [패키지 복원](../what-is-nuget.md)에 포함됩니다.*</span><span class="sxs-lookup"><span data-stu-id="c6180-111">*Originally in [Package restore](../what-is-nuget.md).*</span></span>

<span data-ttu-id="c6180-112">관리 형식 목록에서:</span><span class="sxs-lookup"><span data-stu-id="c6180-112">In the list of management formats:</span></span>

- <span data-ttu-id="c6180-113">[`project.json`](project-json.md): *(사용되지 않음)* 연결된 `project.lock.json` 파일의 전체 패키지 그래프와 함께 프로젝트의 종속성 목록을 유지 관리하는 JSON 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-113">[`project.json`](project-json.md): *(deprecated)* A JSON file that maintains a list of the project's dependencies with an overall package graph in an associated file, `project.lock.json`.</span></span> <span data-ttu-id="c6180-114">이 형식 대신 PackageReference가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-114">This format is deprecated in favor of PackageReference.</span></span>

## <a name="nuget-restore-on-mono"></a><span data-ttu-id="c6180-115">Mono에서 nuget 복원</span><span class="sxs-lookup"><span data-stu-id="c6180-115">nuget restore on Mono</span></span>

<span data-ttu-id="c6180-116">*원래 [NuGet 클라이언트 도구 설치](../install-nuget-client-tools.md)에 포함됩니다.*</span><span class="sxs-lookup"><span data-stu-id="c6180-116">*Originally in [Install NuGet client tools](../install-nuget-client-tools.md).*</span></span>

<span data-ttu-id="c6180-117">`project.json`에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-117">Works with `project.json`.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="c6180-118">복원을 사용하여 패키지 버전 제한</span><span class="sxs-lookup"><span data-stu-id="c6180-118">Constraining package versions with restore</span></span>

<span data-ttu-id="c6180-119">*원래 [패키지 복원](../consume-packages/package-restore.md#constrain-package-versions-with-restore)에 포함됩니다.*</span><span class="sxs-lookup"><span data-stu-id="c6180-119">*Originally in [Package restore](../consume-packages/package-restore.md#constrain-package-versions-with-restore).*</span></span>

- <span data-ttu-id="c6180-120">`project.json`: 종속성의 버전 번호를 사용하여 버전 범위를 직접 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-120">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="c6180-121">예:</span><span class="sxs-lookup"><span data-stu-id="c6180-121">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

## <a name="nuget-cli-commands"></a><span data-ttu-id="c6180-122">NuGet CLI 명령</span><span class="sxs-lookup"><span data-stu-id="c6180-122">NuGet CLI commands</span></span>

- <span data-ttu-id="c6180-123">`nuget install`은 `project.json`에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-123">`nuget install` does not work with `project.json`.</span></span>
- <span data-ttu-id="c6180-124">`nuget restore`: `project.json`을 사용하는 프로젝트에서 필요한 경우 `project.lock.json` 파일과 `<project>.nuget.props` 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-124">`nuget restore`: with projects using `project.json`, generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="c6180-125">(두 파일 모두 소스 제어에서 생략할 수 있습니다.) `<projectPath>` 인수는 `project.json` 파일을 가리키고 `packages.config` 또는 프로젝트 파일을 가리키는 것과 동일한 동작을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-125">(Both files can be omitted from source control.) The `<projectPath>` argument can point a `project.json` file and has the same behavior as pointing to a `packages.config` or project file.</span></span> <span data-ttu-id="c6180-126">패키지 폴더의 우선 순위에서 `project.json`를 사용하면 `%userprofile%\.nuget\packages`가 먼저 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-126">In the priority order for package folders, `%userprofile%\.nuget\packages` is searched first when using `project.json`.</span></span>
- <span data-ttu-id="c6180-127">`nuget update`: Mono에서 이 명령은 `project.json`을 사용하는 프로젝트에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-127">`nuget update`: On Mono, this command does not work with projects using `project.json`.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="c6180-128">PackageReference를 사용하여 종속성 확인</span><span class="sxs-lookup"><span data-stu-id="c6180-128">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="c6180-129">*원래 [종속성 확인](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)에 포함됩니다.*</span><span class="sxs-lookup"><span data-stu-id="c6180-129">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).*</span></span>

<span data-ttu-id="c6180-130">PackageReference의 동작은 `project.json`에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-130">The behavior of PackageReference applies also to `project.json`.</span></span> <span data-ttu-id="c6180-131">NuGet 복원은 종속성 그래프를 `project.json` 옆에 있는 `project.lock.json` 파일에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-131">NuGet restore writes the dependency graph into a file named `project.lock.json` alongside `project.json`.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="c6180-132">종속성 자산 관리</span><span class="sxs-lookup"><span data-stu-id="c6180-132">Managing dependency assets</span></span>

<span data-ttu-id="c6180-133">*원래 [종속성 확인](../consume-packages/dependency-resolution.md#managing-dependency-assets)에 포함됩니다.*</span><span class="sxs-lookup"><span data-stu-id="c6180-133">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#managing-dependency-assets).*</span></span>

<span data-ttu-id="c6180-134">`project.json` 형식을 사용하는 경우 종속성에서 최상위 프로젝트로 이동하는 자산을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-134">When using the `project.json` format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="c6180-135">자세한 내용은 [project.json](project-json.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6180-135">For details, see [project.json](project-json.md).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="c6180-136">참조 제외</span><span class="sxs-lookup"><span data-stu-id="c6180-136">Excluding references</span></span>

<span data-ttu-id="c6180-137">*원래 [종속성 확인](../consume-packages/dependency-resolution.md#excluding-references)에 포함됩니다.*</span><span class="sxs-lookup"><span data-stu-id="c6180-137">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#excluding-references).*</span></span>

- <span data-ttu-id="c6180-138">`project.json`: PackageC에 대한 종속성에 `"exclude" : "all"`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-138">`project.json`: add `"exclude" : "all"` in the dependency for PackageC:</span></span>

    ```json
    {
        "dependencies": {
            "PackageC": {
            "version": "1.0.0",
            "exclude": "all"
            }
        }
    }
    ```

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="c6180-139">호환되지 않는 패키지 오류 해결</span><span class="sxs-lookup"><span data-stu-id="c6180-139">Resolving incompatible package errors</span></span>

<span data-ttu-id="c6180-140">*원래 [종속성 확인](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors)에 포함됩니다.*</span><span class="sxs-lookup"><span data-stu-id="c6180-140">*Originally in [Dependency resolution](../consume-packages/dependency-resolution.md#resolving-incompatible-package-errors).*</span></span>

<span data-ttu-id="c6180-141">추가된 오류 해결 방법:</span><span class="sxs-lookup"><span data-stu-id="c6180-141">An added means of resolving errors:</span></span>

- <span data-ttu-id="c6180-142">**권장하지 않음**: 패키지 작성자와 함께 작업하는 동안의 임시 해결 방법으로, `netcore`, `netstandard` 및 `netcoreapp`을 대상으로 하는 프로젝트에서 다른 프레임워크를 호환되는 항목으로 나타낼 수 있으므로 다른 프레임워크를 대상으로 하는 패키지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-142">**Not recommended**: as a temporary solution while you work with the package author, projects targeting `netcore`, `netstandard`, and `netcoreapp` can denote other frameworks as being compatible, thereby allowing packages targeting those other frameworks to be used.</span></span> <span data-ttu-id="c6180-143">[project.json imports](project-json.md#imports) 및 [PackageTargetFallback MSBuild restore 대상](../reference/msbuild-targets.md#packagetargetfallback)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6180-143">See [project.json imports](project-json.md#imports) and [MSBuild restore target PackageTargetFallback](../reference/msbuild-targets.md#packagetargetfallback).</span></span> <span data-ttu-id="c6180-144">이로 인해 예기치 않은 동작이 발생할 수 있으므로 업데이트 시 패키지 작성자와 협력하여 패키지 비호환성 문제를 해결하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-144">This can cause unexpected behaviors, so again, it's best to resolve package incompatibilities by working with the package author on an update.</span></span>

## <a name="target-frameworks"></a><span data-ttu-id="c6180-145">대상 프레임워크</span><span class="sxs-lookup"><span data-stu-id="c6180-145">Target frameworks</span></span>

<span data-ttu-id="c6180-146">*원래 [대상 프레임워크](../reference/target-frameworks.md)에 포함됩니다.*</span><span class="sxs-lookup"><span data-stu-id="c6180-146">*Originally in [Target frameworks](../reference/target-frameworks.md).*</span></span>

- <span data-ttu-id="c6180-147">[project.json](project-json.md): `frameworks` 노드는 프로젝트를 컴파일할 수 있는 프레임워크 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-147">[project.json](project-json.md): The `frameworks` node specifies the framework versions that the project can be compiled against.</span></span>

## <a name="creating-a-package"></a><span data-ttu-id="c6180-148">패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="c6180-148">Creating a package</span></span>

<span data-ttu-id="c6180-149">*원래 [패키지 만들기](../create-packages/creating-a-package.md)에 포함됩니다.*</span><span class="sxs-lookup"><span data-stu-id="c6180-149">*Originally in [Creating a package](../create-packages/creating-a-package.md)*</span></span>

### <a name="setting-a-package-type"></a><span data-ttu-id="c6180-150">패키지 유형 설정</span><span class="sxs-lookup"><span data-stu-id="c6180-150">Setting a package type</span></span>

<span data-ttu-id="c6180-151">.NET Core 1.x의 경우 DotnetCliTool 패키지가 설치되면 Visual Studio에서는 패키지를 `dependencies` 노드 대신 `project.json` `tools` 노드에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-151">With .NET Core 1.x, when a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

<span data-ttu-id="c6180-152">패키지 형식은 `project.json`에 설정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-152">Package types are set in `project.json`.</span></span>

- <span data-ttu-id="c6180-153">`project.json`: `packOptions.packageType` 속성 json 내에 패키지 유형을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-153">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="c6180-154">MSBuild용 targets 및 props 추가</span><span class="sxs-lookup"><span data-stu-id="c6180-154">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="c6180-155">*원래 [Visual Studio 2015를 통해 .NET Standard NuGet 패키지 만들기](../guides/create-net-standard-packages-vs2015.md)에 포함됩니다.*</span><span class="sxs-lookup"><span data-stu-id="c6180-155">*Originally in [Create .NET Standard NuGet Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md).*</span></span>

<span data-ttu-id="c6180-156">`project.json`을 사용하는 경우 대상이 프로젝트에는 추가되지 않지만 `project.lock.json`을 통해 사용될 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-156">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>

### <a name="package-versioning"></a><span data-ttu-id="c6180-157">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="c6180-157">Package versioning</span></span>

<span data-ttu-id="c6180-158">*원래 [패키지 버전 관리](../reference/package-versioning.md)에 포함됩니다.*</span><span class="sxs-lookup"><span data-stu-id="c6180-158">*Originally in [Package versioning](../reference/package-versioning.md).*</span></span>

<span data-ttu-id="c6180-159">`project.json` 형식을 사용하는 경우 NuGet은 숫자의 주, 부, 패치 및 시험판 접미사 부분에 와일드카드 표기법(\*)도 사용하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-159">When using the `project.json` format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span>

### <a name="nugetconfig-reference"></a><span data-ttu-id="c6180-160">NuGet.Config 참조</span><span class="sxs-lookup"><span data-stu-id="c6180-160">NuGet.Config reference</span></span>

<span data-ttu-id="c6180-161">*원래 [NuGet.Config 참조](../reference/nuget-config-file.md)에 포함됩니다.*</span><span class="sxs-lookup"><span data-stu-id="c6180-161">*Originally in [NuGet.Config reference](../reference/nuget-config-file.md).*</span></span>

<span data-ttu-id="c6180-162">`globalPackagesFolder`는 `project.json`에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-162">`globalPackagesFolder` applies only to `project.json`.</span></span> <span data-ttu-id="c6180-163">(추가 참고: PackageReference에도 적용됩니다.)</span><span class="sxs-lookup"><span data-stu-id="c6180-163">(Added note: also applies to PackageReference.)</span></span>

### <a name="nuspec-file-reference"></a><span data-ttu-id="c6180-164">nuspec 파일 참조</span><span class="sxs-lookup"><span data-stu-id="c6180-164">nuspec file reference</span></span>

<span data-ttu-id="c6180-165">*원래 [nuspec 참조](../reference/nuspec.md)에 포함됩니다.*</span><span class="sxs-lookup"><span data-stu-id="c6180-165">*Originally in [nuspec reference](../reference/nuspec.md).*</span></span>

<span data-ttu-id="c6180-166">`project.json`에서는 `<contentFiles>` 요소가 `<files>` 대신 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-166">The `<contentFiles>` element is used instead of `<files>` with `project.json`.</span></span>

### <a name="package-manager-options-control"></a><span data-ttu-id="c6180-167">패키지 관리자 옵션 제어</span><span class="sxs-lookup"><span data-stu-id="c6180-167">Package manager options control</span></span>

<span data-ttu-id="c6180-168">*원래 [패키지 관리자 UI 참조](../consume-packages/install-use-packages-visual-studio.md)에 포함됩니다.*</span><span class="sxs-lookup"><span data-stu-id="c6180-168">*Originally in [Package Manager UI reference](../consume-packages/install-use-packages-visual-studio.md).*</span></span>

<span data-ttu-id="c6180-169">`project.json` 관리 형식을 사용하는 프로젝트는 **미리 보기 창 표시** 옵션만 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-169">Projects using `project.json` management format show only the **Show preview window** option.</span></span>

### <a name="visual-studio-templates"></a><span data-ttu-id="c6180-170">Visual Studio 템플릿</span><span class="sxs-lookup"><span data-stu-id="c6180-170">Visual Studio Templates</span></span>

<span data-ttu-id="c6180-171">*원래 [Visual Studio 템플릿의 NuGet 패키지](../visual-studio-extensibility/visual-studio-templates.md)에 포함됩니다.*</span><span class="sxs-lookup"><span data-stu-id="c6180-171">*Originally in [NuGet Packages in Visual Studio templates](../visual-studio-extensibility/visual-studio-templates.md).*</span></span>

<span data-ttu-id="c6180-172">모범 사례: `project.json` 파일을 템플릿에 포함하지 않고, NuGet 패키지를 설치할 때 추가될 참조 또는 내용을 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c6180-172">Best practices: templates do not include a `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>