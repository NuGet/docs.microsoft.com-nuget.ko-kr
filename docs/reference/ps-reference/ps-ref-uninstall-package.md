---
title: NuGet Uninstall-Package PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 Uninstall-Package PowerShell 명령에 대 한 참조입니다.
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 961a9d68e5cba09030401fc871a93bf1145b23a3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777398"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Visual Studio의 패키지 관리자 콘솔)

*이 항목에서는 Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내의 명령을 설명 합니다. 일반 PowerShell Uninstall-Package 명령의 경우 [Powershell PackageManagement 참조](/powershell/module/packagemanagement/?view=powershell-6)를 참조 하세요.*

프로젝트에서 패키지를 제거 하 고 필요에 따라 해당 종속성을 제거 합니다. 이 패키지에 다른 패키지가 종속된 경우 –Force 옵션을 지정하지 않으면 명령이 실패합니다.

## <a name="syntax"></a>Syntax

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

이 패키지에 다른 패키지가 종속된 경우 –Force 옵션을 지정하지 않으면 명령이 실패합니다.

## <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --- | --- |
| Id | 하다 제거할 패키지의 식별자입니다. -Id 스위치 자체는 선택 사항입니다. |
| 버전 | 제거할 패키지의 버전입니다. 기본값은 현재 설치 된 버전입니다. |
| RemoveDependencies | 패키지와 사용 되지 않는 종속성을 제거 합니다. 즉, 종속성에 종속 된 다른 패키지가 있는 경우이를 건너뜁니다. |
| ProjectName | 패키지를 제거할 프로젝트 이며 기본 프로젝트를 기본값으로 합니다. |
| Force | 다른 패키지에 종속 된 경우에도 패키지를 강제로 제거 합니다. |
| WhatIf | 실제로 제거를 수행 하지 않고 명령을 실행할 때 발생 하는 상황을 보여 줍니다. |

이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.

## <a name="common-parameters"></a>일반 매개 변수

`Uninstall-Package` 에서는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](/powershell/module/microsoft.powershell.core/about/about_commonparameters)를 지원 합니다.

## <a name="examples"></a>예

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```