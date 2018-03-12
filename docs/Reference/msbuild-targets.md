---
title: "MSBuild 대상으로서의 NuGet pack 및 restore | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet pack 및 restore는 NuGet 4.0 이상에서 MSBuild 대상으로 직접 작동할 수 있습니다."
keywords: "NuGet 및 MSBuild, NuGet pack 대상, NuGet restore 대상"
ms.reviewer:
- karann-msft
ms.openlocfilehash: 798b3550718294072d86b6e4827ec5017178d2cc
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/08/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="b62c1-104">MSBuild 대상으로서의 NuGet pack 및 restore</span><span class="sxs-lookup"><span data-stu-id="b62c1-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="b62c1-105">*NuGet 4.0 이상*</span><span class="sxs-lookup"><span data-stu-id="b62c1-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="b62c1-106">PackageReference 형식을 사용하면 NuGet 4.0 이상은 별도의 `.nuspec` 파일을 사용하는 대신 프로젝트 파일 내에서 모든 매니페스트 메타데이터를 직접 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="b62c1-107">MSBuild 15.1 이상에서 NuGet은 아래에서 설명한 대로 `pack` 및 `restore` 대상이 있는 일류 MSBuild 시민이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="b62c1-108">이러한 대상을 사용하면 다른 MSBuild 작업 또는 대상과 마찬가지로 NuGet을 사용하여 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="b62c1-109">(NuGet 3.x 및 이전 버전의 경우 NuGet CLI를 통해 [pack](../tools/cli-ref-pack.md) 및 [restore](../tools/cli-ref-restore.md) 명령을 대신 사용합니다.)</span><span class="sxs-lookup"><span data-stu-id="b62c1-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="b62c1-110">대상 빌드 순서</span><span class="sxs-lookup"><span data-stu-id="b62c1-110">Target build order</span></span>

<span data-ttu-id="b62c1-111">`pack` 및 `restore`는 MSBuild 대상이므로 이 대상에 액세스하여 워크플로를 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="b62c1-112">예를 들어 패키지를 압축한 후 네트워크 공유에 복사한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="b62c1-113">이렇게 하려면 프로젝트 파일에 다음을 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="b62c1-114">마찬가지로, MSBuild 작업을 작성하고, 고유한 대상을 작성하고, MSBuild 작업에서 NuGet 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="b62c1-115">pack 대상</span><span class="sxs-lookup"><span data-stu-id="b62c1-115">pack target</span></span>

<span data-ttu-id="b62c1-116">pack 대상을 사용할 경우(`msbuild /t:pack`) MSBuild는 프로젝트 파일에서 해당 입력을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-116">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the project file.</span></span> <span data-ttu-id="b62c1-117">아래 표에서는 첫 번째 `<PropertyGroup>` 노드 내에서 프로젝트 파일에 추가할 수 있는 MSBuild 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="b62c1-118">Visual Studio 2017 이상에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **{project_name} 편집**을 선택하여 이러한 편집 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="b62c1-119">편의상 이 표는 [`.nuspec` 파일 ](../reference/nuspec.md)에 있는 동등한 속성으로 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="b62c1-120">`.nuspec`의 `Owners` 및 `Summary` 속성은 MSBuild에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="b62c1-121">특성/NuSpec 값</span><span class="sxs-lookup"><span data-stu-id="b62c1-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="b62c1-122">MSBuild 속성</span><span class="sxs-lookup"><span data-stu-id="b62c1-122">MSBuild Property</span></span> | <span data-ttu-id="b62c1-123">기본</span><span class="sxs-lookup"><span data-stu-id="b62c1-123">Default</span></span> | <span data-ttu-id="b62c1-124">노트</span><span class="sxs-lookup"><span data-stu-id="b62c1-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="b62c1-125">ID</span><span class="sxs-lookup"><span data-stu-id="b62c1-125">Id</span></span> | <span data-ttu-id="b62c1-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="b62c1-126">PackageId</span></span> | <span data-ttu-id="b62c1-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="b62c1-127">AssemblyName</span></span> | <span data-ttu-id="b62c1-128">MSBuild의 $(AssemblyName)입니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="b62c1-129">버전</span><span class="sxs-lookup"><span data-stu-id="b62c1-129">Version</span></span> | <span data-ttu-id="b62c1-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="b62c1-130">PackageVersion</span></span> | <span data-ttu-id="b62c1-131">버전</span><span class="sxs-lookup"><span data-stu-id="b62c1-131">Version</span></span> | <span data-ttu-id="b62c1-132">"1.0.0", "1.0.0-beta" 또는 "1.0.0-beta-00345"와 같이 semver와 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="b62c1-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="b62c1-133">VersionPrefix</span></span> | <span data-ttu-id="b62c1-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="b62c1-134">PackageVersionPrefix</span></span> | <span data-ttu-id="b62c1-135">비어 있음</span><span class="sxs-lookup"><span data-stu-id="b62c1-135">empty</span></span> | <span data-ttu-id="b62c1-136">PackageVersion을 설정하면 PackageVersionPrefix를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="b62c1-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="b62c1-137">VersionSuffix</span></span> | <span data-ttu-id="b62c1-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="b62c1-138">PackageVersionSuffix</span></span> | <span data-ttu-id="b62c1-139">비어 있음</span><span class="sxs-lookup"><span data-stu-id="b62c1-139">empty</span></span> | <span data-ttu-id="b62c1-140">MSBuild의 $(VersionSuffix)입니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="b62c1-141">PackageVersion을 설정하면 PackageVersionSuffix를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="b62c1-142">만든 이</span><span class="sxs-lookup"><span data-stu-id="b62c1-142">Authors</span></span> | <span data-ttu-id="b62c1-143">만든 이</span><span class="sxs-lookup"><span data-stu-id="b62c1-143">Authors</span></span> | <span data-ttu-id="b62c1-144">현재 사용자의 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="b62c1-144">Username of the current user</span></span> | |
| <span data-ttu-id="b62c1-145">Owners</span><span class="sxs-lookup"><span data-stu-id="b62c1-145">Owners</span></span> | <span data-ttu-id="b62c1-146">N/A</span><span class="sxs-lookup"><span data-stu-id="b62c1-146">N/A</span></span> | <span data-ttu-id="b62c1-147">NuSpec에는 없음</span><span class="sxs-lookup"><span data-stu-id="b62c1-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="b62c1-148">제목</span><span class="sxs-lookup"><span data-stu-id="b62c1-148">Title</span></span> | <span data-ttu-id="b62c1-149">제목</span><span class="sxs-lookup"><span data-stu-id="b62c1-149">Title</span></span> | <span data-ttu-id="b62c1-150">PackageId</span><span class="sxs-lookup"><span data-stu-id="b62c1-150">The PackageId</span></span>| |
| <span data-ttu-id="b62c1-151">설명</span><span class="sxs-lookup"><span data-stu-id="b62c1-151">Description</span></span> | <span data-ttu-id="b62c1-152">PackageDescription</span><span class="sxs-lookup"><span data-stu-id="b62c1-152">PackageDescription</span></span> | <span data-ttu-id="b62c1-153">"패키지 설명"</span><span class="sxs-lookup"><span data-stu-id="b62c1-153">"Package Description"</span></span> | |
| <span data-ttu-id="b62c1-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="b62c1-154">Copyright</span></span> | <span data-ttu-id="b62c1-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="b62c1-155">Copyright</span></span> | <span data-ttu-id="b62c1-156">비어 있음</span><span class="sxs-lookup"><span data-stu-id="b62c1-156">empty</span></span> | |
| <span data-ttu-id="b62c1-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="b62c1-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="b62c1-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="b62c1-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="b62c1-159">False</span><span class="sxs-lookup"><span data-stu-id="b62c1-159">false</span></span> | |
| <span data-ttu-id="b62c1-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="b62c1-160">LicenseUrl</span></span> | <span data-ttu-id="b62c1-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="b62c1-161">PackageLicenseUrl</span></span> | <span data-ttu-id="b62c1-162">비어 있음</span><span class="sxs-lookup"><span data-stu-id="b62c1-162">empty</span></span> | |
| <span data-ttu-id="b62c1-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="b62c1-163">ProjectUrl</span></span> | <span data-ttu-id="b62c1-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="b62c1-164">PackageProjectUrl</span></span> | <span data-ttu-id="b62c1-165">비어 있음</span><span class="sxs-lookup"><span data-stu-id="b62c1-165">empty</span></span> | |
| <span data-ttu-id="b62c1-166">IconUrl</span><span class="sxs-lookup"><span data-stu-id="b62c1-166">IconUrl</span></span> | <span data-ttu-id="b62c1-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="b62c1-167">PackageIconUrl</span></span> | <span data-ttu-id="b62c1-168">비어 있음</span><span class="sxs-lookup"><span data-stu-id="b62c1-168">empty</span></span> | |
| <span data-ttu-id="b62c1-169">Tags</span><span class="sxs-lookup"><span data-stu-id="b62c1-169">Tags</span></span> | <span data-ttu-id="b62c1-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="b62c1-170">PackageTags</span></span> | <span data-ttu-id="b62c1-171">비어 있음</span><span class="sxs-lookup"><span data-stu-id="b62c1-171">empty</span></span> | <span data-ttu-id="b62c1-172">세미콜론으로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="b62c1-173">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="b62c1-173">ReleaseNotes</span></span> | <span data-ttu-id="b62c1-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="b62c1-174">PackageReleaseNotes</span></span> | <span data-ttu-id="b62c1-175">비어 있음</span><span class="sxs-lookup"><span data-stu-id="b62c1-175">empty</span></span> | |
| <span data-ttu-id="b62c1-176">리포지토리/Url</span><span class="sxs-lookup"><span data-stu-id="b62c1-176">Repository/Url</span></span> | <span data-ttu-id="b62c1-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="b62c1-177">RepositoryUrl</span></span> | <span data-ttu-id="b62c1-178">비어 있음</span><span class="sxs-lookup"><span data-stu-id="b62c1-178">empty</span></span> | <span data-ttu-id="b62c1-179">리포지토리 URL을 복제 하거나 소스 코드를 검색 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-179">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="b62c1-180">Example: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="b62c1-180">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="b62c1-181">저장소/유형</span><span class="sxs-lookup"><span data-stu-id="b62c1-181">Repository/Type</span></span> | <span data-ttu-id="b62c1-182">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="b62c1-182">RepositoryType</span></span> | <span data-ttu-id="b62c1-183">비어 있음</span><span class="sxs-lookup"><span data-stu-id="b62c1-183">empty</span></span> | <span data-ttu-id="b62c1-184">리포지토리 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-184">Repository type.</span></span> <span data-ttu-id="b62c1-185">예: *git*, *tfs*합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-185">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="b62c1-186">리포지토리/분기</span><span class="sxs-lookup"><span data-stu-id="b62c1-186">Repository/Branch</span></span> | <span data-ttu-id="b62c1-187">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="b62c1-187">RepositoryBranch</span></span> | <span data-ttu-id="b62c1-188">비어 있음</span><span class="sxs-lookup"><span data-stu-id="b62c1-188">empty</span></span> | <span data-ttu-id="b62c1-189">선택적 리포지토리 분기 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-189">Optional repository branch information.</span></span> <span data-ttu-id="b62c1-190">*RepositoryUrl* 포함 되도록 하려면이 속성에도 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-190">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="b62c1-191">예: *마스터* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="b62c1-191">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="b62c1-192">리포지토리/커밋</span><span class="sxs-lookup"><span data-stu-id="b62c1-192">Repository/Commit</span></span> | <span data-ttu-id="b62c1-193">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="b62c1-193">RepositoryCommit</span></span> | <span data-ttu-id="b62c1-194">비어 있음</span><span class="sxs-lookup"><span data-stu-id="b62c1-194">empty</span></span> | <span data-ttu-id="b62c1-195">선택적 저장소 커밋 또는 패키지 소스를 나타내기 위해 변경 집합에 대해 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-195">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="b62c1-196">*RepositoryUrl* 포함 되도록 하려면이 속성에도 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-196">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="b62c1-197">예: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="b62c1-197">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="b62c1-198">PackageType</span><span class="sxs-lookup"><span data-stu-id="b62c1-198">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="b62c1-199">요약</span><span class="sxs-lookup"><span data-stu-id="b62c1-199">Summary</span></span> | <span data-ttu-id="b62c1-200">지원 안 함</span><span class="sxs-lookup"><span data-stu-id="b62c1-200">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="b62c1-201">pack 대상 입력</span><span class="sxs-lookup"><span data-stu-id="b62c1-201">pack target inputs</span></span>

- <span data-ttu-id="b62c1-202">IsPackable</span><span class="sxs-lookup"><span data-stu-id="b62c1-202">IsPackable</span></span>
- <span data-ttu-id="b62c1-203">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="b62c1-203">PackageVersion</span></span>
- <span data-ttu-id="b62c1-204">PackageId</span><span class="sxs-lookup"><span data-stu-id="b62c1-204">PackageId</span></span>
- <span data-ttu-id="b62c1-205">만든 이</span><span class="sxs-lookup"><span data-stu-id="b62c1-205">Authors</span></span>
- <span data-ttu-id="b62c1-206">설명</span><span class="sxs-lookup"><span data-stu-id="b62c1-206">Description</span></span>
- <span data-ttu-id="b62c1-207">Copyright</span><span class="sxs-lookup"><span data-stu-id="b62c1-207">Copyright</span></span>
- <span data-ttu-id="b62c1-208">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="b62c1-208">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="b62c1-209">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="b62c1-209">DevelopmentDependency</span></span>
- <span data-ttu-id="b62c1-210">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="b62c1-210">PackageLicenseUrl</span></span>
- <span data-ttu-id="b62c1-211">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="b62c1-211">PackageProjectUrl</span></span>
- <span data-ttu-id="b62c1-212">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="b62c1-212">PackageIconUrl</span></span>
- <span data-ttu-id="b62c1-213">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="b62c1-213">PackageReleaseNotes</span></span>
- <span data-ttu-id="b62c1-214">PackageTags</span><span class="sxs-lookup"><span data-stu-id="b62c1-214">PackageTags</span></span>
- <span data-ttu-id="b62c1-215">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="b62c1-215">PackageOutputPath</span></span>
- <span data-ttu-id="b62c1-216">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="b62c1-216">IncludeSymbols</span></span>
- <span data-ttu-id="b62c1-217">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="b62c1-217">IncludeSource</span></span>
- <span data-ttu-id="b62c1-218">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="b62c1-218">PackageTypes</span></span>
- <span data-ttu-id="b62c1-219">IsTool</span><span class="sxs-lookup"><span data-stu-id="b62c1-219">IsTool</span></span>
- <span data-ttu-id="b62c1-220">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="b62c1-220">RepositoryUrl</span></span>
- <span data-ttu-id="b62c1-221">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="b62c1-221">RepositoryType</span></span>
- <span data-ttu-id="b62c1-222">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="b62c1-222">RepositoryBranch</span></span>
- <span data-ttu-id="b62c1-223">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="b62c1-223">RepositoryCommit</span></span>
- <span data-ttu-id="b62c1-224">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="b62c1-224">NoPackageAnalysis</span></span>
- <span data-ttu-id="b62c1-225">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="b62c1-225">MinClientVersion</span></span>
- <span data-ttu-id="b62c1-226">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="b62c1-226">IncludeBuildOutput</span></span>
- <span data-ttu-id="b62c1-227">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="b62c1-227">IncludeContentInPack</span></span>
- <span data-ttu-id="b62c1-228">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="b62c1-228">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="b62c1-229">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="b62c1-229">ContentTargetFolders</span></span>
- <span data-ttu-id="b62c1-230">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="b62c1-230">NuspecFile</span></span>
- <span data-ttu-id="b62c1-231">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="b62c1-231">NuspecBasePath</span></span>
- <span data-ttu-id="b62c1-232">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="b62c1-232">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="b62c1-233">pack 시나리오</span><span class="sxs-lookup"><span data-stu-id="b62c1-233">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="b62c1-234">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="b62c1-234">PackageIconUrl</span></span>

<span data-ttu-id="b62c1-235">[NuGet 문제 2582](https://github.com/NuGet/Home/issues/2582)에 대한 변경의 일부로서 `PackageIconUrl`은 최종적으로 `PackageIconUri`로 변경되며, 결과 패키지의 루트에 포함될 아이콘 파일에 대한 상대 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-235">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="b62c1-236">출력 어셈블리</span><span class="sxs-lookup"><span data-stu-id="b62c1-236">Output assemblies</span></span>

<span data-ttu-id="b62c1-237">`nuget pack`은 `.exe`, `.dll`, `.xml`, `.winmd`, `.json` 및 `.pri` 확장명의 출력 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-237">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="b62c1-238">복사되는 출력 파일은 `BuiltOutputProjectGroup` 대상에서 제공하는 MSBuild에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-238">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="b62c1-239">프로젝트 파일 또는 명령줄에서 출력 어셈블리의 위치를 제어하는 데 사용할 수 있는 두 가지 MSBuild 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-239">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="b62c1-240">`IncludeBuildOutput`: 빌드 출력 어셈블리를 패키지에 포함할지 여부를 결정하는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-240">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="b62c1-241">`BuildOutputTargetFolder`: 출력 어셈블리를 배치할 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-241">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="b62c1-242">출력 어셈블리(및 기타 출력 파일)는 해당 프레임워크 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-242">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="b62c1-243">패키지 참조</span><span class="sxs-lookup"><span data-stu-id="b62c1-243">Package references</span></span>

<span data-ttu-id="b62c1-244">[프로젝트 파일의 패키지 참조](../consume-packages/package-references-in-project-files.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b62c1-244">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="b62c1-245">프로젝트 간 참조</span><span class="sxs-lookup"><span data-stu-id="b62c1-245">Project to project references</span></span>

<span data-ttu-id="b62c1-246">프로젝트 간 참조는 기본적으로 NuGet 패키지 참조로 간주됩니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-246">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="b62c1-247">또한 다음 메타데이터를 프로젝트 참조에 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-247">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="b62c1-248">패키지에 내용 포함</span><span class="sxs-lookup"><span data-stu-id="b62c1-248">Including content in a package</span></span>

<span data-ttu-id="b62c1-249">콘텐츠를 포함하려면 기존 `<Content>` 항목에 추가 메타데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-249">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="b62c1-250">기본적으로 "Content" 형식의 모든 항목은 다음과 같은 항목으로 재정의하지 않는 한 패키지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-250">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="b62c1-251">패키지 경로를 지정하지 않으면 기본적으로 `content` 및 `contentFiles\any\<target_framework>` 패키지 폴더의 루트에 모든 항목이 추가되고 상대 폴더 구조가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-251">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="b62c1-252">모든 내용을 특정 루트 폴더(`content` 및 `contentFiles` 대신)에만 복사하려면 `ContentTargetFolders` MSBuild 속성을 사용할 수 있습니다. 이 속성은 기본적으로 "content; contentFiles"이지만 다른 폴더 이름으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-252">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="b62c1-253">`ContentTargetFolders`에 "contentFiles"를 지정하면 파일이 `buildAction`에 따라 `contentFiles\any\<target_framework>` 또는 `contentFiles\<language>\<target_framework>`에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-253">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="b62c1-254">`PackagePath`는 세미콜론으로 구분된 대상 경로의 집합일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-254">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="b62c1-255">빈 패키지 경로를 지정하면 파일이 패키지의 루트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-255">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="b62c1-256">예를 들어 다음은 `libuv.txt`를 `content\myfiles`, `content\samples` 및 패키지 루트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-256">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="b62c1-257">또한 `$(IncludeContentInPack)` MSBuild 속성이 있으며 기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-257">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="b62c1-258">모든 프로젝트에서 이 값을 `false`로 설정하면 해당 프로젝트의 내용이 NuGet 패키지에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-258">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="b62c1-259">위의 항목 중 하나에서 설정할 수 있는 다른 pack 특정 메타데이터에는 nuspec 출력의 ```contentFiles``` 항목에 ```CopyToOutput``` 및 ```Flatten``` 값을 설정하는 ```<PackageCopyToOutput>``` 및 ```<PackageFlatten>```이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-259">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="b62c1-260">Content 항목 외에도, 빌드 작업이 Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource 또는 None으로 설정된 파일에 `<Pack>` 및 `<PackagePath>` 메타데이터를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-260">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="b62c1-261">GLOB 패턴을 사용할 때 pack에서 파일 이름을 패키지 경로에 추가하려면 패키지 경로가 폴더 구분 문자로 끝나야 합니다. 그렇지 않으면 패키지 경로가 파일 이름을 포함한 전체 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-261">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="b62c1-262">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="b62c1-262">IncludeSymbols</span></span>

<span data-ttu-id="b62c1-263">`MSBuild /t:pack /p:IncludeSymbols=true`를 사용하면 해당 `.pdb` 파일이 다른 출력 파일(`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`)과 함께 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-263">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="b62c1-264">`IncludeSymbols=true`를 설정하면 일반 패키지 *및* 기호 패키지가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-264">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="b62c1-265">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="b62c1-265">IncludeSource</span></span>

<span data-ttu-id="b62c1-266">`.pdb` 파일과 함께 원본 파일을 복사한다는 점을 제외하고는 `IncludeSymbols`와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-266">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="b62c1-267">`Compile` 형식의 모든 파일이 결과 패키지에서 상대 경로 폴더 구조를 유지하면서 `src\<ProjectName>\`에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-267">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="b62c1-268">또한 `TreatAsPackageReference`가 `false`로 설정된 `ProjectReference`의 원본 파일에 대해서도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-268">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="b62c1-269">Compile 형식의 파일이 프로젝트 폴더의 외부에 있는 경우 이 파일은 `src\<ProjectName>\`에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-269">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="b62c1-270">IsTool</span><span class="sxs-lookup"><span data-stu-id="b62c1-270">IsTool</span></span>

<span data-ttu-id="b62c1-271">`MSBuild /t:pack /p:IsTool=true`를 사용하면 [출력 어셈블리](#output-assemblies) 시나리오에서 지정한 대로 모든 출력 파일이 `lib` 폴더 대신 `tools` 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-271">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="b62c1-272">이는 `.csproj` 파일에서 `PackageType`을 설정하여 지정된 `DotNetCliTool`과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-272">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="b62c1-273">.nuspec을 사용하여 압축</span><span class="sxs-lookup"><span data-stu-id="b62c1-273">Packing using a .nuspec</span></span>

<span data-ttu-id="b62c1-274">pack 작업을 실행할 수 있도록 `NuGet.Build.Tasks.Pack.targets`를 가져오는 프로젝트 파일이 있는 경우 `.nuspec` 파일을 사용하여 프로젝트를 압축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-274">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="b62c1-275">다음 세 가지 MSBuild 속성은 `.nuspec`을 사용하여 압축하는 것과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-275">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="b62c1-276">`NuspecFile`: 압축에 사용되는 `.nuspec` 파일에 대한 상대 또는 절대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-276">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="b62c1-277">`NuspecProperties`: 세미콜론으로 구분된 key=value 쌍의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-277">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="b62c1-278">MSBuild 명령줄 구문 분석이 작동하는 방식으로 인해 여러 속성을 `/p:NuspecProperties=\"key1=value1;key2=value2\"`와 같이 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-278">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="b62c1-279">`NuspecBasePath`: `.nuspec` 파일에 대한 기본 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-279">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="b62c1-280">`dotnet.exe`를 사용하여 프로젝트를 압축하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-280">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="b62c1-281">MSBuild를 사용하여 프로젝트를 압축하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-281">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="b62c1-282">restore 대상</span><span class="sxs-lookup"><span data-stu-id="b62c1-282">restore target</span></span>

<span data-ttu-id="b62c1-283">`MSBuild /t:restore`(.NET Core 프로젝트에서 `nuget restore` 및 `dotnet restore` 사용)는 프로젝트 파일에서 참조된 패키지를 다음과 같이 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-283">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="b62c1-284">모든 프로젝트 간 참조를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-284">Read all project to project references</span></span>
1. <span data-ttu-id="b62c1-285">프로젝트 속성을 읽어 중간 폴더 및 대상 프레임워크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-285">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="b62c1-286">msbuild 데이터를 NuGet.Build.Tasks.dll에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-286">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="b62c1-287">restore를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-287">Run restore</span></span>
1. <span data-ttu-id="b62c1-288">패키지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-288">Download packages</span></span>
1. <span data-ttu-id="b62c1-289">자산, targets 및 props 파일을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-289">Write assets file, targets, and props</span></span>

> [!Note]
> <span data-ttu-id="b62c1-290">`restore` MSBuild 대상을 사용 하 여 프로젝트에 대해서만 작동 `PackageReference` 항목 및 사용 하 여 참조 하는 패키지를 복원 하지 않습니다는 `packages.config` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-290">The `restore` MSBuild target only works for projects using `PackageReference` items and does not restore packages referenced using a `packages.config` file.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="b62c1-291">restore 속성</span><span class="sxs-lookup"><span data-stu-id="b62c1-291">Restore properties</span></span>

<span data-ttu-id="b62c1-292">추가 restore 설정은 프로젝트 파일의 MSBuild 속성에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-292">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="b62c1-293">또한 값은 `/p:` 스위치를 사용하여 명령줄에서 설정할 수 있습니다(아래 예제 참조).</span><span class="sxs-lookup"><span data-stu-id="b62c1-293">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="b62c1-294">속성</span><span class="sxs-lookup"><span data-stu-id="b62c1-294">Property</span></span> | <span data-ttu-id="b62c1-295">설명</span><span class="sxs-lookup"><span data-stu-id="b62c1-295">Description</span></span> |
|--------|--------|
| <span data-ttu-id="b62c1-296">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="b62c1-296">RestoreSources</span></span> | <span data-ttu-id="b62c1-297">세미콜론으로 구분된 패키지 원본의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-297">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="b62c1-298">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="b62c1-298">RestorePackagesPath</span></span> | <span data-ttu-id="b62c1-299">사용자 패키지 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-299">User packages folder path.</span></span> |
| <span data-ttu-id="b62c1-300">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="b62c1-300">RestoreDisableParallel</span></span> | <span data-ttu-id="b62c1-301">다운로드를 한 번에 하나씩으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-301">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="b62c1-302">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="b62c1-302">RestoreConfigFile</span></span> | <span data-ttu-id="b62c1-303">적용할 `Nuget.Config` 파일에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-303">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="b62c1-304">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="b62c1-304">RestoreNoCache</span></span> | <span data-ttu-id="b62c1-305">true이면 웹 캐시를 사용하지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-305">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="b62c1-306">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="b62c1-306">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="b62c1-307">true이면 실패했거나 누락된 패키지 원본을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-307">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="b62c1-308">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="b62c1-308">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="b62c1-309">`NuGet.Build.Tasks.dll`에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-309">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="b62c1-310">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="b62c1-310">RestoreGraphProjectInput</span></span> | <span data-ttu-id="b62c1-311">세미콜론으로 구분된 복원할 프로젝트의 목록이며, 절대 경로가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-311">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="b62c1-312">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="b62c1-312">RestoreOutputPath</span></span> | <span data-ttu-id="b62c1-313">출력 폴더이며, 기본값은 `obj` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-313">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="b62c1-314">예제</span><span class="sxs-lookup"><span data-stu-id="b62c1-314">Examples</span></span>

<span data-ttu-id="b62c1-315">명령줄:</span><span class="sxs-lookup"><span data-stu-id="b62c1-315">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="b62c1-316">프로젝트 파일:</span><span class="sxs-lookup"><span data-stu-id="b62c1-316">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="b62c1-317">restore 출력</span><span class="sxs-lookup"><span data-stu-id="b62c1-317">Restore outputs</span></span>

<span data-ttu-id="b62c1-318">restore는 `obj` 빌드 폴더에 다음 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-318">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="b62c1-319">파일</span><span class="sxs-lookup"><span data-stu-id="b62c1-319">File</span></span> | <span data-ttu-id="b62c1-320">설명</span><span class="sxs-lookup"><span data-stu-id="b62c1-320">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="b62c1-321">이전의 `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="b62c1-321">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="b62c1-322">패키지에 포함된 MSBuild props 파일에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="b62c1-322">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="b62c1-323">패키지에 포함된 MSBuild targets 파일에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="b62c1-323">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="b62c1-324">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="b62c1-324">PackageTargetFallback</span></span>

<span data-ttu-id="b62c1-325">`PackageTargetFallback` 요소를 사용하면 패키지를 복원할 때 사용할 호환 가능한 대상 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-325">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="b62c1-326">dotnet [TxM](../reference/target-frameworks.md)을 사용하는 패키지가 dotnet TxM을 선언하지 않은 호환 패키지와 함께 작동하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-326">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="b62c1-327">즉 프로젝트에서 dotnet TxM을 사용하는 경우, 비dotnet 플랫폼이 dotnet과 호환될 수 있도록 이상 프로젝트에 `<PackageTargetFallback>`을 추가하지 않는 한, 종속되는 모든 패키지에도 dotnet TxM이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-327">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="b62c1-328">예를 들어 프로젝트에서 `netstandard1.6` TxM을 사용하고 종속 패키지에 `lib/net45/a.dll` 및 `lib/portable-net45+win81/a.dll`만 포함되어 있으면 프로젝트 빌드에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-328">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="b62c1-329">가져오려는 항목이 후자의 DLL이면 다음과 같이 `PackageTargetFallback`을 추가하여 `portable-net45+win81` DLL이 호환 가능하다고 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-329">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="b62c1-330">프로젝트의 모든 대상에 대해 대체(fallback)를 선언하려면 `Condition` 특성을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-330">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="b62c1-331">또한 다음과 같이 `$(PackageTargetFallback)`을 포함하여 기존 `PackageTargetFallback`을 확장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-331">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="b62c1-332">복원 그래프에서 단일 라이브러리 대체</span><span class="sxs-lookup"><span data-stu-id="b62c1-332">Replacing one library from a restore graph</span></span>

<span data-ttu-id="b62c1-333">restore에서 잘못된 어셈블리를 가져오는 경우 해당 패키지의 기본 선택 항목을 제외하는 한편 원하는 선택 항목으로 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-333">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="b62c1-334">먼저 최상위 `PackageReference`를 사용하여 모든 자산을 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-334">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="b62c1-335">그런 다음 DLL의 적절한 로컬 복사본에 대한 고유한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b62c1-335">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
