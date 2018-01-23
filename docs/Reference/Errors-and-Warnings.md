---
title: "NuGet 복원 오류 및 경고 참조 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b76b8a00-7155-4163-b533-894086d2ef78
description: "경고 및 패키지를 복원 하는 동안 NuGet에서 발급 한 오류에 대 한 완전 한 지침"
keywords: "NuGet 오류, 경고 NuGet 진단"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 29eb72cbb6c095cd3aeb524fd8b28416ec5dc798
ms.sourcegitcommit: 6ccb963e065680ab2e7df1d8dd5492897fd56b04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="4c3fc-104">오류 및 경고</span><span class="sxs-lookup"><span data-stu-id="4c3fc-104">Errors and warnings</span></span>

<span data-ttu-id="4c3fc-105">오류 및 경고가이 항목에 설명 된 대로 번호가 매겨집니다 4.3.0 NuGet 및 관련 된 문제를 해결할 수 있도록 자세한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-105">In NuGet 4.3.0, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span> 

<span data-ttu-id="4c3fc-106">오류 및 여기에 나열 된 경고에만 사용할 수 있는 [PackageReference 기반](../Consume-Packages/Package-References-in-Project-Files.md) 프로젝트와 NuGet 4.3.0입니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-106">The errors and warnings listed here are available only with [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) projects and NuGet 4.3.0.</span></span> <span data-ttu-id="4c3fc-107">또한 NuGet를 경고를 표시 하거나 오류를 상승을 MSBuild 속성을 준수 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="4c3fc-108">자세한 내용은 참조 [하는 방법: 컴파일러 경고 표시 안 함](/visualstudio/ide/how-to-suppress-compiler-warnings) Visual Studio 설명서에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="4c3fc-109">**오류**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-109">**Errors**</span></span>

| <span data-ttu-id="4c3fc-110">그룹화</span><span class="sxs-lookup"><span data-stu-id="4c3fc-110">Group</span></span> | <span data-ttu-id="4c3fc-111">오류 번호</span><span class="sxs-lookup"><span data-stu-id="4c3fc-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="4c3fc-112">잘못 된 입력된 오류</span><span class="sxs-lookup"><span data-stu-id="4c3fc-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="4c3fc-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="4c3fc-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="4c3fc-114">패키지 및 프로젝트에 대 한 누락 오류</span><span class="sxs-lookup"><span data-stu-id="4c3fc-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="4c3fc-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [ NU1106](#nu1106), [NU1107](#nu1107) (이전에 NU1607) [NU1108](#nu1108) (이전에 NU1606)</span><span class="sxs-lookup"><span data-stu-id="4c3fc-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="4c3fc-116">호환성 오류</span><span class="sxs-lookup"><span data-stu-id="4c3fc-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="4c3fc-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="4c3fc-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="4c3fc-118">**경고**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-118">**Warnings**</span></span>

| <span data-ttu-id="4c3fc-119">그룹화</span><span class="sxs-lookup"><span data-stu-id="4c3fc-119">Group</span></span> | <span data-ttu-id="4c3fc-120">경고 번호</span><span class="sxs-lookup"><span data-stu-id="4c3fc-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="4c3fc-121">잘못 된 입력된 경고</span><span class="sxs-lookup"><span data-stu-id="4c3fc-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="4c3fc-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="4c3fc-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="4c3fc-123">예기치 않은 패키지 버전 경고</span><span class="sxs-lookup"><span data-stu-id="4c3fc-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="4c3fc-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="4c3fc-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="4c3fc-125">해결 프로그램이 충돌 경고</span><span class="sxs-lookup"><span data-stu-id="4c3fc-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="4c3fc-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="4c3fc-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="4c3fc-127">패키지 대체 (fallback) 경고</span><span class="sxs-lookup"><span data-stu-id="4c3fc-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="4c3fc-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="4c3fc-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="4c3fc-129">피드 경고</span><span class="sxs-lookup"><span data-stu-id="4c3fc-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="4c3fc-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="4c3fc-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="4c3fc-131">NuGet 내부 오류 및 경고</span><span class="sxs-lookup"><span data-stu-id="4c3fc-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="4c3fc-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="4c3fc-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="4c3fc-133">잘못 된 입력된 오류</span><span class="sxs-lookup"><span data-stu-id="4c3fc-133">Invalid input errors</span></span>

<span data-ttu-id="4c3fc-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="4c3fc-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="4c3fc-135">NU1001</span><span class="sxs-lookup"><span data-stu-id="4c3fc-135">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-136">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-136">**Issue**</span></span> | <span data-ttu-id="4c3fc-137">프로젝트는 하나 이상의 프레임 워크를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-137">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="4c3fc-138">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-138">**Common causes**</span></span> | <span data-ttu-id="4c3fc-139">프로젝트에 포함 되어 있지 않습니다는 `TargetFramework` 또는 `TargetFrameworks` 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-139">The project doesn't contain a `TargetFramework` or `TargetFrameworks` property.</span></span> |
| <span data-ttu-id="4c3fc-140">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-140">**Example message**</span></span> | <span data-ttu-id="4c3fc-141">*프로젝트 projA c:\tmp\projA.csproj의 대상 프레임 워크를 지정 하지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |

### <a name="nu1002"></a><span data-ttu-id="4c3fc-142">NU1002</span><span class="sxs-lookup"><span data-stu-id="4c3fc-142">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-143">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-143">**Issue**</span></span> | <span data-ttu-id="4c3fc-144">일반 키워드와 함께 입력의 조합이 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-144">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="4c3fc-145">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-145">**Common causes**</span></span> | <span data-ttu-id="4c3fc-146">다른 입력을 지 원하는 일반을 결합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-146">CLEAR may not be combined with other inputs.</span></span> |
| <span data-ttu-id="4c3fc-147">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-147">**Example message**</span></span> | <span data-ttu-id="4c3fc-148">*'CLEAR' 없습니다 다른 값과 함께에서 사용할 수*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |

### <a name="nu1003"></a><span data-ttu-id="4c3fc-149">NU1003</span><span class="sxs-lookup"><span data-stu-id="4c3fc-149">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-150">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-150">**Issue**</span></span> | <span data-ttu-id="4c3fc-151">`PackageTargetFallback`및 `AssetTargetFallback` 자산을 선택 하기 위한 다른 동작을 제공 하 고 함께 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-151">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="4c3fc-152">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-152">**Common causes**</span></span> | <span data-ttu-id="4c3fc-153">둘 다 `PackageTargetFallback` 및 `AssetTargetFallback` 프로젝트에 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-153">Both `PackageTargetFallback` and `AssetTargetFallback` exist in the project.</span></span> |
| <span data-ttu-id="4c3fc-154">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-154">**Example message**</span></span> | <span data-ttu-id="4c3fc-155">*PackageTargetFallback와 AssetTargetFallback는 함께 사용할 수 없습니다. 프로젝트 환경에서 PackageTargetFallback(deprecated) 참조를 제거 합니다.*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="4c3fc-156">패키지 및 프로젝트에 대 한 누락 오류</span><span class="sxs-lookup"><span data-stu-id="4c3fc-156">Missing package and project errors</span></span>

<span data-ttu-id="4c3fc-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="4c3fc-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="4c3fc-158">NU1100</span><span class="sxs-lookup"><span data-stu-id="4c3fc-158">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-159">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-159">**Issue**</span></span> | <span data-ttu-id="4c3fc-160">종속성 그룹 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-160">A dependency group not be resolved.</span></span> <span data-ttu-id="4c3fc-161">패키지 또는 프로젝트 하지 않은 형식에 대 한 일반적인 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-161">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="4c3fc-162">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-162">**Common causes**</span></span> | <span data-ttu-id="4c3fc-163">프로젝트는 존재 하지 않는 항목에 대 한 종속성을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-163">The project contains a dependency on an item that doesn't exist.</span></span> |
| <span data-ttu-id="4c3fc-164">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-164">**Example message**</span></span> | <span data-ttu-id="4c3fc-165">*Net45에 대 한 System.Missing를 확인할 수 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-165">*Unable to resolve System.Missing for net45*</span></span> |

### <a name="nu1101"></a><span data-ttu-id="4c3fc-166">NU1101</span><span class="sxs-lookup"><span data-stu-id="4c3fc-166">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-167">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-167">**Issue**</span></span> | <span data-ttu-id="4c3fc-168">모든 소스에서 패키지를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-168">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="4c3fc-169">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-169">**Common causes**</span></span> | <span data-ttu-id="4c3fc-170">올바른 패키지 원본 누락 되었거나 있는 패키지 식별자가 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-170">The correct package source is missing or the package identifier is incorrect.</span></span> |
| <span data-ttu-id="4c3fc-171">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-171">**Example message**</span></span> | <span data-ttu-id="4c3fc-172">*System.Missing 패키지를 찾을 수 없습니다. 패키지 원본에이 id를 가진 존재: dotnet 코어, dotnet roslyn, nuget.org*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |

### <a name="nu1102"></a><span data-ttu-id="4c3fc-173">NU1102</span><span class="sxs-lookup"><span data-stu-id="4c3fc-173">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-174">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-174">**Issue**</span></span> | <span data-ttu-id="4c3fc-175">패키지 식별자를 찾았지만 소스 중 하나에서 지정 된 종속성 범위 내에서 버전을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-175">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> |
| <span data-ttu-id="4c3fc-176">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-176">**Common causes**</span></span> | <span data-ttu-id="4c3fc-177">올바른 패키지 원본 누락 되었거나 종속성 범위가 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-177">The correct package source is missing or the dependency range is incorrect.</span></span> <span data-ttu-id="4c3fc-178">패키지와 사용자가 아니라에서 범위를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-178">The range might be specified by a package and not the user.</span></span> <span data-ttu-id="4c3fc-179">사용자는이 패키지는 프로젝트에서 직접 참조 하는 경우 사용 가능한 버전으로 전환 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-179">The user may need to switch to an available version if this package is referenced by the project directly.</span></span> |
| <span data-ttu-id="4c3fc-180">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-180">**Example message**</span></span> | <span data-ttu-id="4c3fc-181">*버전으로 NuGet.Versioning 패키지를 찾을 수 없습니다. (> = 9.0.1)<br/> -nuget.org에 30 찾을 버전 [버전 가장 가까운: 4.0.0]<br/> -dotnet buildtools에서 찾은 10 버전 [버전 가장 가까운: 4.0.0-rc-2129]<br/> -9 찾을 수 NuGetVolatile에서 버전 [버전 가장 가까운: 3.0.0-beta-00032]<br/> -0 버전 dotnet 코어 있는<br/> -dotnet roslyn에서 0 버전을 찾을 수*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-181">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1103"></a><span data-ttu-id="4c3fc-182">NU1103</span><span class="sxs-lookup"><span data-stu-id="4c3fc-182">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-183">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-183">**Issue**</span></span> | <span data-ttu-id="4c3fc-184">종속성 범위에 안정적 버전을 찾지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-184">No stable versions were found in the dependency range.</span></span> <span data-ttu-id="4c3fc-185">시험판 버전을 찾았지만 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-185">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="4c3fc-186">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-186">**Common causes**</span></span> | <span data-ttu-id="4c3fc-187">프로젝트는 종속성 범위에 대 한 안정적인 버전을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-187">The project specified a stable version for the dependency range.</span></span> <span data-ttu-id="4c3fc-188">사용자는 시험판 버전을 포함 하도록 버전 범위를 변경 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-188">Users need to change the version range to include pre-release versions.</span></span> |
| <span data-ttu-id="4c3fc-189">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-189">**Example message**</span></span> | <span data-ttu-id="4c3fc-190">*버전과 NuGet.Versioning 안정적인 패키지를 찾을 수 없습니다. (> = 3.0.0)<br/> -dotnet buildtools에서 찾은 10 버전 [버전 가장 가까운: 4.0.0-rc-2129]<br/> -NuGetVolatile에서 찾을 9 버전 [버전 가장 가까운: 3.0.0-beta-00032] <br/> -0 버전 dotnet 코어 있는<br/> -dotnet roslyn에서 0 버전을 찾을 수*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-190">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1104"></a><span data-ttu-id="4c3fc-191">NU1104</span><span class="sxs-lookup"><span data-stu-id="4c3fc-191">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-192">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-192">**Issue**</span></span> | <span data-ttu-id="4c3fc-193">ProjectReference 존재 하지 않는 파일을 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-193">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="4c3fc-194">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-194">**Common causes**</span></span> | <span data-ttu-id="4c3fc-195">프로젝트 파일에는 디스크에서 누락 되었거나는 참조가 잘못 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-195">The project file is missing from disk or the reference is incorrect.</span></span> |
| <span data-ttu-id="4c3fc-196">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-196">**Example message**</span></span> | <span data-ttu-id="4c3fc-197">*프로젝트 참조 'c:\a.csproj' 존재 하지 않습니다. 프로젝트 참조는 유효 하 고 프로젝트 파일이 있는지 확인 합니다.*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-197">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |

### <a name="nu1105"></a><span data-ttu-id="4c3fc-198">NU1105</span><span class="sxs-lookup"><span data-stu-id="4c3fc-198">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-199">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-199">**Issue**</span></span> | <span data-ttu-id="4c3fc-200">프로젝트 파일이 있지만에 제공 된 복원 정보가 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-200">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="4c3fc-201">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-201">**Common causes**</span></span> | <span data-ttu-id="4c3fc-202">Visual Studio에서 프로젝트가 로드 되지 않은 것을 의미할 수이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-202">In Visual Studio this could mean that the project is unloaded.</span></span> <span data-ttu-id="4c3fc-203">명령줄에서이 파일이 손상 되었거나 imports 대상 프로젝트를 읽을 수는 복원에 필요한 이후에 사용자 지정 포함 되지 않았는지를 의미할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-203">From the command line this could mean that the file is corrupt or that it doesn't contain the custom after imports target needed for restore to read the project.</span></span> |
| <span data-ttu-id="4c3fc-204">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-204">**Example message**</span></span> | <span data-ttu-id="4c3fc-205">*'C:\a.csproj'에 대 한 프로젝트 정보를 읽을 수 없습니다. 프로젝트 파일이 올바르지 않거나 누락 된 대상으로 복원 하는 데 필요한 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-205">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

### <a name="nu1106"></a><span data-ttu-id="4c3fc-206">NU1106</span><span class="sxs-lookup"><span data-stu-id="4c3fc-206">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-207">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-207">**Issue**</span></span> | <span data-ttu-id="4c3fc-208">종속성 제약 조건을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-208">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="4c3fc-209">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-209">**Common causes**</span></span> | <span data-ttu-id="4c3fc-210">패키지 범위를 제한 하는 대신 패키지의 정확한 버전에 대 한 종속성을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-210">Packages contain dependency on exact versions of a package instead of open-ended ranges.</span></span> |
| <span data-ttu-id="4c3fc-211">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-211">**Example message**</span></span> | <span data-ttu-id="4c3fc-212">*{Id}에 대 한 충돌 하는 요청을 충족할 수 없습니다. {충돌 경로} 프레임 워크: {대상 그래프}*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-212">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |

<a name="nu1107"></a> 

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="4c3fc-213">NU1107 (이전에 NU1607)</span><span class="sxs-lookup"><span data-stu-id="4c3fc-213">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-214">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-214">**Issue**</span></span> | <span data-ttu-id="4c3fc-215">패키지 간에 종속성 제약 조건을 확인할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-215">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="4c3fc-216">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-216">**Common causes**</span></span> | <span data-ttu-id="4c3fc-217">정확한 버전에 대 한 종속성 제약 조건 사용 하 여 패키지에는 다른 패키지 버전을 필요에 따라 증가를 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-217">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> |
| <span data-ttu-id="4c3fc-218">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-218">**Example message**</span></span> | <span data-ttu-id="4c3fc-219">*NuGet.Versioning에 대 한 검색 버전 충돌 합니다. 이 문제를 해결 하려면 프로젝트에서 직접 패키지를 참조 합니다.<br/>  NuGet.Packaging 3.5.0 NuGet.Versioning (3.5.0 =)-><br/> NuGet.Configuration 4.0.0 NuGet.Versioning (4.0.0 =)->*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-219">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="4c3fc-220">NU1108 (이전에 NU1606)</span><span class="sxs-lookup"><span data-stu-id="4c3fc-220">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-221">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-221">**Issue**</span></span> | <span data-ttu-id="4c3fc-222">순환 종속성이 발견 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-222">A circular dependency was detected.</span></span> |
| <span data-ttu-id="4c3fc-223">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-223">**Common causes**</span></span> | <span data-ttu-id="4c3fc-224">패키지를 제대로 작성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-224">A package is authored incorrectly.</span></span> |
| <span data-ttu-id="4c3fc-225">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-225">**Example message**</span></span> | <span data-ttu-id="4c3fc-226">*순환 발견: A-B A->*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-226">*Cycle detected: A -> B -> A*</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="4c3fc-227">호환성 오류</span><span class="sxs-lookup"><span data-stu-id="4c3fc-227">Compatibility errors</span></span>

<span data-ttu-id="4c3fc-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="4c3fc-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="4c3fc-229">NU1201</span><span class="sxs-lookup"><span data-stu-id="4c3fc-229">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-230">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-230">**Issue**</span></span> | <span data-ttu-id="4c3fc-231">종속성 프로젝트는 현재 프로젝트와 호환 되는 프레임 워크를 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-231">A dependency project doesn't contain a framework compatible with the current project.</span></span> |
| <span data-ttu-id="4c3fc-232">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-232">**Common causes**</span></span> | <span data-ttu-id="4c3fc-233">프로젝트의 대상 프레임 워크에는 프로젝트가 보다 더 높은 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-233">The project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="4c3fc-234">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-234">**Example message**</span></span> | <span data-ttu-id="4c3fc-235">*프로젝트 서버 netstandard1.3와 호환 되지 않습니다 (합니다. NETStandard, Version = v1.3). 프로젝트 서버 지원:<br/> -netstandard1.6 (합니다. NETStandard, Version = v1.6)<br/> -netcoreapp1.0 (합니다. NETCoreApp, Version = v1.0)*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-235">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |

### <a name="nu1202"></a><span data-ttu-id="4c3fc-236">NU1202</span><span class="sxs-lookup"><span data-stu-id="4c3fc-236">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-237">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-237">**Issue**</span></span> | <span data-ttu-id="4c3fc-238">종속성 패키지는 프로젝트와 호환 되는 모든 자산을 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-238">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="4c3fc-239">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-239">**Common causes**</span></span> | <span data-ttu-id="4c3fc-240">패키지는 프로젝트의 대상 프레임 워크를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-240">The package doesn't support the project's target framework.</span></span> |
| <span data-ttu-id="4c3fc-241">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-241">**Example message**</span></span> | <span data-ttu-id="4c3fc-242">*패키지 System.ComponentModel.EventBasedAsync 4.0.11 netstandard1.3와 호환 되지 않습니다 (합니다. NETStandard, Version = v1.3). System.ComponentModel.EventBasedAsync 4.0.11 지원 패키지:<br/> -monoandroid10 (MonoAndroid, 버전 = v1.0)<br/> -monotouch10 (MonoTouch, Version = v1.0)<br/> -net45 (합니다. NETFramework, Version = v4.5)<br/> -netcore50 (합니다. NETCore, Version = v5.0)<br/> -netstandard1.0 (합니다. NETStandard, Version = v1.0)<br/> -portable net45 + win8 + w p 8 + wpa81 (합니다. NETPortable, 버전 = v0.0, 프로필 Profile259 =)<br/> -win8 (Windows, Version = v 8.0)<br/> -w p 8 (WindowsPhone, 버전 v 8.0 =)<br/> -wpa81 (이 WindowsPhoneApp, 버전 = v8.1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-242">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|

### <a name="nu1203"></a><span data-ttu-id="4c3fc-243">NU1203</span><span class="sxs-lookup"><span data-stu-id="4c3fc-243">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-244">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-244">**Issue**</span></span> | <span data-ttu-id="4c3fc-245">패키지는 프로젝트를 지원 하지 않습니다 `RuntimeIdentifier`합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-245">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="4c3fc-246">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-246">**Common causes**</span></span> | <span data-ttu-id="4c3fc-247">패키지는 현재 지원 하지 않는 `RuntimeIdentifier`합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-247">The package doesn't support the current `RuntimeIdentifier`.</span></span> <span data-ttu-id="4c3fc-248">변경 된 `RuntimeIdentifier` 필요한 경우 프로젝트에 사용 되는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-248">Change the `RuntimeIdentifier` values used in the project if needed.</span></span> |
| <span data-ttu-id="4c3fc-249">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-249">**Example message**</span></span> | <span data-ttu-id="4c3fc-250">*System.Example 1.0.0 net461에 a.dll에 대 한 compile-time 참조 어셈블리를 제공 하지만 호환 런타임 어셈블리가 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-250">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |

### <a name="nu1401"></a><span data-ttu-id="4c3fc-251">NU1401</span><span class="sxs-lookup"><span data-stu-id="4c3fc-251">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-252">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-252">**Issue**</span></span> | <span data-ttu-id="4c3fc-253">패키지 기능 또는 현재 설치 된 버전의 NuGet에서 지원 되는 프레임 워크에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-253">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="4c3fc-254">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-254">**Common causes**</span></span> | <span data-ttu-id="4c3fc-255">문제를 해결 하는 NuGet을 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-255">Upgrade NuGet to fix the issue.</span></span> |
| <span data-ttu-id="4c3fc-256">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-256">**Example message**</span></span> | <span data-ttu-id="4c3fc-257">*'NuGet.Versioning' 패키지에는 NuGet 클라이언트 버전 '5.0.0' 필요 이상 하지만 현재 NuGet 버전은 '4.3.0'. NuGet을 업그레이드 하려면 http://docs.nuget.org/consume/installing-nuget으로 이동 하십시오.*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-257">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'. To upgrade NuGet, please go to http://docs.nuget.org/consume/installing-nuget.*</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="4c3fc-258">잘못 된 입력된 경고</span><span class="sxs-lookup"><span data-stu-id="4c3fc-258">Invalid input warnings</span></span>

<span data-ttu-id="4c3fc-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="4c3fc-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="4c3fc-260">NU1501</span><span class="sxs-lookup"><span data-stu-id="4c3fc-260">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-261">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-261">**Issue**</span></span> | <span data-ttu-id="4c3fc-262">프로젝트 복원 작동 하려고에서 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-262">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="4c3fc-263">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-263">**Common causes**</span></span> | <span data-ttu-id="4c3fc-264">프로젝트는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-264">The project is missing.</span></span> |
| <span data-ttu-id="4c3fc-265">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-265">**Example message**</span></span> | <span data-ttu-id="4c3fc-266">*'C:\projects\a' 폴더에 복원할 프로젝트가 없습니다.*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-266">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |

### <a name="nu1502"></a><span data-ttu-id="4c3fc-267">NU1502</span><span class="sxs-lookup"><span data-stu-id="4c3fc-267">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-268">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-268">**Issue**</span></span> | <span data-ttu-id="4c3fc-269">`RuntimeSupports`잘못 된 프로필을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-269">`RuntimeSupports` contains an invalid profile.</span></span> |
| <span data-ttu-id="4c3fc-270">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-270">**Common causes**</span></span> | <span data-ttu-id="4c3fc-271">지원 프로필에 없습니다. 한 `runtime.json` 현재 종속성 패키지의 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-271">The supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span> |
| <span data-ttu-id="4c3fc-272">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-272">**Example message**</span></span> | <span data-ttu-id="4c3fc-273">*알 수 없는 호환성 프로필이: aaa*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-273">*Unknown Compatibility Profile: aaa*</span></span> |

### <a name="nu1503"></a><span data-ttu-id="4c3fc-274">NU1503</span><span class="sxs-lookup"><span data-stu-id="4c3fc-274">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-275">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-275">**Issue**</span></span> | <span data-ttu-id="4c3fc-276">종속성 프로젝트에는 NuGet의 복원 대상 가져오기 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-276">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="4c3fc-277">이 NU1105와 유사 하지만 프로젝트는 생략 여기 모든 복원 실패를 유발 하는 대신 무시 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-277">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="4c3fc-278">복잡 한 솔루션에서 종종 있습니다 다른 형식의 프로젝트 복원을 지원 하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-278">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="4c3fc-279">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-279">**Common causes**</span></span> | <span data-ttu-id="4c3fc-280">이 자동으로 복원 가져오기는 공통 props/대상 가져오지 않는 프로젝트에 대해 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-280">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="4c3fc-281">프로젝트를 복원할 필요가 없는 경우 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-281">If the project doesn't need to be restored this can be ignored.</span></span> |
| <span data-ttu-id="4c3fc-282">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-282">**Example message**</span></span> | <span data-ttu-id="4c3fc-283">*'C:\a.csproj' 프로젝트에 대 한 복원을 건너뜁니다. 프로젝트 파일이 올바르지 않거나 누락 된 대상으로 복원 하는 데 필요한 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-283">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="4c3fc-284">예기치 않은 패키지 버전 경고</span><span class="sxs-lookup"><span data-stu-id="4c3fc-284">Unexpected package version warnings</span></span>

<span data-ttu-id="4c3fc-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="4c3fc-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="4c3fc-286">NU1601</span><span class="sxs-lookup"><span data-stu-id="4c3fc-286">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-287">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-287">**Issue**</span></span> | <span data-ttu-id="4c3fc-288">지정 된 프로젝트 보다 높은 버전을 직접 프로젝트 종속성 추락 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-288">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="4c3fc-289">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-289">**Common causes**</span></span> | <span data-ttu-id="4c3fc-290">다른 종속성 패키지가 더 높은 버전에 필요한 및 패키지 추락.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-290">Another dependency package required a higher version and bumped the package up.</span></span> |
| <span data-ttu-id="4c3fc-291">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-291">**Example message**</span></span> | <span data-ttu-id="4c3fc-292">*지정 된 종속성은 NuGet.Versioning (> = 3.5.0) 이었지만 결과적으로 NuGet.Versioning 4.0.0 합니다.*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-292">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |

### <a name="nu1602"></a><span data-ttu-id="4c3fc-293">NU1602</span><span class="sxs-lookup"><span data-stu-id="4c3fc-293">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-294">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-294">**Issue**</span></span> | <span data-ttu-id="4c3fc-295">패키지 종속성은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-295">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="4c3fc-296">복원 찾을 수 없도록는 *가장 일치 하는*합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-296">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="4c3fc-297">각 복원 아래쪽으로 사용할 수 있는 더 낮은 버전을 검색 하려고 이동 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-297">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="4c3fc-298">즉, 복원 될 때마다 사용자 패키지 폴더에 이미 존재 하는 패키지를 사용 하는 대신 모든 소스를 확인 하려면 온라인 전환 되는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-298">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="4c3fc-299">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-299">**Common causes**</span></span> | <span data-ttu-id="4c3fc-300">이 일반적으로 오류를 제작 하는 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-300">This is usually a package authoring error.</span></span> |
| <span data-ttu-id="4c3fc-301">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-301">**Example message**</span></span> | <span data-ttu-id="4c3fc-302">*NuGet.Packaging 4.0.0 NuGet.Versioning (> 3.5.0) 종속성에 대 한는 경계값을 제공 하지 않습니다. 3.6.0의 일부만 가장 일치 하는 해결 되었습니다.*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-302">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |

### <a name="nu1603"></a><span data-ttu-id="4c3fc-303">NU1603</span><span class="sxs-lookup"><span data-stu-id="4c3fc-303">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-304">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-304">**Issue**</span></span> | <span data-ttu-id="4c3fc-305">패키지 종속성 지정 버전을 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-305">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="4c3fc-306">패키지에 대해 작성 된에서 다른 상위 버전 대신 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-306">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="4c3fc-307">즉, 복원이 찾을 수 없습니다는 *가장 일치 하는*합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-307">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="4c3fc-308">각 복원 아래쪽으로 사용할 수 있는 더 낮은 버전을 검색 하려고 이동 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="4c3fc-309">즉, 복원 될 때마다 사용자 패키지 폴더에 이미 존재 하는 패키지를 사용 하는 대신 모든 소스를 확인 하려면 온라인 전환 되는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="4c3fc-310">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-310">**Common causes**</span></span> | <span data-ttu-id="4c3fc-311">패키지 소스에서 예상된 하한값 버전을 포함 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-311">The package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="4c3fc-312">예상 패키지 해제 되지 않은 경우 오류를 제작 하는 패키지를 수 있습니다이.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-312">If the package expected has not been released then this may be a package authoring error.</span></span> |
| <span data-ttu-id="4c3fc-313">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-313">**Example message**</span></span> | <span data-ttu-id="4c3fc-314">NuGet.Packaging 4.0.0 NuGet.Versioning에 따라 달라 집니다 (> = 4.0.0) 4.0.0를 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-314">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="4c3fc-315">5.0.0의 일부만 가장 일치 하는 해결 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-315">An approximate best match of 5.0.0 was resolved.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="4c3fc-316">NU1604</span><span class="sxs-lookup"><span data-stu-id="4c3fc-316">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-317">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-317">**Issue**</span></span> | <span data-ttu-id="4c3fc-318">프로젝트 종속성 배열은 하 한을 정의 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-318">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="4c3fc-319">즉, 복원이 찾을 수 없습니다는 *가장 일치 하는*합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="4c3fc-320">각 복원 아래쪽으로 사용할 수 있는 더 낮은 버전을 검색 하려고 이동 수입니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="4c3fc-321">즉, 복원 될 때마다 사용자 패키지 폴더에 이미 존재 하는 패키지를 사용 하는 대신 모든 소스를 확인 하려면 온라인 전환 되는 것을 의미 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="4c3fc-322">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-322">**Common causes**</span></span> | <span data-ttu-id="4c3fc-323">프로젝트의 *PackageReference* *버전* 특성 배열은 하 한을 포함 하도록 업데이트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-323">The project's *PackageReference* *Version* attribute should be updated to include a lower bound.</span></span> |
| <span data-ttu-id="4c3fc-324">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-324">**Example message**</span></span> | <span data-ttu-id="4c3fc-325">*종속성 NuGet.Versioning 프로젝트 (< = 9.0.0) doe는 경계값을 포함 하지 합니다. 일치 복원 결과 보장 하는 종속성의 버전에 배열은 하 한을 포함 합니다.*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-325">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |

### <a name="nu1605"></a><span data-ttu-id="4c3fc-326">NU1605</span><span class="sxs-lookup"><span data-stu-id="4c3fc-326">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-327">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-327">**Issue**</span></span> | <span data-ttu-id="4c3fc-328">종속성 패키지에는 궁극적으로 해결 하는 복원 보다 더 높은 버전의 패키지에 버전 제약 조건을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-328">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> |
| <span data-ttu-id="4c3fc-329">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-329">**Common causes**</span></span> | <span data-ttu-id="4c3fc-330">패키지를 확인할 때 가장 가까운 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-330">Nearest wins when resolving packages.</span></span> <span data-ttu-id="4c3fc-331">그래프에 할수록 패키지 먼 패키지를 무시 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-331">A nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="4c3fc-332">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-332">**Example message**</span></span> | <span data-ttu-id="4c3fc-333">*패키지가 다운 그레이드를 발견 했습니다: 3.5.0 4.0.0에서 NuGet.Versioning 합니다. 다른 버전을 선택 하는 프로젝트에서 직접 패키지를 참조 합니다.<br/>  NuGet.Packaging 3.5.0 NuGet.Versioning 3.5.0-><br/> NuGet.Commands 4.0.0 NuGet.Configuration-> 4.0.0 NuGet.Versioning 4.0.0->*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-333">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="4c3fc-334">해결 프로그램이 충돌 경고</span><span class="sxs-lookup"><span data-stu-id="4c3fc-334">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="4c3fc-335">NU1608</span><span class="sxs-lookup"><span data-stu-id="4c3fc-335">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-336">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-336">**Issue**</span></span> | <span data-ttu-id="4c3fc-337">해결 패키지 종속성 제약 조건을 허용 된 것 보다 더 높습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-337">A resolve package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="4c3fc-338">일부 경우에이 의도적인와 경고가 표시 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-338">In some cases this is intentional and the warning can be suppressed.</span></span> |
| <span data-ttu-id="4c3fc-339">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-339">**Common causes**</span></span> | <span data-ttu-id="4c3fc-340">프로젝트에서 직접 참조 하는 패키지에는 다른 패키지에서 제약 조건 종속성 보다 우선 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-340">A package referenced directly by a project will override dependency constraints from other packages.</span></span>   |
| <span data-ttu-id="4c3fc-341">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-341">**Example message**</span></span> | <span data-ttu-id="4c3fc-342">*외부 종속성 제약 조건에서 검색 된 패키지 버전: x 1.0.0 y (1.0.0 =) 이어야 하는데 버전 2.0.0 y 해결 되었습니다.*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-342">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="4c3fc-343">패키지 대체 (fallback) 경고</span><span class="sxs-lookup"><span data-stu-id="4c3fc-343">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="4c3fc-344">NU1701</span><span class="sxs-lookup"><span data-stu-id="4c3fc-344">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-345">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-345">**Issue**</span></span> | <span data-ttu-id="4c3fc-346">*PackageTargetFallback/AssetTargetFallback* 패키지에서 자산을 선택 하는 데 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-346">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span></span> <span data-ttu-id="4c3fc-347">이 경고를 사용자에 게 알리는 자산 100% 호환 되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-347">This is a warning to let the user know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="4c3fc-348">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-348">**Common causes**</span></span> | <span data-ttu-id="4c3fc-349">패키지는 프로젝트 프레임 워크를 지원 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-349">The package doesn't support the project framework.</span></span> |
| <span data-ttu-id="4c3fc-350">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-350">**Example message**</span></span> | <span data-ttu-id="4c3fc-351">*패키지 'NuGet.Versioning'를 사용 하 여 '노트북 net45 + win8' 대신 프로젝트 대상 프레임 워크 'netstandard1.5' 복원 되었습니다. 이 패키지는 프로젝트와 완전히 호환 하지 못할 수 있습니다.*</span><span class="sxs-lookup"><span data-stu-id="4c3fc-351">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="4c3fc-352">피드 경고</span><span class="sxs-lookup"><span data-stu-id="4c3fc-352">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="4c3fc-353">NU1801</span><span class="sxs-lookup"><span data-stu-id="4c3fc-353">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-354">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-354">**Issue**</span></span> | <span data-ttu-id="4c3fc-355">피드를 읽을 때 오류가 발생 했습니다 때 `IgnoreFailedSources` 설정을 true로 변환 하는 치명적이 지 않은 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-355">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="4c3fc-356">이 모든 메시지를 포함할 수 이며 일반 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-356">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="4c3fc-357">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-357">**Common causes**</span></span> | <span data-ttu-id="4c3fc-358">원본이 올바르지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-358">The source is invalid.</span></span> |
| <span data-ttu-id="4c3fc-359">**예제 메시지**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-359">**Example message**</span></span> | <span data-ttu-id="4c3fc-360">N/A</span><span class="sxs-lookup"><span data-stu-id="4c3fc-360">n/a</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="4c3fc-361">NuGet 내부 오류 및 경고</span><span class="sxs-lookup"><span data-stu-id="4c3fc-361">NuGet internal errors and warnings</span></span>

<span data-ttu-id="4c3fc-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="4c3fc-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="4c3fc-363">NU1000</span><span class="sxs-lookup"><span data-stu-id="4c3fc-363">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-364">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-364">**Issue**</span></span> | <span data-ttu-id="4c3fc-365">NuGet에서 비 특정 내부 오류입니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-365">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="4c3fc-366">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-366">**Common causes**</span></span> | <span data-ttu-id="4c3fc-367">자세한 내용은 로그를 확인 하십시오</span><span class="sxs-lookup"><span data-stu-id="4c3fc-367">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="4c3fc-368">NU1500</span><span class="sxs-lookup"><span data-stu-id="4c3fc-368">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="4c3fc-369">**문제**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-369">**Issue**</span></span> | <span data-ttu-id="4c3fc-370">NuGet에서 비 특정 내부 경고 합니다.</span><span class="sxs-lookup"><span data-stu-id="4c3fc-370">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="4c3fc-371">**일반적인 원인**</span><span class="sxs-lookup"><span data-stu-id="4c3fc-371">**Common causes**</span></span> | <span data-ttu-id="4c3fc-372">자세한 내용은 로그를 확인 하십시오</span><span class="sxs-lookup"><span data-stu-id="4c3fc-372">Check the logs for more information</span></span> |
