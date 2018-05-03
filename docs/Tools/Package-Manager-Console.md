---
title: NuGet 패키지 관리자 콘솔 가이드
description: 패키지 작업에 대 한 Visual Studio에서 NuGet 패키지 관리자 콘솔을 사용 하기 위한 지침입니다.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 64912f0dc32a492d9c23a02f45b4303c69faf340
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="package-manager-console"></a>패키지 관리자 콘솔

NuGet 패키지 관리자 콘솔이 Windows 2012 이상 버전에서 Visual Studio에 빌드됩니다. (이 Visual Studio Code 또는 Mac에 대 한 Visual Studio에 포함 합니다.)

콘솔을 통해 사용할 수 있습니다 [NuGet PowerShell 명령을](../tools/powershell-reference.md) 를 찾으려면 설치, 제거 및 NuGet 패키지를 업데이트 합니다. 콘솔을 사용 하는 패키지 관리자 UI 작업을 수행 하는 방법을 제공 하지 않는 경우에 필요 합니다. 사용 하도록 `nuget.exe` 콘솔에서 명령을 참조 [콘솔에서 nuget.exe CLI를 사용 하 여](#using-the-nugetexe-cli-in-the-console)합니다.

예를 들어, 찾기 및 설치 패키지는 3 개의 쉬운 단계를 통해 수행 됩니다.

1. Visual Studio에서 프로젝트/솔루션을 열고 사용 하 여 콘솔을 열고는 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 명령입니다.

1. 설치 하려는 패키지를 찾습니다. 이 이미 알고 있는 경우에 3 단계로 건너뜁니다.

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
> 콘솔에서 사용할 수 있는 모든 작업으로 수행할 수 있습니다는 [NuGet CLI](../tools/nuget-exe-cli-reference.md)합니다. 그러나 콘솔 명령 Visual Studio 및 저장 된 프로젝트/솔루션의 컨텍스트 내에서 작동 하 고 종종의 상응 하는 CLI 명령 이상 수행. 예를 들어 콘솔을 통해 패키지를 설치 하는 CLI 명령에는 없는 반면 프로젝트에 대 한 참조를 추가 합니다. 이러한 이유로 Visual Studio에서 일반적으로 작업 하는 개발자가 CLI에 콘솔을 사용 하 여 선호 합니다.

> [!Tip]
> 많은 콘솔 작업 알려진된 경로 이름으로 연 Visual Studio에서 솔루션을 갖추는 것에 따라 다릅니다. 저장 되지 않은 솔루션 또는 솔루션이 없는 경우 오류를 볼 수 있습니다, "솔루션이 열려 있지 않거나 저장 되지 않습니다. 있는지 확인 하십시오 열려 있고 저장 된 솔루션입니다. " 이 콘솔은 솔루션 폴더를 확인할 수 없음을 나타냅니다. 저장 되지 않은 솔루션을 저장 하거나 만들고 없는 경우 솔루션을 저장를 열고 오류를 수정 해야 합니다.

## <a name="opening-the-console-and-console-controls"></a>콘솔 및 콘솔 컨트롤 열기

1. Visual Studio를 사용 하 여 콘솔을 열고는 **도구 > NuGet 패키지 관리자 > 패키지 관리자 콘솔** 명령입니다. 그러나 콘솔은 정렬 하 고 원하는 배치 수 있는 Visual Studio 창 (참조 [Visual Studio에서 창 레이아웃 사용자 지정](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).

1. 기본적으로 콘솔 명령 특정 패키지 소스 및 프로젝트에 대해 창의 위쪽에 있는 컨트롤에 설정 된 대로 작동 합니다.

    ![프로젝트 및 패키지 원본에 대 한 패키지 관리자 콘솔을 제어합니다.](media/PackageManagerConsoleControls1.png)

1. 다른 패키지 소스 및/또는 프로젝트를 선택 하면 이후 명령에 대 한 이러한 기본 설정을 변경 합니다. 기본값을 변경 하지 않고 이러한 설정을 overrride 하려면 대부분의 명령은 지원 `-Source` 및 `-ProjectName` 옵션입니다.

1. 패키지 소스를 관리 하려면 기어 아이콘을 선택 합니다. 이 바로 가기는 **도구 > 옵션 > NuGet 패키지 관리자 > 패키지 소스** 대화 상자에 설명 된 대로 [패키지 관리자 UI](package-manager-ui.md#package-sources) 페이지. 또한 프로젝트 선택기의 오른쪽에 컨트롤 콘솔의 내용을 지웁니다.

    ![패키지 관리자 콘솔 설정과 일반 제어](media/PackageManagerConsoleControls2.png)

1. 오른쪽에 있는 단추는 장기 실행 명령을 중단합니다. 예를 들면 `Get-Package -ListAvailable -PageSize 500` 최상위 500 패키지를 실행 하는 데 몇 분 정도 소요 될 수 있습니다 (예: nuget.org), 기본 원본에 대해 나열 합니다.

    ![패키지 관리자 콘솔 중지 제어](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a>패키지 설치

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

참조 [Install-package](../tools/ps-ref-install-package.md)합니다.

에 설명 된 대로 동일한 단계를 수행 하는 콘솔에서 패키지를 설치 [패키지 설치 될 때 어떤 일이 생기](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), 다음 사항이 추가:

- 암시 된 계약의 창에서 해당 사용 조건 콘솔에 표시 됩니다. 약관에 동의 하지 않는 경우 패키지를 즉시 제거 해야 합니다.
- 또한 패키지에 대 한 참조를 프로젝트 파일에 추가 되 고 표시 **솔루션 탐색기** 아래는 **참조** 직접 프로젝트 파일에서 변경 내용을 보려면 프로젝트를 저장 해야 하는 노드를 합니다.

## <a name="uninstalling-a-package"></a>패키지를 제거합니다.

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

참조 [Uninstall-package](../tools/ps-ref-uninstall-package.md)합니다. 사용 하 여 [패키지 가져오기](../tools/ps-ref-get-package.md) 현재 식별자를 찾을 해야 할 경우 기본 프로젝트에 설치 된 모든 패키지를 확인할 수 있습니다.

패키지를 제거 합니다. 다음 작업을 수행 합니다.

- 프로젝트 (및 사용 되 고 모든 관리 형식)에서 패키지에 대 한 참조를 제거 합니다. 에 표시 되지 않는 참조 **솔루션 탐색기**합니다. (프로젝트 참조에서 제거를 다시 작성 해야 할 수도 있습니다는 **Bin** 폴더입니다.)
- 변경 내용이 취소 `app.config` 또는 `web.config` 패키지가 설치 된 경우.
- 나머지 패키지 해당 종속성을 사용 하는 경우 종속성을 제거 이전에 설치 합니다.

## <a name="updating-a-package"></a>패키지를 업데이트합니다.

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

참조 [패키지 가져오기](../tools/ps-ref-get-package.md) 및 [업데이트 패키지](../tools/ps-ref-update-package.md)

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

참조 [Find-package](../tools/ps-ref-find-package.md)합니다. Visual Studio 2013 및 이전 버전에서 사용 하 여 [패키지 가져오기](../tools/ps-ref-get-package.md) 대신 합니다.

## <a name="availability-of-the-console"></a>콘솔의 가용성

Visual Studio 2017 NuGet 및 NuGet 패키지 관리자는 자동으로 설치 어떤를 선택 합니다. NET 관련 작업; 설치할 수 있습니다도 개별적으로 확인 하 여는 **개별 구성 요소 > 코드 도구 > NuGet 패키지 관리자** Visual Studio 2017 설치 관리자에 대 한 옵션입니다.

NuGet 패키지 관리자 및 이전 버전 Visual Studio 2015에서 누락 된 하는 경우 확인 **도구 > 확장 및 업데이트 중...**  NuGet 패키지 관리자 확장에 대 한 검색 합니다. Visual studio에서 확장명 설치 관리자를 사용 하는 경우에에서 직접 확장을 다운로드할 수 있습니다 [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html)합니다.

패키지 관리자 콘솔을 현재 Mac.에 대 한 Visual Studio와 함께 사용할 수 없습니다. 해당 명령 사항은 통해 사용할 수는 [NuGet CLI](nuget-exe-CLI-reference.md)합니다. Mac 용 visual Studio NuGet 패키지 관리를 위한 UI가 있습니다. 참조 [프로젝트에 포함 하는 NuGet 패키지](/visualstudio/mac/nuget-walkthrough)합니다.

패키지 관리자 콘솔을 Visual Studio 코드 포함 되지 않습니다.

## <a name="extending-the-package-manager-console"></a>패키지 관리자 콘솔을 확장합니다.

일부 패키지는 콘솔에 대 한 새 명령을 설치합니다. 예를 들어 `MvcScaffolding` 과 같은 명령을 만듭니다 `Scaffold` ASP.NET MVC 컨트롤러와 뷰 생성 아래에 표시 합니다.

![설치 및 MvcScaffold 사용](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a>NuGet PowerShell 프로 파일 설정

PowerShell 프로필에는 PowerShell을 사용 하 여 때마다 일반적으로 사용 되는 명령을 사용할 수 있도록 수 있습니다. NuGet에서는 일반적으로 다음 위치에서 발견 하는 NuGet 특정 프로필을 지원 합니다.

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

프로필을 찾으려면 입력 `$profile` 콘솔에서:

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

자세한 내용은 참조 [Windows PowerShell 프로필](https://technet.microsoft.com/library/bb613488.aspx)합니다.

## <a name="using-the-nugetexe-cli-in-the-console"></a>콘솔에서 nuget.exe CLI를 사용 하 여

확인 하는 [ `nuget.exe` CLI](nuget-exe-cli-reference.md) 패키지 관리자 콘솔에서 사용할 수 있는 설치는 [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) 콘솔에서 패키지:

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
