---
title: MSBuild 대상으로서의 NuGet pack 및 restore
description: NuGet pack 및 restore는 NuGet 4.0 이상에서 MSBuild 대상으로 직접 작동할 수 있습니다.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 8132595cbfaf553736fbcc81aada283a44d6cdbf
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324853"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="d2e75-103">MSBuild 대상으로서의 NuGet pack 및 restore</span><span class="sxs-lookup"><span data-stu-id="d2e75-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="d2e75-104">*NuGet 4.0 이상*</span><span class="sxs-lookup"><span data-stu-id="d2e75-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="d2e75-105">PackageReference 형식을 사용하면 NuGet 4.0 이상은 별도의 `.nuspec` 파일을 사용하는 대신 프로젝트 파일 내에서 모든 매니페스트 메타데이터를 직접 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-105">With the PackageReference format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="d2e75-106">MSBuild 15.1 이상에서 NuGet은 아래에서 설명한 대로 `pack` 및 `restore` 대상이 있는 일류 MSBuild 시민이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="d2e75-107">이러한 대상을 사용하면 다른 MSBuild 작업 또는 대상과 마찬가지로 NuGet을 사용하여 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="d2e75-108">(NuGet 3.x 및 이전 버전의 경우 NuGet CLI를 통해 [pack](../tools/cli-ref-pack.md) 및 [restore](../tools/cli-ref-restore.md) 명령을 대신 사용합니다.)</span><span class="sxs-lookup"><span data-stu-id="d2e75-108">(For NuGet 3.x and earlier, you use the [pack](../tools/cli-ref-pack.md) and [restore](../tools/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="d2e75-109">대상 빌드 순서</span><span class="sxs-lookup"><span data-stu-id="d2e75-109">Target build order</span></span>

<span data-ttu-id="d2e75-110">`pack` 및 `restore`는 MSBuild 대상이므로 이 대상에 액세스하여 워크플로를 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-110">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="d2e75-111">예를 들어 패키지를 압축한 후 네트워크 공유에 복사한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-111">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="d2e75-112">이렇게 하려면 프로젝트 파일에 다음을 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-112">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="d2e75-113">마찬가지로, MSBuild 작업을 작성하고, 고유한 대상을 작성하고, MSBuild 작업에서 NuGet 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-113">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

## <a name="pack-target"></a><span data-ttu-id="d2e75-114">pack 대상</span><span class="sxs-lookup"><span data-stu-id="d2e75-114">pack target</span></span>

<span data-ttu-id="d2e75-115">PackageReference 형식을 사용 하 여.NET Standard 프로젝트에 대 한 `msbuild -t:pack` NuGet 패키지를 만드는 데 사용할 프로젝트 파일에서 입력을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-115">For .NET Standard projects using the PackageReference format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="d2e75-116">아래 표에서는 첫 번째 `<PropertyGroup>` 노드 내에서 프로젝트 파일에 추가할 수 있는 MSBuild 속성을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-116">The table below describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="d2e75-117">Visual Studio 2017 이상에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **{project_name} 편집**을 선택하여 이러한 편집 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-117">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="d2e75-118">편의상 이 표는 [`.nuspec` 파일 ](../reference/nuspec.md)에 있는 동등한 속성으로 구성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-118">For convenience the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="d2e75-119">`.nuspec`의 `Owners` 및 `Summary` 속성은 MSBuild에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-119">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="d2e75-120">특성/NuSpec 값</span><span class="sxs-lookup"><span data-stu-id="d2e75-120">Attribute/NuSpec Value</span></span> | <span data-ttu-id="d2e75-121">MSBuild 속성</span><span class="sxs-lookup"><span data-stu-id="d2e75-121">MSBuild Property</span></span> | <span data-ttu-id="d2e75-122">기본</span><span class="sxs-lookup"><span data-stu-id="d2e75-122">Default</span></span> | <span data-ttu-id="d2e75-123">노트</span><span class="sxs-lookup"><span data-stu-id="d2e75-123">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="d2e75-124">ID</span><span class="sxs-lookup"><span data-stu-id="d2e75-124">Id</span></span> | <span data-ttu-id="d2e75-125">PackageId</span><span class="sxs-lookup"><span data-stu-id="d2e75-125">PackageId</span></span> | <span data-ttu-id="d2e75-126">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="d2e75-126">AssemblyName</span></span> | <span data-ttu-id="d2e75-127">MSBuild의 $(AssemblyName)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-127">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="d2e75-128">버전</span><span class="sxs-lookup"><span data-stu-id="d2e75-128">Version</span></span> | <span data-ttu-id="d2e75-129">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="d2e75-129">PackageVersion</span></span> | <span data-ttu-id="d2e75-130">버전</span><span class="sxs-lookup"><span data-stu-id="d2e75-130">Version</span></span> | <span data-ttu-id="d2e75-131">"1.0.0", "1.0.0-beta" 또는 "1.0.0-beta-00345"와 같이 semver와 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-131">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="d2e75-132">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="d2e75-132">VersionPrefix</span></span> | <span data-ttu-id="d2e75-133">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="d2e75-133">PackageVersionPrefix</span></span> | <span data-ttu-id="d2e75-134">비어 있음</span><span class="sxs-lookup"><span data-stu-id="d2e75-134">empty</span></span> | <span data-ttu-id="d2e75-135">PackageVersion을 설정하면 PackageVersionPrefix를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-135">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="d2e75-136">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="d2e75-136">VersionSuffix</span></span> | <span data-ttu-id="d2e75-137">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="d2e75-137">PackageVersionSuffix</span></span> | <span data-ttu-id="d2e75-138">비어 있음</span><span class="sxs-lookup"><span data-stu-id="d2e75-138">empty</span></span> | <span data-ttu-id="d2e75-139">MSBuild의 $(VersionSuffix)입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-139">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="d2e75-140">PackageVersion을 설정하면 PackageVersionSuffix를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-140">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="d2e75-141">만든 이</span><span class="sxs-lookup"><span data-stu-id="d2e75-141">Authors</span></span> | <span data-ttu-id="d2e75-142">만든 이</span><span class="sxs-lookup"><span data-stu-id="d2e75-142">Authors</span></span> | <span data-ttu-id="d2e75-143">현재 사용자의 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="d2e75-143">Username of the current user</span></span> | |
| <span data-ttu-id="d2e75-144">Owners</span><span class="sxs-lookup"><span data-stu-id="d2e75-144">Owners</span></span> | <span data-ttu-id="d2e75-145">N/A</span><span class="sxs-lookup"><span data-stu-id="d2e75-145">N/A</span></span> | <span data-ttu-id="d2e75-146">NuSpec에는 없음</span><span class="sxs-lookup"><span data-stu-id="d2e75-146">Not present in NuSpec</span></span> | |
| <span data-ttu-id="d2e75-147">제목</span><span class="sxs-lookup"><span data-stu-id="d2e75-147">Title</span></span> | <span data-ttu-id="d2e75-148">제목</span><span class="sxs-lookup"><span data-stu-id="d2e75-148">Title</span></span> | <span data-ttu-id="d2e75-149">PackageId</span><span class="sxs-lookup"><span data-stu-id="d2e75-149">The PackageId</span></span>| |
| <span data-ttu-id="d2e75-150">설명</span><span class="sxs-lookup"><span data-stu-id="d2e75-150">Description</span></span> | <span data-ttu-id="d2e75-151">설명</span><span class="sxs-lookup"><span data-stu-id="d2e75-151">Description</span></span> | <span data-ttu-id="d2e75-152">"패키지 설명"</span><span class="sxs-lookup"><span data-stu-id="d2e75-152">"Package Description"</span></span> | |
| <span data-ttu-id="d2e75-153">Copyright</span><span class="sxs-lookup"><span data-stu-id="d2e75-153">Copyright</span></span> | <span data-ttu-id="d2e75-154">Copyright</span><span class="sxs-lookup"><span data-stu-id="d2e75-154">Copyright</span></span> | <span data-ttu-id="d2e75-155">비어 있음</span><span class="sxs-lookup"><span data-stu-id="d2e75-155">empty</span></span> | |
| <span data-ttu-id="d2e75-156">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="d2e75-156">RequireLicenseAcceptance</span></span> | <span data-ttu-id="d2e75-157">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="d2e75-157">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="d2e75-158">False</span><span class="sxs-lookup"><span data-stu-id="d2e75-158">false</span></span> | |
| <span data-ttu-id="d2e75-159">라이선스</span><span class="sxs-lookup"><span data-stu-id="d2e75-159">license</span></span> | <span data-ttu-id="d2e75-160">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="d2e75-160">PackageLicenseExpression</span></span> | <span data-ttu-id="d2e75-161">비어 있음</span><span class="sxs-lookup"><span data-stu-id="d2e75-161">empty</span></span> | <span data-ttu-id="d2e75-162">에 해당 `<license type="expression">`</span><span class="sxs-lookup"><span data-stu-id="d2e75-162">Corresponds to `<license type="expression">`</span></span> |
| <span data-ttu-id="d2e75-163">라이선스</span><span class="sxs-lookup"><span data-stu-id="d2e75-163">license</span></span> | <span data-ttu-id="d2e75-164">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="d2e75-164">PackageLicenseFile</span></span> | <span data-ttu-id="d2e75-165">비어 있음</span><span class="sxs-lookup"><span data-stu-id="d2e75-165">empty</span></span> | <span data-ttu-id="d2e75-166">`<license type="file">`에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-166">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="d2e75-167">명시적으로 참조 된 라이선스 파일을 압축 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-167">You may need to explicitly pack the referenced license file.</span></span> |
| <span data-ttu-id="d2e75-168">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="d2e75-168">LicenseUrl</span></span> | <span data-ttu-id="d2e75-169">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="d2e75-169">PackageLicenseUrl</span></span> | <span data-ttu-id="d2e75-170">비어 있음</span><span class="sxs-lookup"><span data-stu-id="d2e75-170">empty</span></span> | <span data-ttu-id="d2e75-171">`licenseUrl` PackageLicenseExpression 또는 PackageLicenseFile 속성을 사용 하 여 계속</span><span class="sxs-lookup"><span data-stu-id="d2e75-171">`licenseUrl` is being deprecated, use the PackageLicenseExpression or PackageLicenseFile property</span></span> |
| <span data-ttu-id="d2e75-172">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="d2e75-172">ProjectUrl</span></span> | <span data-ttu-id="d2e75-173">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="d2e75-173">PackageProjectUrl</span></span> | <span data-ttu-id="d2e75-174">비어 있음</span><span class="sxs-lookup"><span data-stu-id="d2e75-174">empty</span></span> | |
| <span data-ttu-id="d2e75-175">IconUrl</span><span class="sxs-lookup"><span data-stu-id="d2e75-175">IconUrl</span></span> | <span data-ttu-id="d2e75-176">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="d2e75-176">PackageIconUrl</span></span> | <span data-ttu-id="d2e75-177">비어 있음</span><span class="sxs-lookup"><span data-stu-id="d2e75-177">empty</span></span> | |
| <span data-ttu-id="d2e75-178">태그</span><span class="sxs-lookup"><span data-stu-id="d2e75-178">Tags</span></span> | <span data-ttu-id="d2e75-179">PackageTags</span><span class="sxs-lookup"><span data-stu-id="d2e75-179">PackageTags</span></span> | <span data-ttu-id="d2e75-180">비어 있음</span><span class="sxs-lookup"><span data-stu-id="d2e75-180">empty</span></span> | <span data-ttu-id="d2e75-181">세미콜론으로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-181">Tags are semi-colon delimited.</span></span> |
| <span data-ttu-id="d2e75-182">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="d2e75-182">ReleaseNotes</span></span> | <span data-ttu-id="d2e75-183">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="d2e75-183">PackageReleaseNotes</span></span> | <span data-ttu-id="d2e75-184">비어 있음</span><span class="sxs-lookup"><span data-stu-id="d2e75-184">empty</span></span> | |
| <span data-ttu-id="d2e75-185">리포지토리/Url</span><span class="sxs-lookup"><span data-stu-id="d2e75-185">Repository/Url</span></span> | <span data-ttu-id="d2e75-186">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="d2e75-186">RepositoryUrl</span></span> | <span data-ttu-id="d2e75-187">비어 있음</span><span class="sxs-lookup"><span data-stu-id="d2e75-187">empty</span></span> | <span data-ttu-id="d2e75-188">복제 또는 소스 코드를 검색 하는 데 사용 되는 리포지토리 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-188">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="d2e75-189">예: *https://github.com/NuGet/NuGet.Client.git*</span><span class="sxs-lookup"><span data-stu-id="d2e75-189">Example: *https://github.com/NuGet/NuGet.Client.git*</span></span> |
| <span data-ttu-id="d2e75-190">저장소/유형</span><span class="sxs-lookup"><span data-stu-id="d2e75-190">Repository/Type</span></span> | <span data-ttu-id="d2e75-191">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="d2e75-191">RepositoryType</span></span> | <span data-ttu-id="d2e75-192">비어 있음</span><span class="sxs-lookup"><span data-stu-id="d2e75-192">empty</span></span> | <span data-ttu-id="d2e75-193">리포지토리 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-193">Repository type.</span></span> <span data-ttu-id="d2e75-194">예: *git*하십시오 *tfs*합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-194">Examples: *git*, *tfs*.</span></span> |
| <span data-ttu-id="d2e75-195">리포지토리/분기</span><span class="sxs-lookup"><span data-stu-id="d2e75-195">Repository/Branch</span></span> | <span data-ttu-id="d2e75-196">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="d2e75-196">RepositoryBranch</span></span> | <span data-ttu-id="d2e75-197">비어 있음</span><span class="sxs-lookup"><span data-stu-id="d2e75-197">empty</span></span> | <span data-ttu-id="d2e75-198">선택적 리포지토리에서 분기 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-198">Optional repository branch information.</span></span> <span data-ttu-id="d2e75-199">*RepositoryUrl* 포함 되도록이 속성에도 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-199">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="d2e75-200">예: *마스터* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="d2e75-200">Example: *master* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="d2e75-201">저장소/커밋</span><span class="sxs-lookup"><span data-stu-id="d2e75-201">Repository/Commit</span></span> | <span data-ttu-id="d2e75-202">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="d2e75-202">RepositoryCommit</span></span> | <span data-ttu-id="d2e75-203">비어 있음</span><span class="sxs-lookup"><span data-stu-id="d2e75-203">empty</span></span> | <span data-ttu-id="d2e75-204">선택적 저장소 커밋 또는 패키지 소스를 나타내기 위해 변경 집합에 대해 구축 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-204">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="d2e75-205">*RepositoryUrl* 포함 되도록이 속성에도 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-205">*RepositoryUrl* must also be specified for this property to be included.</span></span> <span data-ttu-id="d2e75-206">예제: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span><span class="sxs-lookup"><span data-stu-id="d2e75-206">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+)</span></span> |
| <span data-ttu-id="d2e75-207">PackageType</span><span class="sxs-lookup"><span data-stu-id="d2e75-207">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="d2e75-208">요약</span><span class="sxs-lookup"><span data-stu-id="d2e75-208">Summary</span></span> | <span data-ttu-id="d2e75-209">지원 안 함</span><span class="sxs-lookup"><span data-stu-id="d2e75-209">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="d2e75-210">pack 대상 입력</span><span class="sxs-lookup"><span data-stu-id="d2e75-210">pack target inputs</span></span>

- <span data-ttu-id="d2e75-211">IsPackable</span><span class="sxs-lookup"><span data-stu-id="d2e75-211">IsPackable</span></span>
- <span data-ttu-id="d2e75-212">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="d2e75-212">SuppressDependenciesWhenPacking</span></span>
- <span data-ttu-id="d2e75-213">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="d2e75-213">PackageVersion</span></span>
- <span data-ttu-id="d2e75-214">PackageId</span><span class="sxs-lookup"><span data-stu-id="d2e75-214">PackageId</span></span>
- <span data-ttu-id="d2e75-215">만든 이</span><span class="sxs-lookup"><span data-stu-id="d2e75-215">Authors</span></span>
- <span data-ttu-id="d2e75-216">설명</span><span class="sxs-lookup"><span data-stu-id="d2e75-216">Description</span></span>
- <span data-ttu-id="d2e75-217">Copyright</span><span class="sxs-lookup"><span data-stu-id="d2e75-217">Copyright</span></span>
- <span data-ttu-id="d2e75-218">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="d2e75-218">PackageRequireLicenseAcceptance</span></span>
- <span data-ttu-id="d2e75-219">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="d2e75-219">DevelopmentDependency</span></span>
- <span data-ttu-id="d2e75-220">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="d2e75-220">PackageLicenseExpression</span></span>
- <span data-ttu-id="d2e75-221">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="d2e75-221">PackageLicenseFile</span></span>
- <span data-ttu-id="d2e75-222">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="d2e75-222">PackageLicenseUrl</span></span>
- <span data-ttu-id="d2e75-223">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="d2e75-223">PackageProjectUrl</span></span>
- <span data-ttu-id="d2e75-224">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="d2e75-224">PackageIconUrl</span></span>
- <span data-ttu-id="d2e75-225">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="d2e75-225">PackageReleaseNotes</span></span>
- <span data-ttu-id="d2e75-226">PackageTags</span><span class="sxs-lookup"><span data-stu-id="d2e75-226">PackageTags</span></span>
- <span data-ttu-id="d2e75-227">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="d2e75-227">PackageOutputPath</span></span>
- <span data-ttu-id="d2e75-228">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="d2e75-228">IncludeSymbols</span></span>
- <span data-ttu-id="d2e75-229">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="d2e75-229">IncludeSource</span></span>
- <span data-ttu-id="d2e75-230">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="d2e75-230">PackageTypes</span></span>
- <span data-ttu-id="d2e75-231">IsTool</span><span class="sxs-lookup"><span data-stu-id="d2e75-231">IsTool</span></span>
- <span data-ttu-id="d2e75-232">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="d2e75-232">RepositoryUrl</span></span>
- <span data-ttu-id="d2e75-233">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="d2e75-233">RepositoryType</span></span>
- <span data-ttu-id="d2e75-234">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="d2e75-234">RepositoryBranch</span></span>
- <span data-ttu-id="d2e75-235">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="d2e75-235">RepositoryCommit</span></span>
- <span data-ttu-id="d2e75-236">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="d2e75-236">NoPackageAnalysis</span></span>
- <span data-ttu-id="d2e75-237">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="d2e75-237">MinClientVersion</span></span>
- <span data-ttu-id="d2e75-238">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="d2e75-238">IncludeBuildOutput</span></span>
- <span data-ttu-id="d2e75-239">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="d2e75-239">IncludeContentInPack</span></span>
- <span data-ttu-id="d2e75-240">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="d2e75-240">BuildOutputTargetFolder</span></span>
- <span data-ttu-id="d2e75-241">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="d2e75-241">ContentTargetFolders</span></span>
- <span data-ttu-id="d2e75-242">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="d2e75-242">NuspecFile</span></span>
- <span data-ttu-id="d2e75-243">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="d2e75-243">NuspecBasePath</span></span>
- <span data-ttu-id="d2e75-244">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="d2e75-244">NuspecProperties</span></span>

## <a name="pack-scenarios"></a><span data-ttu-id="d2e75-245">pack 시나리오</span><span class="sxs-lookup"><span data-stu-id="d2e75-245">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="d2e75-246">종속성 표시 안 함</span><span class="sxs-lookup"><span data-stu-id="d2e75-246">Suppress dependencies</span></span>

<span data-ttu-id="d2e75-247">생성 된 NuGet 패키지에서 종속성 패키지를 표시 하지 않으려면 설정할 `SuppressDependenciesWhenPacking` 에 `true` 그러면 생성 된 nupkg 파일에서 모든 종속성을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-247">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="d2e75-248">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="d2e75-248">PackageIconUrl</span></span>

<span data-ttu-id="d2e75-249">에 대 한 변경의 일부로 [NuGet 문제 352](https://github.com/NuGet/Home/issues/352)를 `PackageIconUrl` 최종적으로 변경 됩니다 `PackageIconUri` 및 결과 패키지의 루트에 포함 될 아이콘 파일에 상대 경로가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-249">As part of the change for [NuGet Issue 352](https://github.com/NuGet/Home/issues/352), `PackageIconUrl` will eventually be changed to `PackageIconUri` and can be relative path to a icon file which will included at the root of the resulting package.</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="d2e75-250">출력 어셈블리</span><span class="sxs-lookup"><span data-stu-id="d2e75-250">Output assemblies</span></span>

<span data-ttu-id="d2e75-251">`nuget pack`은 `.exe`, `.dll`, `.xml`, `.winmd`, `.json` 및 `.pri` 확장명의 출력 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-251">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="d2e75-252">복사되는 출력 파일은 `BuiltOutputProjectGroup` 대상에서 제공하는 MSBuild에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-252">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="d2e75-253">프로젝트 파일 또는 명령줄에서 출력 어셈블리의 위치를 제어하는 데 사용할 수 있는 두 가지 MSBuild 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-253">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="d2e75-254">`IncludeBuildOutput`: 빌드 출력 어셈블리를 패키지에 포함시킬지 여부를 결정 하는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-254">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="d2e75-255">`BuildOutputTargetFolder`: 출력 어셈블리를 배치할 폴더를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-255">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="d2e75-256">출력 어셈블리(및 기타 출력 파일)는 해당 프레임워크 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-256">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="d2e75-257">패키지 참조</span><span class="sxs-lookup"><span data-stu-id="d2e75-257">Package references</span></span>

<span data-ttu-id="d2e75-258">[프로젝트 파일의 패키지 참조](../consume-packages/package-references-in-project-files.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d2e75-258">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="d2e75-259">프로젝트 간 참조</span><span class="sxs-lookup"><span data-stu-id="d2e75-259">Project to project references</span></span>

<span data-ttu-id="d2e75-260">프로젝트 간 참조는 기본적으로 NuGet 패키지 참조로 간주됩니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-260">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="d2e75-261">또한 다음 메타데이터를 프로젝트 참조에 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-261">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="d2e75-262">패키지에 내용 포함</span><span class="sxs-lookup"><span data-stu-id="d2e75-262">Including content in a package</span></span>

<span data-ttu-id="d2e75-263">콘텐츠를 포함하려면 기존 `<Content>` 항목에 추가 메타데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-263">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="d2e75-264">기본적으로 "Content" 형식의 모든 항목은 다음과 같은 항목으로 재정의하지 않는 한 패키지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-264">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="d2e75-265">패키지 경로를 지정하지 않으면 기본적으로 `content` 및 `contentFiles\any\<target_framework>` 패키지 폴더의 루트에 모든 항목이 추가되고 상대 폴더 구조가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-265">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="d2e75-266">모든 내용을 특정 루트 폴더(`content` 및 `contentFiles` 대신)에만 복사하려면 `ContentTargetFolders` MSBuild 속성을 사용할 수 있습니다. 이 속성은 기본적으로 "content; contentFiles"이지만 다른 폴더 이름으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-266">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="d2e75-267">`ContentTargetFolders`에 "contentFiles"를 지정하면 파일이 `buildAction`에 따라 `contentFiles\any\<target_framework>` 또는 `contentFiles\<language>\<target_framework>`에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-267">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="d2e75-268">`PackagePath`는 세미콜론으로 구분된 대상 경로의 집합일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-268">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="d2e75-269">빈 패키지 경로를 지정하면 파일이 패키지의 루트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-269">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="d2e75-270">예를 들어 다음은 `libuv.txt`를 `content\myfiles`, `content\samples` 및 패키지 루트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-270">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="d2e75-271">또한 `$(IncludeContentInPack)` MSBuild 속성이 있으며 기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-271">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="d2e75-272">모든 프로젝트에서 이 값을 `false`로 설정하면 해당 프로젝트의 내용이 NuGet 패키지에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-272">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="d2e75-273">위의 항목 중 하나에서 설정할 수 있는 다른 pack 특정 메타데이터에는 nuspec 출력의 ```contentFiles``` 항목에 ```CopyToOutput``` 및 ```Flatten``` 값을 설정하는 ```<PackageCopyToOutput>``` 및 ```<PackageFlatten>```이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-273">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="d2e75-274">Content 항목 외에도, 빌드 작업이 Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource 또는 None으로 설정된 파일에 `<Pack>` 및 `<PackagePath>` 메타데이터를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-274">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="d2e75-275">GLOB 패턴을 사용할 때 pack에서 파일 이름을 패키지 경로에 추가하려면 패키지 경로가 폴더 구분 문자로 끝나야 합니다. 그렇지 않으면 패키지 경로가 파일 이름을 포함한 전체 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-275">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="d2e75-276">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="d2e75-276">IncludeSymbols</span></span>

<span data-ttu-id="d2e75-277">`MSBuild -t:pack -p:IncludeSymbols=true`를 사용하면 해당 `.pdb` 파일이 다른 출력 파일(`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`)과 함께 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-277">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="d2e75-278">`IncludeSymbols=true`를 설정하면 일반 패키지 *및* 기호 패키지가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-278">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="d2e75-279">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="d2e75-279">IncludeSource</span></span>

<span data-ttu-id="d2e75-280">`.pdb` 파일과 함께 원본 파일을 복사한다는 점을 제외하고는 `IncludeSymbols`와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-280">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="d2e75-281">`Compile` 형식의 모든 파일이 결과 패키지에서 상대 경로 폴더 구조를 유지하면서 `src\<ProjectName>\`에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-281">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="d2e75-282">또한 `TreatAsPackageReference`가 `false`로 설정된 `ProjectReference`의 원본 파일에 대해서도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-282">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="d2e75-283">Compile 형식의 파일이 프로젝트 폴더의 외부에 있는 경우 이 파일은 `src\<ProjectName>\`에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-283">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="d2e75-284">라이선스 식 또는 라이선스 파일을 압축합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-284">Packing a license expression or a license file</span></span>

<span data-ttu-id="d2e75-285">라이선스 식 사용 PackageLicenseExpression 속성을 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-285">When using a license expression, the PackageLicenseExpression property should be used.</span></span> 
<span data-ttu-id="d2e75-286">[라이선스 식 샘플](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-286">[License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="d2e75-287">[라이선스 식 및 NuGet.org에서 허용 되는 라이선스에 대 한 자세한 정보를 알아보려면](nuspec.md#license)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-287">[Learn more about license expressions and licenses that are accepted by NuGet.org](nuspec.md#license).</span></span>

<span data-ttu-id="d2e75-288">라이선스 파일을 압축할 때 PackageLicenseFile 속성을 사용 하 여 패키지의 루트에 상대적인 패키지 경로 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-288">When packing a license file, you need to use PackageLicenseFile property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="d2e75-289">또한 파일 패키지에 포함 되어 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-289">In addition, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="d2e75-290">예를 들어:</span><span class="sxs-lookup"><span data-stu-id="d2e75-290">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
<span data-ttu-id="d2e75-291">[라이선스 파일 샘플](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-291">[License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

### <a name="istool"></a><span data-ttu-id="d2e75-292">IsTool</span><span class="sxs-lookup"><span data-stu-id="d2e75-292">IsTool</span></span>

<span data-ttu-id="d2e75-293">`MSBuild -t:pack -p:IsTool=true`를 사용하면 [출력 어셈블리](#output-assemblies) 시나리오에서 지정한 대로 모든 출력 파일이 `lib` 폴더 대신 `tools` 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-293">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="d2e75-294">이는 `.csproj` 파일에서 `PackageType`을 설정하여 지정된 `DotNetCliTool`과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-294">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="d2e75-295">.nuspec을 사용하여 압축</span><span class="sxs-lookup"><span data-stu-id="d2e75-295">Packing using a .nuspec</span></span>

<span data-ttu-id="d2e75-296">사용할 수는 `.nuspec` SDK 프로젝트 파일을 가져올가 있는 경우 프로젝트를 압축 파일 `NuGet.Build.Tasks.Pack.targets` 팩 작업을 실행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-296">You can use a `.nuspec` file to pack your project provided that you have a SDK project file to import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="d2e75-297">Nuspec 파일을 압축 하기 전에 프로젝트를 복원 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-297">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="d2e75-298">프로젝트 파일의 대상 프레임 워크로 관련이 없는 고 nuspec을 압축할 때 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-298">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="d2e75-299">다음 세 가지 MSBuild 속성은 `.nuspec`을 사용하여 압축하는 것과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-299">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="d2e75-300">`NuspecFile`: 압축에 사용되는 `.nuspec` 파일에 대한 상대 또는 절대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-300">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="d2e75-301">`NuspecProperties`: 세미콜론으로 구분된 key=value 쌍의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-301">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="d2e75-302">MSBuild 명령줄 구문 분석이 작동하는 방식으로 인해 여러 속성을 `-p:NuspecProperties=\"key1=value1;key2=value2\"`와 같이 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-302">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties=\"key1=value1;key2=value2\"`.</span></span>  
1. <span data-ttu-id="d2e75-303">`NuspecBasePath`: 에 대 한 기본 경로 `.nuspec` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-303">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="d2e75-304">`dotnet.exe`를 사용하여 프로젝트를 압축하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-304">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="d2e75-305">MSBuild를 사용하여 프로젝트를 압축하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-305">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="d2e75-306">해당 nuspec dotnet.exe를 사용 하 여 압축을 유의 하십시오 또는 기본적으로 프로젝트를 구축 하는 데 msbuild 많아집니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-306">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="d2e75-307">전달 하 여이 방지할 수 있습니다 ```--no-build``` 속성을 설정의 해당 하는 dotnet.exe ```<NoBuild>true</NoBuild> ``` 설정 함께 프로젝트 파일에서 ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` 프로젝트 파일에서</span><span class="sxs-lookup"><span data-stu-id="d2e75-307">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file</span></span>

<span data-ttu-id="d2e75-308">Nuspec 파일을 압축할 csproj 파일의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-308">An example of a csproj file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="d2e75-309">고급 사용자 지정된 패키지를 만들려면 확장 지점</span><span class="sxs-lookup"><span data-stu-id="d2e75-309">Advanced extension points to create customized package</span></span>

<span data-ttu-id="d2e75-310">`pack` 대상 내부 대상 프레임 워크 특정 빌드에서 실행 되는 두 개의 확장 지점을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-310">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="d2e75-311">대상 프레임 워크 특정 콘텐츠 및 어셈블리는 패키지를 비롯 하 여 확장 지점을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-311">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="d2e75-312">`TargetsForTfmSpecificBuildOutput` 대상: 내에서 파일에 대 한 사용 합니다 `lib` 를 사용 하 여 지정 된 폴더나 폴더 `BuildOutputTargetFolder`.</span><span class="sxs-lookup"><span data-stu-id="d2e75-312">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="d2e75-313">`TargetsForTfmSpecificContentInPackage` 대상: 외부 파일에 대 한 사용을 `BuildOutputTargetFolder`입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-313">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="d2e75-314">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="d2e75-314">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="d2e75-315">사용자 지정 대상을 작성 하 고 값으로 지정 된 `$(TargetsForTfmSpecificBuildOutput)` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-315">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="d2e75-316">로 이동 해야 하는 모든 파일에 대 한는 `BuildOutputTargetFolder` (lib) 기본적으로 대상의 ItemGroup에 해당 파일을 작성 해야 `BuildOutputInPackage` 다음 두 메타 데이터 값을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-316">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="d2e75-317">`FinalOutputPath`: 파일의 절대 경로 지정 하지 않으면 Id 원본 경로 평가에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-317">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="d2e75-318">`TargetPath`:  (선택 사항) 파일 내에서 하위 폴더로 이동 해야 할 때 설정 `lib\<TargetFramework>` 과 같이 위성 어셈블리는 각 문화권 폴더 아래에 있는 해당 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-318">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="d2e75-319">기본값은 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-319">Defaults to the name of the file.</span></span>

<span data-ttu-id="d2e75-320">예제:</span><span class="sxs-lookup"><span data-stu-id="d2e75-320">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="d2e75-321">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="d2e75-321">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="d2e75-322">사용자 지정 대상을 작성 하 고 값으로 지정 된 `$(TargetsForTfmSpecificContentInPackage)` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-322">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="d2e75-323">패키지에 포함할 모든 파일에 대 한 대상 해야 해당 파일에 쓸 ItemGroup `TfmSpecificPackageFile` 다음과 같은 선택적 메타 데이터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-323">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="d2e75-324">`PackagePath`: 파일은 패키지의 출력 이어야 하는 위치 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-324">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="d2e75-325">둘 이상의 파일에서 동일한 패키지 경로에 추가 되 면 NuGet 경고를 발생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-325">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="d2e75-326">`BuildAction`: 파일에 할당할 빌드 작업을 패키지 경로만 필요 합니다 `contentFiles` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-326">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="d2e75-327">기본값은 "None"입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-327">Defaults to "None".</span></span>

<span data-ttu-id="d2e75-328">예제:</span><span class="sxs-lookup"><span data-stu-id="d2e75-328">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="d2e75-329">restore 대상</span><span class="sxs-lookup"><span data-stu-id="d2e75-329">restore target</span></span>

<span data-ttu-id="d2e75-330">`MSBuild -t:restore`(.NET Core 프로젝트에서 `nuget restore` 및 `dotnet restore` 사용)는 프로젝트 파일에서 참조된 패키지를 다음과 같이 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-330">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="d2e75-331">모든 프로젝트 간 참조를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-331">Read all project to project references</span></span>
1. <span data-ttu-id="d2e75-332">프로젝트 속성을 읽어 중간 폴더 및 대상 프레임워크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-332">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="d2e75-333">msbuild 데이터를 NuGet.Build.Tasks.dll에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-333">Pass msbuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="d2e75-334">restore를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-334">Run restore</span></span>
1. <span data-ttu-id="d2e75-335">패키지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-335">Download packages</span></span>
1. <span data-ttu-id="d2e75-336">자산, targets 및 props 파일을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-336">Write assets file, targets, and props</span></span>

<span data-ttu-id="d2e75-337">합니다 `restore` works 대상 **만** PackageReference 형식을 사용 하 여 프로젝트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-337">The `restore` target works **only** for projects using the PackageReference format.</span></span> <span data-ttu-id="d2e75-338">것 **되지** 사용 하 여 프로젝트에 대해 작동 합니다 `packages.config` 은 형식을 사용 하 여 [nuget 복원](../tools/cli-ref-restore.md) 대신 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-338">It does **not** work for projects using the `packages.config` format; use [nuget restore](../tools/cli-ref-restore.md) instead.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="d2e75-339">restore 속성</span><span class="sxs-lookup"><span data-stu-id="d2e75-339">Restore properties</span></span>

<span data-ttu-id="d2e75-340">추가 restore 설정은 프로젝트 파일의 MSBuild 속성에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-340">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="d2e75-341">또한 값은 `-p:` 스위치를 사용하여 명령줄에서 설정할 수 있습니다(아래 예제 참조).</span><span class="sxs-lookup"><span data-stu-id="d2e75-341">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="d2e75-342">속성</span><span class="sxs-lookup"><span data-stu-id="d2e75-342">Property</span></span> | <span data-ttu-id="d2e75-343">설명</span><span class="sxs-lookup"><span data-stu-id="d2e75-343">Description</span></span> |
|--------|--------|
| <span data-ttu-id="d2e75-344">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="d2e75-344">RestoreSources</span></span> | <span data-ttu-id="d2e75-345">세미콜론으로 구분된 패키지 원본의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-345">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="d2e75-346">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="d2e75-346">RestorePackagesPath</span></span> | <span data-ttu-id="d2e75-347">사용자 패키지 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-347">User packages folder path.</span></span> |
| <span data-ttu-id="d2e75-348">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="d2e75-348">RestoreDisableParallel</span></span> | <span data-ttu-id="d2e75-349">다운로드를 한 번에 하나씩으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-349">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="d2e75-350">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="d2e75-350">RestoreConfigFile</span></span> | <span data-ttu-id="d2e75-351">적용할 `Nuget.Config` 파일에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-351">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="d2e75-352">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="d2e75-352">RestoreNoCache</span></span> | <span data-ttu-id="d2e75-353">True 이면 캐시 된 패키지를 사용 하 여 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-353">If true, avoids using cached packages.</span></span> <span data-ttu-id="d2e75-354">참조 [전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-354">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="d2e75-355">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="d2e75-355">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="d2e75-356">true이면 실패했거나 누락된 패키지 원본을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-356">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="d2e75-357">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="d2e75-357">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="d2e75-358">`NuGet.Build.Tasks.dll`에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-358">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="d2e75-359">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="d2e75-359">RestoreGraphProjectInput</span></span> | <span data-ttu-id="d2e75-360">세미콜론으로 구분된 복원할 프로젝트의 목록이며, 절대 경로가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-360">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="d2e75-361">RestoreOutputPath</span><span class="sxs-lookup"><span data-stu-id="d2e75-361">RestoreOutputPath</span></span> | <span data-ttu-id="d2e75-362">출력 폴더이며, 기본값은 `obj` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-362">Output folder, defaulting to the `obj` folder.</span></span> |

#### <a name="examples"></a><span data-ttu-id="d2e75-363">예제</span><span class="sxs-lookup"><span data-stu-id="d2e75-363">Examples</span></span>

<span data-ttu-id="d2e75-364">명령줄:</span><span class="sxs-lookup"><span data-stu-id="d2e75-364">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="d2e75-365">프로젝트 파일:</span><span class="sxs-lookup"><span data-stu-id="d2e75-365">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="d2e75-366">restore 출력</span><span class="sxs-lookup"><span data-stu-id="d2e75-366">Restore outputs</span></span>

<span data-ttu-id="d2e75-367">restore는 `obj` 빌드 폴더에 다음 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-367">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="d2e75-368">파일</span><span class="sxs-lookup"><span data-stu-id="d2e75-368">File</span></span> | <span data-ttu-id="d2e75-369">설명</span><span class="sxs-lookup"><span data-stu-id="d2e75-369">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="d2e75-370">패키지에 대 한 모든 참조의 종속성 그래프를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-370">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="d2e75-371">패키지에 포함된 MSBuild props 파일에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="d2e75-371">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="d2e75-372">패키지에 포함된 MSBuild targets 파일에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="d2e75-372">References to MSBuild targets contained in packages</span></span> |

### <a name="packagetargetfallback"></a><span data-ttu-id="d2e75-373">PackageTargetFallback</span><span class="sxs-lookup"><span data-stu-id="d2e75-373">PackageTargetFallback</span></span>

<span data-ttu-id="d2e75-374">`PackageTargetFallback` 요소를 사용하면 패키지를 복원할 때 사용할 호환 가능한 대상 집합을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-374">The `PackageTargetFallback` element allows you to specify a set of compatible targets to be used when restoring packages.</span></span> <span data-ttu-id="d2e75-375">dotnet [TxM](../reference/target-frameworks.md)을 사용하는 패키지가 dotnet TxM을 선언하지 않은 호환 패키지와 함께 작동하도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-375">It's designed to allow packages that use a dotnet [TxM](../reference/target-frameworks.md) to work with compatible packages that don't declare a dotnet TxM.</span></span> <span data-ttu-id="d2e75-376">즉 프로젝트에서 dotnet TxM을 사용하는 경우, 비dotnet 플랫폼이 dotnet과 호환될 수 있도록 이상 프로젝트에 `<PackageTargetFallback>`을 추가하지 않는 한, 종속되는 모든 패키지에도 dotnet TxM이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-376">That is, if your project uses the dotnet TxM, then all the packages it depends on must also have a dotnet TxM, unless you add the `<PackageTargetFallback>` to your project in order to allow non-dotnet platforms to be compatible with dotnet.</span></span>

<span data-ttu-id="d2e75-377">예를 들어 프로젝트에서 `netstandard1.6` TxM을 사용하고 종속 패키지에 `lib/net45/a.dll` 및 `lib/portable-net45+win81/a.dll`만 포함되어 있으면 프로젝트 빌드에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-377">For example, if the project is using the `netstandard1.6` TxM, and a dependent package contains only `lib/net45/a.dll` and `lib/portable-net45+win81/a.dll`, then the project will fail to build.</span></span> <span data-ttu-id="d2e75-378">가져오려는 항목이 후자의 DLL이면 다음과 같이 `PackageTargetFallback`을 추가하여 `portable-net45+win81` DLL이 호환 가능하다고 나타낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-378">If what you want to bring in is the latter DLL, then you can add a `PackageTargetFallback` as follows to say that the `portable-net45+win81` DLL is compatible:</span></span>

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

<span data-ttu-id="d2e75-379">프로젝트의 모든 대상에 대해 대체(fallback)를 선언하려면 `Condition` 특성을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-379">To declare a fallback for all targets in your project, leave off the `Condition` attribute.</span></span> <span data-ttu-id="d2e75-380">또한 다음과 같이 `$(PackageTargetFallback)`을 포함하여 기존 `PackageTargetFallback`을 확장할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-380">You can also extend any existing `PackageTargetFallback` by including `$(PackageTargetFallback)` as shown here:</span></span>

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="d2e75-381">복원 그래프에서 단일 라이브러리 대체</span><span class="sxs-lookup"><span data-stu-id="d2e75-381">Replacing one library from a restore graph</span></span>

<span data-ttu-id="d2e75-382">restore에서 잘못된 어셈블리를 가져오는 경우 해당 패키지의 기본 선택 항목을 제외하는 한편 원하는 선택 항목으로 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-382">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="d2e75-383">먼저 최상위 `PackageReference`를 사용하여 모든 자산을 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-383">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="d2e75-384">그런 다음 DLL의 적절한 로컬 복사본에 대한 고유한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d2e75-384">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
