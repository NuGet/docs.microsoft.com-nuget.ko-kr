---
title: Visual Studio에서 NuGet 패키지 설치 및 관리
description: NuGet 패키지 작업을 위해 Visual Studio에서 NuGet 패키지 관리자 UI를 사용하는 방법에 대한 지침입니다.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 3adceac8c725d9ea1610aea090753c9c1d8bc818
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428422"
---
# <a name="install-and-manage-packages-in-visual-studio-using-the-nuget-package-manager"></a>Visual Studio에서 NuGet 패키지 관리자를 사용하여 패키지 설치 및 관리

Windows의 Visual Studio의 NuGet 패키지 관리자 UI를 사용하여 프로젝트 및 솔루션에서 NuGet 패키지를 쉽게 설치, 제거 및 업데이트할 수 있습니다. Mac용 Visual Studio 환경의 경우 [프로젝트에 NuGet 패키지 포함](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)을 참조하세요. 패키지 관리자 UI는 Visual Studio Code에 포함되어 있지 않습니다.

> [!NOTE]
> Visual Studio 2015에서 NuGet 패키지 관리자가 누락된 경우 **도구 > 확장 및 업데이트...** 를 선택하고 *NuGet 패키지 관리자* 확장을 검색합니다. Visual Studio에서 확장 설치 관리자를 사용할 수 없는 경우 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)에서 직접 확장을 다운로드합니다.
>
> Visual Studio 2017부터 NuGet 및 NuGet 패키지 관리자는 .NET 관련 워크로드와 함께 자동으로 설치됩니다. Visual Studio 설치 관리자에서 **개별 구성 요소 > 코드 도구 > NuGet 패키지 관리자** 옵션을 선택하여 따로 설치합니다.

## <a name="find-and-install-a-package"></a>패키지 찾기 및 설치

1. **솔루션 탐색기**에서 **참조** 또는 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리...** 를 선택합니다.

    ![NuGet 패키지 관리 메뉴 옵션](media/ManagePackagesUICommand.png)

1. **찾아보기** 탭은 현재 선택된 원본의 패키지를 인지도별로 표시합니다([패키지 원본](#package-sources) 참조). 왼쪽 위의 검색 상자를 사용하여 특정 패키지를 검색합니다. 목록에서 패키지를 선택하여 해당 정보를 표시합니다. 이 경우 버전 선택드롭다운과 함께 **설치** 단추도 사용할 수 있게 됩니다.

    ![NuGet 패키지 관리 대화 상자의 찾아보기 탭](media/Search.png)

1. 드롭다운에서 원하는 버전을 선택하고 **설치**를 선택합니다. Visual Studio는 패키지와 해당 종속성을 프로젝트에 설치합니다. 사용 조건에 동의하라는 메시지가 표시될 수 있습니다. 설치가 완료되면 추가된 패키지가 **설치됨** 탭에 나타납니다. 패키지는 솔루션 탐색기의 **참조** 노드에도 표시되어, `using` 문을 사용하여 프로젝트에서 해당 패키지를 참조할 수 있음을 나타냅니다.

    ![솔루션 탐색기의 참조](media/References.png)

> [!Tip]
> 검색에 시험판 버전을 포함하고 버전 드롭다운에서 시험판 버전을 사용할 수 있도록 하려면 **시험판 포함** 옵션을 선택합니다.

> [!Note]
> NuGet에는 프로젝트에서 패키지를 사용할 수 있는 두 가지 형식([`PackageReference`](package-references-in-project-files.md) 및 [`packages.config`](../reference/packages-config.md))이 있습니다. [Visual Studio의 옵션 창에서 기본값을 설정할 수 있습니다](Package-Restore.md#choose-default-package-management-format).

## <a name="uninstall-a-package"></a>패키지 제거

1. **솔루션 탐색기**에서 **참조** 또는 원하는 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리...** 를 선택합니다.
1. **설치됨** 탭을 선택합니다.
1. 제거할 패키지를 선택하고(필요한 경우 검색을 사용하여 목록 필터링) **제거**를 선택합니다.

    ![패키지 제거](media/UninstallPackage.png)

1. 패키지를 제거할 때 **시험판 포함** 및 **패키지 원본** 컨트롤은 아무런 영향도 주지 않습니다.

## <a name="update-a-package"></a>패키지 업데이트

1. **솔루션 탐색기**에서 **참조** 또는 원하는 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리...** 를 선택합니다. (웹 사이트 프로젝트에서 **Bin** 폴더를 마우스 오른쪽 단추로 클릭합니다.)
1. **업데이트** 탭을 선택하여 선택한 패키지 원본의 사용 가능한 업데이트가 있는 패키지를 확인합니다. 업데이트 목록에 시험판 패키지를 포함하려면 **시험판 포함**을 선택합니다.
1. 업데이트할 패키지를 선택하고 오른쪽의 드롭다운에서 원하는 버전을 선택하고 **업데이트**를 선택합니다.

    ![패키지 업데이트](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>일부 패키지의 경우 **업데이트** 단추가 사용하지 않도록 설정되고 "SDK에서 암시적으로 참조됩니다.”(또는 “자동 참조됨")이라는 메시지가 표시됩니다. 이 메시지는 패키지가 더 큰 프레임워크 또는 SDK의 일부이며 독립적으로 업데이트해서는 안 됨을 나타냅니다. (이러한 패키지는 내부적으로 `<IsImplicitlyDefined>True</IsImplicitlyDefined>`로 표시됩니다.) 예를 들어 `Microsoft.NETCore.App`은 .NET Core SDK의 일부이며 패키지 버전은 애플리케이션에서 사용하는 런타임 프레임워크의 버전과 동일하지 않습니다. 새 버전의 ASP.NET Core 및 .NET Core 런타임을 가져오려면 [.NET Core 설치를 업데이트](https://aka.ms/dotnet-download)해야 합니다. [.NET Core 메타패키지 및 버전 관리에 대한 자세한 내용은 이 문서를 참조하세요.](/dotnet/core/packages) 이 문서는 일반적으로 사용되는 다음 패키지에 적용됩니다.
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft.NETCore.App
    * NETStandard.Library

    ![암시적 참조 또는 자동 참조로 표시된 예제 패키지](media/PackageManagerUIAutoReferenced.png)

1. 여러 패키지를 최신 버전으로 업데이트하려면 목록에서 해당 패키지를 선택하고 목록 위의 **업데이트** 단추를 선택합니다.
1. **설치됨** 탭에서 개별 패키지를 업데이트할 수도 있습니다. 이 경우 패키지에 대한 세부 정보에는 버전 선택기(**시험판 포함** 옵션의 영향을 받음) 및 **업데이트** 단추가 포함됩니다.

## <a name="manage-packages-for-the-solution"></a>솔루션 패키지 관리

솔루션의 패키지를 관리하는 것은 여러 프로젝트를 동시에 사용할 수 있는 편리한 방법입니다.

1. **도구 > Nuget 패키지 관리자 > 솔루션에 대한 NuGet 패키지 관리...** 메뉴 명령을 선택하거나 솔루션을 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리...** 를 선택합니다.

    ![솔루션에 대한 NuGet 패키지 관리](media/ManagePackagesSolutionUICommand.png)

1. 솔루션의 패키지를 관리할 때 UI를 사용하여 작업의 영향을 받는 프로젝트를 선택할 수 있습니다.

    ![솔루션의 패키지를 관리할 경우의 프로젝트 선택기](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>통합 탭

개발자들은 일반적으로 동일한 솔루션의 여러 프로젝트에서 동일한 NuGet 패키지의 여러 버전을 사용하는 것이 적절하지 않다고 생각합니다. 솔루션의 패키지를 관리하도록 선택하면 패키지 관리자 UI에서 **통합** 탭을 합니다. 이 탭에서는 고유한 버전 번호가 있는 패키지가 솔루션의 여러 다른 프로젝트에서 사용되는 경우를 쉽게 확인할 수 있습니다.

![패키지 관리자 UI 통합 탭](media/ConsolidateTab.png)

이 예제에서 ClassLibrary1 프로젝트는 EntityFramework 6.2.0을 사용하지만, ConsoleApp1는 EntityFramework 6.1.0을 사용합니다. 패키지 버전을 통합하려면 다음을 수행합니다.

- 프로젝트 목록에서 업데이트할 프로젝트를 선택합니다.
- **버전** 제어에서 모든 프로젝트에서 사용할 버전(예: Entityframework 6.2.0)을 선택합니다.
- **설치** 단추를 선택합니다.

패키지 관리자가 선택한 모든 프로젝트에 선택한 패키지 버전을 설치하면, 해당 패키지가 더 이상 **통합** 탭에 표시되지 않습니다.

## <a name="package-sources"></a>패키지 원본

Visual Studio에서 패키지를 가져오는 원본을 변경하려면 원본 선택기에서 하나를 선택합니다.

![패키지 관리자 UI의 패키지 원본 선택기](media/PackageSourceDropDown.png)

패키지 원본을 관리하려면

1. 아래에 설명된 패키지 관리자 UI에서 **설정** 아이콘을 선택하거나 **도구 > 옵션** 명령을 사용하고 **NuGet 패키지 관리자**로 스크롤합니다.

    ![패키지 관리자 UI 설정 아이콘](media/PackageSourceSettings.png)

1. 다음과 같이 **패키지 원본** 노드를 선택합니다.

    ![패키지 원본 옵션](media/options.png)

1. 원본을 추가하려면 **+** 를 선택하고 이름을 편집한 후 **원본** 제어에서 URL 또는 경로를 입력하고 **업데이트**를 선택합니다. 이제 원본이 선택기 드롭다운에 표시됩니다.
1. 패키지 원본을 변경하려면 해당 패키지 원본을 선택하고 **이름** 및 **원본** 상자에서 편집한 후 **업데이트**를 선택합니다.
1. 패키지 원본을 사용하지 않도록 설정하려면 목록에서 이름 왼쪽에 있는 확인란을 선택 취소합니다.
1. 패키지 원본을 제거하려면 해당 패키지 원본을 선택한 다음, **X** 단추를 선택합니다.
1. 위쪽 및 아래쪽 화살표 단추를 사용해도 패키지 원본의 우선 순위는 변경되지 않습니다. Visual Studio는 패키지 소스의 순서를 무시하고, 소스가 요청에 응답하는 순서대로 패키지를 사용합니다. 자세한 내용은 [패키지 복원](../consume-packages/package-restore.md)을 참조하세요.

> [!Tip]
> 삭제 후 패키지 원본이 다시 표시되면 컴퓨터 수준 또는 사용자 수준 `NuGet.Config` 파일에 나열될 수 있습니다. 이러한 파일의 위치를 [일반 NuGet 구성](../consume-packages/configuring-nuget-behavior.md)에서 확인한 후, 파일을 수동으로 편집하거나 [nuget sources 명령](../reference/nuget-exe-CLI-reference.md)을 사용하여 원본을 제거합니다.

## <a name="package-manager-options-control"></a>패키지 관리자 옵션 제어

패키지를 선택하면 패키지 관리자 UI에서 버전 선택기 아래에 확장 가능한 작은 **옵션** 컨트롤이 표시됩니다(여기에는 축소형과 확장형이 모두 표시됨). 일부 프로젝트 형식의 경우 **미리 보기 창 표시** 옵션만 제공됩니다.

![패키지 관리자 옵션](media/PackageManagerUIOptions.png)

다음 섹션에서는 이러한 옵션에 대해 설명합니다.

### <a name="show-preview-window"></a>미리 보기 창 표시

이 옵션을 선택하면 패키지를 설치하기 전에 선택한 패키지의 종속성이 모달 창에 표시됩니다.

![예제 미리 보기 대화 상자](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>설치 및 업데이트 옵션

(일부 프로젝트 형식에는 사용할 수 없습니다.)

**종속성 동작**은 NuGet에서 설치할 종속 패키지의 버전을 결정하는 방법을 구성합니다.

- *종속성 무시*는 설치 중인 패키지를 중단하는 종속성의 설치를 건너뜁니다.
- *최하위*[기본값]는 선택한 기본 패키지의 요구 사항을 충족하는 최소 버전 번호의 종속성을 설치합니다.
- *최상위 패치*는 주 및 부 버전 번호는 같지만 최상위 패치 번호는 다른 버전을 설치합니다. 예를 들어, 버전 1.2.2를 지정한 경우 1.2로 시작하는 최고 버전이 설치됩니다.
- *최상위 부*는 주 버전 번호는 같지만 최상위 부 번호와 패치 번호는 다른 버전을 설치합니다. 버전 1.2.2를 지정한 경우 1로 시작하는 최고 버전이 설치됩니다.
- *최상위*는 패키지의 사용 가능한 최상위 버전을 설치합니다.

**파일 충돌 작업**은 NuGet이 프로젝트 또는 로컬 컴퓨터에 이미 있는 패키지를 처리하는 방법을 지정합니다.

- *프롬프트*는 기존 패키지를 유지할지 아니면 덮어쓸지 묻는 메시지를 요청하도록 NuGet에 지시합니다.
- *모두 무시*는 기존 패키지 덮어쓰기를 건너뛰도록 NuGet에 지시합니다.
- *모두 덮어쓰기*는 기존 패키지를 덮어쓰도록 NuGet에 지시합니다.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>제거 옵션

(일부 프로젝트 형식에는 사용할 수 없습니다.)

**종속성 제거**: 이 옵션을 선택하면 프로젝트의 다른 곳에서 참조되지 않는 모든 종속 패키지가 제거됩니다.

**관련 종속성이 있더라도 강제 제거**: 이 옵션을 선택하면 프로젝트에서 아직 참조되고 있더라도 패키지를 제거합니다. 일반적으로 **종속성 제거**와 함께 사용하여 패키지 및 설치한 종속성을 제거합니다. 그러나 이 옵션을 사용하면 프로젝트에서 참조가 손상될 수 있습니다. 이러한 경우 [다른 패키지를 다시 설치](../consume-packages/reinstalling-and-updating-packages.md)해야 할 수도 있습니다.
