---
title: "NuGet에서 UWP 컨트롤을 패키지하는 방법 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 3/21/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 1f9de20a-f394-4cf2-8e40-ba0f4239cd5e
description: "Visual Studio 및 Blend 디자이너에 필요한 메타데이터 및 지원되는 파일을 포함하여 UWP 컨트롤을 포함하는 NuGet 패키지를 만드는 방법입니다."
keywords: "NuGet UWP 컨트롤, Visual Studio XAML 디자이너, Blend 디자이너, 컨트롤 사용자 지정"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f51dbabd406199752e4f9d612b498f59ffb54021
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="creating-uwp-controls-as-nuget-packages"></a><span data-ttu-id="7da61-104">NuGet 패키지인 UWP 컨트롤 만들기</span><span class="sxs-lookup"><span data-stu-id="7da61-104">Creating UWP controls as NuGet packages</span></span>

<span data-ttu-id="7da61-105">Visual Studio 2017에서 NuGet 패키지에서 제공하는 UWP 컨트롤에 추가된 기능을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-105">With Visual Studio 2017, you can take advantage of added capabilities for UWP controls that you deliver in NuGet packages.</span></span> <span data-ttu-id="7da61-106">이 가이드는 [ExtensionSDKasNuGetPackage 샘플](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)을 사용하여 이러한 기능을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-106">This guide walks you through these capabilities using the [ExtensionSDKasNuGetPackage sample](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage).</span></span> 

## <a name="pre-requisites"></a><span data-ttu-id="7da61-107">필수 구성 요소:</span><span class="sxs-lookup"><span data-stu-id="7da61-107">Pre-requisites:</span></span>

1.  <span data-ttu-id="7da61-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="7da61-108">Visual Studio 2017</span></span>
1.  <span data-ttu-id="7da61-109">[UWP 패키지를 만드는](create-uwp-packages.md) 방법 이해</span><span class="sxs-lookup"><span data-stu-id="7da61-109">Understanding of how to [Create UWP Packages](create-uwp-packages.md)</span></span>

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a><span data-ttu-id="7da61-110">XAML 컨트롤에 도구 상자/자산 창 지원 추가</span><span class="sxs-lookup"><span data-stu-id="7da61-110">Add toolbox/assets pane support for XAML controls</span></span>

<span data-ttu-id="7da61-111">Visual Studio 및 Blend의 자산 창에 있는 XAML 디자이너의 도구 상자에 XAML 컨트롤을 표시하려면 패키지 프로젝트의 `tools` 폴더 루트에 `VisualStudioToolsManifest.xml` 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-111">To have a XAML control appear in the XAML designer’s toolbox in Visual Studio and the Assets pane of Blend, create a `VisualStudioToolsManifest.xml` file in the root of the `tools` folder of your package project.</span></span> <span data-ttu-id="7da61-112">컨트롤을 도구 상자 또는 자산 창에서 표시하지 않아도 되는 경우 이 파일이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-112">This file is not required if you don’t need the control to appear in the toolbox or Assets pane.</span></span>

```
\build
\lib
\tools
    \VisualStudioToolsManifest.xml
```    

<span data-ttu-id="7da61-113">파일의 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-113">The structure of the file is as follows:</span></span>

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

<span data-ttu-id="7da61-114">여기서</span><span class="sxs-lookup"><span data-stu-id="7da61-114">where:</span></span>

- <span data-ttu-id="7da61-115">*your_package_file*: `ManagedPackage.winmd`와 같은 컨트롤 파일의 이름입니다("ManagedPackage"는 이 예제에 사용되고 다른 의미가 없음).</span><span class="sxs-lookup"><span data-stu-id="7da61-115">*your_package_file*: the name of your control file, such as `ManagedPackage.winmd` ("ManagedPackage" is an arbitrary named used for this example and has no other meaning).</span></span>
- <span data-ttu-id="7da61-116">*vs_category*: Visual Studio 디자이너의 도구 상자에서 컨트롤이 표시되어야 하는 그룹의 레이블입니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-116">*vs_category*: The label for the group in which the control should appear in the Visual Studio designer’s toolbox.</span></span> <span data-ttu-id="7da61-117">`VSCategory`는 컨트롤을 도구 상자에 표시하기 위해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-117">A `VSCategory` is necessary for the control to appear in the toolbox.</span></span>
- <span data-ttu-id="7da61-118">*blend_category*: Blend 디자이너의 자산 창에서 컨트롤이 표시되어야 하는 그룹의 레이블입니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-118">*blend_category*: The label for the group in which the control should appear in the Blend designer’s Assets pane.</span></span> <span data-ttu-id="7da61-119">`BlendCategory`는 컨트롤을 자산에 표시하기 위해 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-119">A `BlendCategory` is necessary for the control to appear in Assets.</span></span>
- <span data-ttu-id="7da61-120">*type_full_name_n*: `ManagedPackage.MyCustomControl`과 같은 네임스페이스를 포함하여 각 컨트롤의 정규화된 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-120">*type_full_name_n*: The fully-qualified name for each control, including the namespace, such as `ManagedPackage.MyCustomControl`.</span></span> <span data-ttu-id="7da61-121">점 양식은 관리 및 네이티브 형식에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-121">Note that the dot format is used for both managed and native types.</span></span>

<span data-ttu-id="7da61-122">고급 시나리오에서 단일 패키지에 여러 컨트롤 어셈블리가 포함되는 경우 `<FileList>` 내에 여러 `<File>` 요소가 포함될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-122">In more advanced scenarios, you can also include multiple `<File>` elements within `<FileList>` when a single package contains multiple control assemblies.</span></span> <span data-ttu-id="7da61-123">컨트롤을 별도 범주로 구성하려는 경우 단일 `<File>` 내에 여러 `<ToolboxItems>` 노드가 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-123">You can also have multiple `<ToolboxItems>` nodes within a single `<File>` if you want to organize your controls into separate categories.</span></span>

<span data-ttu-id="7da61-124">다음 예제에서 `ManagedPackage.winmd`에서 구현된 컨트롤은 "관리 패키지"라는 그룹의 Visual Studio 및 Blend에 표시되고 "MyCustomControl"은 해당 그룹에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-124">In the following example, the control implemented in `ManagedPackage.winmd` will appear in Visual Studio and Blend in a group named “Managed Package”, and “MyCustomControl” will appear in that group.</span></span> <span data-ttu-id="7da61-125">이러한 이름은 모두 임의로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-125">All these names are arbitrary.</span></span>

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Visual Studio에서 표시되는 예제 컨트롤](media/UWP-control-vs-toolbox.png)

![Blend에서 표시되는 예제 컨트롤](media/UWP-control-blend-assets.png)

> [!Note]
> <span data-ttu-id="7da61-128">도구 상자/자산 창에서 확인하려는 모든 컨트롤을 명시적으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-128">You must explicitly specify every control that you would like to see in the toolbox/assets pane.</span></span> <span data-ttu-id="7da61-129">`Namespace.ControlName` 형식으로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-129">Ensure you specify them in the format `Namespace.ControlName`.</span></span>

## <a name="add-custom-icons-to-your-controls"></a><span data-ttu-id="7da61-130">컨트롤에 사용자 지정 아이콘 추가</span><span class="sxs-lookup"><span data-stu-id="7da61-130">Add custom icons to your controls</span></span>

<span data-ttu-id="7da61-131">도구 상자/자산 창에서 사용자 지정 아이콘을 표시하려면 이미지를 프로젝트 또는 "Namespace.ControlName.extension"이라는 해당 `design.dll` 프로젝트에 추가하고 빌드 작업을 "포함 리소스"로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-131">To display a custom icon in the toolbox/assets pane, add an image to your project or the corresponding `design.dll` project with the name “Namespace.ControlName.extension” and set the build action to “Embedded Resource”.</span></span> <span data-ttu-id="7da61-132">지원되는 형식은 `.png`, `.jpg`, `.jpeg`, `.gif` 및 `.bmp`입니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-132">Supported formats are `.png`, `.jpg`, `.jpeg`, `.gif`, and `.bmp`.</span></span> <span data-ttu-id="7da61-133">권장된 이미지 크기는 64x64픽셀입니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-133">The recommended image size is 64 pixels by 64 pixels.</span></span>

<span data-ttu-id="7da61-134">아래 예제에서 프로젝트에는 "ManagedPackage.MyCustomControl.png"라는 이미지 파일이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-134">In the example below, the project contains an image file named “ManagedPackage.MyCustomControl.png”.</span></span>

![프로젝트에서 사용자 지정 아이콘 설정](media/UWP-control-custom-icon.png)

> [!Note]
> <span data-ttu-id="7da61-136">네이티브 컨트롤의 경우 `design.dll` 프로젝트에서 리소스로 아이콘을 삽입해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-136">For native controls, you must put the icon as a resource in the `design.dll` project.</span></span>

## <a name="support-specific-windows-platform-versions"></a><span data-ttu-id="7da61-137">특정 Windows 플랫폼 버전 지원</span><span class="sxs-lookup"><span data-stu-id="7da61-137">Support specific Windows platform versions</span></span>

<span data-ttu-id="7da61-138">UWP 패키지에는 앱을 설치할 수 있는 OS 버전의 상한 및 하한 경계를 정의하는 TargetPlatformVersion(TPV) 및 TargetPlatformMinVersion(TPMinV)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-138">UWP packages have a TargetPlatformVersion (TPV) and TargetPlatformMinVersion (TPMinV) that define the upper and lower bounds of the OS version where the app can be installed.</span></span> <span data-ttu-id="7da61-139">나아가 TPV는 앱을 빌드할 SDK의 버전을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-139">TPV further specifies the version of the SDK against which the app is built.</span></span> <span data-ttu-id="7da61-140">UWP 패키지를 작성할 때 이러한 속성을 고려하세요. 앱에 정의된 플랫폼 버전의 범위 밖에서 API를 사용하면 런타임 시 빌드에 실패하거나 앱이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-140">Be mindful of these properties when authoring a UWP package: using APIs outside the bounds of the platform versions defined in the app will cause either the build to fail or the app to fail at runtime.</span></span>

<span data-ttu-id="7da61-141">예를 들어 TPMinV 컨트롤 패키지를 Windows 10 Anniversary Edition(10.0;빌드 14393)으로 설정했다고 가정해 보겠습니다. 따라서 패키지가 낮은 해당 범위와 일치하는 UWP 프로젝트에서만 사용되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-141">For example, let’s say you’ve set the TPMinV for you controls package to Windows 10 Anniversary Edition (10.0; Build 14393), so you want to ensure that the package is consumed only by UWP projects that match that lower bound.</span></span> <span data-ttu-id="7da61-142">패키지를 `project.json` 기반 UWP 프로젝트에서 사용할 수 있도록 허용하려면 다음 폴더 이름을 가진 컨트롤을 패키지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-142">To allow your package to be consumed by `project.json` based UWP projects, you must package your controls with the following folder names:</span></span>

```
\lib\uap10.0\*
\ref\uap10.0\*
```

<span data-ttu-id="7da61-143">적절한 TPMinV 검사를 적용하려면 [MSBuild 대상 파일](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets)을 만들고 빌드 폴더에서 패키지합니다("your_assembly_name"을 특정 어셈블리의 이름으로 바꿈).</span><span class="sxs-lookup"><span data-stu-id="7da61-143">To enforce the appropriate TPMinV check, create an [MSBuild targets file](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets) and package it under the build folder (replacing "your_assembly_name" with the name of your specific assembly):</span></span>

```
\build
    \uap10.0
        your_assembly_name.targets
\lib
\tools
```

<span data-ttu-id="7da61-144">대상 파일이 표시되는 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-144">Here is an example of what the targets file should look like:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="Build;ReBuild" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a><span data-ttu-id="7da61-145">디자인 타임 지원 추가</span><span class="sxs-lookup"><span data-stu-id="7da61-145">Add design-time support</span></span>

<span data-ttu-id="7da61-146">속성 검사자에서 컨트롤 속성이 표시되는 위치를 구성하려면 사용자 지정 표시기 등을 추가하고, `design.dll` 파일을 `lib\<platform>\Design` 폴더에 대상 플랫폼에 적합하도록 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-146">To configure where the control properties show up in the property inspector, add custom adorners, etc., place your `design.dll` file inside the `lib\<platform>\Design` folder as appropriate to the target platform.</span></span> <span data-ttu-id="7da61-147">또한 **[템플릿 편집 > 복사본 편집](https://docs.microsoft.com/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** 기능이 작동하도록 하려면 `<AssemblyName>\Themes` 폴더에서 병합되는 `Generic.xaml` 및 리소스가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-147">Also, to ensure that the **[Edit Template > Edit a Copy](https://docs.microsoft.com/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** feature works, you must include the `Generic.xaml` and any resource dictionaries that it merges in the `<AssemblyName>\Themes` folder.</span></span> <span data-ttu-id="7da61-148">(이 파일은 컨트롤의 런타임 동작에 아무런 영향을 주지 않습니다.)</span><span class="sxs-lookup"><span data-stu-id="7da61-148">(This file has no impact on the runtime behavior of a control.)</span></span>


```
\build
\lib
    \uap10.0.14393.0
        \Design
            \MyControl.design.dll
        \your_assembly_name
            \Themes     
                Generic.xaml
\tools
```

> [!Note]
> <span data-ttu-id="7da61-149">기본적으로 컨트롤 속성은 속성 검사자의 기타 범주에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-149">By default, control properties will show up under the Miscellaneous category in the property inspector.</span></span>


## <a name="use-strings-and-resources"></a><span data-ttu-id="7da61-150">문자열 및 리소스 사용</span><span class="sxs-lookup"><span data-stu-id="7da61-150">Use strings and resources</span></span>

<span data-ttu-id="7da61-151">패키지에 문자열 리소스(`.resw`)를 포함할 수 있으며 해당 리소스를 컨트롤 또는 사용 중인 UWP 프로젝트에서 사용할 수 있습니다. `.resw` 파일의 **빌드 작업** 속성을 **PRIResource**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-151">You can embed string resources (`.resw`) in your package that can be used by your control or the consuming UWP project, set the **Build Action** property of the `.resw` file to **PRIResource**.</span></span>

<span data-ttu-id="7da61-152">예를 들어 ExtensionSDKasNuGetPackage 샘플에서 [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7da61-152">For an example, refer to [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) in the ExtensionSDKasNuGetPackage sample.</span></span>

## <a name="package-content-such-as-images"></a><span data-ttu-id="7da61-153">이미지 등 패키지 콘텐츠</span><span class="sxs-lookup"><span data-stu-id="7da61-153">Package content such as images</span></span>

<span data-ttu-id="7da61-154">컨트롤 또는 사용 중인 UWP 프로젝트에서 사용할 수 있는 이미지와 같은 콘텐츠를 패키지하려면</span><span class="sxs-lookup"><span data-stu-id="7da61-154">To package content such as images that can be used by your control or the consuming UWP project.</span></span> <span data-ttu-id="7da61-155">다음과 같이 해당 파일을 `lib\uap10.0.14393.0` 폴더에 추가합니다("your_assembly_name"은 특정 컨트롤과 일치해야 함).</span><span class="sxs-lookup"><span data-stu-id="7da61-155">add those files `lib\uap10.0.14393.0` folder as follows ("your_assembly_name" should again match your particular control):</span></span>

```
\build
\lib
    \uap10.0.14393.0
        \Design
        \your_assembly_name
\contosoSampleImage.jpg
\tools
```

<span data-ttu-id="7da61-156">[MSBuild 대상 파일](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets)을 작성하여 자산이 사용 중인 프로젝트의 출력 폴더에 복사되었는지 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7da61-156">You may also author an[MSBuild targets file](https://docs.microsoft.com/visualstudio/msbuild/msbuild-targets) to ensure the asset is copied to the consuming project’s output folder:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0.14393.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a><span data-ttu-id="7da61-157">참고 항목</span><span class="sxs-lookup"><span data-stu-id="7da61-157">See also</span></span>

- [<span data-ttu-id="7da61-158">UWP 패키지 만들기</span><span class="sxs-lookup"><span data-stu-id="7da61-158">Create UWP Packages</span></span>](create-uwp-packages.md)
- [<span data-ttu-id="7da61-159">ExtensionSDKasNuGetPackage 샘플</span><span class="sxs-lookup"><span data-stu-id="7da61-159">ExtensionSDKasNuGetPackage sample</span></span>](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
