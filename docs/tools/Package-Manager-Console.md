---
title: 설치 하 고 콘솔을 사용 하 여 Visual Studio에서 NuGet 패키지 관리
description: Visual Studio에서 NuGet 패키지 관리자 콘솔을 사용 하 여 패키지를 사용 하 여 작업에 대 한 지침입니다.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 91ab3859994e5ae738c6637219681ebbfc92d420
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842591"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a>설치 하 고 Visual Studio (PowerShell)에서 패키지 관리자 콘솔을 사용 하 여 패키지를 관리

NuGet 패키지 관리자 콘솔에서 사용할 수 있습니다 [NuGet PowerShell 명령을](../tools/powershell-reference.md) 를 찾으려면 설치, 제거 및 NuGet 패키지를 업데이트 합니다. 콘솔을 사용 하는 패키지 관리자 UI 작업을 수행 하는 방법을 제공 하지 않는 경우에 필요 합니다. 사용 하도록 `nuget.exe` 콘솔에서 CLI 명령 참조 [콘솔에서 nuget.exe CLI를 사용 하 여](#using-the-nugetexe-cli-in-the-console)입니다.

콘솔은 Windows에서 Visual Studio에 빌드됩니다. Visual Studio Code 또는 Mac 용 Visual Studio를 사용 하 여 포함 되지 않습니다.

## <a name="find-and-install-a-package"></a>찾기 및 패키지를 설치 합니다.

예를 들어, 찾기 및 패키지를 설치 하는 간단한 세 단계로 수행 됩니다.

1. Visual Studio에서 프로젝트/솔루션을 열고 사용 하 여 콘솔을 엽니다는 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 명령입니다.

1. 설치 하려는 패키지를 찾습니다. 이 이미 알고 있는 경우 3 단계로 건너뜁니다.

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. 설치 명령을 실행 합니다.

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> 사용 하 여 콘솔에서 사용할 수 있는 모든 작업을 수행할 수도 있습니다는 [NuGet CLI](../tools/nuget-exe-cli-reference.md)합니다. 그러나 콘솔 명령 Visual Studio 및 저장 된 프로젝트/솔루션의 컨텍스트 내에서 작동 하 고 종종 해당 해당 CLI 명령 보다를 수행 합니다. 예를 들어, 콘솔을 통해 패키지를 설치 하는 CLI 명령의 반면 프로젝트에 대 한 참조를 추가 합니다. 이 따라서 일반적으로 Visual Studio에서 작업 하는 개발자는 cli 콘솔을 사용 하 여 선호 합니다.

> [!Tip]
> 많은 콘솔 작업 알려진된 경로 이름을 사용 하 여 Visual Studio에서 열린 솔루션에 따라 달라 집니다. 저장 되지 않은 솔루션 또는 솔루션이 없는 경우 오류를 볼 수 있습니다, "솔루션이 열려 있지 되거나 저장 되지 않습니다. 중인지 열기 및 저장 된 솔루션입니다. " 이 콘솔을 솔루션 폴더를 확인할 수 없음을 나타냅니다. 저장 되지 않은 솔루션을 저장 하거나 만들고 계정이 없는 경우 솔루션을 저장를 열고 오류를 수정 해야 합니다.

## <a name="opening-the-console-and-console-controls"></a>콘솔 및 콘솔 컨트롤 열기

1. 콘솔을 사용 하 여 Visual Studio에서 엽니다는 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 명령입니다. 콘솔은 정렬 하 고 원하는 대로 정할 수 있을 수 있는 Visual Studio 창 (참조 [Visual Studio에서 창 레이아웃 사용자 지정](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. 기본적으로 콘솔 명령은 창의 맨 위에 있는 컨트롤에 설정 된 대로 특정 패키지 소스를 프로젝트에 대해 작동 합니다.

    ![패키지 원본 및 프로젝트에 대 한 패키지 관리자 콘솔을 제어합니다.](media/PackageManagerConsoleControls1.png)

1. 다른 패키지 소스 및/또는 프로젝트를 선택 하면 후속 명령에 대 한 이러한 기본값을 변경 합니다. 기본값을 변경 하지 않고 이러한 설정을 overrride에 대부분의 명령은 지원 `-Source` 고 `-ProjectName` 옵션입니다.

1. 패키지 소스를 관리 하려면 기어 아이콘을 선택 합니다. 이것이 바로 가기를 합니다 **도구 > 옵션 > NuGet 패키지 관리자 > 패키지 소스** 대화 상자에 설명 된 대로 합니다 [패키지 관리자 UI](package-manager-ui.md#package-sources) 페이지. 또한 프로젝트 선택기의 오른쪽에 컨트롤을 콘솔의 내용을 지웁니다.

    ![패키지 관리자 콘솔 설정 및 일반 컨트롤](media/PackageManagerConsoleControls2.png)

1. 맨 오른쪽 단추를 장기 실행 명령을 중단합니다. 예를 들어 실행 `Get-Package -ListAvailable -PageSize 500` 정도 실행 하는 데 몇 분 정도 걸릴 수 있습니다 (예: nuget.org)를 기본 원본에서 상위 500 패키지를 나열 합니다.

    ![패키지 관리자 콘솔 중지 제어](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>패키지를 설치합니다.

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

참조 [Install-package](../tools/ps-ref-install-package.md)합니다.

에 설명 된 대로 동일한 단계를 수행 하는 콘솔에 패키지를 설치 [패키지를 설치 하는 경우](../concepts/package-installation-process.md), 다음 내용을 추가 하 여:

- 콘솔을 암시 된 계약을 사용 하 여 해당 창에서 해당 사용 약관을 표시합니다. 약관에 동의 하지 않는 경우 패키지를 즉시 제거 해야 합니다.
- 또한 패키지에 대 한 참조를 프로젝트 파일에 추가 되 고 나타나는 **솔루션 탐색기** 아래의 합니다 **참조** 직접 프로젝트 파일의 변경 내용을 보려면 프로젝트를 저장 해야 하는 노드를 합니다.

## <a name="uninstalling-a-package"></a>패키지를 제거합니다.

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

참조 [Uninstall-package](../tools/ps-ref-uninstall-package.md)합니다. 사용 하 여 [패키지 가져오기](../tools/ps-ref-get-package.md) 현재 식별자를 찾아야 할 경우 기본 프로젝트에 설치 된 모든 패키지를 확인 합니다.

패키지를 제거한 다음 작업을 수행 합니다.

- 프로젝트 (및 모든 관리 형식을 사용 중인)에서 패키지에 대 한 참조를 제거 합니다. 참조에 더 이상 나타나지 **솔루션 탐색기**합니다. (에서 제거 하는지 확인 하려면 프로젝트를 다시 작성 해야 합니다 **Bin** 폴더입니다.)
- 변경 내용이 되돌리는 `app.config` 또는 `web.config` 패키지가 설치 된 경우.
- 나머지 패키지 없음 해당 종속성을 사용 하는 경우 종속성을 제거 이전에 설치 합니다.

## <a name="updating-a-package"></a>패키지를 업데이트 하는 중

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

참조 [패키지 가져오기](../tools/ps-ref-get-package.md) 고 [업데이트 패키지](../tools/ps-ref-update-package.md)

## <a name="finding-a-package"></a>패키지 찾기

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

참조 [Find-package](../tools/ps-ref-find-package.md)합니다. Visual Studio 2013 및 이전 버전에서는 사용할 [패키지 가져오기](../tools/ps-ref-get-package.md) 대신 합니다.

## <a name="availability-of-the-console"></a>콘솔의 가용성

Visual Studio 2017부터, NuGet 및 NuGet 패키지 관리자를 자동으로 설치 됩니다 하나를 선택 합니다. NET 관련 워크 로드. 설치할 수 있습니다도 개별적으로 확인 하 여 합니다 **개별 구성 요소 > 코드 도구 > NuGet 패키지 관리자** Visual Studio 설치 관리자에서 옵션입니다.

Visual Studio 2015 및 이전 버전의 NuGet 패키지 관리자를 누락 하는 경우 확인 하는 또한 **도구 > 확장 및 업데이트 하는 중...**  및 NuGet 패키지 관리자 확장명을 검색 합니다. Visual Studio에 확장 설치 관리자를 사용할 수 없습니다 경우에서 직접 확장을 다운로드할 수 있습니다 [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html)합니다.

Mac 용 Visual Studio를 사용 하 여 현재 사용 가능한 패키지 관리자 콘솔 아닙니다. 그러나 해당 명령을 통해 사용할 수는 [NuGet CLI](nuget-exe-CLI-reference.md)합니다. Mac 용 visual Studio NuGet 패키지 관리를 위한 UI가 있습니다. 참조 [NuGet 패키지 포함 프로젝트에서](/visualstudio/mac/nuget-walkthrough)합니다.

패키지 관리자 콘솔을 Visual Studio Code를 사용 하 여 포함 되지 않습니다.

## <a name="extending-the-package-manager-console"></a>패키지 관리자 콘솔 확장

일부 패키지는 콘솔에 대 한 새 명령을 설치합니다. 예를 들어 `MvcScaffolding` 와 같은 명령을 만듭니다 `Scaffold` 아래 그림을 생성 하는 ASP.NET MVC 컨트롤러 및 보기:

![설치 및 MvcScaffold 사용](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>NuGet PowerShell 프로필 설정

PowerShell 프로필을 사용 하면 PowerShell을 사용 하 여 어디서 나 자주 사용 하는 명령을 사용할 수 있도록 수 있습니다. NuGet은 일반적으로 다음 위치에 있는 NuGet 관련 프로필을 지원 합니다.

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

프로필을 찾으려면 입력 `$profile` 콘솔에서:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

자세한 내용은 참조 [Windows PowerShell 프로필](https://technet.microsoft.com/library/bb613488.aspx)합니다.

## <a name="using-the-nugetexe-cli-in-the-console"></a>콘솔에서 nuget.exe CLI를 사용 하 여

확인 합니다 [ `nuget.exe` CLI](nuget-exe-cli-reference.md) 패키지 관리자 콘솔에서 사용할 수 있는 설치를 [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) 콘솔에서 패키지:

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
