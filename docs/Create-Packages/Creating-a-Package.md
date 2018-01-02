---
title: "NuGet 패키지를 만드는 방법 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 456797cb-e3e4-4b88-9b01-8b5153cee802
description: "파일 및 버전 관리와 같은 주요 결정 사항을 포함하여 NuGet 패키지를 디자인하고 만드는 과정을 자세히 안내합니다."
keywords: "NuGet 패키지 만들기, 패키지 만들기, nuspec 매니페스트, NuGet 패키지 규칙, NuGet 패키지 버전"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e7a2c4d02afb2387161c22fe5bd443eb0991ea8c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="3d463-104">NuGet 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="3d463-104">Creating NuGet packages</span></span>

<span data-ttu-id="3d463-105">패키지의 기능 또는 포함된 코드에 관계없이 `nuget.exe`를 사용하여 해당 기능을 임의 수의 다른 개발자와 공유하고 사용할 수 있는 구성 요소로 패키지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-105">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="3d463-106">`nuget.exe`를 설치하려면 [NuGet CLI 설치](../guides/Install-NuGet.md#nuget-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d463-106">To install `nuget.exe`, see [Install NuGet CLI](../guides/Install-NuGet.md#nuget-cli).</span></span> <span data-ttu-id="3d463-107">Visual Studio에는 `nuget.exe`가 자동으로 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-107">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="3d463-108">엄밀히 말해, NuGet 패키지는 `.nupkg` 확장명으로 이름이 변경되고 내용이 특정 규칙과 일치하는 ZIP 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-108">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="3d463-109">규칙을 충족하는 패키지를 만드는 자세한 프로세스에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-109">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="3d463-110">집중적인 연습에 대해서는 [패키지 만들기 및 게시 빠른 시작](../quickstart/create-and-publish-a-package.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d463-110">For a focused walkthrough, refer to [Create and Publish a Package Quickstart](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="3d463-111">패키징은 패키지로 전달하려는 컴파일된 코드(어셈블리), 기호 및/또는 기타 파일로 시작됩니다([개요 및 워크플로](Overview-and-Workflow.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="3d463-111">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](Overview-and-Workflow.md)).</span></span> <span data-ttu-id="3d463-112">이 프로세스는 프로젝트 파일의 정보에서 끌어오기를 사용하여 컴파일된 어셈블리 및 패키지를 동기화된 상태로 유지할 수 있지만, 패키지에 포함된 파일을 컴파일하거나 생성하는 프로세스와는 관련이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-112">This process is independent from compiling or otherwise generating the files that go into the package, although you can use draw from information in a project file to keep the compiled assemblines and packages in sync.</span></span>

<span data-ttu-id="3d463-113">항목 내용:</span><span class="sxs-lookup"><span data-stu-id="3d463-113">In this topic:</span></span>

- [<span data-ttu-id="3d463-114">패키지할 어셈블리 결정</span><span class="sxs-lookup"><span data-stu-id="3d463-114">Deciding which assemblies to package</span></span>](#deciding-which-assemblies-to-package)
- [<span data-ttu-id="3d463-115">`.nuspec` 파일의 역할 및 구조</span><span class="sxs-lookup"><span data-stu-id="3d463-115">The role and structure of the `.nuspec` file</span></span>](#the-role-and-structure-of-the-nuspec-file)
- <span data-ttu-id="3d463-116">[`.nuspec` 파일 만들기](#creating-the-nuspec-file) - 원본은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-116">[Creating the `.nuspec` file](#creating-the-nuspec-file) from:</span></span>
    - [<span data-ttu-id="3d463-117">규칙 기반 작업 디렉터리</span><span class="sxs-lookup"><span data-stu-id="3d463-117">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
    - [<span data-ttu-id="3d463-118">어셈블리 DLL</span><span class="sxs-lookup"><span data-stu-id="3d463-118">An assembly DLL</span></span>](#from-an-assembly-dll)
    - [<span data-ttu-id="3d463-119">Visual Studio 프로젝트</span><span class="sxs-lookup"><span data-stu-id="3d463-119">A Visual Studio project</span></span>](#from-a-visual-studio-project)
    - [<span data-ttu-id="3d463-120">기본값이 있는 새 파일</span><span class="sxs-lookup"><span data-stu-id="3d463-120">New file with default values</span></span>](#new-file-with-default-values)    
- [<span data-ttu-id="3d463-121">고유한 패키지 식별자 선택 및 버전 번호 설정</span><span class="sxs-lookup"><span data-stu-id="3d463-121">Choosing a unique package identifier and setting the version number</span></span>](#choosing-a-unique-package-identifier-and-setting-the-version-number)
- <span data-ttu-id="3d463-122">[패키지 유형 설정](#setting-a-package-type)(NuGet 3.5 이상)</span><span class="sxs-lookup"><span data-stu-id="3d463-122">[Setting a package type](#setting-a-package-type) (NuGet 3.5 and later)</span></span>
- [<span data-ttu-id="3d463-123">추가 정보 및 기타 파일 추가</span><span class="sxs-lookup"><span data-stu-id="3d463-123">Adding a readme and other files</span></span>](#adding-a-readme-and-other-files)
- [<span data-ttu-id="3d463-124">패키지에 MSBuild props 및 targets 포함</span><span class="sxs-lookup"><span data-stu-id="3d463-124">Including MSBuild props and targets in a package</span></span>](#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="3d463-125">COM interop 어셈블리가 포함된 패키지 제작</span><span class="sxs-lookup"><span data-stu-id="3d463-125">Authoring packages that contain COM interop assemblies</span></span>](#authoring-packages-with-com-interop-assemblies)
- [<span data-ttu-id="3d463-126">nugkg pack을 실행하여 .nupkg 파일 생성</span><span class="sxs-lookup"><span data-stu-id="3d463-126">Running nuget pack to generate the .nupkg file</span></span>](#running-nuget-pack-to-generate-the-nupkg-file)

<span data-ttu-id="3d463-127">이러한 핵심 단계가 완료되면 이 설명서의 다른 부분에서 설명한 대로 다양한 다른 기능을 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-127">After these core steps, you can incorporate a variety of other features as described elsewhere in this documentation.</span></span> <span data-ttu-id="3d463-128">아래의 [다음 단계](#next-steps)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d463-128">See [Next steps](#next-steps) below.</span></span>

> [!Note]
> <span data-ttu-id="3d463-129">이 항목은 Visual Studio 2017 및 NuGet 4.0 이상을 사용하는 .NET Core 프로젝트 이외의 프로젝트 형식에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-129">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="3d463-130">이러한 .NET Core 프로젝트에서 NuGet은 `.csproj` 파일의 정보를 직접 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-130">In those .NET Core projects, NuGet uses information in the `.csproj` file directly.</span></span> <span data-ttu-id="3d463-131">자세한 내용은 [Visual Studio 2017을 사용하여 .NET Standard 패키지 만들기](../guides/create-net-standard-packages-vs2017.md) 및 [MSBuild 대상으로서의 NuGet pack 및 restore](../schema/msbuild-targets.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d463-131">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="3d463-132">패키지할 어셈블리 결정</span><span class="sxs-lookup"><span data-stu-id="3d463-132">Deciding which assemblies to package</span></span>

<span data-ttu-id="3d463-133">가장 일반적인 용도의 패키지에는 다른 개발자가 자신의 프로젝트에서 사용할 수 있는 하나 이상의 어셈블리가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-133">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="3d463-134">일반적으로 각 어셈블리가 독립적으로 유용한 경우 NuGet 패키지당 하나의 어셈블리가 있는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-134">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="3d463-135">예를 들어 `Parser.dll`에 종속된 `Utilities.dll`이 있고 `Parser.dll`이 자체적으로 유용할 경우 각각에 대해 하나의 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-135">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="3d463-136">이렇게 하면 개발자가 `Utilities.dll`과는 독립적으로 `Parser.dll`을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-136">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="3d463-137">라이브러리가 독립적으로 유용하지 않은 여러 어셈블리로 구성된 경우 이를 하나의 패키지로 결합하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-137">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="3d463-138">앞의 예제를 사용하여 `Utilities.dll`에서만 사용되는 코드가 `Parser.dll`에 포함된 경우 동일한 패키지에 `Parser.dll`을 유지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-138">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>
    - <span data-ttu-id="3d463-139">마찬가지로, `Utilities.dll`이 `Utilities.resources.dll`에 종속되고 후자가 자체적으로 유용하지 않은 경우 두 라이브러리를 모두 동일한 패키지에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-139">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="3d463-140">실제로 리소스는 특별한 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-140">Resources are, in fact, a special case.</span></span> <span data-ttu-id="3d463-141">패키지가 프로젝트에 설치되면 어셈블리 참조가 지역화된 위성 어셈블리로 간주되므로 NuGet은 `.resources.dll`이라는 DLL을 *제외한* 패키지의 DLL에 해당 어셈블리 참조를 자동으로 추가합니다([지역화된 패키지 만들기](creating-localized-packages.md) 참조).</span><span class="sxs-lookup"><span data-stu-id="3d463-141">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="3d463-142">이러한 이유로 다른 경우에 필수 패키지 코드가 포함되는 파일에는 `.resources.dll`을 사용하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="3d463-142">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="3d463-143">라이브러리에 COM interop 어셈블리가 포함되어 있으면 [COM interop 어셈블리가 포함된 패키지 제작](#authoring-packages-with-com-interop-assemblies)의 지침을 추가로 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="3d463-143">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="3d463-144">.nuspec 파일의 역할 및 구조</span><span class="sxs-lookup"><span data-stu-id="3d463-144">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="3d463-145">패키지하려는 파일을 알고 있으면 다음 단계는 `.nuspec` XML 파일에 패키지 매니페스트를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-145">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="3d463-146">매니페스트:</span><span class="sxs-lookup"><span data-stu-id="3d463-146">The manifest:</span></span>

1. <span data-ttu-id="3d463-147">패키지의 내용을 설명하며 패키지에 직접 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-147">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="3d463-148">패키지를 만들도록 구동하고 프로젝트에 해당 패키지를 설치하는 방법을 NuGet에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-148">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="3d463-149">예를 들어 매니페스트는 다른 패키지 종속성을 식별하여 NuGet에서 기본 패키지를 설치할 때 해당 종속성을 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-149">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="3d463-150">아래에서 설명한 대로 필수 및 선택적 속성을 모두 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-150">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="3d463-151">여기서 언급하지 않은 다른 속성을 포함하여 정확한 세부 정보는 [.nuspec 참조](../schema/nuspec.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d463-151">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../schema/nuspec.md).</span></span>

<span data-ttu-id="3d463-152">필수 속성:</span><span class="sxs-lookup"><span data-stu-id="3d463-152">Required properties:</span></span>

- <span data-ttu-id="3d463-153">패키지를 호스팅하는 갤러리에서 고유해야 하는 패키지 식별자</span><span class="sxs-lookup"><span data-stu-id="3d463-153">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="3d463-154">*Major.Minor.Patch[-Suffix]* 형식의 특정 버전 번호(여기서 *-Suffix*는 [시험판 버전](Prerelease-Packages.md)을 식별함)</span><span class="sxs-lookup"><span data-stu-id="3d463-154">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](Prerelease-Packages.md)</span></span>
- <span data-ttu-id="3d463-155">호스트에 표시되어야 하는 패키지 제목(예: nuget.org)</span><span class="sxs-lookup"><span data-stu-id="3d463-155">The package title as it should appears on the host (like nuget.org)</span></span>
- <span data-ttu-id="3d463-156">작성자 및 소유자 정보</span><span class="sxs-lookup"><span data-stu-id="3d463-156">Author and owner information.</span></span>
- <span data-ttu-id="3d463-157">패키지에 대한 자세한 설명</span><span class="sxs-lookup"><span data-stu-id="3d463-157">A long description of the package.</span></span>

<span data-ttu-id="3d463-158">선택적 일반 속성:</span><span class="sxs-lookup"><span data-stu-id="3d463-158">Common optional properties:</span></span>

- <span data-ttu-id="3d463-159">릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="3d463-159">Release notes</span></span>
- <span data-ttu-id="3d463-160">저작권 정보</span><span class="sxs-lookup"><span data-stu-id="3d463-160">Copyright information</span></span>
- <span data-ttu-id="3d463-161">[Visual Studio의 패키지 관리자 UI](../Tools/Package-Manager-UI.md)에 대한 간단한 설명</span><span class="sxs-lookup"><span data-stu-id="3d463-161">A short description for the [Package Manager UI in Visual Studio](../Tools/Package-Manager-UI.md)</span></span>
- <span data-ttu-id="3d463-162">로캘 ID</span><span class="sxs-lookup"><span data-stu-id="3d463-162">A locale ID</span></span>
- <span data-ttu-id="3d463-163">홈 페이지 및 라이선스 URL</span><span class="sxs-lookup"><span data-stu-id="3d463-163">Home page and license URLs</span></span>
- <span data-ttu-id="3d463-164">아이콘 URL</span><span class="sxs-lookup"><span data-stu-id="3d463-164">An icon URL</span></span>
- <span data-ttu-id="3d463-165">종속성 및 참조 목록</span><span class="sxs-lookup"><span data-stu-id="3d463-165">Lists of dependencies and references</span></span>
- <span data-ttu-id="3d463-166">갤러리 검색을 지원하는 태그</span><span class="sxs-lookup"><span data-stu-id="3d463-166">Tags that assist in gallery searches</span></span>

<span data-ttu-id="3d463-167">다음은 속성을 설명하는 주석이 포함된 가상의 일반적인 `.nuspec` 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-167">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

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

    <!-- Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  -->
    <owners>dejanatc, rjdey</owners>

    <!-- License and project URLs provide links for the gallery -->
    <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
    <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

    <!-- The icon is used in Visual Studio's package manager UI -->
    <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

    <!-- If true, this value prompts the user to accept the license when
            installing the package. -->
    <requireLicenseAcceptance>false</requireLicenseAcceptance>

    <!-- Any details about this particular release -->
    <releaseNotes>Bug fixes and performance improvements</releaseNotes>

    <!-- The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. -->
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

<span data-ttu-id="3d463-168">종속성 선언 및 버전 번호 지정에 대한 자세한 내용은 [패키지 버전 관리](../reference/package-versioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d463-168">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="3d463-169">`dependency` 요소의 `include` 및 `exclude` 특성을 사용하여 패키지에 종속성의 자산을 직접 공개할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-169">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="3d463-170">[.nuspec 참조 - 종속성](../Schema/nuspec.md#dependencies)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d463-170">See [.nuspec Reference - Dependencies](../Schema/nuspec.md#dependencies).</span></span>

<span data-ttu-id="3d463-171">매니페스트는 이 매니페스트에서 만든 패키지에 포함되어 있으므로 기존 패키지를 검사하여 임의 개수의 추가 예제를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-171">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="3d463-172">좋은 원본은 컴퓨터에 있는 전역 패키지 캐시이며, 해당 위치는 다음 명령으로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-172">A good source is the global package cache on your machine, the location of which is returned by the following command:</span></span>

```
nuget locals -list global-packages
```

<span data-ttu-id="3d463-173">*package\version* 폴더로 이동하여 `.nupkg` 파일을 `.zip` 파일에 복사한 다음, 해당 `.zip` 파일을 열고 그 안에 있는 `.nuspec` 파일을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-173">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="3d463-174">Visual Studio 프로젝트에서 `.nuspec`을 만드는 경우 패키지를 빌드할 때 프로젝트의 정보로 대체되는 토큰이 매니페스트에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-174">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are be replaced with information from the project when the package is built.</span></span> <span data-ttu-id="3d463-175">[Visual Studio 프로젝트에서 .nuspec 만들기](#from-a-visual-studio-project)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d463-175">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="3d463-176">.nuspec 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="3d463-176">Creating the .nuspec file</span></span>

<span data-ttu-id="3d463-177">완전한 매니페스트를 만드는 것은 일반적으로 다음 방법 중 하나를 통해 생성된 기본 `.nuspec` 파일로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-177">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="3d463-178">규칙 기반 작업 디렉터리</span><span class="sxs-lookup"><span data-stu-id="3d463-178">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="3d463-179">어셈블리 DLL</span><span class="sxs-lookup"><span data-stu-id="3d463-179">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="3d463-180">Visual Studio 프로젝트</span><span class="sxs-lookup"><span data-stu-id="3d463-180">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="3d463-181">기본값이 있는 새 파일</span><span class="sxs-lookup"><span data-stu-id="3d463-181">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="3d463-182">그런 다음 최종 패키지에 원하는 정확한 내용을 설명하도록 파일을 직접 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-182">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="3d463-183">생성된 `.nuspec` 파일에는 `nuget pack` 명령을 사용하여 패키지를 만들기 전에 수정해야 하는 자리 표시자가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-183">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="3d463-184">`.nuspec`에 자리 표시자가 있으면 이 명령이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-184">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="3d463-185">원본: 규칙 기반 작업 디렉터리</span><span class="sxs-lookup"><span data-stu-id="3d463-185">From a convention-based working directory</span></span>

<span data-ttu-id="3d463-186">NuGet 패키지는 `.nupkg` 확장명으로 이름이 바뀐 ZIP 파일일 뿐이므로 파일 시스템에서 원하는 폴더 구조를 만드는 것이 가장 쉽습니다. 이 경우 해당 구조에서 `.nuspec` 파일을 직접 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-186">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, its often easiest to create the folder structure you want on the file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="3d463-187">그런 다음 `nuget pack` 명령은 해당 폴더 구조의 모든 파일을 자동으로 추가합니다(동일한 구조의 개인 파일을 유지할 수 있도록 `.`으로 시작하는 폴더는 제외함).</span><span class="sxs-lookup"><span data-stu-id="3d463-187">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you keep private files in the same structure).</span></span>

<span data-ttu-id="3d463-188">이 방식의 장점은 이 항목의 뒷부분에서 설명한 대로 패키지에 포함하려는 파일을 매니페스트에 지정할 필요가 없다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-188">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="3d463-189">빌드 프로세스에서 패키지로 이동하는 정확한 폴더 구조를 생성하기만 하면 되고, 그렇지 않은 경우 프로젝트의 일부가 아닌 다른 파일을 쉽게 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-189">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="3d463-190">대상 프로젝트에 삽입해야 하는 콘텐츠 및 소스 코드</span><span class="sxs-lookup"><span data-stu-id="3d463-190">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="3d463-191">PowerShell 스크립트(NuGet 2.x에서 사용되는 패키지에는 NuGet 3.x 이상에서 지원되지 않는 설치 스크립트도 포함될 수 있음).</span><span class="sxs-lookup"><span data-stu-id="3d463-191">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="3d463-192">프로젝트의 기존 구성 및 소스 코드 파일로의 변환</span><span class="sxs-lookup"><span data-stu-id="3d463-192">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="3d463-193">폴더 규칙은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-193">The folder conventions are as follows:</span></span>

| <span data-ttu-id="3d463-194">폴더</span><span class="sxs-lookup"><span data-stu-id="3d463-194">Folder</span></span> | <span data-ttu-id="3d463-195">설명</span><span class="sxs-lookup"><span data-stu-id="3d463-195">Description</span></span> | <span data-ttu-id="3d463-196">패키지 설치 시의 작업</span><span class="sxs-lookup"><span data-stu-id="3d463-196">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3d463-197">(루트)</span><span class="sxs-lookup"><span data-stu-id="3d463-197">(root)</span></span> | <span data-ttu-id="3d463-198">readme.txt에 대한 위치</span><span class="sxs-lookup"><span data-stu-id="3d463-198">Location for readme.txt</span></span> | <span data-ttu-id="3d463-199">패키지를 설치할 때 Visual Studio에서 패키지 루트에 readme.txt 파일을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-199">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="3d463-200">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="3d463-200">lib/{tfm}</span></span> | <span data-ttu-id="3d463-201">지정된 TFM(대상 프레임워크 모니커)에 대한 어셈블리(`.dll`), 문서(`.xml`) 및 기호(`.pdb`) 파일</span><span class="sxs-lookup"><span data-stu-id="3d463-201">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="3d463-202">어셈블리는 참조로 추가되고, `.xml` 및 `.pdb`는 프로젝트 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-202">Assemblies are added as references; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="3d463-203">프레임워크 대상 특정의 하위 폴더를 만들려면 [여러 대상 프레임워크 지원](Supporting-Multiple-Target-Frameworks.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d463-203">See [Supporting multiple target frameworks](Supporting-Multiple-Target-Frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="3d463-204">runtimes</span><span class="sxs-lookup"><span data-stu-id="3d463-204">runtimes</span></span> | <span data-ttu-id="3d463-205">아키텍처 특정 어셈블리(`.dll`), 기호(`.pdb`) 및 네이티브 리소스(`.pri`) 파일</span><span class="sxs-lookup"><span data-stu-id="3d463-205">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="3d463-206">어셈블리는 참조로 추가되고, 다른 파일은 프로젝트 폴더에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-206">Assemblies are added as references; other files are copied into project folders.</span></span> <span data-ttu-id="3d463-207">[여러 대상 프레임워크 지원](Supporting-Multiple-Target-Frameworks.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d463-207">See [Supporting multiple target frameworks](Supporting-Multiple-Target-Frameworks.md).</span></span> |
| <span data-ttu-id="3d463-208">내용</span><span class="sxs-lookup"><span data-stu-id="3d463-208">content</span></span> | <span data-ttu-id="3d463-209">임의 파일</span><span class="sxs-lookup"><span data-stu-id="3d463-209">Arbitrary files</span></span> | <span data-ttu-id="3d463-210">콘텐츠가 프로젝트 루트에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-210">Contents are copied to the project root.</span></span> <span data-ttu-id="3d463-211">**content** 폴더를 궁극적으로 패키지를 사용하는 대상 응용 프로그램의 루트로 간주합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-211">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="3d463-212">패키지에서 응용 프로그램의 */images* 폴더에 이미지를 추가하도록 하려면 패키지의 *content/images* 폴더에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-212">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="3d463-213">빌드</span><span class="sxs-lookup"><span data-stu-id="3d463-213">build</span></span> | <span data-ttu-id="3d463-214">MSBuild `.targets` 및 `.props` 파일</span><span class="sxs-lookup"><span data-stu-id="3d463-214">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="3d463-215">프로젝트 파일(NuGet 2.x) 또는 `project.lock.json`(NuGet 3.x 이상)에 자동으로 삽입됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-215">Automatically inserted into the project file (NuGet 2.x) or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="3d463-216">도구</span><span class="sxs-lookup"><span data-stu-id="3d463-216">tools</span></span> | <span data-ttu-id="3d463-217">패키지 관리자 콘솔에서 액세스할 수 있는 Powershell 스크립트 및 프로그램</span><span class="sxs-lookup"><span data-stu-id="3d463-217">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="3d463-218">`tools` 폴더는 패키지 관리자 콘솔에 대한 `PATH` 환경 변수에만 추가 됩니다(특히 프로젝트를 빌드할 때는 MSBuild에 설정한 대로 `PATH`에 *추가되지 않음*).</span><span class="sxs-lookup"><span data-stu-id="3d463-218">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="3d463-219">폴더 구조에는 임의 개수의 대상 프레임워크에 대해 임의 개수의 어셈블리가 포함될 수 있으므로, 이 방법은 여러 프레임워크를 지원하는 패키지를 만들 때 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-219">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks</span></span> 

<span data-ttu-id="3d463-220">어떤 경우이든 원하는 폴더 구조를 배치한 후에는 해당 폴더에서 다음 명령을 실행하여 `.nuspec` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-220">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```
nuget spec
```

<span data-ttu-id="3d463-221">또 다시 말하지만, 생성된 `.nuspec`에는 폴더 구조의 파일에 대한 명시적 참조가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-221">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="3d463-222">NuGet은 패키지를 만들 때 자동으로 모든 파일을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-222">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="3d463-223">그러나 매니페스트의 다른 부분에서 자리 표시자 값을 편집해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-223">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="3d463-224">원본 : 어셈블리 DLL</span><span class="sxs-lookup"><span data-stu-id="3d463-224">From an assembly DLL</span></span>

<span data-ttu-id="3d463-225">어셈블리에서 패키지를 만드는 간단한 경우 다음 명령을 사용하여 어셈블리의 메타데이터에서 `.nuspec` 파일을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-225">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```
nuget spec <assembly-name>.dll
```

<span data-ttu-id="3d463-226">이 형식을 사용하면 매니페스트의 몇 가지 자리 표시자를 어셈블리의 특정 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-226">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="3d463-227">예를 들어 `<id>` 속성은 어셈블리 이름으로 설정되고, `<version>`은 어셈블리 버전으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-227">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="3d463-228">그러나 매니페스트의 다른 속성은 어셈블리의 값과 일치하지 않으므로 여전히 자리 표시자를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-228">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="3d463-229">원본: Visual Studio 프로젝트</span><span class="sxs-lookup"><span data-stu-id="3d463-229">From a Visual Studio project</span></span>

<span data-ttu-id="3d463-230">`.csproj` 또는 `.vbproj` 파일에서 `.nuspec`을 만드는 것은 프로젝트에 설치된 다른 패키지가 자동으로 종속성으로 참조되기 때문에 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-230">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="3d463-231">프로젝트 파일과 동일한 폴더에서 다음 명령을 사용하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-231">Simply use the following command in the same folder as the project file:</span></span>

```
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="3d463-232">결과 `<project-name>.nuspec` 파일에는 패키지 시간에 프로젝트의 값(이미 설치된 다른 패키지에 대한 참조 포함)으로 대체되는 *토큰*이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-232">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="3d463-233">토큰은 프로젝트 속성의 양쪽에 `$` 기호로 구분됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-233">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="3d463-234">예를 들어 이 방식으로 생성된 매니페스트의 `<id>` 값은 일반적으로 다음과 같이 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-234">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="3d463-235">이 토큰은 패키지 시간에 프로젝트 파일의 `AssemblyName` 값으로 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-235">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="3d463-236">`.nuspec` 토큰에 대한 프로젝트 값의 정확한 매핑은 [대체 토큰 참조](../schema/nuspec.md#replacement-tokens)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d463-236">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../schema/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="3d463-237">토큰을 사용하면 프로젝트를 업데이트할 때 `.nuspec`의 버전 번호와 같은 중요한 값을 업데이트할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-237">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="3d463-238">(원하는 경우 언제든지 토큰을 리터럴 값으로 바꿀 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="3d463-238">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="3d463-239">뒤에 나오는 [nuget pack을 실행하여 .nupkg 파일 생성](#running-nuget-pack-to-generate-the-nupkg-file)에서 설명한 대로 Visual Studio 프로젝트에서 작업할 때 사용할 수 있는 몇 가지 추가 패키징 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-239">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="3d463-240">솔루션 수준 패키지</span><span class="sxs-lookup"><span data-stu-id="3d463-240">Solution-level packages</span></span>

<span data-ttu-id="3d463-241">*NuGet 2.x에만 해당, NuGet 3.0 이상에서는 사용할 수 없음*</span><span class="sxs-lookup"><span data-stu-id="3d463-241">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="3d463-242">NuGet 2.x는 패키지 관리자 콘솔(`tools` 폴더의 콘텐츠)용 도구 또는 추가 명령을 설치하는 솔루션 수준 패키지에 대한 개념을 지원하지만, 솔루션의 어떠한 프로젝트에도 참조, 콘텐츠 또는 빌드 사용자 지정을 추가하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-242">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="3d463-243">이러한 패키지는 `lib`, `content` 또는 `build` 폴더에 파일을 직접 포함하지 않으며, 해당되는 어떤 종속성에도 해당 `lib`, `content` 또는 `build` 폴더의 파일이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-243">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span> 

<span data-ttu-id="3d463-244">NuGet은 설치된 솔루션 수준 패키지를 프로젝트의 `packages.config` 파일이 아닌 `.nuget` 폴더의 `packages.config` 파일에서 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-244">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="3d463-245">기본값이 있는 새 파일</span><span class="sxs-lookup"><span data-stu-id="3d463-245">New file with default values</span></span>

<span data-ttu-id="3d463-246">다음 명령은 자리 표시자를 사용하여 기본 매니페스트를 만들므로 적절한 파일 구조로 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-246">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```
nuget spec [<package-name>]
```

<span data-ttu-id="3d463-247">\<package-name\>을 생략하면 결과 파일은 `Package.nuspec`입니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-247">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="3d463-248">`Contoso.Utility.UsefulStuff`와 같은 이름을 제공하면 파일은 `Contoso.Utility.UsefulStuff.nuspec`입니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-248">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="3d463-249">결과 `.nuspec`에는 `projectUrl`과 같은 값에 대한 자리 표시자가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-249">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="3d463-250">파일을 사용하기 전에 편집하여 최종 `.nupkg` 파일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-250">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="3d463-251">고유한 패키지 식별자 선택 및 버전 번호 설정</span><span class="sxs-lookup"><span data-stu-id="3d463-251">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="3d463-252">패키지 식별자(`<id>` 요소)와 버전 번호(`<version>` 요소)는 패키지에 포함된 정확한 코드를 고유하게 식별하므로 매니페스트에서 가장 중요한 두 가지 값입니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-252">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="3d463-253">**패키지 식별자에 대한 모범 사례:**</span><span class="sxs-lookup"><span data-stu-id="3d463-253">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="3d463-254">**고유성**: 식별자는 nuget.org 또는 패키지를 호스팅하는 모든 갤러리에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-254">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="3d463-255">식별자를 결정하기 전에 해당 갤러리를 검색하여 해당 이름이 이미 사용 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-255">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="3d463-256">충돌을 방지하기 위한 좋은 패턴은 회사 이름을 식별자의 첫 번째 부분(예: `Contoso.`)으로 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-256">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="3d463-257">**네임스페이스 형식의 이름**: 하이픈 대신 점 표기법을 사용하여 .NET의 네임스페이스와 비슷한 패턴을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-257">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="3d463-258">예를 들어 `Contoso-Utility-UsefulStuff` 또는 `Contoso_Utility_UsefulStuff` 대신 `Contoso.Utility.UsefulStuff`를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-258">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="3d463-259">패키지 식별자가 코드에 사용된 네임스페이스와 일치할 때 소비자가 이 형식의 이름이 유용하다는 것을 알게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-259">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="3d463-260">**샘플 패키지**: 다른 패키지를 사용하는 방법을 보여 주는 샘플 코드 패키지를 생성하는 경우 `Contoso.Utility.UsefulStuff.Sample`과 같이 `.Sample`을 접미사로 식별자에 붙입니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-260">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="3d463-261">(물론 샘플 패키지에는 다른 패키지에 대한 종속성이 있습니다.) 샘플 패키지를 만드는 경우 앞에서 설명한 규칙 기반 작업 디렉터리 방법을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-261">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="3d463-262">`content` 폴더에서 `\Samples\Contoso.Utility.UsefulStuff.Sample`과 같이 `\Samples\<identifier>`라는 폴더에 샘플 코드를 정렬합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-262">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="3d463-263">**패키지 버전에 대한 모범 사례:**</span><span class="sxs-lookup"><span data-stu-id="3d463-263">**Best practices for the package version:**</span></span>

- <span data-ttu-id="3d463-264">일반적으로 반드시 필요한 것은 아니지만 라이브러리의 버전과 일치하도록 패키지의 버전을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-264">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="3d463-265">이는 앞서의 [패키지할 어셈블리 결정](#deciding-which-assemblies-to-package)에서 설명한 대로 패키지를 단일 어셈블리로 제한할 때의 간단한 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-265">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="3d463-266">전반적으로 NuGet 자체는 종속성을 확인할 때 어셈블리 버전이 아니라 패키지 버전을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-266">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="3d463-267">비표준 버전 구성표를 사용하는 경우 [패키지 버전 관리](../reference/package-versioning.md)에서 설명한 대로 NuGet 버전 관리 규칙을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-267">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="3d463-268">다음과 같은 일련의 간단한 블로그 게시물도 버전 관리를 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-268">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - [<span data-ttu-id="3d463-269">1부: DLL 지옥에서 가져오기</span><span class="sxs-lookup"><span data-stu-id="3d463-269">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="3d463-270">2부: 핵심 알고리즘</span><span class="sxs-lookup"><span data-stu-id="3d463-270">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="3d463-271">3부: 바인딩 리디렉션을 통한 통합</span><span class="sxs-lookup"><span data-stu-id="3d463-271">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a><span data-ttu-id="3d463-272">패키지 유형 설정</span><span class="sxs-lookup"><span data-stu-id="3d463-272">Setting a package type</span></span>

<span data-ttu-id="3d463-273">NuGet 3.5 이상을 사용하면 의도한 용도를 나타내기 위해 패키지를 특정 *패키지 유형*으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-273">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="3d463-274">이전 버전의 NuGet으로 만든 모든 패키지를 포함하여 유형으로 표시되지 않은 패키지의 기본값은 `Dependency` 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-274">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="3d463-275">`Dependency` 유형 패키지는 라이브러리 또는 응용 프로그램에 빌드 시간 자산 또는 런타임 자산을 추가하며, 모든 프로젝트 형식에 설치할 수 있습니다(호환된다고 가정할 경우).</span><span class="sxs-lookup"><span data-stu-id="3d463-275">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="3d463-276">`DotnetCliTool` 유형 패키지는 [.NET CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index)의 확장이며, 명령줄에서 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-276">`DotnetCliTool` type packages are extensions to the [.NET CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="3d463-277">이러한 패키지는 .NET Core 프로젝트에만 설치할 수 있으며 복원 작업에는 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-277">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="3d463-278">이러한 프로젝트별 확장에 대한 자세한 내용은 [.NET Core 확장성](https://docs.microsoft.com/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d463-278">More details about these per-project extensions are available in the  [.NET Core extensibility](https://docs.microsoft.com/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

    <span data-ttu-id="3d463-279">DotnetCliTool 패키지가 설치되면 Visual Studio에서 패키지를 `dependencies` 노드 대신 `project.json` `tools` 노드에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-279">When a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

- <span data-ttu-id="3d463-280">사용자 지정 유형 패키지는 패키지 ID와 동일한 형식 규칙을 준수하는 임의 형식의 식별자를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-280">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="3d463-281">그러나 `Dependency` 및 `DotnetCliTool` 이외의 유형은 Visual Studio의 NuGet 패키지 관리자에서 인식되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-281">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="3d463-282">패키지 유형은 `.nuspec` 파일 또는 `project.json`에 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-282">Package types are set either in the `.nuspec` file or in `project.json`.</span></span> <span data-ttu-id="3d463-283">두 경우 모두 이전 버전과의 호환성에서 `Dependency` 유형을 명시적으로 *설정하지 않고*, 유형을 지정하지 않은 경우 이 유형을 가정하여 NuGet을 대신 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-283">In both cases, it's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="3d463-284">`.nuspec`: `<metadata>` 요소 아래의 `packageTypes\packageType` 노드 내에서 패키지 유형을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-284">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

- <span data-ttu-id="3d463-285">`project.json`: `packOptions.packageType` 속성 json 내에 패키지 유형을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-285">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="3d463-286">추가 정보 및 기타 파일 추가</span><span class="sxs-lookup"><span data-stu-id="3d463-286">Adding a readme and other files</span></span>

<span data-ttu-id="3d463-287">패키지에 포함할 파일을 직접 지정 하려면 `.nuspec` 파일에서 `<metadata>` 태그 *다음에 오는* `<files>` 노드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-287">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

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
> <span data-ttu-id="3d463-288">규칙 기반 작업 디렉터리 방식을 사용하는 경우 패키지 루트에 readme.txt를 배치하고, `content` 폴더에는 다른 콘텐츠를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-288">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="3d463-289">매니페스트에는 `<file>` 요소가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-289">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="3d463-290">패키지 루트에 `readme.txt`라는 파일이 포함되면 Visual Studio에서 패키지를 직접 설치한 직후 해당 파일의 내용을 일반 텍스트로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-290">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="3d463-291">종속성으로 설치된 패키지에는 추가 정보 파일이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-291">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="3d463-292">예를 들어 HtmlAgilityPack 패키지에 대한 추가 정보가 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-292">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![설치 시 NuGet 패키지에 대한 추가 정보 파일 표시](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="3d463-294">`.nuspec` 파일에서 빈 `<files>` 노드가 포함되면 NuGet은 `lib` 폴더에 있는 것 이외의 다른 콘텐츠를 패키지에 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-294">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="3d463-295">패키지에 MSBuild props 및 targets 포함</span><span class="sxs-lookup"><span data-stu-id="3d463-295">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="3d463-296">경우에 따라 패키지를 사용하는 프로젝트에 사용자 지정 빌드 대상 또는 속성(예: 빌드하는 동안 사용자 지정 도구 또는 프로세스 실행)을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-296">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="3d463-297">이렇게 하려면 프로젝트의 `\build` 폴더 내에 `<package_id>.targets` 또는 `<package_id>.props`(예: `Contoso.Utility.UsefulStuff.targets`) 형식의 파일을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-297">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="3d463-298">루트 `\build` 폴더의 파일은 모든 대상 프레임워크에 적합한 파일로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-298">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="3d463-299">프레임워크 특정 파일을 제공하려면 먼저 다음과 같이 적절한 하위 폴더에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-299">To provide framework-specific files, first place those within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="3d463-300">그런 다음 `.nuspec` 파일의 `<files>` 노드에서 이러한 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-300">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
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

<span data-ttu-id="3d463-301">NuGet 2.x에서 `\build` 파일이 포함된 패키지를 설치하는 경우 `.targets` 및 `.props` 파일을 가리키는 MSBuild `<Import>` 요소를 프로젝트 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-301">When NuGet 2.x installs a package with `\build` files, it adds an MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="3d463-302">(`.props`는 프로젝트 파일의 위쪽에 추가되고, `.targets`는 아래쪽에 추가됩니다.)</span><span class="sxs-lookup"><span data-stu-id="3d463-302">(`.props` is added at the top of the project file; `.targets` is added at the bottom.)</span></span>

<span data-ttu-id="3d463-303">NuGet 3.x를 사용하면 대상이 프로젝트에 추가되지 않고 대신 `project.lock.json`을 통해 사용할 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-303">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="3d463-304">COM interop 어셈블리가 포함된 패키지 제작</span><span class="sxs-lookup"><span data-stu-id="3d463-304">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="3d463-305">COM interop 어셈블리가 포함된 패키지에는 적절한 [targets 파일](#including-msbuild-props-and-targets-in-a-package)이 포함되어야 올바른 `EmbedInteropTypes` 메타데이터가 PackageReference 형식을 사용하여 프로젝트에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-305">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="3d463-306">기본적으로 PackageReference를 사용하는 경우 `EmbedInteropTypes` 메타데이터는 모든 어셈블리에 대해 항상 false이므로 targets 파일에는 이 메타데이터가 명시적으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-306">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="3d463-307">충돌을 방지하기 위해 대상 이름은 고유해야 합니다. 이상적으로는 패키지 이름과 포함되는 어셈블리의 조합을 사용하여 아래 예제의 `{InteropAssemblyName}`을 해당 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-307">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="3d463-308">(예제는 [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop)을 참조하세요.)</span><span class="sxs-lookup"><span data-stu-id="3d463-308">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml      
<Target Name="EmbeddingAssemblyNameFromPackageId" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <PropertyGroup>
    <_InteropAssemblyFileName>{InteropAssemblyName}</_InteropAssemblyFileName>
  </PropertyGroup>
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '$(_InteropAssemblyFileName)' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="3d463-309">`packages.config` 참조 형식을 사용하는 경우 패키지에서 어셈블리에 대한 참조를 추가하면 NuGet 및 Visual Studio에서 COM interop 어셈블리를 확인하고 프로젝트 파일에서 `EmbedInteropTypes`를 true로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-309">Note that when using the `packages.config` reference format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="3d463-310">이 경우 targets 파일이 재정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-310">In this case the targets are overriden.</span></span>

<span data-ttu-id="3d463-311">또한 기본적으로 [빌드 자산은 전이적으로 이동하지 않습니다](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="3d463-311">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="3d463-312">여기서 설명한 대로 작성된 패키지는 프로젝트 간 참조에서 전이 종속성으로 끌어올 때 다르게 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-312">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="3d463-313">패키지 소비자는 빌드를 포함하지 않도록 PrivateAssets 기본값을 수정하여 패키지를 이동할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-313">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>  

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="3d463-314">nugkg pack을 실행하여 .nupkg 파일 생성</span><span class="sxs-lookup"><span data-stu-id="3d463-314">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="3d463-315">어셈블리 또는 규칙 기반 작업 디렉터리를 사용하는 경우 `.nuspec` 파일이 포함된 `nuget pack`을 실행하고 `<manifest-name>`을 특정 파일 이름으로 바꿔 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-315">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<manifest-name>` with your specific filename:</span></span>

```
nuget pack <project-name>.nuspec
```

<span data-ttu-id="3d463-316">Visual Studio 프로젝트를 사용하는 경우 프로젝트 파일이 포함된 `nuget pack`을 실행하면 프로젝트 파일의 값을 사용하여 프로젝트의 `.nuspec` 파일을 자동으로 로드하고 그 안에 있는 모든 토큰을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-316">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="3d463-317">프로젝트가 토큰 값의 원본이므로 토큰 대체의 경우 프로젝트 파일을 직접 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-317">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="3d463-318">`.nuspec` 파일이 포함된 `nuget pack`을 사용하면 토큰 대체가 발생하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-318">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="3d463-319">모든 경우에 `nuget pack`은 마침표로 시작하는 폴더(예: `.git` 또는 `.hg`)를 제외합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-319">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="3d463-320">NuGet은 매니페스트의 자리 표시자 값을 변경하지 않은 경우와 같이 수정이 필요한 오류가 `.nuspec` 파일에 있는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-320">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="3d463-321">`nuget pack`이 성공하면 [패키지 게시](../create-packages/publish-a-package.md)에서 설명한 대로 적합한 갤러리에 게시할 수 있는 `.nupkg` 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-321">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="3d463-322">패키지를 만든 후 검사하는 유용한 방법은 [패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) 도구에서 해당 패키지를 여는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-322">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="3d463-323">이렇게 하면 패키지의 내용과 해당 매니페스트를 보여 주는 그래픽 뷰가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-323">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="3d463-324">또한 결과 `.nupkg` 파일의 이름을 `.zip` 파일로 바꾸고 그 내용을 직접 탐색할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-324">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="3d463-325">추가 옵션</span><span class="sxs-lookup"><span data-stu-id="3d463-325">Additional options</span></span>

<span data-ttu-id="3d463-326">`nuget pack`에서 다양한 명령줄 스위치를 사용하여 파일을 제외하고, 매니페스트의 버전 번호를 재정의하고, 다른 기능 중에서 출력 폴더를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-326">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="3d463-327">전체 목록은 [pack 명령 참조](../tools/cli-ref-pack.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3d463-327">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="3d463-328">다음은 Visual Studio 프로젝트에서 일반적으로 사용되는 몇 가지 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-328">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="3d463-329">**참조된 프로젝트**: 프로젝트에서 다른 프로젝트를 참조하는 경우 `-IncludeReferencedProjects` 옵션을 사용하여 참조된 프로젝트를 패키지의 일부로 또는 종속성으로 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-329">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="3d463-330">이 포함 프로세스는 재귀적이므로, `MyProject.csproj`에서 B와 C 프로젝트를 참조하고 해당 프로젝트에서 D, E 및 F를 참조하면, B, C, D, E 및 F의 파일이 패키지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-330">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="3d463-331">참조된 프로젝트에 자체의 `.nuspec` 파일이 포함되어 있으면 NuGet은 참조된 프로젝트를 종속성으로 대신 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-331">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="3d463-332">해당 프로젝트를 별도로 패키지하고 게시해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-332">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="3d463-333">**빌드 구성**: 기본적으로 NuGet은 프로젝트 파일에 설정된 기본 빌드 구성(일반적으로 *Debug*)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-333">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="3d463-334">*Release*와 같은 다른 빌드 구성의 파일을 압축하려면 다음과 같이 구성에 `-properties` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-334">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="3d463-335">**기호**: 소비자가 디버거에서 패키지 코드를 단계별로 실행할 수 있게 하는 기호를 포함하려면 `-Symbols` 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-335">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="3d463-336">패키지 설치 테스트</span><span class="sxs-lookup"><span data-stu-id="3d463-336">Testing package installation</span></span>

<span data-ttu-id="3d463-337">일반적으로 패키지를 게시하기 전에 프로젝트에 패키지를 설치하는 프로세스를 테스트하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-337">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="3d463-338">테스트를 통해 모든 파일이 프로젝트의 올바른 위치에 있는지 반드시 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-338">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="3d463-339">일반적인 [패키지 설치 단계](../Quickstart/Use-a-Package.md)를 사용하여 Visual Studio 또는 명령줄에서 수동으로 설치를 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-339">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../Quickstart/Use-a-Package.md).</span></span>

<span data-ttu-id="3d463-340">자동 테스트의 경우 기본 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-340">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="3d463-341">`.nupkg` 파일을 로컬 폴더에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-341">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="3d463-342">`nuget sources -name <name> -source <path>` 명령([nuget sources](../tools/cli-ref-sources.md) 참조)을 사용하여 패키지 원본에 폴더를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-342">Add the folder to your package sources using the `nuget sources -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="3d463-343">지정된 컴퓨터에서 이 로컬 원본을 한 번만 설정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-343">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="3d463-344">`nuget install <packageID> -source <name>`을 사용하여 해당 원본에서 패키지를 설치합니다. 여기서 `<name>`은 `nuget sources`에 지정된 원본 이름과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-344">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="3d463-345">원본을 지정하면 해당 원본에서만 패키지가 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-345">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="3d463-346">파일 시스템을 검사하여 파일이 올바르게 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-346">Examine the file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d463-347">다음 단계</span><span class="sxs-lookup"><span data-stu-id="3d463-347">Next Steps</span></span>

<span data-ttu-id="3d463-348">패키지(`.nupkg` 파일)를 만들었으면 [패키지 게시](../create-packages/publish-a-package.md)에서 설명한 대로 원하는 갤러리에 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-348">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="3d463-349">다음 항목에서 설명한 대로 패키지의 기능을 확장하거나 그렇지 않고 다른 시나리오를 지원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-349">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="3d463-350">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="3d463-350">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="3d463-351">여러 대상 프레임워크 지원</span><span class="sxs-lookup"><span data-stu-id="3d463-351">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="3d463-352">원본 및 구성 파일 변환</span><span class="sxs-lookup"><span data-stu-id="3d463-352">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="3d463-353">지역화</span><span class="sxs-lookup"><span data-stu-id="3d463-353">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="3d463-354">시험판 버전</span><span class="sxs-lookup"><span data-stu-id="3d463-354">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="3d463-355">마지막으로 주의해야 할 추가 패키지 유형이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3d463-355">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="3d463-356">네이티브 패키지</span><span class="sxs-lookup"><span data-stu-id="3d463-356">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="3d463-357">기호 패키지</span><span class="sxs-lookup"><span data-stu-id="3d463-357">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
