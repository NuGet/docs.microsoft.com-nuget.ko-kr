---
title: "NuGet 질문과 대답 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/11/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "명령줄 및 Visual Studio에서 NuGet을 사용하고 NuGet 갤러리에서 작업하는 경우와 관련된 일반적인 질문과 대답입니다."
keywords: "NuGet Q&A, 질문과 대답, 일반적인 문제, NuGet 버전, 패키지 버전"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3782fe5dcf8df002d99446aa7548a6eacc62211c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="nuget-frequently-asked-questions"></a><span data-ttu-id="5d067-104">NuGet 질문과 대답</span><span class="sxs-lookup"><span data-stu-id="5d067-104">NuGet frequently-asked questions</span></span>

<span data-ttu-id="5d067-105">**NuGet을 실행하는 데 필요한 것은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-105">**What is required to run NuGet?**</span></span>

<span data-ttu-id="5d067-106">UI 및 명령줄 도구에 관한 모든 정보는 [설치 가이드](../install-nuget-client-tools.md)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-106">All the information around both UI and command-line tools is available in the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="5d067-107">**NuGet은 Mono를 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-107">**Does NuGet support Mono?**</span></span>

<span data-ttu-id="5d067-108">`nuget.exe` 명령줄 도구는 Mono 3.2 이상에서 빌드하고 실행되며, Mono에서 패키지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-108">The command-line tool, `nuget.exe`, builds and runs under Mono 3.2+ and can create packages in Mono.</span></span>

<span data-ttu-id="5d067-109">`nuget.exe`는 Windows에서 완벽하게 작동하지만, Linux 및 OS X에서는 알려진 문제가 있습니다. GitHub의 [Mono 문제](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-109">Although `nuget.exe` works fully on Windows, there are known issues on Linux and OS X. Refer to [Mono issues](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono) on GitHub.</span></span>

<span data-ttu-id="5d067-110">[그래픽 클라이언트](https://github.com/mrward/monodevelop-nuget-addin)는 MonoDevelop용 추가 기능으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-110">A [graphical client](https://github.com/mrward/monodevelop-nuget-addin) is available as an add-in for MonoDevelop.</span></span>

<span data-ttu-id="5d067-111">**패키지에 포함된 내용과 응용 프로그램에 안정적이고 유용한 지 여부를 확인하려면 어떻게 해야 할까요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-111">**How can I determine what a package contains and whether it's stable and useful for my application?**</span></span>

<span data-ttu-id="5d067-112">패키지 학습에 대한 기본 소스는 nuget.org(또는 다른 개인 피드)의 목록 페이지입니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-112">The primary source for learning about a package is its listing page on nuget.org (or another private feed).</span></span> <span data-ttu-id="5d067-113">nuget.org의 각 패키지 페이지에는 패키지에 대한 설명, 해당 버전 기록 및 사용 통계가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-113">Each package page on nuget.org includes a description of the package, its version history, and usage statistics.</span></span> <span data-ttu-id="5d067-114">또한 패키지 페이지의 **정보** 섹션에는 프로젝트의 웹 사이트에 대한 링크가 포함되어 있으며, 여기서 패키지를 사용하는 방법을 알아보는 데 도움이 되는 많은 예제와 기타 문서를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-114">The **Info** section on the package page also contains a link to the project's web site where you typically find many examples and other documentation to help you learn how the package is used.</span></span>

<span data-ttu-id="5d067-115">자세한 내용은 [패키지 찾기 및 선택](../consume-packages/finding-and-choosing-packages.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-115">For more information, see [Finding and choosing packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="nuget-in-visual-studio"></a><span data-ttu-id="5d067-116">Visual Studio의 NuGet</span><span class="sxs-lookup"><span data-stu-id="5d067-116">NuGet in Visual Studio</span></span>

<span data-ttu-id="5d067-117">**다른 Visual Studio 제품에서는 NuGet을 어떻게 지원하나요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-117">**How is NuGet supported in different Visual Studio products?**</span></span>

- <span data-ttu-id="5d067-118">Windows에서 Visual Studio는 [패키지 관리자 UI](../tools/package-manager-ui.md)와 [패키지 관리자 콘솔](../tools/package-manager-console.md)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-118">Visual Studio on Windows supports the [Package Manager UI](../tools/package-manager-ui.md) and the [Package Manager Console](../tools/package-manager-console.md).</span></span>
- <span data-ttu-id="5d067-119">Mac용 Visual Studio에는 [프로젝트에 NuGet 패키지 포함](/visualstudio/mac/nuget-walkthrough)에서 설명한 대로 NuGet 기능이 기본적으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-119">Visual Studio for Mac has built-in NuGet capabilities as described on [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>
- <span data-ttu-id="5d067-120">Visual Studio Code(모든 플랫폼)에는 직접적인 NuGet 통합이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-120">Visual Studio Code (all platforms) does not have any direct NuGet integration.</span></span> <span data-ttu-id="5d067-121">[NuGet CLI](../tools/nuget-exe-cli-reference.md) 또는 [dotnet CLI](../tools/dotnet-commands.md)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-121">Use the [NuGet CLI](../tools/nuget-exe-cli-reference.md) or the [dotnet CLI](../tools/dotnet-commands.md).</span></span>
- <span data-ttu-id="5d067-122">Visual Studio Team Services는 [NuGet 패키지를 복원하는 빌드 단계](/vsts/build-release/tasks/package/nuget)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-122">Visual Studio Team Services provides [a build step to restore NuGet packages](/vsts/build-release/tasks/package/nuget).</span></span> <span data-ttu-id="5d067-123">또한 [Team Services에서 전용 NuGet 패키지 피드를 호스팅](https://www.visualstudio.com/docs/package/nuget/publish)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-123">You can also [host private NuGet package feeds on Team Services](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

<span data-ttu-id="5d067-124">**설치된 NuGet 도구의 정확한 버전을 확인하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-124">**How do I check the exact version of the NuGet tools that are installed?**</span></span>

<span data-ttu-id="5d067-125">Visual Studio에서 **도움말 > Microsoft Visual Studio 정보** 명령을 사용하고 **NuGet 패키지 관리자** 옆에 표시된 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-125">In Visual Studio, use the **Help > About Microsoft Visual Studio** command and look at the version displayed next to **NuGet Package Manager**.</span></span>

<span data-ttu-id="5d067-126">또는 패키지 관리자 콘솔(**도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔**)을 시작하고, `$host`를 입력하여 버전을 포함한 NuGet 관련 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-126">Alternatively, launch the Package Manager Console (**Tools > NuGet Package Manager > Package Manager Console**) and enter `$host` to see information about NuGet including the version.</span></span>

<span data-ttu-id="5d067-127">**NuGet에서 지원하는 프로그래밍 언어는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-127">**What programming languages are supported by NuGet?**</span></span>

<span data-ttu-id="5d067-128">NuGet은 일반적으로 .NET 언어에서 작동하며, .NET 라이브러리를 프로젝트에 가져오도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-128">NuGet generally works for .NET languages and is designed to bring .NET libraries into a project.</span></span> <span data-ttu-id="5d067-129">또한 일부 프로젝트 형식에서 MSBuild 및 Visual Studio 자동화를 지원하므로 다른 프로젝트와 언어를 다양한 수준으로 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-129">Because it also supports MSBuild and Visual Studio automation in some project types, it also supports other projects and languages to various degrees.</span></span>

<span data-ttu-id="5d067-130">최신 버전의 NuGet은 C#, Visual Basic, F#, WiX 및 C++을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-130">The most recent version of NuGet supports C#, Visual Basic, F#, WiX, and C++.</span></span>

<span data-ttu-id="5d067-131">**NuGet에서 지원하는 프로젝트 템플릿은 무엇인가요??**</span><span class="sxs-lookup"><span data-stu-id="5d067-131">**What project templates are supported by NuGet?**</span></span>

<span data-ttu-id="5d067-132">NuGet은 Windows, 웹, 클라우드, SharePoint, Wix 등과 같은 다양한 프로젝트 템플릿을 완벽하게 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-132">NuGet has full support for a variety of project templates like Windows, Web, Cloud, SharePoint, Wix, and so on.</span></span>

<span data-ttu-id="5d067-133">**Visual Studio 템플릿의 일부인 패키지를 업데이트하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-133">**How do I update packages that are part of Visual Studio templates?**</span></span>

<span data-ttu-id="5d067-134">패키지 관리자 UI에서 **업데이트** 탭으로 이동하여 **모두 업데이트**를 선택하거나, 패키지 관리자 콘솔에서 [`Update-Package` 명령](../tools/ps-ref-update-package.md)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-134">Go to the **Updates** tab in the Package Manager UI and select **Update All**, or use the [`Update-Package` command](../tools/ps-ref-update-package.md) from the Package Manager Console.</span></span>

<span data-ttu-id="5d067-135">템플릿 자체를 업데이트하려면 템플릿 리포지토리를 수동으로 업데이트해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-135">To update the template itself, you need to manually update the template repository.</span></span> <span data-ttu-id="5d067-136">이 주제에 대한 [Xavier Decoster의 블로그](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-136">See [Xavier Decoster's blog](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages) on this subject.</span></span> <span data-ttu-id="5d067-137">모든 종속성의 최신 버전이 서로 호환되지 않을 경우 수동으로 업데이트하면 템플릿이 손상될 수 있으므로 이 작업은 사용자의 책임 하에 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-137">Note that this is done at your own risk, because manual updates might corrupt the template if the latest version of all dependencies are not compatible with each other.</span></span>

<span data-ttu-id="5d067-138">**Visual Studio 외부에서 NuGet을 사용할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-138">**Can I use NuGet outside of Visual Studio?**</span></span>

<span data-ttu-id="5d067-139">예, NuGet은 명령줄에서 직접 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-139">Yes, NuGet works directly from the command line.</span></span> <span data-ttu-id="5d067-140">[설치 가이드](../install-nuget-client-tools.md) 및 [CLI 참조](../tools/nuget-exe-cli-reference.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-140">See the [Install guide](../install-nuget-client-tools.md) and the [CLI reference](../tools/nuget-exe-cli-reference.md).</span></span>

## <a name="nuget-command-line"></a><span data-ttu-id="5d067-141">NuGet 명령줄</span><span class="sxs-lookup"><span data-stu-id="5d067-141">NuGet command line</span></span>

<span data-ttu-id="5d067-142">**최신 버전의 NuGet 명령줄 도구를 가져오려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-142">**How do I get the latest version of NuGet command line tool?**</span></span>

<span data-ttu-id="5d067-143">[설치 가이드](../install-nuget-client-tools.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-143">See the [Install guide](../install-nuget-client-tools.md).</span></span>

<span data-ttu-id="5d067-144">**nuget.exe에 대한 라이선스는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-144">**What is the license for nuget.exe?**</span></span>

<span data-ttu-id="5d067-145">MIT 라이선스 조건 하에 nuget.exe를 재배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-145">You are allowed to redistribute nuget.exe under the terms of the MIT license.</span></span> <span data-ttu-id="5d067-146">재배포하도록 선택한 nuget.exe의 복사본을 업데이트하고 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-146">You are responsible for updating and servicing any copies of nuget.exe that you choose to redistribute.</span></span>

<span data-ttu-id="5d067-147">**NuGet 명령줄 도구는 확장할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-147">**Is it possible to extend the NuGet command line tool?**</span></span>

<span data-ttu-id="5d067-148">예, [Rob Reynold의 게시물](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx)에서 설명한 대로 사용자 지정 명령을 `nuget.exe`에 추가하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-148">Yes, it's possible to add custom commands to `nuget.exe`, as described in [Rob Reynold's post](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx).</span></span>

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a><span data-ttu-id="5d067-149">NuGet 패키지 관리자 콘솔(Windows의 Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="5d067-149">NuGet Package Manager Console (Visual Studio on Windows)</span></span>

<span data-ttu-id="5d067-150">**패키지 관리자 콘솔에서 DTE 개체에 액세스하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-150">**How do I get access to the DTE object in the Package Manager console?**</span></span>

<span data-ttu-id="5d067-151">Visual Studio 자동화 개체 모델의 최상위 개체를 DTE(개발 도구 환경) 개체라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-151">The top-level object in the Visual Studio automation object model is called the DTE (Development Tools Environment) object.</span></span> <span data-ttu-id="5d067-152">콘솔에서 `$DTE`라는 변수를 통해 이 개체를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-152">The console provides this through a variable named `$DTE`.</span></span> <span data-ttu-id="5d067-153">자세한 내용은 Visual Studio 확장성 설명서에서 [자동화 모델 개요](/visualstudio/extensibility/internals/automation-model-overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-153">For more information, see [Automation Model Overview](/visualstudio/extensibility/internals/automation-model-overview) in the Visual Studio Extensibility documentation.</span></span>

<span data-ttu-id="5d067-154">**$DTE 변수를 DTE2 형식으로 캐스팅하려고 했지만 ""EnvDTE.DTEClass" 형식의 "EnvDTE.DTEClass" 값을 "EnvDTE80.DTE2" 형식으로 변환할 수 없습니다."라는 오류가 발생합니다. 무엇이 문제인가요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-154">**I try to cast the $DTE variable to the type DTE2, but I get an error: Cannot convert the "EnvDTE.DTEClass" value of type "EnvDTE.DTEClass" to type "EnvDTE80.DTE2". What's wrong?**</span></span>

<span data-ttu-id="5d067-155">이는 PowerShell이 COM 개체와 상호 작용하는 방법과 관련하여 알려진 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-155">This is a known issue with how PowerShell interacts with a COM object.</span></span> <span data-ttu-id="5d067-156">다음과 같이 수행해 보세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-156">Try the following:</span></span>

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

<span data-ttu-id="5d067-157">`Get-Interface`는 NuGet PowerShell 호스트에서 추가한 도우미 함수입니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-157">`Get-Interface` is a helper function added by the NuGet PowerShell host.</span></span>

## <a name="creating-and-publishing-packages"></a><span data-ttu-id="5d067-158">패키지 만들기 및 게시</span><span class="sxs-lookup"><span data-stu-id="5d067-158">Creating and publishing packages</span></span>

<span data-ttu-id="5d067-159">**내 패키지를 피드에 나열하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-159">**How do I list my package in a feed?**</span></span>

<span data-ttu-id="5d067-160">[패키지 만들기 및 게시](../quickstart/create-and-publish-a-package.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-160">See [Creating and publishing a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="5d067-161">**다른 버전의 .NET Framework를 대상으로 하는 여러 버전의 라이브러리가 있습니다. 이를 지원하는 단일 패키지를 빌드하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-161">**I have multiple versions of my library that target different versions of the .NET Framework. How do I build a single package that supports this?**</span></span>

<span data-ttu-id="5d067-162">[여러 .NET Framework 버전 지원](../create-packages/supporting-multiple-target-frameworks.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-162">See [Supporting Multiple .NET Framework Versions and Profiles](../create-packages/supporting-multiple-target-frameworks.md).</span></span>

<span data-ttu-id="5d067-163">**내 리포지토리 또는 피드를 설정하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-163">**How do I set up my own repository or feed?**</span></span>

<span data-ttu-id="5d067-164">[패키지 호스팅 개요](../hosting-packages/overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-164">See the [Hosting packages overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="5d067-165">**NuGet 피드에 패키지를 대량으로 업로드하려면 어떻게 해야 할까요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-165">**How can I upload packages to my NuGet feed in bulk?**</span></span>

<span data-ttu-id="5d067-166">[NuGet 패키지 대량 게시](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx)(jeffhandly.com)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-166">See [Bulk publishing NuGet packages](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).</span></span>

## <a name="working-with-packages"></a><span data-ttu-id="5d067-167">패키지 작업</span><span class="sxs-lookup"><span data-stu-id="5d067-167">Working with packages</span></span>

<span data-ttu-id="5d067-168">**프로젝트 수준 패키지와 솔루션 수준 패키지의 차이점은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-168">**What is the difference between a project-level package and a solution-level package?**</span></span>

<span data-ttu-id="5d067-169">솔루션 수준 패키지(NuGet 3.x 이상)는 솔루션에 한 번만 설치되며 솔루션의 모든 프로젝트에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-169">A solution-level package (NuGet 3.x+) is installed only once in a solution and is then available for all projects in the solution.</span></span> <span data-ttu-id="5d067-170">프로젝트 수준 패키지는 이를 사용하는 각 프로젝트에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-170">A project-level package is installed in each project that uses it.</span></span> <span data-ttu-id="5d067-171">또한 솔루션 수준 패키지는 패키지 관리자 콘솔 내에서 호출할 수 있는 새 명령을 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-171">A solution-level package might also install new commands that can be called from within the Package Manager Console.</span></span>

<span data-ttu-id="5d067-172">**인터넷 연결 없이 NuGet 패키지를 설치할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-172">**Is it possible to install NuGet packages without Internet connectivity?**</span></span>

<span data-ttu-id="5d067-173">예, Scott Hanselman의 블로그 게시물인 [nuget.org가 다운되었을 때(또는 비행기에 탑승한 경우) NuGet에 액세스하는 방법](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx)(hanselman.com)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-173">Yes, see Scott Hanselman's Blog post [How to access NuGet when nuget.org is down (or you're on a plane)](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) (hanselman.com).</span></span>

<span data-ttu-id="5d067-174">**기본 패키지 폴더와 다른 위치에 패키지를 설치하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-174">**How do I install packages in a different location from the default packages folder?**</span></span>

<span data-ttu-id="5d067-175">`nuget config -set repositoryPath=<path>`를 사용하여 `Nuget.Config`의 [`repositoryPath`](../reference/nuget-config-file.md#config-section) 설정을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-175">Set the [`repositoryPath`](../reference/nuget-config-file.md#config-section) setting in `Nuget.Config` using `nuget config -set repositoryPath=<path>`.</span></span>

<span data-ttu-id="5d067-176">**NuGet 패키지 폴더를 원본 제어에 추가하지 않도록 방지하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-176">**How do I avoid adding the NuGet packages folder into to source control?**</span></span>

<span data-ttu-id="5d067-177">`Nuget.Config`의 [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section)을 `true`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-177">Set the [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` to `true`.</span></span> <span data-ttu-id="5d067-178">이 키는 솔루션 수준에서 작동하므로 `$(Solutiondir)\.nuget\Nuget.Config` 파일에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-178">This key works at the solution level and hence need to be added to the `$(Solutiondir)\.nuget\Nuget.Config` file.</span></span> <span data-ttu-id="5d067-179">Visual Studio에서 패키지 복원을 사용하면 이 파일이 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-179">Enabling package restore from Visual Studio creates this file automatically.</span></span>

<span data-ttu-id="5d067-180">**패키지 복원을 해제하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-180">**How do I turn off package restore?**</span></span>

<span data-ttu-id="5d067-181">[패키지 복원 사용 설정/해제](../consume-packages/package-restore.md#enabling-and-disabling-package-restore)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-181">See [Enabling and disabling package restore](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).</span></span>

<span data-ttu-id="5d067-182">**원격 종속성이 있는 로컬 패키지를 설치할 때 "종속성을 확인할 수 없습니다."라는 오류 메시지가 표시되는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-182">**Why do I get an "Unable to resolve dependency error" when installing a local package with remote dependencies?**</span></span>

<span data-ttu-id="5d067-183">프로젝트에 로컬 패키지를 설치할 때 **모든** 원본을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-183">You need to select the **All** source when installing a local package into the project.</span></span> <span data-ttu-id="5d067-184">이렇게 하면 하나만 사용하는 대신 모든 피드를 집계합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-184">This aggregates all the feeds instead of using just one.</span></span> <span data-ttu-id="5d067-185">이 오류가 나타나는 이유는 로컬 리포지토리의 사용자가 기업 정책으로 인해 실수로 원격 패키지를 설치하지 않도록 하려는 경우가 많기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-185">The reason this error appears is that users of a local repository often want to avoid accidentally installing a remote package due to corporate polices.</span></span>

<span data-ttu-id="5d067-186">**동일한 폴더에 여러 프로젝트가 있습니다. 각 프로젝트마다 별도의 packages.config 파일을 사용하려면 어떻게 해야 할까요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-186">**I have multiple projects in the same folder, how can I use separate packages.config files for each project?**</span></span>

<span data-ttu-id="5d067-187">개별 프로젝트가 별도의 폴더에 있는 대부분의 프로젝트에서는 NuGet이 각 프로젝트의 `packages.config` 파일을 식별하므로 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-187">In most projects where separate projects live in separate folders, this is not a problem as NuGet identifies the `packages.config` files in each project.</span></span> <span data-ttu-id="5d067-188">동일한 폴더에 NuGet 3.3 이상 및 여러 프로젝트가 있는 경우, `packages.{project-name}.config` 패턴을 사용하는 `packages.config` 파일 이름에 프로젝트 이름을 삽입할 수 있으며, NuGet에서 해당 파일을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-188">With NuGet 3.3+ and multiple projects in the same folder, you can insert the name of the project into the `packages.config` filenames use the pattern `packages.{project-name}.config`, and NuGet uses that file.</span></span>

<span data-ttu-id="5d067-189">이는 PackageReference를 사용할 때 각 프로젝트 파일에 자체의 종속성 목록이 포함되므로 문제가 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-189">This is not an issue when using PackageReference, as each project file contains its own list of dependencies.</span></span>

<span data-ttu-id="5d067-190">**내 리포지토리 목록에 nuget.org가 표시되지 않습니다. 다시 가져오려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-190">**I don't see nuget.org in my list of repositories, how do I get it back?**</span></span>

- <span data-ttu-id="5d067-191">원본 목록에 `https://api.nuget.org/v3/index.json`을 추가합니다. 또는</span><span class="sxs-lookup"><span data-stu-id="5d067-191">Add `https://api.nuget.org/v3/index.json` to your list of sources, or</span></span>
- <span data-ttu-id="5d067-192">`%appdata%\.nuget\NuGet.Config`(Windows) 또는 `~/.nuget/NuGet/NuGet.Config`(Mac/Linux)를 삭제하고 NuGet에서 다시 만들도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-192">Delete `%appdata%\.nuget\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) and let NuGet re-create it.</span></span>

<span data-ttu-id="5d067-193">**패키지에서 특정 라이선스 정보를 제공하지 않는 경우 기본 사용 조건은 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-193">**What are the default license terms if a package doesn't provide specific license information?**</span></span>

<span data-ttu-id="5d067-194">각 패키지는 패키지에 포함된 사용 조건이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-194">Each package is governed by the terms that are included with the package.</span></span> <span data-ttu-id="5d067-195">패키지를 액세스, 다운로드 또는 획득하기 전에 해당 사용 조건을 검토해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-195">You should review the applicable terms before accessing, downloading, or acquiring any packages.</span></span> <span data-ttu-id="5d067-196">nuget.org의 패키지 페이지에 있는 **라이선스 정보** 링크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-196">On nuget.org, use the **License Info** link on the package page.</span></span>

<span data-ttu-id="5d067-197">패키지에서 사용 조건을 지정하지 않은 경우 nuget.org 패키지 페이지의 **연락처 소유자** 링크를 사용하여 패키지 소유자에게 직접 문의해 보세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-197">If a package does not specify the licensing terms, contact the package owner directly using the **Contact owners** link on the nuget.org package page.</span></span> <span data-ttu-id="5d067-198">Microsoft는 타사 패키지 공급자로부터 사용자에게 지적 재산권을 부여하지 않으며 타사에서 제공한 정보에 대해 책임을 지지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-198">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

## <a name="managing-packages-on-nugetorg"></a><span data-ttu-id="5d067-199">nuget.org의 패키지 관리</span><span class="sxs-lookup"><span data-stu-id="5d067-199">Managing packages on nuget.org</span></span>

<span data-ttu-id="5d067-200">**패키지 메타데이터를 업로드한 후에 편집할 수 있나요? 패키지 메타데이터를 변경하기 위해 nuspec을 편집하고 새 패키지를 업로드하는 것이 필요한 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-200">**Can I edit package metadata after it's been uploaded? Why do you require editing the nuspec and uploading a new package for making changes to package metadata?**</span></span>

<span data-ttu-id="5d067-201">NuGet은 모든 패키지에 서명이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-201">NuGet requires all packages to be signed.</span></span> <span data-ttu-id="5d067-202">패키지 서명의 디자인 원칙은 nuspec을 포함한 서명된 패키지 콘텐츠를 변경할 수 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-202">A design principle of package signing is that signed package content must be immutable, which includes the nuspec.</span></span> <span data-ttu-id="5d067-203">패키지 메타데이터를 편집하면 nuspec이 변경되고 기존 서명이 무효화됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-203">Editing the package metadata results in changes to the nuspec, invalidating existing signatures.</span></span> <span data-ttu-id="5d067-204">패키지를 만든 후에 패키지 메타데이터를 편집할 필요가 없도록 기존 워크플로를 수정하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-204">We recommend modifying existing workflows to not require editing the package metadata after the package has been created.</span></span>

<span data-ttu-id="5d067-205">패키지에 대해 나열된 종속성은 패키지 자체에서 자동으로 생성되며 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-205">Note that dependencies listed for your package are generated automatically from the package itself and cannot be edited.</span></span>

<span data-ttu-id="5d067-206">또한 [staging.nuget.org](http://staging.nuget.org)에 패키지를 업로드하는 것은 공용 갤러리에서 패키지를 사용하지 않고도 패키지를 테스트하고 유효성을 검사할 수 있는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-206">In addition, uploading packages to [staging.nuget.org](http://staging.nuget.org) is a great way to test and validate your package without making a package available in the public gallery.</span></span>

<span data-ttu-id="5d067-207">**나중에 게시되는 패키지의 이름을 예약할 수 있나요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-207">**Is it possible to reserve names for packages that will be published in future?**</span></span>

<span data-ttu-id="5d067-208">예.</span><span class="sxs-lookup"><span data-stu-id="5d067-208">Yes.</span></span> <span data-ttu-id="5d067-209">계정에 대한 패키지 ID 접두사를 요청하여 [nuget.org](https://www.nuget.org/)에서 패키지 ID를 예약할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-209">You can reserve IDs for packages on [nuget.org](https://www.nuget.org/) by requesting a package ID prefix for your account.</span></span> <span data-ttu-id="5d067-210">패키지 ID 접두사를 요청하려면 [설명서](https://docs.microsoft.com/nuget/reference/id-prefix-reservation)의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-210">In order to request a package ID prefix, follow the instructions in the [documentation](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).</span></span>

<span data-ttu-id="5d067-211">**패키지 소유권을 주장하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-211">**How do I claim ownership for packages ?**</span></span>

<span data-ttu-id="5d067-212">[nuget.org에서 패키지 소유자 관리](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-212">See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span>

<span data-ttu-id="5d067-213">**소프트웨어 라이선스를 위반하는 패키지 소유자를 처리하려면 어떻게 할까요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-213">**How do I deal with a package owner who is violating my software license?**</span></span>

<span data-ttu-id="5d067-214">NuGet 커뮤니티에서 패키지 소유자와 다른 소프트웨어 소유자 간에 발생할 수 있는 분쟁을 해결하기 위해 함께 노력하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-214">We encourage the NuGet community to work together to resolve any disputes that may arise between package owners and the owners of other software.</span></span> <span data-ttu-id="5d067-215">nuget.org 관리자에게 중재를 요청하기 전에 따라야 할 [분쟁 해결 절차](../policies/dispute-resolution.md)가 마련되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-215">We have crafted a [dispute resolution process](../policies/dispute-resolution.md) to follow before asking nuget.org administrators to intercede.</span></span>

<span data-ttu-id="5d067-216">**내 테스트 패키지를 nuget.org에 업로드하는 것이 좋을까요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-216">**Is it recommended to upload my test packages to nuget.org?**</span></span>

<span data-ttu-id="5d067-217">테스트를 위해 [staging.nuget.org](http://staging.nuget.org) 또는 대체 공용 NuGet 서버(예: [myget.org](https://myget.org) 또는 [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/))를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-217">For test purposes, you can use [staging.nuget.org](http://staging.nuget.org), or alternative public NuGet servers like [myget.org](https://myget.org) or [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/).</span></span>

<span data-ttu-id="5d067-218">staging.nuget.org에 업로드된 패키지는 유지되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-218">Note that packages uploaded to staging.nuget.org may not be preserved.</span></span> <span data-ttu-id="5d067-219">[Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-219">See [Goodbye preview](http://blog.nuget.org/20130419/goodbye-preview.html).</span></span>

<span data-ttu-id="5d067-220">**nuget.org에 업로드할 수 있는 패키지의 최대 크기는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-220">**What is the maximum size of packages I can upload to nuget.org?**</span></span>

<span data-ttu-id="5d067-221">nuget.org는 최대 250MB의 패키지를 허용하지만, 가능한 한 패키지를 1MB 미만으로 유지하고 종속성을 사용하여 패키지를 함께 연결하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-221">nuget.org allows packages up to 250MB, but we recommend keeping packages under 1MB if possible and using dependencies to link packages together.</span></span> <span data-ttu-id="5d067-222">경험상 패키지는 충돌을 방지하기 위해 하나의 어셈블리만 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-222">As a rule of thumb, packages contain only one assembly to avoid collisions.</span></span>

<span data-ttu-id="5d067-223">NuGet은 HTTP를 사용하여 패키지를 다운로드하므로, 큰 패키지는 작은 패키지보다 설치에 실패할 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-223">NuGet uses HTTP to download packages, so larger packages have a higher likelihood of failed installs than smaller ones.</span></span>

<span data-ttu-id="5d067-224">여러 패키지 간에 종속성을 공유하여 NuGet 패키지의 소비자에 대한 전체 다운로드 크기를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-224">It is possible to share dependencies between multiple packages, making the total download size for consumers of your NuGet packages smaller.</span></span>

<span data-ttu-id="5d067-225">종속성은 대부분 정적이며 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-225">Dependencies are mostly static and never change.</span></span> <span data-ttu-id="5d067-226">코드에서 버그를 수정하는 경우 종속성을 업데이트할 필요가 없을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-226">When fixing a bug in code, the dependencies may not need to be updated.</span></span> <span data-ttu-id="5d067-227">종속성을 번들로 제공하면 매번 더 큰 패키지를 다시 전달하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-227">If you bundle dependencies, you end up reshipping larger packages every time.</span></span> <span data-ttu-id="5d067-228">NuGet 패키지를 관련 종속성으로 분할하면 패키지 소비자가 훨씬 더 세부적으로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-228">By splitting NuGet packages into related dependencies, upgrades are much more fine-grained for consumers of your package.</span></span>

## <a name="nugetorg-not-accessible"></a><span data-ttu-id="5d067-229">nuget.org에 액세스할 수 없음</span><span class="sxs-lookup"><span data-stu-id="5d067-229">nuget.org not accessible</span></span>

<span data-ttu-id="5d067-230">**nuget.org에서 패키지를 다운로드하거나 업로드할 수 없는 이유는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-230">**Why can't I download packages from or upload packages to nuget.org?**</span></span>

<span data-ttu-id="5d067-231">먼저 최신 버전의 NuGet을 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-231">First, make sure you're using the latest versions of NuGet.</span></span> <span data-ttu-id="5d067-232">해당 버전이 계속 실패하면 [지원 부서에 문의](https://www.nuget.org/policies/Contact)하여 다음을 포함한 추가 연결 문제 해결 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-232">If that version continues to fail, [contact support](https://www.nuget.org/policies/Contact) and provide additional connection troubleshooting information including:</span></span>

- <span data-ttu-id="5d067-233">사용 중인 NuGet 버전</span><span class="sxs-lookup"><span data-stu-id="5d067-233">The version of NuGet you're using</span></span>
- <span data-ttu-id="5d067-234">사용 중인 패키지 원본</span><span class="sxs-lookup"><span data-stu-id="5d067-234">The package sources you're using</span></span>
- <span data-ttu-id="5d067-235">자세한 세부 정보가 있는 복원 로그</span><span class="sxs-lookup"><span data-stu-id="5d067-235">A restore log with detailed verbosity</span></span>
- <span data-ttu-id="5d067-236">MTR 또는 Fiddler 추적(아래 참조)</span><span class="sxs-lookup"><span data-stu-id="5d067-236">MTR or a Fiddler traces (see below)</span></span>
- <span data-ttu-id="5d067-237">사용자의 지리적 지역</span><span class="sxs-lookup"><span data-stu-id="5d067-237">Your geographical area</span></span>
- <span data-ttu-id="5d067-238">운영 체제 버전</span><span class="sxs-lookup"><span data-stu-id="5d067-238">Your operating system version</span></span>
- <span data-ttu-id="5d067-239">컴퓨터 구성(CPU, 네트워크, 하드 드라이브)</span><span class="sxs-lookup"><span data-stu-id="5d067-239">Machine configuration (CPU, Network, hard drive)</span></span>
- <span data-ttu-id="5d067-240">컴퓨터에서 프록시 또는 방화벽을 사용하는지 여부</span><span class="sxs-lookup"><span data-stu-id="5d067-240">Whether is your machine behind a proxy or firewall</span></span>
- <span data-ttu-id="5d067-241">컴퓨터에 설치된 .NET 버전</span><span class="sxs-lookup"><span data-stu-id="5d067-241">The versions of .NET that are installed on the machine</span></span>
- <span data-ttu-id="5d067-242">사용 중인 플랫폼 간 도구(예: .NET CLI 또는 DNU)의 버전</span><span class="sxs-lookup"><span data-stu-id="5d067-242">Versions of cross-platform tools such as .NET CLI, or DNU that you're using</span></span>

<span data-ttu-id="5d067-243">*MTR을 캡처하려면:*</span><span class="sxs-lookup"><span data-stu-id="5d067-243">*To capture MTR:*</span></span>

- <span data-ttu-id="5d067-244">[http://winmtr.net/download/](http://winmtr.net/)에서 WinMTR 다운로드</span><span class="sxs-lookup"><span data-stu-id="5d067-244">Download WinMTR from [http://winmtr.net/download/](http://winmtr.net/)</span></span>
- <span data-ttu-id="5d067-245">호스트 이름으로 `api.nuget.org`를 입력하고 **시작**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-245">Enter `api.nuget.org` as the hostname and click **Start**.</span></span>
- <span data-ttu-id="5d067-246">**보냄** 열이 100개 이상이 될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-246">Wait until the **Sent** column is >= 100.</span></span>

    ![캡처 중인 MTR](media/mtr.png)

- <span data-ttu-id="5d067-248">클립보드에 텍스트를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-248">Copy text to clipboard.</span></span>

<span data-ttu-id="5d067-249">*Fiddler를 캡처하려면:*</span><span class="sxs-lookup"><span data-stu-id="5d067-249">*To capture Fiddler:*</span></span>

- <span data-ttu-id="5d067-250">최신 버전의 [Fiddler](http://www.telerik.com/download/fiddler)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-250">Install the latest version of [Fiddler](http://www.telerik.com/download/fiddler).</span></span>
- <span data-ttu-id="5d067-251">Fiddler를 시작하고 **파일 > 트래픽 캡처** 메뉴를 사용하여 트래픽 캡처를 사용하지 않도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-251">Start Fiddler and disable capturing traffic using the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="5d067-252">모든 세션을 제거합니다(목록에서 모든 항목을 선택하고 **삭제** 키를 누름).</span><span class="sxs-lookup"><span data-stu-id="5d067-252">Remove all sessions (select all items in the list, press the **Delete** key).</span></span>
- <span data-ttu-id="5d067-253">**도구 > Fiddler 옵션...** 메뉴의 **HTTPS** 탭에서 **HTTPS 트래픽 해독**을 선택하여 HTTPS 트래픽을 캡처하도록 Fiddler를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-253">Configure Fiddler to capture HTTPS traffic by checking **Decrypt HTTPS traffic** in the **HTTPS** tab of the **Tools > Fiddler Options...** menu.</span></span>
- <span data-ttu-id="5d067-254">Visual Studio를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-254">Close Visual Studio.</span></span>
- <span data-ttu-id="5d067-255">**파일 > 트래픽 캡처** 메뉴를 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-255">Enable the **File > Capture Traffic** menu.</span></span>
- <span data-ttu-id="5d067-256">Visual Studio 또는 nuget.exe .exe를 시작하고 작동하지 않는 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-256">Start Visual Studio or nuget.exe .exe and perform the actions that are not working.</span></span> <span data-ttu-id="5d067-257">이러한 작업으로 생성된 트래픽이 Fiddler에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-257">The traffic generated by these actions should show up in Fiddler.</span></span>
- <span data-ttu-id="5d067-258">작업이 실행되면 **파일 > 저장 > 모든 세션**을 사용하여 캡처된 세션을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-258">Once the actions have run, use **File > Save > All Sessions** to store the captured sessions.</span></span>

<span data-ttu-id="5d067-259">참고: Fiddler를 통해 NuGet 트래픽을 라우팅하기 위해 `HTTP_PROXY` 환경 변수를 `http://127.0.0.1:8888`로 설정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5d067-259">Note: it may be required to set the `HTTP_PROXY` environment variable to `http://127.0.0.1:8888` for routing NuGet traffic through Fiddler.</span></span>

<span data-ttu-id="5d067-260">실패하면 [StackOverflow 게시물에서 언급한 팁](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall)을 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="5d067-260">If that fails, try the [tips mentioned in this StackOverflow post](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).</span></span>

<span data-ttu-id="5d067-261">**nuget.org에 대한 API 엔드포인트는 무엇인가요?**</span><span class="sxs-lookup"><span data-stu-id="5d067-261">**What are the API endpoints for nuget.org?**</span></span>

<span data-ttu-id="5d067-262">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/`(V2 API는 더 이상 사용되지 않으며 NuGet 4 이상에서 작동하지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="5d067-262">V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Note that the V2 API is deprecated and does not work with NuGet 4+.)</span></span>
