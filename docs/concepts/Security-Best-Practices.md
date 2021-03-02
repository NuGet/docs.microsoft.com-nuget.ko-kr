---
title: 보안 소프트웨어 공급망에 대한 모범 사례
description: NuGet 및 GitHub를 사용하여 소프트웨어 공급망을 보호하는 모범 사례입니다.
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: 125579832db2ac32217d24f6fc6fc1b555f54350
ms.sourcegitcommit: aeb9072f2fcaca73dc9de05b7fd643f1aa7c5821
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/18/2021
ms.locfileid: "101101399"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a><span data-ttu-id="3d967-103">보안 소프트웨어 공급망에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="3d967-103">Best practices for a secure software supply chain</span></span>

<span data-ttu-id="3d967-104">오픈 소스는 어디에나 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-104">Open Source is everywhere.</span></span> <span data-ttu-id="3d967-105">많은 소유 코드베이스 및 커뮤니티 프로젝트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-105">It is in many proprietary codebases and community projects.</span></span> <span data-ttu-id="3d967-106">조직 및 개인의 경우 질문은 오픈 소스 코드를 사용하고 있는지가 아니라 사용 중인 오픈 소스 코드가 무엇이고 얼마나 많이 사용하는지에 관한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-106">For organizations and individuals, the question today is not whether you are or are not using open-source code, but what open-source code you are using, and how much.</span></span>

<span data-ttu-id="3d967-107">소프트웨어 공급망이 어떻게 구성되는지 잘 모르는 경우 종속성 중 하나의 업스트림 취약성이 치명적일 수 있고, 이로 인해 개발자와 고객이 잠재적 손상에 취약해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-107">If you're not aware of what is in your software supply chain, an upstream vulnerability in one of your dependencies can be fatal, making you, and your customers, vulnerable to a potential compromise.</span></span> <span data-ttu-id="3d967-108">이 문서에서는 “소프트웨어 공급망”이라는 용어의 의미, 해당 용어의 중요성, 모범 사례를 사용하여 프로젝트의 공급망을 보호하는 방법을 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-108">In this document, we will dive deeper into what the term “software supply chain” means, why it matters, and how you can help secure your project’s supply chain with best practices.</span></span>

![The State of the Octoverse 2020 - 오픈 소스](media/opensource-percent.png)

## <a name="dependencies"></a><span data-ttu-id="3d967-110">종속성</span><span class="sxs-lookup"><span data-stu-id="3d967-110">Dependencies</span></span> 

<span data-ttu-id="3d967-111">소프트웨어 공급망이라는 용어는 소프트웨어에 들어가는 모든 항목과 소프트웨어가 제공되는 위치를 나타내는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-111">The term software supply chain is used to refer to everything that goes into your software and where it comes from.</span></span> <span data-ttu-id="3d967-112">소프트웨어 공급망이 의존하는 종속성 및 해당 종속성의 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-112">It is the dependencies and properties of your dependencies that your software supply chain depends on.</span></span> <span data-ttu-id="3d967-113">종속성은 소프트웨어를 실행하는 데 필요한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-113">A dependency is what your software needs to run.</span></span> <span data-ttu-id="3d967-114">코드, 이진 또는 기타 구성 요소와 해당 항목이 생성되는 위치(예: 리포지토리 또는 패키지 관리자)일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-114">It can be code, binaries, or other components, and where they come from, such as a repository or package manager.</span></span>

<span data-ttu-id="3d967-115">여기에는 코드 작성자, 코드가 제공된 시간, 코드의 보안 문제가 검토된 방법, 알려진 취약성, 지원되는 버전, 라이선스 정보, 프로세스의 특정 시점에 코드를 사용한 거의 모든 것이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-115">It includes who wrote the code, when it was contributed, how it was reviewed for security issues, known vulnerabilities, supported versions, license information, and just about anything that touches it at any point of the process.</span></span>

<span data-ttu-id="3d967-116">공급망은 빌드 및 패키징 스크립트나 애플리케이션에서 사용하는 인프라를 실행하는 소프트웨어와 같이 단일 애플리케이션을 넘어선 해당 스택의 다른 부분도 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-116">Your supply chain also encompasses other parts of your stack beyond a single application, such as your build and packaging scripts or the software that runs the infrastructure your application relies on.</span></span>

## <a name="vulnerabilities"></a><span data-ttu-id="3d967-117">취약점</span><span class="sxs-lookup"><span data-stu-id="3d967-117">Vulnerabilities</span></span>

<span data-ttu-id="3d967-118">오늘날 소프트웨어 종속성은 널리 사용되고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-118">Today, software dependencies are pervasive.</span></span> <span data-ttu-id="3d967-119">프로젝트에서 직접 작성할 필요가 없는 수백 개의 오픈 소스 종속성을 기능에 사용하는 것은 아주 흔한 일입니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-119">It is quite common for your projects to use hundreds of open-source dependencies for functionality that you did not have to write yourself.</span></span> <span data-ttu-id="3d967-120">즉, 대부분 애플리케이션이 직접 작성하지 않은 코드로 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-120">This may mean that most of your application consists of code that you did not author.</span></span> 

![The State of the Octoverse 2020 - 종속성](media/dependencies.png)

<span data-ttu-id="3d967-122">타사 또는 오픈 소스 종속성의 가능한 취약성은 아마도 직접 작성하는 코드만큼 긴밀하게 제어할 수 없는 종속성이므로 공급망에서 잠재적 보안 위험을 초래할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-122">Possible vulnerabilities in your third-party or open-source dependencies, are presumably dependencies you cannot control as tightly as the code you write, which can create potential security risks in your supply chain.</span></span>

<span data-ttu-id="3d967-123">관련 종속성 중 하나에 취약성이 포함되면 개발자도 취약성을 보유하게 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-123">If one of these dependencies has a vulnerability, the chances are you have a vulnerability as well.</span></span> <span data-ttu-id="3d967-124">종속성 중 하나가 개발자 모르게 변경될 수 있으므로 심각한 문제가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-124">This can be scary as one of your dependencies may change without you even knowing.</span></span> <span data-ttu-id="3d967-125">현재 취약성이 종속성에 포함되지만 악용되지 않더라도 나중에 악용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-125">Even if a vulnerability exists in a dependency today, but is not exploitable, it can be exploitable in the future.</span></span> 

<span data-ttu-id="3d967-126">수천 명의 오픈 소스 개발자와 라이브러리 작성자의 작업을 이용할 수 있다는 것은 수천 명의 낯선 사람이 프로덕션 코드에 직접 효과적으로 관여할 수 있음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-126">Being able to leverage the work of thousands of open-source developers and library authors means that thousands of strangers can effectively contribute directly to your production code.</span></span> <span data-ttu-id="3d967-127">제품은 소프트웨어 공급망을 통해 패치가 적용되지 않은 취약성, 단순한 실수 또는 종속성에 대한 악의적인 공격에서도 영향을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-127">Your product, through your software supply chain, is affected by unpatched vulnerabilities, innocent mistakes, or even malicious attacks against dependencies.</span></span>

## <a name="supply-chain-compromises"></a><span data-ttu-id="3d967-128">공급망 손상</span><span class="sxs-lookup"><span data-stu-id="3d967-128">Supply chain compromises</span></span>

<span data-ttu-id="3d967-129">공급망의 일반적인 정의는 제조업에서 제공됩니다. 공급망은 어떤 것을 제조하고 공급하는 데 필요한 프로세스 체인입니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-129">The traditional definition of a supply chain comes from manufacturing; it is the chain of processes required to make and supply something.</span></span> <span data-ttu-id="3d967-130">여기에는 계획, 자재 공급, 제조 및 소매가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-130">It includes planning, supply of materials, manufacturing, and retail.</span></span> <span data-ttu-id="3d967-131">소프트웨어 공급망은 자재 대신 코드라는 점을 제외하고 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-131">A software supply chain is similar, except instead of materials, it is code.</span></span> <span data-ttu-id="3d967-132">제조 대신 개발입니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-132">Instead of manufacturing, it is development.</span></span> <span data-ttu-id="3d967-133">땅에서 광석을 캐는 대신 공급자, 상용 또는 오픈 소스에서 코드를 제공하며 일반적으로 리포지토리에서 오픈 소스 코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-133">Instead of digging ore from the ground, code is sourced from suppliers, commercial or open source, and, in general, the open-source code comes from repositories.</span></span> <span data-ttu-id="3d967-134">리포지토리의 코드를 추가하면 제품이 해당 코드의 종속성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-134">Adding code from a repository means your product takes a dependency on that code.</span></span>

<span data-ttu-id="3d967-135">소프트웨어 공급망 공격의 한 가지 예는 종속성의 공급망을 사용하여 희생자에게 코드를 배포하는 악성 코드가 의도적으로 종속성에 추가된 경우 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-135">One example of a software supply chain attack occurs when malicious code is purposefully added to a dependency, using the supply chain of that dependency to distribute the code to its victims.</span></span> <span data-ttu-id="3d967-136">공급망 공격은 실제입니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-136">Supply chain attacks are real.</span></span> <span data-ttu-id="3d967-137">악성 코드를 새 기여자로 직접 삽입하는 방법부터 다른 사람이 모르게 기여자의 계정을 탈취하거나 서명 키를 손상해 공식적으로 종속성의 일부가 아닌 소프트웨어를 배포하는 방법까지 공급망을 공격하는 다양한 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-137">There are many methods to attack a supply chain, from directly inserting malicious code as a new contributor, to taking over a contributor’s account without others noticing, or even compromising a signing key to distribute software that is not officially part of the dependency.</span></span>

<span data-ttu-id="3d967-138">소프트웨어 공급망 공격 자체는 거의 최종 목표가 아니며, 오히려 공격자가 맬웨어를 삽입하거나 나중에 액세스하기 위해 백도어를 제공할 기회의 시작입니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-138">A software supply chain attack is in and of itself rarely the end goal, rather it is the beginning of an opportunity for an attacker to insert malware or provide a backdoor for future access.</span></span>

![The State of the Octoverse 2020 - 취약성 수명 주기](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a><span data-ttu-id="3d967-140">패치가 적용되지 않은 소프트웨어</span><span class="sxs-lookup"><span data-stu-id="3d967-140">Unpatched software</span></span>

<span data-ttu-id="3d967-141">현재 오픈 소스 사용은 주목할 만하며 곧 둔화할 것 같지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-141">The use of open source today is significant and is not expected to slow down anytime soon.</span></span> <span data-ttu-id="3d967-142">오픈 소스 소프트웨어 사용을 중지하지 않을 경우 공급망 보안에 대한 위협은 패치가 적용되지 않은 소프트웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-142">Given that we are not going to stop using open-source software, the threat to supply chain security is unpatched software.</span></span> <span data-ttu-id="3d967-143">프로젝트의 종속성에 취약성이 포함되는 위험을 해결하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="3d967-143">Knowing that, how can you address the risk that a dependency of your project has a vulnerability?</span></span>

- <span data-ttu-id="3d967-144">**환경을 구성하는 항목 파악.**</span><span class="sxs-lookup"><span data-stu-id="3d967-144">**Knowing what is in your environment.**</span></span> <span data-ttu-id="3d967-145">이를 위해 종속성 및 전이적 종속성을 검색하여 취약성 또는 라이선스 제한과 같은 해당 종속성의 위험을 파악해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-145">This requires discovering your dependencies and any transitive dependencies to understand the risks of those dependencies such as vulnerabilities or licensing restrictions.</span></span>
- <span data-ttu-id="3d967-146">**종속성 관리.**</span><span class="sxs-lookup"><span data-stu-id="3d967-146">**Manage your dependencies.**</span></span> <span data-ttu-id="3d967-147">새 보안 취약성이 검색되면 영향을 받는지 여부를 확인하고, 영향을 받는 경우 사용 가능한 최신 버전 및 보안 패치로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-147">When a new security vulnerability is discovered, you must determine whether you are impacted, and if so, update to the latest version and security patch available.</span></span> <span data-ttu-id="3d967-148">새 종속성을 도입하는 변경 내용을 검토하거나 정기적으로 이전 종속성을 감사하는 경우 해당 작업이 특히 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-148">This is especially important to review changes that introduce new dependencies or regularly auditing older dependencies.</span></span>
- <span data-ttu-id="3d967-149">**공급망 모니터링.**</span><span class="sxs-lookup"><span data-stu-id="3d967-149">**Monitor your supply chain.**</span></span> <span data-ttu-id="3d967-150">이를 위해 종속성을 관리하기 위해 적용하는 컨트롤을 감사합니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-150">This is by auditing the controls you have in place to manage your dependencies.</span></span> <span data-ttu-id="3d967-151">해당 방법으로 종속성에 맞게 더 제한적인 조건을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-151">This will help you enforce more restrictive conditions to be met for your dependencies.</span></span>

![The State of the Octoverse 2020 - 권장 사항](media/advisories.png)

<span data-ttu-id="3d967-153">현재 프로젝트 내부에서 잠재적 위험을 해결하는 데 사용할 수 있는 NuGet 및 GitHub에서 제공하는 다양한 도구 및 기술을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-153">We will cover various tools and techniques that NuGet and GitHub provides, which you can use today to address potential risks inside your project.</span></span> 

## <a name="knowing-what-is-in-your-environment"></a><span data-ttu-id="3d967-154">환경을 구성하는 항목 파악</span><span class="sxs-lookup"><span data-stu-id="3d967-154">Knowing what is in your environment</span></span>

### <a name="nuget-dependency-graph"></a><span data-ttu-id="3d967-155">NuGet 종속성 그래프</span><span class="sxs-lookup"><span data-stu-id="3d967-155">NuGet dependency graph</span></span>

<span data-ttu-id="3d967-156">**📦 패키지 소비자**</span><span class="sxs-lookup"><span data-stu-id="3d967-156">**📦 Package Consumer**</span></span>

<span data-ttu-id="3d967-157">각 프로젝트 파일을 직접 확인하여 프로젝트에서 NuGet 종속성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-157">You can view your NuGet dependencies in your project by looking directly at the respective project file.</span></span>

<span data-ttu-id="3d967-158">해당 항목은 일반적으로 다음 두 위치 중 하나에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-158">This is typically found in one of two places:</span></span>

-   <span data-ttu-id="3d967-159">[`packages.config`](../reference/packages-config.md) – 프로젝트 루트에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-159">[`packages.config`](../reference/packages-config.md) – Located in the project root.</span></span>
-   <span data-ttu-id="3d967-160">[`<PackageReference>`](../consume-packages/package-references-in-project-files.md) – 프로젝트 파일에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-160">[`<PackageReference>`](../consume-packages/package-references-in-project-files.md) – Located in the project file.</span></span> 

<span data-ttu-id="3d967-161">NuGet 종속성을 관리하는 데 사용하는 방법에 따라 Visual Studio를 사용하여 [솔루션 탐색기](/visualstudio/ide/solutions-and-projects-in-visual-studio?view=vs-2019#solution-explorer) 또는 [NuGet 패키지 관리자](../consume-packages/install-use-packages-visual-studio.md)에서 직접 종속성을 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-161">Depending on what method you use to manage your NuGet dependencies, you can also use Visual Studio to view your dependencies directly in [Solution Explorer](/visualstudio/ide/solutions-and-projects-in-visual-studio?view=vs-2019#solution-explorer) or [NuGet Package Manager](../consume-packages/install-use-packages-visual-studio.md).</span></span>

<span data-ttu-id="3d967-162">CLI 환경의 경우 [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) 명령을 사용하여 프로젝트 또는 솔루션의 종속성을 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-162">For CLI environments, you can use the [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) command to list out your project or solution’s dependencies.</span></span> 

<span data-ttu-id="3d967-163">NuGet 종속성 관리에 관한 자세한 내용은 [다음 설명서를 참조](../consume-packages/overview-and-workflow.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="3d967-163">For more information on managing NuGet dependencies, [see the following documentation](../consume-packages/overview-and-workflow.md).</span></span>

### <a name="github-dependency-graph"></a><span data-ttu-id="3d967-164">GitHub 종속성 그래프</span><span class="sxs-lookup"><span data-stu-id="3d967-164">GitHub dependency graph</span></span> 

<span data-ttu-id="3d967-165">**📦 패키지 소비자 | 📦🖊 패키지 작성자**</span><span class="sxs-lookup"><span data-stu-id="3d967-165">**📦 Package Consumer | 📦🖊 Package Author**</span></span>

<span data-ttu-id="3d967-166">GitHub의 종속성 그래프를 사용하여 프로젝트가 사용하는 패키지 및 프로젝트를 사용하는 리포지토리를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-166">You can use GitHub’s dependency graph to see the packages your project depends on and the repositories that depend on it.</span></span> <span data-ttu-id="3d967-167">이를 통해 해당 종속성에서 검색된 취약성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-167">This can help you see any vulnerabilities detected in its dependencies.</span></span>

<span data-ttu-id="3d967-168">GitHub 리포지토리 종속성에 관한 자세한 내용은 [다음 설명서를 참조](https://github.co/dependency-graph)하세요.</span><span class="sxs-lookup"><span data-stu-id="3d967-168">For more information on GitHub repository dependencies, [see the following documentation](https://github.co/dependency-graph).</span></span>

### <a name="dependency-versions"></a><span data-ttu-id="3d967-169">종속성 버전</span><span class="sxs-lookup"><span data-stu-id="3d967-169">Dependency versions</span></span>

<span data-ttu-id="3d967-170">**📦 패키지 소비자 | 📦🖊 패키지 작성자**</span><span class="sxs-lookup"><span data-stu-id="3d967-170">**📦 Package Consumer | 📦🖊 Package Author**</span></span>

<span data-ttu-id="3d967-171">종속성의 보안 공급망을 보장하기 위해 모든 종속성 및 도구를 안정적인 최신 버전으로 정기적으로 업데이트하려고 합니다. 이렇게 하면 해당 종속성과 도구에는 알려진 취약성에 대한 최신 기능 및 보안 패치가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-171">To ensure a secure supply chain of dependencies, you will want to ensure that all of your dependencies & tooling are regularly updated to the latest stable version as they will often include the latest functionality and security patches to known vulnerabilities.</span></span> <span data-ttu-id="3d967-172">종속성에는 사용하는 코드, 소비하는 이진, 사용하는 도구 및 기타 구성 요소가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-172">Your dependencies can include code you depend on, binaries you consume, tooling you use, and other components.</span></span> <span data-ttu-id="3d967-173">다음을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-173">This may include:</span></span>

-   [<span data-ttu-id="3d967-174">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3d967-174">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/)
-   [<span data-ttu-id="3d967-175">.NET SDK 및 런타임</span><span class="sxs-lookup"><span data-stu-id="3d967-175">.NET SDK & Runtime</span></span>](https://dotnet.microsoft.com/download)
-   [<span data-ttu-id="3d967-176">NuGet</span><span class="sxs-lookup"><span data-stu-id="3d967-176">NuGet</span></span>](https://www.nuget.org/downloads)
-   [<span data-ttu-id="3d967-177">NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="3d967-177">NuGet packages</span></span>](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a><span data-ttu-id="3d967-178">종속성 관리</span><span class="sxs-lookup"><span data-stu-id="3d967-178">Manage your dependencies</span></span>

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a><span data-ttu-id="3d967-179">NuGet 사용되지 않고 취약한 종속성</span><span class="sxs-lookup"><span data-stu-id="3d967-179">NuGet deprecated and vulnerable dependencies</span></span>

<span data-ttu-id="3d967-180">**📦 패키지 소비자 | 📦🖊 패키지 작성자**</span><span class="sxs-lookup"><span data-stu-id="3d967-180">**📦 Package Consumer | 📦🖊 Package Author**</span></span>

<span data-ttu-id="3d967-181">[dotnet CLI](/dotnet/core/tools/dotnet-list-package)를 사용하여 프로젝트나 솔루션 내부에 있을 수 있는 사용되지 않거나 취약한 알려진 종속성을 모두 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-181">You can use the [dotnet CLI](/dotnet/core/tools/dotnet-list-package) to list any known deprecated or vulnerable dependencies you may have inside your project or solution.</span></span> <span data-ttu-id="3d967-182">`dotnet list package --deprecated` 또는 `dotnet list package --vulnerable` 명령을 사용하여 알려진 사용 중단 또는 취약성 목록을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-182">You can use the command `dotnet list package --deprecated` or `dotnet list package --vulnerable` to provide you a list of any known deprecations or vulnerabilities.</span></span>

### <a name="github-vulnerable-dependencies"></a><span data-ttu-id="3d967-183">GitHub 취약한 종속성</span><span class="sxs-lookup"><span data-stu-id="3d967-183">GitHub vulnerable dependencies</span></span>

<span data-ttu-id="3d967-184">**📦 패키지 소비자 | 📦🖊 패키지 작성자**</span><span class="sxs-lookup"><span data-stu-id="3d967-184">**📦 Package Consumer | 📦🖊 Package Author**</span></span>

<span data-ttu-id="3d967-185">프로젝트가 GitHub에서 호스트되는 경우 [GitHub 보안](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors)을 이용하여 프로젝트에서 보안 취약성 및 오류를 찾을 수 있으며, Dependabot은 코드베이스에 대해 끌어오기 요청을 열어 이를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-185">If your project is hosted on GitHub, you can leverage [GitHub Security](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) to find security vulnerabilities and errors in your project and Dependabot will fix them by opening up a pull request against your codebase.</span></span> 

<span data-ttu-id="3d967-186">취약한 종속성이 도입되기 전에 해당 종속성을 포착하는 것은 [“시프트 레프트”](https://en.wikipedia.org/wiki/Shift-left_testing) 이동의 한 가지 목표입니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-186">Catching vulnerable dependencies before they are introduced is one goal of the [“Shift Left”](https://en.wikipedia.org/wiki/Shift-left_testing) movement.</span></span> <span data-ttu-id="3d967-187">해당 라이선스, 전이적 종속성 및 종속성 기간 등 종속성에 관한 정보를 얻을 수 있으면 해당 작업을 수행하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-187">Being able to have information about your dependencies such as their license, transitive dependencies, and the age of dependencies helps you do just that.</span></span>

<span data-ttu-id="3d967-188">Dependabot 경고 및 보안 업데이트에 관한 자세한 내용은 [다음 설명서를 참조](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies)하세요.</span><span class="sxs-lookup"><span data-stu-id="3d967-188">For more information about Dependabot alerts & security updates, [see the following documentation](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies).</span></span>

### <a name="nuget-feeds"></a><span data-ttu-id="3d967-189">NuGet 피드</span><span class="sxs-lookup"><span data-stu-id="3d967-189">NuGet feeds</span></span>

<span data-ttu-id="3d967-190">**📦 패키지 소비자**</span><span class="sxs-lookup"><span data-stu-id="3d967-190">**📦 Package Consumer**</span></span>

<span data-ttu-id="3d967-191">여러 퍼블릭 및 프라이빗 NuGet 소스 피드를 사용하는 경우 모든 피드에서 패키지를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-191">When using multiple public & private NuGet source feeds, a package can be downloaded from any of the feeds.</span></span> <span data-ttu-id="3d967-192">빌드가 예측 가능하고 [종속성 혼동](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610)과 같은 알려진 공격으로부터 보호되도록 하기 위해 패키지를 제공하는 특정 피드가 무엇인지 알고 있는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-192">To ensure your build is predictable and secure from known attacks such as [Dependency Confusion](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610), knowing what specific feed(s) your packages are coming from is a best practice.</span></span> <span data-ttu-id="3d967-193">보호를 위해 업스트림 기능이 있는 단일 피드 또는 프라이빗 피드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-193">You can use a single feed or private feed with upstreaming capabilities for protection.</span></span>

<span data-ttu-id="3d967-194">패키지 피드를 보호하는 방법에 관한 자세한 내용은 [3 Ways to Mitigate Risk When Using Private Package Feeds](https://azure.microsoft.com/en-us/resources/3-ways-to-mitigate-risk-using-private-package-feeds/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d967-194">For more information to secure your package feeds, see [3 Ways to Mitigate Risk When Using Private Package Feeds](https://azure.microsoft.com/en-us/resources/3-ways-to-mitigate-risk-using-private-package-feeds/).</span></span>

### <a name="client-trust-policies"></a><span data-ttu-id="3d967-195">클라이언트 트러스트 정책</span><span class="sxs-lookup"><span data-stu-id="3d967-195">Client trust policies</span></span>

<span data-ttu-id="3d967-196">**📦 패키지 소비자**</span><span class="sxs-lookup"><span data-stu-id="3d967-196">**📦 Package Consumer**</span></span>

<span data-ttu-id="3d967-197">서명하는 데 사용하는 패키지가 필요한 옵트인 가능한 정책이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-197">There are policies that you can opt-into in which you require the packages you use to be signed.</span></span> <span data-ttu-id="3d967-198">이를 통해 작성자가 서명한 경우 패키지 작성자를 신뢰하거나 NuGet.org에서 서명한 리포지토리인 특정 사용자 또는 계정이 소유하는 경우 패키지를 신뢰할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-198">This allows you to trust a package author, as long as it is author signed, or trust a package if it is owned by a specific user or account that is repository signed by NuGet.org.</span></span>

<span data-ttu-id="3d967-199">클라이언트 트러스트 정책을 구성하려면 [다음 설명서를 참조](../consume-packages/installing-signed-packages.md)하세요.</span><span class="sxs-lookup"><span data-stu-id="3d967-199">To configure client trust policies, [see the following documentation](../consume-packages/installing-signed-packages.md).</span></span>

### <a name="lock-files"></a><span data-ttu-id="3d967-200">잠금 파일</span><span class="sxs-lookup"><span data-stu-id="3d967-200">Lock files</span></span>

<span data-ttu-id="3d967-201">**📦 패키지 소비자**</span><span class="sxs-lookup"><span data-stu-id="3d967-201">**📦 Package Consumer**</span></span>

<span data-ttu-id="3d967-202">잠금 파일은 패키지 콘텐츠의 해시를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-202">Lock files store the hash of your package’s content.</span></span> <span data-ttu-id="3d967-203">설치하려는 패키지의 콘텐츠 해시가 잠금 파일과 일치하는 경우 패키지 반복성을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-203">If the content hash of a package you want to install matches with the lock file, it will ensure package repeatability.</span></span>

<span data-ttu-id="3d967-204">잠금 파일을 사용하도록 설정하려면 [다음 설명서를 참조](../consume-packages/package-references-in-project-files#locking-dependencies)하세요.</span><span class="sxs-lookup"><span data-stu-id="3d967-204">To enable lock files, [see the following documentation](../consume-packages/package-references-in-project-files#locking-dependencies).</span></span>

## <a name="monitor-your-supply-chain"></a><span data-ttu-id="3d967-205">공급망 모니터링</span><span class="sxs-lookup"><span data-stu-id="3d967-205">Monitor your supply chain</span></span>

### <a name="github-secret-scanning"></a><span data-ttu-id="3d967-206">GitHub 암호 검색</span><span class="sxs-lookup"><span data-stu-id="3d967-206">GitHub secret scanning</span></span>

<span data-ttu-id="3d967-207">**📦🖊 패키지 작성자**</span><span class="sxs-lookup"><span data-stu-id="3d967-207">**📦🖊 Package Author**</span></span>

<span data-ttu-id="3d967-208">GitHub는 리포지토리에서 NuGet API 키를 검색하여 실수로 커밋된 비밀의 사기성이 있는 사용을 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-208">GitHub scans repositories for NuGet API keys to prevent fraudulent uses of secrets that were accidentally committed.</span></span> 

<span data-ttu-id="3d967-209">비밀 검색에 관한 자세한 내용은 [비밀 검색 정보](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d967-209">To learn more about secret scanning, see [About secret scanning](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning).</span></span>

### <a name="author-package-signing"></a><span data-ttu-id="3d967-210">작성자 패키지 서명</span><span class="sxs-lookup"><span data-stu-id="3d967-210">Author Package Signing</span></span>

<span data-ttu-id="3d967-211">**📦🖊 패키지 작성자**</span><span class="sxs-lookup"><span data-stu-id="3d967-211">**📦🖊 Package Author**</span></span>

<span data-ttu-id="3d967-212">[작성자 서명](../reference/signed-packages-reference.md)을 사용하여 패키지 작성자는 패키지에서 해당 ID에 스탬프를 지정할 수 있고 소비자는 작성자가 해당 스탬프를 제공하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-212">[Author signing](../reference/signed-packages-reference.md) allows a package author to stamp their identity on a package and for a consumer to verify it came from you.</span></span> <span data-ttu-id="3d967-213">해당 서명은 콘텐츠 변조를 방지하며 패키지 출처 및 패키지 신뢰성에 관한 단일 데이터 소스로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-213">This protects you against content tampering and serves as a single source of truth about the origin of the package and the package authenticity.</span></span> <span data-ttu-id="3d967-214">클라이언트 트러스트 정책과 결합할 경우 특정 작성자가 패키지를 제공했는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-214">When combined with client trust policies, you can verify a package came from a specific author.</span></span>

<span data-ttu-id="3d967-215">패키지에 작성자 서명하려면 [패키지 서명](../create-packages/sign-a-package.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d967-215">To author sign a package, see [Sign a package](../create-packages/sign-a-package.md).</span></span>

### <a name="two-factor-authentication-2fa"></a><span data-ttu-id="3d967-216">2FA(2단계 인증)</span><span class="sxs-lookup"><span data-stu-id="3d967-216">Two-Factor Authentication (2FA)</span></span>

<span data-ttu-id="3d967-217">**📦🖊 패키지 작성자**</span><span class="sxs-lookup"><span data-stu-id="3d967-217">**📦🖊 Package Author**</span></span>

<span data-ttu-id="3d967-218">2FA(2단계 인증)를 사용하면 [GitHub 계정](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) 또는 [NuGet.org 퍼블릭 패키지 리포지토리에 로그인](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa)할 때 추가 보안 계층을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-218">Enabling two-factor authentication (2FA) can add an extra layer of security when [logging into your GitHub account](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) or the [NuGet.org public package repository](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa).</span></span> <span data-ttu-id="3d967-219">계정을 보호하려면 2단계 인증을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-219">It is recommended that you enable two-factor authentication to protect your account.</span></span>

### <a name="package-id-prefix-reservation"></a><span data-ttu-id="3d967-220">패키지 ID 접두사 예약</span><span class="sxs-lookup"><span data-stu-id="3d967-220">Package ID prefix reservation</span></span> 

<span data-ttu-id="3d967-221">**📦🖊 패키지 작성자**</span><span class="sxs-lookup"><span data-stu-id="3d967-221">**📦🖊 Package Author**</span></span>

<span data-ttu-id="3d967-222">패키지 ID를 보호하려면 각 네임스페이스로 패키지 ID 접두사를 예약하여 패키지 ID 접두사가 [지정된 조건](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria)에 제대로 해당하는 경우 일치하는 소유자를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-222">To protect the identity of your packages, you can reserve a package ID prefix with your respective namespace to associate a matching owner if your package ID prefix properly falls under the [specified criteria](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria).</span></span> 

<span data-ttu-id="3d967-223">ID 접두사 예약에 관한 자세한 내용은 [패키지 ID 접두사 예약](../nuget-org/id-prefix-reservation.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d967-223">To learn about reserving ID prefixes, see [Package ID prefix reservation](../nuget-org/id-prefix-reservation.md).</span></span>

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a><span data-ttu-id="3d967-224">취약한 패키지 사용 중단 및 나열 취소</span><span class="sxs-lookup"><span data-stu-id="3d967-224">Deprecating and unlisting a vulnerable package</span></span>

<span data-ttu-id="3d967-225">**📦🖊 패키지 작성자**</span><span class="sxs-lookup"><span data-stu-id="3d967-225">**📦🖊 Package Author**</span></span>

<span data-ttu-id="3d967-226">작성한 패키지에서 취약성을 발견한 경우 .NET 패키지 에코시스템을 보호하려면 패키지를 검색하는 사용자에게 표시되지 않도록 패키지를 사용 중단하고 나열 취소하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-226">To protect the .NET package ecosystem when you are aware of a vulnerability in a package you have authored, do your best to deprecate and unlist the package so it is hidden from users searching for packages.</span></span> <span data-ttu-id="3d967-227">사용되지 않고 나열되지 않은 패키지를 사용하고 있는 경우에는 해당 패키지를 사용하지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-227">If you are consuming a package that is deprecated and unlisted, you should avoid using the package.</span></span>

<span data-ttu-id="3d967-228">패키지를 사용 중단 및 나열 취소하는 방법에 관한 자세한 내용은 [패키지 사용 중단](../nuget-org/deprecate-packages.md) 및 [나열 취소](../nuget-org/policies/deleting-packages.md#unlisting-a-package)에 관한 다음 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d967-228">To learn how to deprecate and unlist a package, see the following documentation on [deprecating](../nuget-org/deprecate-packages.md) and [unlisting packages](../nuget-org/policies/deleting-packages.md#unlisting-a-package).</span></span>

## <a name="summary"></a><span data-ttu-id="3d967-229">요약</span><span class="sxs-lookup"><span data-stu-id="3d967-229">Summary</span></span>

<span data-ttu-id="3d967-230">소프트웨어 공급망은 코드에 들어가거나 코드에 영향을 주는 어떤 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-230">Your software supply chain is anything that goes into or affects your code.</span></span> <span data-ttu-id="3d967-231">공급망 손상이 실제적이고 확산하고 있더라도 해당 손상은 여전히 드문 현상입니다. 따라서 할 수 있는 가장 중요한 작업은 **종속성을 인식하고, 종속성을 관리하고**, **공급망을 모니터링** 하여 공급망을 보호하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-231">Even though supply chain compromises are real and growing in popularity, they are still rare; so the most important thing you can do is protect your supply chain by **being aware of your dependencies, managing your dependencies** and **monitoring your supply chain.**</span></span>

<span data-ttu-id="3d967-232">현재 공급망 확인, 관리 및 모니터링 시 더 효과적일 수 있고 NuGet 및 [GitHub](/learn/modules/maintain-secure-repository-github/)에서 제공하는 다양한 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="3d967-232">You learned about various methods that NuGet and [GitHub](/learn/modules/maintain-secure-repository-github/) provide that are available to you today to be more effective in viewing, managing, and monitoring your supply chain.</span></span>

<span data-ttu-id="3d967-233">전 세계 소프트웨어를 보호하는 방법에 관한 자세한 내용은 [The State of the Octoverse 2020 보안 보고서](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d967-233">For more information about securing the world's software, see [The State of the Octoverse 2020 Security Report](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf).</span></span>
