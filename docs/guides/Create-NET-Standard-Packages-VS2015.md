---
title: Visual Studio 2015를 사용하여 .NET Standard 및 .NET Framework NuGet 패키지 만들기
description: NuGet 3.x 및 Visual Studio 2015를 사용하여 .NET Standard 및 .NET Framework NuGet 패키지를 만드는 종단 간 연습입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: c66e782ea5d4e9e2a9585d8301dc2a1b2e8c72b9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818736"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="226ef-103">Visual Studio 2015를 사용하여 .NET Standard 및 .NET Framework 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="226ef-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="226ef-104">**참고:** .NET Standard 라이브러리를 개발할 때는 Visual Studio 2017을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="226ef-105">Visual Studio 2015도 사용해도 되지만 .NET Core 도구가 미리 보기 상태로만 제공되었습니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="226ef-106">NuGet 4.x 이상과 Visual Studio 2017을 사용하려면 [Visual Studio 2017을 사용하여 패키지 생성 및 게시](../quickstart/create-and-publish-a-package-using-visual-studio.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="226ef-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="226ef-107">[.NET Standard 라이브러리](/dotnet/articles/standard/library)는 모든 .NET 런타임에서 사용할 수 있도록 만들어진 .NET API의 공식 사양이며, 이에 따라 .NET 생태계에서 더 균일하게 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="226ef-108">.NET Standard 라이브러리는 워크로드와는 별도로 구현할 모든 .NET 플랫폼에 대해 균일한 BCL(기본 클래스 라이브러리) API 집합을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="226ef-109">개발자가 모든 .NET 런타임에서 사용할 수 있는 코드를 생성할 수 있으며, 공유 코드에서 플랫폼별 조건부 컴파일 지시문을 제거하지 않더라도 이를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="226ef-110">이 가이드에서는 .NET Standard 라이브러리 1.4를 대상으로 하는 NuGet 패키지 또는 .NET Framework 4.6을 대상으로 하는 NuGet 패키지를 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="226ef-111">.NET Standard 1.4 라이브러리는 .NET Framework 4.6.1, 유니버설 Windows 플랫폼 10, .NET Core 및 Mono/Xamarin에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="226ef-112">자세한 내용은 [.NET Standard 매핑 테이블](/dotnet/standard/net-standard#net-implementation-support)(.NET 설명서)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="226ef-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="226ef-113">원하는 경우 다른 버전의 .NET Standard 라이브러리를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="226ef-114">전제 조건</span><span class="sxs-lookup"><span data-stu-id="226ef-114">Prerequisites</span></span>

1. <span data-ttu-id="226ef-115">Visual Studio 2015 업데이트 3</span><span class="sxs-lookup"><span data-stu-id="226ef-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="226ef-116">(.NET Standard에만 해당) [.NET Core SDK](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="226ef-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="226ef-117">NuGet CLI -</span><span class="sxs-lookup"><span data-stu-id="226ef-117">NuGet CLI.</span></span> <span data-ttu-id="226ef-118">[nuget.org/downloads](https://nuget.org/downloads)에서 최신 버전의 nuget.exe를 다운로드하여 원하는 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="226ef-119">그런 다음 해당 위치를 PATH 환경 변수에 추가합니다(아직 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="226ef-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="226ef-120">nuget.exe는 설치 관리자가 아니라 CLI 도구 자체이므로 브라우저에서 다운로드한 파일을 실행하는 대신 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="226ef-121">클래스 라이브러리 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="226ef-121">Create the class library project</span></span>

1. <span data-ttu-id="226ef-122">Visual Studio의 **파일> 새로 만들기> 프로젝트**에서 **Visual C# > Windows** 노드를 확장하고, **클래스 라이브러리(이식 가능)** 를 선택하고, 이름을 AppLogger로 변경한 다음, **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![새 클래스 라이브러리 프로젝트 만들기](media/NetStandard-NewProject.png)

1. <span data-ttu-id="226ef-124">**이식 가능한 클래스 라이브러리 추가** 대화 상자가 표시되면 `.NET Framework 4.6` 및 `ASP.NET Core 1.0`에 대한 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="226ef-125">(.NET Framework를 대상으로 하는 경우에는 원하는 적절한 옵션을 선택할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="226ef-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="226ef-126">.NET Standard를 대상으로 지정하는 경우 솔루션 탐색기에서 `AppLogger (Portable)`을 마우스 오른쪽 단추로 클릭하고, **속성**을 선택하고, **라이브러리** 탭을 선택한 다음, **대상 지정** 섹션에서 **.NET 플랫폼 표준을 대상으로 지정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="226ef-127">그러면 확인을 묻는 메시지가 표시되며, 확인하면 드롭다운에서 `.NET Standard 1.4`(또는 다른 사용 가능한 버전)를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![대상을 .NET Standard 1.4로 설정](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="226ef-129">**빌드** 탭을 클릭하고, **구성**을 `Release`로 변경하고, **XML 문서 파일** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="226ef-130">구성 요소에 다음과 같은 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-130">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. <span data-ttu-id="226ef-131">구성을 릴리스로 설정하고, 프로젝트를 빌드하고, DLL 및 XML 파일이 `bin\Release` 폴더 내에 생성되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="226ef-132">.nuspec 파일 만들기 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="226ef-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="226ef-133">명령 프롬프트를 열고, `.sln` 파일이 있는 위치에서 한 수준 아래의 `AppLogger.csproj` 폴더로 이동한 다음, NuGet `spec` 명령을 실행하여 초기 `AppLogger.nuspec` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="226ef-134">편집기에서 `AppLogger.nuspec`을 열고 YOUR_NAME을 적절한 값으로 바꿔 다음과 일치하도록 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="226ef-135">특히 `<id>` 값은 nuget.org 전체에서 고유해야 합니다([패키지 만들기](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)에서 설명한 명명 규칙 참조).</span><span class="sxs-lookup"><span data-stu-id="226ef-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="226ef-136">또한 작성자 및 설명 태그도 업데이트해야 합니다. 그렇지 않으면 압축 단계에서 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="226ef-137">참조 어셈블리를 `.nuspec` 파일, 즉 라이브러리의 DLL 및 IntelliSense XML 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="226ef-138">.NET Standard를 대상으로 지정하는 경우 항목은 다음과 유사하게 표시되고,</span><span class="sxs-lookup"><span data-stu-id="226ef-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="226ef-139">.NET Framework를 대상으로 하는 경우 항목이 다음과 유사하게 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="226ef-140">솔루션을 마우스 오른쪽 단추로 클릭하고 **솔루션 빌드**를 선택하여 패키지에 대한 모든 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="226ef-141">종속성 선언</span><span class="sxs-lookup"><span data-stu-id="226ef-141">Declaring dependencies</span></span>

<span data-ttu-id="226ef-142">다른 NuGet 패키지에 대한 종속성이 있는 경우 매니페스트의 `<dependencies>` 요소에서 `<group>` 요소를 사용하여 해당 패키지를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="226ef-143">예를 들어 NewtonSoft.Json 8.0.3 이상에 대한 종속성을 선언하려면 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="226ef-144">여기서 *version* 특성의 구문은 버전 8.0.3 이상을 사용할 수 있음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="226ef-145">다른 버전 범위를 지정하려면 [패키지 버전 관리](../reference/package-versioning.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="226ef-145">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="226ef-146">추가 정보 추가</span><span class="sxs-lookup"><span data-stu-id="226ef-146">Adding a readme</span></span>

<span data-ttu-id="226ef-147">`readme.txt` 파일을 만들어 프로젝트 루트 폴더에 배치하고 `.nuspec` 파일에서 이를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="226ef-148">프로젝트에 패키지가 설치되면 Visual Studio에서 `readme.txt`를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="226ef-149">.NET Core 프로젝트에 패키지가 설치되거나 패키지가 종속성으로 설치된 경우에는 파일이 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="226ef-150">구성 요소 패키징</span><span class="sxs-lookup"><span data-stu-id="226ef-150">Package the component</span></span>

<span data-ttu-id="226ef-151">완료된 `.nuspec`에서 패키지에 포함되어야 하는 모든 파일을 참조하면 `pack` 명령을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="226ef-152">이 명령은 `AppLogger.YOUR_NAME.1.0.0.nupkg`를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="226ef-153">[NuGet 패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)와 같은 도구에서 이 파일을 열고 모든 노드를 확장하면 다음과 같은 내용이 표시됩니다(.NET Standard의 경우).</span><span class="sxs-lookup"><span data-stu-id="226ef-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![AppLogger 패키지를 보여 주는 NuGet 패키지 탐색기](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="226ef-155">`.nupkg` 파일은 확장명이 다른 ZIP 파일일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="226ef-156">`.nupkg`를 `.zip`으로 변경하여 패키지 내용을 검사할 수도 있지만 패키지를 nuget.org에 업로드하려면 먼저 확장명을 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="226ef-157">다른 개발자가 패키지를 사용할 수 있게 하려면 [패키지 게시](../create-packages/publish-a-package.md)의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="226ef-157">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="226ef-158">`pack`에는 Mac OS X에서 Mono 4.4.2가 필요하며, Linux 시스템에서는 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="226ef-159">또한 Mac에서는 `.nuspec` 파일의 Windows 경로 이름을 Unix 스타일 경로로 변환해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="226ef-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="226ef-160">관련 항목</span><span class="sxs-lookup"><span data-stu-id="226ef-160">Related topics</span></span>

- [<span data-ttu-id="226ef-161">.nuspec 참조</span><span class="sxs-lookup"><span data-stu-id="226ef-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="226ef-162">여러 .NET Framework 버전 지원</span><span class="sxs-lookup"><span data-stu-id="226ef-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="226ef-163">패키지에 MSBuild props 및 targets 포함</span><span class="sxs-lookup"><span data-stu-id="226ef-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="226ef-164">지역화된 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="226ef-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="226ef-165">기호 패키지</span><span class="sxs-lookup"><span data-stu-id="226ef-165">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="226ef-166">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="226ef-166">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="226ef-167">.NET Standard 라이브러리 설명서</span><span class="sxs-lookup"><span data-stu-id="226ef-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="226ef-168">.NET Framework에서 .NET Core로 이식</span><span class="sxs-lookup"><span data-stu-id="226ef-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
