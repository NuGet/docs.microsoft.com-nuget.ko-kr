---
title: NuGet대상으로 팩 및 복원 MSBuild
description: NuGet pack 및 복원은 MSBuild 4.0 +의 대상으로 직접 작동할 수 있습니다 NuGet .
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 8ebf0329f9dc7af09a59f1498a934754842df365
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067312"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a><span data-ttu-id="76a30-103">NuGet대상으로 팩 및 복원 MSBuild</span><span class="sxs-lookup"><span data-stu-id="76a30-103">NuGet pack and restore as MSBuild targets</span></span>

<span data-ttu-id="76a30-104">*NuGet 4.0 이상*</span><span class="sxs-lookup"><span data-stu-id="76a30-104">*NuGet 4.0+*</span></span>

<span data-ttu-id="76a30-105">[PackageReference](../consume-packages/package-references-in-project-files.md) 형식을 사용 하는 경우 NuGet 4.0 이상에서는 별도의 파일을 사용 하지 않고 프로젝트 파일 내에 모든 매니페스트 메타 데이터를 직접 저장할 수 있습니다 `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="76a30-105">With the [PackageReference](../consume-packages/package-references-in-project-files.md) format, NuGet 4.0+ can store all manifest metadata directly within a project file rather than using a separate `.nuspec` file.</span></span>

<span data-ttu-id="76a30-106">15.1 +를 사용 하는 경우 MSBuild 아래에 NuGet 설명 된 MSBuild 및 대상과 함께 최고 수준의 시민 이기도 합니다 `pack` `restore` .</span><span class="sxs-lookup"><span data-stu-id="76a30-106">With MSBuild 15.1+, NuGet is also a first-class MSBuild citizen with the `pack` and `restore` targets as described below.</span></span> <span data-ttu-id="76a30-107">이러한 대상을 사용 하면 NuGet 다른 MSBuild 작업 또는 대상과 마찬가지로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-107">These targets allow you to work with NuGet as you would with any other MSBuild task or target.</span></span> <span data-ttu-id="76a30-108">를 사용 하 여 패키지를 만드는 방법은를 NuGet MSBuild [ NuGet 사용 하 여 MSBuild 패키지 만들기 ](../create-packages/creating-a-package-msbuild.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-108">For instructions creating a NuGet package using MSBuild, see [Create a NuGet package using MSBuild](../create-packages/creating-a-package-msbuild.md).</span></span> <span data-ttu-id="76a30-109">(의 경우 NuGet ) 3. x 및 이전 버전에서는 대신 CLI를 통해 [pack](../reference/cli-reference/cli-ref-pack.md) 및 [restore](../reference/cli-reference/cli-ref-restore.md) 명령을 사용 NuGet 합니다.)</span><span class="sxs-lookup"><span data-stu-id="76a30-109">(For NuGet 3.x and earlier, you use the [pack](../reference/cli-reference/cli-ref-pack.md) and [restore](../reference/cli-reference/cli-ref-restore.md) commands through the NuGet CLI instead.)</span></span>

## <a name="target-build-order"></a><span data-ttu-id="76a30-110">대상 빌드 순서</span><span class="sxs-lookup"><span data-stu-id="76a30-110">Target build order</span></span>

<span data-ttu-id="76a30-111">`pack`및는 대상 이기 때문에 액세스 하 여 `restore` 워크플로를 향상 시킬 수 있습니다 MSBuild .</span><span class="sxs-lookup"><span data-stu-id="76a30-111">Because `pack` and `restore` are  MSBuild targets, you can access them to enhance your workflow.</span></span> <span data-ttu-id="76a30-112">예를 들어 패키지를 압축 한 후에 네트워크 공유에 복사 하려는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-112">For example, let's say you want to copy your package to a network share after packing it.</span></span> <span data-ttu-id="76a30-113">이렇게 하려면 프로젝트 파일에 다음을 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-113">You can do that by adding the following in your project file:</span></span>

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

<span data-ttu-id="76a30-114">마찬가지로 작업 MSBuild 을 작성 하 고, 고유한 대상을 작성 하 고, NuGet 작업에서 속성을 사용할 수 있습니다 MSBuild .</span><span class="sxs-lookup"><span data-stu-id="76a30-114">Similarly, you can write an MSBuild task, write your own target and consume NuGet properties in the MSBuild task.</span></span>

> [!NOTE]
> <span data-ttu-id="76a30-115">`$(OutputPath)` 는 상대적 이며 프로젝트 루트에서 명령을 실행 하는 것으로 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-115">`$(OutputPath)` is relative and expects that you are running the command from the project root.</span></span>

## <a name="pack-target"></a><span data-ttu-id="76a30-116">pack 대상</span><span class="sxs-lookup"><span data-stu-id="76a30-116">pack target</span></span>

<span data-ttu-id="76a30-117">형식을 사용 하는 .NET 프로젝트의 경우 `PackageReference` 를 사용 하 여 `msbuild -t:pack` 패키지를 만드는 데 사용할 프로젝트 파일의 입력을 그립니다 NuGet .</span><span class="sxs-lookup"><span data-stu-id="76a30-117">For .NET projects that use the `PackageReference` format, using `msbuild -t:pack` draws inputs from the project file to use in creating a NuGet package.</span></span>

<span data-ttu-id="76a30-118">다음 표에서는 MSBuild 첫 번째 노드 내에서 프로젝트 파일에 추가할 수 있는 속성을 설명 합니다 `<PropertyGroup>` .</span><span class="sxs-lookup"><span data-stu-id="76a30-118">The following table describes the MSBuild properties that can be added to a project file within the first `<PropertyGroup>` node.</span></span> <span data-ttu-id="76a30-119">Visual Studio 2017 이상에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **{project_name} 편집** 을 선택하여 이러한 편집 작업을 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-119">You can make these edits easily in Visual Studio 2017 and later by right-clicking the project and selecting **Edit {project_name}** on the context menu.</span></span> <span data-ttu-id="76a30-120">편의상 테이블은 [ `.nuspec` 파일](../reference/nuspec.md)의 해당 속성을 기준으로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-120">For convenience, the table is organized by the equivalent property in a [`.nuspec` file](../reference/nuspec.md).</span></span>

> [!NOTE]
> <span data-ttu-id="76a30-121">`Owners` 및 `Summary` 의 속성 `.nuspec` 은에서 지원 되지 않습니다 MSBuild .</span><span class="sxs-lookup"><span data-stu-id="76a30-121">`Owners` and `Summary` properties from `.nuspec` are not supported with MSBuild.</span></span>

| <span data-ttu-id="76a30-122">특성/ nuspec 값</span><span class="sxs-lookup"><span data-stu-id="76a30-122">Attribute/nuspec Value</span></span> | <span data-ttu-id="76a30-123">MSBuild 속성</span><span class="sxs-lookup"><span data-stu-id="76a30-123">MSBuild Property</span></span> | <span data-ttu-id="76a30-124">기본값</span><span class="sxs-lookup"><span data-stu-id="76a30-124">Default</span></span> | <span data-ttu-id="76a30-125">메모</span><span class="sxs-lookup"><span data-stu-id="76a30-125">Notes</span></span> |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | <span data-ttu-id="76a30-126">MSBuild의 `$(AssemblyName)`</span><span class="sxs-lookup"><span data-stu-id="76a30-126">`$(AssemblyName)` from MSBuild</span></span> |
| `Version` | `PackageVersion` | <span data-ttu-id="76a30-127">버전</span><span class="sxs-lookup"><span data-stu-id="76a30-127">Version</span></span> | <span data-ttu-id="76a30-128">이는 semver와 호환 됩니다. 예를 들어, 또는입니다. `1.0.0` `1.0.0-beta``1.0.0-beta-00345`</span><span class="sxs-lookup"><span data-stu-id="76a30-128">This is semver compatible, for example `1.0.0`, `1.0.0-beta`, or `1.0.0-beta-00345`</span></span> |
| `VersionPrefix` | `PackageVersionPrefix` | <span data-ttu-id="76a30-129">비어 있음</span><span class="sxs-lookup"><span data-stu-id="76a30-129">empty</span></span> | <span data-ttu-id="76a30-130">`PackageVersion`덮어쓰기 설정`PackageVersionPrefix`</span><span class="sxs-lookup"><span data-stu-id="76a30-130">Setting `PackageVersion` overwrites `PackageVersionPrefix`</span></span> |
| `VersionSuffix` | `PackageVersionSuffix` | <span data-ttu-id="76a30-131">비어 있음</span><span class="sxs-lookup"><span data-stu-id="76a30-131">empty</span></span> | <span data-ttu-id="76a30-132">`$(VersionSuffix)` 에서 MSBuild .</span><span class="sxs-lookup"><span data-stu-id="76a30-132">`$(VersionSuffix)` from MSBuild.</span></span> <span data-ttu-id="76a30-133">`PackageVersion`덮어쓰기 설정`PackageVersionSuffix`</span><span class="sxs-lookup"><span data-stu-id="76a30-133">Setting `PackageVersion` overwrites `PackageVersionSuffix`</span></span> |
| `Authors` | `Authors` | <span data-ttu-id="76a30-134">현재 사용자의 사용자 이름</span><span class="sxs-lookup"><span data-stu-id="76a30-134">Username of the current user</span></span> | <span data-ttu-id="76a30-135">Nuget.org의 프로필 이름과 일치 하는, 세미콜론으로 구분 된 패키지 작성자 목록입니다. 이러한는 NuGet nuget.org의 갤러리에 표시 되 고 동일한 작성자가 패키지를 상호 참조 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-135">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Owners` | <span data-ttu-id="76a30-136">해당 없음</span><span class="sxs-lookup"><span data-stu-id="76a30-136">N/A</span></span> | <span data-ttu-id="76a30-137">에 없음 nuspec</span><span class="sxs-lookup"><span data-stu-id="76a30-137">Not present in nuspec</span></span> | |
| `Title` | `Title` | <span data-ttu-id="76a30-138">`PackageId`입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-138">The `PackageId`</span></span> | <span data-ttu-id="76a30-139">사람들에게 친숙한 패키지 제목이며 보통 nuget.org 및 Visual Studio의 패키지 관리자에서 UI 표시에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-139">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> |
| `Description` | `Description` | <span data-ttu-id="76a30-140">"패키지 설명"</span><span class="sxs-lookup"><span data-stu-id="76a30-140">"Package Description"</span></span> | <span data-ttu-id="76a30-141">어셈블리에 대한 자세한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-141">A long description for the assembly.</span></span> <span data-ttu-id="76a30-142">`PackageDescription`을 지정하지 않으면 이 속성이 패키지 설명으로도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-142">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | `Copyright` | <span data-ttu-id="76a30-143">비어 있음</span><span class="sxs-lookup"><span data-stu-id="76a30-143">empty</span></span> | <span data-ttu-id="76a30-144">패키지에 대한 저작권 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-144">Copyright details for the package.</span></span> |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | <span data-ttu-id="76a30-145">클라이언트에서, 소비자가 패키지를 설치하기 전에 패키지 라이선스에 동의하도록 물어야 할지 여부를 지정하는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-145">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| `license` | `PackageLicenseExpression` | <span data-ttu-id="76a30-146">비어 있음</span><span class="sxs-lookup"><span data-stu-id="76a30-146">empty</span></span> | <span data-ttu-id="76a30-147">`<license type="expression">`에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-147">Corresponds to `<license type="expression">`.</span></span> <span data-ttu-id="76a30-148">[라이선스 식 또는 라이선스 파일 압축을](#packing-a-license-expression-or-a-license-file)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-148">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `license` | `PackageLicenseFile` | <span data-ttu-id="76a30-149">비어 있음</span><span class="sxs-lookup"><span data-stu-id="76a30-149">empty</span></span> | <span data-ttu-id="76a30-150">사용자 지정 라이선스 또는 SPDX 식별자가 할당 되지 않은 라이선스를 사용 하는 경우 패키지 내의 라이선스 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-150">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> <span data-ttu-id="76a30-151">참조 된 라이선스 파일을 명시적으로 압축 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-151">You need to explicitly pack the referenced license file.</span></span> <span data-ttu-id="76a30-152">`<license type="file">`에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-152">Corresponds to `<license type="file">`.</span></span> <span data-ttu-id="76a30-153">[라이선스 식 또는 라이선스 파일 압축을](#packing-a-license-expression-or-a-license-file)참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-153">See [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `LicenseUrl` | `PackageLicenseUrl` | <span data-ttu-id="76a30-154">비어 있음</span><span class="sxs-lookup"><span data-stu-id="76a30-154">empty</span></span> | <span data-ttu-id="76a30-155">`PackageLicenseUrl`는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-155">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="76a30-156">대신 `PackageLicenseExpression` 또는 `PackageLicenseFile`를 사용하십시오.</span><span class="sxs-lookup"><span data-stu-id="76a30-156">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `ProjectUrl` | `PackageProjectUrl` | <span data-ttu-id="76a30-157">비어 있음</span><span class="sxs-lookup"><span data-stu-id="76a30-157">empty</span></span> | |
| `Icon` | `PackageIcon` | <span data-ttu-id="76a30-158">비어 있음</span><span class="sxs-lookup"><span data-stu-id="76a30-158">empty</span></span> | <span data-ttu-id="76a30-159">패키지 아이콘으로 사용할 패키지의 이미지에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-159">A path to an image in the package to use as a package icon.</span></span> <span data-ttu-id="76a30-160">참조 된 아이콘 이미지 파일을 명시적으로 압축 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-160">You need to explicitly pack the referenced icon image file.</span></span> <span data-ttu-id="76a30-161">자세한 내용은 [아이콘 이미지 파일](#packing-an-icon-image-file) 및 [ `icon` 메타 데이터](./nuspec.md#icon)압축을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-161">For more information, see [Packing an icon image file](#packing-an-icon-image-file) and [`icon` metadata](./nuspec.md#icon).</span></span> |
| `IconUrl` | `PackageIconUrl` | <span data-ttu-id="76a30-162">비어 있음</span><span class="sxs-lookup"><span data-stu-id="76a30-162">empty</span></span> | <span data-ttu-id="76a30-163">`PackageIconUrl` 는를 위해 더 이상 사용 되지 않습니다 `PackageIcon` .</span><span class="sxs-lookup"><span data-stu-id="76a30-163">`PackageIconUrl` is deprecated in favor of `PackageIcon`.</span></span> <span data-ttu-id="76a30-164">그러나 최상의 하위 환경에서는 이외에를 지정 해야 `PackageIconUrl` `PackageIcon` 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-164">However, for the best downlevel experience, you should specify `PackageIconUrl` in addition to `PackageIcon`.</span></span> |
| `Readme` | `PackageReadmeFile` | <span data-ttu-id="76a30-165">비어 있음</span><span class="sxs-lookup"><span data-stu-id="76a30-165">empty</span></span> | <span data-ttu-id="76a30-166">참조 된 추가 정보 파일을 명시적으로 압축 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-166">You need to explicitly pack the referenced readme file.</span></span>|
| `Tags` | `PackageTags` | <span data-ttu-id="76a30-167">비어 있음</span><span class="sxs-lookup"><span data-stu-id="76a30-167">empty</span></span> | <span data-ttu-id="76a30-168">패키지를 지정하는 세미콜론으로 구분된 태그 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-168">A semicolon-delimited list of tags that designates the package.</span></span> |
| `ReleaseNotes` | `PackageReleaseNotes` | <span data-ttu-id="76a30-169">비어 있음</span><span class="sxs-lookup"><span data-stu-id="76a30-169">empty</span></span> | <span data-ttu-id="76a30-170">패키지에 대한 릴리스 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-170">Release notes for the package.</span></span> |
| `Repository/Url` | `RepositoryUrl` | <span data-ttu-id="76a30-171">비어 있음</span><span class="sxs-lookup"><span data-stu-id="76a30-171">empty</span></span> | <span data-ttu-id="76a30-172">소스 코드를 복제 하거나 검색 하는 데 사용 되는 리포지토리 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-172">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="76a30-173">예: *https://github.com/ NuGet / NuGet . 클라이언트. git*.</span><span class="sxs-lookup"><span data-stu-id="76a30-173">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `Repository/Type` | `RepositoryType` | <span data-ttu-id="76a30-174">비어 있음</span><span class="sxs-lookup"><span data-stu-id="76a30-174">empty</span></span> | <span data-ttu-id="76a30-175">리포지토리 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-175">Repository type.</span></span> <span data-ttu-id="76a30-176">예: `git` (기본값), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="76a30-176">Examples: `git` (default), `tfs`.</span></span> |
| `Repository/Branch` | `RepositoryBranch` | <span data-ttu-id="76a30-177">비어 있음</span><span class="sxs-lookup"><span data-stu-id="76a30-177">empty</span></span> | <span data-ttu-id="76a30-178">선택적 리포지토리 분기 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-178">Optional repository branch information.</span></span> <span data-ttu-id="76a30-179">`RepositoryUrl`도 이 속성을 포함하도록 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-179">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="76a30-180">예: *master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="76a30-180">Example: *master* (NuGet 4.7.0+).</span></span> |
| `Repository/Commit` | `RepositoryCommit` | <span data-ttu-id="76a30-181">비어 있음</span><span class="sxs-lookup"><span data-stu-id="76a30-181">empty</span></span> | <span data-ttu-id="76a30-182">패키지가 빌드된 소스를 나타내는 선택적 리포지토리 커밋 또는 변경 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-182">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="76a30-183">`RepositoryUrl`도 이 속성을 포함하도록 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-183">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="76a30-184">예: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="76a30-184">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `PackageType` | `<PackageType>CustomType1, 1.0.0.0;CustomType2</PackageType>` | | <span data-ttu-id="76a30-185">패키지의 용도를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-185">Indicates the package's intended use.</span></span> <span data-ttu-id="76a30-186">패키지 유형은 패키지 Id와 동일한 형식을 사용 하며로 구분 됩니다 `;` .</span><span class="sxs-lookup"><span data-stu-id="76a30-186">Package types use the same format as package IDs and are delimited by `;`.</span></span> <span data-ttu-id="76a30-187">및 문자열을 추가 하 여 패키지 형식의 버전을 지정할 수 있습니다 `,` [`Version`](/dotnet/api/system.version) .</span><span class="sxs-lookup"><span data-stu-id="76a30-187">Package types may be versioned by appending a `,` and a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="76a30-188">[ NuGet 패키지 형식 설정](../create-packages/set-package-type.md) ( NuGet 3.5.0 +)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-188">See [Set a NuGet package type](../create-packages/set-package-type.md) (NuGet 3.5.0+).</span></span> |
| `Summary` | <span data-ttu-id="76a30-189">지원되지 않음</span><span class="sxs-lookup"><span data-stu-id="76a30-189">Not supported</span></span> | | |

### <a name="pack-target-inputs"></a><span data-ttu-id="76a30-190">pack 대상 입력</span><span class="sxs-lookup"><span data-stu-id="76a30-190">pack target inputs</span></span>

| <span data-ttu-id="76a30-191">속성</span><span class="sxs-lookup"><span data-stu-id="76a30-191">Property</span></span> | <span data-ttu-id="76a30-192">Description</span><span class="sxs-lookup"><span data-stu-id="76a30-192">Description</span></span> |
| - | - |
| `IsPackable` | <span data-ttu-id="76a30-193">프로젝트를 압축할 수 있는지 여부를 지정하는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-193">A Boolean value that specifies whether the project can be packed.</span></span> <span data-ttu-id="76a30-194">기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-194">The default value is `true`.</span></span> |
| `SuppressDependenciesWhenPacking` | <span data-ttu-id="76a30-195">생성 된 `true` 패키지에서 패키지 종속성을 표시 하지 않으려면로 설정 NuGet 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-195">Set to `true` to suppress package dependencies from the generated NuGet package.</span></span> |
| `PackageVersion` | <span data-ttu-id="76a30-196">결과 패키지의 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-196">Specifies the version that the resulting package will have.</span></span> <span data-ttu-id="76a30-197">모든 형식의 NuGet 버전 문자열을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-197">Accepts all forms of NuGet version string.</span></span> <span data-ttu-id="76a30-198">기본값은 `$(Version)`의 값입니다. 즉 프로젝트에서 `Version` 속성의 값입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-198">Default is the value of `$(Version)`, that is, of the property `Version` in the project.</span></span> |
| `PackageId` | <span data-ttu-id="76a30-199">결과 패키지의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-199">Specifies the name for the resulting package.</span></span> <span data-ttu-id="76a30-200">지정하지 않으면 `pack` 작업에서 기본값으로 `AssemblyName`을 사용하거나 패키지 이름으로 디렉터리 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-200">If not specified, the `pack` operation will default to using the `AssemblyName` or directory name as the name of the package.</span></span> |
| `PackageDescription` | <span data-ttu-id="76a30-201">UI 표시를 위한 패키지에 대한 자세한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-201">A long description of the package for UI display.</span></span> |
| `Authors` | <span data-ttu-id="76a30-202">Nuget.org의 프로필 이름과 일치 하는, 세미콜론으로 구분 된 패키지 작성자 목록입니다. 이러한는 NuGet nuget.org의 갤러리에 표시 되 고 동일한 작성자가 패키지를 상호 참조 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-202">A semicolon-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |
| `Description` | <span data-ttu-id="76a30-203">어셈블리에 대한 자세한 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-203">A long description for the assembly.</span></span> <span data-ttu-id="76a30-204">`PackageDescription`을 지정하지 않으면 이 속성이 패키지 설명으로도 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-204">If `PackageDescription` is not specified, then this property is also used as the description of the package.</span></span> |
| `Copyright` | <span data-ttu-id="76a30-205">패키지에 대한 저작권 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-205">Copyright details for the package.</span></span> |
| `PackageRequireLicenseAcceptance` | <span data-ttu-id="76a30-206">클라이언트에서, 소비자가 패키지를 설치하기 전에 패키지 라이선스에 동의하도록 물어야 할지 여부를 지정하는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-206">A Boolean value that specifies whether the client must prompt the consumer to accept the package license before installing the package.</span></span> <span data-ttu-id="76a30-207">기본값은 `false`입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-207">The default is `false`.</span></span> |
| `DevelopmentDependency` | <span data-ttu-id="76a30-208">패키지가 다른 패키지의 종속성으로 포함되지 않도록 패키지를 개발 전용 종속성으로 표시할지 여부를 지정하는 부울 값입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-208">A Boolean value that specifies whether the package is marked as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="76a30-209">`PackageReference`( NuGet 4.8 +)를 사용 하는 경우이 플래그는 컴파일 타임 자산이 컴파일에서 제외 됨을 의미 하기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-209">With `PackageReference` (NuGet 4.8+), this flag also means that compile-time assets are excluded from compilation.</span></span> <span data-ttu-id="76a30-210">자세한 내용은 [PackageReference에 대한 DevelopmentDependency 지원](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-210">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span> |
| `PackageLicenseExpression` | <span data-ttu-id="76a30-211">[Spdx 라이선스 식별자](https://spdx.org/licenses/) 또는 식입니다 (예:) `Apache-2.0` .</span><span class="sxs-lookup"><span data-stu-id="76a30-211">An [SPDX license identifier](https://spdx.org/licenses/) or expression, for example, `Apache-2.0`.</span></span> <span data-ttu-id="76a30-212">자세한 내용은 [라이선스 식 또는 라이선스 파일 압축](#packing-a-license-expression-or-a-license-file)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-212">For more information, see [Packing a license expression or a license file](#packing-a-license-expression-or-a-license-file).</span></span> |
| `PackageLicenseFile` | <span data-ttu-id="76a30-213">사용자 지정 라이선스 또는 SPDX 식별자가 할당 되지 않은 라이선스를 사용 하는 경우 패키지 내의 라이선스 파일 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-213">Path to a license file within the package if you're using a custom license or a license that hasn't been assigned an SPDX identifier.</span></span> |
| `PackageLicenseUrl` | <span data-ttu-id="76a30-214">`PackageLicenseUrl`는 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-214">`PackageLicenseUrl` is deprecated.</span></span> <span data-ttu-id="76a30-215">대신 `PackageLicenseExpression` 또는 `PackageLicenseFile`를 사용하십시오.</span><span class="sxs-lookup"><span data-stu-id="76a30-215">Use `PackageLicenseExpression` or `PackageLicenseFile` instead.</span></span> |
| `PackageProjectUrl` | |
| `PackageIcon` | <span data-ttu-id="76a30-216">패키지의 루트에 상대적인 패키지 아이콘 경로를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-216">Specifies the package icon path, relative to the root of the package.</span></span> <span data-ttu-id="76a30-217">자세한 내용은 [아이콘 이미지 파일 압축](#packing-an-icon-image-file)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-217">For more information, see [Packing an icon image file](#packing-an-icon-image-file).</span></span> |
| `PackageReleaseNotes` | <span data-ttu-id="76a30-218">패키지에 대한 릴리스 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-218">Release notes for the package.</span></span> |
| `PackageReadmeFile` | <span data-ttu-id="76a30-219">패키지에 대 한 추가 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-219">Readme for the package.</span></span> |
| `PackageTags` | <span data-ttu-id="76a30-220">패키지를 지정하는 세미콜론으로 구분된 태그 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-220">A semicolon-delimited list of tags that designates the package.</span></span> |
| `PackageOutputPath` | <span data-ttu-id="76a30-221">압축된 패키지가 삭제되는 출력 경로를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-221">Determines the output path in which the packed package will be dropped.</span></span> <span data-ttu-id="76a30-222">기본값은 `$(OutputPath)`입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-222">Default is `$(OutputPath)`.</span></span> |
| `IncludeSymbols` | <span data-ttu-id="76a30-223">이 부울 값은 프로젝트가 압축될 때 패키지에서 추가 기호 패키지를 만들어야 하는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-223">This Boolean value indicates whether the package should create an additional symbols package when the project is packed.</span></span> <span data-ttu-id="76a30-224">기호 패키지의 형식은 `SymbolPackageFormat` 속성으로 제어됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-224">The symbols package's format is controlled by the `SymbolPackageFormat` property.</span></span> <span data-ttu-id="76a30-225">자세한 내용은 [includesymbols](#includesymbols)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-225">For more information, see [IncludeSymbols](#includesymbols).</span></span> |
| `IncludeSource` | <span data-ttu-id="76a30-226">이 부울 값은 팩 프로세스에서 소스 패키지를 만들어야 하는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-226">This Boolean value indicates whether the pack process should create a source package.</span></span> <span data-ttu-id="76a30-227">소스 패키지에는 PDB 파일뿐만 아니라 라이브러리의 소스 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-227">The source package contains the library's source code as well as PDB files.</span></span> <span data-ttu-id="76a30-228">소스 파일은 결과 패키지 파일의 `src/ProjectName` 디렉터리 아래에 놓입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-228">Source files are put under the `src/ProjectName` directory in the resulting package file.</span></span> <span data-ttu-id="76a30-229">자세한 내용은 [Includesource](#includesource)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-229">For more information, see [IncludeSource](#includesource).</span></span> |
| `PackageType` | |
| `IsTool` | <span data-ttu-id="76a30-230">모든 출력 파일이 *lib* 폴더 대신 *tools* 폴더에 복사되는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-230">Specifies whether all output files are copied to the *tools* folder instead of the *lib* folder.</span></span> <span data-ttu-id="76a30-231">자세한 내용은 [IsTool](#istool)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-231">For more information, see [IsTool](#istool).</span></span> |
| `RepositoryUrl` | <span data-ttu-id="76a30-232">소스 코드를 복제 하거나 검색 하는 데 사용 되는 리포지토리 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-232">Repository URL used to clone or retrieve source code.</span></span> <span data-ttu-id="76a30-233">예: *https://github.com/ NuGet / NuGet . 클라이언트. git*.</span><span class="sxs-lookup"><span data-stu-id="76a30-233">Example: *https://github.com/NuGet/NuGet.Client.git*.</span></span> |
| `RepositoryType` | <span data-ttu-id="76a30-234">리포지토리 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-234">Repository type.</span></span> <span data-ttu-id="76a30-235">예: `git` (기본값), `tfs` .</span><span class="sxs-lookup"><span data-stu-id="76a30-235">Examples: `git` (default), `tfs`.</span></span> |
| `RepositoryBranch` | <span data-ttu-id="76a30-236">선택적 리포지토리 분기 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-236">Optional repository branch information.</span></span> <span data-ttu-id="76a30-237">`RepositoryUrl`도 이 속성을 포함하도록 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-237">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="76a30-238">예: *master* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="76a30-238">Example: *master* (NuGet 4.7.0+).</span></span> |
| `RepositoryCommit` | <span data-ttu-id="76a30-239">패키지가 빌드된 소스를 나타내는 선택적 리포지토리 커밋 또는 변경 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-239">Optional repository commit or changeset to indicate which source the package was built against.</span></span> <span data-ttu-id="76a30-240">`RepositoryUrl`도 이 속성을 포함하도록 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-240">`RepositoryUrl` must also be specified for this property to be included.</span></span> <span data-ttu-id="76a30-241">예: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +).</span><span class="sxs-lookup"><span data-stu-id="76a30-241">Example: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+).</span></span> |
| `SymbolPackageFormat` | <span data-ttu-id="76a30-242">기호 패키지의 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-242">Specifies the format of the symbols package.</span></span> <span data-ttu-id="76a30-243">"Nupkg" 인 경우 Pdb, Dll 및 기타 출력 파일을 포함 하는 *nupkg* 확장을 사용 하 여 레거시 기호 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-243">If "symbols.nupkg", a legacy symbols package is created with a *.symbols.nupkg* extension containing PDBs, DLLs, and other output files.</span></span> <span data-ttu-id="76a30-244">"Snupkg" 인 경우 이식 가능한 Pdb를 포함 하는 snupkg 기호 패키지가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-244">If "snupkg", a snupkg symbol package is created containing the portable PDBs.</span></span> <span data-ttu-id="76a30-245">기본값은 "nupkg"입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-245">The default is "symbols.nupkg".</span></span> |
| `NoPackageAnalysis` | <span data-ttu-id="76a30-246">`pack`에서 패키지를 빌드한 후 패키지 분석을 실행 하지 않도록 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-246">Specifies that `pack` should not run package analysis after building the package.</span></span> |
| `MinClientVersion` | <span data-ttu-id="76a30-247">NuGet이 패키지를 설치할 수 있는 클라이언트의 최소 버전을 지정 하 고 nuget.exe 및 Visual Studio 패키지 관리자에 의해 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-247">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> |
| `IncludeBuildOutput` | <span data-ttu-id="76a30-248">이 부울 값은 빌드 출력 어셈블리를 *.nupkg* 파일에 압축해야 할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-248">This Boolean value specifies whether the build output assemblies should be packed into the *.nupkg* file or not.</span></span> |
| `IncludeContentInPack` | <span data-ttu-id="76a30-249">이 부울 값은 형식이 인 항목이 `Content` 자동으로 결과 패키지에 포함 되는지 여부를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-249">This Boolean value specifies whether any items that have a type of `Content` are included in the resulting package automatically.</span></span> <span data-ttu-id="76a30-250">기본값은 `true`입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-250">The default is `true`.</span></span> |
| `BuildOutputTargetFolder` | <span data-ttu-id="76a30-251">출력 어셈블리를 배치할 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-251">Specifies the folder where to place the output assemblies.</span></span> <span data-ttu-id="76a30-252">출력 어셈블리(및 기타 출력 파일)는 해당 프레임워크 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-252">The output assemblies (and other output files) are copied into their respective framework folders.</span></span> <span data-ttu-id="76a30-253">자세한 내용은 [출력 어셈블리](#output-assemblies)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-253">For more information, see [Output assemblies](#output-assemblies).</span></span> |
| `ContentTargetFolders` | <span data-ttu-id="76a30-254">가 지정 되지 않은 경우 모든 콘텐츠 파일이 이동 해야 하는 기본 위치를 지정 합니다 `PackagePath` .</span><span class="sxs-lookup"><span data-stu-id="76a30-254">Specifies the default location of where all the content files should go if `PackagePath` is not specified for them.</span></span> <span data-ttu-id="76a30-255">기본값은 "content;contentFiles"입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-255">The default value is "content;contentFiles".</span></span> <span data-ttu-id="76a30-256">자세한 내용은 [패키지에 콘텐츠 포함](#including-content-in-a-package)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-256">For more information, see [Including content in a package](#including-content-in-a-package).</span></span> |
| `NuspecFile` | <span data-ttu-id="76a30-257">압축에 사용 되는 파일에 대 한 상대 또는 절대 경로 *.nuspec* 입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-257">Relative or absolute path to the *.nuspec* file being used for packing.</span></span> <span data-ttu-id="76a30-258">지정 된 경우 패키징 정보에 **만** 사용 되며 프로젝트의 정보는 사용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-258">If specified, it's used **exclusively** for packaging information, and any information in the projects is not used.</span></span> <span data-ttu-id="76a30-259">자세한 내용은 [를 .nuspec 사용 하 여 압축 ](#packing-using-a-nuspec-file)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-259">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecBasePath` | <span data-ttu-id="76a30-260">파일의 기본 경로 *.nuspec* 입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-260">Base path for the *.nuspec* file.</span></span> <span data-ttu-id="76a30-261">자세한 내용은 [를 .nuspec 사용 하 여 압축 ](#packing-using-a-nuspec-file)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-261">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |
| `NuspecProperties` | <span data-ttu-id="76a30-262">key=value 쌍의 세미콜론으로 구분된 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-262">Semicolon separated list of key=value pairs.</span></span> <span data-ttu-id="76a30-263">자세한 내용은 [를 .nuspec 사용 하 여 압축 ](#packing-using-a-nuspec-file)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-263">For more information, see [Packing using a .nuspec](#packing-using-a-nuspec-file).</span></span> |

## <a name="pack-scenarios"></a><span data-ttu-id="76a30-264">pack 시나리오</span><span class="sxs-lookup"><span data-stu-id="76a30-264">pack scenarios</span></span>

### <a name="suppressing-dependencies"></a><span data-ttu-id="76a30-265">종속성 표시 안 함</span><span class="sxs-lookup"><span data-stu-id="76a30-265">Suppressing dependencies</span></span>

<span data-ttu-id="76a30-266">생성 된 패키지에서 패키지 종속성을 표시 하지 않으려면 NuGet `SuppressDependenciesWhenPacking` 생성 된 `true` nupkg 파일에서 모든 종속성을 건너뛰도록 허용 하는을로 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-266">To suppress package dependencies from generated NuGet package, set `SuppressDependenciesWhenPacking` to `true` which will allow skipping all the dependencies from generated nupkg file.</span></span>

### `PackageIconUrl`

<span data-ttu-id="76a30-267">`PackageIconUrl` 는 속성을 위해 더 이상 사용 되지 않습니다 [`PackageIcon`](#packageicon) .</span><span class="sxs-lookup"><span data-stu-id="76a30-267">`PackageIconUrl` is deprecated in favor of the [`PackageIcon`](#packageicon) property.</span></span> <span data-ttu-id="76a30-268">NuGet5.3 및 Visual Studio 2019 버전 16.3부터 `pack` 패키지 메타 데이터는만 지정 하는 경우 [NU5048](./errors-and-warnings/nu5048.md) 경고를 발생 시킵니다 `PackageIconUrl` .</span><span class="sxs-lookup"><span data-stu-id="76a30-268">Starting with NuGet 5.3 and Visual Studio 2019 version 16.3, `pack` raises the [NU5048](./errors-and-warnings/nu5048.md) warning if the package metadata only specifies `PackageIconUrl`.</span></span>

### `PackageIcon`

> [!Tip]
> <span data-ttu-id="76a30-269">아직 지원 되지 않는 클라이언트 및 원본에 대 한 이전 버전과의 호환성을 유지 하려면 `PackageIcon` 및를 모두 지정 `PackageIcon` `PackageIconUrl` 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-269">To maintain backward compatibility with clients and sources that don't yet support `PackageIcon`, specify both `PackageIcon` and `PackageIconUrl`.</span></span> <span data-ttu-id="76a30-270">Visual Studio `PackageIcon` 는 폴더 기반 소스에서 가져온 패키지를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-270">Visual Studio supports `PackageIcon` for packages coming from a folder-based source.</span></span>

#### <a name="packing-an-icon-image-file"></a><span data-ttu-id="76a30-271">아이콘 이미지 파일 압축</span><span class="sxs-lookup"><span data-stu-id="76a30-271">Packing an icon image file</span></span>

<span data-ttu-id="76a30-272">아이콘 이미지 파일을 압축 하는 경우 `PackageIcon` 속성을 사용 하 여 패키지의 루트에 상대적인 아이콘 파일 경로를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-272">When packing an icon image file, use `PackageIcon` property to specify the icon file path, relative to the root of the package.</span></span> <span data-ttu-id="76a30-273">또한 파일이 패키지에 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-273">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="76a30-274">이미지 파일 크기는 1mb로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-274">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="76a30-275">지원 되는 파일 형식에는 JPEG 및 PNG가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-275">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="76a30-276">128x128 이미지를 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-276">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="76a30-277">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-277">For example:</span></span>

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

<span data-ttu-id="76a30-278">[패키지 아이콘 샘플](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span><span class="sxs-lookup"><span data-stu-id="76a30-278">[Package Icon sample](https://github.com/NuGet/Samples/tree/main/PackageIconExample).</span></span>

<span data-ttu-id="76a30-279">이에 대 한 nuspec [ nuspec 참조는 아이콘에 대 한 참조](nuspec.md#icon)를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-279">For the nuspec equivalent, take a look at [nuspec reference for icon](nuspec.md#icon).</span></span>

### <a name="packagereadmefile"></a><span data-ttu-id="76a30-280">PackageReadmeFile</span><span class="sxs-lookup"><span data-stu-id="76a30-280">PackageReadmeFile</span></span>

<span data-ttu-id="76a30-281">***NuGet 5.10.0 preview 2**  /  **.net SDK 5.0.300** 이상에서 지원 됨*</span><span class="sxs-lookup"><span data-stu-id="76a30-281">*Supported with **NuGet 5.10.0 preview 2** / **.NET SDK 5.0.300** and above*</span></span>

<span data-ttu-id="76a30-282">추가 정보 파일을 압축 하는 경우 속성을 사용 하 여 패키지 `PackageReadmeFile` 의 루트에 상대적인 패키지 경로를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-282">When packing a readme file, you need to use the `PackageReadmeFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="76a30-283">이 외에도 파일이 패키지에 포함 되어 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-283">In addition to this, you need to make sure that the file is included in the package.</span></span> <span data-ttu-id="76a30-284">지원 되는 파일 형식에는 Markdown (*md*)만 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-284">Supported file formats include only Markdown (*.md*).</span></span>

<span data-ttu-id="76a30-285">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-285">For example:</span></span>

```xml
<PropertyGroup>
    ...
    <PackageReadmeFile>readme.md</PackageReadmeFile>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="docs\readme.md" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

<span data-ttu-id="76a30-286">nuspec이와 동등한 경우 [ nuspec 추가 정보에 대 한 참조](nuspec.md#readme)를 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-286">For the nuspec equivalent, take a look at [nuspec reference for readme](nuspec.md#readme).</span></span>

### <a name="output-assemblies"></a><span data-ttu-id="76a30-287">출력 어셈블리</span><span class="sxs-lookup"><span data-stu-id="76a30-287">Output assemblies</span></span>

<span data-ttu-id="76a30-288">`nuget pack`은 `.exe`, `.dll`, `.xml`, `.winmd`, `.json` 및 `.pri` 확장명의 출력 파일을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-288">`nuget pack` copies output files with extensions `.exe`, `.dll`, `.xml`, `.winmd`, `.json`, and `.pri`.</span></span> <span data-ttu-id="76a30-289">복사 된 출력 파일은 대상의에서 제공 하는 내용에 따라 달라 집니다 MSBuild `BuiltOutputProjectGroup` .</span><span class="sxs-lookup"><span data-stu-id="76a30-289">The output files that are copied depend on what MSBuild provides from the `BuiltOutputProjectGroup` target.</span></span>

<span data-ttu-id="76a30-290">MSBuild출력 어셈블리의 이동 위치를 제어 하기 위해 프로젝트 파일이 나 명령줄에서 사용할 수 있는 두 가지 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-290">There are two MSBuild  properties that you can use in your project file or command line to control where output assemblies go:</span></span>

- <span data-ttu-id="76a30-291">`IncludeBuildOutput`: 빌드 출력 어셈블리를 패키지에 포함할지 여부를 결정하는 부울입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-291">`IncludeBuildOutput`: A boolean that determines whether the build output assemblies should be included in the package.</span></span>
- <span data-ttu-id="76a30-292">`BuildOutputTargetFolder`: 출력 어셈블리를 배치할 폴더를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-292">`BuildOutputTargetFolder`: Specifies the folder in which the output assemblies should be placed.</span></span> <span data-ttu-id="76a30-293">출력 어셈블리(및 기타 출력 파일)는 해당 프레임워크 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-293">The output assemblies (and other output files) are copied into their respective framework folders.</span></span>

### <a name="package-references"></a><span data-ttu-id="76a30-294">패키지 참조</span><span class="sxs-lookup"><span data-stu-id="76a30-294">Package references</span></span>

<span data-ttu-id="76a30-295">[프로젝트 파일의 패키지 참조](../consume-packages/package-references-in-project-files.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-295">See [Package References in Project Files](../consume-packages/package-references-in-project-files.md).</span></span>

### <a name="project-to-project-references"></a><span data-ttu-id="76a30-296">프로젝트 간 참조</span><span class="sxs-lookup"><span data-stu-id="76a30-296">Project to project references</span></span>

<span data-ttu-id="76a30-297">프로젝트 간 참조는 기본적으로 패키지 참조로 간주 됩니다 NuGet .</span><span class="sxs-lookup"><span data-stu-id="76a30-297">Project to project references are considered by default as NuGet package references.</span></span> <span data-ttu-id="76a30-298">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-298">For example:</span></span>

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

<span data-ttu-id="76a30-299">또한 다음 메타데이터를 프로젝트 참조에 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-299">You can also add the following metadata to your project reference:</span></span>

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a><span data-ttu-id="76a30-300">패키지에 내용 포함</span><span class="sxs-lookup"><span data-stu-id="76a30-300">Including content in a package</span></span>

<span data-ttu-id="76a30-301">콘텐츠를 포함하려면 기존 `<Content>` 항목에 추가 메타데이터를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-301">To include content, add extra metadata to the existing `<Content>` item.</span></span> <span data-ttu-id="76a30-302">기본적으로 "Content" 형식의 모든 항목은 다음과 같은 항목으로 재정의하지 않는 한 패키지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-302">By default everything of type "Content" gets included in the package unless you override with entries like the following:</span></span>

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

<span data-ttu-id="76a30-303">패키지 경로를 지정하지 않으면 기본적으로 `content` 및 `contentFiles\any\<target_framework>` 패키지 폴더의 루트에 모든 항목이 추가되고 상대 폴더 구조가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-303">By default, everything gets added to the root of the `content` and `contentFiles\any\<target_framework>` folder within a package and preserves the relative folder structure, unless you specify a package path:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

<span data-ttu-id="76a30-304">모든 콘텐츠를 특정 루트 폴더 (대신 `content` 및 둘 다)로 복사 하려는 경우 `contentFiles` MSBuild `ContentTargetFolders` "content; contentfiles"로 기본 설정 되지만 다른 폴더 이름으로 설정 될 수 있는 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-304">If you want to copy all your content to only a specific root folder(s) (instead of `content` and `contentFiles` both), you can use the MSBuild property `ContentTargetFolders`, which defaults to "content;contentFiles" but can be set to any other folder names.</span></span> <span data-ttu-id="76a30-305">`ContentTargetFolders`에 "contentFiles"를 지정하면 파일이 `buildAction`에 따라 `contentFiles\any\<target_framework>` 또는 `contentFiles\<language>\<target_framework>`에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-305">Note that just specifying "contentFiles" in `ContentTargetFolders` puts files under `contentFiles\any\<target_framework>` or `contentFiles\<language>\<target_framework>` based on `buildAction`.</span></span>

<span data-ttu-id="76a30-306">`PackagePath`는 세미콜론으로 구분된 대상 경로의 집합일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-306">`PackagePath` can be a semicolon-delimited set of target paths.</span></span> <span data-ttu-id="76a30-307">빈 패키지 경로를 지정하면 파일이 패키지의 루트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-307">Specifying an empty package path would add the file to the root of the package.</span></span> <span data-ttu-id="76a30-308">예를 들어 다음은 `libuv.txt`를 `content\myfiles`, `content\samples` 및 패키지 루트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-308">For example, the following adds `libuv.txt` to `content\myfiles`, `content\samples`, and the package root:</span></span>

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

<span data-ttu-id="76a30-309">또한 MSBuild 속성은 `$(IncludeContentInPack)` 로 기본 설정 됩니다 `true` .</span><span class="sxs-lookup"><span data-stu-id="76a30-309">There is also an MSBuild property `$(IncludeContentInPack)`, which defaults to `true`.</span></span> <span data-ttu-id="76a30-310">모든 프로젝트에서 이 값을 `false`로 설정하면 해당 프로젝트의 내용이 NuGet 패키지에 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-310">If this is set to `false` on any project, then the content from that project are not included in the nuget package.</span></span>

<span data-ttu-id="76a30-311">위의 항목에 대해 설정할 수 있는 기타 pack 관련 메타 데이터에는 ```<PackageCopyToOutput>``` ```<PackageFlatten>``` ```CopyToOutput``` ```Flatten``` 출력의 항목에 대 한 및 값을 설정 ```contentFiles``` nuspec 하는 및가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-311">Other pack specific metadata that you can set on any of the above items includes ```<PackageCopyToOutput>``` and ```<PackageFlatten>``` which sets ```CopyToOutput``` and ```Flatten``` values on the ```contentFiles``` entry in the output nuspec.</span></span>

> [!Note]
> <span data-ttu-id="76a30-312">Content 항목 외에도, 빌드 작업이 Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource 또는 None으로 설정된 파일에 `<Pack>` 및 `<PackagePath>` 메타데이터를 설정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-312">Apart from Content items, the `<Pack>` and `<PackagePath>` metadata can also be set on files with a build action of Compile, EmbeddedResource, ApplicationDefinition, Page, Resource, SplashScreen, DesignData, DesignDataWithDesignTimeCreateableTypes, CodeAnalysisDictionary, AndroidAsset, AndroidResource, BundleResource or None.</span></span>
>
> <span data-ttu-id="76a30-313">GLOB 패턴을 사용할 때 pack에서 파일 이름을 패키지 경로에 추가하려면 패키지 경로가 폴더 구분 문자로 끝나야 합니다. 그렇지 않으면 패키지 경로가 파일 이름을 포함한 전체 경로로 처리됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-313">For pack to append the filename to your package path when using globbing patterns, your package path must end with the folder separator character, otherwise the package path is treated as the full path including the file name.</span></span>

### <a name="includesymbols"></a><span data-ttu-id="76a30-314">IncludeSymbols</span><span class="sxs-lookup"><span data-stu-id="76a30-314">IncludeSymbols</span></span>

<span data-ttu-id="76a30-315">`MSBuild -t:pack -p:IncludeSymbols=true`를 사용하면 해당 `.pdb` 파일이 다른 출력 파일(`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`)과 함께 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-315">When using `MSBuild -t:pack -p:IncludeSymbols=true`, the corresponding `.pdb` files are copied along with other output files (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`).</span></span> <span data-ttu-id="76a30-316">`IncludeSymbols=true`를 설정하면 일반 패키지 *및* 기호 패키지가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-316">Note that setting `IncludeSymbols=true` creates a regular package *and* a symbols package.</span></span>

### <a name="includesource"></a><span data-ttu-id="76a30-317">IncludeSource</span><span class="sxs-lookup"><span data-stu-id="76a30-317">IncludeSource</span></span>

<span data-ttu-id="76a30-318">`.pdb` 파일과 함께 원본 파일을 복사한다는 점을 제외하고는 `IncludeSymbols`와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-318">This is the same as `IncludeSymbols`, except that it copies source files along with `.pdb` files as well.</span></span> <span data-ttu-id="76a30-319">`Compile` 형식의 모든 파일이 결과 패키지에서 상대 경로 폴더 구조를 유지하면서 `src\<ProjectName>\`에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-319">All files of type `Compile` are copied over to `src\<ProjectName>\` preserving the relative path folder structure in the resulting package.</span></span> <span data-ttu-id="76a30-320">또한 `TreatAsPackageReference`가 `false`로 설정된 `ProjectReference`의 원본 파일에 대해서도 마찬가지입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-320">The same also happens for source files of any `ProjectReference` which has `TreatAsPackageReference` set to `false`.</span></span>

<span data-ttu-id="76a30-321">Compile 형식의 파일이 프로젝트 폴더의 외부에 있는 경우 이 파일은 `src\<ProjectName>\`에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-321">If a file of type Compile, is outside the project folder, then it's just added to `src\<ProjectName>\`.</span></span>

### <a name="packing-a-license-expression-or-a-license-file"></a><span data-ttu-id="76a30-322">라이선스 식 또는 라이선스 파일 압축</span><span class="sxs-lookup"><span data-stu-id="76a30-322">Packing a license expression or a license file</span></span>

<span data-ttu-id="76a30-323">라이선스 식을 사용 하는 경우 속성을 사용 `PackageLicenseExpression` 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-323">When using a license expression, use the `PackageLicenseExpression` property.</span></span> <span data-ttu-id="76a30-324">샘플은 [라이선스 식 샘플](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-324">For a sample, see [License expression sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample).</span></span>

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

<span data-ttu-id="76a30-325">. 조직에서 허용 하는 라이선스 식 및 라이선스에 대 한 자세한 NuGet 내용은 [라이선스 메타 데이터](nuspec.md#license)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-325">To learn more about license expressions and licenses that are accepted by NuGet.org, see [license metadata](nuspec.md#license).</span></span>

<span data-ttu-id="76a30-326">라이선스 파일을 압축 하는 경우 속성을 사용 하 여 패키지 `PackageLicenseFile` 의 루트에 상대적인 패키지 경로를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-326">When packing a license file, use `PackageLicenseFile` property to specify the package path, relative to the root of the package.</span></span> <span data-ttu-id="76a30-327">또한 파일이 패키지에 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-327">In addition, make sure that the file is included in the package.</span></span> <span data-ttu-id="76a30-328">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-328">For example:</span></span>

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

<span data-ttu-id="76a30-329">샘플은 [라이선스 파일 샘플](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-329">For a sample, see [License file sample](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample).</span></span>

> [!NOTE]
> <span data-ttu-id="76a30-330">, 및 중 하나만 한 `PackageLicenseExpression` `PackageLicenseFile` `PackageLicenseUrl` 번에 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-330">Only one of `PackageLicenseExpression`, `PackageLicenseFile`, and `PackageLicenseUrl` can be specified at a time.</span></span>

### <a name="packing-a-file-without-an-extension"></a><span data-ttu-id="76a30-331">확장명 없이 파일 압축</span><span class="sxs-lookup"><span data-stu-id="76a30-331">Packing a file without an extension</span></span>

<span data-ttu-id="76a30-332">라이선스 파일을 압축 하는 경우와 같은 일부 시나리오에서는 확장명이 없는 파일을 포함 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-332">In some scenarios, like when packing a license file, you might want to include a file without an extension.</span></span>
<span data-ttu-id="76a30-333">기록을 위해 NuGet  &  MSBuild 확장명이 없는 경로를 디렉터리로 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-333">For historical reasons, NuGet & MSBuild treat paths without an extension as directories.</span></span>

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

<span data-ttu-id="76a30-334">[확장명 샘플이 없는 파일](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/)입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-334">[File without an extension sample](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).</span></span>

### <a name="istool"></a><span data-ttu-id="76a30-335">IsTool</span><span class="sxs-lookup"><span data-stu-id="76a30-335">IsTool</span></span>

<span data-ttu-id="76a30-336">`MSBuild -t:pack -p:IsTool=true`를 사용하면 [출력 어셈블리](#output-assemblies) 시나리오에서 지정한 대로 모든 출력 파일이 `lib` 폴더 대신 `tools` 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-336">When using `MSBuild -t:pack -p:IsTool=true`, all output files, as specified in the [Output Assemblies](#output-assemblies) scenario, are copied to the `tools` folder instead of the `lib` folder.</span></span> <span data-ttu-id="76a30-337">이는 `.csproj` 파일에서 `PackageType`을 설정하여 지정된 `DotNetCliTool`과 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-337">Note that this is different from a `DotNetCliTool` which is specified by setting the `PackageType` in `.csproj` file.</span></span>

### <a name="packing-using-a-nuspec-file"></a><span data-ttu-id="76a30-338">파일을 사용 하 여 압축 `.nuspec`</span><span class="sxs-lookup"><span data-stu-id="76a30-338">Packing using a `.nuspec` file</span></span>

<span data-ttu-id="76a30-339">일반적으로 파일에 있는 [모든 속성](../reference/msbuild-targets.md#pack-target) 을 프로젝트 파일에 포함 하는 것이 좋지만 `.nuspec` , 파일을 사용 하 여 프로젝트를 압축 하도록 선택할 수 있습니다 `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="76a30-339">Although it is recommended that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead, you can choose to use a `.nuspec` file to pack your project.</span></span> <span data-ttu-id="76a30-340">를 사용 하는 비 SDK 스타일 프로젝트의 경우 `PackageReference` `NuGet.Build.Tasks.Pack.targets` pack 작업을 실행할 수 있도록를 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-340">For a non-SDK-style project that uses `PackageReference`, you must import `NuGet.Build.Tasks.Pack.targets` so that the pack task can be executed.</span></span> <span data-ttu-id="76a30-341">여전히 프로젝트를 복원 해야 파일을 압축할 수 있습니다 nuspec .</span><span class="sxs-lookup"><span data-stu-id="76a30-341">You still need to restore the project before you can pack a nuspec file.</span></span> <span data-ttu-id="76a30-342">SDK 스타일 프로젝트는 기본적으로 pack 대상을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-342">(An SDK-style project includes the pack targets by default.)</span></span>

<span data-ttu-id="76a30-343">프로젝트 파일의 대상 프레임 워크는 관련이 없으며를 압축 하는 경우에는 사용 되지 않습니다 nuspec .</span><span class="sxs-lookup"><span data-stu-id="76a30-343">The target framework of the project file is irrelevant and not used when packing a nuspec.</span></span> <span data-ttu-id="76a30-344">다음 세 가지 MSBuild 속성은을 사용 하 여 압축 하는 것과 관련이 있습니다 `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="76a30-344">The following three MSBuild properties are relevant to packing using a `.nuspec`:</span></span>

1. <span data-ttu-id="76a30-345">`NuspecFile`: 압축에 사용되는 `.nuspec` 파일에 대한 상대 또는 절대 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-345">`NuspecFile`: relative or absolute path to the `.nuspec` file being used for packing.</span></span>
1. <span data-ttu-id="76a30-346">`NuspecProperties`: 세미콜론으로 구분된 key=value 쌍의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-346">`NuspecProperties`: a semicolon-separated list of key=value pairs.</span></span> <span data-ttu-id="76a30-347">명령줄 구문 분석이 작동 하는 방식으로 인해 MSBuild 여러 속성을 다음과 같이 지정 해야 합니다 `-p:NuspecProperties="key1=value1;key2=value2"` .</span><span class="sxs-lookup"><span data-stu-id="76a30-347">Due to the way MSBuild command-line parsing works, multiple properties must be specified as follows: `-p:NuspecProperties="key1=value1;key2=value2"`.</span></span>  
1. <span data-ttu-id="76a30-348">`NuspecBasePath`: `.nuspec` 파일에 대한 기본 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-348">`NuspecBasePath`: Base path for the `.nuspec` file.</span></span>

<span data-ttu-id="76a30-349">`dotnet.exe`를 사용하여 프로젝트를 압축하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-349">If using `dotnet.exe` to pack your project, use a command like the following:</span></span>

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="76a30-350">MSBuild를 사용하여 프로젝트를 압축하는 경우 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-350">If using MSBuild to pack your project, use a command like the following:</span></span>

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

<span data-ttu-id="76a30-351">nuspecdotnet.exe 또는 msbuild를 사용 하 여를 압축 하면 기본적으로 프로젝트를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-351">Please note that packing a nuspec using dotnet.exe or msbuild also leads to building the project by default.</span></span> <span data-ttu-id="76a30-352">이는 프로젝트 파일의 ```--no-build``` ```<NoBuild>true</NoBuild> ``` 설정과 함께 프로젝트 파일의 설정과 동일한 속성을 dotnet.exe 전달 하 여 방지할 수 있습니다 ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` .</span><span class="sxs-lookup"><span data-stu-id="76a30-352">This can be avoided by passing ```--no-build``` property to dotnet.exe, which is the equivalent of setting ```<NoBuild>true</NoBuild> ``` in your project file, along with setting ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in the project file.</span></span>

<span data-ttu-id="76a30-353">파일을 압축 하는 *.csproj* 파일의 예는 nuspec 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-353">An example of a *.csproj* file to pack a nuspec file is:</span></span>

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

### <a name="advanced-extension-points-to-create-customized-package"></a><span data-ttu-id="76a30-354">사용자 지정 패키지를 만들기 위한 고급 확장점</span><span class="sxs-lookup"><span data-stu-id="76a30-354">Advanced extension points to create customized package</span></span>

<span data-ttu-id="76a30-355">`pack`대상은 내부, 대상 프레임 워크 특정 빌드에서 실행 되는 두 개의 확장 지점이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-355">The `pack` target provides two extension points that run in the inner, target framework specific build.</span></span> <span data-ttu-id="76a30-356">확장 지점은 대상 프레임 워크 관련 콘텐츠 및 어셈블리를 패키지에 포함 하 여 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-356">The extension points support including target framework specific content and assemblies into a package:</span></span>

- <span data-ttu-id="76a30-357">`TargetsForTfmSpecificBuildOutput` 대상: `lib` 폴더 또는를 사용 하 여 지정 된 폴더 내의 파일에 사용 `BuildOutputTargetFolder` 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-357">`TargetsForTfmSpecificBuildOutput` target: Use for files inside the `lib` folder or a folder specified using `BuildOutputTargetFolder`.</span></span>
- <span data-ttu-id="76a30-358">`TargetsForTfmSpecificContentInPackage` 대상: 외부의 파일에 사용 `BuildOutputTargetFolder` 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-358">`TargetsForTfmSpecificContentInPackage` target: Use for files outside the `BuildOutputTargetFolder`.</span></span>

#### `TargetsForTfmSpecificBuildOutput`

<span data-ttu-id="76a30-359">사용자 지정 대상을 작성 하 고이를 속성의 값으로 지정 `$(TargetsForTfmSpecificBuildOutput)` 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-359">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificBuildOutput)` property.</span></span> <span data-ttu-id="76a30-360">로 이동 해야 하는 파일 `BuildOutputTargetFolder` (기본적으로 lib)의 경우 대상은 해당 파일을 ItemGroup에 쓰고 `BuildOutputInPackage` 다음 두 메타 데이터 값을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-360">For any files that need to go into the `BuildOutputTargetFolder` (lib by default), the target should write those files into the ItemGroup `BuildOutputInPackage` and set the following two metadata values:</span></span>

- <span data-ttu-id="76a30-361">`FinalOutputPath`: 파일의 절대 경로입니다. 제공 하지 않으면 Id가 원본 경로를 평가 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-361">`FinalOutputPath`: The absolute path of the file; if not provided, the Identity is used to evaluate source path.</span></span>
- <span data-ttu-id="76a30-362">`TargetPath`: (선택 사항) `lib\<TargetFramework>` 해당 문화권 폴더 아래에 있는 위성 어셈블리와 같이 파일을 내 하위 폴더로 이동 해야 하는 경우에 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-362">`TargetPath`:  (Optional) Set when the file needs to go into a subfolder within `lib\<TargetFramework>` , like satellite assemblies that go under their respective culture folders.</span></span> <span data-ttu-id="76a30-363">기본값은 파일의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-363">Defaults to the name of the file.</span></span>

<span data-ttu-id="76a30-364">예제:</span><span class="sxs-lookup"><span data-stu-id="76a30-364">Example:</span></span>

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

#### `TargetsForTfmSpecificContentInPackage`

<span data-ttu-id="76a30-365">사용자 지정 대상을 작성 하 고이를 속성의 값으로 지정 `$(TargetsForTfmSpecificContentInPackage)` 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-365">Write a custom target and specify it as the value of the `$(TargetsForTfmSpecificContentInPackage)` property.</span></span> <span data-ttu-id="76a30-366">패키지에 포함할 파일의 경우 대상은 해당 파일을 ItemGroup에 쓰고 `TfmSpecificPackageFile` 다음과 같은 선택적 메타 데이터를 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-366">For any files to include in the package, the target should write those files into the ItemGroup `TfmSpecificPackageFile` and set the following optional metadata:</span></span>

- <span data-ttu-id="76a30-367">`PackagePath`: 패키지에서 파일이 출력 되어야 하는 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-367">`PackagePath`: Path where the file should be output in the package.</span></span> <span data-ttu-id="76a30-368">NuGet 두 개 이상의 파일이 동일한 패키지 경로에 추가 되 면 경고를 발생 시킵니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-368">NuGet issues a warning if more than one file is added to the same package path.</span></span>
- <span data-ttu-id="76a30-369">`BuildAction`: 파일에 할당할 빌드 작업으로, 패키지 경로가 폴더에 있는 경우에만 필요 합니다 `contentFiles` .</span><span class="sxs-lookup"><span data-stu-id="76a30-369">`BuildAction`: The build action to assign to the file, required only if the package path is in the `contentFiles` folder.</span></span> <span data-ttu-id="76a30-370">기본값은 "None"입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-370">Defaults to "None".</span></span>

<span data-ttu-id="76a30-371">예제:</span><span class="sxs-lookup"><span data-stu-id="76a30-371">An example:</span></span>
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

## <a name="restore-target"></a><span data-ttu-id="76a30-372">restore 대상</span><span class="sxs-lookup"><span data-stu-id="76a30-372">restore target</span></span>

<span data-ttu-id="76a30-373">`MSBuild -t:restore`(.NET Core 프로젝트에서 `nuget restore` 및 `dotnet restore` 사용)는 프로젝트 파일에서 참조된 패키지를 다음과 같이 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-373">`MSBuild -t:restore` (which `nuget restore` and `dotnet restore` use with .NET Core projects), restores packages referenced in the project file as follows:</span></span>

1. <span data-ttu-id="76a30-374">모든 프로젝트 간 참조를 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-374">Read all project to project references</span></span>
1. <span data-ttu-id="76a30-375">프로젝트 속성을 읽어 중간 폴더 및 대상 프레임워크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-375">Read the project properties to find the intermediate folder and target frameworks</span></span>
1. <span data-ttu-id="76a30-376">MSBuild.Build.Tasks.dll에 데이터 NuGet 전달</span><span class="sxs-lookup"><span data-stu-id="76a30-376">Pass MSBuild data to NuGet.Build.Tasks.dll</span></span>
1. <span data-ttu-id="76a30-377">restore를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-377">Run restore</span></span>
1. <span data-ttu-id="76a30-378">패키지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-378">Download packages</span></span>
1. <span data-ttu-id="76a30-379">자산, targets 및 props 파일을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-379">Write assets file, targets, and props</span></span>

<span data-ttu-id="76a30-380">`restore`대상은 PackageReference 형식을 사용 하는 프로젝트에 대해 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-380">The `restore` target works for projects using the PackageReference format.</span></span>
<span data-ttu-id="76a30-381">`MSBuild 16.5+` 또한에서는 형식에 대 한 [옵트인 지원도 제공](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) `packages.config` 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-381">`MSBuild 16.5+` also has [opt-in support](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) for the `packages.config` format.</span></span>

> [!NOTE]
> <span data-ttu-id="76a30-382">대상은 `restore` 대상과 함께 [실행 해서는](#restoring-and-building-with-one-msbuild-command) 안 됩니다 `build` .</span><span class="sxs-lookup"><span data-stu-id="76a30-382">The `restore` target [should not be run](#restoring-and-building-with-one-msbuild-command) in combination with the `build` target.</span></span>

### <a name="restore-properties"></a><span data-ttu-id="76a30-383">restore 속성</span><span class="sxs-lookup"><span data-stu-id="76a30-383">Restore properties</span></span>

<span data-ttu-id="76a30-384">추가 복원 설정은 MSBuild 프로젝트 파일의 속성에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-384">Additional restore settings may come from MSBuild properties in the project file.</span></span> <span data-ttu-id="76a30-385">또한 값은 `-p:` 스위치를 사용하여 명령줄에서 설정할 수 있습니다(아래 예제 참조).</span><span class="sxs-lookup"><span data-stu-id="76a30-385">Values can also be set from the command line using the `-p:` switch (see Examples below).</span></span>

| <span data-ttu-id="76a30-386">속성</span><span class="sxs-lookup"><span data-stu-id="76a30-386">Property</span></span> | <span data-ttu-id="76a30-387">Description</span><span class="sxs-lookup"><span data-stu-id="76a30-387">Description</span></span> |
|--------|--------|
| `RestoreSources` | <span data-ttu-id="76a30-388">세미콜론으로 구분된 패키지 원본의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-388">Semicolon-delimited list of package sources.</span></span> |
| `RestorePackagesPath` | <span data-ttu-id="76a30-389">사용자 패키지 폴더에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-389">User packages folder path.</span></span> |
| `RestoreDisableParallel` | <span data-ttu-id="76a30-390">다운로드를 한 번에 하나씩으로 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-390">Limit downloads to one at a time.</span></span> |
| `RestoreConfigFile` | <span data-ttu-id="76a30-391">적용할 `Nuget.Config` 파일에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-391">Path to a `Nuget.Config` file to apply.</span></span> |
| `RestoreNoCache` | <span data-ttu-id="76a30-392">True 이면 캐시 된 패키지를 사용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-392">If true, avoids using cached packages.</span></span> <span data-ttu-id="76a30-393">[전역 패키지 및 캐시 폴더 관리](../consume-packages/managing-the-global-packages-and-cache-folders.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-393">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| `RestoreIgnoreFailedSources` | <span data-ttu-id="76a30-394">true이면 실패했거나 누락된 패키지 원본을 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-394">If true, ignores failing or missing package sources.</span></span> |
| `RestoreFallbackFolders` | <span data-ttu-id="76a30-395">사용자 패키지 폴더를 사용 하는 것과 같은 방식으로 사용 되는 대체 (Fallback) 폴더</span><span class="sxs-lookup"><span data-stu-id="76a30-395">Fallback folders, used in the same way the user packages folder is used.</span></span> |
| `RestoreAdditionalProjectSources` | <span data-ttu-id="76a30-396">복원 하는 동안 사용할 추가 원본입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-396">Additional sources to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFolders` | <span data-ttu-id="76a30-397">복원 중에 사용할 추가 대체 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-397">Additional fallback folders to use during restore.</span></span> |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | <span data-ttu-id="76a30-398">에 지정 된 대체 폴더를 제외 합니다. `RestoreAdditionalProjectFallbackFolders`</span><span class="sxs-lookup"><span data-stu-id="76a30-398">Excludes fallback folders specified in `RestoreAdditionalProjectFallbackFolders`</span></span> |
| `RestoreTaskAssemblyFile` | <span data-ttu-id="76a30-399">`NuGet.Build.Tasks.dll`에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-399">Path to `NuGet.Build.Tasks.dll`.</span></span> |
| `RestoreGraphProjectInput` | <span data-ttu-id="76a30-400">세미콜론으로 구분된 복원할 프로젝트의 목록이며, 절대 경로가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-400">Semicolon-delimited list of projects to restore, which should contain absolute paths.</span></span> |
| `RestoreUseSkipNonexistentTargets`  | <span data-ttu-id="76a30-401">프로젝트를 통해 수집 된 프로젝트는 MSBuild 최적화를 사용 하 여 수집 되는지 여부를 결정 합니다 `SkipNonexistentTargets` .</span><span class="sxs-lookup"><span data-stu-id="76a30-401">When the projects are collected via MSBuild it determines whether they are collected using the `SkipNonexistentTargets` optimization.</span></span> <span data-ttu-id="76a30-402">설정 하지 않으면 기본적으로로 설정 `true` 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-402">When not set, defaults to `true`.</span></span> <span data-ttu-id="76a30-403">결과는 프로젝트의 대상을 가져올 수 없는 경우의 빠른 오류 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-403">The consequence is a fail-fast behavior when a project's targets cannot be imported.</span></span> |
| `MSBuildProjectExtensionsPath` | <span data-ttu-id="76a30-404">출력 폴더, 및 폴더에 대 한 기본값입니다 `BaseIntermediateOutputPath` `obj` .</span><span class="sxs-lookup"><span data-stu-id="76a30-404">Output folder, defaulting to `BaseIntermediateOutputPath` and the `obj` folder.</span></span> |
| `RestoreForce` | <span data-ttu-id="76a30-405">PackageReference 기반 프로젝트에서 마지막 복원이 성공한 경우에도 모든 종속성이 확인 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-405">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="76a30-406">이 플래그를 지정 하는 것은 파일을 삭제 하는 것과 비슷합니다 `project.assets.json` .</span><span class="sxs-lookup"><span data-stu-id="76a30-406">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="76a30-407">이는 http 캐시를 우회 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-407">This does not bypass the http-cache.</span></span> |
| `RestorePackagesWithLockFile` | <span data-ttu-id="76a30-408">잠금 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-408">Opts into the usage of a lock file.</span></span> |
| `RestoreLockedMode` | <span data-ttu-id="76a30-409">잠금 모드에서 복원을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-409">Run restore in locked mode.</span></span> <span data-ttu-id="76a30-410">즉, 복원은 종속성을 다시 평가 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-410">This means that restore will not reevaluate the dependencies.</span></span> |
| `NuGetLockFilePath` | <span data-ttu-id="76a30-411">잠금 파일의 사용자 지정 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-411">A custom location for the lock file.</span></span> <span data-ttu-id="76a30-412">기본 위치는 프로젝트 옆에 있고 이름은 `packages.lock.json` 입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-412">The default location is next to the project and is named `packages.lock.json`.</span></span> |
| `RestoreForceEvaluate` | <span data-ttu-id="76a30-413">강제로 복원 하 여 종속성을 다시 계산 하 고 경고 없이 잠금 파일을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-413">Forces restore to recompute the dependencies and update the lock file without any warning.</span></span> |
| `RestorePackagesConfig` | <span data-ttu-id="76a30-414">packages.config를 사용 하 여 프로젝트를 복원 하는 옵트인 스위치. 만 지원 `MSBuild -t:restore` 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-414">An opt-in switch, that restores projects with packages.config. Support with `MSBuild -t:restore` only.</span></span> |
| `RestoreUseStaticGraphEvaluation` | <span data-ttu-id="76a30-415">표준 평가 대신 정적 그래프 평가를 사용 하는 옵트인 스위치입니다 MSBuild .</span><span class="sxs-lookup"><span data-stu-id="76a30-415">An opt-in switch to use static graph MSBuild evaluation instead of the standard evaluation.</span></span> <span data-ttu-id="76a30-416">정적 그래프 평가는 큰 리포지토리 및 솔루션에 대해 훨씬 더 빠른 실험적 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-416">Static graph evaluation is an experimental feature that's significantly faster for large repos and solutions.</span></span> |

#### <a name="examples"></a><span data-ttu-id="76a30-417">예</span><span class="sxs-lookup"><span data-stu-id="76a30-417">Examples</span></span>

<span data-ttu-id="76a30-418">명령줄:</span><span class="sxs-lookup"><span data-stu-id="76a30-418">Command line:</span></span>

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

<span data-ttu-id="76a30-419">프로젝트 파일:</span><span class="sxs-lookup"><span data-stu-id="76a30-419">Project file:</span></span>

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a><span data-ttu-id="76a30-420">restore 출력</span><span class="sxs-lookup"><span data-stu-id="76a30-420">Restore outputs</span></span>

<span data-ttu-id="76a30-421">restore는 `obj` 빌드 폴더에 다음 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-421">Restore creates the following files in the build `obj` folder:</span></span>

| <span data-ttu-id="76a30-422">파일</span><span class="sxs-lookup"><span data-stu-id="76a30-422">File</span></span> | <span data-ttu-id="76a30-423">Description</span><span class="sxs-lookup"><span data-stu-id="76a30-423">Description</span></span> |
|--------|--------|
| `project.assets.json` | <span data-ttu-id="76a30-424">모든 패키지 참조의 종속성 그래프를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-424">Contains the dependency graph of all package references.</span></span> |
| `{projectName}.projectFileExtension.nuget.g.props` | <span data-ttu-id="76a30-425">MSBuild패키지에 포함 된 props에 대 한 참조</span><span class="sxs-lookup"><span data-stu-id="76a30-425">References to MSBuild props contained in packages</span></span> |
| `{projectName}.projectFileExtension.nuget.g.targets` | <span data-ttu-id="76a30-426">MSBuild패키지에 포함 된 대상에 대 한 참조</span><span class="sxs-lookup"><span data-stu-id="76a30-426">References to MSBuild targets contained in packages</span></span> |

### <a name="restoring-and-building-with-one-msbuild-command"></a><span data-ttu-id="76a30-427">단일 명령을 사용 하 여 복원 및 빌드 MSBuild</span><span class="sxs-lookup"><span data-stu-id="76a30-427">Restoring and building with one MSBuild command</span></span>

<span data-ttu-id="76a30-428">NuGet MSBuild 대상 및 props을 가져오는 패키지를 복원할 수 있으므로 복원 및 빌드 평가는 다른 전역 속성을 사용 하 여 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-428">Due to the fact that NuGet can restore packages that bring down MSBuild targets and props, the restore and build evaluations are run with different global properties.</span></span>
<span data-ttu-id="76a30-429">즉, 다음은 예측할 수 없으며 종종 잘못 된 동작을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-429">This means that the following will have an unpredictable and often incorrect behavior.</span></span>

```cli
msbuild -t:restore,build
```

 <span data-ttu-id="76a30-430">대신에 권장 되는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-430">Instead the recommended approach is:</span></span>

```cli
msbuild -t:build -restore
```

<span data-ttu-id="76a30-431">같은 논리는와 유사한 다른 대상에도 적용 됩니다 `build` .</span><span class="sxs-lookup"><span data-stu-id="76a30-431">The same logic applies to other targets similar to `build`.</span></span>

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a><span data-ttu-id="76a30-432">PackageReference 및 packages.config 프로젝트 복원 MSBuild</span><span class="sxs-lookup"><span data-stu-id="76a30-432">Restoring PackageReference and packages.config projects with MSBuild</span></span>

<span data-ttu-id="76a30-433">MSBuild16.5 +를 사용 하는 경우에도 packages.config 지원 됩니다 `msbuild -t:restore` .</span><span class="sxs-lookup"><span data-stu-id="76a30-433">With MSBuild 16.5+, packages.config are also supported for `msbuild -t:restore`.</span></span>

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> <span data-ttu-id="76a30-434">`packages.config` restore는와 함께 사용할 수 `MSBuild 16.5+` 없습니다. `dotnet.exe`</span><span class="sxs-lookup"><span data-stu-id="76a30-434">`packages.config` restore is only available with `MSBuild 16.5+`, and not with `dotnet.exe`</span></span>

### <a name="restoring-with-msbuild-static-graph-evaluation"></a><span data-ttu-id="76a30-435">정적 그래프 평가를 사용 하 여 복원 MSBuild</span><span class="sxs-lookup"><span data-stu-id="76a30-435">Restoring with MSBuild static graph evaluation</span></span>

> [!NOTE]
> <span data-ttu-id="76a30-436">MSBuild16.6 +를 사용 하는 경우 NuGet 큰 리포지토리의 복원 시간이 크게 향상 되는 명령줄에서 정적 그래프 평가를 사용 하는 실험적 기능을 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-436">With MSBuild 16.6+, NuGet has added an experimental feature to use static graph evaluation from the command line that significantly improves the restore time for large repositories.</span></span>

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

<span data-ttu-id="76a30-437">또는 디렉터리에 속성을 설정 하 여 사용 하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-437">Alternatively you can enable it by setting the property in a Directory.Build.Props.</span></span>

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> <span data-ttu-id="76a30-438">Visual Studio 2019. x 및 2.x의 NuGet 경우이 기능은 실험적 이며 옵트인 (opt in) 이라고 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-438">As of Visual Studio 2019.x and NuGet 5.x, this feature is considered experimental and opt-in.</span></span> <span data-ttu-id="76a30-439">이 기능이 기본적으로 사용 되는 경우에 대 한 자세한 내용은 [ NuGet /Home # 9803](https://github.com/NuGet/Home/issues/9803) 를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-439">Follow [NuGet/Home#9803](https://github.com/NuGet/Home/issues/9803) for details on when this feature will be enabled by default.</span></span>

<span data-ttu-id="76a30-440">정적 그래프 복원은 복원, 프로젝트 읽기 및 평가의 msbuild 부분을 변경 하지만 복원 알고리즘은 변경 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-440">Static graph restore changes the msbuild part of restore, the project reading and evaluation, but not the restore algorithm!</span></span> <span data-ttu-id="76a30-441">복원 알고리즘은 모든 NuGet 도구 ( NuGet .exe, MSBuild .exe, dotnet.exe 및 Visual Studio)에서 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-441">The restore algorithm is the same across all NuGet tools (NuGet.exe, MSBuild.exe, dotnet.exe and Visual Studio).</span></span>

<span data-ttu-id="76a30-442">거의 모든 시나리오에서 정적 그래프 복원은 현재 복원과 다르게 동작할 수 있으며 선언 된 특정 PackageReferences 또는 ProjectReferences가 누락 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-442">In very few scenarios, static graph restore may behave differently from current restore and certain declared PackageReferences or ProjectReferences might be missing.</span></span>

<span data-ttu-id="76a30-443">정적 그래프 복원으로 마이그레이션할 때를 한 번만 확인 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-443">To ease your mind, as a one time check, when migrating to static graph restore, consider running:</span></span>

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

<span data-ttu-id="76a30-444">NuGet 변경 *내용을 보고 하면 안 됩니다* .</span><span class="sxs-lookup"><span data-stu-id="76a30-444">NuGet should *not* report any changes.</span></span> <span data-ttu-id="76a30-445">불일치가 표시 되는 경우 [ NuGet /Home](https://github.com/nuget/home/issues/new)에서 문제를 파일에 입력 하세요.</span><span class="sxs-lookup"><span data-stu-id="76a30-445">If you do see a discrepancy, please file an issue at [NuGet/Home](https://github.com/nuget/home/issues/new).</span></span>

### <a name="replacing-one-library-from-a-restore-graph"></a><span data-ttu-id="76a30-446">복원 그래프에서 단일 라이브러리 대체</span><span class="sxs-lookup"><span data-stu-id="76a30-446">Replacing one library from a restore graph</span></span>

<span data-ttu-id="76a30-447">restore에서 잘못된 어셈블리를 가져오는 경우 해당 패키지의 기본 선택 항목을 제외하는 한편 원하는 선택 항목으로 대체할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-447">If a restore is bringing the wrong assembly, it's possible to exclude that packages default choice, and replace it with your own choice.</span></span> <span data-ttu-id="76a30-448">먼저 최상위 `PackageReference`를 사용하여 모든 자산을 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-448">First with a top level `PackageReference`, exclude all assets:</span></span>

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

<span data-ttu-id="76a30-449">그런 다음 DLL의 적절한 로컬 복사본에 대한 고유한 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="76a30-449">Next, add your own reference to the appropriate local copy of the DLL:</span></span>

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
