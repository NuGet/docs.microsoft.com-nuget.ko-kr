---
title: 유니버설 Windows 플랫폼용 NuGet 패키지 만들기
description: C#에서 유니버설 Windows 플랫폼용 Windows 런타임 구성 요소를 사용하여 NuGet 패키지를 만드는 엔드투엔드 연습입니다.
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231754"
---
# <a name="create-uwp-packages-c"></a><span data-ttu-id="d361f-103">UWP 패키지 만들기(C#)</span><span class="sxs-lookup"><span data-stu-id="d361f-103">Create UWP packages (C#)</span></span>

<span data-ttu-id="d361f-104">[UWP(유니버설 Windows 플랫폼)](/windows/uwp)은 Windows 10을 실행하는 모든 디바이스에 공통된 응용 프로그램 플랫폼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-104">The [Universal Windows Platform (UWP)](/windows/uwp) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="d361f-105">이 모델 내에서 UWP 응용 프로그램은 모든 디바이스에 공통적인 WinRT API 및 응용 프로그램이 실행되는 디바이스 제품군에만 적용되는 API(Win32 및 .NET 포함)를 모두 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="d361f-106">이 연습에서는 관리형 및 네이티브 프로젝트에서 모두 사용할 수 있는 C# UWP 구성 요소(XAML 컨트롤 포함)를 사용하여 NuGet 패키지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-106">In this walkthrough you create a NuGet package with a C# UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d361f-107">사전 요구 사항</span><span class="sxs-lookup"><span data-stu-id="d361f-107">Prerequisites</span></span>

1. <span data-ttu-id="d361f-108">Visual Studio 2019.</span><span class="sxs-lookup"><span data-stu-id="d361f-108">Visual Studio 2019.</span></span> <span data-ttu-id="d361f-109">[visualstudio.com](https://www.visualstudio.com/)에서 추가 비용 없이 2019 Community 버전을 설치합니다. Professional 및 Enterprise 버전도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-109">Install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="d361f-110">NuGet CLI -</span><span class="sxs-lookup"><span data-stu-id="d361f-110">NuGet CLI.</span></span> <span data-ttu-id="d361f-111">[nuget.org/downloads](https://nuget.org/downloads)에서 최신 버전의 `nuget.exe`를 다운로드하여 선택한 위치에 저장합니다(다운로드는 바로 `.exe`임).</span><span class="sxs-lookup"><span data-stu-id="d361f-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="d361f-112">그런 다음 해당 위치를 PATH 환경 변수에 추가합니다(아직 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="d361f-112">Then add that location to your PATH environment variable if it isn't already.</span></span> <span data-ttu-id="d361f-113">[자세한 내용](/nuget/reference/nuget-exe-cli-reference#windows).</span><span class="sxs-lookup"><span data-stu-id="d361f-113">[More details](/nuget/reference/nuget-exe-cli-reference#windows).</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="d361f-114">UWP Windows 런타임 구성 요소 만들기</span><span class="sxs-lookup"><span data-stu-id="d361f-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="d361f-115">Visual Studio에서 **파일 > 새로 만들기 > 프로젝트**를 차례로 선택하고 “uwp c#”을 검색한 다음, **Windows 런타임 구성 요소(유니버설 Windows)** 템플릿을 선택합니다. [다음]을 클릭하고 이름을 ImageEnhancer로 변경한 다음, [만들기]를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-115">In Visual Studio, choose **File > New > Project**, search for "uwp c#", select the **Windows Runtime Component (Universal Windows)** template, click next, change the name to ImageEnhancer, and click Create.</span></span> <span data-ttu-id="d361f-116">메시지가 표시되면 대상 버전 및 최소 버전에 대한 기본값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![새 UWP Windows 런타임 구성 요소 프로젝트 만들기](media/UWP-NewProject-CS.png)

1. <span data-ttu-id="d361f-118">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가 > 새 항목**을 차례로 선택한 다음, **템플릿 기반 컨트롤**을 선택합니다. 이름을 AwesomeImageControl.cs로 변경하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-118">Right click the project in Solution Explorer, select **Add > New Item**, select **Templated Control**, change the name to AwesomeImageControl.cs, and click **Add**:</span></span>

    ![프로젝트에 새 XAML 템플릿 기반 컨트롤 항목 추가](media/UWP-NewXAMLControl-CS.png)

1. <span data-ttu-id="d361f-120">[솔루션 탐색기]에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="d361f-121">[속성] 페이지에서 **빌드** 탭을 선택하고 **XML 문서 파일**을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-121">In the Properties page, choose **Build** tab and enable **XML Documentation File**:</span></span>

    ![XML 문서 파일 생성을 Yes로 설정](media/UWP-GenerateXMLDocFiles-CS.png)

1. <span data-ttu-id="d361f-123">이제 *솔루션*을 마우스 오른쪽 단추로 클릭하고 **일괄 빌드**를 선택한 다음, 아래 그림과 같이 대화 상자에서 5개의 빌드 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-123">Right click the *solution* now, select **Batch Build**, check the five build boxes in the dialog as shown below.</span></span> <span data-ttu-id="d361f-124">이렇게 하면 빌드를 수행할 때 Windows에서 지원하는 각 대상 시스템에 대한 전체 아티팩트 집합이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![일괄 빌드](media/UWP-BatchBuild-CS.png)

1. <span data-ttu-id="d361f-126">[일괄 빌드] 대화 상자에서 **빌드**를 클릭하여 프로젝트를 확인하고, NuGet 패키지에 필요한 출력 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="d361f-127">이 연습에서는 패키지에 대한 [디버그] 아티팩트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="d361f-128">디버그가 아닌 패키지의 경우 [일괄 빌드] 대화 상자에서 [릴리스] 옵션을 대신 선택하고 다음 단계에서 나오는 결과 [Release] 폴더를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d361f-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="d361f-129">.nuspec 파일 만들기 및 업데이트</span><span class="sxs-lookup"><span data-stu-id="d361f-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="d361f-130">초기 `.nuspec` 파일을 만들려면 아래의 세 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="d361f-131">다음에 나오는 섹션에서 필요한 다른 업데이트를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="d361f-132">명령 프롬프트를 열고 `ImageEnhancer.csproj`가 포함된 폴더(솔루션 파일이 있는 폴더의 하위 폴더)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.csproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="d361f-133">[`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) 명령을 실행하여 `ImageEnhancer.nuspec`(`.csroj` 파일의 이름에서 가져온 파일 이름)를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-133">Run the [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.csroj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="d361f-134">편집기에서 `ImageEnhancer.nuspec`을 열고 YOUR_NAME을 적절한 값으로 바꿔 다음과 일치하도록 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="d361f-135">$PropertyName$ 값을 그대로 두지 마세요.</span><span class="sxs-lookup"><span data-stu-id="d361f-135">Do not leave any of the $propertyName$ values.</span></span> <span data-ttu-id="d361f-136">특히 `<id>` 값은 nuget.org 전체에서 고유해야 합니다([패키지 만들기](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)에서 설명한 명명 규칙 참조).</span><span class="sxs-lookup"><span data-stu-id="d361f-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="d361f-137">또한 작성자 및 설명 태그도 업데이트해야 합니다. 그렇지 않으면 압축 단계에서 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2020</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="d361f-138">공용으로 빌드된 패키지의 경우 `<tags>` 요소에 특히 주의하세요. 이러한 태그는 다른 사람들이 패키지를 찾고 그 기능을 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="d361f-139">패키지에 Windows 메타데이터 추가</span><span class="sxs-lookup"><span data-stu-id="d361f-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="d361f-140">Windows 런타임 구성 요소에는 공개적으로 사용할 수 있는 모든 형식을 설명하는 메타데이터가 필요하며, 이를 통해 다른 앱과 라이브러리에서 해당 구성 요소를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="d361f-141">이 메타데이터는 프로젝트를 컴파일할 때 만들어지며 NuGet 패키지에 포함되어야 하는 .winmd 파일에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="d361f-142">또한 IntelliSense 데이터가 있는 XML 파일도 동시에 빌드되므로 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="d361f-143">다음 `<files>` 노드를 `.nuspec` 파일에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="d361f-144">XAML 콘텐츠 추가</span><span class="sxs-lookup"><span data-stu-id="d361f-144">Adding XAML content</span></span>

<span data-ttu-id="d361f-145">구성 요소에 XAML 컨트롤을 포함하려면 프로젝트 템플릿으로 생성되는 컨트롤에 대한 기본 템플릿이 있는 XAML 파일을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="d361f-146">이는 `<files>` 섹션에도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-146">This also goes in the `<files>` section:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="d361f-147">네이티브 구현 라이브러리 추가</span><span class="sxs-lookup"><span data-stu-id="d361f-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="d361f-148">구성 요소 내에서 ImageEnhancer 형식의 핵심 논리는 각 대상 런타임(ARM, ARM64, x86 및 x64)에 대해 생성되는 다양한 `ImageEnhancer.winmd` 어셈블리에 포함된 네이티브 코드에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.winmd` assemblies that are generated for each target runtime (ARM, ARM64, x86, and x64).</span></span> <span data-ttu-id="d361f-149">패키지에 이러한 어셈블리를 포함하려면 다음과 같이 `<files>` 섹션에서 관련된 .pri 리소스 파일과 함께 이를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="d361f-150">최종 .nuspec</span><span class="sxs-lookup"><span data-stu-id="d361f-150">Final .nuspec</span></span>

<span data-ttu-id="d361f-151">최종 `.nuspec` 파일은 이제 다음과 같으며, YOUR_NAME을 적절한 값으로 바꾸어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-151">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="d361f-152">구성 요소 패키징</span><span class="sxs-lookup"><span data-stu-id="d361f-152">Package the component</span></span>

<span data-ttu-id="d361f-153">완료된 `.nuspec`에서 패키지에 포함되어야 하는 모든 파일을 참조하면 [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) 명령을 실행할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-153">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="d361f-154">이 명령은 `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-154">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="d361f-155">[NuGet 패키지 탐색기](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)와 같은 도구에서 이 파일을 열고 모든 노드를 확장하면 다음과 같은 내용이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-155">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![ImageEnhancer 패키지를 보여 주는 NuGet 패키지 탐색기](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="d361f-157">`.nupkg` 파일은 확장명이 다른 ZIP 파일일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-157">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="d361f-158">`.nupkg`를 `.zip`으로 변경하여 패키지 내용을 검사할 수도 있지만 패키지를 nuget.org에 업로드하려면 먼저 확장명을 복원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d361f-158">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="d361f-159">다른 개발자가 패키지를 사용할 수 있게 하려면 [패키지 게시](../nuget-org/publish-a-package.md)의 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="d361f-159">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="d361f-160">관련 항목</span><span class="sxs-lookup"><span data-stu-id="d361f-160">Related topics</span></span>

- [<span data-ttu-id="d361f-161">.nuspec 참조</span><span class="sxs-lookup"><span data-stu-id="d361f-161">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="d361f-162">기호 패키지</span><span class="sxs-lookup"><span data-stu-id="d361f-162">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="d361f-163">패키지 버전 관리</span><span class="sxs-lookup"><span data-stu-id="d361f-163">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="d361f-164">여러 .NET Framework 버전 지원</span><span class="sxs-lookup"><span data-stu-id="d361f-164">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="d361f-165">패키지에 MSBuild props 및 targets 포함</span><span class="sxs-lookup"><span data-stu-id="d361f-165">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="d361f-166">지역화된 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="d361f-166">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
