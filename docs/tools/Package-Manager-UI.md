---
title: NuGet 패키지 관리자 UI 참조
description: Visual Studio에서 NuGet 패키지 관리자 UI를 사용 하 여 NuGet 패키지 사용에 대 한 지침입니다.
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 422faf99e58e058d86db774a8f3c1c576b3dc393
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58637625"
---
# <a name="nuget-package-manager-ui"></a>NuGet 패키지 관리자 UI

Windows의 Visual Studio에서 NuGet 패키지 관리자 UI를 사용 하면 쉽게 설치, 제거 및 프로젝트 및 솔루션의 NuGet 패키지를 업데이트할 수 있습니다. Mac 용 Visual Studio의 환경에 대해서 [NuGet 패키지 포함 프로젝트에서](/visualstudio/mac/nuget-walkthrough)합니다. 패키지 관리자 UI를 Visual Studio Code를 사용 하 여 포함 되지 않습니다.

항목 내용:

- [찾기 및 설치 패키지 (찾아보기 탭)](#finding-and-installing-a-package)
- [(설치 됨 탭) 패키지를 제거합니다.](#uninstalling-a-package)
- [(설치 및 업데이트 탭) 패키지를 업데이트 하는 중](#updating-a-package) (포함 된 ["SDK에서 참조 된 암시적 으로" 또는 "AutoReferenced" 메시지](#implicit_reference))
- [솔루션에 대 한 패키지 관리](#managing-packages-for-the-solution) (동시에 여러 프로젝트가 포함 된 작업).
- [패키지 소스](#package-sources)
- [패키지 관리자 옵션 제어](#package-manager-options-control)

> [!Note]
> Visual Studio 2015에서 NuGet 패키지 관리자를 누락 하는 경우 확인 **도구 > 확장 및 업데이트 하는 중...**  검색 된 *NuGet 패키지 관리자* 확장 합니다. Visual Studio에 확장 설치 관리자를 사용할 수 없습니다 경우에서 직접 확장을 다운로드할 [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html)합니다.
>
> Visual Studio 2017에서 NuGet 및 NuGet 패키지 관리자를 자동으로 사용 하 여 설치 됩니다. NET 관련 워크 로드입니다. 선택 하 여 개별적으로 설치 합니다 **개별 구성 요소 > 코드 도구 > NuGet 패키지 관리자** Visual Studio 2017 설치 관리자의 옵션입니다.

## <a name="finding-and-installing-a-package"></a>찾기 및 패키지를 설치 합니다.

1. **솔루션 탐색기**, 중 하나를 마우스 오른쪽 단추로 클릭 **참조가** 프로젝트 및 선택 **NuGet 패키지 관리...** .

    ![NuGet 패키지 메뉴 옵션 관리](media/ManagePackagesUICommand.png)

1. 합니다 **찾아보기** 탭에서 현재 선택한 소스에서 널리 사용 되 고 패키지가 표시 됩니다 (참조 [패키지 원본](#package-sources)). 왼쪽 위에 검색 상자를 사용 하 여 특정 패키지를 검색 합니다. 하며 해당 정보를 표시 하려면 목록에서 패키지를 선택 합니다 **설치** 버전 선택 드롭다운 단추입니다.

    ![NuGet 패키지 대화 찾아보기 탭 관리](media/Search.png)

1. 드롭다운 목록에서 원하는 버전을 선택 하 고 선택 **설치**합니다. Visual Studio 프로젝트에 패키지 및 해당 종속성을 설치합니다. 라이선스에 동의 하 라는 메시지가 표시 될 수 있습니다. 설치가 완료 되 면 추가 패키지에 표시 된 **설치 됨** 탭 합니다. 패키지에도 나열 됩니다는 **참조가** 프로젝트에서를 참조할 수를 나타내는 솔루션 탐색기의 노드 `using` 문입니다.

    ![솔루션 탐색기의 참조](media/References.png)

> [!Tip]
> 검색의 시험판 버전 포함 되도록 시험판 버전에서 사용할 수 있는 드롭다운을 선택 합니다 **시험판 포함** 옵션입니다.

## <a name="uninstalling-a-package"></a>패키지를 제거합니다.

1. **솔루션 탐색기**, 중 하나를 마우스 오른쪽 단추로 클릭 **참조가** 원하는 프로젝트를 마우스 또는 **NuGet 패키지 관리...** .
1. 선택 된 **설치 됨** 탭 합니다.
1. (필요한 경우 목록을 필터링 하려면 검색을 사용 합니다.)를 제거 하려면 패키지 선택 및 선택 **제거**합니다.

    ![패키지를 제거합니다.](media/UninstallPackage.png)

1. 합니다 **시험판 포함** 하 고 **패키지 원본** 컨트롤 영향을 주지 않습니다 패키지를 제거 하는 경우.

## <a name="updating-a-package"></a>패키지를 업데이트 하는 중

1. **솔루션 탐색기**, 중 하나를 마우스 오른쪽 단추로 클릭 **참조가** 원하는 프로젝트를 마우스 또는 **NuGet 패키지 관리...** . (웹 사이트 프로젝트에서 마우스 오른쪽 단추로 클릭 합니다 **Bin** 폴더입니다.)
1. 선택 된 **업데이트** 선택한 패키지 원본에서 사용 가능한 업데이트가 있는 패키지를 탭 합니다. 선택 **시험판 포함** 업데이트 목록에 시험판 패키지를 포함 합니다.
1. 패키지, 업데이트 하 고, 오른쪽의 드롭다운 목록에서 원하는 버전을 선택 하 고, 선택를 선택한 **업데이트**합니다.

    ![패키지를 업데이트 하는 중](media/UpdatePackages.png)

1. <a name="implicit_reference"></a>일부 패키지는 **업데이트** 단추가 비활성화 되 고 있는지 "암시적으로 참조 하는 SDK" 라는 메시지가 나타납니다 (또는 "AutoReferenced"). 이 메시지는 패키지를 더 큰 프레임 워크 또는 SDK의 일부 이며 독립적으로 업데이트 되지 않아야 나타냅니다. (이러한 패키지는 내부적으로 표시 `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) 예를 들어 `Microsoft.NETCore.App` .NET Core SDK의 일부인 아니며 패키지 버전의 응용 프로그램에서 사용 하는 런타임 프레임 워크 버전과 동일 합니다. 해야 [.NET Core 설치를 업데이트](https://aka.ms/dotnet-download) 새 버전의 ASP.NET Core 및.NET Core 런타임을 가져오려고 합니다. [.NET Core 메타 패키지 및 버전 관리에 대 한 자세한 내용은이 문서를 참조 하세요.](/dotnet/core/packages)합니다. 이 일반적으로 사용 되는 패키지에 적용 됩니다.
    * Microsoft.AspNetCore.All
    * Microsoft.AspNetCore.App
    * Microsoft.NETCore.App
    * NETStandard.Library

    ![참조 또는 AutoReferenced로 암시적으로 표시 되는 예제 패키지](media/PackageManagerUIAutoReferenced.png)

1. 선택 목록에서 선택할 여러 패키지를 최신 버전으로 업데이트 하려면 합니다 **업데이트** 목록 위에 있는 단추입니다.
1. 개별 패키지를 업데이트할 수도 있습니다는 **설치 됨** 탭 합니다. 패키지에 대 한 세부 정보를 버전 선택기를 포함 하는 예제의 경우 (적용 된 **시험판 포함** 옵션) 및 **업데이트** 단추입니다.

## <a name="managing-packages-for-the-solution"></a>솔루션에 대 한 패키지 관리

동시에 여러 프로젝트를 사용 하 여 작업 하는 편리한 방법을 솔루션의 패키지를 관리 합니다.

1. 선택 된 **도구 > NuGet 패키지 관리자 > 솔루션용 NuGet 패키지 관리...**  메뉴 명령을 실행 하거나 솔루션을 마우스 오른쪽 단추로 클릭 하 고 선택 **NuGet 패키지 관리...** :

    ![솔루션용 NuGet 패키지 관리](media/ManagePackagesSolutionUICommand.png)

1. 솔루션에 대 한 패키지를 관리 하는 경우 UI 작업의 영향을 받는 프로젝트를 선택할 수 있습니다.

    ![프로젝트 선택기 솔루션에 대 한 패키지를 관리 하는 경우](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a>통합 탭

개발자가 일반적으로 고려 잘못 된 방법은 동일한 솔루션 내의 여러 프로젝트에서 동일한 NuGet 패키지의 서로 다른 버전을 사용 합니다. 패키지 관리자 UI를 제공 하는 솔루션의 패키지를 관리 하려는 경우는 **통합** 를 쉽게 확인할 수 있습니다 고유한 버전 번호를 사용 하 여 패키지를 솔루션의 다른 프로젝트에서 사용 되는 위치 탭:

![패키지 관리자 UI 통합 탭](media/ConsolidateTab.png)

이 예제에서는 ClassLibrary1 프로젝트 ConsoleApp1 6.1.0 EntityFramework를 사용 하는 반면 6.2.0, EntityFramework를 사용한 됩니다. 패키지 버전을 통합 하려면 다음을 수행 합니다.

- 프로젝트 목록에서 업데이트할 프로젝트를 선택 합니다.
- 이러한 모든 프로젝트에 사용할 버전을 선택 합니다 **버전** EntityFramework 6.2.0 등의 컨트롤입니다.
- 선택 된 **설치** 단추입니다.

패키지 관리자는 선택한 모든 프로젝트에는 패키지에 더 이상 나타나지 선택한 패키지 버전을 설치 합니다 **통합** 탭 합니다.

## <a name="package-sources"></a>패키지 소스

Visual Studio는 패키지를 가져올 소스를 변경 하려면 원본 선택기에서 하나를 선택 합니다.

![패키지 관리자 UI에서에서 패키지 원본 선택기](media/PackageSourceDropDown.png)

패키지 소스를 관리 합니다.

1. 선택 합니다 **설정을** 패키지 관리자 UI에서 아이콘 아래에 설명 된 또는 사용 합니다 **도구 > 옵션** 를 스크롤하여 명령 **NuGet 패키지 관리자**:

    ![패키지 관리자 UI 설정 아이콘](media/PackageSourceSettings.png)

1. 선택 된 **패키지 원본** 노드:

    ![패키지 원본 옵션](media/options.png)

1. 소스를 추가 하려면 선택 **+** 이름을 편집 하 고, URL 또는 경로 입력 합니다 **소스** 컨트롤을 선택한 **업데이트**합니다. 이제 원본 선택기 드롭다운 목록에에서 나타납니다.
1. 패키지 소스를 변경 하려면 선택, 편집에 **이름** 및 **원본** 입력란과 선택 **업데이트**합니다.
1. 패키지 소스를 해제 하려면 목록에서 이름 왼쪽에 상자를 취소 합니다.
1. 패키지 소스를 제거 하려면 선택 하 고 다음을 선택 합니다 **X** 단추입니다.
1. 사용 하 고 아래쪽 화살표 단추 패키지 원본의 우선 순위 변경 되지 않습니다. Visual Studio는 먼저 요청에 응답 하도록 소스가에서 패키지를 사용 하 여 패키지 소스의 순서를 무시 합니다. 자세한 내용은 [패키지 복원](../consume-packages/package-restore.md)합니다.

> [!Tip]
> 패키지 소스를 삭제 한 후 다시 나타나면, 컴퓨터 수준 또는 사용자 수준에 나타날 수 있습니다 `NuGet.Config` 파일입니다. 참조 [NuGet 동작 구성](../consume-packages/configuring-nuget-behavior.md) 이러한 파일의 위치에 대해 다음 원본을 제거 파일을 수동으로 편집 하거나 사용 하 여 합니다 [nuget 명령 원본](../tools/nuget-exe-CLI-reference.md)합니다.

## <a name="package-manager-options-control"></a>패키지 관리자 옵션 제어

패키지 관리자 UI 표시는 작은 패키지를 선택 하면 확장 가능한 **옵션** (확장 및 축소 모두 표시) 버전 선택기 아래 제어 합니다. 일부 프로젝트에는 형식 에서만 합니다 **미리 보기 창 표시** 옵션이 제공 됩니다.

![패키지 관리자 옵션](media/PackageManagerUIOptions.png)

다음 섹션에서는 이러한 옵션을 설명합니다.

### <a name="show-preview-window"></a>미리 보기 창 표시

옵션을 선택 하면 모달 창 종속성을 표시 하는 선택한 패키지의 패키지를 설치 하기 전에:

![예제에서는 미리 보기 대화 상자](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a>설치 및 업데이트 옵션

(사용할 수 없음의 모든 프로젝트 형식에 대 한 합니다.)

**종속성 동작** NuGet 버전을 설치 하려면 종속 패키지를 결정 하는 방법 구성:

- *종속성 무시* 일반적으로 설치 되는 패키지를 중단 하는 모든 종속성을 설치를 건너뜁니다.
- *가장 낮은* [기본값] 기본 선택한 패키지의 요구 사항을 충족 하는 최소 버전 번호를 사용 하 여 종속성을 설치 합니다.
- *가장 높은 패치* 동일한 주 및 부 버전 번호, 있지만 패치 번호가 가장 높은 버전을 설치 합니다. 예를 들어 버전 1.2.2 이상을 지정 하는 경우 다음 1.2를 사용 하 여 시작 하는 가장 높은 버전을 설치할
- *가장 높은 보조* 버전이 동일한 주 버전 번호를 하지만 보조 번호가 가장 높은 패치 번호와 함께 설치 합니다. 버전 1.2.2 이상을 지정 된 경우 다음 1로 시작 하는 가장 높은 버전을 설치할
- *가장 높은* 패키지의 사용 가능한 가장 높은 버전을 설치 합니다.

**파일 충돌 작업** NuGet에서 프로젝트 또는 로컬 컴퓨터에 이미 있는 패키지를 처리 하는 방법을 지정 합니다.

- *프롬프트* 유지 하거나 기존 패키지를 덮어쓸 것인지 확인 하는 NuGet에 지시 합니다.
- *모두 무시* 기존 패키지를 덮어쓰지 않으려면 NuGet에 지시 합니다.
- *모두 덮어쓰기* 기존 패키지를 덮어쓸 수는 NuGet에 지시 합니다.

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a>제거 옵션

(사용할 수 없음의 모든 프로젝트 형식에 대 한 합니다.)

**종속성을 제거**: 옵션을 선택 하면는 하지 프로젝트에서 다른 곳에서 참조 하는 경우 모든 종속 패키지를 제거 합니다.

**에 종속 된 경우에 강제 제거**: 옵션을 선택 하면 프로젝트에서 참조 되는 경우에 패키지를 제거 합니다. 일반적으로 함께에서 사용 됩니다 **종속성을 제거** 패키지와 관계 없이 제거할 종속성 설치 되는 것입니다. 그러나이 옵션을 사용 하 여 프로젝트에 대 한 손상 된 참조가 발생할 수 있습니다. 이러한 경우 해야 [다른 패키지를 다시 설치](../consume-packages/reinstalling-and-updating-packages.md)합니다.
