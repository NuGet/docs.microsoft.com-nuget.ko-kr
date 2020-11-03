---
title: NuGet Update-Package PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 Update-Package PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: af918d11e8f976be962d52084c5eda4d53e382c6
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238038"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (Visual Studio의 패키지 관리자 콘솔)

*Windows의 Visual Studio에서 [NuGet 패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내 에서만 사용할 수 있습니다.*

패키지와 해당 종속성 또는 프로젝트의 모든 패키지를 최신 버전으로 업데이트 합니다.

## <a name="syntax"></a>구문

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

NuGet 2.8 +에서를 `Update-Package` 사용 하 여 프로젝트의 기존 패키지를 다운 그레이드할 수 있습니다. 예를 들어 5.1.0이 설치 되어 있는 경우 다음 명령을 5.0.0로 다운 그레이드 합니다.

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>매개 변수

|  매개 변수 | Description |
| --- | --- |
| Id | 업데이트할 패키지의 식별자입니다. 생략 하면 모든 패키지를 업데이트 합니다. -Id 스위치 자체는 선택 사항입니다. |
| IgnoreDependencies | 패키지 종속성 업데이트를 건너뜁니다. |
| ProjectName | 업데이트할 패키지를 포함 하는 프로젝트의 이름입니다. 모든 프로젝트를 기본값으로 합니다. |
| 버전 | 업그레이드에 사용할 버전입니다. 기본적으로 최신 버전이 사용 됩니다. NuGet 3.0 이상에서 버전 값은 *최하위, 최고, HighestMinor* 또는 *HighestPatch* 중 하나 여야 합니다 (-Safe와 동일). |
| Safe | 현재 설치 된 패키지와 주 버전과 부 버전이 동일한 버전 으로만 업그레이드를 제한 합니다. |
| 원본 | 검색할 패키지 원본에 대 한 URL 또는 폴더 경로입니다. 로컬 폴더 경로는 절대 경로 이거나 현재 폴더에 대 한 상대 경로일 수 있습니다. 생략 하면 `Update-Package` 현재 선택 된 패키지 소스를 검색 합니다. |
| IncludePrerelease | 업데이트를 위한 시험판 패키지를 포함 합니다. |
| 다시 설치 | 현재 설치 된 버전을 사용 하 여 패키지를 Resintalls 합니다. [패키지 다시 설치 및 업데이트를](../../consume-packages/reinstalling-and-updating-packages.md)참조 하세요. |
| FileConflictAction | 프로젝트에서 참조 하는 기존 파일을 덮어쓰거나 무시 하도록 요청 된 경우 수행할 작업입니다. 가능한 값은 *Overwrite, Ignore, None, OverwriteAll* 및 *ignoreall* (3.0 +)입니다. |
| DependencyVersion | 사용할 종속성 패키지의 버전은 다음 중 하나일 수 있습니다.<br/><ul><li>*가장 낮음* (기본값): 가장 낮은 버전</li><li>*HighestPatch* : 최하위 주, 최저 부, 최고 패치가 있는 버전</li><li>*HighestMinor* : 최하위 주, 가장 높은 부, 최고 패치가 있는 버전</li><li>*가장 높음* (매개 변수가 없는 Update-Package에 대 한 기본값): 가장 높은 버전</li></ul>파일의 설정을 사용 하 여 기본값을 설정할 수 있습니다 [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` . |
| ToHighestPatch | -Safe와 동일 합니다. |
| ToHighestMinor | 업그레이드를 현재 설치 된 패키지와 동일한 주 버전의 버전 으로만 제한 합니다. |
| WhatIf | 실제로 업데이트를 수행 하지 않고 명령을 실행할 때 발생 하는 상황을 보여 줍니다. |

이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.

### <a name="common-parameters"></a>일반 매개 변수

`Update-Package` 에서는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](/powershell/module/microsoft.powershell.core/about/about_commonparameters)를 지원 합니다.

### <a name="examples"></a>예

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package Elmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package Elmah –reinstall -ignoreDependencies
```
