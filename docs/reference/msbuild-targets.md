---
title: MSBuild 대상으로서의 NuGet pack 및 restore
description: NuGet pack 및 restore는 NuGet 4.0 이상에서 MSBuild 대상으로 직접 작동할 수 있습니다.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 7de3f0f1133a89848e9268d489751293fb3cbf25
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235700"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="c05ed-103">MSBuild 대상으로서의 NuGet pack 및 restore</span><span class="sxs-lookup"><span data-stu-id="c05ed-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="c05ed-104">*NuGet 4.0 이상*</span><span class="sxs-lookup"><span data-stu-id="c05ed-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="c05ed-105">[PackageReference](../consume-packages/package-references-in-project-files.md) 형식을 사용 하는 경우 NuGet 4.0 이상에서는 별도의 파일을 사용 하지 않고 프로젝트 파일 내에 모든 매니페스트 메타 데이터를 직접 저장할 수 있습니다 `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="c05ed-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="c05ed-106">MSBuild 15.1 이상에서 NuGet은 아래에서 설명한 대로 `pack` 및 `restore` 대상이 있는 일류 MSBuild 시민이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="c05ed-107">이러한 대상을 사용하면 다른 MSBuild 작업 또는 대상과 마찬가지로 NuGet을 사용하여 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="c05ed-108">MSBuild를 사용 하 여 NuGet 패키지를 만드는 방법에 대 한 지침은 [msbuild를 사용 하 여 nuget 패키지 만들기](../create-packages/creating-a-package-msbuild.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c05ed-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="c05ed-109">(NuGet 3.x 및 이전 버전의 경우 NuGet CLI를 통해 [pack](../reference/cli-reference/cli-ref-pack.md) 및 [restore](../reference/cli-reference/cli-ref-restore.md) 명령을 대신 사용합니다.)</span><span class="sxs-lookup"><span data-stu-id="c05ed-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="c05ed-110">대상 빌드 순서</span><span class="sxs-lookup"><span data-stu-id="c05ed-110">Target build order</span></span>

<span data-ttu-id="c05ed-111">`pack` 및 `restore`는 MSBuild 대상이므로 이 대상에 액세스하여 워크플로를 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="c05ed-112">예를 들어 패키지를 압축한 후 네트워크 공유에 복사한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="c05ed-113">이렇게 하려면 프로젝트 파일에 다음을 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="c05ed-114">마찬가지로, MSBuild 작업을 작성하고, 고유한 대상을 작성하고, MSBuild 작업에서 NuGet 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="c05ed-115">`$(OutputPath)` 는 상대적 이며 프로젝트 루트에서 명령을 실행 하는 것으로 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="c05ed-116">pack 대상</span><span class="sxs-lookup"><span data-stu-id="c05ed-116">pack target</span></span>

<span data-ttu-id="c05ed-117">PackageReference 형식을 사용 하는 .NET Standard 프로젝트의 경우를 사용 하 여 `msbuild -t:pack` NuGet 패키지를 만드는 데 사용할 프로젝트 파일의 입력을 그립니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-117">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="c05ed-118">아래 표에서는 첫 번째 `<PropertyGroup>` 노드 내에서 프로젝트 파일에 추가할 수 있는 MSBuild 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-118">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="c05ed-119">Visual Studio 2017 이상에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **{project_name} 편집** 을 선택하여 이러한 편집 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="c05ed-120">편의상 테이블은 [ `.nuspec` 파일](../reference/nuspec.md)의 해당 속성을 기준으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-120">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="c05ed-121">`.nuspec`의 `Owners` 및 `Summary` 속성은 MSBuild에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="c05ed-122">특성/NuSpec 값</span><span class="sxs-lookup"><span data-stu-id="c05ed-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="c05ed-123">MSBuild 속성</span><span class="sxs-lookup"><span data-stu-id="c05ed-123">MSBuild Property</span></span> | <span data-ttu-id="c05ed-124">기본값</span><span class="sxs-lookup"><span data-stu-id="c05ed-124">Default</span></span> | <span data-ttu-id="c05ed-125">참고</span><span class="sxs-lookup"><span data-stu-id="c05ed-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="c05ed-126">Id</span><span class="sxs-lookup"><span data-stu-id="c05ed-126">Id</span></span> | <span data-ttu-id="c05ed-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="c05ed-127">PackageId</span></span> | <span data-ttu-id="c05ed-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="c05ed-128">AssemblyName</span></span> | <span data-ttu-id="c05ed-129">MSBuild의 $(AssemblyName)입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="c05ed-130">버전</span><span class="sxs-lookup"><span data-stu-id="c05ed-130">Version</span></span> | <span data-ttu-id="c05ed-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="c05ed-131">PackageVersion</span></span> | <span data-ttu-id="c05ed-132">버전</span><span class="sxs-lookup"><span data-stu-id="c05ed-132">Version</span></span> | <span data-ttu-id="c05ed-133">"1.0.0", "1.0.0-beta" 또는 "1.0.0-beta-00345"와 같이 semver와 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="c05ed-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="c05ed-134">VersionPrefix</span></span> | <span data-ttu-id="c05ed-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="c05ed-135">PackageVersionPrefix</span></span> | <span data-ttu-id="c05ed-136">비어 있음</span><span class="sxs-lookup"><span data-stu-id="c05ed-136">empty</span></span> | <span data-ttu-id="c05ed-137">PackageVersion을 설정하면 PackageVersionPrefix를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="c05ed-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="c05ed-138">VersionSuffix</span></span> | <span data-ttu-id="c05ed-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="c05ed-139">PackageVersionSuffix</span></span> | <span data-ttu-id="c05ed-140">비어 있음</span><span class="sxs-lookup"><span data-stu-id="c05ed-140">empty</span></span> | <span data-ttu-id="c05ed-141">MSBuild의 $(VersionSuffix)입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="c05ed-142">PackageVersion을 설정하면 PackageVersionSuffix를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="c05ed-143">Authors</span><span class="sxs-lookup"><span data-stu-id="c05ed-143">Authors</span></span> | <span data-ttu-id="c05ed-144">Authors</span><span class="sxs-lookup"><span data-stu-id="c05ed-144">Authors</span></span> | <span data-ttu-id="c05ed-145">현재 사용자의 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="c05ed-145">Username of the current user</span></span> | |
| <span data-ttu-id="c05ed-146">소유자</span><span class="sxs-lookup"><span data-stu-id="c05ed-146">Owners</span></span> | <span data-ttu-id="c05ed-147">해당 없음</span><span class="sxs-lookup"><span data-stu-id="c05ed-147">N/A</span></span> | <span data-ttu-id="c05ed-148">NuSpec에는 없음</span><span class="sxs-lookup"><span data-stu-id="c05ed-148">Not present in NuSpec</span></span> | |
| <span data-ttu-id="c05ed-149">제목</span><span class="sxs-lookup"><span data-stu-id="c05ed-149">Title</span></span> | <span data-ttu-id="c05ed-150">제목</span><span class="sxs-lookup"><span data-stu-id="c05ed-150">Title</span></span> | <span data-ttu-id="c05ed-151">PackageId</span><span class="sxs-lookup"><span data-stu-id="c05ed-151">The PackageId</span></span>| |
| <span data-ttu-id="c05ed-152">Description</span><span class="sxs-lookup"><span data-stu-id="c05ed-152">Description</span></span> | <span data-ttu-id="c05ed-153">Description</span><span class="sxs-lookup"><span data-stu-id="c05ed-153">Description</span></span> | <span data-ttu-id="c05ed-154">"패키지 설명"</span><span class="sxs-lookup"><span data-stu-id="c05ed-154">"Package Description"</span></span> | |
| <span data-ttu-id="c05ed-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="c05ed-155">Copyright</span></span> | <span data-ttu-id="c05ed-156">Copyright</span><span class="sxs-lookup"><span data-stu-id="c05ed-156">Copyright</span></span> | <span data-ttu-id="c05ed-157">비어 있음</span><span class="sxs-lookup"><span data-stu-id="c05ed-157">empty</span></span> | |
| <span data-ttu-id="c05ed-158">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="c05ed-158">RequireLicenseAcceptance</span></span> | <span data-ttu-id="c05ed-159">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="c05ed-159">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="c05ed-160">false</span><span class="sxs-lookup"><span data-stu-id="c05ed-160">false</span></span> | |
| <span data-ttu-id="c05ed-161">license</span><span class="sxs-lookup"><span data-stu-id="c05ed-161">license</span></span> | <span data-ttu-id="c05ed-162">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="c05ed-162">PackageLicenseExpression</span></span> | <span data-ttu-id="c05ed-163">비어 있음</span><span class="sxs-lookup"><span data-stu-id="c05ed-163">empty</span></span> | <span data-ttu-id="c05ed-164">`<license type="expression">`에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-164">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="c05ed-165">license</span><span class="sxs-lookup"><span data-stu-id="c05ed-165">license</span></span> | <span data-ttu-id="c05ed-166">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="c05ed-166">PackageLicenseFile</span></span> | <span data-ttu-id="c05ed-167">비어 있음</span><span class="sxs-lookup"><span data-stu-id="c05ed-167">empty</span></span> | <span data-ttu-id="c05ed-168">`<license type="file">`에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-168">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="c05ed-169">참조 된 라이선스 파일을 명시적으로 압축 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-169">You need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="c05ed-170">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="c05ed-170">LicenseUrl</span></span> | <span data-ttu-id="c05ed-171">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="c05ed-171">PackageLicenseUrl</span></span> | <span data-ttu-id="c05ed-172">비어 있음</span><span class="sxs-lookup"><span data-stu-id="c05ed-172">empty</span></span> | <span data-ttu-id="c05ed-173">`PackageLicenseUrl` 는 사용 되지 않습니다. PackageLicenseExpression 또는 PackageLicenseFile 속성을 사용 하십시오.</span><span class="sxs-lookup"><span data-stu-id="c05ed-173">`PackageLicenseUrl` is deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="c05ed-174">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="c05ed-174">ProjectUrl</span></span> | <span data-ttu-id="c05ed-175">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="c05ed-175">PackageProjectUrl</span></span> | <span data-ttu-id="c05ed-176">비어 있음</span><span class="sxs-lookup"><span data-stu-id="c05ed-176">empty</span></span> | |
| <span data-ttu-id="c05ed-177">아이콘</span><span class="sxs-lookup"><span data-stu-id="c05ed-177">Icon</span></span> | <span data-ttu-id="c05ed-178">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="c05ed-178">PackageIcon</span></span> | <span data-ttu-id="c05ed-179">비어 있음</span><span class="sxs-lookup"><span data-stu-id="c05ed-179">empty</span></span> | <span data-ttu-id="c05ed-180">참조 된 아이콘 이미지 파일을 명시적으로 압축 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-180">You need to explicitly pack the referenced icon image file.</span></span>|
| <span data-ttu-id="c05ed-181">IconUrl</span><span class="sxs-lookup"><span data-stu-id="c05ed-181">IconUrl</span></span> | <span data-ttu-id="c05ed-182">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="c05ed-182">PackageIconUrl</span></span> | <span data-ttu-id="c05ed-183">비어 있음</span><span class="sxs-lookup"><span data-stu-id="c05ed-183">empty</span></span> | <span data-ttu-id="c05ed-184">최상의 하위 환경에서는를 `PackageIconUrl` 추가로 지정 해야 `PackageIcon` 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-184">For the best downlevel experience, `PackageIconUrl` should be specified in addition to `PackageIcon`.</span></span> <span data-ttu-id="c05ed-185">장기적으로 `PackageIconUrl` 는 더 이상 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-185">Longer term, `PackageIconUrl` will be deprecated.</span></span> |
| <span data-ttu-id="c05ed-186">태그</span><span class="sxs-lookup"><span data-stu-id="c05ed-186">Tags</span></span> | <span data-ttu-id="c05ed-187">PackageTags</span><span class="sxs-lookup"><span data-stu-id="c05ed-187">PackageTags</span></span> | <span data-ttu-id="c05ed-188">비어 있음</span><span class="sxs-lookup"><span data-stu-id="c05ed-188">empty</span></span> | <span data-ttu-id="c05ed-189">세미콜론으로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-189">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="c05ed-190">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="c05ed-190">ReleaseNotes</span></span> | <span data-ttu-id="c05ed-191">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="c05ed-191">PackageReleaseNotes</span></span> | <span data-ttu-id="c05ed-192">비어 있음</span><span class="sxs-lookup"><span data-stu-id="c05ed-192">empty</span></span> | |
| <span data-ttu-id="c05ed-193">리포지토리/u r l</span><span class="sxs-lookup"><span data-stu-id="c05ed-193">Repository/Url</span></span> | <span data-ttu-id="c05ed-194">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="c05ed-194">RepositoryUrl</span></span> | <span data-ttu-id="c05ed-195">비어 있음</span><span class="sxs-lookup"><span data-stu-id="c05ed-195">empty</span></span> | <span data-ttu-id="c05ed-196">소스 코드를 복제 하거나 검색 하는 데 사용 되는 리포지토리 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-196">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="c05ed-197">예 들어 *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="c05ed-197">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="c05ed-198">리포지토리/유형</span><span class="sxs-lookup"><span data-stu-id="c05ed-198">Repository/Type</span></span> | <span data-ttu-id="c05ed-199">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="c05ed-199">RepositoryType</span></span> | <span data-ttu-id="c05ed-200">비어 있음</span><span class="sxs-lookup"><span data-stu-id="c05ed-200">empty</span></span> | <span data-ttu-id="c05ed-201">리포지토리 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-201">Repository type.</span></span> <span data-ttu-id="c05ed-202">예: *git*, *tfs*.</span><span class="sxs-lookup"><span data-stu-id="c05ed-202">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="c05ed-203">리포지토리/분기</span><span class="sxs-lookup"><span data-stu-id="c05ed-203">Repository/Branch</span></span> | <span data-ttu-id="c05ed-204">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="c05ed-204">RepositoryBranch</span></span> | <span data-ttu-id="c05ed-205">비어 있음</span><span class="sxs-lookup"><span data-stu-id="c05ed-205">empty</span></span> | <span data-ttu-id="c05ed-206">선택적 리포지토리 분기 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-206">Optional repository branch information.</span></span> <span data-ttu-id="c05ed-207">이 속성을 포함 하려면 *RepositoryUrl* 도 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-207">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="c05ed-208">예: *master* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="c05ed-208">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="c05ed-209">리포지토리/커밋</span><span class="sxs-lookup"><span data-stu-id="c05ed-209">Repository/Commit</span></span> | <span data-ttu-id="c05ed-210">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="c05ed-210">RepositoryCommit</span></span> | <span data-ttu-id="c05ed-211">비어 있음</span><span class="sxs-lookup"><span data-stu-id="c05ed-211">empty</span></span> | <span data-ttu-id="c05ed-212">패키지가 빌드된 소스를 나타내는 선택적 리포지토리 커밋 또는 변경 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-212">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="c05ed-213">이 속성을 포함 하려면 *RepositoryUrl* 도 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-213">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="c05ed-214">예: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +)</span><span class="sxs-lookup"><span data-stu-id="c05ed-214">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="c05ed-215">PackageType</span><span class="sxs-lookup"><span data-stu-id="c05ed-215">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="c05ed-216">요약</span><span class="sxs-lookup"><span data-stu-id="c05ed-216">Summary</span></span> | <span data-ttu-id="c05ed-217">지원 안 함</span><span class="sxs-lookup"><span data-stu-id="c05ed-217">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="c05ed-218">pack 대상 입력</span><span class="sxs-lookup"><span data-stu-id="c05ed-218">pack target inputs</span></span>

- <span data-ttu-id="c05ed-219">IsPackable</span><span class="sxs-lookup"><span data-stu-id="c05ed-219">IsPackable</span></span>
- <span data-ttu-id="c05ed-220">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="c05ed-220">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="c05ed-221">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="c05ed-221">PackageVersion</span></span>
- <span data-ttu-id="c05ed-222">PackageId</span><span class="sxs-lookup"><span data-stu-id="c05ed-222">PackageId</span></span>
- <span data-ttu-id="c05ed-223">Authors</span><span class="sxs-lookup"><span data-stu-id="c05ed-223">Authors</span></span>
- <span data-ttu-id="c05ed-224">설명</span><span class="sxs-lookup"><span data-stu-id="c05ed-224">Description</span></span>
- <span data-ttu-id="c05ed-225">Copyright</span><span class="sxs-lookup"><span data-stu-id="c05ed-225">Copyright</span></span>
- <span data-ttu-id="c05ed-226">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="c05ed-226">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="c05ed-227">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="c05ed-227">DevelopmentDependency</span></span>
- <span data-ttu-id="c05ed-228">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="c05ed-228">PackageLicenseExpression</span></span>
- <span data-ttu-id="c05ed-229">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="c05ed-229">PackageLicenseFile</span></span>
- <span data-ttu-id="c05ed-230">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="c05ed-230">PackageLicenseUrl</span></span>
- <span data-ttu-id="c05ed-231">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="c05ed-231">PackageProjectUrl</span></span>
- <span data-ttu-id="c05ed-232">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="c05ed-232">PackageIconUrl</span></span>
- <span data-ttu-id="c05ed-233">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="c05ed-233">PackageReleaseNotes</span></span>
- <span data-ttu-id="c05ed-234">PackageTags</span><span class="sxs-lookup"><span data-stu-id="c05ed-234">PackageTags</span></span>
- <span data-ttu-id="c05ed-235">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="c05ed-235">PackageOutputPath</span></span>
- <span data-ttu-id="c05ed-236">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="c05ed-236">IncludeSymbols</span></span>
- <span data-ttu-id="c05ed-237">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="c05ed-237">IncludeSource</span></span>
- <span data-ttu-id="c05ed-238">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="c05ed-238">PackageTypes</span></span>
- <span data-ttu-id="c05ed-239">IsTool</span><span class="sxs-lookup"><span data-stu-id="c05ed-239">IsTool</span></span>
- <span data-ttu-id="c05ed-240">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="c05ed-240">RepositoryUrl</span></span>
- <span data-ttu-id="c05ed-241">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="c05ed-241">RepositoryType</span></span>
- <span data-ttu-id="c05ed-242">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="c05ed-242">RepositoryBranch</span></span>
- <span data-ttu-id="c05ed-243">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="c05ed-243">RepositoryCommit</span></span>
- <span data-ttu-id="c05ed-244">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="c05ed-244">NoPackageAnalysis</span></span>
- <span data-ttu-id="c05ed-245">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="c05ed-245">MinClientVersion</span></span>
- <span data-ttu-id="c05ed-246">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="c05ed-246">IncludeBuildOutput</span></span>
- <span data-ttu-id="c05ed-247">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="c05ed-247">IncludeContentInPack</span></span>
- <span data-ttu-id="c05ed-248">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="c05ed-248">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="c05ed-249">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="c05ed-249">ContentTargetFolders</span></span>
- <span data-ttu-id="c05ed-250">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="c05ed-250">NuspecFile</span></span>
- <span data-ttu-id="c05ed-251">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="c05ed-251">NuspecBasePath</span></span>
- <span data-ttu-id="c05ed-252">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="c05ed-252">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="c05ed-253">pack 시나리오</span><span class="sxs-lookup"><span data-stu-id="c05ed-253">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="c05ed-254">종속성 표시 안 함</span><span class="sxs-lookup"><span data-stu-id="c05ed-254">Suppress dependencies</span></span>

<span data-ttu-id="c05ed-255">생성 된 NuGet 패키지에서 패키지 종속성을 표시 하지 `SuppressDependenciesWhenPacking` 않으려면 `true` 생성 된 nupkg 파일에서 모든 종속성을 건너뛰도록 허용 하는을로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-255">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="c05ed-256">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="c05ed-256">PackageIconUrl</span></span>

<span data-ttu-id="c05ed-257">`PackageIconUrl` 는 새로운 속성을 위해 더 이상 사용 되지 않습니다 [`PackageIcon`](#packageicon) .</span><span class="sxs-lookup"><span data-stu-id="c05ed-257">`PackageIconUrl` will be deprecated in favor of the new [`PackageIcon`](#packageicon) property.</span></span>

<span data-ttu-id="c05ed-258">NuGet 5.3 & Visual Studio 2019 버전 16.3부터 `pack` 패키지 메타 데이터에서만 지정 하는 경우 [NU5048](./errors-and-warnings/nu5048.md) 경고가 발생 합니다 `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="c05ed-258">Starting with NuGet 5.3 & Visual Studio 2019 version 16.3, `pack` will raise [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="c05ed-259">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="c05ed-259">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="c05ed-260">`PackageIcon` `PackageIconUrl` 아직 지원 하지 않는 클라이언트 및 원본과의 호환성을 유지 하려면 및를 둘 다 지정 해야 `PackageIcon` 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-260">You should specify both `PackageIcon` and `PackageIconUrl` to maintain backward compatibility with clients and sources that do not yet support `PackageIcon`.</span></span> <span data-ttu-id="c05ed-261">Visual Studio는 `PackageIcon` 이후 릴리스에서 폴더 기반 소스에서 가져온 패키지를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-261">Visual Studio will support `PackageIcon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="c05ed-262">아이콘 이미지 파일 압축</span><span class="sxs-lookup"><span data-stu-id="c05ed-262">Packing an icon image file</span></span>

<span data-ttu-id="c05ed-263">아이콘 이미지 파일을 압축 하는 경우 속성을 사용 하 여 패키지 `PackageIcon` 의 루트에 상대적인 패키지 경로를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-263">When packing an icon image file, you need to use `PackageIcon` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="c05ed-264">또한 파일이 패키지에 포함 되어 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-264">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="c05ed-265">이미지 파일 크기는 1mb로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-265">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="c05ed-266">지원 되는 파일 형식에는 JPEG 및 PNG가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-266">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="c05ed-267">128x128 이미지를 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-267">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="c05ed-268">예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-268">For example:</span></span>

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

<span data-ttu-id="c05ed-269">[패키지 아이콘 샘플](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="c05ed-269">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="c05ed-270">Nuspec에 대 한 자세한 내용은 [nuspec reference에 대 한 참조를 참조](nuspec.md#icon)하세요.</span><span class="sxs-lookup"><span data-stu-id="c05ed-270">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="c05ed-271">출력 어셈블리</span><span class="sxs-lookup"><span data-stu-id="c05ed-271">Output assemblies</span></span>

<span data-ttu-id="c05ed-272">`nuget pack`은 `.exe`, `.dll`, `.xml`, `.winmd`, `.json` 및 `.pri` 확장명의 출력 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-272">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="c05ed-273">복사되는 출력 파일은 `BuiltOutputProjectGroup` 대상에서 제공하는 MSBuild에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-273">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="c05ed-274">프로젝트 파일 또는 명령줄에서 출력 어셈블리의 위치를 제어하는 데 사용할 수 있는 두 가지 MSBuild 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-274">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="c05ed-275">`IncludeBuildOutput`: 빌드 출력 어셈블리를 패키지에 포함할지 여부를 결정하는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-275">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="c05ed-276">`BuildOutputTargetFolder`: 출력 어셈블리를 배치할 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-276">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="c05ed-277">출력 어셈블리(및 기타 출력 파일)는 해당 프레임워크 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-277">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="c05ed-278">패키지 참조</span><span class="sxs-lookup"><span data-stu-id="c05ed-278">Package references</span></span>

<span data-ttu-id="c05ed-279">[프로젝트 파일의 패키지 참조](../consume-packages/package-references-in-project-files.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c05ed-279">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="c05ed-280">프로젝트 간 참조</span><span class="sxs-lookup"><span data-stu-id="c05ed-280">Project to project references</span></span>

<span data-ttu-id="c05ed-281">프로젝트 간 참조는 기본적으로 NuGet 패키지 참조로 간주됩니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-281">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="c05ed-282">또한 다음 메타데이터를 프로젝트 참조에 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-282">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="c05ed-283">패키지에 내용 포함</span><span class="sxs-lookup"><span data-stu-id="c05ed-283">Including content in a package</span></span>

<span data-ttu-id="c05ed-284">콘텐츠를 포함하려면 기존 `<Content>` 항목에 추가 메타데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-284">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="c05ed-285">기본적으로 "Content" 형식의 모든 항목은 다음과 같은 항목으로 재정의하지 않는 한 패키지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-285">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="c05ed-286">패키지 경로를 지정하지 않으면 기본적으로 `content` 및 `contentFiles\any\<target_framework>` 패키지 폴더의 루트에 모든 항목이 추가되고 상대 폴더 구조가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-286">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="c05ed-287">모든 내용을 특정 루트 폴더(`content` 및 `contentFiles` 대신)에만 복사하려면 `ContentTargetFolders` MSBuild 속성을 사용할 수 있습니다. 이 속성은 기본적으로 "content; contentFiles"이지만 다른 폴더 이름으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-287">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="c05ed-288">`ContentTargetFolders`에 "contentFiles"를 지정하면 파일이 `buildAction`에 따라 `contentFiles\any\<target_framework>` 또는 `contentFiles\<language>\<target_framework>`에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-288">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="c05ed-289">`PackagePath`는 세미콜론으로 구분된 대상 경로의 집합일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-289">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="c05ed-290">빈 패키지 경로를 지정하면 파일이 패키지의 루트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-290">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="c05ed-291">예를 들어 다음은 `libuv.txt`를 `content\myfiles`, `content\samples` 및 패키지 루트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-291">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="c05ed-292">또한 `$(IncludeContentInPack)` MSBuild 속성이 있으며 기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-292">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="c05ed-293">모든 프로젝트에서 이 값을 `false`로 설정하면 해당 프로젝트의 내용이 NuGet 패키지에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-293">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="c05ed-294">위의 항목 중 하나에서 설정할 수 있는 다른 pack 특정 메타데이터에는 nuspec 출력의 ```contentFiles``` 항목에 ```CopyToOutput``` 및 ```Flatten``` 값을 설정하는 ```<PackageCopyToOutput>``` 및 ```<PackageFlatten>```이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-294">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="c05ed-295">Content 항목 외에도, 빌드 작업이 Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource 또는 None으로 설정된 파일에 `<Pack>` 및 `<PackagePath>` 메타데이터를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-295">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="c05ed-296">GLOB 패턴을 사용할 때 pack에서 파일 이름을 패키지 경로에 추가하려면 패키지 경로가 폴더 구분 문자로 끝나야 합니다. 그렇지 않으면 패키지 경로가 파일 이름을 포함한 전체 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-296">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="c05ed-297">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="c05ed-297">IncludeSymbols</span></span>

<span data-ttu-id="c05ed-298">`MSBuild -t:pack -p:IncludeSymbols=true`를 사용하면 해당 `.pdb` 파일이 다른 출력 파일(`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`)과 함께 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-298">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="c05ed-299">`IncludeSymbols=true`를 설정하면 일반 패키지 *및* 기호 패키지가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-299">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="c05ed-300">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="c05ed-300">IncludeSource</span></span>

<span data-ttu-id="c05ed-301">`.pdb` 파일과 함께 원본 파일을 복사한다는 점을 제외하고는 `IncludeSymbols`와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-301">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="c05ed-302">`Compile` 형식의 모든 파일이 결과 패키지에서 상대 경로 폴더 구조를 유지하면서 `src\<ProjectName>\`에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-302">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="c05ed-303">또한 `TreatAsPackageReference`가 `false`로 설정된 `ProjectReference`의 원본 파일에 대해서도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-303">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="c05ed-304">Compile 형식의 파일이 프로젝트 폴더의 외부에 있는 경우 이 파일은 `src\<ProjectName>\`에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-304">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="c05ed-305">라이선스 식 또는 라이선스 파일 압축</span><span class="sxs-lookup"><span data-stu-id="c05ed-305">Packing a license expression or a license file</span></span>

<span data-ttu-id="c05ed-306">라이선스 식을 사용할 때 PackageLicenseExpression 속성을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-306">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="c05ed-307">[라이선스 식 샘플](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-307">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="c05ed-308">[NuGet.org에서 허용 하는 라이선스 식 및 라이선스에 대해 자세히 알아보세요](nuspec.md#license).</span><span class="sxs-lookup"><span data-stu-id="c05ed-308">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="c05ed-309">라이선스 파일을 압축 하는 경우 PackageLicenseFile 속성을 사용 하 여 패키지의 루트에 상대적인 패키지 경로를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-309">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="c05ed-310">또한 파일이 패키지에 포함 되어 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-310">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="c05ed-311">예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-311">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="c05ed-312">[라이선스 파일 샘플](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span><span class="sxs-lookup"><span data-stu-id="c05ed-312">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="c05ed-313">확장명 없이 파일 압축</span><span class="sxs-lookup"><span data-stu-id="c05ed-313">Packing a file without an extension</span></span>

<span data-ttu-id="c05ed-314">라이선스 파일을 압축 하는 경우와 같은 일부 시나리오에서는 확장명이 없는 파일을 포함 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-314">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="c05ed-315">기록을 위해 NuGet & MSBuild는 확장 없이 경로를 디렉터리로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-315">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="c05ed-316">[확장명 샘플이 없는 파일](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/)입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-316">[File without an extension sample](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span></span>
### <a name="istool"></a><span data-ttu-id="c05ed-317">IsTool</span><span class="sxs-lookup"><span data-stu-id="c05ed-317">IsTool</span></span>

<span data-ttu-id="c05ed-318">`MSBuild -t:pack -p:IsTool=true`를 사용하면 [출력 어셈블리](#output-assemblies) 시나리오에서 지정한 대로 모든 출력 파일이 `lib` 폴더 대신 `tools` 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-318">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="c05ed-319">이는 `.csproj` 파일에서 `PackageType`을 설정하여 지정된 `DotNetCliTool`과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-319">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="c05ed-320">.nuspec을 사용하여 압축</span><span class="sxs-lookup"><span data-stu-id="c05ed-320">Packing using a .nuspec</span></span>

<span data-ttu-id="c05ed-321">일반적으로 파일에 있는 [모든 속성](../reference/msbuild-targets.md#pack-target) 을 프로젝트 파일에 포함 하는 것이 좋지만 `.nuspec` , 파일을 사용 하 여 프로젝트를 압축 하도록 선택할 수 있습니다 `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="c05ed-321">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="c05ed-322">를 사용 하는 비 SDK 스타일 프로젝트의 경우 `PackageReference` `NuGet.Build.Tasks.Pack.targets` pack 작업을 실행할 수 있도록를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-322">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="c05ed-323">여전히 프로젝트를 복원 해야 nuspec 파일을 압축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-323">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="c05ed-324">SDK 스타일 프로젝트는 기본적으로 pack 대상을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-324">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="c05ed-325">프로젝트 파일의 대상 프레임 워크는 관련이 없으며 nuspec을 압축 하는 경우에는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-325">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="c05ed-326">다음 세 가지 MSBuild 속성은 `.nuspec`을 사용하여 압축하는 것과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-326">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="c05ed-327">`NuspecFile`: 압축에 사용되는 `.nuspec` 파일에 대한 상대 또는 절대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-327">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="c05ed-328">`NuspecProperties`: 세미콜론으로 구분된 key=value 쌍의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-328">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="c05ed-329">MSBuild 명령줄 구문 분석이 작동하는 방식으로 인해 여러 속성을 `-p:NuspecProperties="key1=value1;key2=value2"`와 같이 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-329">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="c05ed-330">`NuspecBasePath`: `.nuspec` 파일에 대한 기본 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-330">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="c05ed-331">`dotnet.exe`를 사용하여 프로젝트를 압축하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-331">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="c05ed-332">MSBuild를 사용하여 프로젝트를 압축하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-332">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="c05ed-333">dotnet.exe 또는 msbuild를 사용 하 여 nuspec을 압축 하면 기본적으로 프로젝트를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-333">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="c05ed-334">이는 프로젝트 파일의 ```--no-build``` ```<NoBuild>true</NoBuild> ``` 설정과 함께 프로젝트 파일의 설정과 동일한 속성을 dotnet.exe 전달 하 여 방지할 수 있습니다 ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` .</span><span class="sxs-lookup"><span data-stu-id="c05ed-334">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="c05ed-335">Nuspec 파일을 압축 하는 *.csproj* 파일의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-335">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="c05ed-336">사용자 지정 패키지를 만들기 위한 고급 확장점</span><span class="sxs-lookup"><span data-stu-id="c05ed-336">Advanced extension points to create customized package</span></span>

<span data-ttu-id="c05ed-337">`pack`대상은 내부, 대상 프레임 워크 특정 빌드에서 실행 되는 두 개의 확장 지점이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-337">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="c05ed-338">확장 지점은 대상 프레임 워크 관련 콘텐츠 및 어셈블리를 패키지에 포함 하 여 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-338">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="c05ed-339">`TargetsForTfmSpecificBuildOutput` 대상: `lib` 폴더 또는를 사용 하 여 지정 된 폴더 내의 파일에 사용 `BuildOutputTargetFolder` 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-339">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="c05ed-340">`TargetsForTfmSpecificContentInPackage` 대상: 외부의 파일에 사용 `BuildOutputTargetFolder` 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-340">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="c05ed-341">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="c05ed-341">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="c05ed-342">사용자 지정 대상을 작성 하 고이를 속성의 값으로 지정 `$(TargetsForTfmSpecificBuildOutput)` 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-342">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="c05ed-343">로 이동 해야 하는 파일 `BuildOutputTargetFolder` (기본적으로 lib)의 경우 대상은 해당 파일을 ItemGroup에 쓰고 `BuildOutputInPackage` 다음 두 메타 데이터 값을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-343">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="c05ed-344">`FinalOutputPath`: 파일의 절대 경로입니다. 제공 하지 않으면 Id가 원본 경로를 평가 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-344">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="c05ed-345">`TargetPath`: (선택 사항) `lib\<TargetFramework>` 해당 문화권 폴더 아래에 있는 위성 어셈블리와 같이 파일을 내 하위 폴더로 이동 해야 하는 경우에 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-345">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="c05ed-346">기본값은 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-346">Defaults to the name of the file.</span></span>

<span data-ttu-id="c05ed-347">예제:</span><span class="sxs-lookup"><span data-stu-id="c05ed-347">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="c05ed-348">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="c05ed-348">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="c05ed-349">사용자 지정 대상을 작성 하 고이를 속성의 값으로 지정 `$(TargetsForTfmSpecificContentInPackage)` 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-349">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="c05ed-350">패키지에 포함할 파일의 경우 대상은 해당 파일을 ItemGroup에 쓰고 `TfmSpecificPackageFile` 다음과 같은 선택적 메타 데이터를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-350">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="c05ed-351">`PackagePath`: 패키지에서 파일이 출력 되어야 하는 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-351">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="c05ed-352">동일한 패키지 경로에 두 개 이상의 파일이 추가 되 면 NuGet에서 경고를 발생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-352">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="c05ed-353">`BuildAction`: 파일에 할당할 빌드 작업으로, 패키지 경로가 폴더에 있는 경우에만 필요 합니다 `contentFiles` .</span><span class="sxs-lookup"><span data-stu-id="c05ed-353">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="c05ed-354">기본값은 "None"입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-354">Defaults to "None".</span></span>

<span data-ttu-id="c05ed-355">예제:</span><span class="sxs-lookup"><span data-stu-id="c05ed-355">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="c05ed-356">restore 대상</span><span class="sxs-lookup"><span data-stu-id="c05ed-356">restore target</span></span>

<span data-ttu-id="c05ed-357">`MSBuild -t:restore`(.NET Core 프로젝트에서 `nuget restore` 및 `dotnet restore` 사용)는 프로젝트 파일에서 참조된 패키지를 다음과 같이 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-357">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="c05ed-358">모든 프로젝트 간 참조를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-358">Read all project to project references</span></span>
1. <span data-ttu-id="c05ed-359">프로젝트 속성을 읽어 중간 폴더 및 대상 프레임워크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-359">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="c05ed-360">NuGet.Build.Tasks.dll에 MSBuild 데이터 전달</span><span class="sxs-lookup"><span data-stu-id="c05ed-360">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="c05ed-361">restore를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-361">Run restore</span></span>
1. <span data-ttu-id="c05ed-362">패키지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-362">Download packages</span></span>
1. <span data-ttu-id="c05ed-363">자산, targets 및 props 파일을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-363">Write assets file, targets, and props</span></span>

<span data-ttu-id="c05ed-364">`restore`대상은 PackageReference 형식을 사용 하는 프로젝트에 대해 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-364">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="c05ed-365">`MSBuild 16.5+` 또한에서는 형식에 대 한 [옵트인 지원도 제공](#restoring-packagereference-and-packagesconfig-with-msbuild) `packages.config` 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-365">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="c05ed-366">대상은 `restore` 대상과 함께 [실행 해서는](#restoring-and-building-with-one-msbuild-command) 안 됩니다 `build` .</span><span class="sxs-lookup"><span data-stu-id="c05ed-366">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="c05ed-367">restore 속성</span><span class="sxs-lookup"><span data-stu-id="c05ed-367">Restore properties</span></span>

<span data-ttu-id="c05ed-368">추가 restore 설정은 프로젝트 파일의 MSBuild 속성에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-368">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="c05ed-369">또한 값은 `-p:` 스위치를 사용하여 명령줄에서 설정할 수 있습니다(아래 예제 참조).</span><span class="sxs-lookup"><span data-stu-id="c05ed-369">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="c05ed-370">속성</span><span class="sxs-lookup"><span data-stu-id="c05ed-370">Property</span></span> | <span data-ttu-id="c05ed-371">설명</span><span class="sxs-lookup"><span data-stu-id="c05ed-371">Description</span></span> |
|--------|--------|
| <span data-ttu-id="c05ed-372">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="c05ed-372">RestoreSources</span></span> | <span data-ttu-id="c05ed-373">세미콜론으로 구분된 패키지 원본의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-373">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="c05ed-374">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="c05ed-374">RestorePackagesPath</span></span> | <span data-ttu-id="c05ed-375">사용자 패키지 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-375">User packages folder path.</span></span> |
| <span data-ttu-id="c05ed-376">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="c05ed-376">RestoreDisableParallel</span></span> | <span data-ttu-id="c05ed-377">다운로드를 한 번에 하나씩으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-377">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="c05ed-378">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="c05ed-378">RestoreConfigFile</span></span> | <span data-ttu-id="c05ed-379">적용할 `Nuget.Config` 파일에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-379">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="c05ed-380">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="c05ed-380">RestoreNoCache</span></span> | <span data-ttu-id="c05ed-381">True 이면 캐시 된 패키지를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-381">If true, avoids using cached packages.</span></span> <span data-ttu-id="c05ed-382">[전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="c05ed-382">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="c05ed-383">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="c05ed-383">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="c05ed-384">true이면 실패했거나 누락된 패키지 원본을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-384">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="c05ed-385">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="c05ed-385">RestoreFallbackFolders</span></span> | <span data-ttu-id="c05ed-386">사용자 패키지 폴더를 사용 하는 것과 같은 방식으로 사용 되는 대체 (Fallback) 폴더</span><span class="sxs-lookup"><span data-stu-id="c05ed-386">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="c05ed-387">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="c05ed-387">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="c05ed-388">복원 하는 동안 사용할 추가 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-388">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="c05ed-389">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="c05ed-389">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="c05ed-390">복원 중에 사용할 추가 대체 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-390">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="c05ed-391">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="c05ed-391">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="c05ed-392">에 지정 된 대체 폴더를 제외 합니다. `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="c05ed-392">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="c05ed-393">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="c05ed-393">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="c05ed-394">`NuGet.Build.Tasks.dll`에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-394">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="c05ed-395">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="c05ed-395">RestoreGraphProjectInput</span></span> | <span data-ttu-id="c05ed-396">세미콜론으로 구분된 복원할 프로젝트의 목록이며, 절대 경로가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-396">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="c05ed-397">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="c05ed-397">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="c05ed-398">MSBuild를 통해 프로젝트를 수집 하는 경우 해당 프로젝트는 최적화를 사용 하 여 수집 되는지 여부를 결정 합니다 `SkipNonexistentTargets` .</span><span class="sxs-lookup"><span data-stu-id="c05ed-398">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="c05ed-399">설정 하지 않으면 기본적으로로 설정 `true` 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-399">When not set, defaults to `true`.</span></span> <span data-ttu-id="c05ed-400">결과는 프로젝트의 대상을 가져올 수 없는 경우의 빠른 오류 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-400">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="c05ed-401">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="c05ed-401">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="c05ed-402">출력 폴더, 및 폴더에 대 한 기본값입니다 `BaseIntermediateOutputPath` `obj` .</span><span class="sxs-lookup"><span data-stu-id="c05ed-402">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="c05ed-403">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="c05ed-403">RestoreForce</span></span> | <span data-ttu-id="c05ed-404">PackageReference 기반 프로젝트에서 마지막 복원이 성공한 경우에도 모든 종속성이 확인 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-404">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="c05ed-405">이 플래그를 지정 하는 것은 파일을 삭제 하는 것과 비슷합니다 `project.assets.json` .</span><span class="sxs-lookup"><span data-stu-id="c05ed-405">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="c05ed-406">이는 http 캐시를 우회 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-406">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="c05ed-407">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="c05ed-407">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="c05ed-408">잠금 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-408">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="c05ed-409">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="c05ed-409">RestoreLockedMode</span></span> | <span data-ttu-id="c05ed-410">잠금 모드에서 복원을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-410">Run restore in locked mode.</span></span> <span data-ttu-id="c05ed-411">즉, 복원은 종속성을 다시 평가 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-411">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="c05ed-412">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="c05ed-412">NuGetLockFilePath</span></span> | <span data-ttu-id="c05ed-413">잠금 파일의 사용자 지정 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-413">A custom location for the lock file.</span></span> <span data-ttu-id="c05ed-414">기본 위치는 프로젝트 옆에 있고 이름은 `packages.lock.json` 입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-414">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="c05ed-415">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="c05ed-415">RestoreForceEvaluate</span></span> | <span data-ttu-id="c05ed-416">강제로 복원 하 여 종속성을 다시 계산 하 고 경고 없이 잠금 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-416">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="c05ed-417">RestorePackagesConfig</span><span class="sxs-lookup"><span data-stu-id="c05ed-417">RestorePackagesConfig</span></span> | <span data-ttu-id="c05ed-418">packages.config를 사용 하 여 프로젝트를 복원 하는 옵트인 스위치. 만 지원 `MSBuild -t:restore` 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-418">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| <span data-ttu-id="c05ed-419">RestoreUseStaticGraphEvaluation</span><span class="sxs-lookup"><span data-stu-id="c05ed-419">RestoreUseStaticGraphEvaluation</span></span> | <span data-ttu-id="c05ed-420">표준 평가 대신 정적 그래프 MSBuild 평가를 사용 하는 옵트인 스위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-420">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="c05ed-421">정적 그래프 평가는 큰 리포지토리 및 솔루션에 대해 훨씬 더 빠른 실험적 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-421">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="c05ed-422">예제</span><span class="sxs-lookup"><span data-stu-id="c05ed-422">Examples</span></span>

<span data-ttu-id="c05ed-423">명령줄:</span><span class="sxs-lookup"><span data-stu-id="c05ed-423">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="c05ed-424">프로젝트 파일:</span><span class="sxs-lookup"><span data-stu-id="c05ed-424">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="c05ed-425">restore 출력</span><span class="sxs-lookup"><span data-stu-id="c05ed-425">Restore outputs</span></span>

<span data-ttu-id="c05ed-426">restore는 `obj` 빌드 폴더에 다음 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-426">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="c05ed-427">파일</span><span class="sxs-lookup"><span data-stu-id="c05ed-427">File</span></span> | <span data-ttu-id="c05ed-428">설명</span><span class="sxs-lookup"><span data-stu-id="c05ed-428">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="c05ed-429">모든 패키지 참조의 종속성 그래프를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-429">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="c05ed-430">패키지에 포함된 MSBuild props 파일에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="c05ed-430">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="c05ed-431">패키지에 포함된 MSBuild targets 파일에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="c05ed-431">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="c05ed-432">하나의 MSBuild 명령을 사용 하 여 복원 및 빌드</span><span class="sxs-lookup"><span data-stu-id="c05ed-432">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="c05ed-433">NuGet은 MSBuild 대상 및 props을 가져오는 패키지를 복원할 수 있으므로 다른 전역 속성을 사용 하 여 복원 및 빌드 평가가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-433">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="c05ed-434">즉, 다음은 예측할 수 없으며 종종 잘못 된 동작을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-434">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="c05ed-435">대신에 권장 되는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-435">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="c05ed-436">같은 논리는와 유사한 다른 대상에도 적용 됩니다 `build` .</span><span class="sxs-lookup"><span data-stu-id="c05ed-436">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="c05ed-437">MSBuild를 사용 하 여 PackageReference 및 packages.config 복원</span><span class="sxs-lookup"><span data-stu-id="c05ed-437">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="c05ed-438">MSBuild 16.5 +를 사용 하는 경우에도 packages.config 지원 됩니다 `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="c05ed-438">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="c05ed-439">`packages.config` restore는와 함께 사용할 수 `MSBuild 16.5+` 없습니다. `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="c05ed-439">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="c05ed-440">MSBuild 정적 그래프 평가를 사용 하 여 복원</span><span class="sxs-lookup"><span data-stu-id="c05ed-440">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="c05ed-441">MSBuild 16.6 +를 사용 하는 경우 NuGet은 큰 리포지토리의 복원 시간을 크게 개선 하는 명령줄에서 정적 그래프 평가를 사용 하는 실험적 기능을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-441">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="c05ed-442">또는 디렉터리에 속성을 설정 하 여 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-442">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="c05ed-443">Visual Studio 2019. x 및 NuGet 5.x를 기반으로이 기능은 실험적이 고 옵트인 (opt in) 된 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-443">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="c05ed-444">이 기능이 기본적으로 사용 되는 경우에 대 한 자세한 내용은 [NuGet/Home # 9803](https://github.com/NuGet/Home/issues/9803) 를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="c05ed-444">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="c05ed-445">정적 그래프 복원은 복원, 프로젝트 읽기 및 평가의 msbuild 부분을 변경 하지만 복원 알고리즘은 변경 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-445">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="c05ed-446">복원 알고리즘은 모든 NuGet 도구 (NuGet.exe, MSBuild.exe, dotnet.exe 및 Visual Studio)에서 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-446">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="c05ed-447">거의 모든 시나리오에서 정적 그래프 복원은 현재 복원과 다르게 동작할 수 있으며 선언 된 특정 PackageReferences 또는 ProjectReferences가 누락 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-447">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="c05ed-448">정적 그래프 복원으로 마이그레이션할 때를 한 번만 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-448">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="c05ed-449">NuGet은 어떠한 변경 내용도 보고 *하지 않습니다* .</span><span class="sxs-lookup"><span data-stu-id="c05ed-449">NuGet should *not* report any changes.</span></span> <span data-ttu-id="c05ed-450">불일치가 표시 되는 경우 [NuGet/Home](https://github.com/nuget/home/issues/new)에서 문제를 파일에 입력 하세요.</span><span class="sxs-lookup"><span data-stu-id="c05ed-450">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="c05ed-451">복원 그래프에서 단일 라이브러리 대체</span><span class="sxs-lookup"><span data-stu-id="c05ed-451">Replacing one library from a restore graph</span></span>

<span data-ttu-id="c05ed-452">restore에서 잘못된 어셈블리를 가져오는 경우 해당 패키지의 기본 선택 항목을 제외하는 한편 원하는 선택 항목으로 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-452">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="c05ed-453">먼저 최상위 `PackageReference`를 사용하여 모든 자산을 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-453">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="c05ed-454">그런 다음 DLL의 적절한 로컬 복사본에 대한 고유한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c05ed-454">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
