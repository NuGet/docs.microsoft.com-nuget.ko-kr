---
title: "NuGet 클라이언트 도구 설치 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "클라이언트 도구, CLI(명령줄 인터페이스) 및 Visual Studio용 패키지 관리자 설치에 대한 지침입니다."
keywords: "nuget.exe CLI, NuGet 클라이언트 도구, NuGet 패키지 관리자, NuGet 패키지 관리자 콘솔, Visual Studio용 NuGet, NuGet 베타 채널"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2f67c298d269149bba9f36ad9e026d5443c39b6a
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/05/2018
---
# <a name="installing-nuget-client-tools"></a><span data-ttu-id="cb373-104">NuGet 클라이언트 도구 설치</span><span class="sxs-lookup"><span data-stu-id="cb373-104">Installing NuGet client tools</span></span>

> [!Tip]
> <span data-ttu-id="cb373-105">**패키지 설치를 원하십니까? [빠른 시작 - 패키지 사용](../Quickstart/Use-a-Package.md)을 참조하세요.**</span><span class="sxs-lookup"><span data-stu-id="cb373-105">**Looking to install a package? See [Quickstart - Use a package](../Quickstart/Use-a-Package.md).**</span></span>

<span data-ttu-id="cb373-106">NuGet 패키지를 빌드, 게시 및 사용하는 데 사용할 수 있는 두 가지 기본 도구가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-106">There are two primary tools available to help you build, publish and consume NuGet packages:</span></span>

1. <span data-ttu-id="cb373-107">[**NuGet CLI**](#nuget-cli)는 모든 NuGet 기능을 제공하는 Windows용 명령줄 유틸리티입니다. Mono 또는 .NET Core CLI(`dotnet`)를 사용하여 Mac OSX 및 Linux에서 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-107">The [**NuGet CLI**](#nuget-cli) is the command-line utility for Windows that provides all NuGet capabilities; it can also be run on Mac OSX and Linux using Mono, or through the .NET Core CLI (`dotnet`).</span></span>
1. <span data-ttu-id="cb373-108">[**Visual Studio의 NuGet 패키지 관리자**](#nuget-package-manager-in-visual-studio)(Windows 전용)는 패키지를 관리하기 위한 GUI 도구이며, Visual Studio 내에서 특정 NuGet 명령을 직접 사용할 수 있는 PowerShell 콘솔을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-108">The [**NuGet Package Manager in Visual Studio**](#nuget-package-manager-in-visual-studio) (Windows only) is a GUI tool for managing packages and includes a PowerShell console through which you can use certain NuGet commands directly within Visual Studio.</span></span> <span data-ttu-id="cb373-109">패키지 관리자 UI 및 콘솔은 모두 Visual Studio(Windows) 2012 이상에 포함되어 있으며 이전 버전에는 수동으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-109">The Package Manager UI and Console are both included with Visual Studio (on Windows) 2012 and later and can be installed manually for earlier versions.</span></span>

    <span data-ttu-id="cb373-110">Mac용 Visual Studio에는 NuGet 기능이 직접 기본적으로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-110">With Visual Studio for Mac, NuGet capabilities are built in directly.</span></span> <span data-ttu-id="cb373-111">연습은 [프로젝트에 NuGet 패키지 포함](/visualstudio/mac/nuget-walkthrough)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cb373-111">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough) for a walkthrough.</span></span>

    <span data-ttu-id="cb373-112">현재 Visual Studio Code에는 기본 제공 NuGet 지원이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-112">Visual Studio Code at present does not have any built-in NuGet support.</span></span> <span data-ttu-id="cb373-113">NuGet CLI 또는 [dotnet CLI](../Tools/dotnet-Commands.md)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-113">Use the NuGet CLI or the [dotnet CLI](../Tools/dotnet-Commands.md).</span></span>

<span data-ttu-id="cb373-114">NuGet CLI 및 패키지 관리자는 모두 다음 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-114">The NuGet CLI and Package Manager both support the following operations:</span></span>

- <span data-ttu-id="cb373-115">패키지 검색</span><span class="sxs-lookup"><span data-stu-id="cb373-115">Search packages</span></span>
- <span data-ttu-id="cb373-116">패키지 설치</span><span class="sxs-lookup"><span data-stu-id="cb373-116">Install packages</span></span>
- <span data-ttu-id="cb373-117">패키지 업데이트</span><span class="sxs-lookup"><span data-stu-id="cb373-117">Update packages</span></span>
- <span data-ttu-id="cb373-118">패키지 제거</span><span class="sxs-lookup"><span data-stu-id="cb373-118">Uninstall packages</span></span>
- <span data-ttu-id="cb373-119">패키지 복원(패키지 관리자에서 UI만)</span><span class="sxs-lookup"><span data-stu-id="cb373-119">Restore packages (UI only in the Package Manager)</span></span>
- <span data-ttu-id="cb373-120">NuGet 원본 관리</span><span class="sxs-lookup"><span data-stu-id="cb373-120">Manage NuGet sources</span></span>

<span data-ttu-id="cb373-121">다음 기능은 NuGet CLI에서만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-121">The following capabilities are supported only in the NuGet CLI:</span></span>

- <span data-ttu-id="cb373-122">패키지 관리(nuget.org 또는 개인 피드)</span><span class="sxs-lookup"><span data-stu-id="cb373-122">Manage packages (nuget.org or private feed)</span></span>
- <span data-ttu-id="cb373-123">패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="cb373-123">Create packages</span></span> 
- <span data-ttu-id="cb373-124">패키지 게시</span><span class="sxs-lookup"><span data-stu-id="cb373-124">Publish packages</span></span>
- <span data-ttu-id="cb373-125">Nuget.Config 관리</span><span class="sxs-lookup"><span data-stu-id="cb373-125">Manage Nuget.Config</span></span>
- <span data-ttu-id="cb373-126">NuGet 캐시 관리</span><span class="sxs-lookup"><span data-stu-id="cb373-126">Manage the NuGet cache</span></span>
- <span data-ttu-id="cb373-127">패키지 복제</span><span class="sxs-lookup"><span data-stu-id="cb373-127">Replicating a package</span></span>

> [!Note]
> <span data-ttu-id="cb373-128">또 다른 좋은 도구는 NuGet 패키지를 시각적으로 탐색, 생성 및 편집할 수 있는 오픈 소스 독립 실행형 도구인 [NuGet 패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)입니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-128">Another good tool is the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), an open-source, stand-alone tool to visually explore, create, and edit NuGet packages.</span></span> <span data-ttu-id="cb373-129">예를 들어 매번 패키지를 다시 빌드할 필요 없이 패키지 구조를 실험적으로 변경하는 것이 매우 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-129">It's very helpful, for example, to make experimental changes to a package structure without having to rebuild the package each time.</span></span>
> <span data-ttu-id="cb373-130">.NET Core 응용 프로그램 개발에 사용되는 플랫폼 간 [.NET Core CLI](/dotnet/articles/core/tools/index#installation) 도구 체인은 delete, locals, push, pack 및 restore와 같은 몇 가지 NuGet 명령을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-130">The cross-platform [.NET Core CLI](/dotnet/articles/core/tools/index#installation) toolchain, used for developing .NET Core applications, supports several NuGet commands, such as delete, locals, push, pack, and restore.</span></span> 

## <a name="nuget-cli"></a><span data-ttu-id="cb373-131">NuGet CLI</span><span class="sxs-lookup"><span data-stu-id="cb373-131">NuGet CLI</span></span>

<span data-ttu-id="cb373-132">NuGet 명령줄 인터페이스는 모든 NuGet 기능에 대한 액세스를 제공하며, 다음 섹션에서 설명한 대로 Windows, Mac OSX 및 Linux에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-132">The NuGet command-line interface provides access to all NuGet capabilities, and can be run on Windows, Mac OSX, and Linux as described in the following sections.</span></span>

### <a name="windows"></a><span data-ttu-id="cb373-133">Windows</span><span class="sxs-lookup"><span data-stu-id="cb373-133">Windows</span></span>

<span data-ttu-id="cb373-134">**직접 다운로드:**</span><span class="sxs-lookup"><span data-stu-id="cb373-134">**Direct download:**</span></span>

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> <span data-ttu-id="cb373-135">NuGet 1.4 이상을 사용하면 `nuget update -self`를 사용하여 기존 nuget.exe를 최신 버전으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-135">With NuGet 1.4+, you can use `nuget update -self` to update your existing nuget.exe to the latest version.</span></span>

<span data-ttu-id="cb373-136">**다른 방법:**</span><span class="sxs-lookup"><span data-stu-id="cb373-136">**Other methods:**</span></span>

- <span data-ttu-id="cb373-137">**Chocolatey**: [Chocolatey](http://chocolatey.org) 클라이언트를 사용하여 [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-137">**Chocolatey**: Install the [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey package using the [Chocolatey](http://chocolatey.org) client.</span></span> 

    ```ps
    choco install nuget.commandline
    ```

- <span data-ttu-id="cb373-138">**Visual Studio**: Visual Studio의 패키지 관리자 콘솔에서 [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-138">**Visual Studio**: Install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the Package Manager Console in Visual Studio.</span></span>

    > [!Note]
    > <span data-ttu-id="cb373-139">**NuGet 2.x 사용자의 경우**: NuGet 3.2에 도입된 주요 변경으로 인해 [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe)는 지속적인 통합 시스템이 잠재적으로 손상되지 않도록 안정적인 최신 NuGet 2.x 릴리스를 가리킵니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-139">**For NuGet 2.x users**: Because of breaking changes introduced in NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) points to the latest stable NuGet 2.x release to prevent continuous integration systems from potentially breaking.</span></span>

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a><span data-ttu-id="cb373-140">Mac OSX 및 Linux</span><span class="sxs-lookup"><span data-stu-id="cb373-140">Mac OSX and Linux</span></span>

<span data-ttu-id="cb373-141">Mac OSX 및 Linux의 경우 NuGet CLI를 실행하는 다음 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-141">On Mac OSX and Linux, there are two ways to run the NuGet CLI:</span></span>

- <span data-ttu-id="cb373-142">핵심 NuGet 기능이 포함된 [.NET Core SDK](https://www.microsoft.com/net/download/core)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-142">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core), which includes the core NuGet capabilities.</span></span> <span data-ttu-id="cb373-143">다운로드는 [github.com/dotnet/cli](https://github.com/dotnet/cli)에도 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-143">Downloads are also listed on [github.com/dotnet/cli](https://github.com/dotnet/cli).</span></span> <span data-ttu-id="cb373-144">더 완벽한 기능이 필요한 경우 아래의 두 번째 옵션을 사용하여 Mono에서 `nuget.exe`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-144">If you need fuller capabilities, then use the second option below to use `nuget.exe` with Mono.</span></span>

- <span data-ttu-id="cb373-145">[Mono](http://www.mono-project.com/docs/getting-started/install/)를 설치한 다음 [nuget.org/downloads](https://nuget.org/downloads)에서 `nuget.exe` Windows용 명령줄 실행 파일(버전 3.2 이상)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-145">Install [Mono](http://www.mono-project.com/docs/getting-started/install/) and then use the `nuget.exe` command-line executable for Windows (version 3.2 and later) from [nuget.org/downloads](https://nuget.org/downloads).</span></span> <span data-ttu-id="cb373-146">Mono에서 NuGet을 실행하는 경우 적용되는 제한 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-146">Running NuGet on Mono is subject to the following limitations:</span></span>

    - <span data-ttu-id="cb373-147">제대로 작동하는지 테스트된 명령:</span><span class="sxs-lookup"><span data-stu-id="cb373-147">Commands tested to work:</span></span>
        - <span data-ttu-id="cb373-148">config</span><span class="sxs-lookup"><span data-stu-id="cb373-148">config</span></span>
        - <span data-ttu-id="cb373-149">삭제</span><span class="sxs-lookup"><span data-stu-id="cb373-149">delete</span></span>
        - <span data-ttu-id="cb373-150">도움말</span><span class="sxs-lookup"><span data-stu-id="cb373-150">help</span></span>
        - <span data-ttu-id="cb373-151">install</span><span class="sxs-lookup"><span data-stu-id="cb373-151">install</span></span>
        - <span data-ttu-id="cb373-152">list</span><span class="sxs-lookup"><span data-stu-id="cb373-152">list</span></span>
        - <span data-ttu-id="cb373-153">push</span><span class="sxs-lookup"><span data-stu-id="cb373-153">push</span></span>
        - <span data-ttu-id="cb373-154">setApiKey</span><span class="sxs-lookup"><span data-stu-id="cb373-154">setApiKey</span></span>
        - <span data-ttu-id="cb373-155">sources</span><span class="sxs-lookup"><span data-stu-id="cb373-155">sources</span></span>
        - <span data-ttu-id="cb373-156">spec</span><span class="sxs-lookup"><span data-stu-id="cb373-156">spec</span></span>

    - <span data-ttu-id="cb373-157">부분적으로 작동하는 명령:</span><span class="sxs-lookup"><span data-stu-id="cb373-157">Partially-working commands:</span></span>
        - <span data-ttu-id="cb373-158">pack: `.nuspec` 파일은 사용할 수 있지만 프로젝트 파일은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-158">pack: works with `.nuspec` files but not with project files.</span></span>
        - <span data-ttu-id="cb373-159">restore: `packages.config` 및 `project.json` 파일은 사용할 수 있지만 솔루션(`.sln`) 파일은 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-159">restore: works with `packages.config` and `project.json` files but not with solution (`.sln`) files.</span></span>

    - <span data-ttu-id="cb373-160">작동하지 않는 명령:</span><span class="sxs-lookup"><span data-stu-id="cb373-160">Commands that do not work:</span></span>
        - <span data-ttu-id="cb373-161">업데이트</span><span class="sxs-lookup"><span data-stu-id="cb373-161">update</span></span>

### <a name="related-topics"></a><span data-ttu-id="cb373-162">관련 항목</span><span class="sxs-lookup"><span data-stu-id="cb373-162">Related topics</span></span>

- [<span data-ttu-id="cb373-163">NuGet CLI 참조</span><span class="sxs-lookup"><span data-stu-id="cb373-163">NuGet CLI reference</span></span>](../tools/nuget-exe-cli-reference.md)
- [<span data-ttu-id="cb373-164">패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="cb373-164">Creating a package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="cb373-165">패키지 게시</span><span class="sxs-lookup"><span data-stu-id="cb373-165">Publishing a Package</span></span>](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a><span data-ttu-id="cb373-166">Visual Studio의 NuGet 패키지 관리자</span><span class="sxs-lookup"><span data-stu-id="cb373-166">NuGet Package Manager in Visual Studio</span></span>

<span data-ttu-id="cb373-167">Windows의 모든 Visual Studio 버전(2012 이상)에는 NuGet 패키지 관리자가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-167">The NuGet Package Manager is included in every edition of Visual Studio on Windows, 2012 and later.</span></span> <span data-ttu-id="cb373-168">여기에는 패키지 관리자 UI([참조](../tools/package-manager-ui.md)) 및 특정 패키지([참조](../tools/package-manager-console.md))와 함께 제공되는 도구에 액세스할 수 있는 패키지 관리자 콘솔이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-168">It includes the Package Manager UI ([reference](../tools/package-manager-ui.md)), and the Package Manager Console through which you can access tools that come with certain packages ([reference](../tools/package-manager-console.md)).</span></span>

<span data-ttu-id="cb373-169">Visual Studio 2017 설치 관리자에는 .NET을 사용하는 모든 워크로드가 있는 NuGet 패키지 관리자가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-169">The Visual Studio 2017 installer includes the NuGet Package Manager with any workload that employs .NET.</span></span> <span data-ttu-id="cb373-170">별도로 설치하거나 패키지 관리자가 설치되어 있는지 확인하려면 Visual Studio 2017 설치 관리자를 실행하고 **개별 구성 요소 > 코드 도구 > NuGet 패키지 관리자** 아래에서 옵션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-170">To install separately, or to verify that the Package Manager is installed, run the Visual Studio 2017 installer and check the option under **Individual Components > Code tools > NuGet package manager**.</span></span>

> [!Note]
> <span data-ttu-id="cb373-171">콘솔에는 Windows 7 이상 및 Windows Server 2008 R2 이상에 이미 설치되어 있는 [PowerShell 2.0](http://support.microsoft.com/kb/968929)이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-171">The console requires [PowerShell 2.0](http://support.microsoft.com/kb/968929), which will already be installed on Windows 7 or higher and Windows Server 2008 R2 or higher.</span></span>
>
> <span data-ttu-id="cb373-172">또한 패키지 관리자 콘솔 명령은 Windows의 Visual Studio 내에서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-172">Package Manager Console commands also work only within Visual Studio on Windows.</span></span> <span data-ttu-id="cb373-173">Mac용 Visual Studio 및 Visual Studio Code를 포함하여 해당 환경 외부에서 NuGet CLI를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-173">Use the NuGet CLI outside of that environment, including with Visual Studio for Mac and Visual Studio Code.</span></span>

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a><span data-ttu-id="cb373-174">Visual Studio 2010 및 이전 버전용 패키지 관리자 설치</span><span class="sxs-lookup"><span data-stu-id="cb373-174">Package Manager installation for Visual Studio 2010 and earlier</span></span>

<span data-ttu-id="cb373-175">*패키지 관리자가 이미 포함된 Visual Studio 2012 이상에서는 다음 단계가 필요하지 않습니다.*</span><span class="sxs-lookup"><span data-stu-id="cb373-175">*These steps are not necessary for Visual Studio 2012 and later, which already include the Package Manager.*</span></span>

1. <span data-ttu-id="cb373-176">Visual Studio 2010 및 이전 버전에서는 **도구 > 확장 및 업데이트**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-176">In Visual Studio 2010 and earlier, click **Tools > Extension and Updates**.</span></span>
1. <span data-ttu-id="cb373-177">**온라인**으로 이동한 다음 "Visual Studio용 NuGet 패키지 관리자"를 검색하고 **다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-177">Navigate to **Online**, then search for "NuGet Package Manager for Visual Studio" and click **Download**.</span></span>
1. <span data-ttu-id="cb373-178">설치 관리자 대화 상자에서 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-178">In the Installer dialog box, click **Install**.</span></span>
1. <span data-ttu-id="cb373-179">설치가 완료되면 Visual Studio를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-179">When installation is complete, restart Visual Studio.</span></span>

> [!Tip]
> <span data-ttu-id="cb373-180">Visual Studio에서 **확장 및 업데이트** 대화 상자를 사용할 수 없는 경우(예: 프록시로 인해 차단된 경우) [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)에서 직접 Visual Studio 2013 및 2015용 확장을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-180">If you're unable to use the **Extensions and Updates** dialog in Visual Studio (for example, its blocked by a proxy), you can download extensions for Visual Studio 2013 and 2015 directly at [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

### <a name="updating-the-package-manager"></a><span data-ttu-id="cb373-181">패키지 관리자 업데이트</span><span class="sxs-lookup"><span data-stu-id="cb373-181">Updating the Package Manager</span></span>

<span data-ttu-id="cb373-182">Visual Studio 2015 업데이트 2 이상의 경우, 패키지 관리자는 자동으로 안정적인 최신 릴리스로 업데이트됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-182">For Visual Studio 2015 Update 2 and later, the Package Manager is automatically updated to the latest stable release.</span></span>

<span data-ttu-id="cb373-183">Visual Studio 2015 업데이트 1 및 이전 버전의 경우, **도구 > 확장 및 업데이트**  명령을 선택하고 **업데이트** 탭을 클릭하여 패키지 관리자의 새 버전을 사용할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-183">For Visual Studio 2015 Update 1 and earlier, select the **Tools > Extensions and Updates** command and click on the **Updates** tab to see if a new version of the Package Manager is available.</span></span>  

### <a name="nuget-previews"></a><span data-ttu-id="cb373-184">NuGet 미리 보기</span><span class="sxs-lookup"><span data-stu-id="cb373-184">NuGet previews</span></span>

<span data-ttu-id="cb373-185">예정된 NuGet 기능을 미리 보려면 안정적인 Visual Studio 릴리스와 함께 작동하는 [Visual Studio 2017 미리 보기](https://www.visualstudio.com/vs/preview/)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-185">If you'd like to preview upcoming NuGet features, install the [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), which works side-by-side with stable releases of Visual Studio.</span></span>

<span data-ttu-id="cb373-186">이전의 Visual Studio 2015용 NuGet 베타 채널(`https://dotnet.myget.org/F/nuget-beta/vsix/`)은 더 이상 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cb373-186">Note that the previous NuGet Beta Channel (`https://dotnet.myget.org/F/nuget-beta/vsix/`) for Visual Studio 2015 is no longer used.</span></span>

<span data-ttu-id="cb373-187">모든 NuGet 릴리스 관련 문제를 보고하거나 아이디어를 공유하려면 [NuGet GitHub 리포지토리](https://github.com/Nuget/Home)에서 문제를 공개해 주세요.</span><span class="sxs-lookup"><span data-stu-id="cb373-187">To report problems with any release of NuGet or to share ideas, open an issue on the [NuGet GitHub repository](https://github.com/Nuget/Home).</span></span>

### <a name="related-topics"></a><span data-ttu-id="cb373-188">관련 항목</span><span class="sxs-lookup"><span data-stu-id="cb373-188">Related topics</span></span>

- [<span data-ttu-id="cb373-189">패키지 관리자 UI 참조</span><span class="sxs-lookup"><span data-stu-id="cb373-189">Package Manager UI reference</span></span>](../tools/package-manager-ui.md)
- [<span data-ttu-id="cb373-190">패키지 관리자 콘솔 참조</span><span class="sxs-lookup"><span data-stu-id="cb373-190">Package Manager Console reference</span></span>](../tools/package-manager-console.md)
- [<span data-ttu-id="cb373-191">패키지 관리자 콘솔 PowerShell 참조</span><span class="sxs-lookup"><span data-stu-id="cb373-191">Package Manager Console PowerShell reference</span></span>](../tools/powershell-reference.md)