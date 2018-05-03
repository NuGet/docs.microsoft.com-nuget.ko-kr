---
title: NuGet Uninstall-package PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔의 제거 패키지 PowerShell 명령에 대 한 참조입니다.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5969526a12cb6e06f23f35a2481d0385bb9780ab
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>(Visual Studio에서 패키지 관리자 콘솔) Uninstall-package

*이 항목에서는 내에서 명령을 설명에서 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows에서 Visual Studio에서 합니다. 일반 PowerShell Uninstall-package 명령에 대 한 참조는 [PowerShell PackageManagement 참조](/powershell/module/packagemanagement/?view=powershell-6)합니다.*

필요에 따라 해당 종속성을 제거 하는 프로젝트에서 패키지를 제거 합니다. 하지 않으면 명령이 실패 합니다 다른 패키지가이 패키지에 종속 되어, 하는 경우 – Force 옵션을 지정 합니다.

## <a name="syntax"></a>구문

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

하지 않으면 명령이 실패 합니다 다른 패키지가이 패키지에 종속 되어, 하는 경우 – Force 옵션을 지정 합니다.

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| ID | (필수) 제거할 패키지의 식별자입니다. -Id 스위치 자체는 선택 사항입니다. |
| 버전 | 버전을 제거 하려면 패키지의 현재 설치 된 버전을 기본값으로 설정 됩니다. |
| RemoveDependencies | 패키지와 그 사용 하지 않는 종속성을 제거 합니다. 즉, 모든 종속성에 의존 하는 다른 패키지,이 건너뜁니다. |
| ProjectName | 기본 프로젝트에 기본값으로 설정 하 고 패키지를 제거할 프로젝트입니다. |
| 강제 | 다른 패키지가 종속 되어 있는 경우에를 제거 해야 패키지를 강제로 합니다. |
| WhatIf | 실제로 제거를 수행 하지 않고 명령을 실행할 때 어떻게 되는지를 보여 줍니다. |

매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.

## <a name="common-parameters"></a>일반 매개 변수

`Uninstall-Package` 다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.

## <a name="examples"></a>예제

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
