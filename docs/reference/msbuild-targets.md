---
title: MSBuild 대상으로서의 NuGet pack 및 restore
description: NuGet pack 및 restore는 NuGet 4.0 이상에서 MSBuild 대상으로 직접 작동할 수 있습니다.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 0c32978baf6146f10c262ba7af94f61fee22272d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777712"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="a0bab-103">MSBuild 대상으로서의 NuGet pack 및 restore</span><span class="sxs-lookup"><span data-stu-id="a0bab-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="a0bab-104">*NuGet 4.0 이상*</span><span class="sxs-lookup"><span data-stu-id="a0bab-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="a0bab-105">[PackageReference](../consume-packages/package-references-in-project-files.md) 형식을 사용 하는 경우 NuGet 4.0 이상에서는 별도의 파일을 사용 하지 않고 프로젝트 파일 내에 모든 매니페스트 메타 데이터를 직접 저장할 수 있습니다 `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="a0bab-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="a0bab-106">MSBuild 15.1 이상에서 NuGet은 아래에서 설명한 대로 `pack` 및 `restore` 대상이 있는 일류 MSBuild 시민이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="a0bab-107">이러한 대상을 사용하면 다른 MSBuild 작업 또는 대상과 마찬가지로 NuGet을 사용하여 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="a0bab-108">MSBuild를 사용 하 여 NuGet 패키지를 만드는 방법에 대 한 지침은 [msbuild를 사용 하 여 nuget 패키지 만들기](../create-packages/creating-a-package-msbuild.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="a0bab-109">(NuGet 3.x 및 이전 버전의 경우 NuGet CLI를 통해 [pack](../reference/cli-reference/cli-ref-pack.md) 및 [restore](../reference/cli-reference/cli-ref-restore.md) 명령을 대신 사용합니다.)</span><span class="sxs-lookup"><span data-stu-id="a0bab-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="a0bab-110">대상 빌드 순서</span><span class="sxs-lookup"><span data-stu-id="a0bab-110">Target build order</span></span>

<span data-ttu-id="a0bab-111">`pack` 및 `restore`는 MSBuild 대상이므로 이 대상에 액세스하여 워크플로를 향상시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="a0bab-112">예를 들어 패키지를 압축한 후 네트워크 공유에 복사한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-112">For example, let’s say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="a0bab-113">이렇게 하려면 프로젝트 파일에 다음을 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="a0bab-114">마찬가지로, MSBuild 작업을 작성하고, 고유한 대상을 작성하고, MSBuild 작업에서 NuGet 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="a0bab-115">`$(OutputPath)` 는 상대적 이며 프로젝트 루트에서 명령을 실행 하는 것으로 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="a0bab-116">pack 대상</span><span class="sxs-lookup"><span data-stu-id="a0bab-116">pack target</span></span>

<span data-ttu-id="a0bab-117">형식을 사용 하는 .NET 프로젝트의 경우 `PackageReference` 를 사용 하 여 `msbuild -t:pack` NuGet 패키지를 만드는 데 사용할 프로젝트 파일의 입력을 그립니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="a0bab-118">다음 표에서는 첫 번째 노드 내에서 프로젝트 파일에 추가할 수 있는 MSBuild 속성을 설명 합니다 `<PropertyGroup>` .</span><span class="sxs-lookup"><span data-stu-id="a0bab-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="a0bab-119">Visual Studio 2017 이상에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **{project_name} 편집** 을 선택하여 이러한 편집 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="a0bab-120">편의상 테이블은 [ `.nuspec` 파일](../reference/nuspec.md)의 해당 속성을 기준으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

<span data-ttu-id="a0bab-121">`.nuspec`의 `Owners` 및 `Summary` 속성은 MSBuild에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-121">Note that the `Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="a0bab-122">특성/NuSpec 값</span><span class="sxs-lookup"><span data-stu-id="a0bab-122">Attribute/NuSpec Value</span></span> | <span data-ttu-id="a0bab-123">MSBuild 속성</span><span class="sxs-lookup"><span data-stu-id="a0bab-123">MSBuild Property</span></span> | <span data-ttu-id="a0bab-124">기본값</span><span class="sxs-lookup"><span data-stu-id="a0bab-124">Default</span></span> | <span data-ttu-id="a0bab-125">메모</span><span class="sxs-lookup"><span data-stu-id="a0bab-125">Notes</span></span> |
|--------|--------|--------|--------|
| <span data-ttu-id="a0bab-126">Id</span><span class="sxs-lookup"><span data-stu-id="a0bab-126">Id</span></span> | <span data-ttu-id="a0bab-127">PackageId</span><span class="sxs-lookup"><span data-stu-id="a0bab-127">PackageId</span></span> | <span data-ttu-id="a0bab-128">AssemblyName</span><span class="sxs-lookup"><span data-stu-id="a0bab-128">AssemblyName</span></span> | <span data-ttu-id="a0bab-129">MSBuild의 $(AssemblyName)입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-129">$(AssemblyName) from MSBuild</span></span> |
| <span data-ttu-id="a0bab-130">버전</span><span class="sxs-lookup"><span data-stu-id="a0bab-130">Version</span></span> | <span data-ttu-id="a0bab-131">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="a0bab-131">PackageVersion</span></span> | <span data-ttu-id="a0bab-132">버전</span><span class="sxs-lookup"><span data-stu-id="a0bab-132">Version</span></span> | <span data-ttu-id="a0bab-133">"1.0.0", "1.0.0-beta" 또는 "1.0.0-beta-00345"와 같이 semver와 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-133">This is semver compatible, for example “1.0.0”, “1.0.0-beta”, or “1.0.0-beta-00345”</span></span> |
| <span data-ttu-id="a0bab-134">VersionPrefix</span><span class="sxs-lookup"><span data-stu-id="a0bab-134">VersionPrefix</span></span> | <span data-ttu-id="a0bab-135">PackageVersionPrefix</span><span class="sxs-lookup"><span data-stu-id="a0bab-135">PackageVersionPrefix</span></span> | <span data-ttu-id="a0bab-136">비어 있음</span><span class="sxs-lookup"><span data-stu-id="a0bab-136">empty</span></span> | <span data-ttu-id="a0bab-137">PackageVersion을 설정하면 PackageVersionPrefix를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-137">Setting PackageVersion overwrites PackageVersionPrefix</span></span> |
| <span data-ttu-id="a0bab-138">VersionSuffix</span><span class="sxs-lookup"><span data-stu-id="a0bab-138">VersionSuffix</span></span> | <span data-ttu-id="a0bab-139">PackageVersionSuffix</span><span class="sxs-lookup"><span data-stu-id="a0bab-139">PackageVersionSuffix</span></span> | <span data-ttu-id="a0bab-140">비어 있음</span><span class="sxs-lookup"><span data-stu-id="a0bab-140">empty</span></span> | <span data-ttu-id="a0bab-141">MSBuild의 $(VersionSuffix)입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-141">$(VersionSuffix) from MSBuild.</span></span> <span data-ttu-id="a0bab-142">PackageVersion을 설정하면 PackageVersionSuffix를 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-142">Setting PackageVersion overwrites PackageVersionSuffix</span></span> |
| <span data-ttu-id="a0bab-143">Authors</span><span class="sxs-lookup"><span data-stu-id="a0bab-143">Authors</span></span> | <span data-ttu-id="a0bab-144">Authors</span><span class="sxs-lookup"><span data-stu-id="a0bab-144">Authors</span></span> | <span data-ttu-id="a0bab-145">현재 사용자의 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="a0bab-145">Username of the current user</span></span> | <span data-ttu-id="a0bab-146">nuget.org에서 프로필 이름과 일치하는, 세미콜론으로 구분된 패키지 작성자 목록입니다. 이러한 목록은 nuget.org의 NuGet 갤러리에 표시되고 동일한 작성자가 패키지를 상호 참조하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-146">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| <span data-ttu-id="a0bab-147">소유자</span><span class="sxs-lookup"><span data-stu-id="a0bab-147">Owners</span></span> | <span data-ttu-id="a0bab-148">해당 없음</span><span class="sxs-lookup"><span data-stu-id="a0bab-148">N/A</span></span> | <span data-ttu-id="a0bab-149">NuSpec에는 없음</span><span class="sxs-lookup"><span data-stu-id="a0bab-149">Not present in NuSpec</span></span> | |
| <span data-ttu-id="a0bab-150">title</span><span class="sxs-lookup"><span data-stu-id="a0bab-150">Title</span></span> | <span data-ttu-id="a0bab-151">title</span><span class="sxs-lookup"><span data-stu-id="a0bab-151">Title</span></span> | <span data-ttu-id="a0bab-152">PackageId</span><span class="sxs-lookup"><span data-stu-id="a0bab-152">The PackageId</span></span>| <span data-ttu-id="a0bab-153">사람들에게 친숙한 패키지 제목이며 보통 nuget.org 및 Visual Studio의 패키지 관리자에서 UI 표시에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-153">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| <span data-ttu-id="a0bab-154">Description</span><span class="sxs-lookup"><span data-stu-id="a0bab-154">Description</span></span> | <span data-ttu-id="a0bab-155">Description</span><span class="sxs-lookup"><span data-stu-id="a0bab-155">Description</span></span> | <span data-ttu-id="a0bab-156">"패키지 설명"</span><span class="sxs-lookup"><span data-stu-id="a0bab-156">"Package Description"</span></span> | <span data-ttu-id="a0bab-157">어셈블리에 대한 자세한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-157">A long description for the assembly.</span></span> <span data-ttu-id="a0bab-158">`PackageDescription`을 지정하지 않으면 이 속성이 패키지 설명으로도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-158">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| <span data-ttu-id="a0bab-159">Copyright</span><span class="sxs-lookup"><span data-stu-id="a0bab-159">Copyright</span></span> | <span data-ttu-id="a0bab-160">Copyright</span><span class="sxs-lookup"><span data-stu-id="a0bab-160">Copyright</span></span> | <span data-ttu-id="a0bab-161">비어 있음</span><span class="sxs-lookup"><span data-stu-id="a0bab-161">empty</span></span> | <span data-ttu-id="a0bab-162">패키지에 대한 저작권 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-162">Copyright details for the package.</span></span> |
| <span data-ttu-id="a0bab-163">RequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="a0bab-163">RequireLicenseAcceptance</span></span> | <span data-ttu-id="a0bab-164">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="a0bab-164">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="a0bab-165">false</span><span class="sxs-lookup"><span data-stu-id="a0bab-165">false</span></span> | <span data-ttu-id="a0bab-166">클라이언트에서, 소비자가 패키지를 설치하기 전에 패키지 라이선스에 동의하도록 물어야 할지 여부를 지정하는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-166">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| <span data-ttu-id="a0bab-167">license</span><span class="sxs-lookup"><span data-stu-id="a0bab-167">license</span></span> | <span data-ttu-id="a0bab-168">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="a0bab-168">PackageLicenseExpression</span></span> | <span data-ttu-id="a0bab-169">비어 있음</span><span class="sxs-lookup"><span data-stu-id="a0bab-169">empty</span></span> | <span data-ttu-id="a0bab-170">`<license type="expression">`에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-170">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="a0bab-171">[라이선스 식 또는 라이선스 파일 압축을](#packing-a-license-expression-or-a-license-file)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-171">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| <span data-ttu-id="a0bab-172">license</span><span class="sxs-lookup"><span data-stu-id="a0bab-172">license</span></span> | <span data-ttu-id="a0bab-173">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="a0bab-173">PackageLicenseFile</span></span> | <span data-ttu-id="a0bab-174">비어 있음</span><span class="sxs-lookup"><span data-stu-id="a0bab-174">empty</span></span> | <span data-ttu-id="a0bab-175">사용자 지정 라이선스 또는 SPDX 식별자가 할당 되지 않은 라이선스를 사용 하는 경우 패키지 내의 라이선스 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-175">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="a0bab-176">참조 된 라이선스 파일을 명시적으로 압축 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-176">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="a0bab-177">`<license type="file">`에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-177">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="a0bab-178">[라이선스 식 또는 라이선스 파일 압축을](#packing-a-license-expression-or-a-license-file)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-178">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| <span data-ttu-id="a0bab-179">LicenseUrl</span><span class="sxs-lookup"><span data-stu-id="a0bab-179">LicenseUrl</span></span> | <span data-ttu-id="a0bab-180">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="a0bab-180">PackageLicenseUrl</span></span> | <span data-ttu-id="a0bab-181">비어 있음</span><span class="sxs-lookup"><span data-stu-id="a0bab-181">empty</span></span> | <span data-ttu-id="a0bab-182">`PackageLicenseUrl`는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-182">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="a0bab-183">대신 `PackageLicenseExpression` 또는 `PackageLicenseFile`를 사용하십시오.</span><span class="sxs-lookup"><span data-stu-id="a0bab-183">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| <span data-ttu-id="a0bab-184">ProjectUrl</span><span class="sxs-lookup"><span data-stu-id="a0bab-184">ProjectUrl</span></span> | <span data-ttu-id="a0bab-185">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="a0bab-185">PackageProjectUrl</span></span> | <span data-ttu-id="a0bab-186">비어 있음</span><span class="sxs-lookup"><span data-stu-id="a0bab-186">empty</span></span> | |
| <span data-ttu-id="a0bab-187">아이콘</span><span class="sxs-lookup"><span data-stu-id="a0bab-187">Icon</span></span> | <span data-ttu-id="a0bab-188">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="a0bab-188">PackageIcon</span></span> | <span data-ttu-id="a0bab-189">비어 있음</span><span class="sxs-lookup"><span data-stu-id="a0bab-189">empty</span></span> | <span data-ttu-id="a0bab-190">패키지 아이콘으로 사용할 패키지의 이미지에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-190">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="a0bab-191">참조 된 아이콘 이미지 파일을 명시적으로 압축 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-191">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="a0bab-192">자세한 내용은 [아이콘 이미지 파일](#packing-an-icon-image-file) 및 [ `icon` 메타 데이터](/nuget/reference/nuspec#icon)압축을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-192">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](/nuget/reference/nuspec#icon).</span></span> |
| <span data-ttu-id="a0bab-193">IconUrl</span><span class="sxs-lookup"><span data-stu-id="a0bab-193">IconUrl</span></span> | <span data-ttu-id="a0bab-194">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="a0bab-194">PackageIconUrl</span></span> | <span data-ttu-id="a0bab-195">비어 있음</span><span class="sxs-lookup"><span data-stu-id="a0bab-195">empty</span></span> | <span data-ttu-id="a0bab-196">`PackageIconUrl` 는를 위해 더 이상 사용 되지 않습니다 `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="a0bab-196">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="a0bab-197">그러나 최상의 하위 환경에서는 이외에를 지정 해야 `PackageIconUrl` `PackageIcon` 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-197">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| <span data-ttu-id="a0bab-198">태그들</span><span class="sxs-lookup"><span data-stu-id="a0bab-198">Tags</span></span> | <span data-ttu-id="a0bab-199">PackageTags</span><span class="sxs-lookup"><span data-stu-id="a0bab-199">PackageTags</span></span> | <span data-ttu-id="a0bab-200">비어 있음</span><span class="sxs-lookup"><span data-stu-id="a0bab-200">empty</span></span> | <span data-ttu-id="a0bab-201">패키지를 지정하는 세미콜론으로 구분된 태그 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-201">A semicolon-delimited list of tags that designates the package.</span></span> |
| <span data-ttu-id="a0bab-202">ReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="a0bab-202">ReleaseNotes</span></span> | <span data-ttu-id="a0bab-203">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="a0bab-203">PackageReleaseNotes</span></span> | <span data-ttu-id="a0bab-204">비어 있음</span><span class="sxs-lookup"><span data-stu-id="a0bab-204">empty</span></span> | <span data-ttu-id="a0bab-205">패키지에 대한 릴리스 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-205">Release notes for the package.</span></span> |
| <span data-ttu-id="a0bab-206">리포지토리/u r l</span><span class="sxs-lookup"><span data-stu-id="a0bab-206">Repository/Url</span></span> | <span data-ttu-id="a0bab-207">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="a0bab-207">RepositoryUrl</span></span> | <span data-ttu-id="a0bab-208">비어 있음</span><span class="sxs-lookup"><span data-stu-id="a0bab-208">empty</span></span> | <span data-ttu-id="a0bab-209">소스 코드를 복제 하거나 검색 하는 데 사용 되는 리포지토리 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-209">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="a0bab-210">예: *https://github.com/NuGet/NuGet.Client.git* .</span><span class="sxs-lookup"><span data-stu-id="a0bab-210">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| <span data-ttu-id="a0bab-211">리포지토리/유형</span><span class="sxs-lookup"><span data-stu-id="a0bab-211">Repository/Type</span></span> | <span data-ttu-id="a0bab-212">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="a0bab-212">RepositoryType</span></span> | <span data-ttu-id="a0bab-213">비어 있음</span><span class="sxs-lookup"><span data-stu-id="a0bab-213">empty</span></span> | <span data-ttu-id="a0bab-214">리포지토리 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-214">Repository type.</span></span> <span data-ttu-id="a0bab-215">예: `git` (기본값), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="a0bab-215">Examples: `git` (default), `tfs`.</span></span> |
| <span data-ttu-id="a0bab-216">리포지토리/분기</span><span class="sxs-lookup"><span data-stu-id="a0bab-216">Repository/Branch</span></span> | <span data-ttu-id="a0bab-217">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="a0bab-217">RepositoryBranch</span></span> | <span data-ttu-id="a0bab-218">비어 있음</span><span class="sxs-lookup"><span data-stu-id="a0bab-218">empty</span></span> | <span data-ttu-id="a0bab-219">선택적 리포지토리 분기 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-219">Optional repository branch information.</span></span> <span data-ttu-id="a0bab-220">`RepositoryUrl`도 이 속성을 포함하도록 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-220">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="a0bab-221">예: *master* (NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="a0bab-221">Example: *master* (NuGet 4.7.0+).</span></span> |
| <span data-ttu-id="a0bab-222">리포지토리/커밋</span><span class="sxs-lookup"><span data-stu-id="a0bab-222">Repository/Commit</span></span> | <span data-ttu-id="a0bab-223">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="a0bab-223">RepositoryCommit</span></span> | <span data-ttu-id="a0bab-224">비어 있음</span><span class="sxs-lookup"><span data-stu-id="a0bab-224">empty</span></span> | <span data-ttu-id="a0bab-225">패키지가 빌드된 소스를 나타내는 선택적 리포지토리 커밋 또는 변경 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-225">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="a0bab-226">`RepositoryUrl`도 이 속성을 포함하도록 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-226">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="a0bab-227">예: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="a0bab-227">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| <span data-ttu-id="a0bab-228">PackageType</span><span class="sxs-lookup"><span data-stu-id="a0bab-228">PackageType</span></span> | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| <span data-ttu-id="a0bab-229">요약</span><span class="sxs-lookup"><span data-stu-id="a0bab-229">Summary</span></span> | <span data-ttu-id="a0bab-230">지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="a0bab-230">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="a0bab-231">pack 대상 입력</span><span class="sxs-lookup"><span data-stu-id="a0bab-231">pack target inputs</span></span>

| <span data-ttu-id="a0bab-232">속성</span><span class="sxs-lookup"><span data-stu-id="a0bab-232">Property</span></span> | <span data-ttu-id="a0bab-233">Description</span><span class="sxs-lookup"><span data-stu-id="a0bab-233">Description</span></span> |
| - | - |
| <span data-ttu-id="a0bab-234">IsPackable</span><span class="sxs-lookup"><span data-stu-id="a0bab-234">IsPackable</span></span> | <span data-ttu-id="a0bab-235">프로젝트를 압축할 수 있는지 여부를 지정하는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-235">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="a0bab-236">기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-236">The default value is `true`.</span></span> |
| <span data-ttu-id="a0bab-237">SuppressDependenciesWhenPacking</span><span class="sxs-lookup"><span data-stu-id="a0bab-237">SuppressDependenciesWhenPacking</span></span> | <span data-ttu-id="a0bab-238">생성 된 `true` NuGet 패키지에서 패키지 종속성을 표시 하지 않으려면로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-238">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| <span data-ttu-id="a0bab-239">PackageVersion</span><span class="sxs-lookup"><span data-stu-id="a0bab-239">PackageVersion</span></span> | <span data-ttu-id="a0bab-240">결과 패키지의 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-240">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="a0bab-241">모든 형식의 NuGet 버전 문자열을 수락합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-241">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="a0bab-242">기본값은 `$(Version)`의 값입니다. 즉 프로젝트에서 `Version` 속성의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-242">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| <span data-ttu-id="a0bab-243">PackageId</span><span class="sxs-lookup"><span data-stu-id="a0bab-243">PackageId</span></span> | <span data-ttu-id="a0bab-244">결과 패키지의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-244">Specifies the name for the resulting package.</span></span> <span data-ttu-id="a0bab-245">지정하지 않으면 `pack` 작업에서 기본값으로 `AssemblyName`을 사용하거나 패키지 이름으로 디렉터리 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-245">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| <span data-ttu-id="a0bab-246">PackageDescription</span><span class="sxs-lookup"><span data-stu-id="a0bab-246">PackageDescription</span></span> | <span data-ttu-id="a0bab-247">UI 표시를 위한 패키지에 대한 자세한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-247">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="a0bab-248">만든 이</span><span class="sxs-lookup"><span data-stu-id="a0bab-248">Authors</span></span> | <span data-ttu-id="a0bab-249">nuget.org에서 프로필 이름과 일치하는, 세미콜론으로 구분된 패키지 작성자 목록입니다. 이러한 목록은 nuget.org의 NuGet 갤러리에 표시되고 동일한 작성자가 패키지를 상호 참조하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-249">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| <span data-ttu-id="a0bab-250">설명</span><span class="sxs-lookup"><span data-stu-id="a0bab-250">Description</span></span> | <span data-ttu-id="a0bab-251">어셈블리에 대한 자세한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-251">A long description for the assembly.</span></span> <span data-ttu-id="a0bab-252">`PackageDescription`을 지정하지 않으면 이 속성이 패키지 설명으로도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-252">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| <span data-ttu-id="a0bab-253">Copyright</span><span class="sxs-lookup"><span data-stu-id="a0bab-253">Copyright</span></span> | <span data-ttu-id="a0bab-254">패키지에 대한 저작권 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-254">Copyright details for the package.</span></span> |
| <span data-ttu-id="a0bab-255">PackageRequireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="a0bab-255">PackageRequireLicenseAcceptance</span></span> | <span data-ttu-id="a0bab-256">클라이언트에서, 소비자가 패키지를 설치하기 전에 패키지 라이선스에 동의하도록 물어야 할지 여부를 지정하는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-256">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="a0bab-257">기본값은 `false`입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-257">The default is `false`.</span></span> |
| <span data-ttu-id="a0bab-258">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="a0bab-258">DevelopmentDependency</span></span> | <span data-ttu-id="a0bab-259">패키지가 다른 패키지의 종속성으로 포함되지 않도록 패키지를 개발 전용 종속성으로 표시할지 여부를 지정하는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-259">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="a0bab-260">`PackageReference`(NuGet 4.8 +)를 사용 하는 경우이 플래그는 컴파일 타임 자산이 컴파일에서 제외 됨을 의미 하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-260">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="a0bab-261">자세한 내용은 [PackageReference에 대한 DevelopmentDependency 지원](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-261">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| <span data-ttu-id="a0bab-262">PackageLicenseExpression</span><span class="sxs-lookup"><span data-stu-id="a0bab-262">PackageLicenseExpression</span></span> | <span data-ttu-id="a0bab-263">[Spdx 라이선스 식별자](https://spdx.org/licenses/) 또는 식입니다 (예:) `Apache-2.0` .</span><span class="sxs-lookup"><span data-stu-id="a0bab-263">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="a0bab-264">자세한 내용은 [라이선스 식 또는 라이선스 파일 압축](#packing-a-license-expression-or-a-license-file)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-264">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| <span data-ttu-id="a0bab-265">PackageLicenseFile</span><span class="sxs-lookup"><span data-stu-id="a0bab-265">PackageLicenseFile</span></span> | <span data-ttu-id="a0bab-266">사용자 지정 라이선스 또는 SPDX 식별자가 할당 되지 않은 라이선스를 사용 하는 경우 패키지 내의 라이선스 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-266">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| <span data-ttu-id="a0bab-267">PackageLicenseUrl</span><span class="sxs-lookup"><span data-stu-id="a0bab-267">PackageLicenseUrl</span></span> | <span data-ttu-id="a0bab-268">`PackageLicenseUrl`는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-268">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="a0bab-269">대신 `PackageLicenseExpression` 또는 `PackageLicenseFile`를 사용하십시오.</span><span class="sxs-lookup"><span data-stu-id="a0bab-269">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| <span data-ttu-id="a0bab-270">PackageProjectUrl</span><span class="sxs-lookup"><span data-stu-id="a0bab-270">PackageProjectUrl</span></span> | |
| <span data-ttu-id="a0bab-271">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="a0bab-271">PackageIcon</span></span> | <span data-ttu-id="a0bab-272">패키지의 루트에 상대적인 패키지 아이콘 경로를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-272">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="a0bab-273">자세한 내용은 [아이콘 이미지 파일 압축](#packing-an-icon-image-file)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-273">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| <span data-ttu-id="a0bab-274">PackageReleaseNotes</span><span class="sxs-lookup"><span data-stu-id="a0bab-274">PackageReleaseNotes</span></span>| <span data-ttu-id="a0bab-275">패키지에 대한 릴리스 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-275">Release notes for the package.</span></span> |
| <span data-ttu-id="a0bab-276">PackageTags</span><span class="sxs-lookup"><span data-stu-id="a0bab-276">PackageTags</span></span> | <span data-ttu-id="a0bab-277">패키지를 지정하는 세미콜론으로 구분된 태그 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-277">A semicolon-delimited list of tags that designates the package.</span></span> |
| <span data-ttu-id="a0bab-278">PackageOutputPath</span><span class="sxs-lookup"><span data-stu-id="a0bab-278">PackageOutputPath</span></span> | <span data-ttu-id="a0bab-279">압축된 패키지가 삭제되는 출력 경로를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-279">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="a0bab-280">기본값은 `$(OutputPath)`입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-280">Default is `$(OutputPath)`.</span></span> |
| <span data-ttu-id="a0bab-281">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="a0bab-281">IncludeSymbols</span></span> | <span data-ttu-id="a0bab-282">이 부울 값은 프로젝트가 압축될 때 패키지에서 추가 기호 패키지를 만들어야 하는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-282">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="a0bab-283">기호 패키지의 형식은 `SymbolPackageFormat` 속성으로 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-283">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="a0bab-284">자세한 내용은 [includesymbols](#includesymbols)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-284">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| <span data-ttu-id="a0bab-285">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="a0bab-285">IncludeSource</span></span> | <span data-ttu-id="a0bab-286">이 부울 값은 팩 프로세스에서 소스 패키지를 만들어야 하는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-286">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="a0bab-287">소스 패키지에는 PDB 파일뿐만 아니라 라이브러리의 소스 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-287">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="a0bab-288">소스 파일은 결과 패키지 파일의 `src/ProjectName` 디렉터리 아래에 놓입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-288">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="a0bab-289">자세한 내용은 [Includesource](#includesource)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-289">For more information, see [IncludeSource](#includesource).</span></span> |
| <span data-ttu-id="a0bab-290">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="a0bab-290">PackageTypes</span></span>
| <span data-ttu-id="a0bab-291">IsTool</span><span class="sxs-lookup"><span data-stu-id="a0bab-291">IsTool</span></span> | <span data-ttu-id="a0bab-292">모든 출력 파일이 *lib* 폴더 대신 *tools* 폴더에 복사되는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-292">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="a0bab-293">자세한 내용은 [IsTool](#istool)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-293">For more information, see [IsTool](#istool).</span></span> |
| <span data-ttu-id="a0bab-294">RepositoryUrl</span><span class="sxs-lookup"><span data-stu-id="a0bab-294">RepositoryUrl</span></span> | <span data-ttu-id="a0bab-295">소스 코드를 복제 하거나 검색 하는 데 사용 되는 리포지토리 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-295">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="a0bab-296">예: *https://github.com/NuGet/NuGet.Client.git* .</span><span class="sxs-lookup"><span data-stu-id="a0bab-296">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| <span data-ttu-id="a0bab-297">RepositoryType</span><span class="sxs-lookup"><span data-stu-id="a0bab-297">RepositoryType</span></span> | <span data-ttu-id="a0bab-298">리포지토리 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-298">Repository type.</span></span> <span data-ttu-id="a0bab-299">예: `git` (기본값), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="a0bab-299">Examples: `git` (default), `tfs`.</span></span> |
| <span data-ttu-id="a0bab-300">RepositoryBranch</span><span class="sxs-lookup"><span data-stu-id="a0bab-300">RepositoryBranch</span></span> | <span data-ttu-id="a0bab-301">선택적 리포지토리 분기 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-301">Optional repository branch information.</span></span> <span data-ttu-id="a0bab-302">`RepositoryUrl`도 이 속성을 포함하도록 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-302">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="a0bab-303">예: *master* (NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="a0bab-303">Example: *master* (NuGet 4.7.0+).</span></span> |
| <span data-ttu-id="a0bab-304">RepositoryCommit</span><span class="sxs-lookup"><span data-stu-id="a0bab-304">RepositoryCommit</span></span> | <span data-ttu-id="a0bab-305">패키지가 빌드된 소스를 나타내는 선택적 리포지토리 커밋 또는 변경 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-305">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="a0bab-306">`RepositoryUrl`도 이 속성을 포함하도록 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-306">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="a0bab-307">예: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="a0bab-307">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| <span data-ttu-id="a0bab-308">SymbolPackageFormat</span><span class="sxs-lookup"><span data-stu-id="a0bab-308">SymbolPackageFormat</span></span> | <span data-ttu-id="a0bab-309">기호 패키지의 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-309">Specifies the format of the symbols package.</span></span> <span data-ttu-id="a0bab-310">"Nupkg" 인 경우 Pdb, Dll 및 기타 출력 파일을 포함 하는 *nupkg* 확장을 사용 하 여 레거시 기호 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-310">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="a0bab-311">"Snupkg" 인 경우 이식 가능한 Pdb를 포함 하는 snupkg 기호 패키지가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-311">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="a0bab-312">기본값은 "nupkg"입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-312">The default is "symbols.nupkg".</span></span> |
| <span data-ttu-id="a0bab-313">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="a0bab-313">NoPackageAnalysis</span></span> | <span data-ttu-id="a0bab-314">`pack`에서 패키지를 빌드한 후 패키지 분석을 실행 하지 않도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-314">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="a0bab-315">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="a0bab-315">MinClientVersion</span></span> | <span data-ttu-id="a0bab-316">nuget.exe 및 Visual Studio 패키지 관리자에 의해 적용되는, 이 패키지를 설치할 수 있는 NuGet 클라이언트의 최소 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-316">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| <span data-ttu-id="a0bab-317">IncludeBuildOutput</span><span class="sxs-lookup"><span data-stu-id="a0bab-317">IncludeBuildOutput</span></span> | <span data-ttu-id="a0bab-318">이 부울 값은 빌드 출력 어셈블리를 *.nupkg* 파일에 압축해야 할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-318">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| <span data-ttu-id="a0bab-319">IncludeContentInPack</span><span class="sxs-lookup"><span data-stu-id="a0bab-319">IncludeContentInPack</span></span> | <span data-ttu-id="a0bab-320">이 부울 값은 형식이 인 항목이 `Content` 자동으로 결과 패키지에 포함 되는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-320">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="a0bab-321">기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-321">The default is `true`.</span></span> |
| <span data-ttu-id="a0bab-322">BuildOutputTargetFolder</span><span class="sxs-lookup"><span data-stu-id="a0bab-322">BuildOutputTargetFolder</span></span> | <span data-ttu-id="a0bab-323">출력 어셈블리를 배치할 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-323">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="a0bab-324">출력 어셈블리(및 기타 출력 파일)는 해당 프레임워크 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-324">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="a0bab-325">자세한 내용은 [출력 어셈블리](#output-assemblies)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-325">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| <span data-ttu-id="a0bab-326">ContentTargetFolders</span><span class="sxs-lookup"><span data-stu-id="a0bab-326">ContentTargetFolders</span></span> | <span data-ttu-id="a0bab-327">가 지정 되지 않은 경우 모든 콘텐츠 파일이 이동 해야 하는 기본 위치를 지정 합니다 `PackagePath` .</span><span class="sxs-lookup"><span data-stu-id="a0bab-327">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="a0bab-328">기본값은 "content;contentFiles"입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-328">The default value is "content;contentFiles".</span></span> <span data-ttu-id="a0bab-329">자세한 내용은 [패키지에 콘텐츠 포함](#including-content-in-a-package)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-329">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| <span data-ttu-id="a0bab-330">NuspecFile</span><span class="sxs-lookup"><span data-stu-id="a0bab-330">NuspecFile</span></span> | <span data-ttu-id="a0bab-331">압축에 사용되는 *.nuspec* 파일에 대한 상대 또는 절대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-331">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="a0bab-332">지정 된 경우 패키징 정보에 **만** 사용 되며 프로젝트의 정보는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-332">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="a0bab-333">자세한 내용은 [nuspec를 사용 하 여 압축](#packing-using-a-nuspec)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-333">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec).</span></span> |
| <span data-ttu-id="a0bab-334">NuspecBasePath</span><span class="sxs-lookup"><span data-stu-id="a0bab-334">NuspecBasePath</span></span> | <span data-ttu-id="a0bab-335">*.nuspec* 파일에 대한 기본 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-335">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="a0bab-336">자세한 내용은 [nuspec를 사용 하 여 압축](#packing-using-a-nuspec)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-336">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec).</span></span> |
| <span data-ttu-id="a0bab-337">NuspecProperties</span><span class="sxs-lookup"><span data-stu-id="a0bab-337">NuspecProperties</span></span> | <span data-ttu-id="a0bab-338">key=value 쌍의 세미콜론으로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-338">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="a0bab-339">자세한 내용은 [nuspec를 사용 하 여 압축](#packing-using-a-nuspec)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-339">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="a0bab-340">pack 시나리오</span><span class="sxs-lookup"><span data-stu-id="a0bab-340">pack scenarios</span></span>

### <a name="suppress-dependencies"></a><span data-ttu-id="a0bab-341">종속성 표시 안 함</span><span class="sxs-lookup"><span data-stu-id="a0bab-341">Suppress dependencies</span></span>

<span data-ttu-id="a0bab-342">생성 된 NuGet 패키지에서 패키지 종속성을 표시 하지 `SuppressDependenciesWhenPacking` 않으려면 `true` 생성 된 nupkg 파일에서 모든 종속성을 건너뛰도록 허용 하는을로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-342">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### <a name="packageiconurl"></a><span data-ttu-id="a0bab-343">PackageIconUrl</span><span class="sxs-lookup"><span data-stu-id="a0bab-343">PackageIconUrl</span></span>

<span data-ttu-id="a0bab-344">`PackageIconUrl` 는 속성을 위해 더 이상 사용 되지 않습니다 [`PackageIcon`](#packageicon) .</span><span class="sxs-lookup"><span data-stu-id="a0bab-344">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="a0bab-345">NuGet 5.3 및 Visual Studio 2019 버전 16.3부터 `pack` 패키지 메타 데이터는만 지정 하는 경우 [NU5048](./errors-and-warnings/nu5048.md) 경고를 발생 시킵니다 `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="a0bab-345">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### <a name="packageicon"></a><span data-ttu-id="a0bab-346">PackageIcon</span><span class="sxs-lookup"><span data-stu-id="a0bab-346">PackageIcon</span></span>

> [!Tip]
> <span data-ttu-id="a0bab-347">아직 지원 되지 않는 클라이언트 및 원본에 대 한 이전 버전과의 호환성을 유지 하려면 `PackageIcon` 및를 모두 지정 `PackageIcon` `PackageIconUrl` 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-347">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="a0bab-348">Visual Studio `PackageIcon` 는 폴더 기반 소스에서 가져온 패키지를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-348">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="a0bab-349">아이콘 이미지 파일 압축</span><span class="sxs-lookup"><span data-stu-id="a0bab-349">Packing an icon image file</span></span>

<span data-ttu-id="a0bab-350">아이콘 이미지 파일을 압축 하는 경우 `PackageIcon` 속성을 사용 하 여 패키지의 루트에 상대적인 아이콘 파일 경로를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-350">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="a0bab-351">또한 파일이 패키지에 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-351">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="a0bab-352">이미지 파일 크기는 1mb로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-352">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="a0bab-353">지원 되는 파일 형식에는 JPEG 및 PNG가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-353">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="a0bab-354">128x128 이미지를 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-354">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="a0bab-355">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-355">For example:</span></span>

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

<span data-ttu-id="a0bab-356">[패키지 아이콘 샘플](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="a0bab-356">[Package Icon sample](https://github.com/NuGet/Samples/tree/master/PackageIconExample).</span></span>

<span data-ttu-id="a0bab-357">Nuspec에 대 한 자세한 내용은 [nuspec reference에 대 한 참조를 참조](nuspec.md#icon)하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-357">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="a0bab-358">출력 어셈블리</span><span class="sxs-lookup"><span data-stu-id="a0bab-358">Output assemblies</span></span>

<span data-ttu-id="a0bab-359">`nuget pack`은 `.exe`, `.dll`, `.xml`, `.winmd`, `.json` 및 `.pri` 확장명의 출력 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-359">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="a0bab-360">복사되는 출력 파일은 `BuiltOutputProjectGroup` 대상에서 제공하는 MSBuild에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-360">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="a0bab-361">프로젝트 파일 또는 명령줄에서 출력 어셈블리의 위치를 제어하는 데 사용할 수 있는 두 가지 MSBuild 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-361">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="a0bab-362">`IncludeBuildOutput`: 빌드 출력 어셈블리를 패키지에 포함할지 여부를 결정하는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-362">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="a0bab-363">`BuildOutputTargetFolder`: 출력 어셈블리를 배치할 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-363">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="a0bab-364">출력 어셈블리(및 기타 출력 파일)는 해당 프레임워크 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-364">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="a0bab-365">패키지 참조</span><span class="sxs-lookup"><span data-stu-id="a0bab-365">Package references</span></span>

<span data-ttu-id="a0bab-366">[프로젝트 파일의 패키지 참조](../consume-packages/package-references-in-project-files.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-366">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="a0bab-367">프로젝트 간 참조</span><span class="sxs-lookup"><span data-stu-id="a0bab-367">Project to project references</span></span>

<span data-ttu-id="a0bab-368">프로젝트 간 참조는 기본적으로 NuGet 패키지 참조로 간주됩니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-368">Project to project references are considered by default as nuget package references, for example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="a0bab-369">또한 다음 메타데이터를 프로젝트 참조에 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-369">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="a0bab-370">패키지에 내용 포함</span><span class="sxs-lookup"><span data-stu-id="a0bab-370">Including content in a package</span></span>

<span data-ttu-id="a0bab-371">콘텐츠를 포함하려면 기존 `<Content>` 항목에 추가 메타데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-371">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="a0bab-372">기본적으로 "Content" 형식의 모든 항목은 다음과 같은 항목으로 재정의하지 않는 한 패키지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-372">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="a0bab-373">패키지 경로를 지정하지 않으면 기본적으로 `content` 및 `contentFiles\any\<target_framework>` 패키지 폴더의 루트에 모든 항목이 추가되고 상대 폴더 구조가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-373">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="a0bab-374">모든 내용을 특정 루트 폴더(`content` 및 `contentFiles` 대신)에만 복사하려면 `ContentTargetFolders` MSBuild 속성을 사용할 수 있습니다. 이 속성은 기본적으로 "content; contentFiles"이지만 다른 폴더 이름으로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-374">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="a0bab-375">`ContentTargetFolders`에 "contentFiles"를 지정하면 파일이 `buildAction`에 따라 `contentFiles\any\<target_framework>` 또는 `contentFiles\<language>\<target_framework>`에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-375">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="a0bab-376">`PackagePath`는 세미콜론으로 구분된 대상 경로의 집합일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-376">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="a0bab-377">빈 패키지 경로를 지정하면 파일이 패키지의 루트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-377">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="a0bab-378">예를 들어 다음은 `libuv.txt`를 `content\myfiles`, `content\samples` 및 패키지 루트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-378">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="a0bab-379">또한 `$(IncludeContentInPack)` MSBuild 속성이 있으며 기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-379">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="a0bab-380">모든 프로젝트에서 이 값을 `false`로 설정하면 해당 프로젝트의 내용이 NuGet 패키지에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-380">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="a0bab-381">위의 항목 중 하나에서 설정할 수 있는 다른 pack 특정 메타데이터에는 nuspec 출력의 ```contentFiles``` 항목에 ```CopyToOutput``` 및 ```Flatten``` 값을 설정하는 ```<PackageCopyToOutput>``` 및 ```<PackageFlatten>```이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-381">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="a0bab-382">Content 항목 외에도, 빌드 작업이 Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource 또는 None으로 설정된 파일에 `<Pack>` 및 `<PackagePath>` 메타데이터를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-382">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="a0bab-383">GLOB 패턴을 사용할 때 pack에서 파일 이름을 패키지 경로에 추가하려면 패키지 경로가 폴더 구분 문자로 끝나야 합니다. 그렇지 않으면 패키지 경로가 파일 이름을 포함한 전체 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-383">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="a0bab-384">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="a0bab-384">IncludeSymbols</span></span>

<span data-ttu-id="a0bab-385">`MSBuild -t:pack -p:IncludeSymbols=true`를 사용하면 해당 `.pdb` 파일이 다른 출력 파일(`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`)과 함께 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-385">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="a0bab-386">`IncludeSymbols=true`를 설정하면 일반 패키지 *및* 기호 패키지가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-386">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="a0bab-387">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="a0bab-387">IncludeSource</span></span>

<span data-ttu-id="a0bab-388">`.pdb` 파일과 함께 원본 파일을 복사한다는 점을 제외하고는 `IncludeSymbols`와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-388">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="a0bab-389">`Compile` 형식의 모든 파일이 결과 패키지에서 상대 경로 폴더 구조를 유지하면서 `src\<ProjectName>\`에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-389">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="a0bab-390">또한 `TreatAsPackageReference`가 `false`로 설정된 `ProjectReference`의 원본 파일에 대해서도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-390">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="a0bab-391">Compile 형식의 파일이 프로젝트 폴더의 외부에 있는 경우 이 파일은 `src\<ProjectName>\`에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-391">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="a0bab-392">라이선스 식 또는 라이선스 파일 압축</span><span class="sxs-lookup"><span data-stu-id="a0bab-392">Packing a license expression or a license file</span></span>

<span data-ttu-id="a0bab-393">라이선스 식을 사용 하는 경우 속성을 사용 `PackageLicenseExpression` 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-393">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="a0bab-394">샘플은 [라이선스 식 샘플](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-394">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="a0bab-395">NuGet.org에서 허용 하는 라이선스 식 및 라이선스에 대 한 자세한 내용은 [라이선스 메타 데이터](nuspec.md#license)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-395">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="a0bab-396">라이선스 파일을 압축 하는 경우 속성을 사용 하 여 패키지 `PackageLicenseFile` 의 루트에 상대적인 패키지 경로를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-396">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="a0bab-397">또한 파일이 패키지에 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-397">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="a0bab-398">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-398">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="a0bab-399">샘플은 [라이선스 파일 샘플](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-399">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="a0bab-400">, 및 중 하나만 한 `PackageLicenseExpression` `PackageLicenseFile` `PackageLicenseUrl` 번에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-400">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="a0bab-401">확장명 없이 파일 압축</span><span class="sxs-lookup"><span data-stu-id="a0bab-401">Packing a file without an extension</span></span>

<span data-ttu-id="a0bab-402">라이선스 파일을 압축 하는 경우와 같은 일부 시나리오에서는 확장명이 없는 파일을 포함 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-402">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="a0bab-403">기록을 위해 NuGet & MSBuild는 확장 없이 경로를 디렉터리로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-403">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="a0bab-404">[확장명 샘플이 없는 파일](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/)입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-404">[File without an extension sample](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).</span></span>
### <a name="istool"></a><span data-ttu-id="a0bab-405">IsTool</span><span class="sxs-lookup"><span data-stu-id="a0bab-405">IsTool</span></span>

<span data-ttu-id="a0bab-406">`MSBuild -t:pack -p:IsTool=true`를 사용하면 [출력 어셈블리](#output-assemblies) 시나리오에서 지정한 대로 모든 출력 파일이 `lib` 폴더 대신 `tools` 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-406">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="a0bab-407">이는 `.csproj` 파일에서 `PackageType`을 설정하여 지정된 `DotNetCliTool`과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-407">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec"></a><span data-ttu-id="a0bab-408">.nuspec을 사용하여 압축</span><span class="sxs-lookup"><span data-stu-id="a0bab-408">Packing using a .nuspec</span></span>

<span data-ttu-id="a0bab-409">일반적으로 파일에 있는 [모든 속성](../reference/msbuild-targets.md#pack-target) 을 프로젝트 파일에 포함 하는 것이 좋지만 `.nuspec` , 파일을 사용 하 여 프로젝트를 압축 하도록 선택할 수 있습니다 `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="a0bab-409">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="a0bab-410">를 사용 하는 비 SDK 스타일 프로젝트의 경우 `PackageReference` `NuGet.Build.Tasks.Pack.targets` pack 작업을 실행할 수 있도록를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-410">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="a0bab-411">여전히 프로젝트를 복원 해야 nuspec 파일을 압축할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-411">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="a0bab-412">SDK 스타일 프로젝트는 기본적으로 pack 대상을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-412">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="a0bab-413">프로젝트 파일의 대상 프레임 워크는 관련이 없으며 nuspec을 압축 하는 경우에는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-413">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="a0bab-414">다음 세 가지 MSBuild 속성은 `.nuspec`을 사용하여 압축하는 것과 관련이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-414">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="a0bab-415">`NuspecFile`: 압축에 사용되는 `.nuspec` 파일에 대한 상대 또는 절대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-415">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="a0bab-416">`NuspecProperties`: 세미콜론으로 구분된 key=value 쌍의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-416">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="a0bab-417">MSBuild 명령줄 구문 분석이 작동하는 방식으로 인해 여러 속성을 `-p:NuspecProperties="key1=value1;key2=value2"`와 같이 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-417">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="a0bab-418">`NuspecBasePath`: `.nuspec` 파일에 대한 기본 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-418">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="a0bab-419">`dotnet.exe`를 사용하여 프로젝트를 압축하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-419">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="a0bab-420">MSBuild를 사용하여 프로젝트를 압축하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-420">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="a0bab-421">dotnet.exe 또는 msbuild를 사용 하 여 nuspec을 압축 하면 기본적으로 프로젝트를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-421">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="a0bab-422">이는 프로젝트 파일의 ```--no-build``` ```<NoBuild>true</NoBuild> ``` 설정과 함께 프로젝트 파일의 설정과 동일한 속성을 dotnet.exe 전달 하 여 방지할 수 있습니다 ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` .</span><span class="sxs-lookup"><span data-stu-id="a0bab-422">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="a0bab-423">Nuspec 파일을 압축 하는 *.csproj* 파일의 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-423">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="a0bab-424">사용자 지정 패키지를 만들기 위한 고급 확장점</span><span class="sxs-lookup"><span data-stu-id="a0bab-424">Advanced extension points to create customized package</span></span>

<span data-ttu-id="a0bab-425">`pack`대상은 내부, 대상 프레임 워크 특정 빌드에서 실행 되는 두 개의 확장 지점이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-425">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="a0bab-426">확장 지점은 대상 프레임 워크 관련 콘텐츠 및 어셈블리를 패키지에 포함 하 여 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-426">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="a0bab-427">`TargetsForTfmSpecificBuildOutput` 대상: `lib` 폴더 또는를 사용 하 여 지정 된 폴더 내의 파일에 사용 `BuildOutputTargetFolder` 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-427">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="a0bab-428">`TargetsForTfmSpecificContentInPackage` 대상: 외부의 파일에 사용 `BuildOutputTargetFolder` 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-428">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### <a name="targetsfortfmspecificbuildoutput"></a><span data-ttu-id="a0bab-429">TargetsForTfmSpecificBuildOutput</span><span class="sxs-lookup"><span data-stu-id="a0bab-429">TargetsForTfmSpecificBuildOutput</span></span>

<span data-ttu-id="a0bab-430">사용자 지정 대상을 작성 하 고이를 속성의 값으로 지정 `$(TargetsForTfmSpecificBuildOutput)` 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-430">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="a0bab-431">로 이동 해야 하는 파일 `BuildOutputTargetFolder` (기본적으로 lib)의 경우 대상은 해당 파일을 ItemGroup에 쓰고 `BuildOutputInPackage` 다음 두 메타 데이터 값을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-431">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="a0bab-432">`FinalOutputPath`: 파일의 절대 경로입니다. 제공 하지 않으면 Id가 원본 경로를 평가 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-432">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="a0bab-433">`TargetPath`: (선택 사항) `lib\<TargetFramework>` 해당 문화권 폴더 아래에 있는 위성 어셈블리와 같이 파일을 내 하위 폴더로 이동 해야 하는 경우에 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-433">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="a0bab-434">기본값은 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-434">Defaults to the name of the file.</span></span>

<span data-ttu-id="a0bab-435">예제:</span><span class="sxs-lookup"><span data-stu-id="a0bab-435">Example:</span></span>

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

#### <a name="targetsfortfmspecificcontentinpackage"></a><span data-ttu-id="a0bab-436">TargetsForTfmSpecificContentInPackage</span><span class="sxs-lookup"><span data-stu-id="a0bab-436">TargetsForTfmSpecificContentInPackage</span></span>

<span data-ttu-id="a0bab-437">사용자 지정 대상을 작성 하 고이를 속성의 값으로 지정 `$(TargetsForTfmSpecificContentInPackage)` 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-437">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="a0bab-438">패키지에 포함할 파일의 경우 대상은 해당 파일을 ItemGroup에 쓰고 `TfmSpecificPackageFile` 다음과 같은 선택적 메타 데이터를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-438">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="a0bab-439">`PackagePath`: 패키지에서 파일이 출력 되어야 하는 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-439">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="a0bab-440">동일한 패키지 경로에 두 개 이상의 파일이 추가 되 면 NuGet에서 경고를 발생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-440">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="a0bab-441">`BuildAction`: 파일에 할당할 빌드 작업으로, 패키지 경로가 폴더에 있는 경우에만 필요 합니다 `contentFiles` .</span><span class="sxs-lookup"><span data-stu-id="a0bab-441">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="a0bab-442">기본값은 "None"입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-442">Defaults to "None".</span></span>

<span data-ttu-id="a0bab-443">예제:</span><span class="sxs-lookup"><span data-stu-id="a0bab-443">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="a0bab-444">restore 대상</span><span class="sxs-lookup"><span data-stu-id="a0bab-444">restore target</span></span>

<span data-ttu-id="a0bab-445">`MSBuild -t:restore`(.NET Core 프로젝트에서 `nuget restore` 및 `dotnet restore` 사용)는 프로젝트 파일에서 참조된 패키지를 다음과 같이 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-445">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="a0bab-446">모든 프로젝트 간 참조를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-446">Read all project to project references</span></span>
1. <span data-ttu-id="a0bab-447">프로젝트 속성을 읽어 중간 폴더 및 대상 프레임워크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-447">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="a0bab-448">NuGet.Build.Tasks.dll에 MSBuild 데이터 전달</span><span class="sxs-lookup"><span data-stu-id="a0bab-448">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="a0bab-449">restore를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-449">Run restore</span></span>
1. <span data-ttu-id="a0bab-450">패키지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-450">Download packages</span></span>
1. <span data-ttu-id="a0bab-451">자산, targets 및 props 파일을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-451">Write assets file, targets, and props</span></span>

<span data-ttu-id="a0bab-452">`restore`대상은 PackageReference 형식을 사용 하는 프로젝트에 대해 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-452">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="a0bab-453">`MSBuild 16.5+` 또한에서는 형식에 대 한 [옵트인 지원도 제공](#restoring-packagereference-and-packagesconfig-with-msbuild) `packages.config` 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-453">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="a0bab-454">대상은 `restore` 대상과 함께 [실행 해서는](#restoring-and-building-with-one-msbuild-command) 안 됩니다 `build` .</span><span class="sxs-lookup"><span data-stu-id="a0bab-454">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="a0bab-455">restore 속성</span><span class="sxs-lookup"><span data-stu-id="a0bab-455">Restore properties</span></span>

<span data-ttu-id="a0bab-456">추가 restore 설정은 프로젝트 파일의 MSBuild 속성에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-456">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="a0bab-457">또한 값은 `-p:` 스위치를 사용하여 명령줄에서 설정할 수 있습니다(아래 예제 참조).</span><span class="sxs-lookup"><span data-stu-id="a0bab-457">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="a0bab-458">속성</span><span class="sxs-lookup"><span data-stu-id="a0bab-458">Property</span></span> | <span data-ttu-id="a0bab-459">Description</span><span class="sxs-lookup"><span data-stu-id="a0bab-459">Description</span></span> |
|--------|--------|
| <span data-ttu-id="a0bab-460">RestoreSources</span><span class="sxs-lookup"><span data-stu-id="a0bab-460">RestoreSources</span></span> | <span data-ttu-id="a0bab-461">세미콜론으로 구분된 패키지 원본의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-461">Semicolon-delimited list of package sources.</span></span> |
| <span data-ttu-id="a0bab-462">RestorePackagesPath</span><span class="sxs-lookup"><span data-stu-id="a0bab-462">RestorePackagesPath</span></span> | <span data-ttu-id="a0bab-463">사용자 패키지 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-463">User packages folder path.</span></span> |
| <span data-ttu-id="a0bab-464">RestoreDisableParallel</span><span class="sxs-lookup"><span data-stu-id="a0bab-464">RestoreDisableParallel</span></span> | <span data-ttu-id="a0bab-465">다운로드를 한 번에 하나씩으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-465">Limit downloads to one at a time.</span></span> |
| <span data-ttu-id="a0bab-466">RestoreConfigFile</span><span class="sxs-lookup"><span data-stu-id="a0bab-466">RestoreConfigFile</span></span> | <span data-ttu-id="a0bab-467">적용할 `Nuget.Config` 파일에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-467">Path to a `Nuget.Config` file to apply.</span></span> |
| <span data-ttu-id="a0bab-468">RestoreNoCache</span><span class="sxs-lookup"><span data-stu-id="a0bab-468">RestoreNoCache</span></span> | <span data-ttu-id="a0bab-469">True 이면 캐시 된 패키지를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-469">If true, avoids using cached packages.</span></span> <span data-ttu-id="a0bab-470">[전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-470">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="a0bab-471">RestoreIgnoreFailedSources</span><span class="sxs-lookup"><span data-stu-id="a0bab-471">RestoreIgnoreFailedSources</span></span> | <span data-ttu-id="a0bab-472">true이면 실패했거나 누락된 패키지 원본을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-472">If true, ignores failing or missing package sources.</span></span> |
| <span data-ttu-id="a0bab-473">RestoreFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="a0bab-473">RestoreFallbackFolders</span></span> | <span data-ttu-id="a0bab-474">사용자 패키지 폴더를 사용 하는 것과 같은 방식으로 사용 되는 대체 (Fallback) 폴더</span><span class="sxs-lookup"><span data-stu-id="a0bab-474">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| <span data-ttu-id="a0bab-475">RestoreAdditionalProjectSources</span><span class="sxs-lookup"><span data-stu-id="a0bab-475">RestoreAdditionalProjectSources</span></span> | <span data-ttu-id="a0bab-476">복원 하는 동안 사용할 추가 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-476">Additional sources to use during restore.</span></span> |
| <span data-ttu-id="a0bab-477">RestoreAdditionalProjectFallbackFolders</span><span class="sxs-lookup"><span data-stu-id="a0bab-477">RestoreAdditionalProjectFallbackFolders</span></span> | <span data-ttu-id="a0bab-478">복원 중에 사용할 추가 대체 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-478">Additional fallback folders to use during restore.</span></span> |
| <span data-ttu-id="a0bab-479">RestoreAdditionalProjectFallbackFoldersExcludes</span><span class="sxs-lookup"><span data-stu-id="a0bab-479">RestoreAdditionalProjectFallbackFoldersExcludes</span></span> | <span data-ttu-id="a0bab-480">에 지정 된 대체 폴더를 제외 합니다. `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="a0bab-480">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| <span data-ttu-id="a0bab-481">RestoreTaskAssemblyFile</span><span class="sxs-lookup"><span data-stu-id="a0bab-481">RestoreTaskAssemblyFile</span></span> | <span data-ttu-id="a0bab-482">`NuGet.Build.Tasks.dll`에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-482">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| <span data-ttu-id="a0bab-483">RestoreGraphProjectInput</span><span class="sxs-lookup"><span data-stu-id="a0bab-483">RestoreGraphProjectInput</span></span> | <span data-ttu-id="a0bab-484">세미콜론으로 구분된 복원할 프로젝트의 목록이며, 절대 경로가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-484">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| <span data-ttu-id="a0bab-485">RestoreUseSkipNonexistentTargets</span><span class="sxs-lookup"><span data-stu-id="a0bab-485">RestoreUseSkipNonexistentTargets</span></span>  | <span data-ttu-id="a0bab-486">MSBuild를 통해 프로젝트를 수집 하는 경우 해당 프로젝트는 최적화를 사용 하 여 수집 되는지 여부를 결정 합니다 `SkipNonexistentTargets` .</span><span class="sxs-lookup"><span data-stu-id="a0bab-486">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="a0bab-487">설정 하지 않으면 기본적으로로 설정 `true` 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-487">When not set, defaults to `true`.</span></span> <span data-ttu-id="a0bab-488">결과는 프로젝트의 대상을 가져올 수 없는 경우의 빠른 오류 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-488">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| <span data-ttu-id="a0bab-489">MSBuildProjectExtensionsPath</span><span class="sxs-lookup"><span data-stu-id="a0bab-489">MSBuildProjectExtensionsPath</span></span> | <span data-ttu-id="a0bab-490">출력 폴더, 및 폴더에 대 한 기본값입니다 `BaseIntermediateOutputPath` `obj` .</span><span class="sxs-lookup"><span data-stu-id="a0bab-490">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| <span data-ttu-id="a0bab-491">RestoreForce</span><span class="sxs-lookup"><span data-stu-id="a0bab-491">RestoreForce</span></span> | <span data-ttu-id="a0bab-492">PackageReference 기반 프로젝트에서 마지막 복원이 성공한 경우에도 모든 종속성이 확인 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-492">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="a0bab-493">이 플래그를 지정 하는 것은 파일을 삭제 하는 것과 비슷합니다 `project.assets.json` .</span><span class="sxs-lookup"><span data-stu-id="a0bab-493">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="a0bab-494">이는 http 캐시를 우회 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-494">This does not bypass the http-cache.</span></span> |
| <span data-ttu-id="a0bab-495">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="a0bab-495">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="a0bab-496">잠금 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-496">Opts into the usage of a lock file.</span></span> |
| <span data-ttu-id="a0bab-497">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="a0bab-497">RestoreLockedMode</span></span> | <span data-ttu-id="a0bab-498">잠금 모드에서 복원을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-498">Run restore in locked mode.</span></span> <span data-ttu-id="a0bab-499">즉, 복원은 종속성을 다시 평가 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-499">This means that restore will not reevaluate the dependencies.</span></span> |
| <span data-ttu-id="a0bab-500">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="a0bab-500">NuGetLockFilePath</span></span> | <span data-ttu-id="a0bab-501">잠금 파일의 사용자 지정 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-501">A custom location for the lock file.</span></span> <span data-ttu-id="a0bab-502">기본 위치는 프로젝트 옆에 있고 이름은 `packages.lock.json` 입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-502">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| <span data-ttu-id="a0bab-503">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="a0bab-503">RestoreForceEvaluate</span></span> | <span data-ttu-id="a0bab-504">강제로 복원 하 여 종속성을 다시 계산 하 고 경고 없이 잠금 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-504">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| <span data-ttu-id="a0bab-505">RestorePackagesConfig</span><span class="sxs-lookup"><span data-stu-id="a0bab-505">RestorePackagesConfig</span></span> | <span data-ttu-id="a0bab-506">packages.config를 사용 하 여 프로젝트를 복원 하는 옵트인 스위치. 만 지원 `MSBuild -t:restore` 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-506">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| <span data-ttu-id="a0bab-507">RestoreUseStaticGraphEvaluation</span><span class="sxs-lookup"><span data-stu-id="a0bab-507">RestoreUseStaticGraphEvaluation</span></span> | <span data-ttu-id="a0bab-508">표준 평가 대신 정적 그래프 MSBuild 평가를 사용 하는 옵트인 스위치입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-508">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="a0bab-509">정적 그래프 평가는 큰 리포지토리 및 솔루션에 대해 훨씬 더 빠른 실험적 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-509">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="a0bab-510">예제</span><span class="sxs-lookup"><span data-stu-id="a0bab-510">Examples</span></span>

<span data-ttu-id="a0bab-511">명령줄:</span><span class="sxs-lookup"><span data-stu-id="a0bab-511">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="a0bab-512">프로젝트 파일:</span><span class="sxs-lookup"><span data-stu-id="a0bab-512">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="a0bab-513">restore 출력</span><span class="sxs-lookup"><span data-stu-id="a0bab-513">Restore outputs</span></span>

<span data-ttu-id="a0bab-514">restore는 `obj` 빌드 폴더에 다음 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-514">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="a0bab-515">파일</span><span class="sxs-lookup"><span data-stu-id="a0bab-515">File</span></span> | <span data-ttu-id="a0bab-516">Description</span><span class="sxs-lookup"><span data-stu-id="a0bab-516">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="a0bab-517">모든 패키지 참조의 종속성 그래프를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-517">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="a0bab-518">패키지에 포함된 MSBuild props 파일에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="a0bab-518">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="a0bab-519">패키지에 포함된 MSBuild targets 파일에 대한 참조</span><span class="sxs-lookup"><span data-stu-id="a0bab-519">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="a0bab-520">하나의 MSBuild 명령을 사용 하 여 복원 및 빌드</span><span class="sxs-lookup"><span data-stu-id="a0bab-520">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="a0bab-521">NuGet은 MSBuild 대상 및 props을 가져오는 패키지를 복원할 수 있으므로 다른 전역 속성을 사용 하 여 복원 및 빌드 평가가 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-521">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="a0bab-522">즉, 다음은 예측할 수 없으며 종종 잘못 된 동작을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-522">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="a0bab-523">대신에 권장 되는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-523">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="a0bab-524">같은 논리는와 유사한 다른 대상에도 적용 됩니다 `build` .</span><span class="sxs-lookup"><span data-stu-id="a0bab-524">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a><span data-ttu-id="a0bab-525">MSBuild를 사용 하 여 PackageReference 및 packages.config 복원</span><span class="sxs-lookup"><span data-stu-id="a0bab-525">Restoring PackageReference and packages.config with MSBuild</span></span>

<span data-ttu-id="a0bab-526">MSBuild 16.5 +를 사용 하는 경우에도 packages.config 지원 됩니다 `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="a0bab-526">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="a0bab-527">`packages.config` restore는와 함께 사용할 수 `MSBuild 16.5+` 없습니다. `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="a0bab-527">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="a0bab-528">MSBuild 정적 그래프 평가를 사용 하 여 복원</span><span class="sxs-lookup"><span data-stu-id="a0bab-528">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="a0bab-529">MSBuild 16.6 +를 사용 하는 경우 NuGet은 큰 리포지토리의 복원 시간을 크게 개선 하는 명령줄에서 정적 그래프 평가를 사용 하는 실험적 기능을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-529">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="a0bab-530">또는 디렉터리에 속성을 설정 하 여 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-530">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="a0bab-531">Visual Studio 2019. x 및 NuGet 5.x를 기반으로이 기능은 실험적이 고 옵트인 (opt in) 된 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-531">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="a0bab-532">이 기능이 기본적으로 사용 되는 경우에 대 한 자세한 내용은 [NuGet/Home # 9803](https://github.com/NuGet/Home/issues/9803) 를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-532">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="a0bab-533">정적 그래프 복원은 복원, 프로젝트 읽기 및 평가의 msbuild 부분을 변경 하지만 복원 알고리즘은 변경 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-533">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="a0bab-534">복원 알고리즘은 모든 NuGet 도구 (NuGet.exe, MSBuild.exe, dotnet.exe 및 Visual Studio)에서 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-534">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="a0bab-535">거의 모든 시나리오에서 정적 그래프 복원은 현재 복원과 다르게 동작할 수 있으며 선언 된 특정 PackageReferences 또는 ProjectReferences가 누락 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-535">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="a0bab-536">정적 그래프 복원으로 마이그레이션할 때를 한 번만 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-536">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="a0bab-537">NuGet은 어떠한 변경 내용도 보고 *하지 않습니다* .</span><span class="sxs-lookup"><span data-stu-id="a0bab-537">NuGet should *not* report any changes.</span></span> <span data-ttu-id="a0bab-538">불일치가 표시 되는 경우 [NuGet/Home](https://github.com/nuget/home/issues/new)에서 문제를 파일에 입력 하세요.</span><span class="sxs-lookup"><span data-stu-id="a0bab-538">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="a0bab-539">복원 그래프에서 단일 라이브러리 대체</span><span class="sxs-lookup"><span data-stu-id="a0bab-539">Replacing one library from a restore graph</span></span>

<span data-ttu-id="a0bab-540">restore에서 잘못된 어셈블리를 가져오는 경우 해당 패키지의 기본 선택 항목을 제외하는 한편 원하는 선택 항목으로 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-540">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="a0bab-541">먼저 최상위 `PackageReference`를 사용하여 모든 자산을 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-541">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="a0bab-542">그런 다음 DLL의 적절한 로컬 복사본에 대한 고유한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a0bab-542">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
