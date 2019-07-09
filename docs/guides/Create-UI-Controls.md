---
title: NuGet에서 UI 컨트롤을 패키지하는 방법
description: Visual Studio 및 Blend 디자이너에 필요한 메타데이터 및 지원되는 파일을 포함하여 UWP 또는 WPF 컨트롤을 포함하는 NuGet 패키지를 만드는 방법입니다.
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: 522dbbb2a39eb1cb6f0d23f39a48158b07c9076d
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426849"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>NuGet 패키지인 UI 컨트롤 만들기

Visual Studio 2017부터 NuGet 패키지에서 제공하는 UWP 및 WPF 컨트롤에 추가된 기능을 활용할 수 있습니다. 이 가이드는 [ExtensionSDKasNuGetPackage 샘플](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)을 사용하여 UWP 컨트롤의 컨텍스트에서 이러한 기능을 설명합니다. 달리 언급하지 않는 한 WPF 컨트롤에도 동일한 내용이 적용됩니다.

## <a name="prerequisites"></a>전제 조건

1. Visual Studio 2017
1. [UWP 패키지를 만드는](create-uwp-packages.md) 방법 이해

## <a name="generate-library-layout"></a>라이브러리 레이아웃 생성

> [!Note]
> 이 내용은 UWP 컨트롤에만 적용됩니다.

`GenerateLibraryLayout` 속성을 설정하면 프로젝트 빌드 출력이 nuspec의 개별 파일 항목 없이, 패키지할 준비가 된 레이아웃에 생성됩니다.

프로젝트 속성에서 빌드 탭으로 이동하여 “라이브러리 레이아웃 생성” 확인란을 선택합니다. 그러면 프로젝트 파일이 수정되고 현재 선택된 빌드 구성 및 플랫폼에 대해 `GenerateLibraryLayout` 플래그가 true로 설정됩니다.

또는 프로젝트 파일을 편집하여 첫 번째 무조건 속성 그룹에 `<GenerateLibraryLayout>true</GenerateLibraryLayout>`을 추가합니다. 그러면 빌드 구성 및 플랫폼에 상관없이 속성이 적용됩니다.

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

도구 상자/자산 창에서 사용자 지정 아이콘을 표시하려면 이미지를 프로젝트 또는 "Namespace.ControlName.extension"이라는 해당 `design.dll` 프로젝트에 추가하고 빌드 작업을 "포함 리소스"로 설정합니다. 또한 연결된 `AssemblyInfo.cs`가 ProvideMetadata 특성(`[assembly: ProvideMetadata(typeof(RegisterMetadata))]`)을 지정하는지 확인해야 합니다. 이 [샘플](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20)을 참조합니다.

지원되는 형식은 `.png`, `.jpg`, `.jpeg`, `.gif` 및 `.bmp`입니다. 권장 형식은 16픽셀 x 16픽셀의 BMP24입니다.

![도구 상자 아이콘 샘플](https://raw.githubusercontent.com/NuGet/docs.microsoft.com-nuget/live/docs/guides/media/ColorPicker_16x16x24.bmp)

분홍색 배경은 런타임에 바뀝니다. 아이콘은 Visual Studio 테마를 변경하고 배경색이 예상되면 다시 그려집니다. 자세한 내용은 [Visual Studio용 이미지 및 아이콘](https://docs.microsoft.com/en-us/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio)을 참조하세요.

아래 예제에서 프로젝트에는 "ManagedPackage.MyCustomControl.png"라는 이미지 파일이 있습니다.

![프로젝트에서 사용자 지정 아이콘 설정](media/UWP-control-custom-icon.png)

> [!Note]
> 네이티브 컨트롤의 경우 `design.dll` 프로젝트에서 리소스로 아이콘을 삽입해야 합니다.

## <a name="support-specific-windows-platform-versions"></a>특정 Windows 플랫폼 버전 지원

UWP 패키지에는 앱을 설치할 수 있는 OS 버전의 상한 및 하한 경계를 정의하는 TargetPlatformVersion(TPV) 및 TargetPlatformMinVersion(TPMinV)이 있습니다. 나아가 TPV는 앱을 빌드할 SDK의 버전을 지정합니다. UWP 패키지를 작성할 때 이러한 속성을 고려하세요. 앱에 정의된 플랫폼 버전의 범위 밖에서 API를 사용하면 런타임 시 빌드에 실패하거나 앱이 실패합니다.

예를 들어 TPMinV 컨트롤 패키지를 Windows 10 Anniversary Edition(10.0, 빌드 14393)으로 설정했다고 가정해 보겠습니다. 따라서 패키지가 낮은 해당 범위와 일치하는 UWP 프로젝트에서만 사용되는지 확인합니다. 패키지를 UWP 프로젝트에서 사용할 수 있도록 허용하려면 다음 폴더 이름을 가진 컨트롤을 패키지해야 합니다.

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

NuGet은 사용하는 프로젝트의 TPMinV를 자동으로 확인하고 Windows 10 Anniversary Edition(10.0, 빌드 14393)보다 이전 버전인 경우 설치에 실패합니다.

WPF의 경우 .NET Framework v4.6.1 이상을 대상으로 하는 프로젝트에서 WPF 컨트롤 패키지를 사용한다고 가정합니다. 이를 적용하려면 다음 폴더 이름으로 컨트롤을 패키지해야 합니다.

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>디자인 타임 지원 추가

속성 검사자에서 컨트롤 속성이 표시되는 위치를 구성하려면 사용자 지정 표시기 등을 추가하고, `design.dll` 파일을 `lib\uap10.0.14393\Design` 폴더에 대상 플랫폼에 적합하도록 배치합니다. 또한 **[템플릿 편집 > 복사본 편집](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** 기능이 작동하도록 하려면 `<your_assembly_name>\Themes` 폴더에서 병합되는 `Generic.xaml` 및 리소스가 포함되어야 합니다(실제 어셈블리 이름 사용). (이 파일은 컨트롤의 런타임 동작에 아무런 영향을 주지 않습니다.) 따라서 폴더 구조는 다음과 같이 나타납니다.

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


WPF의 경우 .NET Framework v4.6.1 이상을 대상으로 하는 프로젝트에서 WPF 컨트롤 패키지를 사용하는 예를 계속합니다.

    \lib
      \net461
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

> [!Note]
> 이 내용은 UWP 컨트롤에만 적용됩니다.

## <a name="see-also"></a>참고 항목

- [UWP 패키지 만들기](create-uwp-packages.md)
- [ExtensionSDKasNuGetPackage 샘플](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
