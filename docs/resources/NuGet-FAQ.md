---
title: NuGet 질문과 대답
description: 명령줄 및 Visual Studio에서 NuGet을 사용하기 위한 일반적인 질문과 대답
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9b12b1fa27308cf41b58b0c244ea648d3eecdc95
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520393"
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="1783c-103">NuGet 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="1783c-103">NuGet frequently-asked questions</span></span>

<span data-ttu-id="1783c-104">**NuGet을 실행하는 데 필요한 것은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-104">**What is required to run NuGet?**</span></span>

<span data-ttu-id="1783c-105">UI 및 명령줄 도구에 관한 모든 정보는 [설치 가이드](../install-nuget-client-tools.md)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-105">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="1783c-106">**NuGet은 Mono를 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-106">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="1783c-107">`nuget.exe` 명령줄 도구는 Mono 3.2 이상에서 빌드하고 실행되며, Mono에서 패키지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-107">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="1783c-108">`nuget.exe`는 Windows에서 완벽하게 작동하지만, Linux 및 OS X에서는 알려진 문제가 있습니다. GitHub의 [Mono 문제](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1783c-108">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="1783c-109">[그래픽 클라이언트](https://github.com/mrward/monodevelop-nuget-addin)는 MonoDevelop용 추가 기능으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-109">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="1783c-110">**패키지에 포함된 내용과 애플리케이션에 안정적이고 유용한 지 여부를 확인하려면 어떻게 해야 할까요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-110">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="1783c-111">패키지 학습에 대한 기본 소스는 nuget.org(또는 다른 개인 피드)의 목록 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-111">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="1783c-112">nuget.org의 각 패키지 페이지에는 패키지에 대한 설명, 해당 버전 기록 및 사용 통계가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-112">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="1783c-113">또한 패키지 페이지의 **정보** 섹션에는 프로젝트의 웹 사이트에 대한 링크가 포함되어 있으며, 여기서 패키지를 사용하는 방법을 알아보는 데 도움이 되는 많은 예제와 기타 문서를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-113">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="1783c-114">자세한 내용은 [패키지 찾기 및 선택](../consume-packages/finding-and-choosing-packages.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1783c-114">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="1783c-115">Visual Studio의 NuGet</span><span class="sxs-lookup"><span data-stu-id="1783c-115">NuGet in Visual Studio</span></span>

<span data-ttu-id="1783c-116">**다른 Visual Studio 제품에서는 NuGet을 어떻게 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-116">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="1783c-117">Windows에서 Visual Studio는 [패키지 관리자 UI](../consume-packages/install-use-packages-visual-studio.md)와 [패키지 관리자 콘솔](../consume-packages/install-use-packages-powershell.md)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-117">Visual Studio on Windows supports the [Package Manager UI](../consume-packages/install-use-packages-visual-studio.md) and the [Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>
- <span data-ttu-id="1783c-118">Mac용 Visual Studio에는 [프로젝트에 NuGet 패키지 포함](/visualstudio/mac/nuget-walkthrough)에서 설명한 대로 NuGet 기능이 기본적으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-118">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="1783c-119">Visual Studio Code(모든 플랫폼)에는 직접적인 NuGet 통합이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-119">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="1783c-120">[NuGet CLI](../reference/nuget-exe-cli-reference.md) 또는 [dotnet CLI](../reference/dotnet-commands.md)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="1783c-120">Use the [NuGet CLI](../reference/nuget-exe-cli-reference.md) or the [dotnet CLI](../reference/dotnet-commands.md).</span></span>
- <span data-ttu-id="1783c-121">Azure DevOps는 [NuGet 패키지를 복원하는 빌드 단계](/vsts/build-release/tasks/package/nuget)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-121">Azure DevOps provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="1783c-122">또한 [Azure DevOps에서 전용 NuGet 패키지 피드를 호스팅](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-122">You can also [host private NuGet package feeds on Azure DevOps](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).</span></span>

<span data-ttu-id="1783c-123">**설치된 NuGet 도구의 정확한 버전을 확인하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-123">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="1783c-124">Visual Studio에서 **도움말 > Microsoft Visual Studio 정보** 명령을 사용하고 **NuGet 패키지 관리자** 옆에 표시된 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-124">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="1783c-125">또는 패키지 관리자 콘솔(**도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔**)을 시작하고, `$host`를 입력하여 버전을 포함한 NuGet 관련 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-125">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="1783c-126">**NuGet에서 지원하는 프로그래밍 언어는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-126">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="1783c-127">NuGet은 일반적으로 .NET 언어에서 작동하며, .NET 라이브러리를 프로젝트에 가져오도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-127">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="1783c-128">또한 일부 프로젝트 형식에서 MSBuild 및 Visual Studio 자동화를 지원하므로 다른 프로젝트와 언어를 다양한 수준으로 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-128">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="1783c-129">최신 버전의 NuGet은 C#, Visual Basic, F#, WiX 및 C++을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-129">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="1783c-130">**NuGet에서 지원하는 프로젝트 템플릿은 무엇인가요??**</span><span class="sxs-lookup"><span data-stu-id="1783c-130">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="1783c-131">NuGet은 Windows, 웹, 클라우드, SharePoint, Wix 등과 같은 다양한 프로젝트 템플릿을 완벽하게 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-131">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="1783c-132">**Visual Studio 템플릿의 일부인 패키지를 업데이트하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-132">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="1783c-133">패키지 관리자 UI에서 **업데이트** 탭으로 이동하여 **모두 업데이트**를 선택하거나, 패키지 관리자 콘솔에서 [`Update-Package` 명령](../reference/ps-reference/ps-ref-update-package.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-133">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../reference/ps-reference/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="1783c-134">템플릿 자체를 업데이트하려면 템플릿 리포지토리를 수동으로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-134">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="1783c-135">이 주제에 대한 [Xavier Decoster의 블로그](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1783c-135">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="1783c-136">모든 종속성의 최신 버전이 서로 호환되지 않을 경우 수동으로 업데이트하면 템플릿이 손상될 수 있으므로 이 작업은 사용자의 책임 하에 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-136">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="1783c-137">**Visual Studio 외부에서 NuGet을 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-137">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="1783c-138">예, NuGet은 명령줄에서 직접 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-138">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="1783c-139">[설치 가이드](../install-nuget-client-tools.md) 및 [CLI 참조](../reference/nuget-exe-cli-reference.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1783c-139">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../reference/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="1783c-140">NuGet 명령줄</span><span class="sxs-lookup"><span data-stu-id="1783c-140">NuGet command line</span></span>

<span data-ttu-id="1783c-141">**최신 버전의 NuGet 명령줄 도구를 가져오려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-141">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="1783c-142">[설치 가이드](../install-nuget-client-tools.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1783c-142">See the [Install guide](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="1783c-143">현재 설치되어 있는 도구 버전을 확인하려면 `nuget help`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-143">To check the current installed version of the tool, use `nuget help`.</span></span>

<span data-ttu-id="1783c-144">**nuget.exe에 대한 라이선스는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-144">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="1783c-145">MIT 라이선스 조건 하에 nuget.exe를 재배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-145">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="1783c-146">재배포하도록 선택한 nuget.exe의 복사본을 업데이트하고 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-146">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="1783c-147">**NuGet 명령줄 도구는 확장할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-147">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="1783c-148">예, [Rob Reynold의 게시물](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)에서 설명한 대로 사용자 지정 명령을 `nuget.exe`에 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-148">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="1783c-149">NuGet 패키지 관리자 콘솔(Windows의 Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="1783c-149">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="1783c-150">**패키지 관리자 콘솔에서 DTE 개체에 액세스하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-150">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="1783c-151">Visual Studio 자동화 개체 모델의 최상위 개체를 DTE(개발 도구 환경) 개체라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-151">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="1783c-152">콘솔에서 `$DTE`라는 변수를 통해 이 개체를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-152">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="1783c-153">자세한 내용은 Visual Studio 확장성 설명서에서 [자동화 모델 개요](/visualstudio/extensibility/internals/automation-model-overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1783c-153">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="1783c-154">**$DTE 변수를 DTE2 형식으로 캐스팅하려고 하지만 오류가 발생합니다. "EnvDTE.DTEClass" 형식의 "EnvDTE.DTEClass" 값을 "EnvDTE80.DTE2" 형식으로 변환할 수 없습니다. 무엇이 문제인가요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-154">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="1783c-155">이는 PowerShell이 COM 개체와 상호 작용하는 방법과 관련하여 알려진 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-155">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="1783c-156">다음과 같이 수행해 보세요.</span><span class="sxs-lookup"><span data-stu-id="1783c-156">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="1783c-157">`Get-Interface`는 NuGet PowerShell 호스트에서 추가한 도우미 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-157">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="1783c-158">패키지 만들기 및 게시</span><span class="sxs-lookup"><span data-stu-id="1783c-158">Creating and publishing packages</span></span>

<span data-ttu-id="1783c-159">**내 패키지를 피드에 나열하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-159">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="1783c-160">[패키지 만들기 및 게시](../quickstart/create-and-publish-a-package.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1783c-160">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="1783c-161">**다른 버전의 .NET Framework를 대상으로 하는 여러 버전의 라이브러리가 있습니다. 이를 지원하는 단일 패키지를 빌드하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-161">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="1783c-162">[여러 .NET Framework 버전 지원](../create-packages/supporting-multiple-target-frameworks.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1783c-162">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="1783c-163">**내 리포지토리 또는 피드를 설정하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-163">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="1783c-164">[패키지 호스팅 개요](../hosting-packages/overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1783c-164">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="1783c-165">**NuGet 피드에 패키지를 대량으로 업로드하려면 어떻게 해야 할까요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-165">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="1783c-166">[NuGet 패키지 대량 게시](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx)(jeffhandly.com)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1783c-166">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="1783c-167">패키지 작업</span><span class="sxs-lookup"><span data-stu-id="1783c-167">Working with packages</span></span>

<span data-ttu-id="1783c-168">**프로젝트 수준 패키지와 솔루션 수준 패키지의 차이점은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-168">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="1783c-169">솔루션 수준 패키지(NuGet 3.x 이상)는 솔루션에 한 번만 설치되며 솔루션의 모든 프로젝트에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-169">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="1783c-170">프로젝트 수준 패키지는 이를 사용하는 각 프로젝트에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-170">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="1783c-171">또한 솔루션 수준 패키지는 패키지 관리자 콘솔 내에서 호출할 수 있는 새 명령을 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-171">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="1783c-172">**인터넷 연결 없이 NuGet 패키지를 설치할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-172">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="1783c-173">예, Scott Hanselman의 블로그 게시물인 [nuget.org가 다운되었을 때(또는 비행기에 탑승한 경우) NuGet에 액세스하는 방법](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx)(hanselman.com)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1783c-173">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="1783c-174">**기본 패키지 폴더와 다른 위치에 패키지를 설치하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-174">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="1783c-175">`nuget config -set repositoryPath=<path>`를 사용하여 `Nuget.Config`의 [`repositoryPath`](../reference/nuget-config-file.md#config-section) 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-175">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="1783c-176">**NuGet 패키지 폴더를 원본 제어에 추가하지 않도록 방지하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-176">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="1783c-177">`Nuget.Config`의 [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section)을 `true`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-177">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="1783c-178">이 키는 솔루션 수준에서 작동하므로 `$(Solutiondir)\.nuget\Nuget.Config` 파일에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-178">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="1783c-179">Visual Studio에서 패키지 복원을 사용하면 이 파일이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-179">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="1783c-180">**패키지 복원을 해제하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-180">**How do I turn off package restore?**</span></span>

<span data-ttu-id="1783c-181">[패키지 복원 사용 설정/해제](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1783c-181">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enable-and-disable-package-restore-in-visual-studio).</span></span>

<span data-ttu-id="1783c-182">**원격 종속성이 있는 로컬 패키지를 설치할 때 "종속성을 확인할 수 없습니다."라는 오류 메시지가 표시되는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-182">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="1783c-183">프로젝트에 로컬 패키지를 설치할 때 **모든** 원본을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-183">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="1783c-184">이렇게 하면 하나만 사용하는 대신 모든 피드를 집계합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-184">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="1783c-185">이 오류가 나타나는 이유는 로컬 리포지토리의 사용자가 기업 정책으로 인해 실수로 원격 패키지를 설치하지 않도록 하려는 경우가 많기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-185">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="1783c-186">**동일한 폴더에 여러 프로젝트가 있습니다. 각 프로젝트마다 별도의 packages.config 파일을 사용하려면 어떻게 해야 할까요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-186">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="1783c-187">개별 프로젝트가 별도의 폴더에 있는 대부분의 프로젝트에서는 NuGet이 각 프로젝트의 `packages.config` 파일을 식별하므로 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-187">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="1783c-188">동일한 폴더에 NuGet 3.3 이상 및 여러 프로젝트가 있는 경우, `packages.{project-name}.config` 패턴을 사용하는 `packages.config` 파일 이름에 프로젝트 이름을 삽입할 수 있으며, NuGet에서 해당 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-188">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="1783c-189">이는 PackageReference를 사용할 때 각 프로젝트 파일에 자체의 종속성 목록이 포함되므로 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-189">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="1783c-190">**내 리포지토리 목록에 nuget.org가 표시되지 않습니다. 다시 가져오려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="1783c-190">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="1783c-191">원본 목록에 `https://api.nuget.org/v3/index.json`을 추가합니다. 또는</span><span class="sxs-lookup"><span data-stu-id="1783c-191">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="1783c-192">`%appdata%\.nuget\NuGet.Config`(Windows) 또는 `~/.nuget/NuGet/NuGet.Config`(Mac/Linux)를 삭제하고 NuGet에서 다시 만들도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1783c-192">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>
