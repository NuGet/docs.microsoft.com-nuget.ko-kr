---
title: NuGet Uninstall-package PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 Uninstall-package PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: c95479103be2cba3b4eb6964ea761870477863bd
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842469"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Visual Studio의 패키지 관리자 콘솔)

*내에서 명령에 설명 합니다 [패키지 관리자 콘솔](package-manager-console.md) Windows의 Visual Studio에서 합니다. 일반 PowerShell Uninstall-package 명령에 대 한 참조를 [PowerShell PackageManagement 참조](/powershell/module/packagemanagement/?view=powershell-6)합니다.*

필요에 따라 해당 종속성을 제거 하는 프로젝트에서 패키지를 제거 합니다. 하지 않는 한 다른 패키지에이 패키지에 의존 하는 경우 명령이 실패 – Force 옵션을 지정 합니다.

## <a name="syntax"></a>구문

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

하지 않는 한 다른 패키지에이 패키지에 의존 하는 경우 명령이 실패 – Force 옵션을 지정 합니다.

## <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --- | --- |
| ID | (필수) 제거할 패키지의 식별자입니다. -Id 자체 스위치는 선택 사항입니다. |
| 버전 | 를 제거 하려면 패키지 버전을 현재 설치 된 버전을 기본값으로 설정 합니다. |
| RemoveDependencies | 패키지 및 해당 사용 되지 않는 종속성을 제거 합니다. 즉, 모든 종속성에 종속 된 다른 패키지에 있으면이 건너뜁니다. |
| ProjectName | 기본 프로젝트에 기본적으로 패키지를 제거 하는 프로젝트입니다. |
| Force | 다른 패키지에 의존 하는 경우에 제거할 패키지를 강제로 수행 합니다. |
| Whatif | 실제로 제거를 수행 하지 않고 명령을 실행할 때 발생할 상황을 보여 줍니다. |

이러한 매개 변수 중 파이프라인 입력 하거나 와일드 카드 문자 허용 합니다.

## <a name="common-parameters"></a>일반 매개 변수

`Uninstall-Package` 다음을 지원 합니다 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable.

## <a name="examples"></a>예

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
