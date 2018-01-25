---
title: "NuGet 패키지 관리자 UI 참조 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
description: "NuGet 패키지를 사용 하기 위한 Visual Studio에서 NuGet 패키지 관리자 UI를 사용 하기 위한 지침입니다."
keywords: "NuGet 패키지 관리자 UI에서 NuGet 패키지 관리자 Visual Studio에서 NuGet 패키지, NuGet 사용자 인터페이스를 관리 하는 Visual Studio에서 NuGet UI"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0ff60c3cecee5fd9b7f698d2abed7553f5d89c1d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-package-manager-ui"></a>NuGet 패키지 관리자 UI

Windows에서 Visual Studio에서 NuGet 패키지 관리자 UI를 사용 하면 쉽게 설치, 제거 및 프로젝트와 솔루션에서 NuGet 패키지를 업데이트할 수 있습니다. Mac 용 Visual Studio에서 차원에서 참조 [프로젝트에 포함 하는 NuGet 패키지](/visualstudio/mac/nuget-walkthrough)합니다. 패키지 관리자 UI를 Visual Studio 코드 포함 되지 않습니다.

항목 내용:

- [찾기 및 설치 패키지 (찾아보기 탭)](#finding-and-installing-a-package)
- [(설치 됨 탭) 패키지를 제거합니다.](#uninstalling-a-package)
- [업데이트 패키지 (설치 됨 및 업데이트 탭)](#updating-a-package) (포함 된 ["SDK에서 참조 된 암시적 으로" 또는 "AutoReferenced" 메시지](#implicit_reference))
- [솔루션에 대 한 패키지 관리](#managing-packages-for-the-solution) (동시에 여러 프로젝트 작업).
- [패키지 원본](#package-sources)
- [패키지 관리자 옵션 제어](#package-manager-options-control)

> [!Note]
> Visual Studio 2015의 NuGet 패키지 관리자를 누락 하는 경우 확인 **도구 > 확장 및 업데이트 중...**  검색 한는 *NuGet 패키지 관리자* 확장 합니다. Visual studio에서 확장명 설치 관리자를 사용 하는 경우에서 직접 확장을 다운로드 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)합니다.
>
> Visual Studio 2017에 NuGet 및 NuGet 패키지 관리자 자동으로 함께 설치 됩니다. NET 관련 작업 합니다. 선택 하 여 개별적으로 설치 된 **개별 구성 요소 > 코드 도구 > NuGet 패키지 관리자** Visual Studio 2017 설치 관리자에 대 한 옵션입니다.

## <a name="finding-and-installing-a-package"></a>찾기 및 설치 패키지

1. **솔루션 탐색기**, 단추로 클릭 하 고 **참조** 또는 프로젝트를 선택 **NuGet 패키지 관리...** .

    ![메뉴 옵션 NuGet 패키지 관리](media/ManagePackagesUICommand.png)

1. **찾아보기** 인기도 순서로 현재 선택 된 소스에서 패키지를 표시 하는 탭 (참조 [원본 패키지](#package-sources)). 홈페이지에서 검색 상자를 사용 하 여 특정 패키지를 검색 합니다. 또한 수 있는 해당 정보를 표시 하려면 목록에서 패키지를 선택는 **설치** 함께 버전 선택 드롭 다운 단추입니다.

    ![NuGet 패키지 대화 찾아보기 탭 관리](media/Search.png)

1. 드롭다운 목록에서 원하는 버전을 선택 하 고 선택 **설치**합니다. Visual Studio 프로젝트에 패키지 및 해당 종속성을 설치합니다. 사용 조건에 동의 해야 할 수 있습니다. 설치가 완료 되 면 추가 패키지에 표시 된 **설치 됨** 탭 합니다. 패키지에도 나열 됩니다는 **참조** 에서 사용 하 여 프로젝트에 참조할 수 있는지를 나타내는 솔루션 탐색기의 노드 `using` 문.

    ![솔루션 탐색기의 참조가](media/References.png)

> [!Tip]
    > 검색에서 시험판 버전을 포함 하 고 시험판 버전에서 사용할 수 있도록 버전의 드롭다운 목록에서 선택 된 **시험판 포함** 옵션입니다.

## <a name="uninstalling-a-package"></a>패키지를 제거합니다.

1. **솔루션 탐색기**, 단추로 클릭 하 고 **참조** 또는 원하는 프로젝트를 선택 **NuGet 패키지 관리...** .
1. 선택 된 **설치 됨** 탭 합니다.
1. (필요한 경우 목록을 필터링 하려면 검색을 사용 합니다.)을 제거 하려는 패키지 선택 및 선택 **제거**합니다.

    ![패키지를 제거합니다.](media/UninstallPackage.png)

1. **preprelease 포함** 및 **패키지 원본** 컨트롤 효과가 없습니다. 패키지를 제거 하는 경우.

## <a name="updating-a-package"></a>패키지를 업데이트합니다.

1. **솔루션 탐색기**, 단추로 클릭 하 고 **참조** 또는 원하는 프로젝트를 선택 **NuGet 패키지 관리...** . (웹 사이트 프로젝트에서 마우스 오른쪽 단추로 클릭는 **Bin** 폴더입니다.)
1. 선택 된 **업데이트** 탭 선택 된 패키지 소스에서 사용 가능한 업데이트가 있는 패키지를 확인할 수 있습니다. 선택 **시험판 포함** 업데이트 목록에 시험판 패키지를 포함 하도록 합니다.
1. 패키지 업데이트, 오른쪽의 드롭다운 목록에서 원하는 버전을 선택 및 선택를 선택한 **업데이트**합니다.

    ![패키지를 업데이트합니다.](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>일부 패키지에 대 한는 **업데이트** 단추가 비활성화 되 고 "암시적으로 참조 함을 SDK에서" 없다는 메시지가 표시 (또는 "AutoReferenced"). 메시지는 Microsoft.NETCore.App 또는 Microsoft.NETStandard.Library, 같은 패키지를 더 큰 프레임 워크 또는 SDK의 일부 이며 독립적으로 업데이트 되지 않아야 나타냅니다. (이러한 packagee로 내부적으로 표시 된 `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) 패키지를 업데이트 하려면 속해 있는 SDK를 업데이트 합니다.

    ![참조 또는 AutoReferenced로 암시적으로 표시 되는 예제 패키지](media/PackageManagerUIAutoReferenced.png)

1. 고 목록에서 선택 여러 패키지의 최신 버전으로 업데이트 하려면는 **업데이트** 목록 위의 단추입니다.
1. 개별 패키지를 업데이트할 수도 있습니다는 **설치 됨** 탭 합니다. 패키지에 대 한 세부 정보에서 버전 선택기를 포함 하는 경우 (에 **Include 시험판** 옵션) 및 **업데이트** 단추입니다.

## <a name="managing-packages-for-the-solution"></a>솔루션에 대 한 패키지 관리

패키지를 솔루션에 대 한 관리는 동시에 여러 프로젝트와 함께 작업 하는 편리한 방법입니다.

1. 선택 된 **도구 > NuGet 패키지 관리자 > 솔루션용 NuGet 패키지 관리...**  메뉴 명령을 실행 하거나 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리...** :

    ![솔루션에 대 한 NuGet 패키지 관리](media/ManagePackagesSolutionUICommand.png)

1. 솔루션에 대 한 패키지를 관리 하는 경우 UI는 실행 작업의 영향을 받는 프로젝트를 선택할 수 있습니다.

    ![솔루션에 대 한 패키지를 관리 하는 경우 프로젝트 선택기](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>탭 통합

개발자가 일반적으로 고려 동일한 솔루션의 다른 프로젝트에서 서로 다른 버전의 같은 NuGet 패키지를 사용 하는 잘못 된 것입니다. 패키지 관리자 UI를 제공 하는 솔루션에 대 한 패키지를 관리 하려는 경우는 **통합** 를 쉽게 확인할 수 있습니다 고유한 버전 번호를 사용 하 여 패키지 솔루션의 다른 프로젝트에서 사용 되는 위치 탭:

![패키지 관리자 UI 통합 탭](media/ConsolidateTab.png)

이 예제에서는 ClassLibrary1 프로젝트 ConsoleApp1 6.2.0 EntityFramework를 사용 하는 반면 6.2.0, EntityFramework를 사용 중인 합니다. 패키지 버전을 통합 하려면 다음을 수행 합니다.

- 프로젝트 목록에서 업데이트할 프로젝트를 선택 합니다.
- 이러한 모든 프로젝트에 사용할 버전을 선택는 **버전** EntityFramework 6.2.0 같은 제어 합니다.
- 선택 된 **설치** 단추입니다.

패키지 관리자는 패키지에 더 이상 나타나지는 선택한 모든 프로젝트로 선택된 된 패키지 버전을 설치는 **통합** 탭 합니다.

## <a name="package-sources"></a>패키지 원본

Visual Studio는 패키지를 가져올 소스를 변경 하려면 소스 선택기에서 하나를 선택 합니다.

![패키지 관리자 UI에서에서 패키지 원본 선택기](media/PackageSourceDropDown.png)

관리 하려면 패키지 소스:

1. 선택은 **설정** 패키지 관리자 UI에서 아이콘 아래에 설명 된 하거나 사용 하 여는 **도구 > 옵션** 명령를 스크롤하여 **NuGet 패키지 관리자**:

    ![패키지 관리자 UI 설정 아이콘](media/PackageSourceSettings.png)

1. 선택 된 **패키지 소스** 노드:

    ![패키지 소스 옵션](media/options.png)

1. 소스를 추가 하려면 선택  **+** , 이름을 편집 하 고, URL 또는 경로 입력의 **소스** 컨트롤을 선택 **업데이트**합니다. 이제 원본 선택기 드롭다운에에서 나타납니다.
1. 패키지 소스를 변경 하려면 선택에서 항목을 편집 하 고 **이름** 및 **소스** 상자 및 선택 **업데이트**합니다.
1. 패키지 소스를 사용 하지 않으려면 목록의 이름 왼쪽에 확인란의 선택을 취소 합니다.
1. 패키지 소스를 제거 하려면 선택 하 고 다음 선택에서 **X** 단추입니다.
1. 위쪽 및 아래쪽 화살표 단추를 패키지 소스 우선 순위를 변경 합니다. Visual Studio 프로젝트에 대 한 패키지를 복원 하는 경우 이러한 소스 우선 순위 순서 대로 검색 합니다. 자세한 내용은 참조 [패키지를 복원](../Consume-Packages/Package-Restore.md)합니다.

> [!Tip]
> 패키지 소스 삭제 한 후 다시 경우 컴퓨터 수준 또는 사용자 수준에 나타날 수 있습니다 `NuGet.Config` 파일입니다. 참조 [NuGet 구성 동작](../Consume-Packages/Configuring-NuGet-Behavior.md) 이러한 파일의 위치에 대 한 다음 제거 소스 파일을 수동으로 편집 하거나 사용 하 여는 [nuget 명령 원본](../tools/nuget-exe-CLI-reference.md)합니다.

## <a name="package-manager-options-control"></a>패키지 관리자 옵션 제어

패키지를 선택한 경우 패키지 관리자 UI는 작고를 표시 하는 확장 가능한 **옵션** (축소 및 확장 모두 표시) 버전 선택기 아래에 컨트롤입니다. 일부 프로젝트에 대 한 형식 에서만 **미리 보기 창 표시** 옵션이 제공 됩니다.

![패키지 관리자 옵션](media/PackageManagerUIOptions.png)

다음 섹션에서는 이러한 옵션에 설명 합니다.

### <a name="show-preview-window"></a>미리 보기 창 표시

옵션을 선택 하면 모달 창 종속성을 표시 하는 선택한 패키지의 패키지를 설치 하기 전에:

![예제에서는 미리 보기 대화 상자](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>설치 및 업데이트 옵션

(사용할 수 없음 모든 프로젝트 형식에 대 한 합니다.)

**종속성 동작은** NuGet 설치할 종속성 패키지의 버전을 결정 하는 방법 구성:

- *종속성 무시* 일반적으로 설치 되는 패키지를 중단 시키는 모든 종속성을 설치를 건너뜁니다.
- *가장 낮은* [기본값] 기본 선택한 패키지의 요구 사항을 충족 하는 최소 버전 번호와 종속성을 설치 합니다.
- *가장 높은 패치* 같은 주 및 부 버전 번호는 있지만 패치 번호가 가장 높은 버전을 설치 합니다. 예를 들어 1.2.2 버전을 지정 하는 경우 다음 1.2로 시작 하는 가장 높은 버전을 설치할
- *가장 높은 보조* 버전이 주 버전 번호가 같은 있지만 부 버전 번호가 가장 높은 패치 번호와 함께 설치 합니다. 1.2.2 버전을 지정 하는 경우 다음 1로 시작 하는 가장 높은 버전을 설치할
- *가장 높은* 패키지의 사용 가능한 가장 높은 버전을 설치 합니다.

**충돌 작업 파일** NuGet 패키지는 프로젝트 또는 로컬 컴퓨터에 이미 있는 처리 방법을 지정 합니다.

- *Prompt* NuGet 유지 하거나 기존 패키지를 덮어쓸 것인지 확인 하도록 지시 합니다.
- *모두 무시* 모든 기존 패키지를 덮어쓰지 않으려면 NuGet 지시 합니다.
- *모두 덮어쓰기* 모든 기존 패키지를 덮어쓸 수는 NuGet을 지시 합니다.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>제거 옵션

(사용할 수 없음 모든 프로젝트 형식에 대 한 합니다.)

**종속성을 제거**: 옵션을 선택 하면 프로젝트의 다른 곳에서 참조 되지 하는 경우 모든 종속 패키지를 제거 합니다.

**에 종속성이 있더라도 강제 제거**: 옵션을 선택 하면 프로젝트에서 참조 되는 경우에 패키지를 제거 합니다. 이 일반적으로 함께에서 사용 되어 **종속성을 제거** 패키지와 관계 없이 제거할 종속성 설치 되는 것입니다. 그러나이 옵션을 사용 하 여 프로젝트에서 참조가 손상된 발생할 수 있습니다. 이러한 경우 해야 할 수 있습니다 [다른 패키지를 다시 설치](../consume-packages/reinstalling-and-updating-packages.md)합니다.
