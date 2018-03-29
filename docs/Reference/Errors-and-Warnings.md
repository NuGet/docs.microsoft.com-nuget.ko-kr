---
title: NuGet 오류 및 경고 참조 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 경고 및 다양 한 NuGet 작업 도중 NuGet에서 발생 한 오류에 대 한 참조를 완료 합니다.
keywords: NuGet 오류, 경고 NuGet 진단
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
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
ms.openlocfilehash: 020e31dc8646c43b86bcee555f1772e8b1db7761
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="bcec9-104">오류 및 경고</span><span class="sxs-lookup"><span data-stu-id="bcec9-104">Errors and warnings</span></span>

<span data-ttu-id="bcec9-105">오류 및 경고가이 항목에 설명 된 대로 번호가 매겨집니다 NuGet 4.3.0+ 및 관련 된 문제를 해결할 수 있도록 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-105">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="bcec9-106">오류 및 여기에 나열 된 경고에만 사용할 수 있는 [PackageReference 기반](../consume-packages/package-references-in-project-files.md) 프로젝트와 NuGet 4.3.0+ 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-106">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="bcec9-107">또한 NuGet를 경고를 표시 하거나 오류를 상승을 MSBuild 속성을 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="bcec9-108">자세한 내용은 참조 [하는 방법: 컴파일러 경고 표시 안 함](/visualstudio/ide/how-to-suppress-compiler-warnings) Visual Studio 설명서에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="bcec9-109">**오류**</span><span class="sxs-lookup"><span data-stu-id="bcec9-109">**Errors**</span></span>

| <span data-ttu-id="bcec9-110">그룹화</span><span class="sxs-lookup"><span data-stu-id="bcec9-110">Group</span></span> | <span data-ttu-id="bcec9-111">오류 번호</span><span class="sxs-lookup"><span data-stu-id="bcec9-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="bcec9-112">잘못 된 입력된 오류</span><span class="sxs-lookup"><span data-stu-id="bcec9-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="bcec9-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="bcec9-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="bcec9-114">패키지 및 프로젝트에 대 한 누락 오류</span><span class="sxs-lookup"><span data-stu-id="bcec9-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="bcec9-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (이전에 NU1607) [NU1108](#nu1108) (이전에 NU1606)</span><span class="sxs-lookup"><span data-stu-id="bcec9-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="bcec9-116">호환성 오류</span><span class="sxs-lookup"><span data-stu-id="bcec9-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="bcec9-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="bcec9-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="bcec9-118">**경고**</span><span class="sxs-lookup"><span data-stu-id="bcec9-118">**Warnings**</span></span>

| <span data-ttu-id="bcec9-119">그룹화</span><span class="sxs-lookup"><span data-stu-id="bcec9-119">Group</span></span> | <span data-ttu-id="bcec9-120">경고 번호</span><span class="sxs-lookup"><span data-stu-id="bcec9-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="bcec9-121">잘못 된 입력된 경고</span><span class="sxs-lookup"><span data-stu-id="bcec9-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="bcec9-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="bcec9-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="bcec9-123">예기치 않은 패키지 버전 경고</span><span class="sxs-lookup"><span data-stu-id="bcec9-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="bcec9-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="bcec9-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="bcec9-125">해결 프로그램이 충돌 경고</span><span class="sxs-lookup"><span data-stu-id="bcec9-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="bcec9-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="bcec9-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="bcec9-127">패키지 대체 (fallback) 경고</span><span class="sxs-lookup"><span data-stu-id="bcec9-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="bcec9-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="bcec9-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="bcec9-129">피드 경고</span><span class="sxs-lookup"><span data-stu-id="bcec9-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="bcec9-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="bcec9-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="bcec9-131">NuGet 내부 오류 및 경고</span><span class="sxs-lookup"><span data-stu-id="bcec9-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="bcec9-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="bcec9-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="bcec9-133">서명 된 패키지 (만들기 및 확인)</span><span class="sxs-lookup"><span data-stu-id="bcec9-133">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="bcec9-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="bcec9-134">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="bcec9-135">잘못 된 입력된 오류</span><span class="sxs-lookup"><span data-stu-id="bcec9-135">Invalid input errors</span></span>

<span data-ttu-id="bcec9-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="bcec9-136">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="bcec9-137">NU1001</span><span class="sxs-lookup"><span data-stu-id="bcec9-137">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-138">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-138">**Issue**</span></span> | <span data-ttu-id="bcec9-139">프로젝트는 하나 이상의 프레임 워크를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-139">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="bcec9-140">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-140">**Example message**</span></span> | <span data-ttu-id="bcec9-141">*프로젝트 projA c:\tmp\projA.csproj의 대상 프레임 워크를 지정 하지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="bcec9-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="bcec9-142">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-142">**Solution**</span></span> | <span data-ttu-id="bcec9-143">추가 `TargetFramework` 또는 `TargetFrameworks` 속성이 지정 된 프로젝트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-143">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="bcec9-144">NU1002</span><span class="sxs-lookup"><span data-stu-id="bcec9-144">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-145">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-145">**Issue**</span></span> | <span data-ttu-id="bcec9-146">일반 키워드와 함께 입력의 조합이 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-146">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="bcec9-147">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-147">**Example message**</span></span> | <span data-ttu-id="bcec9-148">*'CLEAR' 없습니다 다른 값과 함께에서 사용할 수*</span><span class="sxs-lookup"><span data-stu-id="bcec9-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="bcec9-149">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-149">**Solution**</span></span> | <span data-ttu-id="bcec9-150">지우기 단독으로 사용 하 고 다른 모든 입력을 생략 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-150">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="bcec9-151">NU1003</span><span class="sxs-lookup"><span data-stu-id="bcec9-151">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-152">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-152">**Issue**</span></span> | <span data-ttu-id="bcec9-153">`PackageTargetFallback` 및 `AssetTargetFallback` 자산을 선택 하기 위한 다른 동작을 제공 하 고 함께 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-153">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="bcec9-154">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-154">**Example message**</span></span> | <span data-ttu-id="bcec9-155">*PackageTargetFallback와 AssetTargetFallback는 함께 사용할 수 없습니다. 프로젝트 환경에서 PackageTargetFallback(deprecated) 참조를 제거 합니다.*</span><span class="sxs-lookup"><span data-stu-id="bcec9-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="bcec9-156">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-156">**Solution**</span></span> | <span data-ttu-id="bcec9-157">사용 되지 않는 제거 `PackageTargetFallback` 프로젝트에서 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-157">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="bcec9-158">패키지 및 프로젝트에 대 한 누락 오류</span><span class="sxs-lookup"><span data-stu-id="bcec9-158">Missing package and project errors</span></span>

<span data-ttu-id="bcec9-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="bcec9-159">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="bcec9-160">NU1100</span><span class="sxs-lookup"><span data-stu-id="bcec9-160">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-161">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-161">**Issue**</span></span> | <span data-ttu-id="bcec9-162">종속성 그룹 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-162">A dependency group not be resolved.</span></span> <span data-ttu-id="bcec9-163">패키지 또는 프로젝트 하지 않은 형식에 대 한 일반적인 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-163">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="bcec9-164">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-164">**Example message**</span></span> | <span data-ttu-id="bcec9-165">*Net45에 대 한 System.Missing를 확인할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="bcec9-165">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="bcec9-166">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-166">**Solution**</span></span> | <span data-ttu-id="bcec9-167">프로젝트 파일을 열고 해당 종속 항목 목록을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-167">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="bcec9-168">각 종속성을 사용 하는 패키지 소스에 있고 패키지는 프로젝트의 대상 프레임 워크를 지원 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-168">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="bcec9-169">NU1101</span><span class="sxs-lookup"><span data-stu-id="bcec9-169">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-170">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-170">**Issue**</span></span> | <span data-ttu-id="bcec9-171">모든 소스에서 패키지를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-171">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="bcec9-172">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-172">**Example message**</span></span> | <span data-ttu-id="bcec9-173">*System.Missing 패키지를 찾을 수 없습니다. 패키지 원본에이 id를 가진 존재: dotnet 코어, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="bcec9-173">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="bcec9-174">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-174">**Solution**</span></span> | <span data-ttu-id="bcec9-175">올바른 패키지 식별자와 버전 번호를 사용 하는 확인 하려면 Visual Studio에서 프로젝트의 종속성을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-175">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="bcec9-176">도 있는지 여부를 확인는 [NuGet 구성이](../consume-packages/Configuring-NuGet-Behavior.md) 패키지 소스를 식별 프로그램 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-176">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="bcec9-177">패키지를 사용 하는 경우 [의미 체계 버전 관리 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200)를 사용 하 고 있는지를 확인 하십시오는 [V3 피드](https://api.nuget.org/v3/index.json) 에 [NuGet 구성이](../consume-packages/Configuring-NuGet-Behavior.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-177">If you use packages that have [Semantic Versioning 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), please make sure that you are using the [V3 feed](https://api.nuget.org/v3/index.json) in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="bcec9-178">NU1102</span><span class="sxs-lookup"><span data-stu-id="bcec9-178">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-179">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-179">**Issue**</span></span> | <span data-ttu-id="bcec9-180">패키지 식별자를 찾았지만 소스 중 하나에서 지정 된 종속성 범위 내에서 버전을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-180">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="bcec9-181">패키지와 사용자가 아니라에서 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-181">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="bcec9-182">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-182">**Example message**</span></span> | <span data-ttu-id="bcec9-183">*버전으로 NuGet.Versioning 패키지를 찾을 수 없습니다. (> = 9.0.1)<br/> -nuget.org에 30 찾을 버전 [버전 가장 가까운: 4.0.0]<br/> -dotnet buildtools에서 찾은 10 버전 [버전 가장 가까운: 4.0.0-rc-2129]<br/> -9 찾을 수 NuGetVolatile에서 버전 [버전 가장 가까운: 3.0.0-beta-00032]<br/> -0 버전 dotnet 코어 있는<br/> -dotnet roslyn에서 0 버전을 찾을 수*</span><span class="sxs-lookup"><span data-stu-id="bcec9-183">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="bcec9-184">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-184">**Solution**</span></span> | <span data-ttu-id="bcec9-185">패키지 버전을 해결 하려면 프로젝트 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-185">Edit the project file to correct the package version.</span></span> <span data-ttu-id="bcec9-186">도 있는지 여부를 확인는 [NuGet 구성이](../consume-packages/Configuring-NuGet-Behavior.md) 패키지 소스를 식별 프로그램 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-186">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="bcec9-187">이 패키지는 프로젝트에서 직접 참조 하는 경우 requeted 버전을 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-187">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="bcec9-188">NU1103</span><span class="sxs-lookup"><span data-stu-id="bcec9-188">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-189">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-189">**Issue**</span></span> | <span data-ttu-id="bcec9-190">프로젝트 종속성 범위에 대 한 안정적인 버전을 지정 하지만 해당 범위에 안정적 버전을 찾지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-190">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="bcec9-191">시험판 버전을 찾았지만 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-191">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="bcec9-192">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-192">**Example message**</span></span> | <span data-ttu-id="bcec9-193">*버전과 NuGet.Versioning 안정적인 패키지를 찾을 수 없습니다. (> = 3.0.0)<br/> -dotnet buildtools에서 찾은 10 버전 [버전 가장 가까운: 4.0.0-rc-2129]<br/> -NuGetVolatile에서 찾을 9 버전 [버전 가장 가까운: 3.0.0-beta-00032] <br/> -0 버전 dotnet 코어 있는<br/> -dotnet roslyn에서 0 버전을 찾을 수*</span><span class="sxs-lookup"><span data-stu-id="bcec9-193">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="bcec9-194">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-194">**Solution**</span></span> |  <span data-ttu-id="bcec9-195">시험판 버전을 포함 하도록 프로젝트 파일에 버전 범위를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-195">Edit the version range in the project file to include pre-release versions.</span></span> <span data-ttu-id="bcec9-196">참조 [패키지 버전 관리](../reference/Package-Versioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-196">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="bcec9-197">NU1104</span><span class="sxs-lookup"><span data-stu-id="bcec9-197">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-198">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-198">**Issue**</span></span> | <span data-ttu-id="bcec9-199">ProjectReference 존재 하지 않는 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-199">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="bcec9-200">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-200">**Example message**</span></span> | <span data-ttu-id="bcec9-201">*프로젝트 참조 'c:\a.csproj' 존재 하지 않습니다. 프로젝트 참조는 유효 하 고 프로젝트 파일이 있는지 확인 합니다.*</span><span class="sxs-lookup"><span data-stu-id="bcec9-201">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="bcec9-202">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-202">**Solution**</span></span> | <span data-ttu-id="bcec9-203">참조 된 프로젝트의 경로를 수정 하거나 또는 참조를 제거 하려면 프로젝트 파일을 편집 경우 더 이상 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-203">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="bcec9-204">NU1105</span><span class="sxs-lookup"><span data-stu-id="bcec9-204">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-205">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-205">**Issue**</span></span> | <span data-ttu-id="bcec9-206">프로젝트 파일이 있지만에 제공 된 복원 정보가 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-206">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="bcec9-207">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-207">**Example message**</span></span> | <span data-ttu-id="bcec9-208">*'C:\a.csproj'에 대 한 프로젝트 정보를 읽을 수 없습니다. 프로젝트 파일이 올바르지 않거나 누락 된 대상으로 복원 하는 데 필요한 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="bcec9-208">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="bcec9-209">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-209">**Solution**</span></span> | <span data-ttu-id="bcec9-210">Visual Studio에서 프로젝트가 있는 경우 프로젝트를 다시 로드에 로드 되지 않은 오류 의미할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-210">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="bcec9-211">명령줄에서 파일이 손상 되었거나 "가져오기" 호출 후 사용자 지정 포함 되지 않았는지 의미할 수 있습니다이 프로젝트를 읽을 수는 복원에 필요한 대상입니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-211">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="bcec9-212">프로젝트 파일은 유효한 "가져오기" 호출 후 대상 포함 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-212">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="bcec9-213">NU1106</span><span class="sxs-lookup"><span data-stu-id="bcec9-213">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-214">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-214">**Issue**</span></span> | <span data-ttu-id="bcec9-215">종속성 제약 조건을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-215">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="bcec9-216">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-216">**Example message**</span></span> | <span data-ttu-id="bcec9-217">*{Id}에 대 한 충돌 하는 요청을 충족할 수 없습니다. {충돌 경로} 프레임 워크: {대상 그래프}*</span><span class="sxs-lookup"><span data-stu-id="bcec9-217">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |
| <span data-ttu-id="bcec9-218">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-218">**Solution**</span></span> | <span data-ttu-id="bcec9-219">정확한 버전 보다는 종속성에 대 한 보다 자유로운 범위를 지정 하려면 프로젝트 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-219">Edit the project file to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="bcec9-220">NU1107 (이전에 NU1607)</span><span class="sxs-lookup"><span data-stu-id="bcec9-220">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-221">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-221">**Issue**</span></span> | <span data-ttu-id="bcec9-222">패키지 간에 종속성 제약 조건을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-222">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="bcec9-223">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-223">**Example message**</span></span> | <span data-ttu-id="bcec9-224">*NuGet.Versioning에 대 한 검색 버전 충돌 합니다. 이 문제를 해결 하려면 프로젝트에서 직접 패키지를 참조 합니다.<br/>  NuGet.Packaging 3.5.0 NuGet.Versioning (3.5.0 =)-><br/> NuGet.Configuration 4.0.0 NuGet.Versioning (4.0.0 =)->*</span><span class="sxs-lookup"><span data-stu-id="bcec9-224">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="bcec9-225">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-225">**Solution**</span></span> | <span data-ttu-id="bcec9-226">정확한 버전에 대 한 종속성 제약 조건 사용 하 여 패키지에는 다른 패키지 버전을 필요에 따라 증가를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-226">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="bcec9-227">필요한 정확한 버전으로 직접 (프로젝트 파일에서) 프로젝트에 대 한 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-227">Add a reference to the project directly (in the project file) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="bcec9-228">NU1108 (이전에 NU1606)</span><span class="sxs-lookup"><span data-stu-id="bcec9-228">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-229">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-229">**Issue**</span></span> | <span data-ttu-id="bcec9-230">순환 종속성이 발견 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-230">A circular dependency was detected.</span></span> |
| <span data-ttu-id="bcec9-231">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-231">**Example message**</span></span> | <span data-ttu-id="bcec9-232">*순환 발견: A-B A->*</span><span class="sxs-lookup"><span data-stu-id="bcec9-232">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="bcec9-233">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-233">**Solution**</span></span> | <span data-ttu-id="bcec9-234">패키지를 제대로 작성 버그를 해결 하려면 패키지 소유자에 게 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-234">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="bcec9-235">호환성 오류</span><span class="sxs-lookup"><span data-stu-id="bcec9-235">Compatibility errors</span></span>

<span data-ttu-id="bcec9-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="bcec9-236">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="bcec9-237">NU1201</span><span class="sxs-lookup"><span data-stu-id="bcec9-237">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-238">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-238">**Issue**</span></span> | <span data-ttu-id="bcec9-239">종속성 프로젝트는 현재 프로젝트와 호환 되는 프레임 워크를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-239">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="bcec9-240">일반적으로 프로젝트의 대상 프레임 워크는 사용 중인 프로젝트 보다 높은 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-240">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="bcec9-241">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-241">**Example message**</span></span> | <span data-ttu-id="bcec9-242">*프로젝트 서버 netstandard1.3와 호환 되지 않습니다 (합니다. NETStandard, Version = v1.3). 프로젝트 서버 지원:<br/> -netstandard1.6 (합니다. NETStandard, Version = v1.6)<br/> -netcoreapp1.0 (합니다. NETCoreApp, Version = v1.0)*</span><span class="sxs-lookup"><span data-stu-id="bcec9-242">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="bcec9-243">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-243">**Solution**</span></span> | <span data-ttu-id="bcec9-244">프로젝트의 대상 프레임 워크는 프로젝트가 보다 같거나 낮은 버전으로 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-244">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="bcec9-245">NU1202</span><span class="sxs-lookup"><span data-stu-id="bcec9-245">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-246">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-246">**Issue**</span></span> | <span data-ttu-id="bcec9-247">종속성 패키지는 프로젝트와 호환 되는 모든 자산을 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-247">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="bcec9-248">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-248">**Example message**</span></span> | <span data-ttu-id="bcec9-249">*패키지 System.ComponentModel.EventBasedAsync 4.0.11 netstandard1.3와 호환 되지 않습니다 (합니다. NETStandard, Version = v1.3). System.ComponentModel.EventBasedAsync 4.0.11 지원 패키지:<br/> -monoandroid10 (MonoAndroid, 버전 = v1.0)<br/> -monotouch10 (MonoTouch, Version = v1.0)<br/> -net45 (합니다. NETFramework, Version = v4.5)<br/> -netcore50 (합니다. NETCore, Version = v5.0)<br/> -netstandard1.0 (합니다. NETStandard, Version = v1.0)<br/> -portable net45 + win8 + w p 8 + wpa81 (합니다. NETPortable, 버전 = v0.0, 프로필 Profile259 =)<br/> -win8 (Windows, Version = v 8.0)<br/> -w p 8 (WindowsPhone, 버전 v 8.0 =)<br/> -wpa81 (이 WindowsPhoneApp, 버전 = v8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="bcec9-249">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="bcec9-250">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-250">**Solution**</span></span> | <span data-ttu-id="bcec9-251">패키지에서 지 원하는 하나를 프로젝트의 대상 프레임 워크를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-251">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="bcec9-252">NU1203</span><span class="sxs-lookup"><span data-stu-id="bcec9-252">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-253">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-253">**Issue**</span></span> | <span data-ttu-id="bcec9-254">패키지는 프로젝트를 지원 하지 않습니다 `RuntimeIdentifier`합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-254">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="bcec9-255">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-255">**Example message**</span></span> | <span data-ttu-id="bcec9-256">*System.Example 1.0.0 net461에 a.dll에 대 한 compile-time 참조 어셈블리를 제공 하지만 호환 런타임 어셈블리가 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="bcec9-256">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="bcec9-257">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-257">**Solution**</span></span> | <span data-ttu-id="bcec9-258">변경 된 `RuntimeIdentifier` 필요에 따라 프로젝트에 사용 되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-258">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="bcec9-259">NU1401</span><span class="sxs-lookup"><span data-stu-id="bcec9-259">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-260">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-260">**Issue**</span></span> | <span data-ttu-id="bcec9-261">패키지 기능 또는 현재 설치 된 버전의 NuGet에서 지원 되는 프레임 워크에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-261">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="bcec9-262">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-262">**Example message**</span></span> | <span data-ttu-id="bcec9-263">*'NuGet.Versioning' 패키지에는 NuGet 클라이언트 버전 '5.0.0' 필요 이상 하지만 현재 NuGet 버전은 '4.3.0'.*</span><span class="sxs-lookup"><span data-stu-id="bcec9-263">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="bcec9-264">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-264">**Solution**</span></span> | <span data-ttu-id="bcec9-265">최신 버전의 NuGet 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-265">Install a newer version of NuGet.</span></span> <span data-ttu-id="bcec9-266">참조 [NuGet 설치 클라이언트 도구](../install-nuget-client-tools.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-266">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="bcec9-267">잘못 된 입력된 경고</span><span class="sxs-lookup"><span data-stu-id="bcec9-267">Invalid input warnings</span></span>

<span data-ttu-id="bcec9-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="bcec9-268">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="bcec9-269">NU1501</span><span class="sxs-lookup"><span data-stu-id="bcec9-269">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-270">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-270">**Issue**</span></span> | <span data-ttu-id="bcec9-271">프로젝트 복원 작동 하려고에서 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-271">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="bcec9-272">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-272">**Example message**</span></span> | <span data-ttu-id="bcec9-273">*'C:\projects\a' 폴더에 복원할 프로젝트가 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="bcec9-273">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="bcec9-274">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-274">**Solution**</span></span> | <span data-ttu-id="bcec9-275">프로젝트를 포함 하는 폴더에 nuget 복원을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-275">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="bcec9-276">NU1502</span><span class="sxs-lookup"><span data-stu-id="bcec9-276">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-277">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-277">**Issue**</span></span> | <span data-ttu-id="bcec9-278">`RuntimeSupports` 잘못 된 프로필을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-278">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="bcec9-279">일반적으로 지원 프로필에 없습니다는 `runtime.json` 현재 종속성 패키지의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-279">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="bcec9-280">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-280">**Example message**</span></span> | <span data-ttu-id="bcec9-281">*알 수 없는 호환성 프로필이: aaa*</span><span class="sxs-lookup"><span data-stu-id="bcec9-281">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="bcec9-282">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-282">**Solution**</span></span> | <span data-ttu-id="bcec9-283">확인 된 `RuntimeSupports` 프로젝트에는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-283">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="bcec9-284">NU1503</span><span class="sxs-lookup"><span data-stu-id="bcec9-284">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-285">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-285">**Issue**</span></span> | <span data-ttu-id="bcec9-286">종속성 프로젝트에는 NuGet의 복원 대상 가져오기 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-286">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="bcec9-287">이 NU1105와 유사 하지만 프로젝트는 생략 여기 모든 복원 실패를 유발 하는 대신 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-287">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="bcec9-288">복잡 한 솔루션에서 종종 있습니다 다른 형식의 프로젝트 복원을 지원 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-288">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="bcec9-289">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-289">**Example message**</span></span> | <span data-ttu-id="bcec9-290">*'C:\a.csproj' 프로젝트에 대 한 복원을 건너뜁니다. 프로젝트 파일이 올바르지 않거나 누락 된 대상으로 복원 하는 데 필요한 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="bcec9-290">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="bcec9-291">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-291">**Solution**</span></span> | <span data-ttu-id="bcec9-292">이 자동으로 복원 가져오기는 공통 props/대상 가져오지 않는 프로젝트에 대해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-292">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="bcec9-293">프로젝트를 복원할 필요가 없는 경우 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-293">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="bcec9-294">그렇지 않으면 복원에 대 한 대상을 추가 하려면 영향을 받는 프로젝트를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-294">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="bcec9-295">예기치 않은 패키지 버전 경고</span><span class="sxs-lookup"><span data-stu-id="bcec9-295">Unexpected package version warnings</span></span>

<span data-ttu-id="bcec9-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="bcec9-296">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="bcec9-297">NU1601</span><span class="sxs-lookup"><span data-stu-id="bcec9-297">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-298">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-298">**Issue**</span></span> | <span data-ttu-id="bcec9-299">지정 된 프로젝트 보다 높은 버전을 직접 프로젝트 종속성 추락 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-299">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="bcec9-300">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-300">**Example message**</span></span> | <span data-ttu-id="bcec9-301">*지정 된 종속성은 NuGet.Versioning (> = 3.5.0) 이었지만 결과적으로 NuGet.Versioning 4.0.0 합니다.*</span><span class="sxs-lookup"><span data-stu-id="bcec9-301">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="bcec9-302">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-302">**Solution**</span></span> | <span data-ttu-id="bcec9-303">프로젝트에 종속성을 적절 한 버전으로 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-303">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="bcec9-304">NU1602</span><span class="sxs-lookup"><span data-stu-id="bcec9-304">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-305">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-305">**Issue**</span></span> | <span data-ttu-id="bcec9-306">패키지 종속성은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-306">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="bcec9-307">복원 찾을 수 없도록는 *가장 일치 하는*합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-307">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="bcec9-308">각 복원 아래쪽으로 사용할 수 있는 더 낮은 버전을 검색 하려고 이동 수입니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="bcec9-309">즉, 복원 될 때마다 사용자 패키지 폴더에 이미 존재 하는 패키지를 사용 하는 대신 모든 소스를 확인 하려면 온라인 전환 되는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="bcec9-310">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-310">**Example message**</span></span> | <span data-ttu-id="bcec9-311">*NuGet.Packaging 4.0.0 NuGet.Versioning (> 3.5.0) 종속성에 대 한는 경계값을 제공 하지 않습니다. 3.6.0의 일부만 가장 일치 하는 해결 되었습니다.*</span><span class="sxs-lookup"><span data-stu-id="bcec9-311">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="bcec9-312">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-312">**Solution**</span></span> | <span data-ttu-id="bcec9-313">이 일반적으로 오류를 제작 하는 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-313">This is usually a package authoring error.</span></span> <span data-ttu-id="bcec9-314">문제를 해결 하려면 패키지 작성자를 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="bcec9-314">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="bcec9-315">NU1603</span><span class="sxs-lookup"><span data-stu-id="bcec9-315">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-316">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-316">**Issue**</span></span> | <span data-ttu-id="bcec9-317">패키지 종속성 지정 버전을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-317">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="bcec9-318">일반적으로 패키지 소스에서 예상된 하한값 버전을 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-318">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="bcec9-319">패키지에 대해 작성 된에서 다른 상위 버전 대신 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-319">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="bcec9-320">즉, 복원이 찾을 수 없습니다는 *가장 일치 하는*합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-320">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="bcec9-321">각 복원 아래쪽으로 사용할 수 있는 더 낮은 버전을 검색 하려고 이동 수입니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-321">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="bcec9-322">즉, 복원 될 때마다 사용자 패키지 폴더에 이미 존재 하는 패키지를 사용 하는 대신 모든 소스를 확인 하려면 온라인 전환 되는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-322">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="bcec9-323">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-323">**Example message**</span></span> | <span data-ttu-id="bcec9-324">NuGet.Packaging 4.0.0 NuGet.Versioning에 따라 달라 집니다 (> = 4.0.0) 4.0.0를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-324">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="bcec9-325">5.0.0의 일부만 가장 일치 하는 해결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-325">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="bcec9-326">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-326">**Solution**</span></span> | <span data-ttu-id="bcec9-327">예상 패키지 해제 되지 않은 경우 오류를 제작 하는 패키지를 수 있습니다이.</span><span class="sxs-lookup"><span data-stu-id="bcec9-327">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="bcec9-328">문제를 해결 하려면 패키지 작성자를 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="bcec9-328">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="bcec9-329">패키지 해제 된 경우에 사용 중인 패키지 소스에서 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-329">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="bcec9-330">전용 소스를 사용 하는 경우 해당 피드에서 패키지를 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-330">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="bcec9-331">NU1604</span><span class="sxs-lookup"><span data-stu-id="bcec9-331">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-332">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-332">**Issue**</span></span> | <span data-ttu-id="bcec9-333">프로젝트 종속성 배열은 하 한을 정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-333">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="bcec9-334">즉, 복원이 찾을 수 없습니다는 *가장 일치 하는*합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-334">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="bcec9-335">각 복원 아래쪽으로 사용할 수 있는 더 낮은 버전을 검색 하려고 이동 수입니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-335">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="bcec9-336">즉, 복원 될 때마다 사용자 패키지 폴더에 이미 존재 하는 패키지를 사용 하는 대신 모든 소스를 확인 하려면 온라인 전환 되는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-336">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="bcec9-337">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-337">**Example message**</span></span> | <span data-ttu-id="bcec9-338">*종속성 NuGet.Versioning 프로젝트 (< = 9.0.0) doe는 경계값을 포함 하지 합니다. 일치 복원 결과 보장 하는 종속성의 버전에 배열은 하 한을 포함 합니다.*</span><span class="sxs-lookup"><span data-stu-id="bcec9-338">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="bcec9-339">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-339">**Solution**</span></span> | <span data-ttu-id="bcec9-340">프로젝트의 업데이트 `PackageReference` `Version` 특성 배열은 하 한을 포함 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-340">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="bcec9-341">NU1605</span><span class="sxs-lookup"><span data-stu-id="bcec9-341">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-342">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-342">**Issue**</span></span> | <span data-ttu-id="bcec9-343">종속성 패키지에는 궁극적으로 해결 하는 복원 보다 더 높은 버전의 패키지에 버전 제약 조건을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-343">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="bcec9-344">즉, "wins" 가장 가까운 규칙 패키지를 확인할 때 때문에 그래프에서 할수록 패키지 수 재정의 한 떨어져 있는 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-344">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="bcec9-345">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-345">**Example message**</span></span> | <span data-ttu-id="bcec9-346">*패키지가 다운 그레이드를 발견 했습니다: 3.5.0 4.0.0에서 NuGet.Versioning 합니다. 다른 버전을 선택 하는 프로젝트에서 직접 패키지를 참조 합니다.<br/>  NuGet.Packaging 3.5.0 NuGet.Versioning 3.5.0-><br/> NuGet.Commands 4.0.0 NuGet.Configuration-> 4.0.0 NuGet.Versioning 4.0.0->*</span><span class="sxs-lookup"><span data-stu-id="bcec9-346">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="bcec9-347">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-347">**Solution**</span></span> | <span data-ttu-id="bcec9-348">사용 하려는 패키지의 버전은 더 높은 프로젝트에 대 한 직접 참조를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-348">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="bcec9-349">해결 프로그램이 충돌 경고</span><span class="sxs-lookup"><span data-stu-id="bcec9-349">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="bcec9-350">NU1608</span><span class="sxs-lookup"><span data-stu-id="bcec9-350">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-351">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-351">**Issue**</span></span> | <span data-ttu-id="bcec9-352">확인할된 패키지 종속성 제약 조건을 허용 된 것 보다 더 높습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-352">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="bcec9-353">이 프로젝트에서 직접 참조 하는 패키지를 다른 패키지에서 제약 조건 종속성 재정의 함을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-353">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="bcec9-354">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-354">**Example message**</span></span> | <span data-ttu-id="bcec9-355">*외부 종속성 제약 조건에서 검색 된 패키지 버전: x 1.0.0 y (1.0.0 =) 이어야 하는데 버전 2.0.0 y 해결 되었습니다.*</span><span class="sxs-lookup"><span data-stu-id="bcec9-355">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="bcec9-356">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-356">**Solution**</span></span> | <span data-ttu-id="bcec9-357">일부 경우에이 의도적인와 경고가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-357">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="bcec9-358">그렇지 않은 경우 해당 버전 제약 조건 확장을 패키지에 대 한 프로젝트의 참조를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-358">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="bcec9-359">패키지 대체 (fallback) 경고</span><span class="sxs-lookup"><span data-stu-id="bcec9-359">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="bcec9-360">NU1701</span><span class="sxs-lookup"><span data-stu-id="bcec9-360">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-361">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-361">**Issue**</span></span> | <span data-ttu-id="bcec9-362">`PackageTargetFallback` / `AssetTargetFallback` 패키지에서 자산을 선택 하려면 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-362">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="bcec9-363">이 경고 사용자에 게를 알립니다 자산 100% 호환 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-363">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="bcec9-364">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-364">**Example message**</span></span> | <span data-ttu-id="bcec9-365">*패키지 'NuGet.Versioning'를 사용 하 여 '노트북 net45 + win8' 대신 프로젝트 대상 프레임 워크 'netstandard1.5' 복원 되었습니다. 이 패키지는 프로젝트와 완전히 호환 하지 못할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="bcec9-365">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="bcec9-366">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-366">**Solution**</span></span> | <span data-ttu-id="bcec9-367">패키지에서 지 원하는 하나를 프로젝트의 대상 프레임 워크를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-367">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="bcec9-368">피드 경고</span><span class="sxs-lookup"><span data-stu-id="bcec9-368">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="bcec9-369">NU1801</span><span class="sxs-lookup"><span data-stu-id="bcec9-369">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-370">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-370">**Issue**</span></span> | <span data-ttu-id="bcec9-371">피드를 읽을 때 오류가 발생 했습니다 때 `IgnoreFailedSources` 설정을 true로 변환 하는 치명적이 지 않은 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-371">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="bcec9-372">이 모든 메시지를 포함할 수 이며 일반 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-372">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="bcec9-373">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-373">**Example message**</span></span> | <span data-ttu-id="bcec9-374">N/A</span><span class="sxs-lookup"><span data-stu-id="bcec9-374">n/a</span></span> |
| <span data-ttu-id="bcec9-375">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-375">**Solution**</span></span> | <span data-ttu-id="bcec9-376">올바른 소스를 지정 하 여 구성을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-376">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="bcec9-377">NuGet 내부 오류 및 경고</span><span class="sxs-lookup"><span data-stu-id="bcec9-377">NuGet internal errors and warnings</span></span>

<span data-ttu-id="bcec9-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="bcec9-378">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="bcec9-379">NU1000</span><span class="sxs-lookup"><span data-stu-id="bcec9-379">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-380">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-380">**Issue**</span></span> | <span data-ttu-id="bcec9-381">NuGet에서 비 특정 내부 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-381">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="bcec9-382">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-382">**Solution**</span></span> | <span data-ttu-id="bcec9-383">자세한 내용은 로그를 확인 하십시오</span><span class="sxs-lookup"><span data-stu-id="bcec9-383">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="bcec9-384">NU1500</span><span class="sxs-lookup"><span data-stu-id="bcec9-384">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-385">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-385">**Issue**</span></span> | <span data-ttu-id="bcec9-386">NuGet에서 비 특정 내부 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-386">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="bcec9-387">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-387">**Solution**</span></span> | <span data-ttu-id="bcec9-388">자세한 내용은 로그를 확인 하십시오</span><span class="sxs-lookup"><span data-stu-id="bcec9-388">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="bcec9-389">서명 된 패키지 (만들기 및 확인)</span><span class="sxs-lookup"><span data-stu-id="bcec9-389">Signed packages (creation and verification)</span></span>

<span data-ttu-id="bcec9-390">*NuGet 4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="bcec9-390">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="bcec9-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="bcec9-391">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="bcec9-392">NU3000</span><span class="sxs-lookup"><span data-stu-id="bcec9-392">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-393">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-393">**Issue**</span></span> | <span data-ttu-id="bcec9-394">관련 되지 않은 오류와 관련 된 패키지를 서명 하 고 패키지 확인을 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-394">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="bcec9-395">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-395">**Solution**</span></span> | <span data-ttu-id="bcec9-396">자세한 내용은 로그를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-396">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="bcec9-397">NU3001</span><span class="sxs-lookup"><span data-stu-id="bcec9-397">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-398">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-398">**Issue**</span></span> | <span data-ttu-id="bcec9-399">잘못 된 인수 중 하나에 [명령 서명](../tools/cli-ref-sign.md) 또는 [명령 확인](../tools/cli-ref-verify.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-399">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="bcec9-400">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-400">**Solution**</span></span> | <span data-ttu-id="bcec9-401">확인 하 고 제공 된 인수를 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-401">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="bcec9-402">NU3002</span><span class="sxs-lookup"><span data-stu-id="bcec9-402">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-403">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-403">**Issue**</span></span> | <span data-ttu-id="bcec9-404">`-Timestamper` 사용 옵션을 지정 하지는 [nuget sign 명령](../tools/cli-ref-sign.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-404">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="bcec9-405">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-405">**Example message**</span></span> | <span data-ttu-id="bcec9-406">*'-Timestamper' 옵션이 제공 되지 않았습니다. 서명된 된 패키지는 타임 스탬프가 적용 되지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="bcec9-406">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="bcec9-407">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-407">**Solution**</span></span> | <span data-ttu-id="bcec9-408">지정 된 `-Timestamper` 옵션과 함께 `nuget sign`합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-408">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="bcec9-409">NU3004</span><span class="sxs-lookup"><span data-stu-id="bcec9-409">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-410">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-410">**Issue**</span></span> | <span data-ttu-id="bcec9-411">서명 되지 않은 패키지에 제공 된 [nuget 명령을 확인](../tools/cli-ref-verify.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-411">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="bcec9-412">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-412">**Solution**</span></span> | <span data-ttu-id="bcec9-413">실행 `nuget verify` 서명 된 패키지를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-413">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="bcec9-414">참조 [패키지 서명](../create-packages/Sign-a-Package.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-414">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="bcec9-415">NU3008</span><span class="sxs-lookup"><span data-stu-id="bcec9-415">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-416">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-416">**Issue**</span></span> | <span data-ttu-id="bcec9-417">패키지 무결성 검사는 서명 된 패키지 서명 되 고 이후 변조 되었기를 의미 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-417">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="bcec9-418">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-418">**Solution**</span></span> | <span data-ttu-id="bcec9-419">컴퓨터 바이러스 백신 소프트웨어와 함께 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-419">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="bcec9-420">그런 다음 컴퓨터에서 패키지를 제거 하 고 다시 설치, 작업을 다시 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-420">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="bcec9-421">문제가 지속 되 면 패키지 원본 소유자와 패키지 소유자에 게 문의 하십시오.</span><span class="sxs-lookup"><span data-stu-id="bcec9-421">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="bcec9-422">NU3018</span><span class="sxs-lookup"><span data-stu-id="bcec9-422">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-423">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-423">**Issue**</span></span> | <span data-ttu-id="bcec9-424">주 서명이 대 한 인증서 체인 만들기에 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-424">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="bcec9-425">기본 서명 인증서, 신뢰할 수 있는 해지 되었거나 해지 정보에 대 한 인증서를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-425">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="bcec9-426">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-426">**Example message**</span></span> | <span data-ttu-id="bcec9-427">*경고: NU3018: 해당 함수에 대 한 인증서 해지를 확인할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="bcec9-427">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="bcec9-428">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-428">**Solution**</span></span> | <span data-ttu-id="bcec9-429">신뢰할 수 있는 하 고 유효한 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-429">Use a trusted and valid certificate.</span></span> <span data-ttu-id="bcec9-430">인터넷 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-430">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="bcec9-431">NU3028</span><span class="sxs-lookup"><span data-stu-id="bcec9-431">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="bcec9-432">**문제**</span><span class="sxs-lookup"><span data-stu-id="bcec9-432">**Issue**</span></span> | <span data-ttu-id="bcec9-433">타임 스탬프 서명에 대 한 인증서 체인 만들기에 실패 했습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-433">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="bcec9-434">타임 스탬프 서명 인증서, 신뢰할 수 있는 해지 되었거나 해지 정보에 대 한 인증서를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-434">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="bcec9-435">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="bcec9-435">**Example message**</span></span> | <span data-ttu-id="bcec9-436">*경고: NU3028: 해당 함수에 대 한 인증서 해지를 확인할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="bcec9-436">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="bcec9-437">**해결 방법**</span><span class="sxs-lookup"><span data-stu-id="bcec9-437">**Solution**</span></span> | <span data-ttu-id="bcec9-438">신뢰할 수 있는 하 고 유효한 인증서를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-438">Use a trusted and valid certificate.</span></span> <span data-ttu-id="bcec9-439">인터넷 연결을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="bcec9-439">Check internet connectivity.</span></span> |
