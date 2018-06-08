---
title: NuGet 패키지의 시험판 버전
description: 시험판 패키지를 빌드하기 위한 지침
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 498509e03a794878eeeadd46d499521d19415600
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818375"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="aa106-103">시험판 패키지 빌드</span><span class="sxs-lookup"><span data-stu-id="aa106-103">Building pre-release packages</span></span>

<span data-ttu-id="aa106-104">새 버전 번호를 포함하는 업데이트된 패키지를 릴리스할 때마다 NuGet은 해당 패키지를 Visual Studio 내의 패키지 관리자 UI에 표시된 "안정적인 최신 릴리스"로 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![안정적인 최신 릴리스를 보여주는 패키지 관리자 UI](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="aa106-106">안정적인 릴리스란 프로덕션 환경에서 사용할 수 있을 만큼 안정적인 릴리스입니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="aa106-107">안정적인 최신 릴리스는 패키지를 업데이트하거나 복원하는 동안 설치됩니다([패키지 다시 설치 및 업데이트](../consume-packages/reinstalling-and-updating-packages.md)에 설명된 대로 제약 조건 적용).</span><span class="sxs-lookup"><span data-stu-id="aa106-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="aa106-108">소프트웨어 릴리스 주기를 지원하기 위해 NuGet 1.6 이상을 사용하면 시험판 패키지의 배포에 허용됩니다. 여기서 버전 번호에는 `-alpha`, `-beta` 또는 `-rc`와 같은 유의적 버전 접미사가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="aa106-109">자세한 내용은 [패키지 버전 관리](../reference/package-versioning.md#pre-release-versions)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aa106-109">For more information, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="aa106-110">두 가지 방법으로 이러한 버전을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-110">You can specify such versions in two ways:</span></span>

- <span data-ttu-id="aa106-111">`.nuspec` 파일: `version` 요소에 의미 체계 버전 접미사의 포함:</span><span class="sxs-lookup"><span data-stu-id="aa106-111">`.nuspec` file: include the semantic version suffix in the `version` element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

- <span data-ttu-id="aa106-112">어셈블리 특성: Visual Studio 프로젝트에서 패키지를 빌드할 때(`.csproj` 또는 `.vbproj`) `AssemblyInformationalVersionAttribute`를 사용하여 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-112">Assembly attributes: when building a package from a Visual Studio project (`.csproj` or `.vbproj`), use the `AssemblyInformationalVersionAttribute` to specify the version:</span></span>

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    <span data-ttu-id="aa106-113">NuGet은 `AssemblyVersion` 특성에 지정된 값 대신 이 값을 선택합니다. 여기서는 유의적 버전을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-113">NuGet picks up this value instead of the one specified in the `AssemblyVersion` attribute, which does not support semantic versioning.</span></span>

<span data-ttu-id="aa106-114">안정적인 버전을 출시할 준비가 되면 접미사를 제거합니다. 그러면 패키지가 시험판 버전보다 우선 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-114">When you’re ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="aa106-115">다시 [패키지 버전 관리](../reference/package-versioning.md#pre-release-versions)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aa106-115">Again, see [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="aa106-116">시험판 패키지 설치 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="aa106-116">Installing and updating pre-release packages</span></span>

<span data-ttu-id="aa106-117">기본적으로 NuGet은 패키지에서 작업할 때 시험판 버전을 포함하지 않지만 다음과 같이 이 동작을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-117">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="aa106-118">**Visual Studio의 패키지 관리자 UI**: **NuGet 패키지 관리** UI에서 **시험판 포함** 확인란을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-118">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Visual Studio의 시험판 포함 확인란](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="aa106-120">이 확인란을 설정 또는 해제하면 패키지 관리자 UI 및 설치할 수 있는 사용 가능한 버전 목록을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-120">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="aa106-121">**패키지 관리자 콘솔**: `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` 및 `Update-Package` 명령과 함께 `-IncludePrerelease` 스위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-121">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="aa106-122">[PowerShell 참조](../tools/powershell-reference.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aa106-122">Refer to the [PowerShell Reference](../tools/powershell-reference.md).</span></span>

- <span data-ttu-id="aa106-123">**NuGet CLI**: `install`, `update`, `delete` 및 `mirror` 명령과 함께 `-prerelease` 스위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-123">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="aa106-124">[NuGet CLI 참조](../tools/nuget-exe-cli-reference.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="aa106-124">Refer to the [NuGet CLI reference](../tools/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="aa106-125">유의적 버전</span><span class="sxs-lookup"><span data-stu-id="aa106-125">Semantic versioning</span></span>

<span data-ttu-id="aa106-126">[유의적 버전 또는 SemVer 규칙](http://semver.org/spec/v1.0.0.html)은 버전 번호의 문자열을 활용하여 기본 코드의 의미를 전달하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-126">The [Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey they meaning of the underlying code.</span></span>

<span data-ttu-id="aa106-127">이 규칙에서 각 버전에는 다음과 같은 의미를 포함한 세 부분인 `Major.Minor.Patch`가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-127">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="aa106-128">`Major`: 주요 변경 사항</span><span class="sxs-lookup"><span data-stu-id="aa106-128">`Major`: Breaking changes</span></span>
- <span data-ttu-id="aa106-129">`Minor`: 이전 버전과 호환되는 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="aa106-129">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="aa106-130">`Patch`: 이전 버전과 호환되는 버그 수정에만 해당</span><span class="sxs-lookup"><span data-stu-id="aa106-130">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="aa106-131">시험판 버전은 패치 번호 뒤에 하이픈과 문자열을 추가하여 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-131">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="aa106-132">기술적으로 설명하자면 하이픈 뒤의 *모든* 문자열을 사용할 수 없으며 NuGet은 패키지를 시험판으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-132">Technically speaking, you can use *any *string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="aa106-133">그런 다음 NuGet은 해당 UI에 전체 버전 번호를 표시하여 소비자가 스스로 의미를 해석하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-133">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="aa106-134">이 점을 고려하여 일반적으로 다음과 같이 인식된 명명 규칙을 따르는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-134">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="aa106-135">`-alpha`: 일반적으로 개발 중 및 실험에 사용되는 알파 버전</span><span class="sxs-lookup"><span data-stu-id="aa106-135">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="aa106-136">`-beta`: 일반적으로 다음에 계획된 릴리스에 대한 기능 완료인 베타 릴리스이지만 알려진 버그를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-136">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="aa106-137">`-rc`: 일반적으로 심각한 버그가 발생하지 않는 한 잠재적으로 최종적(안정적)인 릴리스인 릴리스 후보입니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-137">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="aa106-138">NuGet 4.3.0+는 `1.0.1-build.23`과 마찬가지로 점 표기법을 사용하는 시험판 번호를 지원하는 [유의적 버전 v2.0.0](http://semver.org/spec/v2.0.0.html)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-138">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="aa106-139">NuGet 4.3.0 이전 버전에서는 점 표기법이 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-139">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="aa106-140">이전 버전의 NuGet에서는 `1.0.1-build23` 같은 양식을 사용할 수 있지만 이는 항상 시험판 버전으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-140">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="aa106-141">그러나 어떤 접미사를 사용하든지 NuGet은 알파벳 역순으로 우선 순위를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-141">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

<span data-ttu-id="aa106-142">표시된 대로 접미사가 없는 버전은 항상 시험판 버전보다 우선합니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-142">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span> <span data-ttu-id="aa106-143">또한 두 자리 숫자(이상)를 사용할 수 있는 시험판 태그에서 숫자 접미사를 사용하는 경우 앞에 오는 숫자 0(예: beta01 및 beta05)을 사용하여 숫자가 커지는 경우 올바르게 정렬하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa106-143">Note also that if you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta01 and beta05 to ensure that they sort correctly when the numbers get larger.</span></span>
