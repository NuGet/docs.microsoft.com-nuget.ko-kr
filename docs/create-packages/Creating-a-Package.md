---
title: NuGet 패키지를 만드는 방법
description: 파일 및 버전 관리와 같은 주요 결정 사항을 포함하여 NuGet 패키지를 디자인하고 만드는 과정을 자세히 안내합니다.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1dce8556448131c36680167fdc3605e4378b9178
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842300"
---
# <a name="create-nuget-packages"></a><span data-ttu-id="69c34-103">NuGet 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="69c34-103">Create NuGet packages</span></span>

<span data-ttu-id="69c34-104">패키지의 기능 또는 포함된 코드와 관계없이 CLI 도구인 `nuget.exe` 또는 `dotnet.exe`를 사용하여 해당 기능을 임의 수의 다른 개발자와 공유하고 사용할 수 있는 구성 요소로 패키지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="69c34-105">NuGet CLI 도구를 설치하려면 [NuGet 클라이언트 도구 설치](../install-nuget-client-tools.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c34-105">To install NuGet CLI tools, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="69c34-106">Visual Studio에는 CLI 도구가 자동으로 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-106">Note that Visual Studio does not automatically include a CLI tool.</span></span>

- <span data-ttu-id="69c34-107">[SDK 스타일 형식](../resources/check-project-format.md)을 사용하는 .NET Core 및 .NET Standard 프로젝트와 또 다른 SDK 스타일 프로젝트의 경우, NuGet은 프로젝트 파일의 정보를 직접 사용하여 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-107">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="69c34-108">자세한 단계는 [dotnet CLI를 사용하여 .NET Standard 패키지 만들기](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md), [Visual Studion를 사용하여 .NET Standard 패키지 만들기](../quickstart/create-and-publish-a-package-using-visual-studio.md) 또는 [MSBuild 대상으로서의 NuGet pack 및 restore](../reference/msbuild-targets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c34-108">For detailed steps, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md), [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md) or [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

- <span data-ttu-id="69c34-109">SDK 스타일이 아닌 프로젝트(일반적으로 .NET Framework 프로젝트)의 경우에는 이 문서에 설명된 단계에 따라 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-109">For non-SDK-style projects, typically .NET Framework projects, follow the steps described in this article to create a package.</span></span> <span data-ttu-id="69c34-110">[.NET Framework 패키지 만들기 및 게시](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)의 단계에 따라 `nuget.exe` CLI 및 Visual Studio를 사용하여 패키지를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-110">You can also follow the steps in [Create and publish a .NET Framework package](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md) to create a package using the `nuget.exe` CLI and Visual Studio.</span></span>

- <span data-ttu-id="69c34-111">`packages.config`에서 [PackageReference](../consume-packages/package-references-in-project-files.md)로 마이그레이션된 프로젝트의 경우에는 [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-111">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), use [msbuild -t:pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

<span data-ttu-id="69c34-112">엄밀히 말해, NuGet 패키지는 `.nupkg` 확장명으로 이름이 변경되고 내용이 특정 규칙과 일치하는 ZIP 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-112">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="69c34-113">규칙을 충족하는 패키지를 만드는 자세한 프로세스에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-113">This topic describes the detailed process of creating a package that meets those conventions.</span></span>

<span data-ttu-id="69c34-114">패키징은 패키지로 전달하려는 컴파일된 코드(어셈블리), 기호 및/또는 기타 파일로 시작됩니다([개요 및 워크플로](overview-and-workflow.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="69c34-114">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="69c34-115">이 프로세스는 프로젝트 파일의 정보에서 끌어오기를 사용하여 컴파일된 어셈블리 및 패키지를 동기화된 상태로 유지할 수 있지만, 패키지에 포함된 파일을 컴파일하거나 생성하는 프로세스와는 관련이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-115">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Important]
> <span data-ttu-id="69c34-116">이 항목은 SDK 스타일이 아닌 프로젝트 즉, 일반적으로 Visual Studio 2017 이상 버전 및 NuGet 4.0+를 사용하는 .NET Core 및 .NET Standard 프로젝트가 아닌 프로젝트에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-116">This topic applies to non-SDK-style projects, typically projects other than .NET Core and .NET Standard projects using Visual Studio 2017 and higher versions and NuGet 4.0+.</span></span>

## <a name="decide-which-assemblies-to-package"></a><span data-ttu-id="69c34-117">패키지할 어셈블리 결정</span><span class="sxs-lookup"><span data-stu-id="69c34-117">Decide which assemblies to package</span></span>

<span data-ttu-id="69c34-118">가장 일반적인 용도의 패키지에는 다른 개발자가 자신의 프로젝트에서 사용할 수 있는 하나 이상의 어셈블리가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-118">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="69c34-119">일반적으로 각 어셈블리가 독립적으로 유용한 경우 NuGet 패키지당 하나의 어셈블리가 있는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-119">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="69c34-120">예를 들어 `Parser.dll`에 종속된 `Utilities.dll`이 있고 `Parser.dll`이 자체적으로 유용할 경우 각각에 대해 하나의 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-120">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="69c34-121">이렇게 하면 개발자가 `Utilities.dll`과는 독립적으로 `Parser.dll`을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-121">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="69c34-122">라이브러리가 독립적으로 유용하지 않은 여러 어셈블리로 구성된 경우 이를 하나의 패키지로 결합하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-122">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="69c34-123">앞의 예제를 사용하여 `Utilities.dll`에서만 사용되는 코드가 `Parser.dll`에 포함된 경우 동일한 패키지에 `Parser.dll`을 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-123">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="69c34-124">마찬가지로, `Utilities.dll`이 `Utilities.resources.dll`에 종속되고 후자가 자체적으로 유용하지 않은 경우 두 라이브러리를 모두 동일한 패키지에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-124">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="69c34-125">실제로 리소스는 특별한 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-125">Resources are, in fact, a special case.</span></span> <span data-ttu-id="69c34-126">패키지가 프로젝트에 설치되면 어셈블리 참조가 지역화된 위성 어셈블리로 간주되므로 NuGet은 `.resources.dll`이라는 DLL을 *제외한* 패키지의 DLL에 해당 어셈블리 참조를 자동으로 추가합니다([지역화된 패키지 만들기](creating-localized-packages.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="69c34-126">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="69c34-127">이러한 이유로 다른 경우에 필수 패키지 코드가 포함되는 파일에는 `.resources.dll`을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="69c34-127">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="69c34-128">라이브러리에 COM interop 어셈블리가 포함되어 있으면 [COM interop 어셈블리가 포함된 패키지 만들기](author-packages-with-com-interop-assemblies.md)의 지침을 추가로 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="69c34-128">If your library contains COM interop assemblies, follow additional the guidelines in [Create packages with COM interop assemblies](author-packages-with-com-interop-assemblies.md).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="69c34-129">.nuspec 파일의 역할 및 구조</span><span class="sxs-lookup"><span data-stu-id="69c34-129">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="69c34-130">패키지하려는 파일을 알고 있으면 다음 단계는 `.nuspec` XML 파일에 패키지 매니페스트를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-130">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="69c34-131">매니페스트:</span><span class="sxs-lookup"><span data-stu-id="69c34-131">The manifest:</span></span>

1. <span data-ttu-id="69c34-132">패키지의 내용을 설명하며 패키지에 직접 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-132">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="69c34-133">패키지를 만들도록 구동하고 프로젝트에 해당 패키지를 설치하는 방법을 NuGet에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-133">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="69c34-134">예를 들어 매니페스트는 다른 패키지 종속성을 식별하여 NuGet에서 기본 패키지를 설치할 때 해당 종속성을 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-134">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="69c34-135">아래에서 설명한 대로 필수 및 선택적 속성을 모두 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-135">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="69c34-136">여기서 언급하지 않은 다른 속성을 포함하여 정확한 세부 정보는 [.nuspec 참조](../reference/nuspec.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c34-136">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="69c34-137">필수 속성:</span><span class="sxs-lookup"><span data-stu-id="69c34-137">Required properties:</span></span>

- <span data-ttu-id="69c34-138">패키지를 호스팅하는 갤러리에서 고유해야 하는 패키지 식별자</span><span class="sxs-lookup"><span data-stu-id="69c34-138">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="69c34-139">*Major.Minor.Patch[-Suffix]* 형식의 특정 버전 번호(여기서 *-Suffix*는 [시험판 버전](prerelease-packages.md)을 식별함)</span><span class="sxs-lookup"><span data-stu-id="69c34-139">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="69c34-140">호스트에 표시되어야 하는 패키지 제목(예: nuget.org)</span><span class="sxs-lookup"><span data-stu-id="69c34-140">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="69c34-141">작성자 및 소유자 정보</span><span class="sxs-lookup"><span data-stu-id="69c34-141">Author and owner information.</span></span>
- <span data-ttu-id="69c34-142">패키지에 대한 자세한 설명</span><span class="sxs-lookup"><span data-stu-id="69c34-142">A long description of the package.</span></span>

<span data-ttu-id="69c34-143">선택적 일반 속성:</span><span class="sxs-lookup"><span data-stu-id="69c34-143">Common optional properties:</span></span>

- <span data-ttu-id="69c34-144">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="69c34-144">Release notes</span></span>
- <span data-ttu-id="69c34-145">저작권 정보</span><span class="sxs-lookup"><span data-stu-id="69c34-145">Copyright information</span></span>
- <span data-ttu-id="69c34-146">[Visual Studio의 패키지 관리자 UI](../tools/package-manager-ui.md)에 대한 간단한 설명</span><span class="sxs-lookup"><span data-stu-id="69c34-146">A short description for the [Package Manager UI in Visual Studio](../tools/package-manager-ui.md)</span></span>
- <span data-ttu-id="69c34-147">로캘 ID</span><span class="sxs-lookup"><span data-stu-id="69c34-147">A locale ID</span></span>
- <span data-ttu-id="69c34-148">프로젝트 URL</span><span class="sxs-lookup"><span data-stu-id="69c34-148">Project URL</span></span>
- <span data-ttu-id="69c34-149">라이선스(식 또는 파일로 사용)(`licenseUrl`은 사용되지 않으며, [`license`nusec 메타데이터 요소](../reference/nuspec.md#license)를 사용함)</span><span class="sxs-lookup"><span data-stu-id="69c34-149">License as an expression or file (`licenseUrl` is being deprecated, use the [`license` nuspec metadata element](../reference/nuspec.md#license))</span></span>
- <span data-ttu-id="69c34-150">아이콘 URL</span><span class="sxs-lookup"><span data-stu-id="69c34-150">An icon URL</span></span>
- <span data-ttu-id="69c34-151">종속성 및 참조 목록</span><span class="sxs-lookup"><span data-stu-id="69c34-151">Lists of dependencies and references</span></span>
- <span data-ttu-id="69c34-152">갤러리 검색을 지원하는 태그</span><span class="sxs-lookup"><span data-stu-id="69c34-152">Tags that assist in gallery searches</span></span>

<span data-ttu-id="69c34-153">다음은 속성을 설명하는 주석이 포함된 가상의 일반적인 `.nuspec` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-153">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
        <!-- The identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- The package version number that is used when resolving dependencies -->
        <version>1.8.3-beta</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

<span data-ttu-id="69c34-154">종속성 선언 및 버전 번호 지정에 대한 자세한 내용은 [패키지 버전 관리](../reference/package-versioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c34-154">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="69c34-155">`dependency` 요소의 `include` 및 `exclude` 특성을 사용하여 패키지에 종속성의 자산을 직접 공개할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-155">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="69c34-156">[.nuspec 참조 - 종속성](../reference/nuspec.md#dependencies)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c34-156">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="69c34-157">매니페스트는 이 매니페스트에서 만든 패키지에 포함되어 있으므로 기존 패키지를 검사하여 임의 개수의 추가 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-157">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="69c34-158">좋은 소스는 컴퓨터에 있는 *global-packages* 폴더이며, 해당 위치는 다음 명령으로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-158">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="69c34-159">*package\version* 폴더로 이동하여 `.nupkg` 파일을 `.zip` 파일에 복사한 다음, 해당 `.zip` 파일을 열고 그 안에 있는 `.nuspec` 파일을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-159">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="69c34-160">Visual Studio 프로젝트에서 `.nuspec`을 만드는 경우 패키지를 빌드할 때 프로젝트의 정보로 대체되는 토큰이 매니페스트에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-160">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="69c34-161">[Visual Studio 프로젝트에서 .nuspec 만들기](#from-a-visual-studio-project)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c34-161">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="create-the-nuspec-file"></a><span data-ttu-id="69c34-162">.nuspec 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="69c34-162">Create the .nuspec file</span></span>

<span data-ttu-id="69c34-163">완전한 매니페스트를 만드는 것은 일반적으로 다음 방법 중 하나를 통해 생성된 기본 `.nuspec` 파일로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-163">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="69c34-164">규칙 기반 작업 디렉터리</span><span class="sxs-lookup"><span data-stu-id="69c34-164">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="69c34-165">어셈블리 DLL</span><span class="sxs-lookup"><span data-stu-id="69c34-165">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="69c34-166">Visual Studio 프로젝트</span><span class="sxs-lookup"><span data-stu-id="69c34-166">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="69c34-167">기본값이 있는 새 파일</span><span class="sxs-lookup"><span data-stu-id="69c34-167">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="69c34-168">그런 다음 최종 패키지에 원하는 정확한 내용을 설명하도록 파일을 직접 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-168">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="69c34-169">생성된 `.nuspec` 파일에는 `nuget pack` 명령을 사용하여 패키지를 만들기 전에 수정해야 하는 자리 표시자가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-169">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="69c34-170">`.nuspec`에 자리 표시자가 있으면 이 명령이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-170">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="69c34-171">원본: 규칙 기반 작업 디렉터리</span><span class="sxs-lookup"><span data-stu-id="69c34-171">From a convention-based working directory</span></span>

<span data-ttu-id="69c34-172">NuGet 패키지는 `.nupkg` 확장명으로 이름이 바뀐 ZIP 파일일 뿐이므로 로컬 파일 시스템에서 원하는 폴더 구조를 만든 다음, 해당 구조에서 `.nuspec` 파일을 직접 만드는 것이 가장 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-172">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="69c34-173">그런 다음, `nuget pack` 명령은 해당 폴더 구조의 모든 파일을 자동으로 추가합니다(동일한 구조의 개인 파일을 유지할 수 있도록 `.`로 시작하는 폴더는 제외함).</span><span class="sxs-lookup"><span data-stu-id="69c34-173">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="69c34-174">이 방식의 장점은 이 항목의 뒷부분에서 설명한 대로 패키지에 포함하려는 파일을 매니페스트에 지정할 필요가 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-174">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="69c34-175">빌드 프로세스에서 패키지로 이동하는 정확한 폴더 구조를 생성하기만 하면 되고, 그렇지 않은 경우 프로젝트의 일부가 아닌 다른 파일을 쉽게 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-175">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="69c34-176">대상 프로젝트에 삽입해야 하는 콘텐츠 및 소스 코드</span><span class="sxs-lookup"><span data-stu-id="69c34-176">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="69c34-177">PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="69c34-177">PowerShell scripts</span></span>
- <span data-ttu-id="69c34-178">프로젝트의 기존 구성 및 소스 코드 파일로의 변환</span><span class="sxs-lookup"><span data-stu-id="69c34-178">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="69c34-179">폴더 규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-179">The folder conventions are as follows:</span></span>

| <span data-ttu-id="69c34-180">폴더</span><span class="sxs-lookup"><span data-stu-id="69c34-180">Folder</span></span> | <span data-ttu-id="69c34-181">설명</span><span class="sxs-lookup"><span data-stu-id="69c34-181">Description</span></span> | <span data-ttu-id="69c34-182">패키지 설치 시의 작업</span><span class="sxs-lookup"><span data-stu-id="69c34-182">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="69c34-183">(루트)</span><span class="sxs-lookup"><span data-stu-id="69c34-183">(root)</span></span> | <span data-ttu-id="69c34-184">readme.txt에 대한 위치</span><span class="sxs-lookup"><span data-stu-id="69c34-184">Location for readme.txt</span></span> | <span data-ttu-id="69c34-185">패키지를 설치할 때 Visual Studio에서 패키지 루트에 readme.txt 파일을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-185">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="69c34-186">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="69c34-186">lib/{tfm}</span></span> | <span data-ttu-id="69c34-187">지정된 TFM(대상 프레임워크 모니커)에 대한 어셈블리(`.dll`), 문서(`.xml`) 및 기호(`.pdb`) 파일</span><span class="sxs-lookup"><span data-stu-id="69c34-187">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="69c34-188">어셈블리는 컴파일 및 런타임에 대한 참조로 추가됩니다. `.xml` 및 `.pdb`는 프로젝트 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-188">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="69c34-189">프레임워크 대상 특정의 하위 폴더를 만들려면 [여러 대상 프레임워크 지원](supporting-multiple-target-frameworks.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c34-189">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="69c34-190">ref/{tfm}</span><span class="sxs-lookup"><span data-stu-id="69c34-190">ref/{tfm}</span></span> | <span data-ttu-id="69c34-191">지정된 TFM(대상 프레임워크 모니커)에 대한 어셈블리(`.dll`) 및 기호(`.pdb`) 파일</span><span class="sxs-lookup"><span data-stu-id="69c34-191">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="69c34-192">어셈블리는 컴파일 시간에 대한 참조로만 추가됩니다. 따라서 프로젝트 bin 폴더에 아무것도 복사되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-192">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="69c34-193">runtimes</span><span class="sxs-lookup"><span data-stu-id="69c34-193">runtimes</span></span> | <span data-ttu-id="69c34-194">아키텍처 특정 어셈블리(`.dll`), 기호(`.pdb`) 및 네이티브 리소스(`.pri`) 파일</span><span class="sxs-lookup"><span data-stu-id="69c34-194">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="69c34-195">어셈블리는 런타임에 대한 참조로만 추가되고, 다른 파일은 프로젝트 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-195">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="69c34-196">해당 컴파일 시간 어셈블리를 제공하려면 항상 `/ref/{tfm}` 폴더 아래에 해당하는 (TFM) `AnyCPU` 특정 어셈블리가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-196">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="69c34-197">[여러 대상 프레임워크 지원](supporting-multiple-target-frameworks.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c34-197">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="69c34-198">콘텐츠</span><span class="sxs-lookup"><span data-stu-id="69c34-198">content</span></span> | <span data-ttu-id="69c34-199">임의 파일</span><span class="sxs-lookup"><span data-stu-id="69c34-199">Arbitrary files</span></span> | <span data-ttu-id="69c34-200">콘텐츠가 프로젝트 루트에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-200">Contents are copied to the project root.</span></span> <span data-ttu-id="69c34-201">**content** 폴더를 궁극적으로 패키지를 사용하는 대상 애플리케이션의 루트로 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-201">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="69c34-202">패키지에서 애플리케이션의 */images* 폴더에 이미지를 추가하도록 하려면 패키지의 *content/images* 폴더에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-202">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="69c34-203">build</span><span class="sxs-lookup"><span data-stu-id="69c34-203">build</span></span> | <span data-ttu-id="69c34-204">MSBuild `.targets` 및 `.props` 파일</span><span class="sxs-lookup"><span data-stu-id="69c34-204">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="69c34-205">프로젝트 파일 또는 `project.lock.json`(NuGet 3.x 이상)에 자동으로 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-205">Automatically inserted into the project file or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="69c34-206">도구</span><span class="sxs-lookup"><span data-stu-id="69c34-206">tools</span></span> | <span data-ttu-id="69c34-207">패키지 관리자 콘솔에서 액세스할 수 있는 Powershell 스크립트 및 프로그램</span><span class="sxs-lookup"><span data-stu-id="69c34-207">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="69c34-208">`tools` 폴더는 패키지 관리자 콘솔에 대한 `PATH` 환경 변수에만 추가 됩니다(특히 프로젝트를 빌드할 때는 MSBuild에 설정한 대로 `PATH`에 *추가되지 않음*).</span><span class="sxs-lookup"><span data-stu-id="69c34-208">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="69c34-209">폴더 구조에는 임의 개수의 대상 프레임워크에 대해 임의 개수의 어셈블리가 포함될 수 있으므로, 이 방법은 여러 프레임워크를 지원하는 패키지를 만들 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-209">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="69c34-210">어떤 경우이든 원하는 폴더 구조를 배치한 후에는 해당 폴더에서 다음 명령을 실행하여 `.nuspec` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-210">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="69c34-211">또 다시 말하지만, 생성된 `.nuspec`에는 폴더 구조의 파일에 대한 명시적 참조가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-211">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="69c34-212">NuGet은 패키지를 만들 때 자동으로 모든 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-212">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="69c34-213">그러나 매니페스트의 다른 부분에서 자리 표시자 값을 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-213">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="69c34-214">원본 : 어셈블리 DLL</span><span class="sxs-lookup"><span data-stu-id="69c34-214">From an assembly DLL</span></span>

<span data-ttu-id="69c34-215">어셈블리에서 패키지를 만드는 간단한 경우 다음 명령을 사용하여 어셈블리의 메타데이터에서 `.nuspec` 파일을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-215">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="69c34-216">이 형식을 사용하면 매니페스트의 몇 가지 자리 표시자를 어셈블리의 특정 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-216">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="69c34-217">예를 들어 `<id>` 속성은 어셈블리 이름으로 설정되고, `<version>`은 어셈블리 버전으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-217">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="69c34-218">그러나 매니페스트의 다른 속성은 어셈블리의 값과 일치하지 않으므로 여전히 자리 표시자를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-218">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="69c34-219">원본: Visual Studio 프로젝트</span><span class="sxs-lookup"><span data-stu-id="69c34-219">From a Visual Studio project</span></span>

<span data-ttu-id="69c34-220">`.csproj` 또는 `.vbproj` 파일에서 `.nuspec`을 만드는 것은 프로젝트에 설치된 다른 패키지가 자동으로 종속성으로 참조되기 때문에 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-220">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="69c34-221">프로젝트 파일과 동일한 폴더에서 다음 명령을 사용하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-221">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="69c34-222">결과 `<project-name>.nuspec` 파일에는 패키지 시간에 프로젝트의 값(이미 설치된 다른 패키지에 대한 참조 포함)으로 대체되는 *토큰*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-222">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="69c34-223">토큰은 프로젝트 속성의 양쪽에 `$` 기호로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-223">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="69c34-224">예를 들어 이 방식으로 생성된 매니페스트의 `<id>` 값은 일반적으로 다음과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-224">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="69c34-225">이 토큰은 패키지 시간에 프로젝트 파일의 `AssemblyName` 값으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-225">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="69c34-226">`.nuspec` 토큰에 대한 프로젝트 값의 정확한 매핑은 [대체 토큰 참조](../reference/nuspec.md#replacement-tokens)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c34-226">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="69c34-227">토큰을 사용하면 프로젝트를 업데이트할 때 `.nuspec`의 버전 번호와 같은 중요한 값을 업데이트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-227">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="69c34-228">(원하는 경우 언제든지 토큰을 리터럴 값으로 바꿀 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="69c34-228">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="69c34-229">뒤에 나오는 [nuget pack을 실행하여 .nupkg 파일 생성](#run-nuget-pack-to-generate-the-nupkg-file)에서 설명한 대로 Visual Studio 프로젝트에서 작업할 때 사용할 수 있는 몇 가지 추가 패키징 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-229">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#run-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="69c34-230">솔루션 수준 패키지</span><span class="sxs-lookup"><span data-stu-id="69c34-230">Solution-level packages</span></span>

<span data-ttu-id="69c34-231">*NuGet 2.x에만 해당, NuGet 3.0 이상에서는 사용할 수 없음*</span><span class="sxs-lookup"><span data-stu-id="69c34-231">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="69c34-232">NuGet 2.x는 패키지 관리자 콘솔(`tools` 폴더의 콘텐츠)용 도구 또는 추가 명령을 설치하는 솔루션 수준 패키지에 대한 개념을 지원하지만, 솔루션의 어떠한 프로젝트에도 참조, 콘텐츠 또는 빌드 사용자 지정을 추가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-232">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="69c34-233">이러한 패키지는 `lib`, `content` 또는 `build` 폴더에 파일을 직접 포함하지 않으며, 해당되는 어떤 종속성에도 해당 `lib`, `content` 또는 `build` 폴더의 파일이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-233">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="69c34-234">NuGet은 설치된 솔루션 수준 패키지를 프로젝트의 `packages.config` 파일이 아닌 `.nuget` 폴더의 `packages.config` 파일에서 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-234">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="69c34-235">기본값이 있는 새 파일</span><span class="sxs-lookup"><span data-stu-id="69c34-235">New file with default values</span></span>

<span data-ttu-id="69c34-236">다음 명령은 자리 표시자를 사용하여 기본 매니페스트를 만들므로 적절한 파일 구조로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-236">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="69c34-237">\<package-name\>을 생략하면 결과 파일은 `Package.nuspec`입니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-237">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="69c34-238">`Contoso.Utility.UsefulStuff`와 같은 이름을 제공하면 파일은 `Contoso.Utility.UsefulStuff.nuspec`입니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-238">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="69c34-239">결과 `.nuspec`에는 `projectUrl`과 같은 값에 대한 자리 표시자가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-239">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="69c34-240">파일을 사용하기 전에 편집하여 최종 `.nupkg` 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-240">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="69c34-241">고유한 패키지 식별자 선택 및 버전 번호 설정</span><span class="sxs-lookup"><span data-stu-id="69c34-241">Choose a unique package identifier and setting the version number</span></span>

<span data-ttu-id="69c34-242">패키지 식별자(`<id>` 요소)와 버전 번호(`<version>` 요소)는 패키지에 포함된 정확한 코드를 고유하게 식별하므로 매니페스트에서 가장 중요한 두 가지 값입니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-242">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="69c34-243">**패키지 식별자에 대한 모범 사례:**</span><span class="sxs-lookup"><span data-stu-id="69c34-243">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="69c34-244">**고유성**: 식별자는 nuget.org 또는 패키지를 호스팅하는 모든 갤러리에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-244">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="69c34-245">식별자를 결정하기 전에 해당 갤러리를 검색하여 해당 이름이 이미 사용 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-245">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="69c34-246">충돌을 방지하기 위한 좋은 패턴은 회사 이름을 식별자의 첫 번째 부분(예: `Contoso.`)으로 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-246">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="69c34-247">**네임스페이스 형식의 이름**: 하이픈 대신 점 표기법을 사용하여 .NET의 네임스페이스와 비슷한 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-247">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="69c34-248">예를 들어 `Contoso-Utility-UsefulStuff` 또는 `Contoso_Utility_UsefulStuff` 대신 `Contoso.Utility.UsefulStuff`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-248">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="69c34-249">패키지 식별자가 코드에 사용된 네임스페이스와 일치할 때 소비자가 이 형식의 이름이 유용하다는 것을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-249">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="69c34-250">**샘플 패키지**: 다른 패키지를 사용하는 방법을 보여 주는 샘플 코드 패키지를 생성하는 경우 `Contoso.Utility.UsefulStuff.Sample`(와)과 같이 `.Sample`을(를) 접미사로 식별자에 붙입니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-250">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="69c34-251">(물론 샘플 패키지에는 다른 패키지에 대한 종속성이 있습니다.) 샘플 패키지를 만드는 경우 앞에서 설명한 규칙 기반 작업 디렉터리 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-251">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="69c34-252">`content` 폴더에서 `\Samples\Contoso.Utility.UsefulStuff.Sample`과 같이 `\Samples\<identifier>`라는 폴더에 샘플 코드를 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-252">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="69c34-253">**패키지 버전에 대한 모범 사례:**</span><span class="sxs-lookup"><span data-stu-id="69c34-253">**Best practices for the package version:**</span></span>

- <span data-ttu-id="69c34-254">일반적으로 반드시 필요한 것은 아니지만 라이브러리의 버전과 일치하도록 패키지의 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-254">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="69c34-255">이는 앞서의 [패키지할 어셈블리 결정](#decide-which-assemblies-to-package)에서 설명한 대로 패키지를 단일 어셈블리로 제한할 때의 간단한 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-255">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#decide-which-assemblies-to-package).</span></span> <span data-ttu-id="69c34-256">전반적으로 NuGet 자체는 종속성을 확인할 때 어셈블리 버전이 아니라 패키지 버전을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-256">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="69c34-257">비표준 버전 구성표를 사용하는 경우 [패키지 버전 관리](../reference/package-versioning.md)에서 설명한 대로 NuGet 버전 관리 규칙을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-257">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="69c34-258">다음과 같은 일련의 간단한 블로그 게시물도 버전 관리를 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-258">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="69c34-259">1부: DLL 지옥에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="69c34-259">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="69c34-260">2부: 핵심 알고리즘</span><span class="sxs-lookup"><span data-stu-id="69c34-260">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="69c34-261">3부: 바인딩 리디렉션을 통한 통합</span><span class="sxs-lookup"><span data-stu-id="69c34-261">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a><span data-ttu-id="69c34-262">추가 정보 및 기타 파일 추가</span><span class="sxs-lookup"><span data-stu-id="69c34-262">Add a readme and other files</span></span>

<span data-ttu-id="69c34-263">패키지에 포함할 파일을 직접 지정 하려면 `.nuspec` 파일에서 `<metadata>` 태그 *다음에 오는* `<files>` 노드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-263">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> <span data-ttu-id="69c34-264">규칙 기반 작업 디렉터리 방식을 사용하는 경우 패키지 루트에 readme.txt를 배치하고, `content` 폴더에는 다른 콘텐츠를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-264">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="69c34-265">매니페스트에는 `<file>` 요소가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-265">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="69c34-266">패키지 루트에 `readme.txt`라는 파일이 포함되면 Visual Studio에서 패키지를 직접 설치한 직후 해당 파일의 내용을 일반 텍스트로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-266">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="69c34-267">종속성으로 설치된 패키지에는 추가 정보 파일이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-267">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="69c34-268">예를 들어 HtmlAgilityPack 패키지에 대한 추가 정보가 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-268">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![설치 시 NuGet 패키지에 대한 추가 정보 파일 표시](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="69c34-270">`.nuspec` 파일에서 빈 `<files>` 노드가 포함되면 NuGet은 `lib` 폴더에 있는 것 이외의 다른 콘텐츠를 패키지에 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-270">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="include-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="69c34-271">패키지에 MSBuild props 및 targets 포함</span><span class="sxs-lookup"><span data-stu-id="69c34-271">Include MSBuild props and targets in a package</span></span>

<span data-ttu-id="69c34-272">경우에 따라 패키지를 사용하는 프로젝트에 사용자 지정 빌드 대상 또는 속성(예: 빌드하는 동안 사용자 지정 도구 또는 프로세스 실행)을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-272">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="69c34-273">이렇게 하려면 프로젝트의 `\build` 폴더 내에 `<package_id>.targets` 또는 `<package_id>.props`(예: `Contoso.Utility.UsefulStuff.targets`) 형식의 파일을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-273">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="69c34-274">루트 `\build` 폴더의 파일은 모든 대상 프레임워크에 적합한 파일로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-274">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="69c34-275">프레임워크별 파일을 제공하려면 먼저 다음과 같이 적절한 하위 폴더 내에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-275">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="69c34-276">그런 다음 `.nuspec` 파일의 `<files>` 노드에서 이러한 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-276">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

<span data-ttu-id="69c34-277">패키지에 MSBuild props 및 targets 포함은 [NuGet 2.5부터 도입](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files)되었으므로 `minClientVersion="2.5"` 특성을 `metadata` 요소에 추가하여 패키지를 사용하는 데 필요한 최소 NuGet 클라이언트 버전을 나타내는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-277">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="69c34-278">NuGet에서 `\build` 파일이 포함된 패키지를 설치하는 경우 `.targets` 및 `.props` 파일을 가리키는 MSBuild `<Import>` 요소를 프로젝트 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-278">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="69c34-279">(`.props`는 프로젝트 파일의 위쪽에 추가되고, `.targets`는 아래쪽에 추가됩니다.) 각 대상 프레임워크에 대해 별도의 조건부 MSBuild `<Import>` 요소가 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-279">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="69c34-280">프레임워크 간 대상 지정을 위한 MSBuild `.props` 및 `.targets` 파일은 `\buildMultiTargeting` 폴더에 넣을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-280">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildMultiTargeting` folder.</span></span> <span data-ttu-id="69c34-281">패키지 설치 중 NuGet은 해당 `<Import>` 요소를 프로젝트 파일에 추가하고, 대상 프레임워크를 설정하지 않는다는 조건(MSBuild 속성 `$(TargetFramework)`가 비어 있어야 함)을 함께 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-281">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="69c34-282">NuGet 3.x를 사용하면 대상이 프로젝트에 추가되지 않고 대신 `project.lock.json`을 통해 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-282">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="69c34-283">nugkg pack을 실행하여 .nupkg 파일 생성</span><span class="sxs-lookup"><span data-stu-id="69c34-283">Run nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="69c34-284">어셈블리 또는 규칙 기반 작업 디렉터리를 사용하는 경우 `.nuspec` 파일이 포함된 `nuget pack`을 실행하고 `<project-name>`을 특정 파일 이름으로 바꿔 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-284">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="69c34-285">Visual Studio 프로젝트를 사용하는 경우 프로젝트 파일이 포함된 `nuget pack`을 실행하면 프로젝트 파일의 값을 사용하여 프로젝트의 `.nuspec` 파일을 자동으로 로드하고 그 안에 있는 모든 토큰을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-285">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="69c34-286">프로젝트가 토큰 값의 원본이므로 토큰 대체의 경우 프로젝트 파일을 직접 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-286">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="69c34-287">`.nuspec` 파일이 포함된 `nuget pack`을 사용하면 토큰 대체가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-287">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="69c34-288">모든 경우에 `nuget pack`은 마침표로 시작하는 폴더(예: `.git` 또는 `.hg`)를 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-288">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="69c34-289">NuGet은 매니페스트의 자리 표시자 값을 변경하지 않은 경우와 같이 수정이 필요한 오류가 `.nuspec` 파일에 있는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-289">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="69c34-290">`nuget pack`이 성공하면 [패키지 게시](../nuget-org/publish-a-package.md)에서 설명한 대로 적합한 갤러리에 게시할 수 있는 `.nupkg` 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-290">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="69c34-291">패키지를 만든 후 검사하는 유용한 방법은 [패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) 도구에서 해당 패키지를 여는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-291">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="69c34-292">이렇게 하면 패키지의 내용과 해당 매니페스트를 보여 주는 그래픽 뷰가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-292">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="69c34-293">또한 결과 `.nupkg` 파일의 이름을 `.zip` 파일로 바꾸고 그 내용을 직접 탐색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-293">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="69c34-294">추가 옵션</span><span class="sxs-lookup"><span data-stu-id="69c34-294">Additional options</span></span>

<span data-ttu-id="69c34-295">`nuget pack`에서 다양한 명령줄 스위치를 사용하여 파일을 제외하고, 매니페스트의 버전 번호를 재정의하고, 다른 기능 중에서 출력 폴더를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-295">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="69c34-296">전체 목록은 [pack 명령 참조](../tools/cli-ref-pack.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="69c34-296">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="69c34-297">다음은 Visual Studio 프로젝트에서 일반적으로 사용되는 몇 가지 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-297">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="69c34-298">**참조된 프로젝트**: 프로젝트에서 다른 프로젝트를 참조하는 경우 `-IncludeReferencedProjects` 옵션을 사용하여 참조된 프로젝트를 패키지의 일부로 또는 종속성으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-298">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="69c34-299">이 포함 프로세스는 재귀적이므로, `MyProject.csproj`에서 B와 C 프로젝트를 참조하고 해당 프로젝트에서 D, E 및 F를 참조하면, B, C, D, E 및 F의 파일이 패키지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-299">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="69c34-300">참조된 프로젝트에 자체의 `.nuspec` 파일이 포함되어 있으면 NuGet은 참조된 프로젝트를 종속성으로 대신 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-300">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="69c34-301">해당 프로젝트를 별도로 패키지하고 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-301">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="69c34-302">**빌드 구성**: 기본적으로 NuGet은 프로젝트 파일에 설정된 기본 빌드 구성(일반적으로 *Debug*)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-302">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="69c34-303">*Release*와 같은 다른 빌드 구성의 파일을 압축하려면 다음과 같이 구성에 `-properties` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-303">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="69c34-304">**기호**: 소비자가 디버거에서 패키지 코드를 단계별로 실행할 수 있게 하는 기호를 포함하려면 `-Symbols` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-304">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a><span data-ttu-id="69c34-305">패키지 설치 테스트</span><span class="sxs-lookup"><span data-stu-id="69c34-305">Test package installation</span></span>

<span data-ttu-id="69c34-306">일반적으로 패키지를 게시하기 전에 프로젝트에 패키지를 설치하는 프로세스를 테스트하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-306">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="69c34-307">테스트를 통해 모든 파일이 프로젝트의 올바른 위치에 있는지 반드시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-307">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="69c34-308">일반적인 [패키지 설치 단계](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)를 사용하여 Visual Studio 또는 명령줄에서 수동으로 설치를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-308">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

<span data-ttu-id="69c34-309">자동 테스트의 경우 기본 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-309">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="69c34-310">`.nupkg` 파일을 로컬 폴더에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-310">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="69c34-311">`nuget sources add -name <name> -source <path>` 명령([nuget sources](../tools/cli-ref-sources.md) 참조)을 사용하여 패키지 원본에 폴더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-311">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="69c34-312">지정된 컴퓨터에서 이 로컬 원본을 한 번만 설정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-312">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="69c34-313">`nuget install <packageID> -source <name>`을 사용하여 해당 원본에서 패키지를 설치합니다. 여기서 `<name>`은 `nuget sources`에 지정된 원본 이름과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-313">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="69c34-314">원본을 지정하면 해당 원본에서만 패키지가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-314">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="69c34-315">파일 시스템을 검사하여 파일이 올바르게 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-315">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69c34-316">다음 단계</span><span class="sxs-lookup"><span data-stu-id="69c34-316">Next Steps</span></span>

<span data-ttu-id="69c34-317">패키지(`.nupkg` 파일)를 만들었으면 [패키지 게시](../nuget-org/publish-a-package.md)에서 설명한 대로 원하는 갤러리에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-317">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="69c34-318">다음 항목에서 설명한 대로 패키지의 기능을 확장하거나 그렇지 않고 다른 시나리오를 지원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-318">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="69c34-319">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="69c34-319">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="69c34-320">여러 대상 프레임워크 지원</span><span class="sxs-lookup"><span data-stu-id="69c34-320">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="69c34-321">원본 및 구성 파일 변환</span><span class="sxs-lookup"><span data-stu-id="69c34-321">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="69c34-322">지역화</span><span class="sxs-lookup"><span data-stu-id="69c34-322">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="69c34-323">시험판 버전</span><span class="sxs-lookup"><span data-stu-id="69c34-323">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="69c34-324">패키지 형식 설정</span><span class="sxs-lookup"><span data-stu-id="69c34-324">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="69c34-325">COM interop 어셈블리가 포함된 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="69c34-325">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="69c34-326">마지막으로 주의해야 할 추가 패키지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="69c34-326">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="69c34-327">네이티브 패키지</span><span class="sxs-lookup"><span data-stu-id="69c34-327">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="69c34-328">기호 패키지</span><span class="sxs-lookup"><span data-stu-id="69c34-328">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
