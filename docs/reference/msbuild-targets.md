---
title: MSBuild 대상으로서의 NuGet pack 및 restore
description: NuGet pack 및 restore는 NuGet 4.0 이상에서 MSBuild 대상으로 직접 작동할 수 있습니다.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: ed3545454a811c311190a191c566d9e9192f3fcc
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825060"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="02d0e-103">MSBuild 대상으로서의 NuGet pack 및 restore</span><span class="sxs-lookup"><span data-stu-id="02d0e-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="02d0e-104">*NuGet 4.0 이상*</span><span class="sxs-lookup"><span data-stu-id="02d0e-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="02d0e-105">[PackageReference](../consume-packages/package-references-in-project-files.md) 형식을 사용 하는 경우 NuGet 4.0 이상에서는 별도의 `.nuspec` 파일을 사용 하지 않고 프로젝트 파일 내에 모든 매니페스트 메타 데이터를 직접 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="02d0e-106">MSBuild 15.1 이상에서 NuGet은 아래에서 설명한 대로 `pack` 및 `restore` 대상이 있는 일류 MSBuild 시민이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="02d0e-107">이러한 대상을 사용하면 다른 MSBuild 작업 또는 대상과 마찬가지로 NuGet을 사용하여 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="02d0e-108">MSBuild를 사용 하 여 NuGet 패키지를 만드는 방법에 대 한 지침은 [msbuild를 사용 하 여 nuget 패키지 만들기](../create-packages/creating-a-package-msbuild.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="02d0e-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="02d0e-109">(NuGet 3.x 및 이전 버전의 경우 NuGet CLI를 통해 [pack](../reference/cli-reference/cli-ref-pack.md) 및 [restore](../reference/cli-reference/cli-ref-restore.md) 명령을 대신 사용합니다.)</span><span class="sxs-lookup"><span data-stu-id="02d0e-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="02d0e-110">대상 빌드 순서</span><span class="sxs-lookup"><span data-stu-id="02d0e-110">Target build order</span></span>

<span data-ttu-id="02d0e-111">`pack` 및 `restore`는 MSBuild 대상이므로 이 대상에 액세스하여 워크플로를 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="02d0e-112">예를 들어 패키지를 압축한 후 네트워크 공유에 복사한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="02d0e-113">이렇게 하려면 프로젝트 파일에 다음을 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="02d0e-114">마찬가지로, MSBuild 작업을 작성하고, 고유한 대상을 작성하고, MSBuild 작업에서 NuGet 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="02d0e-115">`$(OutputPath)`는 상대적 이며, 프로젝트 루트에서 명령을 실행 하는 것으로 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="02d0e-116">pack 대상</span><span class="sxs-lookup"><span data-stu-id="02d0e-116">pack target</span></span>

<span data-ttu-id="02d0e-117">PackageReference 형식을 사용 하는 .NET Standard 프로젝트의 경우 `msbuild -t:pack`를 사용 하 여 NuGet 패키지를 만드는 데 사용할 프로젝트 파일의 입력을 그립니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="02d0e-118">아래 표에서는 첫 번째 `<PropertyGroup>` 노드 내에서 프로젝트 파일에 추가할 수 있는 MSBuild 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="02d0e-119">Visual Studio 2017 이상에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **{project_name} 편집**을 선택하여 이러한 편집 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="02d0e-120">편의상 이 표는 [`.nuspec` 파일 ](../reference/nuspec.md)에 있는 동등한 속성으로 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="02d0e-121">`.nuspec`의 `Owners` 및 `Summary` 속성은 MSBuild에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="02d0e-122">특성/NuSpec 값</span><span class="sxs-lookup"><span data-stu-id="02d0e-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="02d0e-123">MSBuild 속성</span><span class="sxs-lookup"><span data-stu-id="02d0e-123">MSBuild Property</span></span> | <span data-ttu-id="02d0e-124">기본</span><span class="sxs-lookup"><span data-stu-id="02d0e-124">Default</span></span> | <span data-ttu-id="02d0e-125">참고</span><span class="sxs-lookup"><span data-stu-id="02d0e-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="02d0e-126">ID</span><span class="sxs-lookup"><span data-stu-id="02d0e-126">Id</span></span> | <span data-ttu-id="02d0e-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="02d0e-127">PackageId</span></span> | <span data-ttu-id="02d0e-128">어셈블리 이름</span><span class="sxs-lookup"><span data-stu-id="02d0e-128">AssemblyName</span></span> | <span data-ttu-id="02d0e-129">MSBuild의 $(AssemblyName)입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="02d0e-130">Version</span><span class="sxs-lookup"><span data-stu-id="02d0e-130">Version</span></span> | <span data-ttu-id="02d0e-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="02d0e-131">PackageVersion</span></span> | <span data-ttu-id="02d0e-132">Version</span><span class="sxs-lookup"><span data-stu-id="02d0e-132">Version</span></span> | <span data-ttu-id="02d0e-133">"1.0.0", "1.0.0-beta" 또는 "1.0.0-beta-00345"와 같이 semver와 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="02d0e-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="02d0e-134">VersionPrefix</span></span> | <span data-ttu-id="02d0e-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="02d0e-135">PackageVersionPrefix</span></span> | <span data-ttu-id="02d0e-136">비어 있음</span><span class="sxs-lookup"><span data-stu-id="02d0e-136">empty</span></span> | <span data-ttu-id="02d0e-137">PackageVersion을 설정하면 PackageVersionPrefix를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="02d0e-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="02d0e-138">VersionSuffix</span></span> | <span data-ttu-id="02d0e-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="02d0e-139">PackageVersionSuffix</span></span> | <span data-ttu-id="02d0e-140">비어 있음</span><span class="sxs-lookup"><span data-stu-id="02d0e-140">empty</span></span> | <span data-ttu-id="02d0e-141">MSBuild의 $(VersionSuffix)입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="02d0e-142">PackageVersion을 설정하면 PackageVersionSuffix를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="02d0e-143">만든 이</span><span class="sxs-lookup"><span data-stu-id="02d0e-143">Authors</span></span> | <span data-ttu-id="02d0e-144">만든 이</span><span class="sxs-lookup"><span data-stu-id="02d0e-144">Authors</span></span> | <span data-ttu-id="02d0e-145">현재 사용자의 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="02d0e-145">Username of the current user</span></span> | |
| <span data-ttu-id="02d0e-146">Owners</span><span class="sxs-lookup"><span data-stu-id="02d0e-146">Owners</span></span> | <span data-ttu-id="02d0e-147">해당 사항 없음</span><span class="sxs-lookup"><span data-stu-id="02d0e-147">N/A</span></span> | <span data-ttu-id="02d0e-148">NuSpec에는 없음</span><span class="sxs-lookup"><span data-stu-id="02d0e-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="02d0e-149">제목</span><span class="sxs-lookup"><span data-stu-id="02d0e-149">Title</span></span> | <span data-ttu-id="02d0e-150">제목</span><span class="sxs-lookup"><span data-stu-id="02d0e-150">Title</span></span> | <span data-ttu-id="02d0e-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="02d0e-151">The PackageId</span></span>| |
| <span data-ttu-id="02d0e-152">설명</span><span class="sxs-lookup"><span data-stu-id="02d0e-152">Description</span></span> | <span data-ttu-id="02d0e-153">설명</span><span class="sxs-lookup"><span data-stu-id="02d0e-153">Description</span></span> | <span data-ttu-id="02d0e-154">"패키지 설명"</span><span class="sxs-lookup"><span data-stu-id="02d0e-154">"Package Description"</span></span> | |
| <span data-ttu-id="02d0e-155">저작권</span><span class="sxs-lookup"><span data-stu-id="02d0e-155">Copyright</span></span> | <span data-ttu-id="02d0e-156">저작권</span><span class="sxs-lookup"><span data-stu-id="02d0e-156">Copyright</span></span> | <span data-ttu-id="02d0e-157">비어 있음</span><span class="sxs-lookup"><span data-stu-id="02d0e-157">empty</span></span> | |
| <span data-ttu-id="02d0e-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="02d0e-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="02d0e-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="02d0e-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="02d0e-160">false</span><span class="sxs-lookup"><span data-stu-id="02d0e-160">false</span></span> | |
| <span data-ttu-id="02d0e-161">라이선스</span><span class="sxs-lookup"><span data-stu-id="02d0e-161">license</span></span> | <span data-ttu-id="02d0e-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="02d0e-162">PackageLicenseExpression</span></span> | <span data-ttu-id="02d0e-163">비어 있음</span><span class="sxs-lookup"><span data-stu-id="02d0e-163">empty</span></span> | <span data-ttu-id="02d0e-164">`<license type="expression">`에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="02d0e-165">라이선스</span><span class="sxs-lookup"><span data-stu-id="02d0e-165">license</span></span> | <span data-ttu-id="02d0e-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="02d0e-166">PackageLicenseFile</span></span> | <span data-ttu-id="02d0e-167">비어 있음</span><span class="sxs-lookup"><span data-stu-id="02d0e-167">empty</span></span> | <span data-ttu-id="02d0e-168">`<license type="file">`에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="02d0e-169">참조 된 라이선스 파일을 명시적으로 압축 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="02d0e-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="02d0e-170">LicenseUrl</span></span> | <span data-ttu-id="02d0e-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="02d0e-171">PackageLicenseUrl</span></span> | <span data-ttu-id="02d0e-172">비어 있음</span><span class="sxs-lookup"><span data-stu-id="02d0e-172">empty</span></span> | <span data-ttu-id="02d0e-173">`PackageLicenseUrl` 사용 되지 않습니다. PackageLicenseExpression 또는 PackageLicenseFile 속성을 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="02d0e-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="02d0e-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="02d0e-174">ProjectUrl</span></span> | <span data-ttu-id="02d0e-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="02d0e-175">PackageProjectUrl</span></span> | <span data-ttu-id="02d0e-176">비어 있음</span><span class="sxs-lookup"><span data-stu-id="02d0e-176">empty</span></span> | |
| <span data-ttu-id="02d0e-177">아이콘</span><span class="sxs-lookup"><span data-stu-id="02d0e-177">Icon</span></span> | <span data-ttu-id="02d0e-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="02d0e-178">PackageIcon</span></span> | <span data-ttu-id="02d0e-179">비어 있음</span><span class="sxs-lookup"><span data-stu-id="02d0e-179">empty</span></span> | <span data-ttu-id="02d0e-180">참조 된 아이콘 이미지 파일을 명시적으로 압축 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="02d0e-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="02d0e-181">IconUrl</span></span> | <span data-ttu-id="02d0e-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="02d0e-182">PackageIconUrl</span></span> | <span data-ttu-id="02d0e-183">비어 있음</span><span class="sxs-lookup"><span data-stu-id="02d0e-183">empty</span></span> | <span data-ttu-id="02d0e-184">최상의 하위 환경에서는 `PackageIcon`외에도 `PackageIconUrl` 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="02d0e-185">장기적으로는 `PackageIconUrl` 더 이상 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="02d0e-186">Tags</span><span class="sxs-lookup"><span data-stu-id="02d0e-186">Tags</span></span> | <span data-ttu-id="02d0e-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="02d0e-187">PackageTags</span></span> | <span data-ttu-id="02d0e-188">비어 있음</span><span class="sxs-lookup"><span data-stu-id="02d0e-188">empty</span></span> | <span data-ttu-id="02d0e-189">세미콜론으로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="02d0e-190">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="02d0e-190">ReleaseNotes</span></span> | <span data-ttu-id="02d0e-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="02d0e-191">PackageReleaseNotes</span></span> | <span data-ttu-id="02d0e-192">비어 있음</span><span class="sxs-lookup"><span data-stu-id="02d0e-192">empty</span></span> | |
| <span data-ttu-id="02d0e-193">리포지토리/u r l</span><span class="sxs-lookup"><span data-stu-id="02d0e-193">Repository/Url</span></span> | <span data-ttu-id="02d0e-194">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="02d0e-194">RepositoryUrl</span></span> | <span data-ttu-id="02d0e-195">비어 있음</span><span class="sxs-lookup"><span data-stu-id="02d0e-195">empty</span></span> | <span data-ttu-id="02d0e-196">소스 코드를 복제 하거나 검색 하는 데 사용 되는 리포지토리 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="02d0e-197">예: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="02d0e-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="02d0e-198">리포지토리/유형</span><span class="sxs-lookup"><span data-stu-id="02d0e-198">Repository/Type</span></span> | <span data-ttu-id="02d0e-199">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="02d0e-199">RepositoryType</span></span> | <span data-ttu-id="02d0e-200">비어 있음</span><span class="sxs-lookup"><span data-stu-id="02d0e-200">empty</span></span> | <span data-ttu-id="02d0e-201">리포지토리 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-201">Repository type.</span></span> <span data-ttu-id="02d0e-202">예: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="02d0e-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="02d0e-203">리포지토리/분기</span><span class="sxs-lookup"><span data-stu-id="02d0e-203">Repository/Branch</span></span> | <span data-ttu-id="02d0e-204">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="02d0e-204">RepositoryBranch</span></span> | <span data-ttu-id="02d0e-205">비어 있음</span><span class="sxs-lookup"><span data-stu-id="02d0e-205">empty</span></span> | <span data-ttu-id="02d0e-206">선택적 리포지토리 분기 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-206">Optional repository branch information.</span></span> <span data-ttu-id="02d0e-207">이 속성을 포함 하려면 *RepositoryUrl* 도 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="02d0e-208">예: *master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="02d0e-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="02d0e-209">리포지토리/커밋</span><span class="sxs-lookup"><span data-stu-id="02d0e-209">Repository/Commit</span></span> | <span data-ttu-id="02d0e-210">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="02d0e-210">RepositoryCommit</span></span> | <span data-ttu-id="02d0e-211">비어 있음</span><span class="sxs-lookup"><span data-stu-id="02d0e-211">empty</span></span> | <span data-ttu-id="02d0e-212">패키지가 빌드된 소스를 나타내는 선택적 리포지토리 커밋 또는 변경 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="02d0e-213">이 속성을 포함 하려면 *RepositoryUrl* 도 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="02d0e-214">예: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="02d0e-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="02d0e-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="02d0e-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="02d0e-216">요약</span><span class="sxs-lookup"><span data-stu-id="02d0e-216">Summary</span></span> | <span data-ttu-id="02d0e-217">지원 안 함</span><span class="sxs-lookup"><span data-stu-id="02d0e-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="02d0e-218">pack 대상 입력</span><span class="sxs-lookup"><span data-stu-id="02d0e-218">pack target inputs</span></span>

- <span data-ttu-id="02d0e-219">IsPackable</span><span class="sxs-lookup"><span data-stu-id="02d0e-219">IsPackable</span></span>
- <span data-ttu-id="02d0e-220">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="02d0e-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="02d0e-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="02d0e-221">PackageVersion</span></span>
- <span data-ttu-id="02d0e-222">PackageId</span><span class="sxs-lookup"><span data-stu-id="02d0e-222">PackageId</span></span>
- <span data-ttu-id="02d0e-223">만든 이</span><span class="sxs-lookup"><span data-stu-id="02d0e-223">Authors</span></span>
- <span data-ttu-id="02d0e-224">설명</span><span class="sxs-lookup"><span data-stu-id="02d0e-224">Description</span></span>
- <span data-ttu-id="02d0e-225">저작권</span><span class="sxs-lookup"><span data-stu-id="02d0e-225">Copyright</span></span>
- <span data-ttu-id="02d0e-226">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="02d0e-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="02d0e-227">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="02d0e-227">DevelopmentDependency</span></span>
- <span data-ttu-id="02d0e-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="02d0e-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="02d0e-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="02d0e-229">PackageLicenseFile</span></span>
- <span data-ttu-id="02d0e-230">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="02d0e-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="02d0e-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="02d0e-231">PackageProjectUrl</span></span>
- <span data-ttu-id="02d0e-232">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="02d0e-232">PackageIconUrl</span></span>
- <span data-ttu-id="02d0e-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="02d0e-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="02d0e-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="02d0e-234">PackageTags</span></span>
- <span data-ttu-id="02d0e-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="02d0e-235">PackageOutputPath</span></span>
- <span data-ttu-id="02d0e-236">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="02d0e-236">IncludeSymbols</span></span>
- <span data-ttu-id="02d0e-237">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="02d0e-237">IncludeSource</span></span>
- <span data-ttu-id="02d0e-238">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="02d0e-238">PackageTypes</span></span>
- <span data-ttu-id="02d0e-239">IsTool</span><span class="sxs-lookup"><span data-stu-id="02d0e-239">IsTool</span></span>
- <span data-ttu-id="02d0e-240">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="02d0e-240">RepositoryUrl</span></span>
- <span data-ttu-id="02d0e-241">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="02d0e-241">RepositoryType</span></span>
- <span data-ttu-id="02d0e-242">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="02d0e-242">RepositoryBranch</span></span>
- <span data-ttu-id="02d0e-243">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="02d0e-243">RepositoryCommit</span></span>
- <span data-ttu-id="02d0e-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="02d0e-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="02d0e-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="02d0e-245">MinClientVersion</span></span>
- <span data-ttu-id="02d0e-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="02d0e-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="02d0e-247">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="02d0e-247">IncludeContentInPack</span></span>
- <span data-ttu-id="02d0e-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="02d0e-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="02d0e-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="02d0e-249">ContentTargetFolders</span></span>
- <span data-ttu-id="02d0e-250">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="02d0e-250">NuspecFile</span></span>
- <span data-ttu-id="02d0e-251">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="02d0e-251">NuspecBasePath</span></span>
- <span data-ttu-id="02d0e-252">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="02d0e-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="02d0e-253">pack 시나리오</span><span class="sxs-lookup"><span data-stu-id="02d0e-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="02d0e-254">종속성 표시 안 함</span><span class="sxs-lookup"><span data-stu-id="02d0e-254">Suppress dependencies</span></span>

<span data-ttu-id="02d0e-255">생성 된 NuGet 패키지에서 패키지 종속성을 표시 하지 않으려면 생성 된 nupkg 파일에서 모든 종속성을 건너뛰도록 허용 하는 `true` `SuppressDependenciesWhenPacking`를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="02d0e-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="02d0e-256">PackageIconUrl</span></span>

<span data-ttu-id="02d0e-257">`PackageIconUrl` 새 [`PackageIcon`](#packageicon) 속성을 위해 더 이상 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="02d0e-258">NuGet 5.3 & Visual Studio 2019 버전 16.3부터 패키지 메타 데이터에서 `PackageIconUrl`만 지정 하는 경우 `pack` [NU5048](errors-and-warnings/nu5048) 경고를 발생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](errors-and-warnings/nu5048) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="02d0e-259">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="02d0e-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="02d0e-260">`PackageIcon`를 아직 지원 하지 않는 클라이언트 및 원본에 대 한 이전 버전과의 호환성을 유지 하려면 `PackageIcon`와 `PackageIconUrl`를 모두 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="02d0e-261">Visual Studio는 이후 릴리스에서 폴더 기반 원본에서 제공 되는 패키지에 대 한 `PackageIcon`를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="02d0e-262">아이콘 이미지 파일 압축</span><span class="sxs-lookup"><span data-stu-id="02d0e-262">Packing an icon image file</span></span>

<span data-ttu-id="02d0e-263">아이콘 이미지 파일을 압축 하는 경우 패키지의 루트를 기준으로 패키지 경로를 지정 하려면 `PackageIcon` 속성을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="02d0e-264">또한 파일이 패키지에 포함 되어 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="02d0e-265">이미지 파일 크기는 1mb로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="02d0e-266">지원 되는 파일 형식에는 JPEG 및 PNG가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="02d0e-267">64x64의 이미지 해상도를 권장 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-267">We recommend an image resolution of 64x64.</span></span>

<span data-ttu-id="02d0e-268">예를 들면 다음과 같습니다.:</span><span class="sxs-lookup"><span data-stu-id="02d0e-268">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="02d0e-269">[패키지 아이콘 샘플](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="02d0e-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="02d0e-270">Nuspec에 대 한 자세한 내용은 [nuspec reference에 대 한 참조를 참조](nuspec.md#icon)하세요.</span><span class="sxs-lookup"><span data-stu-id="02d0e-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="02d0e-271">출력 어셈블리</span><span class="sxs-lookup"><span data-stu-id="02d0e-271">Output assemblies</span></span>

<span data-ttu-id="02d0e-272">`nuget pack`은 `.exe`, `.dll`, `.xml`, `.winmd`, `.json` 및 `.pri` 확장명의 출력 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="02d0e-273">복사되는 출력 파일은 `BuiltOutputProjectGroup` 대상에서 제공하는 MSBuild에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="02d0e-274">프로젝트 파일 또는 명령줄에서 출력 어셈블리의 위치를 제어하는 데 사용할 수 있는 두 가지 MSBuild 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="02d0e-275">`IncludeBuildOutput`: 빌드 출력 어셈블리를 패키지에 포함할지 여부를 결정하는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="02d0e-276">`BuildOutputTargetFolder`: 출력 어셈블리를 배치할 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="02d0e-277">출력 어셈블리(및 기타 출력 파일)는 해당 프레임워크 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="02d0e-278">패키지 참조</span><span class="sxs-lookup"><span data-stu-id="02d0e-278">Package references</span></span>

<span data-ttu-id="02d0e-279">[프로젝트 파일의 패키지 참조](../consume-packages/package-references-in-project-files.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02d0e-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="02d0e-280">프로젝트 간 참조</span><span class="sxs-lookup"><span data-stu-id="02d0e-280">Project to project references</span></span>

<span data-ttu-id="02d0e-281">프로젝트 간 참조는 기본적으로 NuGet 패키지 참조로 간주됩니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="02d0e-282">또한 다음 메타데이터를 프로젝트 참조에 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="02d0e-283">패키지에 내용 포함</span><span class="sxs-lookup"><span data-stu-id="02d0e-283">Including content in a package</span></span>

<span data-ttu-id="02d0e-284">콘텐츠를 포함하려면 기존 `<Content>` 항목에 추가 메타데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="02d0e-285">기본적으로 "Content" 형식의 모든 항목은 다음과 같은 항목으로 재정의하지 않는 한 패키지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="02d0e-286">패키지 경로를 지정하지 않으면 기본적으로 `content` 및 `contentFiles\any\<target_framework>` 패키지 폴더의 루트에 모든 항목이 추가되고 상대 폴더 구조가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="02d0e-287">모든 내용을 특정 루트 폴더(`content` 및 `contentFiles` 대신)에만 복사하려면 `ContentTargetFolders` MSBuild 속성을 사용할 수 있습니다. 이 속성은 기본적으로 "content; contentFiles"이지만 다른 폴더 이름으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="02d0e-288">`ContentTargetFolders`에 "contentFiles"를 지정하면 파일이 `buildAction`에 따라 `contentFiles\any\<target_framework>` 또는 `contentFiles\<language>\<target_framework>`에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="02d0e-289">`PackagePath`는 세미콜론으로 구분된 대상 경로의 집합일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="02d0e-290">빈 패키지 경로를 지정하면 파일이 패키지의 루트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="02d0e-291">예를 들어 다음은 `libuv.txt`를 `content\myfiles`, `content\samples` 및 패키지 루트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="02d0e-292">또한 `$(IncludeContentInPack)` MSBuild 속성이 있으며 기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="02d0e-293">모든 프로젝트에서 이 값을 `false`로 설정하면 해당 프로젝트의 내용이 NuGet 패키지에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="02d0e-294">위의 항목 중 하나에서 설정할 수 있는 다른 pack 특정 메타데이터에는 nuspec 출력의 ```contentFiles``` 항목에 ```CopyToOutput``` 및 ```Flatten``` 값을 설정하는 ```<PackageCopyToOutput>``` 및 ```<PackageFlatten>```이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="02d0e-295">Content 항목 외에도, 빌드 작업이 Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource 또는 None으로 설정된 파일에 `<Pack>` 및 `<PackagePath>` 메타데이터를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="02d0e-296">GLOB 패턴을 사용할 때 pack에서 파일 이름을 패키지 경로에 추가하려면 패키지 경로가 폴더 구분 문자로 끝나야 합니다. 그렇지 않으면 패키지 경로가 파일 이름을 포함한 전체 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="02d0e-297">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="02d0e-297">IncludeSymbols</span></span>

<span data-ttu-id="02d0e-298">`MSBuild -t:pack -p:IncludeSymbols=true`를 사용하면 해당 `.pdb` 파일이 다른 출력 파일(`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`)과 함께 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="02d0e-299">`IncludeSymbols=true`를 설정하면 일반 패키지 *및* 기호 패키지가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="02d0e-300">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="02d0e-300">IncludeSource</span></span>

<span data-ttu-id="02d0e-301">`.pdb` 파일과 함께 원본 파일을 복사한다는 점을 제외하고는 `IncludeSymbols`와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="02d0e-302">`Compile` 형식의 모든 파일이 결과 패키지에서 상대 경로 폴더 구조를 유지하면서 `src\<ProjectName>\`에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="02d0e-303">또한 `TreatAsPackageReference`가 `false`로 설정된 `ProjectReference`의 원본 파일에 대해서도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="02d0e-304">Compile 형식의 파일이 프로젝트 폴더의 외부에 있는 경우 이 파일은 `src\<ProjectName>\`에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="02d0e-305">라이선스 식 또는 라이선스 파일 압축</span><span class="sxs-lookup"><span data-stu-id="02d0e-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="02d0e-306">라이선스 식을 사용할 때 PackageLicenseExpression 속성을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="02d0e-307">[라이선스 식 샘플](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="02d0e-308">[NuGet.org에서 허용 하는 라이선스 식 및 라이선스에 대해 자세히 알아보세요](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="02d0e-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="02d0e-309">라이선스 파일을 압축 하는 경우 PackageLicenseFile 속성을 사용 하 여 패키지의 루트에 상대적인 패키지 경로를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="02d0e-310">또한 파일이 패키지에 포함 되어 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="02d0e-311">예를 들면 다음과 같습니다.:</span><span class="sxs-lookup"><span data-stu-id="02d0e-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="02d0e-312">[라이선스 파일 샘플](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="02d0e-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="02d0e-313">IsTool</span><span class="sxs-lookup"><span data-stu-id="02d0e-313">IsTool</span></span>

<span data-ttu-id="02d0e-314">`MSBuild -t:pack -p:IsTool=true`를 사용하면 [출력 어셈블리](#output-assemblies) 시나리오에서 지정한 대로 모든 출력 파일이 `lib` 폴더 대신 `tools` 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-314">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="02d0e-315">이는 `.csproj` 파일에서 `PackageType`을 설정하여 지정된 `DotNetCliTool`과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-315">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="02d0e-316">.nuspec을 사용하여 압축</span><span class="sxs-lookup"><span data-stu-id="02d0e-316">Packing using a .nuspec</span></span>

<span data-ttu-id="02d0e-317">일반적으로 `.nuspec` 파일에 있는 [모든 속성](../reference/msbuild-targets.md#pack-target) 을 프로젝트 파일에 포함 하는 것이 좋지만 `.nuspec` 파일을 사용 하 여 프로젝트를 압축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-317">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="02d0e-318">`PackageReference`를 사용 하는 비 SDK 스타일 프로젝트의 경우 pack 작업을 실행할 수 있도록 `NuGet.Build.Tasks.Pack.targets` 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-318">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="02d0e-319">여전히 프로젝트를 복원 해야 nuspec 파일을 압축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-319">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="02d0e-320">SDK 스타일 프로젝트는 기본적으로 pack 대상을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-320">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="02d0e-321">프로젝트 파일의 대상 프레임 워크는 관련이 없으며 nuspec을 압축 하는 경우에는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-321">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="02d0e-322">다음 세 가지 MSBuild 속성은 `.nuspec`을 사용하여 압축하는 것과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-322">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="02d0e-323">`NuspecFile`: 압축에 사용되는 `.nuspec` 파일에 대한 상대 또는 절대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-323">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="02d0e-324">`NuspecProperties`: 세미콜론으로 구분된 key=value 쌍의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-324">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="02d0e-325">MSBuild 명령줄 구문 분석이 작동하는 방식으로 인해 여러 속성을 `-p:NuspecProperties=\"key1=value1;key2=value2\"`와 같이 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-325">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="02d0e-326">`NuspecBasePath`: `.nuspec` 파일에 대한 기본 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-326">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="02d0e-327">`dotnet.exe`를 사용하여 프로젝트를 압축하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-327">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="02d0e-328">MSBuild를 사용하여 프로젝트를 압축하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-328">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="02d0e-329">Dotnet 또는 msbuild를 사용 하 여 nuspec을 압축 하면 기본적으로 프로젝트를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-329">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="02d0e-330">프로젝트 파일에 ```<IncludeBuildOutput>false</IncludeBuildOutput> ```를 설정 하는 것과 함께 프로젝트 파일에 ```<NoBuild>true</NoBuild> ```를 설정 하는 것과 동일한 dotnet에 ```--no-build``` 속성을 전달 하 여이를 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-330">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="02d0e-331">Nuspec 파일을 압축 하는 *.csproj* 파일의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-331">An example of a *.csproj* file to pack a nuspec file is:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="02d0e-332">사용자 지정 된 패키지를 만들기 위한 고급 확장 끝점</span><span class="sxs-lookup"><span data-stu-id="02d0e-332">Advanced extension points to create customized package</span></span>

<span data-ttu-id="02d0e-333">`pack` 대상은 내부, 대상 프레임 워크 특정 빌드에서 실행 되는 두 개의 확장 지점이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-333">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="02d0e-334">확장 지점은 대상 프레임 워크 관련 콘텐츠 및 어셈블리를 패키지에 포함 하 여 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-334">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="02d0e-335">`TargetsForTfmSpecificBuildOutput` 대상: `lib` 폴더 내의 파일 또는 `BuildOutputTargetFolder`를 사용 하 여 지정 된 폴더에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-335">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="02d0e-336">`TargetsForTfmSpecificContentInPackage` 대상: `BuildOutputTargetFolder`외부의 파일에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-336">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="02d0e-337">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="02d0e-337">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="02d0e-338">사용자 지정 대상을 작성 하 고이를 `$(TargetsForTfmSpecificBuildOutput)` 속성의 값으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-338">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="02d0e-339">`BuildOutputTargetFolder` (기본적으로 lib)로 이동 해야 하는 모든 파일의 경우 대상은 해당 파일을 ItemGroup `BuildOutputInPackage`에 쓰고 다음 두 메타 데이터 값을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-339">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="02d0e-340">`FinalOutputPath`: 파일의 절대 경로입니다. 제공 하지 않으면 Id가 원본 경로를 평가 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-340">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="02d0e-341">`TargetPath`: (선택 사항) 각 culture 폴더 아래에 있는 위성 어셈블리와 같이 파일을 `lib\<TargetFramework>` 내의 하위 폴더로 이동 해야 하는 경우에 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-341">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="02d0e-342">기본값은 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-342">Defaults to the name of the file.</span></span>

<span data-ttu-id="02d0e-343">예:</span><span class="sxs-lookup"><span data-stu-id="02d0e-343">Example:</span></span>

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="02d0e-344">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="02d0e-344">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="02d0e-345">사용자 지정 대상을 작성 하 고이를 `$(TargetsForTfmSpecificContentInPackage)` 속성의 값으로 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-345">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="02d0e-346">패키지에 포함할 파일의 경우 대상은 해당 파일을 ItemGroup `TfmSpecificPackageFile`에 쓰고 다음과 같은 선택적 메타 데이터를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-346">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="02d0e-347">`PackagePath`: 패키지에서 파일이 출력 되어야 하는 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-347">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="02d0e-348">동일한 패키지 경로에 두 개 이상의 파일이 추가 되 면 NuGet에서 경고를 발생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-348">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="02d0e-349">`BuildAction`: 파일에 할당할 빌드 작업으로, 패키지 경로가 `contentFiles` 폴더에 있는 경우에만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-349">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="02d0e-350">기본값은 "None"입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-350">Defaults to "None".</span></span>

<span data-ttu-id="02d0e-351">예를 들어</span><span class="sxs-lookup"><span data-stu-id="02d0e-351">An example:</span></span>
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a><span data-ttu-id="02d0e-352">restore 대상</span><span class="sxs-lookup"><span data-stu-id="02d0e-352">restore target</span></span>

<span data-ttu-id="02d0e-353">`MSBuild -t:restore`(.NET Core 프로젝트에서 `nuget restore` 및 `dotnet restore` 사용)는 프로젝트 파일에서 참조된 패키지를 다음과 같이 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-353">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="02d0e-354">모든 프로젝트 간 참조를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-354">Read all project to project references</span></span>
1. <span data-ttu-id="02d0e-355">프로젝트 속성을 읽어 중간 폴더 및 대상 프레임워크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-355">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="02d0e-356">MSBuild 데이터를 Nuget.exe에 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-356">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="02d0e-357">restore를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-357">Run restore</span></span>
1. <span data-ttu-id="02d0e-358">패키지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-358">Download packages</span></span>
1. <span data-ttu-id="02d0e-359">자산, targets 및 props 파일을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-359">Write assets file, targets, and props</span></span>

<span data-ttu-id="02d0e-360">`restore` 대상은 PackageReference 형식을 사용 하는 프로젝트에 **만** 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-360">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="02d0e-361">`packages.config` 형식을 사용 하는 프로젝트에 대해서는 작동 **하지** 않습니다. 대신 [nuget 복원을](../reference/cli-reference/cli-ref-restore.md) 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="02d0e-361">It does **not** work for projects using the `packages.config` format; use [nuget restore](../reference/cli-reference/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="02d0e-362">restore 속성</span><span class="sxs-lookup"><span data-stu-id="02d0e-362">Restore properties</span></span>

<span data-ttu-id="02d0e-363">추가 restore 설정은 프로젝트 파일의 MSBuild 속성에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-363">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="02d0e-364">또한 값은 `-p:` 스위치를 사용하여 명령줄에서 설정할 수 있습니다(아래 예제 참조).</span><span class="sxs-lookup"><span data-stu-id="02d0e-364">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="02d0e-365">속성</span><span class="sxs-lookup"><span data-stu-id="02d0e-365">Property</span></span> | <span data-ttu-id="02d0e-366">설명</span><span class="sxs-lookup"><span data-stu-id="02d0e-366">Description</span></span> |
|--------|--------|
| <span data-ttu-id="02d0e-367">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="02d0e-367">RestoreSources</span></span> | <span data-ttu-id="02d0e-368">세미콜론으로 구분된 패키지 원본의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-368">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="02d0e-369">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="02d0e-369">RestorePackagesPath</span></span> | <span data-ttu-id="02d0e-370">사용자 패키지 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-370">User packages folder path.</span></span> |
| <span data-ttu-id="02d0e-371">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="02d0e-371">RestoreDisableParallel</span></span> | <span data-ttu-id="02d0e-372">다운로드를 한 번에 하나씩으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-372">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="02d0e-373">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="02d0e-373">RestoreConfigFile</span></span> | <span data-ttu-id="02d0e-374">적용할 `Nuget.Config` 파일에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-374">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="02d0e-375">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="02d0e-375">RestoreNoCache</span></span> | <span data-ttu-id="02d0e-376">True 이면 캐시 된 패키지를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-376">If true, avoids using cached packages.</span></span> <span data-ttu-id="02d0e-377">[전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="02d0e-377">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="02d0e-378">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="02d0e-378">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="02d0e-379">true이면 실패했거나 누락된 패키지 원본을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-379">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="02d0e-380">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="02d0e-380">RestoreFallbackFolders</span></span> | <span data-ttu-id="02d0e-381">사용자 패키지 폴더를 사용 하는 것과 같은 방식으로 사용 되는 대체 (Fallback) 폴더</span><span class="sxs-lookup"><span data-stu-id="02d0e-381">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="02d0e-382">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="02d0e-382">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="02d0e-383">복원 하는 동안 사용할 추가 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-383">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="02d0e-384">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="02d0e-384">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="02d0e-385">복원 중에 사용할 추가 대체 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-385">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="02d0e-386">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="02d0e-386">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="02d0e-387">`RestoreAdditionalProjectFallbackFolders`에 지정 된 대체 폴더를 제외 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-387">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="02d0e-388">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="02d0e-388">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="02d0e-389">`NuGet.Build.Tasks.dll`에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-389">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="02d0e-390">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="02d0e-390">RestoreGraphProjectInput</span></span> | <span data-ttu-id="02d0e-391">세미콜론으로 구분된 복원할 프로젝트의 목록이며, 절대 경로가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-391">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="02d0e-392">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="02d0e-392">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="02d0e-393">MSBuild를 통해 프로젝트를 수집 하는 경우 `SkipNonexistentTargets` 최적화를 사용 하 여 해당 프로젝트를 수집할지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-393">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="02d0e-394">설정하지 않으면 기본값은 `true`으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-394">When not set, defaults to `true`.</span></span> <span data-ttu-id="02d0e-395">결과는 프로젝트의 대상을 가져올 수 없는 경우의 빠른 오류 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-395">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="02d0e-396">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="02d0e-396">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="02d0e-397">출력 폴더, 기본적으로 `BaseIntermediateOutputPath` 및 `obj` 폴더를 기본값으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-397">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="02d0e-398">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="02d0e-398">RestoreForce</span></span> | <span data-ttu-id="02d0e-399">PackageReference 기반 프로젝트에서 마지막 복원이 성공한 경우에도 모든 종속성이 확인 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-399">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="02d0e-400">이 플래그를 지정 하는 것은 `project.assets.json` 파일을 삭제 하는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-400">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="02d0e-401">이는 http 캐시를 우회 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-401">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="02d0e-402">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="02d0e-402">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="02d0e-403">잠금 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-403">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="02d0e-404">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="02d0e-404">RestoreLockedMode</span></span> | <span data-ttu-id="02d0e-405">잠금 모드에서 복원을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-405">Run restore in locked mode.</span></span> <span data-ttu-id="02d0e-406">즉, 복원은 종속성을 다시 평가 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-406">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="02d0e-407">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="02d0e-407">NuGetLockFilePath</span></span> | <span data-ttu-id="02d0e-408">잠금 파일의 사용자 지정 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-408">A custom location for the lock file.</span></span> <span data-ttu-id="02d0e-409">기본 위치는 프로젝트 옆에 있고 `packages.lock.json`이름이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-409">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="02d0e-410">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="02d0e-410">RestoreForceEvaluate</span></span> | <span data-ttu-id="02d0e-411">강제로 복원 하 여 종속성을 다시 계산 하 고 경고 없이 잠금 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-411">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> | 

#### <a name="examples"></a><span data-ttu-id="02d0e-412">예</span><span class="sxs-lookup"><span data-stu-id="02d0e-412">Examples</span></span>

<span data-ttu-id="02d0e-413">명령줄:</span><span class="sxs-lookup"><span data-stu-id="02d0e-413">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="02d0e-414">프로젝트 파일:</span><span class="sxs-lookup"><span data-stu-id="02d0e-414">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="02d0e-415">restore 출력</span><span class="sxs-lookup"><span data-stu-id="02d0e-415">Restore outputs</span></span>

<span data-ttu-id="02d0e-416">restore는 `obj` 빌드 폴더에 다음 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-416">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="02d0e-417">File</span><span class="sxs-lookup"><span data-stu-id="02d0e-417">File</span></span> | <span data-ttu-id="02d0e-418">설명</span><span class="sxs-lookup"><span data-stu-id="02d0e-418">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="02d0e-419">모든 패키지 참조의 종속성 그래프를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-419">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="02d0e-420">패키지에 포함된 MSBuild props 파일에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="02d0e-420">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="02d0e-421">패키지에 포함된 MSBuild targets 파일에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="02d0e-421">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="02d0e-422">하나의 MSBuild 명령을 사용 하 여 복원 및 빌드</span><span class="sxs-lookup"><span data-stu-id="02d0e-422">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="02d0e-423">NuGet은 MSBuild 대상 및 props을 가져오는 패키지를 복원할 수 있으므로 다른 전역 속성을 사용 하 여 복원 및 빌드 평가가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-423">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="02d0e-424">즉, 다음은 예측할 수 없으며 종종 잘못 된 동작을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-424">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="02d0e-425">대신에 권장 되는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-425">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="02d0e-426">`build`와 유사한 다른 대상에도 동일한 논리가 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-426">The same logic applies to other targets similar to `build`.</span></span>

### <a name="packagetargetfallback"></a><span data-ttu-id="02d0e-427">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="02d0e-427">PackageTargetFallback</span></span>

<span data-ttu-id="02d0e-428">`PackageTargetFallback` 요소를 사용하면 패키지를 복원할 때 사용할 호환 가능한 대상 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-428">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="02d0e-429">dotnet [TxM](../reference/target-frameworks.md)을 사용하는 패키지가 dotnet TxM을 선언하지 않은 호환 패키지와 함께 작동하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-429">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="02d0e-430">즉 프로젝트에서 dotnet TxM을 사용하는 경우, 비dotnet 플랫폼이 dotnet과 호환될 수 있도록 이상 프로젝트에 `<PackageTargetFallback>`을 추가하지 않는 한, 종속되는 모든 패키지에도 dotnet TxM이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-430">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="02d0e-431">예를 들어 프로젝트에서 `netstandard1.6` TxM을 사용하고 종속 패키지에 `lib/net45/a.dll` 및 `lib/portable-net45+win81/a.dll`만 포함되어 있으면 프로젝트 빌드에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-431">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="02d0e-432">가져오려는 항목이 후자의 DLL이면 다음과 같이 `PackageTargetFallback`을 추가하여 `portable-net45+win81` DLL이 호환 가능하다고 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-432">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="02d0e-433">프로젝트의 모든 대상에 대해 대체(fallback)를 선언하려면 `Condition` 특성을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-433">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="02d0e-434">또한 다음과 같이 `$(PackageTargetFallback)`을 포함하여 기존 `PackageTargetFallback`을 확장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-434">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="02d0e-435">복원 그래프에서 단일 라이브러리 대체</span><span class="sxs-lookup"><span data-stu-id="02d0e-435">Replacing one library from a restore graph</span></span>

<span data-ttu-id="02d0e-436">restore에서 잘못된 어셈블리를 가져오는 경우 해당 패키지의 기본 선택 항목을 제외하는 한편 원하는 선택 항목으로 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-436">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="02d0e-437">먼저 최상위 `PackageReference`를 사용하여 모든 자산을 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-437">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="02d0e-438">그런 다음 DLL의 적절한 로컬 복사본에 대한 고유한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="02d0e-438">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
