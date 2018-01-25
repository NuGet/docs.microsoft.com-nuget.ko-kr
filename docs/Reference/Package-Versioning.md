---
title: "NuGet 패키지 버전 참조 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "버전 번호와 NuGet 패키지에 따라 달라 지는 및 종속성 설치 되는 방식과에 다른 패키지에 대 한 범위를 지정 하는 정확한 세부 정보입니다."
keywords: "버전 관리, NuGet 패키지 종속 파일, NuGet 종속성 버전, NuGet 버전 번호, NuGet 패키지 버전, 버전 범위, 버전 사양, 정규화 된 버전 번호"
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.openlocfilehash: 70472d7d97d073009237a047e0fdf528b221dfd0
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="package-versioning"></a><span data-ttu-id="de039-104">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="de039-104">Package versioning</span></span>

<span data-ttu-id="de039-105">특정 패키지의 패키지 식별자 및 정확한 버전 번호를 사용 하 여 항상 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-105">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="de039-106">예를 들어 [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org 몇 십 개의 사용할 수 있는 버전에서 사이의 특정 패키지에 *4.1.10311* 버전 *6.1.3* (의 안정적인 최신 릴리스)와 같은 다양 한 시험판 버전 *6.2.0-beta1*합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-106">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="de039-107">패키지를 만들 때 선택적 시험판 텍스트 접미사와 함께 특정 버전 번호를 할당 합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-107">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="de039-108">패키지를 사용할 때는 반면에 지정할 수 있습니다는 정확한 버전 번호 또는 다양 한 허용 가능한 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="de039-108">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="de039-109">항목 내용:</span><span class="sxs-lookup"><span data-stu-id="de039-109">In this topic:</span></span>

- <span data-ttu-id="de039-110">[버전의 기초](#version-basics) 시험판 접미사를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-110">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="de039-111">버전 범위 및 와일드 카드</span><span class="sxs-lookup"><span data-stu-id="de039-111">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="de039-112">정규화 된 버전 번호</span><span class="sxs-lookup"><span data-stu-id="de039-112">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="de039-113">버전의 기본 사항</span><span class="sxs-lookup"><span data-stu-id="de039-113">Version basics</span></span>

<span data-ttu-id="de039-114">특정 버전 번호는 형태로 *Major.Minor.Patch [-접미사]*, 여기서 구성 요소는 다음과 같은 의미가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de039-114">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="de039-115">*주요*: 주요 변경 내용</span><span class="sxs-lookup"><span data-stu-id="de039-115">*Major*: Breaking changes</span></span>
- <span data-ttu-id="de039-116">*사소한*: 이전 버전과 호환 되지만 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="de039-116">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="de039-117">*패치*: 이전 버전과 호환 버그 수정</span><span class="sxs-lookup"><span data-stu-id="de039-117">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="de039-118">*-접미사* (선택 사항): 하이픈 다음 시험판 버전을 나타내는 문자열 (다음에서 [의미 체계 버전 관리 또는 SemVer 1.0 규칙](http://semver.org/spec/v1.0.0.html)).</span><span class="sxs-lookup"><span data-stu-id="de039-118">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="de039-119">**예제:**</span><span class="sxs-lookup"><span data-stu-id="de039-119">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="de039-120">nuget.org 거부 된 정확한 버전 번호가 없는 모든 패키지를 업로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-120">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="de039-121">에 버전을 지정 해야 합니다는 `.nuspec` 또는 패키지를 만드는 데 사용 되는 프로젝트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="de039-121">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="de039-122">시험판 버전</span><span class="sxs-lookup"><span data-stu-id="de039-122">Pre-release versions</span></span>

<span data-ttu-id="de039-123">기술적으로 설명 하자면 패키지 작성자가 사용할 수 모든 문자열 접미사로 NuGet 시험판으로 이러한 버전을 처리 하 고 다른 해석 하지 않고는 시험판 버전을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="de039-123">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="de039-124">즉, 모든 UI에서 전체 버전 문자열 NuGet 표시 포함 된 소비자로 접미사의 의미에 대 한 모든 해석은 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="de039-124">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="de039-125">즉, 패키지 개발자가 일반적으로 인식 된 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="de039-125">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="de039-126">`-alpha`: 알파 버전에서는 일반적으로 작업 중인 및 실험에 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-126">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="de039-127">`-beta`: 일반적으로 다음에 계획된 릴리스에 대한 기능 완료인 베타 릴리스이지만 알려진 버그를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="de039-127">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="de039-128">`-rc`: 일반적으로 심각한 버그가 발생하지 않는 한 잠재적으로 최종적(안정적)인 릴리스인 릴리스 후보입니다.</span><span class="sxs-lookup"><span data-stu-id="de039-128">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="de039-129">NuGet 4.3.0+ 지원 [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html)에서 같이 점 표기법을 포함 하는 시험판 숫자 지 원하는 *1.0.1-build.23*합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-129">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="de039-130">점 표기법 4.3.0 이전 버전의 NuGet 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de039-130">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="de039-131">과 같은 폼을 사용할 수 있습니다 *1.0.1-build23*합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-131">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="de039-132">접미사에 의해서만 달라 패키지 참조 및 여러 패키지 버전을 확인할 때 NuGet 접미사가 없는 버전을 먼저 선택 후 시험판 버전에 내림차순 우선 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de039-132">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="de039-133">예를 들어 다음 버전이 표시 된 정확한 순서에서 선택:</span><span class="sxs-lookup"><span data-stu-id="de039-133">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="de039-134">의미 체계 버전 관리 2.0.0</span><span class="sxs-lookup"><span data-stu-id="de039-134">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="de039-135">NuGet 지원 NuGet 4.3.0+와 Visual Studio 2017 버전 15.3 + [의미 체계 버전 관리 2.0.0](http://semver.org/spec/v2.0.0.html)합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-135">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="de039-136">SemVer v2.0.0의 특정 의미 체계는 이전 버전의 클라이언트에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de039-136">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="de039-137">NuGet은 패키지 버전 다음 문 중 하나에 해당 하는 경우 특정 SemVer v2.0.0을 고려 합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-137">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="de039-138">시험판 레이블은 점으로 구분 된 예를 들어 *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="de039-138">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="de039-139">버전에 빌드-메타 데이터가, 예를 들어 *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="de039-139">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="de039-140">다음 문 중 하나에 해당 하는 경우 nuget.org를 패키지 SemVer v2.0.0 패키지로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de039-140">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="de039-141">패키지의 버전이 앞에서 정의한 대로 SemVer v2.0.0 규정을 준수 하지만, SemVer v1.0.0 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de039-141">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="de039-142">패키지의 종속성 버전 범위에; 위에 정의 된 SemVer v2.0.0 규정을 준수 하지만 SemVer v1.0.0 하지 호환 되지 않는 최소 또는 최대 버전 예를 들어 *[1.0.0-alpha.1,)*합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-142">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="de039-143">Nuget.org를 SemVer v2.0.0 관련 패키지를 업로드 하는 경우 패키지 되며 이전 버전의 클라이언트로 테스트를 수행할 수는 다음과 같은 NuGet 클라이언트에만:</span><span class="sxs-lookup"><span data-stu-id="de039-143">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="de039-144">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="de039-144">NuGet 4.3.0+</span></span>
- <span data-ttu-id="de039-145">Visual Studio 2017 버전 15.3 +</span><span class="sxs-lookup"><span data-stu-id="de039-145">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="de039-146">Visual Studio 2015 [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="de039-146">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="de039-147">dotnet.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="de039-147">dotnet.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="de039-148">제 3 자 클라이언트:</span><span class="sxs-lookup"><span data-stu-id="de039-148">Third-party clients:</span></span>

- <span data-ttu-id="de039-149">JetBrains 기</span><span class="sxs-lookup"><span data-stu-id="de039-149">JetBrains Rider</span></span>
- <span data-ttu-id="de039-150">Paket 버전 5.0 이상</span><span class="sxs-lookup"><span data-stu-id="de039-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="de039-151">버전 범위 및 와일드 카드</span><span class="sxs-lookup"><span data-stu-id="de039-151">Version ranges and wildcards</span></span>

<span data-ttu-id="de039-152">패키지 종속 파일을 참조할 때 NuGet 버전 범위, 다음과 같이 요약할 수를 지정 하기 위한 간격 표기법을 사용 하 여 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="de039-153">Notation</span><span class="sxs-lookup"><span data-stu-id="de039-153">Notation</span></span> | <span data-ttu-id="de039-154">적용 된 규칙</span><span class="sxs-lookup"><span data-stu-id="de039-154">Applied rule</span></span> | <span data-ttu-id="de039-155">설명</span><span class="sxs-lookup"><span data-stu-id="de039-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="de039-156">1.0</span><span class="sxs-lookup"><span data-stu-id="de039-156">1.0</span></span> | <span data-ttu-id="de039-157">1.0 ≤ x</span><span class="sxs-lookup"><span data-stu-id="de039-157">1.0 ≤ x</span></span> | <span data-ttu-id="de039-158">최소 버전 (포함)</span><span class="sxs-lookup"><span data-stu-id="de039-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="de039-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="de039-159">(1.0,)</span></span> | <span data-ttu-id="de039-160">1.0 < x</span><span class="sxs-lookup"><span data-stu-id="de039-160">1.0 < x</span></span> | <span data-ttu-id="de039-161">단독 최소 버전</span><span class="sxs-lookup"><span data-stu-id="de039-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="de039-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="de039-162">[1.0]</span></span> | <span data-ttu-id="de039-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="de039-163">x == 1.0</span></span> | <span data-ttu-id="de039-164">일치 하는 정확한 버전</span><span class="sxs-lookup"><span data-stu-id="de039-164">Exact version match</span></span> |
| <span data-ttu-id="de039-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="de039-165">(,1.0]</span></span> | <span data-ttu-id="de039-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="de039-166">x ≤ 1.0</span></span> | <span data-ttu-id="de039-167">최대 버전 (포함)</span><span class="sxs-lookup"><span data-stu-id="de039-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="de039-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="de039-168">(,1.0)</span></span> | <span data-ttu-id="de039-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="de039-169">x < 1.0</span></span> | <span data-ttu-id="de039-170">단독 최대 버전</span><span class="sxs-lookup"><span data-stu-id="de039-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="de039-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="de039-171">[1.0,2.0]</span></span> | <span data-ttu-id="de039-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="de039-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="de039-173">정확한 범위 (포함)</span><span class="sxs-lookup"><span data-stu-id="de039-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="de039-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="de039-174">(1.0,2.0)</span></span> | <span data-ttu-id="de039-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="de039-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="de039-176">단독 정확한 범위</span><span class="sxs-lookup"><span data-stu-id="de039-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="de039-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="de039-177">[1.0,2.0)</span></span> | <span data-ttu-id="de039-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="de039-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="de039-179">혼합된 포괄 및 전용 시간 최소 최대 버전</span><span class="sxs-lookup"><span data-stu-id="de039-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="de039-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="de039-180">(1.0)</span></span>    | <span data-ttu-id="de039-181">잘못된</span><span class="sxs-lookup"><span data-stu-id="de039-181">invalid</span></span> | <span data-ttu-id="de039-182">잘못된</span><span class="sxs-lookup"><span data-stu-id="de039-182">invalid</span></span> |

<span data-ttu-id="de039-183">PackageReference 형식을 사용 하는 경우 NuGet에서는 와일드 카드 표기법을 사용 하 여 \*, 주, 부, Patch 및 수의 시험판 접미사 부분에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="de039-184">와일드 카드는 지원 되지 않습니다는 `packages.config` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="de039-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="de039-185">버전 범위를 확인 하는 동안에 시험판 버전 포함 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de039-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="de039-186">시험판 버전 *는* 포함 와일드 카드를 사용 하는 경우 (\*).</span><span class="sxs-lookup"><span data-stu-id="de039-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="de039-187">버전 범위 *[1.0,2.0]*, 예를 들어을 다루지 않습니다 2.0 베타 하지만 와일드 카드 표기법은 _2.0-\*_ 않습니다.</span><span class="sxs-lookup"><span data-stu-id="de039-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-\*_ does.</span></span> <span data-ttu-id="de039-188">참조 [912 발급](https://github.com/NuGet/Home/issues/912) 추가 대 한 설명은 시험판 와일드 카드입니다.</span><span class="sxs-lookup"><span data-stu-id="de039-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="de039-189">예제</span><span class="sxs-lookup"><span data-stu-id="de039-189">Examples</span></span>

<span data-ttu-id="de039-190">프로젝트 파일에 버전 또는 버전 범위 패키지 종속성에 대 한 작업을 항상 지정 `packages.config` 파일 및 `.nuspec` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="de039-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="de039-191">버전 또는 버전 범위, NuGet 없이 2.8.x 이전를 선택 하 고 최신 사용 가능한 패키지 버전 한 종속성을 확인할 때 반면 NuGet 3.x 나중에 가장 낮은 패키지 버전을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="de039-192">버전 또는 버전 범위 방지이 불확실 한이 정보를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="de039-193">프로젝트 파일 (PackageReference)에 대 한 참조</span><span class="sxs-lookup"><span data-stu-id="de039-193">References in project files (PackageReference)</span></span>

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

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="de039-194">**참조 `packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="de039-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="de039-195">`packages.config`, 모든 종속성이 정확한 함께 나열 `version` 패키지를 복원할 때 사용 되는 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="de039-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="de039-196">`allowedVersions` 특성은 패키지가 업데이트 될 수 있습니다는 버전을 제한 하려면 업데이트 작업 중에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de039-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="de039-197">**참조 `.nuspec` 파일**</span><span class="sxs-lookup"><span data-stu-id="de039-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="de039-198">`version` 특성에 `<dependency>` 요소 종속성에 대해 허용 가능한 범위 버전을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="de039-199">정규화 된 버전 번호</span><span class="sxs-lookup"><span data-stu-id="de039-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="de039-200">주요 변경 내용 NuGet 3.4 이상입니다.</span><span class="sxs-lookup"><span data-stu-id="de039-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="de039-201">다시 설치 또는 복원 작업을 설치 하는 동안 저장소에서 패키지를 가져올 때 NuGet 3.4 + 다음과 같이 버전 번호를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="de039-202">앞에 오는 0은 버전 번호에서 제거 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de039-202">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="de039-203">버전 번호의 네 번째 부분에서 0은 생략 됩니다.</span><span class="sxs-lookup"><span data-stu-id="de039-203">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="de039-204">이 정규화 자체; 패키지에 버전 번호에는 영향을 주지 만 NuGet 일치 방법을 버전 종속성을 확인할 때 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="de039-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="de039-205">그러나 NuGet 패키지 저장소에는 NuGet 패키지 버전 복제 방지 하기 위해 이러한 값을 처리 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="de039-206">버전을 포함 하는 리포지토리의 따라서 *1.0* 패키지도 호스팅해서는 안 버전 *1.0.0* 개별적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="de039-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
