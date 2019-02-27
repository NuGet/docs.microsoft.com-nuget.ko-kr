---
title: NuGet 패키지 버전 참조
description: 버전 번호 및 NuGet 패키지에 따라 달라 지는 및 종속성 설치 방식에 따라 다른 패키지에 대 한 범위를 지정 하는 정확한 세부 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 6407cd2ea5e5e7a9c9e2be679764a8a0d5dd9260
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852470"
---
# <a name="package-versioning"></a><span data-ttu-id="3050b-103">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="3050b-103">Package versioning</span></span>

<span data-ttu-id="3050b-104">특정 패키지의 패키지 식별자 및 정확한 버전 번호를 사용 하 여 항상 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="3050b-105">예를 들어 [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org에 여러 수십 버전에서까지 사용할 수 있는 특정 패키지 *4.1.10311* 버전 *6.1.3* (의 안정적인 최신 릴리스) 및 다양 한 시험판 *6.2.0-beta1*합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="3050b-106">패키지를 만들 때 선택적 시험판 텍스트 접미사를 사용 하 여 특정 버전 번호를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="3050b-107">패키지를 사용할 때는 다른 한편으로 지정할 수 있습니다 정확한 버전 번호 또는 다양 한 허용 가능한 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="3050b-108">항목 내용:</span><span class="sxs-lookup"><span data-stu-id="3050b-108">In this topic:</span></span>

- <span data-ttu-id="3050b-109">[버전의 기본 사항](#version-basics) 시험판 접미사를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="3050b-110">버전 범위 및 와일드 카드</span><span class="sxs-lookup"><span data-stu-id="3050b-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="3050b-111">정규화 된 버전 번호</span><span class="sxs-lookup"><span data-stu-id="3050b-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="3050b-112">버전의 기본 사항</span><span class="sxs-lookup"><span data-stu-id="3050b-112">Version basics</span></span>

<span data-ttu-id="3050b-113">특정 버전 번호는 형태로 *Major.Minor.Patch [-접미사]* 여기서 구성 요소는 다음과 같은 의미가,:</span><span class="sxs-lookup"><span data-stu-id="3050b-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="3050b-114">*주요*: 호환성이 손상되는 변경</span><span class="sxs-lookup"><span data-stu-id="3050b-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="3050b-115">*사소한*: 이전 버전과 호환되는 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="3050b-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="3050b-116">*패치*: 이전 버전과 호환되는 버그 수정에만 해당</span><span class="sxs-lookup"><span data-stu-id="3050b-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="3050b-117">*-접미사* (선택 사항): 시험판 버전을 나타내는 문자열 뒤에 하이픈 (다음 합니다 [유의 적 버전 또는 SemVer 1.0 규칙](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="3050b-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="3050b-118">**예:**</span><span class="sxs-lookup"><span data-stu-id="3050b-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="3050b-119">nuget.org 정확한 버전 번호를 없는 모든 패키지 업로드를 거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="3050b-120">버전을 지정 해야 합니다 `.nuspec` 또는 패키지를 만드는 데 사용 되는 프로젝트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="3050b-121">시험판 버전</span><span class="sxs-lookup"><span data-stu-id="3050b-121">Pre-release versions</span></span>

<span data-ttu-id="3050b-122">엄밀히 말해, 패키지 작성자 문자열 접미사로 하 여 NuGet 시험판으로 이러한 버전을 처리 하 고 다른 해석 하지 않고 사용 하면 시험판 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="3050b-123">즉, NuGet 표시 무엇이 든 UI의 전체 버전 문자열 포함 된 접미사의 의미에 대 한 모든 해석은 소비자를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="3050b-124">즉, 패키지 개발자는 일반적으로 인식 된 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="3050b-125">`-alpha`: 알파 버전에서는 일반적으로 작업 중인 및 실험에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="3050b-126">`-beta`: 일반적으로 다음에 계획된 릴리스에 대한 기능 완료인 베타 릴리스이지만 알려진 버그를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="3050b-127">`-rc`: 일반적으로 심각한 버그가 발생하지 않는 한 잠재적으로 최종적(안정적)인 릴리스인 릴리스 후보입니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="3050b-128">NuGet 4.3.0 [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html)에서 같이 점 표기법을 사용 하는 시험판 번호를 지 *1.0.1-build.23*합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="3050b-129">NuGet 4.3.0 이전 버전에서는 점 표기법이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="3050b-130">과 같은 양식을 사용할 수 있습니다 *1.0.1-build23*합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="3050b-131">패키지 참조 및 여러 패키지 버전 접미사만 다를 해결 하는 경우 NuGet 접미사가 없는 버전을 먼저 선택 다음 역방향 사전순의 시험판 버전 우선 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="3050b-132">예를 들어, 다음 버전이 정확한 순서 대로 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="3050b-133">유의 적 버전 2.0.0</span><span class="sxs-lookup"><span data-stu-id="3050b-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="3050b-134">NuGet 4.3.0와 Visual Studio 2017 버전 15.3 이상 NuGet 지원 [유의 적 버전 2.0.0](http://semver.org/spec/v2.0.0.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="3050b-135">SemVer v2.0.0의 특정 의미 체계는 이전 버전의 클라이언트에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="3050b-136">NuGet은 패키지 버전을 다음 문 중 하나에 해당 하는 경우 특정 SemVer v2.0.0으로 간주 합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="3050b-137">시험판 레이블이 점으로 구분 예를 들어 *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="3050b-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="3050b-138">버전에 빌드 메타 데이터, 예를 들어 *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="3050b-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="3050b-139">Nuget.org의 패키지는 다음 문 중 하나에 해당 하는 경우 SemVer v2.0.0 패키지로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="3050b-140">패키지의 버전 위에 정의 된 SemVer v2.0.0 규정을 준수 하지만 SemVer v1.0.0 없습니다 규격입니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="3050b-141">패키지의 종속성 버전 범위에; 위에 정의 된 SemVer v2.0.0 규정을 준수 하지만 SemVer v1.0.0 없습니다 호환 되는 최소 또는 최대 버전 예를 들어 *[1.0.0-alpha.1,)* 합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="3050b-142">SemVer v2.0.0 특정 패키지를 nuget.org에 업로드 하는 경우에 패키지를 이전 버전의 클라이언트에 표시 되지 않도록 되어 다음 NuGet 클라이언트 에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="3050b-143">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="3050b-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="3050b-144">Visual Studio 2017 버전 15.3 이상</span><span class="sxs-lookup"><span data-stu-id="3050b-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="3050b-145">Visual Studio 2015 [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="3050b-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="3050b-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="3050b-146">dotnet</span></span>
  - <span data-ttu-id="3050b-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="3050b-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="3050b-148">타사 클라이언트:</span><span class="sxs-lookup"><span data-stu-id="3050b-148">Third-party clients:</span></span>

- <span data-ttu-id="3050b-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="3050b-149">JetBrains Rider</span></span>
- <span data-ttu-id="3050b-150">Paket 버전 5.0 이상</span><span class="sxs-lookup"><span data-stu-id="3050b-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="3050b-151">버전 범위 및 와일드 카드</span><span class="sxs-lookup"><span data-stu-id="3050b-151">Version ranges and wildcards</span></span>

<span data-ttu-id="3050b-152">패키지 종속성을 참조할 때 간격 표기법을 사용 하 여 버전 범위를 다음과 같이 요약할 수를 지정 하는 것에 대 한 NuGet 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="3050b-153">Notation</span><span class="sxs-lookup"><span data-stu-id="3050b-153">Notation</span></span> | <span data-ttu-id="3050b-154">적용 된 규칙</span><span class="sxs-lookup"><span data-stu-id="3050b-154">Applied rule</span></span> | <span data-ttu-id="3050b-155">설명</span><span class="sxs-lookup"><span data-stu-id="3050b-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="3050b-156">1.0</span><span class="sxs-lookup"><span data-stu-id="3050b-156">1.0</span></span> | <span data-ttu-id="3050b-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="3050b-157">x ≥ 1.0</span></span> | <span data-ttu-id="3050b-158">최소 버전을 포함</span><span class="sxs-lookup"><span data-stu-id="3050b-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="3050b-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="3050b-159">(1.0,)</span></span> | <span data-ttu-id="3050b-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="3050b-160">x > 1.0</span></span> | <span data-ttu-id="3050b-161">최소 버전을 제외</span><span class="sxs-lookup"><span data-stu-id="3050b-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="3050b-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="3050b-162">[1.0]</span></span> | <span data-ttu-id="3050b-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="3050b-163">x == 1.0</span></span> | <span data-ttu-id="3050b-164">정확한 버전 일치</span><span class="sxs-lookup"><span data-stu-id="3050b-164">Exact version match</span></span> |
| <span data-ttu-id="3050b-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="3050b-165">(,1.0]</span></span> | <span data-ttu-id="3050b-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="3050b-166">x ≤ 1.0</span></span> | <span data-ttu-id="3050b-167">최대 버전 포함</span><span class="sxs-lookup"><span data-stu-id="3050b-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="3050b-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="3050b-168">(,1.0)</span></span> | <span data-ttu-id="3050b-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="3050b-169">x < 1.0</span></span> | <span data-ttu-id="3050b-170">단독 최대 버전</span><span class="sxs-lookup"><span data-stu-id="3050b-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="3050b-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="3050b-171">[1.0,2.0]</span></span> | <span data-ttu-id="3050b-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="3050b-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="3050b-173">정확한 범위 포함</span><span class="sxs-lookup"><span data-stu-id="3050b-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="3050b-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="3050b-174">(1.0,2.0)</span></span> | <span data-ttu-id="3050b-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="3050b-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="3050b-176">정확한 범위, 배타적</span><span class="sxs-lookup"><span data-stu-id="3050b-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="3050b-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="3050b-177">[1.0,2.0)</span></span> | <span data-ttu-id="3050b-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="3050b-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="3050b-179">혼합된 포괄 최소값과 단독 최대 버전</span><span class="sxs-lookup"><span data-stu-id="3050b-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="3050b-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="3050b-180">(1.0)</span></span>    | <span data-ttu-id="3050b-181">잘못된</span><span class="sxs-lookup"><span data-stu-id="3050b-181">invalid</span></span> | <span data-ttu-id="3050b-182">잘못된</span><span class="sxs-lookup"><span data-stu-id="3050b-182">invalid</span></span> |

<span data-ttu-id="3050b-183">PackageReference 형식을 사용 하는 경우 NuGet에서는 와일드 카드 표기법을 사용 하 여 \*, 주, 부, 패치 및 시험판 접미사 부분 개수에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="3050b-184">와일드 카드는 지원 되지 않습니다는 `packages.config` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="3050b-185">버전 범위를 확인할 때 시험판 버전 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="3050b-186">시험판 버전 *됩니다* 와일드 카드를 사용 하는 경우를 포함 (\*).</span><span class="sxs-lookup"><span data-stu-id="3050b-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="3050b-187">버전 범위 *[1.0,2.0]*, 예를 들어 없는 2.0-beta, 하지만 와일드 카드 표기법 _2.0-\*_ 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-\*_ does.</span></span> <span data-ttu-id="3050b-188">참조 [912 발급](https://github.com/NuGet/Home/issues/912) 시험판 와일드 카드에 대 한 자세한 논의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="3050b-189">예제</span><span class="sxs-lookup"><span data-stu-id="3050b-189">Examples</span></span>

<span data-ttu-id="3050b-190">항상 프로젝트 파일의 버전이 나 패키지 종속성에 대 한 버전 범위를 지정 `packages.config` 파일 및 `.nuspec` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="3050b-191">버전 또는 버전 범위, NuGet 없이 2.8.x 이전를 선택 하 고 최신 사용 가능한 패키지 종속성을 확인할 때 반면 NuGet 3.x 이상 가장 낮은 패키지 버전을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="3050b-192">버전 또는 버전 범위 방지이 불확실성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="3050b-193">프로젝트 파일 (PackageReference)의 참조</span><span class="sxs-lookup"><span data-stu-id="3050b-193">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="3050b-194">**참조 `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="3050b-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="3050b-195">`packages.config`, 모든 종속성이 정확한 함께 나열 `version` 패키지를 복원할 때 사용 되는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="3050b-196">`allowedVersions` 특성은 업데이트 작업 중에 패키지 있습니다 업데이트할 버전을 제한 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="3050b-197">**참조 `.nuspec` 파일**</span><span class="sxs-lookup"><span data-stu-id="3050b-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="3050b-198">합니다 `version` 특성을 `<dependency>` 요소 종속성에 대해 허용 가능한 범위 버전을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="3050b-199">정규화 된 버전 번호</span><span class="sxs-lookup"><span data-stu-id="3050b-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="3050b-200">주요 변경 내용 NuGet 3.4 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="3050b-201">다시 설치 또는 복원 작업을 설치 하는 동안 저장소에서 패키지를 가져올 때 NuGet 3.4 이상 다음과 같은 버전 번호를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="3050b-202">앞에 오는 0은 버전 번호에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-202">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="3050b-203">버전 번호의 네 번째 부분에서 0은 생략할 수는</span><span class="sxs-lookup"><span data-stu-id="3050b-203">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="3050b-204">이 정규화, 패키지의 버전 번호를 영향을 주지 않습니다. 만 NuGet 일치 하는 방식을 버전 종속성을 확인할 때 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="3050b-205">그러나 NuGet 패키지 리포지토리에서 패키지 버전 중복을 방지 하기 위해 NuGet으로 동일한 방식으로 이러한 값을 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="3050b-206">따라서 버전을 포함 하는 리포지토리 *1.0* 패키지도 호스팅해서는 안 됩니다 버전 *1.0.0* 별개 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="3050b-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
