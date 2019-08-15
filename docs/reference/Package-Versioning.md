---
title: NuGet 패키지 버전 참조
description: NuGet 패키지가 종속 된 다른 패키지에 대 한 버전 번호 및 범위 지정과 종속성 설치 방법에 대 한 정확한 세부 정보
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69019992"
---
# <a name="package-versioning"></a><span data-ttu-id="b06ee-103">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="b06ee-103">Package versioning</span></span>

<span data-ttu-id="b06ee-104">특정 패키지는 항상 패키지 식별자와 정확한 버전 번호를 사용 하는 것으로 간주 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="b06ee-105">예를 들어 nuget.org의 [Entity Framework](https://www.nuget.org/packages/EntityFramework/) 에는 버전 *4.1.10311* 에서 버전 *6.1.3* (안정적인 최신 릴리스) 및 *6.2.0-beta1과 같은 다양 한 시험판 버전까지 사용 가능한 수십 개의 특정 패키지가 있습니다.* .</span><span class="sxs-lookup"><span data-stu-id="b06ee-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="b06ee-106">패키지를 만들 때 선택적 시험판 텍스트 접미사를 사용 하 여 특정 버전 번호를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="b06ee-107">반면 패키지를 사용 하는 경우 정확한 버전 번호 또는 허용 되는 버전 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="b06ee-108">항목 내용</span><span class="sxs-lookup"><span data-stu-id="b06ee-108">In this topic:</span></span>

- <span data-ttu-id="b06ee-109">시험판 접미사를 포함 한 [버전 기본 사항](#version-basics) 입니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="b06ee-110">버전 범위 및 와일드 카드</span><span class="sxs-lookup"><span data-stu-id="b06ee-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="b06ee-111">정규화 된 버전 번호</span><span class="sxs-lookup"><span data-stu-id="b06ee-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="b06ee-112">버전 기본 사항</span><span class="sxs-lookup"><span data-stu-id="b06ee-112">Version basics</span></span>

<span data-ttu-id="b06ee-113">특정 버전 번호는 *Major [-Suffix]* 형식으로 되어 있습니다. 여기서 구성 요소의 의미는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="b06ee-114">*주*: 호환성이 손상되는 변경</span><span class="sxs-lookup"><span data-stu-id="b06ee-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="b06ee-115">*부*: 이전 버전과 호환되는 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="b06ee-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="b06ee-116">*패치*: 이전 버전과 호환되는 버그 수정에만 해당</span><span class="sxs-lookup"><span data-stu-id="b06ee-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="b06ee-117">*-접미사* (선택 사항): 하이픈 뒤에 시험판 버전을 나타내는 문자열이 오고 있습니다 ( [의미 체계 버전 관리 또는 SemVer 1.0 규칙](http://semver.org/spec/v1.0.0.html)에 따라).</span><span class="sxs-lookup"><span data-stu-id="b06ee-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="b06ee-118">**예:**</span><span class="sxs-lookup"><span data-stu-id="b06ee-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="b06ee-119">nuget.org은 정확한 버전 번호가 없는 패키지 업로드를 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="b06ee-120">패키지를 만드는 데 사용 되는 `.nuspec` 또는 프로젝트 파일에 버전을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="b06ee-121">시험판 버전</span><span class="sxs-lookup"><span data-stu-id="b06ee-121">Pre-release versions</span></span>

<span data-ttu-id="b06ee-122">기술적으로 말하면 패키지 작성자는 모든 문자열을 접미사로 사용 하 여 시험판 버전을 나타낼 수 있습니다. NuGet은 이러한 버전을 시험판으로 처리 하 고 다른 해석을 수행 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="b06ee-123">즉, NuGet은 관련 된 모든 UI에서 전체 버전 문자열을 표시 하 여 접미사의 의미를 소비자로 해석 합니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="b06ee-124">즉, 패키지 개발자는 일반적으로 인식 되는 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="b06ee-125">`-alpha`: 일반적으로 진행 중인 작업 및 실험에 사용 되는 알파 릴리스입니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="b06ee-126">`-beta`: 일반적으로 다음에 계획된 릴리스에 대한 기능 완료인 베타 릴리스이지만 알려진 버그를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="b06ee-127">`-rc`: 일반적으로 심각한 버그가 발생하지 않는 한 잠재적으로 최종적(안정적)인 릴리스인 릴리스 후보입니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="b06ee-128">NuGet 4.3.0 +는 *1.0.1*에서와 같이 점 표기법이 포함 된 시험판 번호를 지 원하는 [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html)를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="b06ee-129">NuGet 4.3.0 이전 버전에서는 점 표기법이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="b06ee-130">*1.0.1-build23*와 같은 양식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="b06ee-131">패키지 참조를 확인 하는 경우 접미사를 사용 하는 경우에만 다른 패키지 버전을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="b06ee-132">예를 들어 다음 버전은 표시 된 순서 대로 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="b06ee-133">의미 체계 버전 관리 2.0.0</span><span class="sxs-lookup"><span data-stu-id="b06ee-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="b06ee-134">NuGet 4.3.0 + 및 Visual Studio 2017 버전 15.3 +에서 NuGet은 [의미 체계 버전 관리 2.0.0](http://semver.org/spec/v2.0.0.html)을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="b06ee-135">SemVer v 2.0.0의 특정 의미 체계가 이전 클라이언트에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="b06ee-136">NuGet은 다음 문 중 하나에 해당 하는 경우 패키지 버전을 SemVer v 2.0.0에 한정 된 것으로 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="b06ee-137">시험판 레이블은 점으로 구분 됩니다 (예: *1.0.0-alpha. 1).*</span><span class="sxs-lookup"><span data-stu-id="b06ee-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="b06ee-138">버전에는 *1.0.0 + githash* 와 같은 빌드 메타 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="b06ee-139">Nuget.org의 경우 패키지는 다음 문 중 하나가 true 인 경우 SemVer v 2.0.0 패키지로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="b06ee-140">패키지의 자체 버전은 위에서 정의한 대로 SemVer v 2.0.0 규격 이지만 SemVer v 1.0.0은 호환 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="b06ee-141">패키지의 모든 종속성 버전 범위에는 위에서 정의 된 SemVer v 2.0.0 규격 이지만 SemVer v 1.0.0 규격이 아닌 최소 또는 최대 버전이 있습니다. 예를 들면 *[1.0.0-alpha. 1,)* 입니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="b06ee-142">SemVer v 2.0.0 관련 패키지를 nuget.org에 업로드 하는 경우 패키지는 이전 클라이언트에 표시 되지 않으며 다음 NuGet 클라이언트 에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="b06ee-143">NuGet 4.3.0 +</span><span class="sxs-lookup"><span data-stu-id="b06ee-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="b06ee-144">Visual Studio 2017 버전 15.3 이상</span><span class="sxs-lookup"><span data-stu-id="b06ee-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="b06ee-145">[NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix) 를 사용 하는 Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="b06ee-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="b06ee-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="b06ee-146">dotnet</span></span>
  - <span data-ttu-id="b06ee-147">dotnetcore (.NET SDK 2.0.0 +)</span><span class="sxs-lookup"><span data-stu-id="b06ee-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="b06ee-148">타사 클라이언트:</span><span class="sxs-lookup"><span data-stu-id="b06ee-148">Third-party clients:</span></span>

- <span data-ttu-id="b06ee-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="b06ee-149">JetBrains Rider</span></span>
- <span data-ttu-id="b06ee-150">Paket 버전 5.0 이상</span><span class="sxs-lookup"><span data-stu-id="b06ee-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="b06ee-151">버전 범위 및 와일드 카드</span><span class="sxs-lookup"><span data-stu-id="b06ee-151">Version ranges and wildcards</span></span>

<span data-ttu-id="b06ee-152">패키지 종속성을 참조할 때 NuGet은 다음과 같이 요약 된 버전 범위를 지정 하기 위한 간격 표기법 사용을 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="b06ee-153">Notation</span><span class="sxs-lookup"><span data-stu-id="b06ee-153">Notation</span></span> | <span data-ttu-id="b06ee-154">적용 된 규칙</span><span class="sxs-lookup"><span data-stu-id="b06ee-154">Applied rule</span></span> | <span data-ttu-id="b06ee-155">Description</span><span class="sxs-lookup"><span data-stu-id="b06ee-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="b06ee-156">1.0</span><span class="sxs-lookup"><span data-stu-id="b06ee-156">1.0</span></span> | <span data-ttu-id="b06ee-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="b06ee-157">x ≥ 1.0</span></span> | <span data-ttu-id="b06ee-158">최소 버전 (포함)</span><span class="sxs-lookup"><span data-stu-id="b06ee-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="b06ee-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="b06ee-159">(1.0,)</span></span> | <span data-ttu-id="b06ee-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="b06ee-160">x > 1.0</span></span> | <span data-ttu-id="b06ee-161">최소 버전, 제외</span><span class="sxs-lookup"><span data-stu-id="b06ee-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="b06ee-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="b06ee-162">[1.0]</span></span> | <span data-ttu-id="b06ee-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="b06ee-163">x == 1.0</span></span> | <span data-ttu-id="b06ee-164">정확한 버전 일치</span><span class="sxs-lookup"><span data-stu-id="b06ee-164">Exact version match</span></span> |
| <span data-ttu-id="b06ee-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="b06ee-165">(,1.0]</span></span> | <span data-ttu-id="b06ee-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="b06ee-166">x ≤ 1.0</span></span> | <span data-ttu-id="b06ee-167">최대 버전 (포함)</span><span class="sxs-lookup"><span data-stu-id="b06ee-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="b06ee-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="b06ee-168">(,1.0)</span></span> | <span data-ttu-id="b06ee-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="b06ee-169">x < 1.0</span></span> | <span data-ttu-id="b06ee-170">최대 버전, 제외</span><span class="sxs-lookup"><span data-stu-id="b06ee-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="b06ee-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="b06ee-171">[1.0,2.0]</span></span> | <span data-ttu-id="b06ee-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="b06ee-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="b06ee-173">정확한 범위 (포함)</span><span class="sxs-lookup"><span data-stu-id="b06ee-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="b06ee-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="b06ee-174">(1.0,2.0)</span></span> | <span data-ttu-id="b06ee-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="b06ee-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="b06ee-176">정확한 범위, 제외</span><span class="sxs-lookup"><span data-stu-id="b06ee-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="b06ee-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="b06ee-177">[1.0,2.0)</span></span> | <span data-ttu-id="b06ee-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="b06ee-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="b06ee-179">혼합 최소값 및 배타 최대 버전</span><span class="sxs-lookup"><span data-stu-id="b06ee-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="b06ee-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="b06ee-180">(1.0)</span></span>    | <span data-ttu-id="b06ee-181">잘못된</span><span class="sxs-lookup"><span data-stu-id="b06ee-181">invalid</span></span> | <span data-ttu-id="b06ee-182">잘못된</span><span class="sxs-lookup"><span data-stu-id="b06ee-182">invalid</span></span> |

<span data-ttu-id="b06ee-183">PackageReference 형식을 사용 하는 경우 NuGet은 숫자의 주, 부, \*패치 및 시험판 접미사 부분에 와일드 카드 표기법을 사용 하도록 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="b06ee-184">와일드 카드는 형식에서 `packages.config` 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="b06ee-185">PackageReference의 버전 범위에는 시험판 버전이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="b06ee-186">기본적으로 부동 버전은 옵트인 (opt in) 하지 않는 한 시험판 버전을 확인 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="b06ee-187">관련 기능 요청의 상태는 [6434 문제](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="b06ee-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="b06ee-188">예</span><span class="sxs-lookup"><span data-stu-id="b06ee-188">Examples</span></span>

<span data-ttu-id="b06ee-189">프로젝트 파일, `packages.config` 파일 및 `.nuspec` 파일에서 패키지 종속성의 버전 또는 버전 범위를 항상 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="b06ee-190">버전 또는 버전 범위를 사용 하지 않으면 NuGet 2.8. x 및 이전 버전은 종속성을 확인할 때 사용 가능한 최신 패키지 버전을 선택 하는 반면, NuGet 3.x 이상에서는 가장 낮은 패키지 버전을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="b06ee-191">버전 또는 버전 범위를 지정 하면 이러한 불확실성이 방지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="b06ee-192">프로젝트 파일의 참조 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="b06ee-192">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="b06ee-193">**의 `packages.config`참조:**</span><span class="sxs-lookup"><span data-stu-id="b06ee-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="b06ee-194">에서 `packages.config`모든 종속성은 패키지를 복원할 때 사용 `version` 되는 정확한 특성으로 나열 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="b06ee-195">`allowedVersions` 특성은 업데이트 작업을 수행 하는 동안에만 패키지를 업데이트할 수 있는 버전을 제한 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="b06ee-196">**파일의 `.nuspec` 참조**</span><span class="sxs-lookup"><span data-stu-id="b06ee-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="b06ee-197">요소의`<dependency>` 특성은 `version` 종속성에 허용 되는 범위 버전을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="b06ee-198">정규화 된 버전 번호</span><span class="sxs-lookup"><span data-stu-id="b06ee-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="b06ee-199">이는 NuGet 3.4 이상에 대 한 주요 변경 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="b06ee-200">설치, 다시 설치 또는 복원 작업 중에 리포지토리에서 패키지를 가져올 때 NuGet 3.4 +는 버전 번호를 다음과 같이 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="b06ee-201">버전 번호에서 앞에 오는 0이 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="b06ee-202">버전 번호의 네 번째 부분에서 0이 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="b06ee-203">`pack`및 `restore` 작업은 가능한 경우 버전을 정규화 합니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-203">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="b06ee-204">이미 빌드된 패키지의 경우에는이 정규화가 패키지 자체의 버전 번호에 영향을 주지 않습니다. 종속성을 확인할 때 NuGet이 버전과 일치 하는 방식에만 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-204">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="b06ee-205">그러나 NuGet 패키지 리포지토리는 패키지 버전 복제를 방지 하기 위해 NuGet과 동일한 방식으로 이러한 값을 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="b06ee-206">따라서 패키지의 버전 *1.0* 을 포함 하는 리포지토리는 버전 *1.0.0* 을 별도의 다른 패키지로 호스트 해서는 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b06ee-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
