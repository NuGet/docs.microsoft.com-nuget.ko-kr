---
title: NuGet 오류 및 경고 참조
description: 경고 및 다양 한 NuGet 작업 도중 NuGet에서 발생 한 오류에 대 한 참조를 완료 합니다.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 748c2746a61886617e2eefe3e6c4a2e2a5b9d4d3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="a0533-103">오류 및 경고</span><span class="sxs-lookup"><span data-stu-id="a0533-103">Errors and warnings</span></span>

<span data-ttu-id="a0533-104">오류 및 경고가이 항목에 설명 된 대로 번호가 매겨집니다 NuGet 4.3.0+ 및 관련 된 문제를 해결할 수 있도록 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-104">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="a0533-105">오류 및 여기에 나열 된 경고에만 사용할 수 있는 [PackageReference 기반](../consume-packages/package-references-in-project-files.md) 프로젝트와 NuGet 4.3.0+ 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-105">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="a0533-106">또한 NuGet를 경고를 표시 하거나 오류를 상승을 MSBuild 속성을 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-106">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="a0533-107">자세한 내용은 참조 [하는 방법: 컴파일러 경고 표시 안 함](/visualstudio/ide/how-to-suppress-compiler-warnings) Visual Studio 설명서에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-107">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="a0533-108">**오류**</span><span class="sxs-lookup"><span data-stu-id="a0533-108">**Errors**</span></span>

| <span data-ttu-id="a0533-109">그룹화</span><span class="sxs-lookup"><span data-stu-id="a0533-109">Group</span></span> | <span data-ttu-id="a0533-110">오류 번호</span><span class="sxs-lookup"><span data-stu-id="a0533-110">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="a0533-111">잘못 된 입력된 오류</span><span class="sxs-lookup"><span data-stu-id="a0533-111">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="a0533-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="a0533-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="a0533-113">패키지 및 프로젝트에 대 한 누락 오류</span><span class="sxs-lookup"><span data-stu-id="a0533-113">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="a0533-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (이전에 NU1607) [NU1108](#nu1108) (이전에 NU1606)</span><span class="sxs-lookup"><span data-stu-id="a0533-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="a0533-115">호환성 오류</span><span class="sxs-lookup"><span data-stu-id="a0533-115">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="a0533-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="a0533-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="a0533-117">**경고**</span><span class="sxs-lookup"><span data-stu-id="a0533-117">**Warnings**</span></span>

| <span data-ttu-id="a0533-118">그룹화</span><span class="sxs-lookup"><span data-stu-id="a0533-118">Group</span></span> | <span data-ttu-id="a0533-119">경고 번호</span><span class="sxs-lookup"><span data-stu-id="a0533-119">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="a0533-120">잘못 된 입력된 경고</span><span class="sxs-lookup"><span data-stu-id="a0533-120">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="a0533-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="a0533-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="a0533-122">예기치 않은 패키지 버전 경고</span><span class="sxs-lookup"><span data-stu-id="a0533-122">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="a0533-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="a0533-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="a0533-124">해결 프로그램이 충돌 경고</span><span class="sxs-lookup"><span data-stu-id="a0533-124">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="a0533-125">NU1608</span><span class="sxs-lookup"><span data-stu-id="a0533-125">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="a0533-126">패키지 대체 (fallback) 경고</span><span class="sxs-lookup"><span data-stu-id="a0533-126">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="a0533-127">NU1701</span><span class="sxs-lookup"><span data-stu-id="a0533-127">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="a0533-128">피드 경고</span><span class="sxs-lookup"><span data-stu-id="a0533-128">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="a0533-129">NU1801</span><span class="sxs-lookup"><span data-stu-id="a0533-129">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="a0533-130">NuGet 내부 오류 및 경고</span><span class="sxs-lookup"><span data-stu-id="a0533-130">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="a0533-131">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="a0533-131">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="a0533-132">서명 된 패키지 (만들기 및 확인)</span><span class="sxs-lookup"><span data-stu-id="a0533-132">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="a0533-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="a0533-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="a0533-134">잘못 된 입력된 오류</span><span class="sxs-lookup"><span data-stu-id="a0533-134">Invalid input errors</span></span>

<span data-ttu-id="a0533-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="a0533-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="a0533-136">NU1001</span><span class="sxs-lookup"><span data-stu-id="a0533-136">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-137">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-137">**Issue**</span></span> | <span data-ttu-id="a0533-138">프로젝트는 하나 이상의 프레임 워크를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-138">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="a0533-139">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-139">**Example message**</span></span> | <span data-ttu-id="a0533-140">*프로젝트 projA c:\tmp\projA.csproj의 대상 프레임 워크를 지정 하지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="a0533-140">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="a0533-141">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-141">**Solution**</span></span> | <span data-ttu-id="a0533-142">추가 `TargetFramework` 또는 `TargetFrameworks` 속성이 지정 된 프로젝트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-142">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="a0533-143">NU1002</span><span class="sxs-lookup"><span data-stu-id="a0533-143">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-144">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-144">**Issue**</span></span> | <span data-ttu-id="a0533-145">일반 키워드와 함께 입력의 조합이 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-145">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="a0533-146">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-146">**Example message**</span></span> | <span data-ttu-id="a0533-147">*'CLEAR' 없습니다 다른 값과 함께에서 사용할 수*</span><span class="sxs-lookup"><span data-stu-id="a0533-147">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="a0533-148">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-148">**Solution**</span></span> | <span data-ttu-id="a0533-149">지우기 단독으로 사용 하 고 다른 모든 입력을 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-149">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="a0533-150">NU1003</span><span class="sxs-lookup"><span data-stu-id="a0533-150">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-151">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-151">**Issue**</span></span> | <span data-ttu-id="a0533-152">`PackageTargetFallback` 및 `AssetTargetFallback` 자산을 선택 하기 위한 다른 동작을 제공 하 고 함께 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-152">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="a0533-153">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-153">**Example message**</span></span> | <span data-ttu-id="a0533-154">*PackageTargetFallback와 AssetTargetFallback는 함께 사용할 수 없습니다. 프로젝트 환경에서 PackageTargetFallback(deprecated) 참조를 제거 합니다.*</span><span class="sxs-lookup"><span data-stu-id="a0533-154">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="a0533-155">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-155">**Solution**</span></span> | <span data-ttu-id="a0533-156">사용 되지 않는 제거 `PackageTargetFallback` 프로젝트에서 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-156">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="a0533-157">패키지 및 프로젝트에 대 한 누락 오류</span><span class="sxs-lookup"><span data-stu-id="a0533-157">Missing package and project errors</span></span>

<span data-ttu-id="a0533-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="a0533-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="a0533-159">NU1100</span><span class="sxs-lookup"><span data-stu-id="a0533-159">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-160">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-160">**Issue**</span></span> | <span data-ttu-id="a0533-161">종속성 그룹 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-161">A dependency group not be resolved.</span></span> <span data-ttu-id="a0533-162">패키지 또는 프로젝트 하지 않은 형식에 대 한 일반적인 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-162">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="a0533-163">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-163">**Example message**</span></span> | <span data-ttu-id="a0533-164">*Net45에 대 한 System.Missing를 확인할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="a0533-164">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="a0533-165">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-165">**Solution**</span></span> | <span data-ttu-id="a0533-166">프로젝트 파일을 열고 해당 종속 항목 목록을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-166">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="a0533-167">각 종속성을 사용 하는 패키지 소스에 있고 패키지는 프로젝트의 대상 프레임 워크를 지원 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-167">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="a0533-168">NU1101</span><span class="sxs-lookup"><span data-stu-id="a0533-168">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-169">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-169">**Issue**</span></span> | <span data-ttu-id="a0533-170">모든 소스에서 패키지를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-170">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="a0533-171">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-171">**Example message**</span></span> | <span data-ttu-id="a0533-172">*System.Missing 패키지를 찾을 수 없습니다. 패키지 원본에이 id를 가진 존재: dotnet 코어, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="a0533-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="a0533-173">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-173">**Solution**</span></span> | <span data-ttu-id="a0533-174">올바른 패키지 식별자와 버전 번호를 사용 하는 확인 하려면 Visual Studio에서 프로젝트의 종속성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-174">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="a0533-175">도 있는지 여부를 확인는 [NuGet 구성이](../consume-packages/Configuring-NuGet-Behavior.md) 패키지 소스를 식별 프로그램 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-175">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="a0533-176">패키지를 사용 하는 경우 [의미 체계 버전 관리 2.0.0](../reference/package-versioning.md#semantic-versioning-200), 피드, v 3을 사용 하 고 있는지 확인 하십시오 `https://api.nuget.org/v3/index.json`에 [NuGet 구성이](../consume-packages/Configuring-NuGet-Behavior.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-176">If you use packages that have [Semantic Versioning 2.0.0](../reference/package-versioning.md#semantic-versioning-200), please make sure that you are using the V3 feed, `https://api.nuget.org/v3/index.json`, in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="a0533-177">NU1102</span><span class="sxs-lookup"><span data-stu-id="a0533-177">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-178">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-178">**Issue**</span></span> | <span data-ttu-id="a0533-179">패키지 식별자를 찾았지만 소스 중 하나에서 지정 된 종속성 범위 내에서 버전을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-179">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="a0533-180">패키지와 사용자가 아니라에서 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-180">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="a0533-181">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-181">**Example message**</span></span> | <span data-ttu-id="a0533-182">*버전으로 NuGet.Versioning 패키지를 찾을 수 없습니다. (> = 9.0.1)<br/> -nuget.org에 30 찾을 버전 [버전 가장 가까운: 4.0.0]<br/> -dotnet buildtools에서 찾은 10 버전 [버전 가장 가까운: 4.0.0-rc-2129]<br/> -9 찾을 수 NuGetVolatile에서 버전 [버전 가장 가까운: 3.0.0-beta-00032]<br/> -0 버전 dotnet 코어 있는<br/> -dotnet roslyn에서 0 버전을 찾을 수*</span><span class="sxs-lookup"><span data-stu-id="a0533-182">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="a0533-183">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-183">**Solution**</span></span> | <span data-ttu-id="a0533-184">패키지 버전을 해결 하려면 프로젝트 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-184">Edit the project file to correct the package version.</span></span> <span data-ttu-id="a0533-185">도 있는지 여부를 확인는 [NuGet 구성이](../consume-packages/Configuring-NuGet-Behavior.md) 패키지 소스를 식별 프로그램 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-185">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="a0533-186">이 패키지는 프로젝트에서 직접 참조 하는 경우 requeted 버전을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-186">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="a0533-187">NU1103</span><span class="sxs-lookup"><span data-stu-id="a0533-187">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-188">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-188">**Issue**</span></span> | <span data-ttu-id="a0533-189">프로젝트 종속성 범위에 대 한 안정적인 버전을 지정 하지만 해당 범위에 안정적 버전을 찾지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-189">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="a0533-190">시험판 버전을 찾았지만 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-190">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="a0533-191">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-191">**Example message**</span></span> | <span data-ttu-id="a0533-192">*버전과 NuGet.Versioning 안정적인 패키지를 찾을 수 없습니다. (> = 3.0.0)<br/> -dotnet buildtools에서 찾은 10 버전 [버전 가장 가까운: 4.0.0-rc-2129]<br/> -NuGetVolatile에서 찾을 9 버전 [버전 가장 가까운: 3.0.0-beta-00032] <br/> -0 버전 dotnet 코어 있는<br/> -dotnet roslyn에서 0 버전을 찾을 수*</span><span class="sxs-lookup"><span data-stu-id="a0533-192">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="a0533-193">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-193">**Solution**</span></span> |  <span data-ttu-id="a0533-194">시험판 버전을 포함 하도록 프로젝트 파일에 버전 범위를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-194">Edit the version range in the project file to include pre-release versions.</span></span> <span data-ttu-id="a0533-195">참조 [패키지 버전 관리](../reference/Package-Versioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-195">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="a0533-196">NU1104</span><span class="sxs-lookup"><span data-stu-id="a0533-196">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-197">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-197">**Issue**</span></span> | <span data-ttu-id="a0533-198">ProjectReference 존재 하지 않는 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-198">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="a0533-199">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-199">**Example message**</span></span> | <span data-ttu-id="a0533-200">*프로젝트 참조 'c:\a.csproj' 존재 하지 않습니다. 프로젝트 참조는 유효 하 고 프로젝트 파일이 있는지 확인 합니다.*</span><span class="sxs-lookup"><span data-stu-id="a0533-200">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="a0533-201">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-201">**Solution**</span></span> | <span data-ttu-id="a0533-202">참조 된 프로젝트의 경로를 수정 하거나 또는 참조를 제거 하려면 프로젝트 파일을 편집 경우 더 이상 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-202">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="a0533-203">NU1105</span><span class="sxs-lookup"><span data-stu-id="a0533-203">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-204">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-204">**Issue**</span></span> | <span data-ttu-id="a0533-205">프로젝트 파일이 있지만에 제공 된 복원 정보가 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-205">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="a0533-206">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-206">**Example message**</span></span> | <span data-ttu-id="a0533-207">*'C:\a.csproj'에 대 한 프로젝트 정보를 읽을 수 없습니다. 프로젝트 파일이 올바르지 않거나 누락 된 대상으로 복원 하는 데 필요한 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="a0533-207">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="a0533-208">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-208">**Solution**</span></span> | <span data-ttu-id="a0533-209">Visual Studio에서 프로젝트가 있는 경우 프로젝트를 다시 로드에 로드 되지 않은 오류 의미할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-209">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="a0533-210">명령줄에서 파일이 손상 되었거나 "가져오기" 호출 후 사용자 지정 포함 되지 않았는지 의미할 수 있습니다이 프로젝트를 읽을 수는 복원에 필요한 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-210">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="a0533-211">프로젝트 파일은 유효한 "가져오기" 호출 후 대상 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-211">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="a0533-212">NU1106</span><span class="sxs-lookup"><span data-stu-id="a0533-212">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-213">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-213">**Issue**</span></span> | <span data-ttu-id="a0533-214">종속성 제약 조건을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-214">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="a0533-215">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-215">**Example message**</span></span> | <span data-ttu-id="a0533-216">*{Id}에 대 한 충돌 하는 요청을 충족할 수 없습니다. {충돌 경로} 프레임 워크: {대상 그래프}*</span><span class="sxs-lookup"><span data-stu-id="a0533-216">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |
| <span data-ttu-id="a0533-217">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-217">**Solution**</span></span> | <span data-ttu-id="a0533-218">정확한 버전 보다는 종속성에 대 한 보다 자유로운 범위를 지정 하려면 프로젝트 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-218">Edit the project file to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="a0533-219">NU1107 (이전에 NU1607)</span><span class="sxs-lookup"><span data-stu-id="a0533-219">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-220">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-220">**Issue**</span></span> | <span data-ttu-id="a0533-221">패키지 간에 종속성 제약 조건을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-221">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="a0533-222">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-222">**Example message**</span></span> | <span data-ttu-id="a0533-223">*NuGet.Versioning에 대 한 검색 버전 충돌 합니다. 이 문제를 해결 하려면 프로젝트에서 직접 패키지를 참조 합니다.<br/>  NuGet.Packaging 3.5.0 NuGet.Versioning (3.5.0 =)-><br/> NuGet.Configuration 4.0.0 NuGet.Versioning (4.0.0 =)->*</span><span class="sxs-lookup"><span data-stu-id="a0533-223">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="a0533-224">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-224">**Solution**</span></span> | <span data-ttu-id="a0533-225">정확한 버전에 대 한 종속성 제약 조건 사용 하 여 패키지에는 다른 패키지 버전을 필요에 따라 증가를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-225">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="a0533-226">필요한 정확한 버전으로 직접 (프로젝트 파일에서) 프로젝트에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-226">Add a reference to the project directly (in the project file) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="a0533-227">NU1108 (이전에 NU1606)</span><span class="sxs-lookup"><span data-stu-id="a0533-227">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-228">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-228">**Issue**</span></span> | <span data-ttu-id="a0533-229">순환 종속성이 발견 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-229">A circular dependency was detected.</span></span> |
| <span data-ttu-id="a0533-230">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-230">**Example message**</span></span> | <span data-ttu-id="a0533-231">*순환 발견: A-B A->*</span><span class="sxs-lookup"><span data-stu-id="a0533-231">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="a0533-232">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-232">**Solution**</span></span> | <span data-ttu-id="a0533-233">패키지를 제대로 작성 버그를 해결 하려면 패키지 소유자에 게 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-233">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="a0533-234">호환성 오류</span><span class="sxs-lookup"><span data-stu-id="a0533-234">Compatibility errors</span></span>

<span data-ttu-id="a0533-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="a0533-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="a0533-236">NU1201</span><span class="sxs-lookup"><span data-stu-id="a0533-236">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-237">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-237">**Issue**</span></span> | <span data-ttu-id="a0533-238">종속성 프로젝트는 현재 프로젝트와 호환 되는 프레임 워크를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-238">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="a0533-239">일반적으로 프로젝트의 대상 프레임 워크는 사용 중인 프로젝트 보다 높은 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-239">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="a0533-240">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-240">**Example message**</span></span> | <span data-ttu-id="a0533-241">*프로젝트 서버 netstandard1.3와 호환 되지 않습니다 (합니다. NETStandard, Version = v1.3). 프로젝트 서버 지원:<br/> -netstandard1.6 (합니다. NETStandard, Version = v1.6)<br/> -netcoreapp1.0 (합니다. NETCoreApp, Version = v1.0)*</span><span class="sxs-lookup"><span data-stu-id="a0533-241">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="a0533-242">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-242">**Solution**</span></span> | <span data-ttu-id="a0533-243">프로젝트의 대상 프레임 워크는 프로젝트가 보다 같거나 낮은 버전으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-243">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="a0533-244">NU1202</span><span class="sxs-lookup"><span data-stu-id="a0533-244">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-245">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-245">**Issue**</span></span> | <span data-ttu-id="a0533-246">종속성 패키지는 프로젝트와 호환 되는 모든 자산을 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-246">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="a0533-247">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-247">**Example message**</span></span> | <span data-ttu-id="a0533-248">*패키지 System.ComponentModel.EventBasedAsync 4.0.11 netstandard1.3와 호환 되지 않습니다 (합니다. NETStandard, Version = v1.3). System.ComponentModel.EventBasedAsync 4.0.11 지원 패키지:<br/> -monoandroid10 (MonoAndroid, 버전 = v1.0)<br/> -monotouch10 (MonoTouch, Version = v1.0)<br/> -net45 (합니다. NETFramework, Version = v4.5)<br/> -netcore50 (합니다. NETCore, Version = v5.0)<br/> -netstandard1.0 (합니다. NETStandard, Version = v1.0)<br/> -portable net45 + win8 + w p 8 + wpa81 (합니다. NETPortable, 버전 = v0.0, 프로필 Profile259 =)<br/> -win8 (Windows, Version = v 8.0)<br/> -w p 8 (WindowsPhone, 버전 v 8.0 =)<br/> -wpa81 (이 WindowsPhoneApp, 버전 = v8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="a0533-248">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="a0533-249">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-249">**Solution**</span></span> | <span data-ttu-id="a0533-250">패키지에서 지 원하는 하나를 프로젝트의 대상 프레임 워크를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-250">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="a0533-251">NU1203</span><span class="sxs-lookup"><span data-stu-id="a0533-251">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-252">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-252">**Issue**</span></span> | <span data-ttu-id="a0533-253">패키지는 프로젝트를 지원 하지 않습니다 `RuntimeIdentifier`합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-253">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="a0533-254">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-254">**Example message**</span></span> | <span data-ttu-id="a0533-255">*System.Example 1.0.0 net461에 a.dll에 대 한 compile-time 참조 어셈블리를 제공 하지만 호환 런타임 어셈블리가 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="a0533-255">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="a0533-256">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-256">**Solution**</span></span> | <span data-ttu-id="a0533-257">변경 된 `RuntimeIdentifier` 필요에 따라 프로젝트에 사용 되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-257">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="a0533-258">NU1401</span><span class="sxs-lookup"><span data-stu-id="a0533-258">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-259">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-259">**Issue**</span></span> | <span data-ttu-id="a0533-260">패키지 기능 또는 현재 설치 된 버전의 NuGet에서 지원 되는 프레임 워크에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-260">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="a0533-261">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-261">**Example message**</span></span> | <span data-ttu-id="a0533-262">*'NuGet.Versioning' 패키지에는 NuGet 클라이언트 버전 '5.0.0' 필요 이상 하지만 현재 NuGet 버전은 '4.3.0'.*</span><span class="sxs-lookup"><span data-stu-id="a0533-262">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="a0533-263">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-263">**Solution**</span></span> | <span data-ttu-id="a0533-264">최신 버전의 NuGet 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-264">Install a newer version of NuGet.</span></span> <span data-ttu-id="a0533-265">참조 [NuGet 설치 클라이언트 도구](../install-nuget-client-tools.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-265">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="a0533-266">잘못 된 입력된 경고</span><span class="sxs-lookup"><span data-stu-id="a0533-266">Invalid input warnings</span></span>

<span data-ttu-id="a0533-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="a0533-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="a0533-268">NU1501</span><span class="sxs-lookup"><span data-stu-id="a0533-268">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-269">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-269">**Issue**</span></span> | <span data-ttu-id="a0533-270">프로젝트 복원 작동 하려고에서 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-270">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="a0533-271">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-271">**Example message**</span></span> | <span data-ttu-id="a0533-272">*'C:\projects\a' 폴더에 복원할 프로젝트가 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="a0533-272">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="a0533-273">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-273">**Solution**</span></span> | <span data-ttu-id="a0533-274">프로젝트를 포함 하는 폴더에 nuget 복원을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-274">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="a0533-275">NU1502</span><span class="sxs-lookup"><span data-stu-id="a0533-275">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-276">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-276">**Issue**</span></span> | <span data-ttu-id="a0533-277">`RuntimeSupports` 잘못 된 프로필을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-277">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="a0533-278">일반적으로 지원 프로필에 없습니다는 `runtime.json` 현재 종속성 패키지의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-278">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="a0533-279">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-279">**Example message**</span></span> | <span data-ttu-id="a0533-280">*알 수 없는 호환성 프로필이: aaa*</span><span class="sxs-lookup"><span data-stu-id="a0533-280">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="a0533-281">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-281">**Solution**</span></span> | <span data-ttu-id="a0533-282">확인 된 `RuntimeSupports` 프로젝트에는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-282">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="a0533-283">NU1503</span><span class="sxs-lookup"><span data-stu-id="a0533-283">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-284">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-284">**Issue**</span></span> | <span data-ttu-id="a0533-285">종속성 프로젝트에는 NuGet의 복원 대상 가져오기 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-285">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="a0533-286">이 NU1105와 유사 하지만 프로젝트는 생략 여기 모든 복원 실패를 유발 하는 대신 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-286">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="a0533-287">복잡 한 솔루션에서 종종 있습니다 다른 형식의 프로젝트 복원을 지원 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-287">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="a0533-288">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-288">**Example message**</span></span> | <span data-ttu-id="a0533-289">*'C:\a.csproj' 프로젝트에 대 한 복원을 건너뜁니다. 프로젝트 파일이 올바르지 않거나 누락 된 대상으로 복원 하는 데 필요한 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="a0533-289">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="a0533-290">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-290">**Solution**</span></span> | <span data-ttu-id="a0533-291">이 자동으로 복원 가져오기는 공통 props/대상 가져오지 않는 프로젝트에 대해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-291">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="a0533-292">프로젝트를 복원할 필요가 없는 경우 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-292">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="a0533-293">그렇지 않으면 복원에 대 한 대상을 추가 하려면 영향을 받는 프로젝트를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-293">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="a0533-294">예기치 않은 패키지 버전 경고</span><span class="sxs-lookup"><span data-stu-id="a0533-294">Unexpected package version warnings</span></span>

<span data-ttu-id="a0533-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="a0533-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="a0533-296">NU1601</span><span class="sxs-lookup"><span data-stu-id="a0533-296">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-297">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-297">**Issue**</span></span> | <span data-ttu-id="a0533-298">지정 된 프로젝트 보다 높은 버전을 직접 프로젝트 종속성 추락 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-298">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="a0533-299">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-299">**Example message**</span></span> | <span data-ttu-id="a0533-300">*지정 된 종속성은 NuGet.Versioning (> = 3.5.0) 이었지만 결과적으로 NuGet.Versioning 4.0.0 합니다.*</span><span class="sxs-lookup"><span data-stu-id="a0533-300">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="a0533-301">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-301">**Solution**</span></span> | <span data-ttu-id="a0533-302">프로젝트에 종속성을 적절 한 버전으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-302">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="a0533-303">NU1602</span><span class="sxs-lookup"><span data-stu-id="a0533-303">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-304">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-304">**Issue**</span></span> | <span data-ttu-id="a0533-305">패키지 종속성은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-305">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="a0533-306">복원 찾을 수 없도록는 *가장 일치 하는*합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-306">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="a0533-307">각 복원 아래쪽으로 사용할 수 있는 더 낮은 버전을 검색 하려고 이동 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-307">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="a0533-308">즉, 복원 될 때마다 사용자 패키지 폴더에 이미 존재 하는 패키지를 사용 하는 대신 모든 소스를 확인 하려면 온라인 전환 되는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-308">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="a0533-309">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-309">**Example message**</span></span> | <span data-ttu-id="a0533-310">*NuGet.Packaging 4.0.0 NuGet.Versioning (> 3.5.0) 종속성에 대 한는 경계값을 제공 하지 않습니다. 3.6.0의 일부만 가장 일치 하는 해결 되었습니다.*</span><span class="sxs-lookup"><span data-stu-id="a0533-310">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="a0533-311">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-311">**Solution**</span></span> | <span data-ttu-id="a0533-312">이 일반적으로 오류를 제작 하는 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-312">This is usually a package authoring error.</span></span> <span data-ttu-id="a0533-313">문제를 해결 하려면 패키지 작성자를 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a0533-313">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="a0533-314">NU1603</span><span class="sxs-lookup"><span data-stu-id="a0533-314">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-315">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-315">**Issue**</span></span> | <span data-ttu-id="a0533-316">패키지 종속성 지정 버전을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-316">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="a0533-317">일반적으로 패키지 소스에서 예상된 하한값 버전을 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-317">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="a0533-318">패키지에 대해 작성 된에서 다른 상위 버전 대신 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-318">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="a0533-319">즉, 복원이 찾을 수 없습니다는 *가장 일치 하는*합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="a0533-320">각 복원 아래쪽으로 사용할 수 있는 더 낮은 버전을 검색 하려고 이동 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="a0533-321">즉, 복원 될 때마다 사용자 패키지 폴더에 이미 존재 하는 패키지를 사용 하는 대신 모든 소스를 확인 하려면 온라인 전환 되는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="a0533-322">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-322">**Example message**</span></span> | <span data-ttu-id="a0533-323">NuGet.Packaging 4.0.0 NuGet.Versioning에 따라 달라 집니다 (> = 4.0.0) 4.0.0를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-323">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="a0533-324">5.0.0의 일부만 가장 일치 하는 해결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-324">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="a0533-325">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-325">**Solution**</span></span> | <span data-ttu-id="a0533-326">예상 패키지 해제 되지 않은 경우 오류를 제작 하는 패키지를 수 있습니다이.</span><span class="sxs-lookup"><span data-stu-id="a0533-326">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="a0533-327">문제를 해결 하려면 패키지 작성자를 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a0533-327">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="a0533-328">패키지 해제 된 경우에 사용 중인 패키지 소스에서 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-328">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="a0533-329">전용 소스를 사용 하는 경우 해당 피드에서 패키지를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-329">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="a0533-330">NU1604</span><span class="sxs-lookup"><span data-stu-id="a0533-330">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-331">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-331">**Issue**</span></span> | <span data-ttu-id="a0533-332">프로젝트 종속성 배열은 하 한을 정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-332">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="a0533-333">즉, 복원이 찾을 수 없습니다는 *가장 일치 하는*합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-333">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="a0533-334">각 복원 아래쪽으로 사용할 수 있는 더 낮은 버전을 검색 하려고 이동 수입니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-334">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="a0533-335">즉, 복원 될 때마다 사용자 패키지 폴더에 이미 존재 하는 패키지를 사용 하는 대신 모든 소스를 확인 하려면 온라인 전환 되는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-335">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="a0533-336">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-336">**Example message**</span></span> | <span data-ttu-id="a0533-337">*종속성 NuGet.Versioning 프로젝트 (< = 9.0.0) doe는 경계값을 포함 하지 합니다. 일치 복원 결과 보장 하는 종속성의 버전에 배열은 하 한을 포함 합니다.*</span><span class="sxs-lookup"><span data-stu-id="a0533-337">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="a0533-338">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-338">**Solution**</span></span> | <span data-ttu-id="a0533-339">프로젝트의 업데이트 `PackageReference` `Version` 특성 배열은 하 한을 포함 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-339">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="a0533-340">NU1605</span><span class="sxs-lookup"><span data-stu-id="a0533-340">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-341">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-341">**Issue**</span></span> | <span data-ttu-id="a0533-342">종속성 패키지에는 궁극적으로 해결 하는 복원 보다 더 높은 버전의 패키지에 버전 제약 조건을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-342">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="a0533-343">즉, "wins" 가장 가까운 규칙 패키지를 확인할 때 때문에 그래프에서 할수록 패키지 수 재정의 한 떨어져 있는 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-343">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="a0533-344">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-344">**Example message**</span></span> | <span data-ttu-id="a0533-345">*패키지가 다운 그레이드를 발견 했습니다: 3.5.0 4.0.0에서 NuGet.Versioning 합니다. 다른 버전을 선택 하는 프로젝트에서 직접 패키지를 참조 합니다.<br/>  NuGet.Packaging 3.5.0 NuGet.Versioning 3.5.0-><br/> NuGet.Commands 4.0.0 NuGet.Configuration-> 4.0.0 NuGet.Versioning 4.0.0->*</span><span class="sxs-lookup"><span data-stu-id="a0533-345">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="a0533-346">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-346">**Solution**</span></span> | <span data-ttu-id="a0533-347">사용 하려는 패키지의 버전은 더 높은 프로젝트에 대 한 직접 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-347">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="a0533-348">해결 프로그램이 충돌 경고</span><span class="sxs-lookup"><span data-stu-id="a0533-348">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="a0533-349">NU1608</span><span class="sxs-lookup"><span data-stu-id="a0533-349">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-350">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-350">**Issue**</span></span> | <span data-ttu-id="a0533-351">확인할된 패키지 종속성 제약 조건을 허용 된 것 보다 더 높습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-351">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="a0533-352">이 프로젝트에서 직접 참조 하는 패키지를 다른 패키지에서 제약 조건 종속성 재정의 함을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-352">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="a0533-353">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-353">**Example message**</span></span> | <span data-ttu-id="a0533-354">*외부 종속성 제약 조건에서 검색 된 패키지 버전: x 1.0.0 y (1.0.0 =) 이어야 하는데 버전 2.0.0 y 해결 되었습니다.*</span><span class="sxs-lookup"><span data-stu-id="a0533-354">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="a0533-355">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-355">**Solution**</span></span> | <span data-ttu-id="a0533-356">일부 경우에이 의도적인와 경고가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-356">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="a0533-357">그렇지 않은 경우 해당 버전 제약 조건 확장을 패키지에 대 한 프로젝트의 참조를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-357">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="a0533-358">패키지 대체 (fallback) 경고</span><span class="sxs-lookup"><span data-stu-id="a0533-358">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="a0533-359">NU1701</span><span class="sxs-lookup"><span data-stu-id="a0533-359">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-360">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-360">**Issue**</span></span> | <span data-ttu-id="a0533-361">`PackageTargetFallback` / `AssetTargetFallback` 패키지에서 자산을 선택 하려면 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-361">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="a0533-362">이 경고 사용자에 게를 알립니다 자산 100% 호환 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-362">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="a0533-363">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-363">**Example message**</span></span> | <span data-ttu-id="a0533-364">*패키지 'NuGet.Versioning'를 사용 하 여 '노트북 net45 + win8' 대신 프로젝트 대상 프레임 워크 'netstandard1.5' 복원 되었습니다. 이 패키지는 프로젝트와 완전히 호환 하지 못할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="a0533-364">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="a0533-365">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-365">**Solution**</span></span> | <span data-ttu-id="a0533-366">패키지에서 지 원하는 하나를 프로젝트의 대상 프레임 워크를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-366">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="a0533-367">피드 경고</span><span class="sxs-lookup"><span data-stu-id="a0533-367">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="a0533-368">NU1801</span><span class="sxs-lookup"><span data-stu-id="a0533-368">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-369">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-369">**Issue**</span></span> | <span data-ttu-id="a0533-370">피드를 읽을 때 오류가 발생 했습니다 때 `IgnoreFailedSources` 설정을 true로 변환 하는 치명적이 지 않은 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-370">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="a0533-371">이 모든 메시지를 포함할 수 이며 일반 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-371">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="a0533-372">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-372">**Example message**</span></span> | <span data-ttu-id="a0533-373">N/A</span><span class="sxs-lookup"><span data-stu-id="a0533-373">n/a</span></span> |
| <span data-ttu-id="a0533-374">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-374">**Solution**</span></span> | <span data-ttu-id="a0533-375">올바른 소스를 지정 하 여 구성을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-375">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="a0533-376">NuGet 내부 오류 및 경고</span><span class="sxs-lookup"><span data-stu-id="a0533-376">NuGet internal errors and warnings</span></span>

<span data-ttu-id="a0533-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="a0533-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="a0533-378">NU1000</span><span class="sxs-lookup"><span data-stu-id="a0533-378">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-379">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-379">**Issue**</span></span> | <span data-ttu-id="a0533-380">NuGet에서 비 특정 내부 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-380">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="a0533-381">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-381">**Solution**</span></span> | <span data-ttu-id="a0533-382">자세한 내용은 로그를 확인 하십시오</span><span class="sxs-lookup"><span data-stu-id="a0533-382">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="a0533-383">NU1500</span><span class="sxs-lookup"><span data-stu-id="a0533-383">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-384">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-384">**Issue**</span></span> | <span data-ttu-id="a0533-385">NuGet에서 비 특정 내부 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-385">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="a0533-386">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-386">**Solution**</span></span> | <span data-ttu-id="a0533-387">자세한 내용은 로그를 확인 하십시오</span><span class="sxs-lookup"><span data-stu-id="a0533-387">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="a0533-388">서명 된 패키지 (만들기 및 확인)</span><span class="sxs-lookup"><span data-stu-id="a0533-388">Signed packages (creation and verification)</span></span>

<span data-ttu-id="a0533-389">*NuGet 4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="a0533-389">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="a0533-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="a0533-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="a0533-391">NU3000</span><span class="sxs-lookup"><span data-stu-id="a0533-391">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-392">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-392">**Issue**</span></span> | <span data-ttu-id="a0533-393">관련 되지 않은 오류와 관련 된 패키지를 서명 하 고 패키지 확인을 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-393">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="a0533-394">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-394">**Solution**</span></span> | <span data-ttu-id="a0533-395">자세한 내용은 로그를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-395">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="a0533-396">NU3001</span><span class="sxs-lookup"><span data-stu-id="a0533-396">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-397">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-397">**Issue**</span></span> | <span data-ttu-id="a0533-398">잘못 된 인수 중 하나에 [명령 서명](../tools/cli-ref-sign.md) 또는 [명령 확인](../tools/cli-ref-verify.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-398">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="a0533-399">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-399">**Solution**</span></span> | <span data-ttu-id="a0533-400">확인 하 고 제공 된 인수를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-400">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="a0533-401">NU3002</span><span class="sxs-lookup"><span data-stu-id="a0533-401">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-402">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-402">**Issue**</span></span> | <span data-ttu-id="a0533-403">`-Timestamper` 사용 옵션을 지정 하지는 [nuget sign 명령](../tools/cli-ref-sign.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-403">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="a0533-404">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-404">**Example message**</span></span> | <span data-ttu-id="a0533-405">*'-Timestamper' 옵션이 제공 되지 않았습니다. 서명된 된 패키지는 타임 스탬프가 적용 되지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="a0533-405">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="a0533-406">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-406">**Solution**</span></span> | <span data-ttu-id="a0533-407">지정 된 `-Timestamper` 옵션과 함께 `nuget sign`합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-407">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="a0533-408">NU3004</span><span class="sxs-lookup"><span data-stu-id="a0533-408">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-409">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-409">**Issue**</span></span> | <span data-ttu-id="a0533-410">서명 되지 않은 패키지에 제공 된 [nuget 명령을 확인](../tools/cli-ref-verify.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-410">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="a0533-411">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-411">**Solution**</span></span> | <span data-ttu-id="a0533-412">실행 `nuget verify` 서명 된 패키지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-412">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="a0533-413">참조 [패키지 서명](../create-packages/Sign-a-Package.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-413">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="a0533-414">NU3008</span><span class="sxs-lookup"><span data-stu-id="a0533-414">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-415">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-415">**Issue**</span></span> | <span data-ttu-id="a0533-416">패키지 무결성 검사는 서명 된 패키지 서명 되 고 이후 변조 되었기를 의미 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-416">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="a0533-417">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-417">**Solution**</span></span> | <span data-ttu-id="a0533-418">컴퓨터 바이러스 백신 소프트웨어와 함께 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-418">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="a0533-419">그런 다음 컴퓨터에서 패키지를 제거 하 고 다시 설치, 작업을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-419">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="a0533-420">문제가 지속 되 면 패키지 원본 소유자와 패키지 소유자에 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="a0533-420">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="a0533-421">NU3018</span><span class="sxs-lookup"><span data-stu-id="a0533-421">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-422">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-422">**Issue**</span></span> | <span data-ttu-id="a0533-423">주 서명이 대 한 인증서 체인 만들기에 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-423">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="a0533-424">기본 서명 인증서, 신뢰할 수 있는 해지 되었거나 해지 정보에 대 한 인증서를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-424">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="a0533-425">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-425">**Example message**</span></span> | <span data-ttu-id="a0533-426">*경고: NU3018: 해당 함수에 대 한 인증서 해지를 확인할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="a0533-426">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="a0533-427">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-427">**Solution**</span></span> | <span data-ttu-id="a0533-428">신뢰할 수 있는 하 고 유효한 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-428">Use a trusted and valid certificate.</span></span> <span data-ttu-id="a0533-429">인터넷 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-429">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="a0533-430">NU3028</span><span class="sxs-lookup"><span data-stu-id="a0533-430">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="a0533-431">**문제**</span><span class="sxs-lookup"><span data-stu-id="a0533-431">**Issue**</span></span> | <span data-ttu-id="a0533-432">타임 스탬프 서명에 대 한 인증서 체인 만들기에 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-432">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="a0533-433">타임 스탬프 서명 인증서, 신뢰할 수 있는 해지 되었거나 해지 정보에 대 한 인증서를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-433">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="a0533-434">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="a0533-434">**Example message**</span></span> | <span data-ttu-id="a0533-435">*경고: NU3028: 해당 함수에 대 한 인증서 해지를 확인할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="a0533-435">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="a0533-436">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="a0533-436">**Solution**</span></span> | <span data-ttu-id="a0533-437">신뢰할 수 있는 하 고 유효한 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-437">Use a trusted and valid certificate.</span></span> <span data-ttu-id="a0533-438">인터넷 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0533-438">Check internet connectivity.</span></span> |
