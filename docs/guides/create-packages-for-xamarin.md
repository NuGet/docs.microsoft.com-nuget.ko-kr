---
title: Visual Studio 2015를 사용하여 Xamarin용 NuGet 패키지 만들기(iOS, Android 및 Windows용)
description: iOS, Android 및 Windows에서 네이티브 API를 사용하는 Xamarin에 대한 NuGet 패키지를 만드는 종단 간 연습입니다.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/09/2017
ms.topic: tutorial
ms.openlocfilehash: 1189151b04da6dc4c7b680f759b6a8ca7c5bd85f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="create-packages-for-xamarin-with-visual-studio-2015"></a><span data-ttu-id="fe97f-103">Visual Studio 2015를 사용하여 Xamarin용 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="fe97f-103">Create packages for Xamarin with Visual Studio 2015</span></span>

<span data-ttu-id="fe97f-104">Xamarin용 패키지에는 런타임 운영 체제에 따라 iOS, Android 및 Windows에서 네이티브 API를 사용하는 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="fe97f-105">이 작업은 간단하지만 개발자가 공통 API 노출 영역을 통해 PCL 또는 .NET Standard 라이브러리에서 패키지를 사용할 수 있게 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="fe97f-106">이 연습에서는 Visual Studio 2015를 사용하여 iOS, Android 및 Windows의 모바일 프로젝트에 사용할 수 있는 플랫폼 간 NuGet 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-106">In this walkthrough you use Visual Studio 2015 create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="fe97f-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fe97f-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="fe97f-108">프로젝트 구조 및 추상화 코드 만들기</span><span class="sxs-lookup"><span data-stu-id="fe97f-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="fe97f-109">플랫폼 특정 코드 작성</span><span class="sxs-lookup"><span data-stu-id="fe97f-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="fe97f-110">.nuspec 파일 만들기 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="fe97f-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="fe97f-111">구성 요소 패키징</span><span class="sxs-lookup"><span data-stu-id="fe97f-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="fe97f-112">관련 항목</span><span class="sxs-lookup"><span data-stu-id="fe97f-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="fe97f-113">전제 조건</span><span class="sxs-lookup"><span data-stu-id="fe97f-113">Prerequisites</span></span>

1. <span data-ttu-id="fe97f-114">UWP(유니버설 Windows 플랫폼) 및 Xamarin이 있는 Visual Studio 2015 -</span><span class="sxs-lookup"><span data-stu-id="fe97f-114">Visual Studio 2015 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="fe97f-115">[visualstudio.com](https://www.visualstudio.com/)에서 추가 비용 없이 Community 버전을 설치합니다. Professional 및 Enterprise 버전도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="fe97f-116">UWP 및 Xamarin 도구를 포함하려면 사용자 지정 설치를 선택하고 적절한 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="fe97f-117">NuGet CLI -</span><span class="sxs-lookup"><span data-stu-id="fe97f-117">NuGet CLI.</span></span> <span data-ttu-id="fe97f-118">[nuget.org/downloads](https://nuget.org/downloads)에서 최신 버전의 nuget.exe를 다운로드하여 원하는 위치에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="fe97f-119">그런 다음 해당 위치를 PATH 환경 변수에 추가합니다(아직 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="fe97f-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="fe97f-120">nuget.exe는 설치 관리자가 아니라 CLI 도구 자체이므로 브라우저에서 다운로드한 파일을 실행하는 대신 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="fe97f-121">프로젝트 구조 및 추상화 코드 만들기</span><span class="sxs-lookup"><span data-stu-id="fe97f-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="fe97f-122">Visual Studio용 [Plugin for Xamarin Templates 확장](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates)을 다운로드하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-122">Download and run the [Plugin for Xamarin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="fe97f-123">이러한 템플릿을 사용하면 이 연습에 필요한 프로젝트 구조를 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="fe97f-124">Visual Studio의 **파일 > 새로 만들기 > 프로젝트**에서 `Plugin`을 검색하고, **Plugin for Xamarin** 템플릿을 선택하고, 이름을 LoggingLibrary로 변경한 다음, [확인]을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-124">In Visual Studio, **File > New > Project**, search for `Plugin`, select the **Plugin for Xamarin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Visual Studio에서 비어 있는 새 앱(이식 가능한 Xamarin.Forms) 프로젝트](media/CrossPlatform-NewProject.png)

<span data-ttu-id="fe97f-126">결과 솔루션에는 다양한 플랫폼 특정 프로젝트와 함께 두 개의 PCL 프로젝트가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-126">The resulting solution contains two PCL projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="fe97f-127">`Plugin.LoggingLibrary.Abstractions (Portable)`라는 PCL은 구성 요소의 공용 인터페이스(API 노출 영역)를 정의합니다. 이 경우 ILoggingLibrary.cs 파일에 포함된 `ILoggingLibrary` 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-127">The PCL named `Plugin.LoggingLibrary.Abstractions (Portable)`, defines the public interface (the API surface area) of the component, in this case the `ILoggingLibrary` interface contained in the ILoggingLibrary.cs file.</span></span> <span data-ttu-id="fe97f-128">여기서는 라이브러리에 대한 인터페이스를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-128">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="fe97f-129">다른 `Plugin.LoggingLibrary (Portable)` PCL에는 런타임 시 추상 인터페이스의 플랫폼 특정 구현을 찾는 CrossLoggingLibrary.cs의 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-129">The other PCL, `Plugin.LoggingLibrary (Portable)`, contains code in CrossLoggingLibrary.cs that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="fe97f-130">일반적으로 이 파일은 수정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-130">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="fe97f-131">`Plugin.LoggingLibrary.Android`와 같은 플랫폼 특정 프로젝트에는 각각 해당 LoggingLibraryImplementation.cs 파일의 네이티브 인터페이스 구현이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-131">The platform-specific projects, such as `Plugin.LoggingLibrary.Android`, each contain contain a native implementation of the interface in their respective LoggingLibraryImplementation.cs files.</span></span> <span data-ttu-id="fe97f-132">여기서는 라이브러리 코드를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-132">This is where you build out your library's code.</span></span>

<span data-ttu-id="fe97f-133">기본적으로 Abstractions 프로젝트의 ILoggingLibrary.cs 파일에는 인터페이스 정의가 있지만 메서드는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-133">By default, the ILoggingLibrary.cs file of the Abstractions project contains an interface definition, but no methods.</span></span> <span data-ttu-id="fe97f-134">이 연습의 목적을 위해 다음과 같이 `Log` 메서드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-134">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="fe97f-135">플랫폼 특정 코드 작성</span><span class="sxs-lookup"><span data-stu-id="fe97f-135">Write your platform-specific code</span></span>

<span data-ttu-id="fe97f-136">`ILoggingLibrary` 인터페이스 및 해당 메서드의 플랫폼 특정 구현을 구현하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-136">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="fe97f-137">각 플랫폼 프로젝트의 `LoggingLibraryImplementation.cs` 파일을 열고 필요한 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-137">Open the `LoggingLibraryImplementation.cs` file of each platform project and add the necessary code.</span></span> <span data-ttu-id="fe97f-138">예를 들어 다음과 같습니다(`Plugin.LoggingLibrary.Android` 프로젝트 사용).</span><span class="sxs-lookup"><span data-stu-id="fe97f-138">For example (using the `Plugin.LoggingLibrary.Android` project):</span></span>

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. <span data-ttu-id="fe97f-139">지원하려는 각 플랫폼에 대한 프로젝트에서 이 구현을 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-139">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="fe97f-140">iOS 프로젝트를 마우스 오른쪽 단추로 클릭하고, **속성**을 선택하고, **빌드** 탭을 클릭한 다음, **출력 경로** 및 **XML 문서 파일** 설정에서 "\iPhone"을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-140">Right-click the iOS project, select **Properties**, click the **Build** tab, and remove "\iPhone" from the **Output path** and **XML documentation file** settings.</span></span> <span data-ttu-id="fe97f-141">이는 이 연습에서 나중의 편의를 위한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-141">This is just for later convenience in this walkthrough.</span></span> <span data-ttu-id="fe97f-142">완료되면 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-142">Save the file when done.</span></span>
1. <span data-ttu-id="fe97f-143">솔루션을 마우스 오른쪽 단추로 클릭하고, **구성 관리자...** 를 선택한 다음, 지원하는 PCL 및 각 플랫폼에 대한 **빌드** 상자를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-143">Right-click the solution, select **Configuration Manager...**, and check the **Build** boxes for the PCLs and each platform you're supporting.</span></span>
1. <span data-ttu-id="fe97f-144">솔루션을 마우스 오른쪽 단추로 클릭하고, **솔루션 빌드**를 선택하여 작업을 확인하고, 다음에 패키지할 아티팩트를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="fe97f-145">누락된 참조에 대한 오류가 발생하면 솔루션을 마우스 오른쪽 단추로 클릭하고, **NuGet 패키지 복원**을 선택하여 종속성을 설치한 다음, 다시 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="fe97f-146">iOS용으로 빌드하려면 [Visual Studio용 Xamarin.iOS 소개](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)에서 설명한 대로 네트워크에서 Visual Studio에 연결된 Mac이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-146">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="fe97f-147">Mac을 사용할 수 없는 경우 구성 관리자에서 iOS 프로젝트를 선택 취소합니다(위 3단계).</span><span class="sxs-lookup"><span data-stu-id="fe97f-147">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="fe97f-148">.nuspec 파일 만들기 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="fe97f-148">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="fe97f-149">명령 프롬프트를 열고, `.sln` 파일이 있는 위치에서 한 수준 아래의 `LoggingLibrary` 폴더로 이동한 다음, NuGet `spec` 명령을 실행하여 초기 `Package.nuspec` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-149">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="fe97f-150">이 파일의 이름을 `LoggingLibrary.nuspec`으로 변경하고 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-150">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="fe97f-151">YOUR_NAME을 적절한 값으로 바꿔 다음과 일치하도록 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-151">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="fe97f-152">특히 `<id>` 값은 nuget.org 전체에서 고유해야 합니다([패키지 만들기](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)에서 설명한 명명 규칙 참조).</span><span class="sxs-lookup"><span data-stu-id="fe97f-152">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="fe97f-153">또한 작성자 및 설명 태그도 업데이트해야 합니다. 그렇지 않으면 압축 단계에서 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-153">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="fe97f-154">패키지 버전에 `-alpha`, `-beta` 또는 `-rc` 접미사를 붙여 패키지를 시험판으로 표시할 수 있습니다. 시험판 버전에 대한 자세한 내용은 [시험판 버전](../create-packages/prerelease-packages.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fe97f-154">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="fe97f-155">참조 어셈블리 추가</span><span class="sxs-lookup"><span data-stu-id="fe97f-155">Add reference assemblies</span></span>

<span data-ttu-id="fe97f-156">플랫폼 특정 참조 어셈블리를 포함하려면 지원되는 플랫폼에 맞게 `LoggingLibrary.nuspec`의 `<files>` 요소에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-156">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> <span data-ttu-id="fe97f-157">DLL 및 XML 파일의 이름을 짧게 하려면, 지정된 프로젝트를 마우스 오른쪽 단추로 클릭하고 **라이브러리** 탭을 선택한 다음 어셈블리 이름을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-157">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="fe97f-158">종속성 추가</span><span class="sxs-lookup"><span data-stu-id="fe97f-158">Add dependencies</span></span>

<span data-ttu-id="fe97f-159">네이티브 구현에 대한 특정 종속성이 있는 경우 `<dependencies>` 요소와 함께 `<group>` 요소를 사용하여 해당 종속성을 지정합니다. 예를 들어 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-159">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

<span data-ttu-id="fe97f-160">예를 들어 다음은 iTextSharp를 UAP 대상에 대한 종속성으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-160">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="fe97f-161">최종 .nuspec</span><span class="sxs-lookup"><span data-stu-id="fe97f-161">Final .nuspec</span></span>

<span data-ttu-id="fe97f-162">최종 `.nuspec` 파일은 이제 다음과 같으며, YOUR_NAME을 적절한 값으로 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-162">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="fe97f-163">구성 요소 패키징</span><span class="sxs-lookup"><span data-stu-id="fe97f-163">Package the component</span></span>

<span data-ttu-id="fe97f-164">완료된 `.nuspec`에서 패키지에 포함되어야 하는 모든 파일을 참조하면 `pack` 명령을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-164">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="fe97f-165">그러면 `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-165">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="fe97f-166">[NuGet 패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)와 같은 도구에서 이 파일을 열고 모든 노드를 확장하면 다음과 같은 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-166">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![LoggingLibrary 패키지를 보여 주는 NuGet 패키지 탐색기](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="fe97f-168">`.nupkg` 파일은 확장명이 다른 ZIP 파일일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-168">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="fe97f-169">`.nupkg`를 `.zip`으로 변경하여 패키지 내용을 검사할 수도 있지만 패키지를 nuget.org에 업로드하려면 먼저 확장명을 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe97f-169">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="fe97f-170">다른 개발자가 패키지를 사용할 수 있게 하려면 [패키지 게시](../create-packages/publish-a-package.md)의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="fe97f-170">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="fe97f-171">관련 항목</span><span class="sxs-lookup"><span data-stu-id="fe97f-171">Related topics</span></span>

- [<span data-ttu-id="fe97f-172">.nuspec 참조</span><span class="sxs-lookup"><span data-stu-id="fe97f-172">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="fe97f-173">기호 패키지</span><span class="sxs-lookup"><span data-stu-id="fe97f-173">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="fe97f-174">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="fe97f-174">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="fe97f-175">여러 .NET Framework 버전 지원</span><span class="sxs-lookup"><span data-stu-id="fe97f-175">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="fe97f-176">패키지에 MSBuild props 및 targets 포함</span><span class="sxs-lookup"><span data-stu-id="fe97f-176">Including MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="fe97f-177">지역화된 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="fe97f-177">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)