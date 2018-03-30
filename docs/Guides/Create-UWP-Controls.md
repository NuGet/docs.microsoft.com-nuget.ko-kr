---
title: NuGet에서 UWP 컨트롤을 패키지하는 방법 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/14/2018
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: Visual Studio 및 Blend 디자이너에 필요한 메타데이터 및 지원되는 파일을 포함하여 UWP 컨트롤을 포함하는 NuGet 패키지를 만드는 방법입니다.
keywords: NuGet UWP 컨트롤, Visual Studio XAML 디자이너, Blend 디자이너, 컨트롤 사용자 지정
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f024fd1823c77d57d30c4f841bf03494194c8339
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a>NuGet 패키지인 UWP 컨트롤 만들기

Visual Studio 2017에서 NuGet 패키지에서 제공하는 UWP 컨트롤에 추가된 기능을 활용할 수 있습니다. 이 가이드는 [ExtensionSDKasNuGetPackage 샘플](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)을 사용하여 이러한 기능을 설명합니다. 

## <a name="prerequisites"></a>전제 조건

1. Visual Studio 2017
1. [UWP 패키지를 만드는](create-uwp-packages.md) 방법 이해

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>XAML 컨트롤에 도구 상자/자산 창 지원 추가

Visual Studio 및 Blend의 자산 창에 있는 XAML 디자이너의 도구 상자에 XAML 컨트롤을 표시하려면 패키지 프로젝트의 `tools` 폴더 루트에 `VisualStudioToolsManifest.xml` 파일을 만듭니다. 컨트롤을 도구 상자 또는 자산 창에서 표시하지 않아도 되는 경우 이 파일이 필요하지 않습니다.

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

파일의 구조는 다음과 같습니다.

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

다음은 각 문자에 대한 설명입니다.

- *your_package_file*: `ManagedPackage.winmd`와 같은 컨트롤 파일의 이름입니다("ManagedPackage"는 이 예제에 사용되고 다른 의미가 없음).
- *vs_category*: Visual Studio 디자이너의 도구 상자에서 컨트롤이 표시되어야 하는 그룹의 레이블입니다. `VSCategory`는 컨트롤을 도구 상자에 표시하기 위해 필요합니다.
- *blend_category*: Blend 디자이너의 자산 창에서 컨트롤이 표시되어야 하는 그룹의 레이블입니다. `BlendCategory`는 컨트롤을 자산에 표시하기 위해 필요합니다.
- *type_full_name_n*: `ManagedPackage.MyCustomControl`과 같은 네임스페이스를 포함하여 각 컨트롤의 정규화된 이름입니다. 점 양식은 관리 및 네이티브 형식에 사용됩니다.

고급 시나리오에서 단일 패키지에 여러 컨트롤 어셈블리가 포함되는 경우 `<FileList>` 내에 여러 `<File>` 요소가 포함될 수도 있습니다. 컨트롤을 별도 범주로 구성하려는 경우 단일 `<File>` 내에 여러 `<ToolboxItems>` 노드가 있을 수도 있습니다.

다음 예제에서 `ManagedPackage.winmd`에서 구현된 컨트롤은 "관리 패키지"라는 그룹의 Visual Studio 및 Blend에 표시되고 "MyCustomControl"은 해당 그룹에 표시됩니다. 이러한 이름은 모두 임의로 지정됩니다.

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
> 도구 상자/자산 창에서 확인하려는 모든 컨트롤을 명시적으로 지정해야 합니다. `Namespace.ControlName` 형식으로 지정해야 합니다.

## <a name="add-custom-icons-to-your-controls"></a>컨트롤에 사용자 지정 아이콘 추가

도구 상자/자산 창에서 사용자 지정 아이콘을 표시하려면 이미지를 프로젝트 또는 "Namespace.ControlName.extension"이라는 해당 `design.dll` 프로젝트에 추가하고 빌드 작업을 "포함 리소스"로 설정합니다. 지원되는 형식은 `.png`, `.jpg`, `.jpeg`, `.gif` 및 `.bmp`입니다. 권장된 이미지 크기는 64x64픽셀입니다.

아래 예제에서 프로젝트에는 "ManagedPackage.MyCustomControl.png"라는 이미지 파일이 있습니다.

![프로젝트에서 사용자 지정 아이콘 설정](media/UWP-control-custom-icon.png)

> [!Note]
> 네이티브 컨트롤의 경우 `design.dll` 프로젝트에서 리소스로 아이콘을 삽입해야 합니다.

## <a name="support-specific-windows-platform-versions"></a>특정 Windows 플랫폼 버전 지원

UWP 패키지에는 앱을 설치할 수 있는 OS 버전의 상한 및 하한 경계를 정의하는 TargetPlatformVersion(TPV) 및 TargetPlatformMinVersion(TPMinV)이 있습니다. 나아가 TPV는 앱을 빌드할 SDK의 버전을 지정합니다. UWP 패키지를 작성할 때 이러한 속성을 고려하세요. 앱에 정의된 플랫폼 버전의 범위 밖에서 API를 사용하면 런타임 시 빌드에 실패하거나 앱이 실패합니다.

예를 들어 TPMinV 컨트롤 패키지를 Windows 10 Anniversary Edition(10.0;빌드 14393)으로 설정했다고 가정해 보겠습니다. 따라서 패키지가 낮은 해당 범위와 일치하는 UWP 프로젝트에서만 사용되는지 확인합니다. 패키지를 UWP 프로젝트에서 사용할 수 있도록 허용하려면 다음 폴더 이름을 가진 컨트롤을 패키지해야 합니다.

    \lib\uap10.0\*
    \ref\uap10.0\*

적절한 TPMinV 검사를 적용하려면 [MSBuild 대상 파일](/visualstudio/msbuild/msbuild-targets)을 만들고 특정 어셈블리의 이름을 사용하여 `build\uap10.0" folder as `<your_assembly_name>.targets`, replacing `<your_assembly_name>` 아래에 패키징합니다.

대상 파일이 표시되는 예는 다음과 같습니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="ResolveAssemblyReferences" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a>디자인 타임 지원 추가

속성 검사자에서 컨트롤 속성이 표시되는 위치를 구성하려면 사용자 지정 표시기 등을 추가하고, `design.dll` 파일을 `lib\uap10.0\Design` 폴더에 대상 플랫폼에 적합하도록 배치합니다. 또한 **[템플릿 편집 > 복사본 편집](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** 기능이 작동하도록 하려면 `<your_assembly_name>\Themes` 폴더에서 병합되는 `Generic.xaml` 및 리소스가 포함되어야 합니다(실제 어셈블리 이름 사용). (이 파일은 컨트롤의 런타임 동작에 아무런 영향을 주지 않습니다.) 따라서 폴더 구조는 다음과 같이 나타납니다.

    \lib
      \uap10.0
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> 기본적으로 컨트롤 속성은 속성 검사자의 기타 범주에 표시됩니다.

## <a name="use-strings-and-resources"></a>문자열 및 리소스 사용

패키지에 문자열 리소스(`.resw`)를 포함할 수 있으며 해당 리소스를 컨트롤 또는 사용 중인 UWP 프로젝트에서 사용할 수 있습니다. `.resw` 파일의 **빌드 작업** 속성을 **PRIResource**로 설정합니다.

예를 들어 ExtensionSDKasNuGetPackage 샘플에서 [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs)를 참조하세요.

## <a name="package-content-such-as-images"></a>이미지 등 패키지 콘텐츠

컨트롤 또는 사용 중인 UWP 프로젝트에서 사용할 수 있는 이미지와 같은 콘텐츠를 패키지하려면 이러한 파일을 `lib\uap10.0` 폴더에 보관합니다.

[MSBuild 대상 파일](/visualstudio/msbuild/msbuild-targets)을 작성하여 자산이 사용 중인 프로젝트의 출력 폴더에 복사되었는지 확인할 수도 있습니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a>참고 항목

- [UWP 패키지 만들기](create-uwp-packages.md)
- [ExtensionSDKasNuGetPackage 샘플](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
