---
title: "Visual Studio 2015를 사용하여 .NET Standard NuGet 패키지 만들기 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: "NuGet 3.x 및 Visual Studio 2015를 사용하여 .NET Standard NuGet 패키지를 만드는 종단 간 연습입니다."
keywords: "패키지 만들기, .NET Standard 패키지, .NET Standard 매핑 테이블"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a912c27e1873d60426f2147995f69e2dcc433ca9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="7abc1-104">Visual Studio 2015를 사용하여 .NET Standard 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="7abc1-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="7abc1-105">*NuGet 3.x에 적용됩니다. NuGet 4.x 이상을 사용하려면 [Visual Studio 2017을 사용하여 .NET Standard 패키지 만들기](../guides/create-net-standard-packages-vs2017.md)를 참조하세요.*</span><span class="sxs-lookup"><span data-stu-id="7abc1-105">*Applies to NuGet 3.x. See [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="7abc1-106">[.NET Standard 라이브러리](https://docs.microsoft.com/dotnet/articles/standard/library)는 모든 .NET 런타임에서 사용할 수 있도록 만들어진 .NET API의 공식 사양이며, 이에 따라 .NET 생태계에서 더 균일하게 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-106">The [.NET Standard Library](https://docs.microsoft.com/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="7abc1-107">.NET Standard 라이브러리는 워크로드와는 별도로 구현할 모든 .NET 플랫폼에 대해 균일한 BCL(기본 클래스 라이브러리) API 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="7abc1-108">개발자가 모든 .NET 런타임에서 사용할 수 있는 PCL을 생성할 수 있으며, 공유 코드에서 플랫폼별 조건부 컴파일 지시문을 제거하지 않더라도 이를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="7abc1-109">이 가이드에서는 .NET Standard 라이브러리 1.4를 대상으로 하는 NuGet 패키지를 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="7abc1-110">이 패키지는 .NET Framework 4.6.1, 유니버설 Windows 플랫폼 10, .NET Core 및 Mono/Xamarin에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-110">This will work across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="7abc1-111">자세한 내용은 이 항목의 뒷부분에 있는 [.NET Standard 매핑 테이블](#net-standard-mapping-table)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7abc1-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

1. [<span data-ttu-id="7abc1-112">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="7abc1-112">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="7abc1-113">클래스 라이브러리 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="7abc1-113">Create the class library project</span></span>](#create-the-class-library-project)
1. [<span data-ttu-id="7abc1-114">.nuspec 파일 만들기 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="7abc1-114">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="7abc1-115">구성 요소 패키징</span><span class="sxs-lookup"><span data-stu-id="7abc1-115">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="7abc1-116">추가 옵션</span><span class="sxs-lookup"><span data-stu-id="7abc1-116">Additional options</span></span>](#additional-options)
1. [<span data-ttu-id="7abc1-117">.NET Standard 매핑 테이블</span><span class="sxs-lookup"><span data-stu-id="7abc1-117">.NET Standard mapping table</span></span>](#net-standard-mapping-table)
1. [<span data-ttu-id="7abc1-118">관련 항목</span><span class="sxs-lookup"><span data-stu-id="7abc1-118">Related topics</span></span>](#related-topics)


## <a name="pre-requisites"></a><span data-ttu-id="7abc1-119">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="7abc1-119">Pre-requisites</span></span>

1. <span data-ttu-id="7abc1-120">Visual Studio 2015 -</span><span class="sxs-lookup"><span data-stu-id="7abc1-120">Visual Studio 2015.</span></span> <span data-ttu-id="7abc1-121">[visualstudio.com](https://www.visualstudio.com/)에서 추가 비용 없이 Community 버전을 설치합니다. Professional 및 Enterprise 버전도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-121">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span>
1. <span data-ttu-id="7abc1-122">.NET Core - [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849)에서 Visual Studio 2015용 템플릿 및 다른 도구와 함께 .NET Core를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-122">.NET Core: Install .NET Core along with templates and other tools for Visual Studio 2015 from [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span></span>
1. <span data-ttu-id="7abc1-123">NuGet CLI -</span><span class="sxs-lookup"><span data-stu-id="7abc1-123">NuGet CLI.</span></span> <span data-ttu-id="7abc1-124">[nuget.org/downloads](https://nuget.org/downloads)에서 최신 버전의 nuget.exe를 다운로드하여 원하는 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-124">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="7abc1-125">그런 다음 해당 위치를 PATH 환경 변수에 추가합니다(아직 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="7abc1-125">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="7abc1-126">nuget.exe는 설치 관리자가 아니라 CLI 도구 자체이므로 브라우저에서 다운로드한 파일을 실행하는 대신 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-126">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>



## <a name="create-the-class-library-project"></a><span data-ttu-id="7abc1-127">클래스 라이브러리 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="7abc1-127">Create the class library project</span></span>

1. <span data-ttu-id="7abc1-128">Visual Studio의 **파일> 새로 만들기> 프로젝트**에서 **Visual C# > Windows** 노드를 차례로 펼치고, **클래스 라이브러리(이식 가능)**를 선택하고, 이름을 AppLogger로 변경한 다음, [확인]을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-128">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![새 클래스 라이브러리 프로젝트 만들기](media/NetStandard-NewProject.png)

1. <span data-ttu-id="7abc1-130">**이식 가능한 클래스 라이브러리 추가** 대화 상자가 표시되면 `.NET Framework 4.6` 및 `ASP.NET Core 1.0` 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-130">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>
1. <span data-ttu-id="7abc1-131">[솔루션 탐색기]에서 `AppLogger (Portable)`을 마우스 오른쪽 단추로 클릭하고, **속성**을 선택하고, **라이브러리** 탭을 선택한 다음, **대상 지정** 섹션에서 **.NET 플랫폼 표준을 대상으로 지정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-131">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="7abc1-132">그러면 확인 메시지가 표시되며, 드롭다운 목록에서 `.NET Standard 1.4`를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-132">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![대상을 .NET Standard 1.4로 설정](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="7abc1-134">**빌드** 탭을 클릭하고, **구성**을 `Release`로 변경하고, **XML 문서 파일** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-134">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>
1. <span data-ttu-id="7abc1-135">구성 요소에 다음과 같은 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-135">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. <span data-ttu-id="7abc1-136">프로젝트를 빌드하고([릴리스] 구성 사용), DLL 및 XML 파일이 bin\Release 폴더 내에 생성되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-136">Build the project (with the Release configuration) and check that DLL and XML files are produced within the bin\Release folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="7abc1-137">.nuspec 파일 만들기 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="7abc1-137">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="7abc1-138">명령 프롬프트를 열고, `.sln` 파일이 있는 위치에서 한 수준 아래의 `AppLogg.csproj` 폴더로 이동한 다음, NuGet `spec` 명령을 실행하여 초기 `AppLogger.nuspec` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-138">Open a command prompt, navigate to the folder containing `AppLogg.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

```
nuget spec
```

1. <span data-ttu-id="7abc1-139">편집기에서 `AppLogger.nuspec`을 열고 YOUR_NAME을 적절한 값으로 바꿔 다음과 일치하도록 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-139">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="7abc1-140">특히 `<id>` 값은 nuget.org 전체에서 고유해야 합니다([패키지 만들기](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)에서 설명한 명명 규칙 참조).</span><span class="sxs-lookup"><span data-stu-id="7abc1-140">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="7abc1-141">또한 작성자 및 설명 태그도 업데이트해야 합니다. 그렇지 않으면 압축 단계에서 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-141">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>AppLogger.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>AppLogger</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. <span data-ttu-id="7abc1-142">참조 어셈블리를 `.nuspec` 파일, 즉 라이브러리의 DLL 및 IntelliSense XML 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-142">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="7abc1-143">솔루션을 마우스 오른쪽 단추로 클릭하고 **솔루션 빌드**를 선택하여 패키지에 대한 모든 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-143">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="7abc1-144">구성 요소 패키징</span><span class="sxs-lookup"><span data-stu-id="7abc1-144">Package the component</span></span>

<span data-ttu-id="7abc1-145">완료된 `.nuspec`에서 패키지에 포함되어야 하는 모든 파일을 참조하면 `pack` 명령을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-145">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack AppLogger.nuspec
```

<span data-ttu-id="7abc1-146">그러면 `AppLogger.YOUR_NAME.1.0.0.nupkg`가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-146">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="7abc1-147">[NuGet 패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)와 같은 도구에서 이 파일을 열고 모든 노드를 펼치면 다음과 같은 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-147">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![AppLogger 패키지를 보여 주는 NuGet 패키지 탐색기](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="7abc1-149">`.nupkg` 파일은 확장명이 다른 ZIP 파일일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-149">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="7abc1-150">`.nupkg`를 `.zip`으로 변경하여 패키지 내용을 검사할 수도 있지만 패키지를 nuget.org에 업로드하려면 먼저 확장명을 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-150">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="7abc1-151">다른 개발자가 패키지를 사용할 수 있게 하려면 [패키지 게시](../create-packages/publish-a-package.md)의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="7abc1-151">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="7abc1-152">`pack`에는 Mac OS X에서 Mono 4.4.2가 필요하며, Linux 시스템에서는 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-152">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="7abc1-153">또한 Mac에서는 `.nuspec` 파일의 Windows 경로 이름을 Unix 스타일 경로로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-153">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="additional-options"></a><span data-ttu-id="7abc1-154">추가 옵션</span><span class="sxs-lookup"><span data-stu-id="7abc1-154">Additional options</span></span>

<span data-ttu-id="7abc1-155">다음 섹션에서는 NuGet 패키지를 만들기 위한 추가 옵션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-155">The following sections go into additional options for NuGet package creation:</span></span>

- [<span data-ttu-id="7abc1-156">종속성 선언</span><span class="sxs-lookup"><span data-stu-id="7abc1-156">Declaring dependencies</span></span>](#declaring-dependencies)
- [<span data-ttu-id="7abc1-157">여러 대상 프레임워크 지원</span><span class="sxs-lookup"><span data-stu-id="7abc1-157">Supporting multiple target frameworks</span></span>](#supporting-multiple-target-frameworks)
- [<span data-ttu-id="7abc1-158">MSBuild용 targets 및 props 추가</span><span class="sxs-lookup"><span data-stu-id="7abc1-158">Adding targets and props for MSBuild</span></span>](#adding-targets-and-props-for-msbuild)
- [<span data-ttu-id="7abc1-159">지역화된 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="7abc1-159">Creating localized packages</span></span>](#creating-localized-packages)
- [<span data-ttu-id="7abc1-160">추가 정보 추가</span><span class="sxs-lookup"><span data-stu-id="7abc1-160">Adding a readme</span></span>](#adding-a-readme)

### <a name="declaring-dependencies"></a><span data-ttu-id="7abc1-161">종속성 선언</span><span class="sxs-lookup"><span data-stu-id="7abc1-161">Declaring dependencies</span></span>

<span data-ttu-id="7abc1-162">다른 NuGet 패키지에 대한 종속성이 있는 경우 `<dependencies>` 요소에서 `<group>` 요소를 사용하여 해당 패키지를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-162">If you have any dependencies on other NuGet packages, list those in the `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="7abc1-163">예를 들어 NewtonSoft.Json 8.0.3 이상에 대한 종속성을 선언하려면 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-163">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="7abc1-164">여기서 *version* 특성의 구문은 버전 8.0.3 이상을 사용할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-164">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="7abc1-165">다른 버전 범위를 지정하려면 [패키지 버전 관리](../reference/package-versioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7abc1-165">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="supporting-multiple-target-frameworks"></a><span data-ttu-id="7abc1-166">여러 대상 프레임워크 지원</span><span class="sxs-lookup"><span data-stu-id="7abc1-166">Supporting multiple target frameworks</span></span>

<span data-ttu-id="7abc1-167">.NET Standard 1.4에서 사용할 수 없는 .NET Framework 4.6.2의 API를 활용하려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-167">Suppose you'd like to take advantage of an API in .NET Framework 4.6.2 that is not available in .NET Standard 1.4.</span></span> <span data-ttu-id="7abc1-168">이렇게 하려면 먼저 조건부 컴파일 또는 공유 프로젝트를 사용하여 라이브러리가 .NET 4.6.2용으로 컴파일되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-168">To do this, you'll first need to make sure the library compiles for .NET 4.6.2 by using conditional compilation or shared projects.</span></span> <span data-ttu-id="7abc1-169">(Visual Studio에서 NetCore 프로젝트를 만들고, 여러 프레임워크 섹션에 선택한 프레임워크를 추가한 다음, 빌드할 수 있습니다.) 다음으로, 다음과 같이 간단한 규칙 기반 작업 디렉터리 기술을 사용하여 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-169">(In Visual Studio, you can create a NetCore project, add the framework of choice to the multiple framework section, and then build.) Then you create the package using the simple convention-based working directory technique as follows:</span></span>

1. <span data-ttu-id="7abc1-170">`.nuspec` 파일이 포함된 프로젝트의 루트 폴더에서 `lib`라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-170">In the project's root folder containing your `.nuspec` file, create a folder named `lib`.</span></span>
1. <span data-ttu-id="7abc1-171">`lib` 내에서 지원하려는 각 플랫폼에 대한 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-171">Inside `lib`, create folders for each platform you want to support:</span></span>

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. <span data-ttu-id="7abc1-172">`.nuspec` 파일에서 `package` 노드 아래에 `files` 노드를 추가하고, 와일드카드를 사용하여 `lib`에 있는 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-172">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `lib` using wildcards.</span></span> <span data-ttu-id="7abc1-173">**참고:** 토큰 대체는 규칙 기반 작업 디렉터리 접근 방식에서 지원되지 않으므로 리터럴 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-173">**Note:** Token replacements are not supported with the convention-based working directory approach, so replace them with literal values:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="7abc1-174">`nuget pack AppLogger.spec`을 사용하여 패키지를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-174">Create the package again using `nuget pack AppLogger.spec`.</span></span>

<span data-ttu-id="7abc1-175">이 기술의 사용에 대한 자세한 내용은 [여러 .NET Framework 버전 지원](../create-packages/supporting-multiple-target-frameworks.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7abc1-175">For more details on using this technique, see [Supporting Multiple .NET Framework Versions](../create-packages/supporting-multiple-target-frameworks.md)</span></span>

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="7abc1-176">MSBuild용 targets 및 props 추가</span><span class="sxs-lookup"><span data-stu-id="7abc1-176">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="7abc1-177">경우에 따라 패키지를 사용하는 프로젝트에 사용자 지정 빌드 대상 또는 속성(예: 빌드하는 동안 사용자 지정 도구 또는 프로세스 실행)을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-177">In some cases you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="7abc1-178">이렇게 하려면 아래 단계에서 설명한 대로 `\build` 폴더에 파일을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-178">You do this by adding files in a `\build` folder as described in the steps below.</span></span> <span data-ttu-id="7abc1-179">NuGet에서 \build 파일이 포함된 패키지를 설치하는 경우 .targets 및 .props 파일을 가리키는 MSBuild 요소를 프로젝트 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-179">When NuGet installs a package with \build files, it adds an MSBuild element in the project file pointing to the .targets and .props files.</span></span>

> [!Note]
> <span data-ttu-id="7abc1-180">`project.json`을 사용하는 경우 대상이 프로젝트에는 추가되지 않지만 `project.lock.json`을 통해 사용될 수 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-180">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>


1. <span data-ttu-id="7abc1-181">`.nuspec` 파일이 포함된 프로젝트 폴더에서 `build`라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-181">In the project folder containing the your `.nuspec` file, create a folder named `build`.</span></span>
1. <span data-ttu-id="7abc1-182">`build` 내에서 지원되는 각 폴더를 만들고 해당 위치 내에 `.targets` 및 `.props` 파일을 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-182">Inside `build`, create folders for each supported, and within those place your `.targets` and `.props` files:</span></span>

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. <span data-ttu-id="7abc1-183">`.nuspec` 파일에서 `package` 노드 아래에 `files` 노드를 추가하고, 와일드카드를 사용하여 `build`에 있는 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-183">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `build` using wildcards.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. <span data-ttu-id="7abc1-184">`nuget pack AppLogger.nuspec`을 사용하여 패키지를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-184">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>

<span data-ttu-id="7abc1-185">자세한 내용은 [패키지에 MSBuild props 및 targets 포함](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7abc1-185">For additional details, refer to [Include MSBuild props and targets in a package](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span></span>


### <a name="creating-localized-packages"></a><span data-ttu-id="7abc1-186">지역화된 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="7abc1-186">Creating localized packages</span></span>

<span data-ttu-id="7abc1-187">지역화된 라이브러리 버전을 만들려면 서로 다른 로캘에 대해 별도의 패키지를 만들거나 단일 패키지 내에 지역화된 리소스 어셈블리를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-187">To create localized versions of your library, you can either create separate packages for different locales, or include localized resource assemblies within a single package.</span></span> <span data-ttu-id="7abc1-188">독일어와 이탈리아어에 대해 후자의 방법을 수행하는 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-188">Here's how to do the latter approach for German and Italian:</span></span>

1. <span data-ttu-id="7abc1-189">`lib` 아래의 각 대상 프레임워크 폴더 내에서 영어 기본값 이외의 지원되는 각 언어에 대한 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-189">Within each target framework folder under `lib`, create folders for each supported language other than the English default.</span></span> <span data-ttu-id="7abc1-190">이러한 폴더에 리소스 어셈블리와 지역화된 IntelliSense XML 파일을 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-190">In these folders you can place resource assemblies  and localized IntelliSense XML files.</span></span> <span data-ttu-id="7abc1-191">예:</span><span class="sxs-lookup"><span data-stu-id="7abc1-191">For example:</span></span>

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. <span data-ttu-id="7abc1-192">`.nuspec` 파일에서 `<files>` 노드에 있는 다음 파일을 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-192">In the `.nuspec` file, reference these files in the `<files>` node:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="7abc1-193">`nuget pack AppLogger.nuspec`을 사용하여 패키지를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-193">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>


### <a name="adding-a-readme"></a><span data-ttu-id="7abc1-194">추가 정보 추가</span><span class="sxs-lookup"><span data-stu-id="7abc1-194">Adding a readme</span></span>

<span data-ttu-id="7abc1-195">패키지의 루트에 `readme.txt` 파일이 포함되면 패키지를 직접 설치할 때 Visual Studio에서 이를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-195">When you include a `readme.txt` file in the root of the package, Visual Studio will display it when the package is installed directly.</span></span>

> [!Note]
> <span data-ttu-id="7abc1-196">종속성으로 설치된 패키지 또는 .NET Core 프로젝트에 대한 추가 정보 파일은 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-196">Readme files are not shown for packages that are installed as a dependency, or for .NET Core projects.</span></span>


<span data-ttu-id="7abc1-197">이렇게 하려면 `readme.txt` 파일을 만들어 프로젝트 루트 폴더에 배치하고 `.nuspec` 파일에서 이를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="7abc1-197">To do this, create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```


## <a name="net-standard-mapping-table"></a><span data-ttu-id="7abc1-198">.NET Standard 매핑 테이블</span><span class="sxs-lookup"><span data-stu-id="7abc1-198">.NET Standard mapping table</span></span>

|<span data-ttu-id="7abc1-199">플랫폼 이름</span><span class="sxs-lookup"><span data-stu-id="7abc1-199">Platform Name</span></span> |<span data-ttu-id="7abc1-200">Alias</span><span class="sxs-lookup"><span data-stu-id="7abc1-200">Alias</span></span>|
|--------------|-----|
|<span data-ttu-id="7abc1-201">.NET 표준</span><span class="sxs-lookup"><span data-stu-id="7abc1-201">.NET Standard</span></span> | <span data-ttu-id="7abc1-202">netstandard</span><span class="sxs-lookup"><span data-stu-id="7abc1-202">netstandard</span></span>| <span data-ttu-id="7abc1-203">1.0</span><span class="sxs-lookup"><span data-stu-id="7abc1-203">1.0</span></span>| <span data-ttu-id="7abc1-204">1.1</span><span class="sxs-lookup"><span data-stu-id="7abc1-204">1.1</span></span>| <span data-ttu-id="7abc1-205">1.2</span><span class="sxs-lookup"><span data-stu-id="7abc1-205">1.2</span></span>| <span data-ttu-id="7abc1-206">1.3</span><span class="sxs-lookup"><span data-stu-id="7abc1-206">1.3</span></span>| <span data-ttu-id="7abc1-207">1.4</span><span class="sxs-lookup"><span data-stu-id="7abc1-207">1.4</span></span>| <span data-ttu-id="7abc1-208">1.5</span><span class="sxs-lookup"><span data-stu-id="7abc1-208">1.5</span></span>| <span data-ttu-id="7abc1-209">1.6</span><span class="sxs-lookup"><span data-stu-id="7abc1-209">1.6</span></span>|
|<span data-ttu-id="7abc1-210">.NET Core</span><span class="sxs-lookup"><span data-stu-id="7abc1-210">.NET Core</span></span> | <span data-ttu-id="7abc1-211">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="7abc1-211">netcoreapp</span></span>| <span data-ttu-id="7abc1-212">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-212">&#x2192;</span></span>| <span data-ttu-id="7abc1-213">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-213">&#x2192;</span></span>| <span data-ttu-id="7abc1-214">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-214">&#x2192;</span></span>| <span data-ttu-id="7abc1-215">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-215">&#x2192;</span></span>| <span data-ttu-id="7abc1-216">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-216">&#x2192;</span></span>| <span data-ttu-id="7abc1-217">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-217">&#x2192;</span></span>| <span data-ttu-id="7abc1-218">1.0</span><span class="sxs-lookup"><span data-stu-id="7abc1-218">1.0</span></span>|
|<span data-ttu-id="7abc1-219">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="7abc1-219">.NET Framework</span></span>| <span data-ttu-id="7abc1-220">net</span><span class="sxs-lookup"><span data-stu-id="7abc1-220">net</span></span>| <span data-ttu-id="7abc1-221">4.5</span><span class="sxs-lookup"><span data-stu-id="7abc1-221">4.5</span></span>| <span data-ttu-id="7abc1-222">4.5.1</span><span class="sxs-lookup"><span data-stu-id="7abc1-222">4.5.1</span></span>| <span data-ttu-id="7abc1-223">4.6</span><span class="sxs-lookup"><span data-stu-id="7abc1-223">4.6</span></span>| <span data-ttu-id="7abc1-224">4.6.1</span><span class="sxs-lookup"><span data-stu-id="7abc1-224">4.6.1</span></span>| <span data-ttu-id="7abc1-225">4.6.2</span><span class="sxs-lookup"><span data-stu-id="7abc1-225">4.6.2</span></span>| <span data-ttu-id="7abc1-226">4.6.3</span><span class="sxs-lookup"><span data-stu-id="7abc1-226">4.6.3</span></span>|
|<span data-ttu-id="7abc1-227">Mono/Xamarin 플랫폼</span><span class="sxs-lookup"><span data-stu-id="7abc1-227">Mono/Xamarin Platforms</span></span>| <span data-ttu-id="7abc1-228">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-228">&#x2192;</span></span>| <span data-ttu-id="7abc1-229">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-229">&#x2192;</span></span>| <span data-ttu-id="7abc1-230">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-230">&#x2192;</span></span>| <span data-ttu-id="7abc1-231">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-231">&#x2192;</span></span>| <span data-ttu-id="7abc1-232">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-232">&#x2192;</span></span>| <span data-ttu-id="7abc1-233">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-233">&#x2192;</span></span>|
|<span data-ttu-id="7abc1-234">유니버설 Windows 플랫폼</span><span class="sxs-lookup"><span data-stu-id="7abc1-234">Universal Windows Platform</span></span>| <span data-ttu-id="7abc1-235">uap</span><span class="sxs-lookup"><span data-stu-id="7abc1-235">uap</span></span>| <span data-ttu-id="7abc1-236">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-236">&#x2192;</span></span>| <span data-ttu-id="7abc1-237">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-237">&#x2192;</span></span>| <span data-ttu-id="7abc1-238">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-238">&#x2192;</span></span>| <span data-ttu-id="7abc1-239">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-239">&#x2192;</span></span>|<span data-ttu-id="7abc1-240">10.0</span><span class="sxs-lookup"><span data-stu-id="7abc1-240">10.0</span></span>|
|<span data-ttu-id="7abc1-241">창</span><span class="sxs-lookup"><span data-stu-id="7abc1-241">Windows</span></span>| <span data-ttu-id="7abc1-242">win</span><span class="sxs-lookup"><span data-stu-id="7abc1-242">win</span></span>| <span data-ttu-id="7abc1-243">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-243">&#x2192;</span></span>| <span data-ttu-id="7abc1-244">8.0</span><span class="sxs-lookup"><span data-stu-id="7abc1-244">8.0</span></span>| <span data-ttu-id="7abc1-245">8.1</span><span class="sxs-lookup"><span data-stu-id="7abc1-245">8.1</span></span>|
|<span data-ttu-id="7abc1-246">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="7abc1-246">Windows Phone</span></span>| <span data-ttu-id="7abc1-247">wpa</span><span class="sxs-lookup"><span data-stu-id="7abc1-247">wpa</span></span>| <span data-ttu-id="7abc1-248">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-248">&#x2192;</span></span>| <span data-ttu-id="7abc1-249">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="7abc1-249">&#x2192;</span></span>|<span data-ttu-id="7abc1-250">8.1</span><span class="sxs-lookup"><span data-stu-id="7abc1-250">8.1</span></span>|
|<span data-ttu-id="7abc1-251">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="7abc1-251">Windows Phone Silverlight</span></span>| <span data-ttu-id="7abc1-252">wp</span><span class="sxs-lookup"><span data-stu-id="7abc1-252">wp</span></span>| <span data-ttu-id="7abc1-253">8.0</span><span class="sxs-lookup"><span data-stu-id="7abc1-253">8.0</span></span>|



## <a name="related-topics"></a><span data-ttu-id="7abc1-254">관련 항목</span><span class="sxs-lookup"><span data-stu-id="7abc1-254">Related topics</span></span>

- [<span data-ttu-id="7abc1-255">.nuspec 참조</span><span class="sxs-lookup"><span data-stu-id="7abc1-255">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="7abc1-256">기호 패키지</span><span class="sxs-lookup"><span data-stu-id="7abc1-256">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="7abc1-257">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="7abc1-257">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="7abc1-258">여러 .NET Framework 버전 지원</span><span class="sxs-lookup"><span data-stu-id="7abc1-258">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="7abc1-259">패키지에 MSBuild props 및 targets 포함</span><span class="sxs-lookup"><span data-stu-id="7abc1-259">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="7abc1-260">지역화된 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="7abc1-260">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="7abc1-261">.NET Standard 라이브러리 설명서</span><span class="sxs-lookup"><span data-stu-id="7abc1-261">.NET Standard Library documentation</span></span>](https://docs.microsoft.com/dotnet/articles/standard/library)
- [<span data-ttu-id="7abc1-262">.NET Framework에서 .NET Core로 이식</span><span class="sxs-lookup"><span data-stu-id="7abc1-262">Porting to .NET Core from .NET Framework</span></span>](https://docs.microsoft.com/dotnet/articles/core/porting/index)
