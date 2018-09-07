---
title: NuGet 패키지 종속성 확인
description: NuGet 패키지의 종속성을 확인하여 NuGet 2.x 및 NuGet 3.x 이상에 모두 설치하는 프로세스를 자세히 설명합니다.
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: cdbe13df04bb27091b684a4ae27b0e751da1098f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549036"
---
# <a name="how-nuget-resolves-package-dependencies"></a><span data-ttu-id="f4bc5-103">NuGet에서 패키지 종속성을 확인하는 방법</span><span class="sxs-lookup"><span data-stu-id="f4bc5-103">How NuGet resolves package dependencies</span></span>

<span data-ttu-id="f4bc5-104">[restore](../consume-packages/package-restore.md) 프로세스의 일부로 설치하는 것을 포함하여 패키지를 설치하거나 다시 설치할 때마다 NuGet은 첫 번째 패키지가 종속된 모든 추가 패키지도 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-104">Any time a package is installed or reinstalled, which includes being installed as part of a [restore](../consume-packages/package-restore.md) process, NuGet also installs any additional packages on which that first package depends.</span></span>

<span data-ttu-id="f4bc5-105">그런 다음 이러한 직접적인 종속성에도 자체의 종속성이 있을 수 있으며, 이에 따라 임의의 수준까지 계속 종속될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-105">Those immediate dependencies might then also have dependencies on their own, which can continue to an arbitrary depth.</span></span> <span data-ttu-id="f4bc5-106">이렇게 하면 패키지 간의 관계가 모든 수준임을 설명하는 *종속성 그래프*를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-106">This produces what's called a *dependency graph* that describes the relationships between packages at all levels.</span></span>

<span data-ttu-id="f4bc5-107">여러 패키지의 종속성이 같은 경우 동일한 패키지 ID가 그래프에 여러 번 표시될 수 있으며, 잠재적으로 서로 다른 버전 제약 조건이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-107">When multiple packages have the same dependency, then the same package ID can appear in the graph multiple times, potentially with different version constraints.</span></span> <span data-ttu-id="f4bc5-108">그러나 프로젝트에서 특정 패키지의 한 버전만 사용할 수 있으므로 NuGet은 사용할 버전을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-108">However, only one version of a given package can be used in a project, so NuGet must choose which version is used.</span></span> <span data-ttu-id="f4bc5-109">정확한 프로세스는 사용되는 패키지 관리 형식에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-109">The exact process depends on the package management format being used.</span></span>

## <a name="dependency-resolution-with-packagereference"></a><span data-ttu-id="f4bc5-110">PackageReference를 사용하여 종속성 확인</span><span class="sxs-lookup"><span data-stu-id="f4bc5-110">Dependency resolution with PackageReference</span></span>

<span data-ttu-id="f4bc5-111">PackageReference 형식을 사용하여 패키지를 프로젝트에 설치하는 경우 NuGet은 적절한 파일에서 단순 패키지 그래프에 대한 참조를 추가하고 충돌을 미리 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-111">When installing packages into projects using the PackageReference format, NuGet adds references to a flat package graph in the appropriate file and resolves conflicts ahead of time.</span></span> <span data-ttu-id="f4bc5-112">이 프로세스는 *전이적 복원*이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-112">This process is referred to as *transitive restore*.</span></span> <span data-ttu-id="f4bc5-113">패키지를 다시 설치하거나 복원하면 그래프에 나열된 패키지가 다운로드되어 더 빠르고 예측 가능한 빌드가 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-113">Reinstalling or restoring packages is then a process of downloading the packages listed in the graph, resulting in faster and more predictable builds.</span></span> <span data-ttu-id="f4bc5-114">또한 2.8.\*와 같은 와일드카드(유동) 버전을 활용하여 클라이언트 컴퓨터 및 빌드 서버에서 비용이 많이 들고 오류가 발생하기 쉬운 `nuget update` 호출을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-114">You can also take advantage of wildcard (floating) versions, such as 2.8.\*, avoiding expensive and error prone calls to `nuget update` on the client machines and build servers.</span></span>

<span data-ttu-id="f4bc5-115">NuGet 복원 프로세스가 빌드하기 전에 실행되면, 먼저 메모리에서 종속성을 확인한 다음, PackageReference를 사용하여 결과 그래프를 프로젝트의 `obj` 폴더에서 `project.assets.json`이라는 파일에 씁니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-115">When the NuGet restore process runs prior to a build, it resolves dependencies first in memory, then writes the resulting graph to a file called `project.assets.json` in the `obj` folder of a project using PackageReference.</span></span> <span data-ttu-id="f4bc5-116">그러면 MSBuild에서 이 파일을 읽고 잠재적인 참조를 찾을 수 있는 폴더의 집합으로 해당 파일을 변환한 다음 메모리의 프로젝트 트리에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-116">MSBuild then reads this file and translates it into a set of folders where potential references can be found, and then adds them to the project tree in memory.</span></span>

<span data-ttu-id="f4bc5-117">잠금 파일은 임시적이며 원본 제어에 추가하면 안됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-117">The lock file is temporary and should not be added to source control.</span></span> <span data-ttu-id="f4bc5-118">`.gitignore`과 `.tfignore` 모두에서 기본적으로 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-118">It's listed by default in both `.gitignore` and `.tfignore`.</span></span> <span data-ttu-id="f4bc5-119">[패키지 및 원본 제어](packages-and-source-control.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-119">See [Packages and source control](packages-and-source-control.md).</span></span>

### <a name="dependency-resolution-rules"></a><span data-ttu-id="f4bc5-120">종속성 확인 규칙</span><span class="sxs-lookup"><span data-stu-id="f4bc5-120">Dependency resolution rules</span></span>

<span data-ttu-id="f4bc5-121">전이적 복원은 종속성을 확인하는 네 가지 주요 규칙, 즉 적용 가능한 가장 낮은 버전, 유동적인 버전, 가장 가까운 성공 및 사촌 종속성을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-121">Transitive restore applies four main rules to resolve dependencies: lowest applicable version, floating versions, nearest-wins, and cousin dependencies.</span></span>

<a name="lowest-applicable-version"></a>

#### <a name="lowest-applicable-version"></a><span data-ttu-id="f4bc5-122">적용 가능한 가장 낮은 버전</span><span class="sxs-lookup"><span data-stu-id="f4bc5-122">Lowest applicable version</span></span>

<span data-ttu-id="f4bc5-123">적용 가능한 가장 낮은 버전 규칙은 패키지의 종속성으로 정의된 대로 가장 낮은 버전의 패키지를 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-123">The lowest applicable version rule restores the lowest possible version of a package as defined by its dependencies.</span></span> <span data-ttu-id="f4bc5-124">[유동적인 버전](#floating-versions)으로 선언되지 않은 경우 응용 프로그램 또는 클래스 라이브러리에 대한 종속성에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-124">It also applies to dependencies on the application or the class library unless declared as [floating](#floating-versions).</span></span>

<span data-ttu-id="f4bc5-125">예를 들어 다음 그림에서 1.0-beta는 1.0보다 낮은 것으로 간주되므로 NuGet은 1.0 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-125">In the following figure, for example, 1.0-beta is considered lower than 1.0 so NuGet chooses the 1.0 version:</span></span>

![적용 가능한 가장 낮은 버전 선택](media/projectJson-dependency-1.png)

<span data-ttu-id="f4bc5-127">다음 그림에서 2.1 버전은 피드에서 사용할 수 없지만 버전 제약 조건이 2.1 이상이므로 이 경우 NuGet에서 찾을 수 있는 버전 중 다음으로 가장 낮은 버전인 2.2를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-127">In the next figure, version 2.1 is not available on the feed but because the version constraint is >= 2.1 NuGet picks the next lowest version it can find, in this case 2.2:</span></span>

![피드에서 사용 가능한 버전 중 다음으로 가장 낮은 버전 선택](media/projectJson-dependency-2.png)

<span data-ttu-id="f4bc5-129">응용 프로그램이 피드에서 사용할 수 없는 정확한 버전 번호(예: 1.2)를 지정하면, 패키지를 설치하거나 복원할 때 오류로 인해 NuGet이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-129">When an application specifies an exact version number, such as 1.2, that is not available on the feed, NuGet fails with an error when attempting to install or restore the package:</span></span>

![정확한 패키지 버전을 사용할 수 없는 경우 NuGet에서 오류 생성](media/projectJson-dependency-3.png)

<a name="floating-versions"></a>

#### <a name="floating-wildcard-versions"></a><span data-ttu-id="f4bc5-131">유동적인(와일드카드) 버전</span><span class="sxs-lookup"><span data-stu-id="f4bc5-131">Floating (wildcard) versions</span></span>

<span data-ttu-id="f4bc5-132">유동 또는 와일드카드 종속성 버전은 \* 와일드카드로 지정됩니다(예: 6.0.\*).</span><span class="sxs-lookup"><span data-stu-id="f4bc5-132">A floating or wildcard dependency version is specified with the \* wildcard, as with 6.0.\*.</span></span> <span data-ttu-id="f4bc5-133">이 버전 사양에는 "최신 6.0.x 버전 사용"이 나와 있습니다. 4.\*는 "최신 4.x 버전 사용"을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-133">This version specification says "use the latest 6.0.x version"; 4.\* means "use the latest 4.x version."</span></span> <span data-ttu-id="f4bc5-134">와일드카드를 사용하면 소비 응용 프로그램(또는 패키지)을 변경하지 않고도 종속성 패키지가 계속 진화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-134">Using a wildcard allows a dependency package to continue evolving without requiring a change to the consuming application (or package).</span></span>

<span data-ttu-id="f4bc5-135">와일드카드를 사용하면 NuGet에서 버전 패턴과 일치하는 패키지의 가장 높은 버전을 확인합니다. 예를 들어 6.0.\*는 6.0으로 시작하는 패키지의 버전 중 가장 높은 버전을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-135">When using a wildcard, NuGet resolves the highest version of a package that matches the version pattern, for example 6.0.\* gets the highest version of a package that starts with 6.0:</span></span>

![유동적인 6.0.\* 버전 요구 시 6.0.1 버전 선택](media/projectJson-dependency-4.png)

> [!Note]
> <span data-ttu-id="f4bc5-137">와일드카드 및 시험판 버전의 동작에 대한 자세한 내용은 [패키지 버전 관리](../reference/package-versioning.md#version-ranges-and-wildcards)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-137">For information on the behavior of wildcards and pre-release versions, see [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>


<a name="nearest-wins"></a>

#### <a name="nearest-wins"></a><span data-ttu-id="f4bc5-138">가장 가까운 성공</span><span class="sxs-lookup"><span data-stu-id="f4bc5-138">Nearest wins</span></span>

<span data-ttu-id="f4bc5-139">응용 프로그램에 대한 패키지 그래프에 동일한 패키지의 다른 버전이 포함된 경우 NuGet은 그래프에서 응용 프로그램과 가장 가까운 패키지를 선택하고 다른 모든 패키지는 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-139">When the package graph for an application contains different versions of the same package, NuGet chooses the package that's closest to the application in the graph and ignores all others.</span></span> <span data-ttu-id="f4bc5-140">이 동작을 통해 응용 프로그램에서 종속성 그래프의 특정 패키지 버전을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-140">This behavior allows an application to override any particular package version in the dependency graph.</span></span>

<span data-ttu-id="f4bc5-141">아래 예에서 응용 프로그램은 버전 제약 조건이 2.0 이상인 B 패키지에 직접 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-141">In the example below, the application depends directly on Package B with a version constraint of >=2.0.</span></span> <span data-ttu-id="f4bc5-142">또한 이 응용 프로그램은 B 패키지에 종속된 A 패키지에도 종속되지만 1.0 이상인 제약 조건을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-142">The application also depends on Package A which in turn also depends on Package B, but with a >=1.0 constraint.</span></span> <span data-ttu-id="f4bc5-143">B 패키지 2.0에 대한 종속성이 그래프의 응용 프로그램에 더 가깝기 때문에 해당 버전이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-143">Because the dependency on Package B 2.0 is nearer to the application in the graph, that version is used:</span></span>

![가장 가까운 성공 규칙을 사용하는 응용 프로그램](media/projectJson-dependency-5.png)

>[!Warning]
> <span data-ttu-id="f4bc5-145">가장 가까운 성공 규칙으로 인해 패키지 버전의 다운그레이드가 발생할 수 있으므로 그래프에서 다른 종속성이 손상될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-145">The Nearest Wins rule can result in a downgrade of the package version, thus potentially breaking other dependencies in the graph.</span></span> <span data-ttu-id="f4bc5-146">따라서 이 규칙은 사용자에게 경고하는 경고와 함께 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-146">Hence this rule is applied with a warning to alert the user.</span></span>

<span data-ttu-id="f4bc5-147">또한 지정된 종속성이 무시되면 NuGet에서 그래프의 해당 분기에 있는 나머지 모든 종속성도 무시하기 때문에 이 규칙에서 큰 종속성 그래프(예: BCL 패키지의 경우)를 사용하여 효율성을 높입니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-147">This rule also results in greater efficiency with a large dependency graph (such as those with the BCL packages) because once a given dependency is ignored, NuGet also ignores all remaining dependencies on that branch of the graph.</span></span> <span data-ttu-id="f4bc5-148">예를 들어 아래 다이어그램에서 C 패키지 2.0이 사용되었기 때문에 NuGet은 이전 버전의 C 패키지를 참조하는 그래프의 모든 분기를 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-148">In the diagram below, for example, because Package C 2.0 is used, NuGet ignores any branches in the graph that refer to an older version of Package C:</span></span>

![NuGet이 그래프에서 패키지를 무시하는 경우 무시되는 전체 분기](media/projectJson-dependency-6.png)

<a name="cousin-dependencies"></a>

#### <a name="cousin-dependencies"></a><span data-ttu-id="f4bc5-150">사촌 종속성</span><span class="sxs-lookup"><span data-stu-id="f4bc5-150">Cousin dependencies</span></span>

<span data-ttu-id="f4bc5-151">응용 프로그램이 그래프의 동일한 거리에서 서로 다른 패키지 버전을 참조하는 경우 NuGet은 모든 버전 요구 사항(예: [적용 가능한 가장 낮은 버전](#lowest-applicable-version) 및 [유동적인 버전](#floating-versions) 규칙)을 충족하는 가장 낮은 버전을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-151">When different package versions are referred to at the same distance in the graph from the application, NuGet uses the lowest version that satisfies all version requirements (as with the [lowest applicable version](#lowest-applicable-version) and [floating versions](#floating-versions) rules).</span></span> <span data-ttu-id="f4bc5-152">예를 들어 아래 이미지에서 B 패키지의 2.0 버전은 1.0 이상의 다른 제약 조건을 충족하므로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-152">In the image below, for example, version 2.0 of Package B satisfies the other >=1.0 constraint, and is thus used:</span></span>

![모든 제약 조건을 충족하는 하위 버전을 사용하여 사촌 종속성 확인](media/projectJson-dependency-7.png)

<span data-ttu-id="f4bc5-154">모든 버전 요구 사항을 충족할 수 없는 경우도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-154">In some cases, it's not possible to meet all version requirements.</span></span> <span data-ttu-id="f4bc5-155">아래와 같이 A 패키지에는 정확히 B 패키지 1.0이 필요하고 C 패키지에는 B 패키지 2.0 이상이 필요한 경우, NuGet에서 종속성을 확인할 수 없으며 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-155">As shown below, if Package A requires exactly Package B 1.0 and Package C requires Package B >=2.0, then NuGet cannot resolve the dependencies and gives an error.</span></span>

![정확한 버전 요구 사항으로 인해 확인할 수 없는 종속성](media/projectJson-dependency-8.png)

<span data-ttu-id="f4bc5-157">이러한 상황에서는 [가장 가까운 성공](#nearest-wins) 규칙이 적용되도록 최상위 소비자(응용 프로그램 또는 패키지)가 B 패키지에 자체의 직접적인 종속성을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-157">In these situations, the top-level consumer (the application or package) should add its own direct dependency on Package B so that the [Nearest Wins](#nearest-wins) rule applies.</span></span>

## <a name="dependency-resolution-with-packagesconfig"></a><span data-ttu-id="f4bc5-158">packages.config를 사용하여 종속성 확인</span><span class="sxs-lookup"><span data-stu-id="f4bc5-158">Dependency resolution with packages.config</span></span>

<span data-ttu-id="f4bc5-159">`packages.config`를 사용하면 프로젝트의 종속성이 단순 목록으로 `packages.config`에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-159">With `packages.config`, a project's dependencies are written to `packages.config` as a flat list.</span></span> <span data-ttu-id="f4bc5-160">이러한 패키지의 모든 종속성도 동일한 목록에 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-160">Any dependencies of those packages are also written in the same list.</span></span> <span data-ttu-id="f4bc5-161">패키지가 설치되면 NuGet에서 `.csproj` 파일, `app.config`, `web.config` 및 기타 개별 파일을 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-161">When packages are installed, NuGet might also modify the `.csproj` file, `app.config`, `web.config`, and other individual files.</span></span>

<span data-ttu-id="f4bc5-162">`packages.config`를 사용하면 NuGet은 각각의 개별 패키지를 설치하는 동안 종속성 충돌을 해결하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-162">With `packages.config`, NuGet attempts to resolve dependency conflicts during the installation of each individual package.</span></span> <span data-ttu-id="f4bc5-163">즉 A 패키지가 설치되고 B 패키지에 종속되어 있고 B 패키지가 이미 다른 패키지의 종속성으로 `packages.config`에 나열되어 있는 경우, NuGet은 요청된 B 패키지의 버전을 비교하고 모든 버전 제약 조건을 충족하는 버전을 찾으려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-163">That is, if Package A is being installed and depends on Package B, and Package B is already listed in `packages.config` as a dependency of something else, NuGet compares the versions of Package B being requested and attempts to find a version that satisfies all version constraints.</span></span> <span data-ttu-id="f4bc5-164">특히 NuGet은 종속성을 충족하는 더 낮은 *major.minor* 버전을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-164">Specifically, NuGet selects the lower *major.minor* version that satisfies dependencies.</span></span>

<span data-ttu-id="f4bc5-165">기본적으로 NuGet 2.8은 가장 낮은 패치 버전을 찾습니다([NuGet 2.8 릴리스 정보](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies) 참조).</span><span class="sxs-lookup"><span data-stu-id="f4bc5-165">By default, NuGet 2.8 looks for the lowest patch version (see [NuGet 2.8 release notes](../release-notes/nuget-2.8.md#patch-resolution-for-dependencies)).</span></span> <span data-ttu-id="f4bc5-166">`Nuget.Config`의 `DependencyVersion` 특성 및 명령줄의 `-DependencyVersion` 스위치를 통해 이 설정을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-166">You can control this setting through the `DependencyVersion` attribute in `Nuget.Config` and the `-DependencyVersion` switch on the command line.</span></span>  

<span data-ttu-id="f4bc5-167">더 큰 종속성 그래프의 경우 종속성을 확인하기 위한 `packages.config` 프로세스가 복잡해집니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-167">The `packages.config` process for resolving dependencies gets complicated for larger dependency graphs.</span></span> <span data-ttu-id="f4bc5-168">새 패키지를 설치할 때마다 그래프 전체를 통과해야 하며 버전 충돌이 발생할 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-168">Each new package installation requires a traversal of the whole graph and raises the chance for version conflicts.</span></span> <span data-ttu-id="f4bc5-169">충돌이 발생하면 특히 프로젝트 파일 자체를 잠재적으로 수정하여 설치가 중지되고 프로젝트가 확정되지 않은 상태로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-169">When a conflict occurs, installation is stopped, leaving the project in an indeterminate state, especially with potential modifications to the project file itself.</span></span> <span data-ttu-id="f4bc5-170">다른 패키지 관리 형식을 사용하는 경우에는 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-170">This is not an issue when using other package management formats.</span></span>

## <a name="managing-dependency-assets"></a><span data-ttu-id="f4bc5-171">종속성 자산 관리</span><span class="sxs-lookup"><span data-stu-id="f4bc5-171">Managing dependency assets</span></span>

<span data-ttu-id="f4bc5-172">PackageReference 형식을 사용하는 경우 종속성에서 최상위 프로젝트로 이동하는 자산을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-172">When using the PackageReference format, you can control which assets from dependencies flow into the top-level project.</span></span> <span data-ttu-id="f4bc5-173">자세한 내용은 [PackageReference](package-references-in-project-files.md#controlling-dependency-assets)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-173">For details, see [PackageReference](package-references-in-project-files.md#controlling-dependency-assets).</span></span>

<span data-ttu-id="f4bc5-174">또한 최상위 프로젝트 자체가 패키지인 경우 `.nuspec` 파일에 나열된 종속성이 있는 `include` 및 `exclude` 특성을 사용하여 이 흐름을 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-174">When the top-level project is itself a package, you also have control over this flow by using the `include` and `exclude` attributes with dependencies listed in the `.nuspec` file.</span></span> <span data-ttu-id="f4bc5-175">[.nuspec 참조 - 종속성](../reference/nuspec.md#dependencies)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-175">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

## <a name="excluding-references"></a><span data-ttu-id="f4bc5-176">참조 제외</span><span class="sxs-lookup"><span data-stu-id="f4bc5-176">Excluding references</span></span>

<span data-ttu-id="f4bc5-177">프로젝트에서 동일한 이름의 어셈블리를 두 번 이상 참조하여 디자인 타임 및 빌드 시간 오류를 생성할 수 있는 시나리오가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-177">There are scenarios in which assemblies with the same name might be referenced more than once in a project, producing design-time and build-time errors.</span></span> <span data-ttu-id="f4bc5-178">`C.dll`의 사용자 지정 버전을 포함하고 `C.dll`도 포함된 C 패키지를 참조하는 프로젝트를 생각해 보세요.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-178">Consider a project that contains a custom version of `C.dll`, and references Package C that also contains `C.dll`.</span></span> <span data-ttu-id="f4bc5-179">동시에 이 프로젝트는 C 패키지와 `C.dll`에도 종속된 B 패키지에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-179">At the same time, the project also depends on Package B which also depends on Package C and `C.dll`.</span></span> <span data-ttu-id="f4bc5-180">결과적으로 NuGet은 사용할 `C.dll`을 결정할 수 없지만 B 패키지도 이에 종속되기 때문에 C 패키지에 대한 프로젝트의 종속성을 제거할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-180">As a result, NuGet can't determine which `C.dll` to use, but you can't just remove the project's dependency on Package C because Package B also depends on it.</span></span>

<span data-ttu-id="f4bc5-181">이 문제를 해결하려면, 원하는 `C.dll`을 직접 참조하거나 올바른 패키지를 참조하는 다른 패키지를 사용한 다음, 해당 자산을 모두 제외하는 C 패키지에 대한 종속성을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-181">To resolve this, you must directly reference the `C.dll` you want (or use another package that references the right one), and then add a dependency on Package C that excludes all its assets.</span></span> <span data-ttu-id="f4bc5-182">이렇게 하려면 사용 중인 패키지 관리 형식에 따라 다음과 같이 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-182">This is done as follows depending on the package management format in use:</span></span>

- <span data-ttu-id="f4bc5-183">[PackageReference](../consume-packages/package-references-in-project-files.md): 종속성에 `Exclude="All"`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-183">[PackageReference](../consume-packages/package-references-in-project-files.md): add `Exclude="All"` in the dependency:</span></span>

    ```xml
    <PackageReference Include="PackageC" Version="1.0.0" Exclude="All" />
    ```

- <span data-ttu-id="f4bc5-184">`packages.config`: 원하는 `C.dll` 버전만 참조하도록 `.csproj` 파일에서 PackageC에 대한 참조를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-184">`packages.config`: remove the reference to PackageC from the `.csproj` file so that it references only the version of `C.dll` that you want.</span></span>
    
## <a name="dependency-updates-during-package-install"></a><span data-ttu-id="f4bc5-185">패키지 설치 중 종속성 업데이트</span><span class="sxs-lookup"><span data-stu-id="f4bc5-185">Dependency updates during package install</span></span> 

<span data-ttu-id="f4bc5-186">종속성 버전이 이미 충족된 경우 다른 패키지를 설치하는 동안 종속성이 업데이트되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-186">If a dependency version is already satisfied, the dependency isn't updated during other package installations.</span></span> <span data-ttu-id="f4bc5-187">예를 들어 B 패키지에 종속된 A 패키지를 고려하고 버전 번호를 1.0으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-187">For example, consider package A that depends on package B and specifies 1.0 for the version number.</span></span> <span data-ttu-id="f4bc5-188">소스 리포지토리에는 B 패키지의 버전 1.0, 1.1 및 1.2가 포함되어 있습니다. B 버전 1.0이 이미 포함된 프로젝트에 A가 설치된 경우 B 1.0은 버전 제약 조건을 충족하므로 계속 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-188">The source repository contains versions 1.0, 1.1, and 1.2 of package B. If A is installed in a project that already contains B version 1.0, then B 1.0 remains in use because it satisfies the version constraint.</span></span> <span data-ttu-id="f4bc5-189">그러나 A 패키지에서 1.1 버전 이상의 B를 요청하면 B 1.2가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-189">However, if package A had requests version 1.1 or higher of B, then B 1.2 would be installed.</span></span> 

## <a name="resolving-incompatible-package-errors"></a><span data-ttu-id="f4bc5-190">호환되지 않는 패키지 오류 해결</span><span class="sxs-lookup"><span data-stu-id="f4bc5-190">Resolving incompatible package errors</span></span>

<span data-ttu-id="f4bc5-191">패키지 복원 작업 중에 "하나 이상의 패키지가 호환되지 않습니다..." 또는 패키지가 프로젝트의 대상 프레임워크와 "호환되지 않습니다."라는 오류가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-191">During a package restore operation, you may see the error "One or more packages are not compatible..." or that a package "is not compatible" with the project's target framework.</span></span>

<span data-ttu-id="f4bc5-192">프로젝트에서 참조하는 하나 이상의 패키지에서 프로젝트의 대상 프레임워크를 지원하지 않는다고 나타내는 경우에 이 오류가 발생합니다. 즉 패키지에는 프로젝트와 호환되는 대상 프레임워크에 대한 `lib` 폴더에 적합한 DLL이 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-192">This error occurs when one or more of the packages referenced in your project do not indicate that they support the project's target framework; that is, the package does not contain a suitable DLL in its `lib` folder for a target framework that is compatible with the project.</span></span> <span data-ttu-id="f4bc5-193">(목록은 [대상 프레임워크](../reference/target-frameworks.md)를 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="f4bc5-193">(See [Target frameworks](../reference/target-frameworks.md) for a list.)</span></span> 

<span data-ttu-id="f4bc5-194">예를 들어 프로젝트에서 `netstandard1.6`을 대상으로 하고 `lib\net20` 및 `\lib\net45` 폴더에만 DLL이 포함되는 패키지를 설치하려고 하면 패키지 및 해당 종속 항목에 대해 다음과 같은 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-194">For example, if a project targets `netstandard1.6` and you attempt to install a package that contains DLLs in only the `lib\net20` and `\lib\net45` folders, then you see messages like the following for the package and possibly its dependents:</span></span>

```output
Restoring packages for myproject.csproj...
Package ContosoUtilities 2.1.2.3 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoUtilities 2.1.2.3 supports:
  - net20 (.NETFramework,Version=v2.0)
  - net45 (.NETFramework,Version=v4.5)
Package ContosoCore 0.86.0 is not compatible with netstandard1.6 (.NETStandard,Version=v1.6). Package ContosoCore 0.86.0 supports:
  - 11 (11,Version=v0.0)
  - net20 (.NETFramework,Version=v2.0)
  - sl3 (Silverlight,Version=v3.0)
  - sl4 (Silverlight,Version=v4.0)
One or more packages are incompatible with .NETStandard,Version=v1.6.
Package restore failed. Rolling back package changes for 'MyProject'.
```

<span data-ttu-id="f4bc5-195">비호환성을 해결하려면 다음 중 하나를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-195">To resolve incompatibilities, do one of the following:</span></span>

- <span data-ttu-id="f4bc5-196">프로젝트의 대상을 사용할 패키지에서 지원하는 프레임워크로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-196">Retarget your project to a framework that is supported by the packages you want to use.</span></span>
- <span data-ttu-id="f4bc5-197">패키지 작성자에게 문의하고 선택한 프레임워크에 대한 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-197">Contact the author of the packages and work with them to add support for your chosen framework.</span></span> <span data-ttu-id="f4bc5-198">[nuget.org](https://www.nuget.org/)의 각 패키지 목록 페이지에는 이 목적을 위한 **연락처 소유자** 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f4bc5-198">Each package listing page on [nuget.org](https://www.nuget.org/) has a **Contact Owners** link for this purpose.</span></span>

