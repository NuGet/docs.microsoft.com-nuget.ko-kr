---
title: NuGet Install-package PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 Install-package PowerShell 명령에 대 한 참조입니다.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5adfbcae0affcaa402f7981c12e108490d546511
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Visual Studio의 패키지 관리자 콘솔)

*이 항목에서는 내에서 명령을 설명에서 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows에서 Visual Studio에서 합니다. 일반 PowerShell Install-package 명령에 대 한 참조는 [PowerShell PackageManagement 참조](/powershell/module/packagemanagement/?view=powershell-6)합니다.*

프로젝트에 패키지 및 해당 종속성을 설치합니다.

## <a name="syntax"></a>구문

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

NuGet 2.8 +에서 `Install-Package` 프로젝트에서 기존 패키지를 다운 그레이드할 수 있습니다. 예를 들어 Microsoft.AspNet.MVC 5.1.0-rc1 설치 되어 있는 경우 다음 명령을에 다운 그레이드 5.0.0에:

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| ID | (필수) 설치할 패키지의 식별자입니다. (*3.0 +*) 식별자 경로 또는 URL 일 수 있습니다는 `packages.config` 파일 또는 `.nupkg` 파일입니다. -Id 스위치 자체는 선택 사항입니다. |
| IgnoreDependencies | 이 패키지만 및 해당 종속성을 설치 합니다. |
| ProjectName | 기본 프로젝트를 패키지를 설치 하는 프로젝트입니다. |
| 소스 | 검색 하기 위해 패키지 원본에 대 한 URL 또는 폴더 경로입니다. 로컬 폴더 경로는 현재 폴더에 상대적 이거나 절대 경로일 수 있습니다. 생략 하면 `Install-Package` 현재 선택된 된 패키지 소스를 검색 합니다. |
| 버전 | 를 설치 하려면 패키지의 버전을 최신 버전을 기본값으로 설정 됩니다. |
| IncludePrerelease | 설치에 시험판 패키지를 고려합니다. 생략 하면 패키지만 고려 됩니다. |
| FileConflictAction | 덮어쓰거나 프로젝트에서 참조 하는 기존 파일을 무시 하도록 요청 시 수행할 동작입니다. 가능한 값은 *덮어쓰기, 건너뛰기, None, OverwriteAll*, 및 *(3.0 이상)* *IgnoreAll*합니다. |
| DependencyVersion | 를 사용 하려면 다음 중 하나일 수 있는 종속성 패키지의 버전:<br/><ul><li>*가장 낮은* (기본값): 최하 버전</li><li>*HighestPatch*: 주요 가장 낮은 가장 낮은 부, 최고의 패치가 포함 된 버전</li><li>*HighestMinor*: 가장 낮은 주 버전과, 가장 높은 보조, 최고의 패치</li><li>*가장 높은* (매개 변수 없이 업데이트 패키지에 대 한 기본값): 가장 높은 버전</li></ul>사용 하 여 기본 값을 설정할 수 있습니다는 [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) 에서 설정 된 `Nuget.Config` 파일입니다. |
| WhatIf | 실제로 설치를 수행 하지 않고 명령을 실행할 때 어떻게 되는지를 보여 줍니다. |

매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.

## <a name="common-parameters"></a>일반 매개 변수

`Install-Package` 다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.

## <a name="examples"></a>예제

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
