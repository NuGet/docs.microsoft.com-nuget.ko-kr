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
ms.openlocfilehash: 6c488f49e12b014e7bd197d57041745387a4d7b4
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="5f4dc-104">MSBuild 대상으로서의 NuGet pack 및 restore</span><span class="sxs-lookup"><span data-stu-id="5f4dc-104">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="5f4dc-105">*NuGet 4.0 이상*</span><span class="sxs-lookup"><span data-stu-id="5f4dc-105">*NuGet 4.0+*</span></span>

<span data-ttu-id="5f4dc-106">NuGet 4.0 이상 PackageReference 형식으로 별도 사용 하 여 보다는 프로젝트 파일 내에서 직접 모든 매니페스트 메타 데이터를 저장할 수 `.nuspec` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-106">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="5f4dc-107">MSBuild 15.1 이상에서 NuGet은 아래에서 설명한 대로 `pack` 및 `restore` 대상이 있는 일류 MSBuild 시민이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-107">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="5f4dc-108">이러한 대상을 사용하면 다른 MSBuild 작업 또는 대상과 마찬가지로 NuGet을 사용하여 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-108">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="5f4dc-109">(NuGet 3.x 및 이전 버전의 경우 NuGet CLI를 통해 [pack](../tools/cli-ref-pack.md) 및 [restore](../tools/cli-ref-restore.md) 명령을 대신 사용합니다.)</span><span class="sxs-lookup"><span data-stu-id="5f4dc-109">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="5f4dc-110">대상 빌드 순서</span><span class="sxs-lookup"><span data-stu-id="5f4dc-110">Target build order</span></span>

<span data-ttu-id="5f4dc-111">`pack` 및 `restore`는 MSBuild 대상이므로 이 대상에 액세스하여 워크플로를 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="5f4dc-112">예를 들어 패키지를 압축한 후 네트워크 공유에 복사한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="5f4dc-113">이렇게 하려면 프로젝트 파일에 다음을 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

<span data-ttu-id="5f4dc-114">마찬가지로, MSBuild 작업을 작성하고, 고유한 대상을 작성하고, MSBuild 작업에서 NuGet 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="5f4dc-115">pack 대상</span><span class="sxs-lookup"><span data-stu-id="5f4dc-115">pack target</span></span>

<span data-ttu-id="5f4dc-116">즉, 팩 대상을 사용 하는 경우 `msbuild /t:pack`, MSBuild 프로젝트 파일에서 입력을 그립니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-116">When using the pack target, that is, `msbuild /t:pack`, MSBuild draws its inputs from the project file.</span></span> <span data-ttu-id="5f4dc-117">다음 표에서 첫 번째 내에서 프로젝트 파일에 추가할 수 있는 MSBuild 속성을 설명 `<PropertyGroup>` 노드.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-117">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="5f4dc-118">Visual Studio 2017 이상에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **{project_name} 편집**을 선택하여 이러한 편집 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-118">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="5f4dc-119">편의상 이 표는 [`.nuspec` 파일 ](../reference/nuspec.md)에 있는 동등한 속성으로 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-119">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="5f4dc-120">`.nuspec`의 `Owners` 및 `Summary` 속성은 MSBuild에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-120">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="5f4dc-121">특성/NuSpec 값</span><span class="sxs-lookup"><span data-stu-id="5f4dc-121">Attribute/NuSpec Value</span></span> | <span data-ttu-id="5f4dc-122">MSBuild 속성</span><span class="sxs-lookup"><span data-stu-id="5f4dc-122">MSBuild Property</span></span> | <span data-ttu-id="5f4dc-123">기본</span><span class="sxs-lookup"><span data-stu-id="5f4dc-123">Default</span></span> | <span data-ttu-id="5f4dc-124">노트</span><span class="sxs-lookup"><span data-stu-id="5f4dc-124">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="5f4dc-125">ID</span><span class="sxs-lookup"><span data-stu-id="5f4dc-125">Id</span></span> | <span data-ttu-id="5f4dc-126">PackageId</span><span class="sxs-lookup"><span data-stu-id="5f4dc-126">PackageId</span></span> | <span data-ttu-id="5f4dc-127">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="5f4dc-127">AssemblyName</span></span> | <span data-ttu-id="5f4dc-128">MSBuild의 $(AssemblyName)입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-128">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="5f4dc-129">버전</span><span class="sxs-lookup"><span data-stu-id="5f4dc-129">Version</span></span> | <span data-ttu-id="5f4dc-130">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="5f4dc-130">PackageVersion</span></span> | <span data-ttu-id="5f4dc-131">버전</span><span class="sxs-lookup"><span data-stu-id="5f4dc-131">Version</span></span> | <span data-ttu-id="5f4dc-132">"1.0.0", "1.0.0-beta" 또는 "1.0.0-beta-00345"와 같이 semver와 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-132">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="5f4dc-133">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5f4dc-133">VersionPrefix</span></span> | <span data-ttu-id="5f4dc-134">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="5f4dc-134">PackageVersionPrefix</span></span> | <span data-ttu-id="5f4dc-135">비어 있음</span><span class="sxs-lookup"><span data-stu-id="5f4dc-135">empty</span></span> | <span data-ttu-id="5f4dc-136">PackageVersionPrefix 덮어씁니다 PackageVersion 설정</span><span class="sxs-lookup"><span data-stu-id="5f4dc-136">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="5f4dc-137">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5f4dc-137">VersionSuffix</span></span> | <span data-ttu-id="5f4dc-138">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="5f4dc-138">PackageVersionSuffix</span></span> | <span data-ttu-id="5f4dc-139">비어 있음</span><span class="sxs-lookup"><span data-stu-id="5f4dc-139">empty</span></span> | <span data-ttu-id="5f4dc-140">MSBuild의 $(VersionSuffix)입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-140">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="5f4dc-141">PackageVersionSuffix 덮어씁니다 PackageVersion 설정</span><span class="sxs-lookup"><span data-stu-id="5f4dc-141">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="5f4dc-142">만든 이</span><span class="sxs-lookup"><span data-stu-id="5f4dc-142">Authors</span></span> | <span data-ttu-id="5f4dc-143">만든 이</span><span class="sxs-lookup"><span data-stu-id="5f4dc-143">Authors</span></span> | <span data-ttu-id="5f4dc-144">현재 사용자의 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="5f4dc-144">Username of the current user</span></span> | |
| <span data-ttu-id="5f4dc-145">Owners</span><span class="sxs-lookup"><span data-stu-id="5f4dc-145">Owners</span></span> | <span data-ttu-id="5f4dc-146">N/A</span><span class="sxs-lookup"><span data-stu-id="5f4dc-146">N/A</span></span> | <span data-ttu-id="5f4dc-147">NuSpec에는 없음</span><span class="sxs-lookup"><span data-stu-id="5f4dc-147">Not present in NuSpec</span></span> | |
| <span data-ttu-id="5f4dc-148">제목</span><span class="sxs-lookup"><span data-stu-id="5f4dc-148">Title</span></span> | <span data-ttu-id="5f4dc-149">제목</span><span class="sxs-lookup"><span data-stu-id="5f4dc-149">Title</span></span> | <span data-ttu-id="5f4dc-150">PackageId</span><span class="sxs-lookup"><span data-stu-id="5f4dc-150">The PackageId</span></span>| |
| <span data-ttu-id="5f4dc-151">설명</span><span class="sxs-lookup"><span data-stu-id="5f4dc-151">Description</span></span> | <span data-ttu-id="5f4dc-152">설명</span><span class="sxs-lookup"><span data-stu-id="5f4dc-152">Description</span></span> | <span data-ttu-id="5f4dc-153">"패키지 설명"</span><span class="sxs-lookup"><span data-stu-id="5f4dc-153">"Package Description"</span></span> | |
| <span data-ttu-id="5f4dc-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="5f4dc-154">Copyright</span></span> | <span data-ttu-id="5f4dc-155">Copyright</span><span class="sxs-lookup"><span data-stu-id="5f4dc-155">Copyright</span></span> | <span data-ttu-id="5f4dc-156">비어 있음</span><span class="sxs-lookup"><span data-stu-id="5f4dc-156">empty</span></span> | |
| <span data-ttu-id="5f4dc-157">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5f4dc-157">RequireLicenseAcceptance</span></span> | <span data-ttu-id="5f4dc-158">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5f4dc-158">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="5f4dc-159">False</span><span class="sxs-lookup"><span data-stu-id="5f4dc-159">false</span></span> | |
| <span data-ttu-id="5f4dc-160">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5f4dc-160">LicenseUrl</span></span> | <span data-ttu-id="5f4dc-161">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5f4dc-161">PackageLicenseUrl</span></span> | <span data-ttu-id="5f4dc-162">비어 있음</span><span class="sxs-lookup"><span data-stu-id="5f4dc-162">empty</span></span> | |
| <span data-ttu-id="5f4dc-163">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5f4dc-163">ProjectUrl</span></span> | <span data-ttu-id="5f4dc-164">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5f4dc-164">PackageProjectUrl</span></span> | <span data-ttu-id="5f4dc-165">비어 있음</span><span class="sxs-lookup"><span data-stu-id="5f4dc-165">empty</span></span> | |
| <span data-ttu-id="5f4dc-166">IconUrl</span><span class="sxs-lookup"><span data-stu-id="5f4dc-166">IconUrl</span></span> | <span data-ttu-id="5f4dc-167">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5f4dc-167">PackageIconUrl</span></span> | <span data-ttu-id="5f4dc-168">비어 있음</span><span class="sxs-lookup"><span data-stu-id="5f4dc-168">empty</span></span> | |
| <span data-ttu-id="5f4dc-169">Tags</span><span class="sxs-lookup"><span data-stu-id="5f4dc-169">Tags</span></span> | <span data-ttu-id="5f4dc-170">PackageTags</span><span class="sxs-lookup"><span data-stu-id="5f4dc-170">PackageTags</span></span> | <span data-ttu-id="5f4dc-171">비어 있음</span><span class="sxs-lookup"><span data-stu-id="5f4dc-171">empty</span></span> | <span data-ttu-id="5f4dc-172">세미콜론으로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-172">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="5f4dc-173">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5f4dc-173">ReleaseNotes</span></span> | <span data-ttu-id="5f4dc-174">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5f4dc-174">PackageReleaseNotes</span></span> | <span data-ttu-id="5f4dc-175">비어 있음</span><span class="sxs-lookup"><span data-stu-id="5f4dc-175">empty</span></span> | |
| <span data-ttu-id="5f4dc-176">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="5f4dc-176">RepositoryUrl</span></span> | <span data-ttu-id="5f4dc-177">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="5f4dc-177">RepositoryUrl</span></span> | <span data-ttu-id="5f4dc-178">비어 있음</span><span class="sxs-lookup"><span data-stu-id="5f4dc-178">empty</span></span> | |
| <span data-ttu-id="5f4dc-179">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="5f4dc-179">RepositoryType</span></span> | <span data-ttu-id="5f4dc-180">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="5f4dc-180">RepositoryType</span></span> | <span data-ttu-id="5f4dc-181">비어 있음</span><span class="sxs-lookup"><span data-stu-id="5f4dc-181">empty</span></span> | |
| <span data-ttu-id="5f4dc-182">PackageType</span><span class="sxs-lookup"><span data-stu-id="5f4dc-182">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="5f4dc-183">요약</span><span class="sxs-lookup"><span data-stu-id="5f4dc-183">Summary</span></span> | <span data-ttu-id="5f4dc-184">지원 안 함</span><span class="sxs-lookup"><span data-stu-id="5f4dc-184">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="5f4dc-185">pack 대상 입력</span><span class="sxs-lookup"><span data-stu-id="5f4dc-185">pack target inputs</span></span>

- <span data-ttu-id="5f4dc-186">IsPackable</span><span class="sxs-lookup"><span data-stu-id="5f4dc-186">IsPackable</span></span>
- <span data-ttu-id="5f4dc-187">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="5f4dc-187">PackageVersion</span></span>
- <span data-ttu-id="5f4dc-188">PackageId</span><span class="sxs-lookup"><span data-stu-id="5f4dc-188">PackageId</span></span>
- <span data-ttu-id="5f4dc-189">만든 이</span><span class="sxs-lookup"><span data-stu-id="5f4dc-189">Authors</span></span>
- <span data-ttu-id="5f4dc-190">설명</span><span class="sxs-lookup"><span data-stu-id="5f4dc-190">Description</span></span>
- <span data-ttu-id="5f4dc-191">Copyright</span><span class="sxs-lookup"><span data-stu-id="5f4dc-191">Copyright</span></span>
- <span data-ttu-id="5f4dc-192">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="5f4dc-192">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="5f4dc-193">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="5f4dc-193">DevelopmentDependency</span></span>
- <span data-ttu-id="5f4dc-194">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="5f4dc-194">PackageLicenseUrl</span></span>
- <span data-ttu-id="5f4dc-195">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="5f4dc-195">PackageProjectUrl</span></span>
- <span data-ttu-id="5f4dc-196">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5f4dc-196">PackageIconUrl</span></span>
- <span data-ttu-id="5f4dc-197">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="5f4dc-197">PackageReleaseNotes</span></span>
- <span data-ttu-id="5f4dc-198">PackageTags</span><span class="sxs-lookup"><span data-stu-id="5f4dc-198">PackageTags</span></span>
- <span data-ttu-id="5f4dc-199">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="5f4dc-199">PackageOutputPath</span></span>
- <span data-ttu-id="5f4dc-200">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="5f4dc-200">IncludeSymbols</span></span>
- <span data-ttu-id="5f4dc-201">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="5f4dc-201">IncludeSource</span></span>
- <span data-ttu-id="5f4dc-202">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="5f4dc-202">PackageTypes</span></span>
- <span data-ttu-id="5f4dc-203">IsTool</span><span class="sxs-lookup"><span data-stu-id="5f4dc-203">IsTool</span></span>
- <span data-ttu-id="5f4dc-204">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="5f4dc-204">RepositoryUrl</span></span>
- <span data-ttu-id="5f4dc-205">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="5f4dc-205">RepositoryType</span></span>
- <span data-ttu-id="5f4dc-206">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="5f4dc-206">NoPackageAnalysis</span></span>
- <span data-ttu-id="5f4dc-207">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="5f4dc-207">MinClientVersion</span></span>
- <span data-ttu-id="5f4dc-208">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="5f4dc-208">IncludeBuildOutput</span></span>
- <span data-ttu-id="5f4dc-209">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="5f4dc-209">IncludeContentInPack</span></span>
- <span data-ttu-id="5f4dc-210">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="5f4dc-210">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="5f4dc-211">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="5f4dc-211">ContentTargetFolders</span></span>
- <span data-ttu-id="5f4dc-212">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="5f4dc-212">NuspecFile</span></span>
- <span data-ttu-id="5f4dc-213">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="5f4dc-213">NuspecBasePath</span></span>
- <span data-ttu-id="5f4dc-214">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="5f4dc-214">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="5f4dc-215">pack 시나리오</span><span class="sxs-lookup"><span data-stu-id="5f4dc-215">pack scenarios</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="5f4dc-216">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="5f4dc-216">PackageIconUrl</span></span>

<span data-ttu-id="5f4dc-217">[NuGet 문제 2582](https://github.com/NuGet/Home/issues/2582)에 대한 변경의 일부로서 `PackageIconUrl`은 최종적으로 `PackageIconUri`로 변경되며, 결과 패키지의 루트에 포함될 아이콘 파일에 대한 상대 경로일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-217">As part of the change for [NuGet Issue 2582](https://github.com/NuGet/Home/issues/2582), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="5f4dc-218">출력 어셈블리</span><span class="sxs-lookup"><span data-stu-id="5f4dc-218">Output assemblies</span></span>

<span data-ttu-id="5f4dc-219">`nuget pack`은 `.exe`, `.dll`, `.xml`, `.winmd`, `.json` 및 `.pri` 확장명의 출력 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-219">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="5f4dc-220">복사되는 출력 파일은 `BuiltOutputProjectGroup` 대상에서 제공하는 MSBuild에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-220">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="5f4dc-221">프로젝트 파일 또는 명령줄에서 출력 어셈블리의 위치를 제어하는 데 사용할 수 있는 두 가지 MSBuild 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-221">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="5f4dc-222">`IncludeBuildOutput`: 빌드 출력 어셈블리를 패키지에 포함할지 여부를 결정하는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-222">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="5f4dc-223">`BuildOutputTargetFolder`: 출력 어셈블리를 배치할 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-223">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="5f4dc-224">출력 어셈블리(및 기타 출력 파일)는 해당 프레임워크 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-224">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="5f4dc-225">패키지 참조</span><span class="sxs-lookup"><span data-stu-id="5f4dc-225">Package references</span></span>

<span data-ttu-id="5f4dc-226">[프로젝트 파일의 패키지 참조](../consume-packages/package-references-in-project-files.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-226">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="5f4dc-227">프로젝트 간 참조</span><span class="sxs-lookup"><span data-stu-id="5f4dc-227">Project to project references</span></span>

<span data-ttu-id="5f4dc-228">프로젝트 간 참조는 기본적으로 NuGet 패키지 참조로 간주됩니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-228">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="5f4dc-229">또한 다음 메타데이터를 프로젝트 참조에 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-229">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="5f4dc-230">패키지에 내용 포함</span><span class="sxs-lookup"><span data-stu-id="5f4dc-230">Including content in a package</span></span>

<span data-ttu-id="5f4dc-231">콘텐츠를 포함하려면 기존 `<Content>` 항목에 추가 메타데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-231">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="5f4dc-232">기본적으로 "Content" 형식의 모든 항목은 다음과 같은 항목으로 재정의하지 않는 한 패키지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-232">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
    <Content Include="..\win7-x64\libuv.txt">
        <Pack>false</Pack>
    </Content>
 ```

<span data-ttu-id="5f4dc-233">패키지 경로를 지정하지 않으면 기본적으로 `content` 및 `contentFiles\any\<target_framework>` 패키지 폴더의 루트에 모든 항목이 추가되고 상대 폴더 구조가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-233">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="5f4dc-234">모든 내용을 특정 루트 폴더(`content` 및 `contentFiles` 대신)에만 복사하려면 `ContentTargetFolders` MSBuild 속성을 사용할 수 있습니다. 이 속성은 기본적으로 "content; contentFiles"이지만 다른 폴더 이름으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-234">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="5f4dc-235">`ContentTargetFolders`에 "contentFiles"를 지정하면 파일이 `buildAction`에 따라 `contentFiles\any\<target_framework>` 또는 `contentFiles\<language>\<target_framework>`에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-235">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="5f4dc-236">`PackagePath`는 세미콜론으로 구분된 대상 경로의 집합일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-236">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="5f4dc-237">빈 패키지 경로를 지정하면 파일이 패키지의 루트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-237">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="5f4dc-238">예를 들어 다음은 `libuv.txt`를 `content\myfiles`, `content\samples` 및 패키지 루트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-238">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="5f4dc-239">또한 `$(IncludeContentInPack)` MSBuild 속성이 있으며 기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-239">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="5f4dc-240">모든 프로젝트에서 이 값을 `false`로 설정하면 해당 프로젝트의 내용이 NuGet 패키지에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-240">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="5f4dc-241">위의 항목 중 하나에서 설정할 수 있는 다른 pack 특정 메타데이터에는 nuspec 출력의 ```contentFiles``` 항목에 ```CopyToOutput``` 및 ```Flatten``` 값을 설정하는 ```<PackageCopyToOutput>``` 및 ```<PackageFlatten>```이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-241">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="5f4dc-242">콘텐츠 항목을 별개로 `<Pack>` 및 `<PackagePath>` 컴파일, 포함 리소스, ApplicationDefinition, 페이지, 리소스, 시작 화면, DesignData, DesignDataWithDesignTimeCreateableTypes 빌드 작업을 사용 하 여 파일에서 메타 데이터를 설정할 수도 있습니다 CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource 또는 None입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-242">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="5f4dc-243">GLOB 패턴을 사용할 때 pack에서 파일 이름을 패키지 경로에 추가하려면 패키지 경로가 폴더 구분 문자로 끝나야 합니다. 그렇지 않으면 패키지 경로가 파일 이름을 포함한 전체 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-243">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="5f4dc-244">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="5f4dc-244">IncludeSymbols</span></span>

<span data-ttu-id="5f4dc-245">`MSBuild /t:pack /p:IncludeSymbols=true`를 사용하면 해당 `.pdb` 파일이 다른 출력 파일(`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`)과 함께 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-245">When using `MSBuild /t:pack /p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="5f4dc-246">`IncludeSymbols=true`를 설정하면 일반 패키지 *및* 기호 패키지가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-246">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="5f4dc-247">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="5f4dc-247">IncludeSource</span></span>

<span data-ttu-id="5f4dc-248">`.pdb` 파일과 함께 원본 파일을 복사한다는 점을 제외하고는 `IncludeSymbols`와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-248">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="5f4dc-249">`Compile` 형식의 모든 파일이 결과 패키지에서 상대 경로 폴더 구조를 유지하면서 `src\<ProjectName>\`에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-249">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="5f4dc-250">또한 `TreatAsPackageReference`가 `false`로 설정된 `ProjectReference`의 원본 파일에 대해서도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-250">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="5f4dc-251">Compile 형식의 파일이 프로젝트 폴더의 외부에 있는 경우 이 파일은 `src\<ProjectName>\`에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-251">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="istool"></a><span data-ttu-id="5f4dc-252">IsTool</span><span class="sxs-lookup"><span data-stu-id="5f4dc-252">IsTool</span></span>

<span data-ttu-id="5f4dc-253">`MSBuild /t:pack /p:IsTool=true`를 사용하면 [출력 어셈블리](#output-assemblies) 시나리오에서 지정한 대로 모든 출력 파일이 `lib` 폴더 대신 `tools` 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-253">When using `MSBuild /t:pack /p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="5f4dc-254">이는 `.csproj` 파일에서 `PackageType`을 설정하여 지정된 `DotNetCliTool`과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-254">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="5f4dc-255">.nuspec을 사용하여 압축</span><span class="sxs-lookup"><span data-stu-id="5f4dc-255">Packing using a .nuspec</span></span>

<span data-ttu-id="5f4dc-256">pack 작업을 실행할 수 있도록 `NuGet.Build.Tasks.Pack.targets`를 가져오는 프로젝트 파일이 있는 경우 `.nuspec` 파일을 사용하여 프로젝트를 압축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-256">You can use a `.nuspec` file to pack your project provided that you have a project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="5f4dc-257">다음 세 가지 MSBuild 속성은 `.nuspec`을 사용하여 압축하는 것과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-257">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="5f4dc-258">`NuspecFile`: 압축에 사용되는 `.nuspec` 파일에 대한 상대 또는 절대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-258">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="5f4dc-259">`NuspecProperties`: 세미콜론으로 구분된 key=value 쌍의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-259">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="5f4dc-260">MSBuild 명령줄 구문 분석이 작동하는 방식으로 인해 여러 속성을 `/p:NuspecProperties=\"key1=value1;key2=value2\"`와 같이 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-260">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `/p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="5f4dc-261">`NuspecBasePath`: `.nuspec` 파일에 대한 기본 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-261">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="5f4dc-262">`dotnet.exe`를 사용하여 프로젝트를 압축하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-262">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="5f4dc-263">MSBuild를 사용하여 프로젝트를 압축하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-263">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a><span data-ttu-id="5f4dc-264">restore 대상</span><span class="sxs-lookup"><span data-stu-id="5f4dc-264">restore target</span></span>

<span data-ttu-id="5f4dc-265">`MSBuild /t:restore`(.NET Core 프로젝트에서 `nuget restore` 및 `dotnet restore` 사용)는 프로젝트 파일에서 참조된 패키지를 다음과 같이 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-265">`MSBuild /t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="5f4dc-266">모든 프로젝트 간 참조를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-266">Read all project to project references</span></span>
1. <span data-ttu-id="5f4dc-267">프로젝트 속성을 읽어 중간 폴더 및 대상 프레임워크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-267">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="5f4dc-268">msbuild 데이터를 NuGet.Build.Tasks.dll에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-268">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="5f4dc-269">restore를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-269">Run restore</span></span>
1. <span data-ttu-id="5f4dc-270">패키지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-270">Download packages</span></span>
1. <span data-ttu-id="5f4dc-271">자산, targets 및 props 파일을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-271">Write assets file, targets, and props</span></span>

### <a name="restore-properties"></a><span data-ttu-id="5f4dc-272">restore 속성</span><span class="sxs-lookup"><span data-stu-id="5f4dc-272">Restore properties</span></span>

<span data-ttu-id="5f4dc-273">추가 restore 설정은 프로젝트 파일의 MSBuild 속성에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-273">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="5f4dc-274">또한 값은 `/p:` 스위치를 사용하여 명령줄에서 설정할 수 있습니다(아래 예제 참조).</span><span class="sxs-lookup"><span data-stu-id="5f4dc-274">Values can also be set from the command line using the `/p:` switch (see Examples below).</span></span>

| <span data-ttu-id="5f4dc-275">속성</span><span class="sxs-lookup"><span data-stu-id="5f4dc-275">Property</span></span> | <span data-ttu-id="5f4dc-276">설명</span><span class="sxs-lookup"><span data-stu-id="5f4dc-276">Description</span></span> |
|--------|--------|
| <span data-ttu-id="5f4dc-277">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="5f4dc-277">RestoreSources</span></span> | <span data-ttu-id="5f4dc-278">세미콜론으로 구분된 패키지 원본의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-278">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="5f4dc-279">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="5f4dc-279">RestorePackagesPath</span></span> | <span data-ttu-id="5f4dc-280">사용자 패키지 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-280">User packages folder path.</span></span> |
| <span data-ttu-id="5f4dc-281">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="5f4dc-281">RestoreDisableParallel</span></span> | <span data-ttu-id="5f4dc-282">다운로드를 한 번에 하나씩으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-282">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="5f4dc-283">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="5f4dc-283">RestoreConfigFile</span></span> | <span data-ttu-id="5f4dc-284">적용할 `Nuget.Config` 파일에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-284">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="5f4dc-285">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="5f4dc-285">RestoreNoCache</span></span> | <span data-ttu-id="5f4dc-286">true이면 웹 캐시를 사용하지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-286">If true, avoids using the web cache.</span></span> |
| <span data-ttu-id="5f4dc-287">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="5f4dc-287">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="5f4dc-288">true이면 실패했거나 누락된 패키지 원본을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-288">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="5f4dc-289">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="5f4dc-289">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="5f4dc-290">`NuGet.Build.Tasks.dll`에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-290">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="5f4dc-291">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="5f4dc-291">RestoreGraphProjectInput</span></span> | <span data-ttu-id="5f4dc-292">세미콜론으로 구분된 복원할 프로젝트의 목록이며, 절대 경로가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-292">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="5f4dc-293">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="5f4dc-293">RestoreOutputPath</span></span> | <span data-ttu-id="5f4dc-294">출력 폴더이며, 기본값은 `obj` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-294">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="5f4dc-295">예제</span><span class="sxs-lookup"><span data-stu-id="5f4dc-295">Examples</span></span>

<span data-ttu-id="5f4dc-296">명령줄:</span><span class="sxs-lookup"><span data-stu-id="5f4dc-296">Command line:</span></span>

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

<span data-ttu-id="5f4dc-297">프로젝트 파일:</span><span class="sxs-lookup"><span data-stu-id="5f4dc-297">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="5f4dc-298">restore 출력</span><span class="sxs-lookup"><span data-stu-id="5f4dc-298">Restore outputs</span></span>

<span data-ttu-id="5f4dc-299">restore는 `obj` 빌드 폴더에 다음 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-299">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="5f4dc-300">파일</span><span class="sxs-lookup"><span data-stu-id="5f4dc-300">File</span></span> | <span data-ttu-id="5f4dc-301">설명</span><span class="sxs-lookup"><span data-stu-id="5f4dc-301">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="5f4dc-302">이전의 `project.lock.json`</span><span class="sxs-lookup"><span data-stu-id="5f4dc-302">Previously `project.lock.json`</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="5f4dc-303">패키지에 포함된 MSBuild props 파일에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="5f4dc-303">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="5f4dc-304">패키지에 포함된 MSBuild targets 파일에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="5f4dc-304">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="5f4dc-305">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="5f4dc-305">PackageTargetFallback</span></span>

<span data-ttu-id="5f4dc-306">`PackageTargetFallback` 요소를 사용하면 패키지를 복원할 때 사용할 호환 가능한 대상 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-306">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="5f4dc-307">dotnet [TxM](../reference/target-frameworks.md)을 사용하는 패키지가 dotnet TxM을 선언하지 않은 호환 패키지와 함께 작동하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-307">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="5f4dc-308">즉 프로젝트에서 dotnet TxM을 사용하는 경우, 비dotnet 플랫폼이 dotnet과 호환될 수 있도록 이상 프로젝트에 `<PackageTargetFallback>`을 추가하지 않는 한, 종속되는 모든 패키지에도 dotnet TxM이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-308">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="5f4dc-309">예를 들어 프로젝트에서 `netstandard1.6` TxM을 사용하고 종속 패키지에 `lib/net45/a.dll` 및 `lib/portable-net45+win81/a.dll`만 포함되어 있으면 프로젝트 빌드에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-309">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="5f4dc-310">가져오려는 항목이 후자의 DLL이면 다음과 같이 `PackageTargetFallback`을 추가하여 `portable-net45+win81` DLL이 호환 가능하다고 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-310">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="5f4dc-311">프로젝트의 모든 대상에 대해 대체(fallback)를 선언하려면 `Condition` 특성을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-311">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="5f4dc-312">또한 다음과 같이 `$(PackageTargetFallback)`을 포함하여 기존 `PackageTargetFallback`을 확장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-312">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="5f4dc-313">복원 그래프에서 단일 라이브러리 대체</span><span class="sxs-lookup"><span data-stu-id="5f4dc-313">Replacing one library from a restore graph</span></span>

<span data-ttu-id="5f4dc-314">restore에서 잘못된 어셈블리를 가져오는 경우 해당 패키지의 기본 선택 항목을 제외하는 한편 원하는 선택 항목으로 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-314">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="5f4dc-315">먼저 최상위 `PackageReference`를 사용하여 모든 자산을 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-315">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
    <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="5f4dc-316">그런 다음 DLL의 적절한 로컬 복사본에 대한 고유한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="5f4dc-316">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
