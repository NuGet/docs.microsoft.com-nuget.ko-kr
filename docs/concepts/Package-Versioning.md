---
title: NuGet 패키지 버전 참조
description: NuGet 패키지가 종속된 다른 패키지의 버전 번호 및 범위 지정과 종속성 설치 방법에 대한 정확한 세부 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 4cb12f439d796d583f52d657225c39418d5a4836
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237363"
---
# <a name="package-versioning"></a><span data-ttu-id="dbf09-103">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="dbf09-103">Package versioning</span></span>

<span data-ttu-id="dbf09-104">특정 패키지는 항상 패키지 식별자와 정확한 버전 번호를 사용하여 참조됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="dbf09-105">예를 들어, nuget.org의 [Entity Framework](https://www.nuget.org/packages/EntityFramework/)에는 버전 *4.1.10311* 에서 버전 *6.1.3* (안정적인 최신 릴리스)과 *6.2.0-beta1* 과 같은 다양한 시험판 버전에 이르기까지 수십 개의 특정 패키지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="dbf09-106">패키지를 만들 때 선택적 시험판 문자 접미사를 사용하여 특정 버전 번호를 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="dbf09-107">반면, 패키지를 사용할 때는 정확한 버전 번호 또는 허용 가능한 버전 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="dbf09-108">항목 내용</span><span class="sxs-lookup"><span data-stu-id="dbf09-108">In this topic:</span></span>

- <span data-ttu-id="dbf09-109">시험판 접미사 등의 [버전 기본 사항](#version-basics)입니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="dbf09-110">버전 범위</span><span class="sxs-lookup"><span data-stu-id="dbf09-110">Version ranges</span></span>](#version-ranges)
- [<span data-ttu-id="dbf09-111">정규화된 버전 번호</span><span class="sxs-lookup"><span data-stu-id="dbf09-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="dbf09-112">버전 기본 사항</span><span class="sxs-lookup"><span data-stu-id="dbf09-112">Version basics</span></span>

<span data-ttu-id="dbf09-113">특정 버전 번호는 *주.부.패치[-접미사]* 형식으로 되어 있으며, 해당 구성 요소의 의미는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]* , where the components have the following meanings:</span></span>

- <span data-ttu-id="dbf09-114">*주* : 호환성이 손상되는 변경</span><span class="sxs-lookup"><span data-stu-id="dbf09-114">*Major* : Breaking changes</span></span>
- <span data-ttu-id="dbf09-115">*부* : 이전 버전과 호환되는 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="dbf09-115">*Minor* : New features, but backwards compatible</span></span>
- <span data-ttu-id="dbf09-116">*패치* : 이전 버전과 호환되는 버그 수정에만 해당</span><span class="sxs-lookup"><span data-stu-id="dbf09-116">*Patch* : Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="dbf09-117">*-접미사* (선택 사항): 하이픈 다음에는 시험판 버전을 나타내는 문자열( [유의적 버전 또는 SemVer 1.0 규칙](https://semver.org/spec/v1.0.0.html)을 따름)이 옵니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="dbf09-118">**예:**</span><span class="sxs-lookup"><span data-stu-id="dbf09-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="dbf09-119">nuget.org는 정확한 버전 번호가 없는 패키지 업로드를 모두 거부합니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="dbf09-120">버전은 패키지를 만드는 데 사용되는 `.nuspec` 또는 프로젝트 파일에 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="dbf09-121">시험판 버전</span><span class="sxs-lookup"><span data-stu-id="dbf09-121">Pre-release versions</span></span>

<span data-ttu-id="dbf09-122">엄밀히 따지면, 패키지 작성자는 어떤 문자열이든 시험판 버전을 나타내는 접미사로 사용할 수 있습니다. 그 이유는 NuGet이 이러한 모든 버전을 시험판으로 처리하며, 달리 해석하지 않기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="dbf09-123">즉, NuGet은 어떤 UI가 사용되었는지에 상관없이 전체 버전 문자열을 표시하며, 접미사의 의미는 전적으로 소비자의 해석에 맡깁니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="dbf09-124">그렇긴 하지만 패키지 개발자는 일반적으로 널리 인정된 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="dbf09-125">`-alpha`: 일반적으로 진행 중인 작업이나 실험에 사용되는 알파 릴리스입니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="dbf09-126">`-beta`: 일반적으로 다음에 계획된 릴리스에 대한 기능 완료인 베타 릴리스이지만 알려진 버그를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="dbf09-127">`-rc`: 일반적으로 심각한 버그가 발생하지 않는 한 잠재적으로 최종적(안정적)인 릴리스인 릴리스 후보입니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="dbf09-128">NuGet 4.3.0 이상은 *1.0.1-build.23* 에서와 같이 시험판 번호에 점 표기법을 지원하는 [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="dbf09-129">NuGet 4.3.0 이전 버전에서는 점 표기법이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="dbf09-130">*1.0.1-build23* 과 같은 형식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="dbf09-131">패키지 참조를 확인할 때 패키지 버전 여러 개가 접미사만 다른 경우 NuGet은 먼저 접미사가 없는 버전을 선택한 다음, 알파벳 역순으로 시험판 버전에 우선 순위를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="dbf09-132">예를 들어, 다음 버전은 정확히 표시된 순서대로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="dbf09-133">유의적 버전 2.0.0</span><span class="sxs-lookup"><span data-stu-id="dbf09-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="dbf09-134">NuGet은 NuGet 4.3.0 이상 및 Visual Studio 2017 버전 15.3 이상을 통해 [유의적 버전 2.0.0](https://semver.org/spec/v2.0.0.html)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="dbf09-135">SemVer v2.0.0의 특정 의미 체계는 이전 클라이언트에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="dbf09-136">NuGet은 다음 문 중 하나라도 참인 경우 패키지 버전이 SemVer v2.0.0에 해당한다고 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="dbf09-137">시험판 레이블이 점으로 구분됩니다(예: *1.0.0-alpha.1* ).</span><span class="sxs-lookup"><span data-stu-id="dbf09-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="dbf09-138">버전에 빌드-메타데이터(예: *1.0.0+githash* )가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="dbf09-139">nuget.org의 경우 패키지는 다음 문 중 하나가 참인 경우 SemVer v2.0.0 패키지로 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="dbf09-140">패키지의 자체 버전은 위에서 정의한 대로 SemVer v2.0.0 규격이며, SemVer v1.0.0 규격이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="dbf09-141">패키지의 모든 종속성 버전 범위에는 최소 또는 최대 버전이 있으며, 이는 위에서 정의한 대로 SemVer v2.0.0 규격이며, SemVer v1.0.0 규격이 아닙니다(예: *[1.0.0-alpha.1, )* ).</span><span class="sxs-lookup"><span data-stu-id="dbf09-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="dbf09-142">SemVer v2.0.0 특정 패키지를 nuget.org에 업로드하는 경우 패키지는 이전 클라이언트에 표시되지 않으며, 다음 NuGet 클라이언트에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="dbf09-143">NuGet 4.3.0 이상</span><span class="sxs-lookup"><span data-stu-id="dbf09-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="dbf09-144">Visual Studio 2017 버전 15.3 이상</span><span class="sxs-lookup"><span data-stu-id="dbf09-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="dbf09-145">[NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)을 사용하는 Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="dbf09-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="dbf09-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="dbf09-146">dotnet</span></span>
  - <span data-ttu-id="dbf09-147">dotnetcore.exe(.NET SDK 2.0.0 이상)</span><span class="sxs-lookup"><span data-stu-id="dbf09-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="dbf09-148">타사 클라이언트:</span><span class="sxs-lookup"><span data-stu-id="dbf09-148">Third-party clients:</span></span>

- <span data-ttu-id="dbf09-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="dbf09-149">JetBrains Rider</span></span>
- <span data-ttu-id="dbf09-150">Paket 버전 5.0 이상</span><span class="sxs-lookup"><span data-stu-id="dbf09-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a><span data-ttu-id="dbf09-151">버전 범위</span><span class="sxs-lookup"><span data-stu-id="dbf09-151">Version ranges</span></span>

<span data-ttu-id="dbf09-152">패키지 종속성을 참조할 때 NuGet은 간격 표기법으로 버전 범위를 다음과 같이 요약하여 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="dbf09-153">Notation</span><span class="sxs-lookup"><span data-stu-id="dbf09-153">Notation</span></span> | <span data-ttu-id="dbf09-154">적용된 규칙</span><span class="sxs-lookup"><span data-stu-id="dbf09-154">Applied rule</span></span> | <span data-ttu-id="dbf09-155">설명</span><span class="sxs-lookup"><span data-stu-id="dbf09-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="dbf09-156">1.0</span><span class="sxs-lookup"><span data-stu-id="dbf09-156">1.0</span></span> | <span data-ttu-id="dbf09-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="dbf09-157">x ≥ 1.0</span></span> | <span data-ttu-id="dbf09-158">최소 버전(포함)</span><span class="sxs-lookup"><span data-stu-id="dbf09-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="dbf09-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="dbf09-159">(1.0,)</span></span> | <span data-ttu-id="dbf09-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="dbf09-160">x > 1.0</span></span> | <span data-ttu-id="dbf09-161">최소 버전(제외)</span><span class="sxs-lookup"><span data-stu-id="dbf09-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="dbf09-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="dbf09-162">[1.0]</span></span> | <span data-ttu-id="dbf09-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="dbf09-163">x == 1.0</span></span> | <span data-ttu-id="dbf09-164">정확한 버전 일치</span><span class="sxs-lookup"><span data-stu-id="dbf09-164">Exact version match</span></span> |
| <span data-ttu-id="dbf09-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="dbf09-165">(,1.0]</span></span> | <span data-ttu-id="dbf09-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="dbf09-166">x ≤ 1.0</span></span> | <span data-ttu-id="dbf09-167">최대 버전(포함)</span><span class="sxs-lookup"><span data-stu-id="dbf09-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="dbf09-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="dbf09-168">(,1.0)</span></span> | <span data-ttu-id="dbf09-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="dbf09-169">x < 1.0</span></span> | <span data-ttu-id="dbf09-170">최대 버전(제외)</span><span class="sxs-lookup"><span data-stu-id="dbf09-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="dbf09-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="dbf09-171">[1.0,2.0]</span></span> | <span data-ttu-id="dbf09-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="dbf09-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="dbf09-173">정확한 범위(포함)</span><span class="sxs-lookup"><span data-stu-id="dbf09-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="dbf09-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="dbf09-174">(1.0,2.0)</span></span> | <span data-ttu-id="dbf09-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="dbf09-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="dbf09-176">정확한 범위(제외)</span><span class="sxs-lookup"><span data-stu-id="dbf09-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="dbf09-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="dbf09-177">[1.0,2.0)</span></span> | <span data-ttu-id="dbf09-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="dbf09-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="dbf09-179">최소 포함 및 최대 제외 혼합 버전</span><span class="sxs-lookup"><span data-stu-id="dbf09-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="dbf09-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="dbf09-180">(1.0)</span></span>    | <span data-ttu-id="dbf09-181">잘못된</span><span class="sxs-lookup"><span data-stu-id="dbf09-181">invalid</span></span> | <span data-ttu-id="dbf09-182">잘못된</span><span class="sxs-lookup"><span data-stu-id="dbf09-182">invalid</span></span> |

<span data-ttu-id="dbf09-183">PackageReference 형식을 사용하는 경우 NuGet은 버전 번호의 주, 부, 패치, 시험판 접미사 부분에 부동 표기법(\*)도 사용할 수 있도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-183">When using the PackageReference format, NuGet also supports using a floating notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="dbf09-184">`packages.config` 형식에서는 부동 버전이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-184">Floating versions are not supported with the `packages.config` format.</span></span> <span data-ttu-id="dbf09-185">부동 버전이 지정된 경우, 규칙은 버전 설명과 일치하는 기존의 최상 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-185">When a floating version is specified, the rule is to resolve to the highest existent version that matches the version description.</span></span> <span data-ttu-id="dbf09-186">부동 버전 및 해상도의 예는 아래와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-186">Examples of floating versions and the resolutions are below.</span></span>

> [!Note]
> <span data-ttu-id="dbf09-187">PackageReference의 버전 범위에는 시험판 버전이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-187">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="dbf09-188">부동 버전은 옵트인되지 않는 한 의도적으로 시험판 버전을 확인하지 않도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-188">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="dbf09-189">관련 기능 요청 상태는 [문제 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dbf09-189">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="dbf09-190">예제</span><span class="sxs-lookup"><span data-stu-id="dbf09-190">Examples</span></span>

<span data-ttu-id="dbf09-191">프로젝트 파일, `packages.config` 파일, `.nuspec` 파일에서 패키지 종속성의 버전 또는 버전 범위를 항상 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-191">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="dbf09-192">버전 또는 버전 범위가 없으면, 종속성을 확인할 때 NuGet 2.8.x 이하는 사용 가능한 최신 패키지 버전을 선택하는 반면, NuGet 3.x 이상은 가장 낮은 패키지 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-192">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="dbf09-193">버전 또는 버전 범위를 지정하면 이러한 불확실성을 피할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-193">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="dbf09-194">프로젝트 파일의 참조(PackageReference)</span><span class="sxs-lookup"><span data-stu-id="dbf09-194">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version.
     Will resolve to the highest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. 
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. 
     Will resolve to the smallest acceptable stable version.
     -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher.
     Will resolve to the smallest acceptable stable version. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

#### <a name="floating-version-resolutions"></a><span data-ttu-id="dbf09-195">부동 버전 해상도</span><span class="sxs-lookup"><span data-stu-id="dbf09-195">Floating version resolutions</span></span> 

| <span data-ttu-id="dbf09-196">버전</span><span class="sxs-lookup"><span data-stu-id="dbf09-196">Version</span></span> | <span data-ttu-id="dbf09-197">서버에 표시되는 버전</span><span class="sxs-lookup"><span data-stu-id="dbf09-197">Versions present on server</span></span> | <span data-ttu-id="dbf09-198">해결 방법</span><span class="sxs-lookup"><span data-stu-id="dbf09-198">Resolution</span></span> | <span data-ttu-id="dbf09-199">이유</span><span class="sxs-lookup"><span data-stu-id="dbf09-199">Reason</span></span> | <span data-ttu-id="dbf09-200">참고</span><span class="sxs-lookup"><span data-stu-id="dbf09-200">Notes</span></span> |
|----------|--------------|-------------|-------------|-------------|
| * | <span data-ttu-id="dbf09-201">1.1.0</span><span class="sxs-lookup"><span data-stu-id="dbf09-201">1.1.0</span></span> <br> <span data-ttu-id="dbf09-202">1.1.1</span><span class="sxs-lookup"><span data-stu-id="dbf09-202">1.1.1</span></span> <br> <span data-ttu-id="dbf09-203">1.2.0</span><span class="sxs-lookup"><span data-stu-id="dbf09-203">1.2.0</span></span> <br> <span data-ttu-id="dbf09-204">1.3.0-alpha</span><span class="sxs-lookup"><span data-stu-id="dbf09-204">1.3.0-alpha</span></span>  | <span data-ttu-id="dbf09-205">1.2.0</span><span class="sxs-lookup"><span data-stu-id="dbf09-205">1.2.0</span></span> | <span data-ttu-id="dbf09-206">안정적인 최상 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-206">The highest stable version.</span></span> |
| <span data-ttu-id="dbf09-207">1.1.\*</span><span class="sxs-lookup"><span data-stu-id="dbf09-207">1.1.\*</span></span> | <span data-ttu-id="dbf09-208">1.1.0</span><span class="sxs-lookup"><span data-stu-id="dbf09-208">1.1.0</span></span> <br> <span data-ttu-id="dbf09-209">1.1.1</span><span class="sxs-lookup"><span data-stu-id="dbf09-209">1.1.1</span></span> <br> <span data-ttu-id="dbf09-210">1.1.2-alpha</span><span class="sxs-lookup"><span data-stu-id="dbf09-210">1.1.2-alpha</span></span> <br> <span data-ttu-id="dbf09-211">1.2.0-alpha</span><span class="sxs-lookup"><span data-stu-id="dbf09-211">1.2.0-alpha</span></span> | <span data-ttu-id="dbf09-212">1.1.1</span><span class="sxs-lookup"><span data-stu-id="dbf09-212">1.1.1</span></span> | <span data-ttu-id="dbf09-213">지정된 패턴을 따르는 안정적인 최상 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-213">The highest stable version that respects the specified pattern.</span></span>|
| <span data-ttu-id="dbf09-214">\* - \*</span><span class="sxs-lookup"><span data-stu-id="dbf09-214">\* - \*</span></span> | <span data-ttu-id="dbf09-215">1.1.0</span><span class="sxs-lookup"><span data-stu-id="dbf09-215">1.1.0</span></span> <br> <span data-ttu-id="dbf09-216">1.1.1</span><span class="sxs-lookup"><span data-stu-id="dbf09-216">1.1.1</span></span> <br> <span data-ttu-id="dbf09-217">1.1.2-alpha</span><span class="sxs-lookup"><span data-stu-id="dbf09-217">1.1.2-alpha</span></span> <br> <span data-ttu-id="dbf09-218">1.3.0-beta</span><span class="sxs-lookup"><span data-stu-id="dbf09-218">1.3.0-beta</span></span>  | <span data-ttu-id="dbf09-219">1.3.0-beta</span><span class="sxs-lookup"><span data-stu-id="dbf09-219">1.3.0-beta</span></span> | <span data-ttu-id="dbf09-220">불안정한 버전을 포함하는 최상 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-220">The highest version including the not stable versions.</span></span> | <span data-ttu-id="dbf09-221">Visual Studio 버전 16.6, NuGet 버전 5.6, .NET Core SDK 버전 3.1.300에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="dbf09-221">Available in Visual Studio version 16.6, NuGet version 5.6, .NET Core SDK version 3.1.300</span></span> |
| <span data-ttu-id="dbf09-222">1.1.\* - \*</span><span class="sxs-lookup"><span data-stu-id="dbf09-222">1.1.\* - \*</span></span> | <span data-ttu-id="dbf09-223">1.1.0</span><span class="sxs-lookup"><span data-stu-id="dbf09-223">1.1.0</span></span> <br> <span data-ttu-id="dbf09-224">1.1.1</span><span class="sxs-lookup"><span data-stu-id="dbf09-224">1.1.1</span></span> <br> <span data-ttu-id="dbf09-225">1.1.2-alpha</span><span class="sxs-lookup"><span data-stu-id="dbf09-225">1.1.2-alpha</span></span> <br> <span data-ttu-id="dbf09-226">1.1.2-beta</span><span class="sxs-lookup"><span data-stu-id="dbf09-226">1.1.2-beta</span></span> <br> <span data-ttu-id="dbf09-227">1.3.0-beta</span><span class="sxs-lookup"><span data-stu-id="dbf09-227">1.3.0-beta</span></span>  | <span data-ttu-id="dbf09-228">1.1.2-beta</span><span class="sxs-lookup"><span data-stu-id="dbf09-228">1.1.2-beta</span></span> | <span data-ttu-id="dbf09-229">불안정한 버전을 포함하며 패턴을 따르는 최상 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-229">The highest version respecting the pattern and including the not stable versions.</span></span> | <span data-ttu-id="dbf09-230">Visual Studio 버전 16.6, NuGet 버전 5.6, .NET Core SDK 버전 3.1.300에서 사용 가능</span><span class="sxs-lookup"><span data-stu-id="dbf09-230">Available in Visual Studio version 16.6, NuGet version 5.6, .NET Core SDK version 3.1.300</span></span> |

<span data-ttu-id="dbf09-231">**`packages.config`에서의 참조:**</span><span class="sxs-lookup"><span data-stu-id="dbf09-231">**References in `packages.config`:**</span></span>

<span data-ttu-id="dbf09-232">`packages.config`에서 모든 종속성은 패키지를 복원할 때 사용되는 정확한 `version` 특성과 함께 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-232">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="dbf09-233">`allowedVersions` 특성은 패키지가 업데이트될 수 있는 버전을 제한하기 위해 업데이트 작업 시에만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-233">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

<span data-ttu-id="dbf09-234">**`.nuspec`파일에서의 참조**</span><span class="sxs-lookup"><span data-stu-id="dbf09-234">**References in `.nuspec` files**</span></span>

<span data-ttu-id="dbf09-235">`<dependency>` 요소의 `version` 특성은 종속성에 허용되는 범위 버전을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-235">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a><span data-ttu-id="dbf09-236">정규화된 버전 번호</span><span class="sxs-lookup"><span data-stu-id="dbf09-236">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="dbf09-237">이는 NuGet 3.4 이상에서 호환성이 손상되는 변경입니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-237">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="dbf09-238">설치, 다시 설치 또는 복원 작업 시 리포지토리에서 패키지를 가져올 때 NuGet 3.4 이상은 버전 번호를 다음과 같이 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-238">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="dbf09-239">버전 번호 앞에 있는 0을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-239">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="dbf09-240">버전 번호의 네 번째 파트에서 0을 생략합니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-240">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1
        
- <span data-ttu-id="dbf09-241">SemVer 2.0.0 빌드 메타데이터가 제거됨</span><span class="sxs-lookup"><span data-stu-id="dbf09-241">SemVer 2.0.0 build metadata is removed</span></span>

        1.0.7+r3456 is treated as 1.0.7

<span data-ttu-id="dbf09-242">`pack` 및 `restore` 작업은 가능한 경우 항상 버전을 정규화합니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-242">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="dbf09-243">이미 빌드된 패키지의 경우, 이 정규화 작업이 패키지 자체의 버전 번호에 영향을 주지는 않습니다. NuGet이 종속성을 확인할 때 버전과 일치시키는 방식에만 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-243">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="dbf09-244">그러나 패키지 버전 중복을 방지하기 위해서는 NuGet 패키지 리포지토리에서 이러한 값을 NuGet과 동일한 방식으로 처리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-244">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="dbf09-245">따라서 패키지 버전 *1.0* 을 포함하는 리포지토리는 버전 *1.0.0* 도 별도의 다른 패키지로 호스트해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dbf09-245">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
