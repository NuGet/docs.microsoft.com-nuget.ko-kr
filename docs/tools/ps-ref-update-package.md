---
title: NuGet Update-package PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 Update-package PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a5b5a11ee11d9e2cf6a90d56ac63b1f7bad750ea
ms.sourcegitcommit: 2a9d149bc6f5ff76b0b657324820bd0429cddeef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67496488"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (Visual Studio의 패키지 관리자 콘솔)

*내 에서만 사용 가능 합니다 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows의 Visual Studio에서 합니다.*

최신 버전으로 프로젝트의 모든 패키지 및 해당 종속성 또는 패키지를 업데이트합니다.

## <a name="syntax"></a>구문

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

Nuget 2.8 + `Update-Package` 프로젝트에서 기존 패키지를 다운 그레이드할 수 있습니다. 예를 들어 Microsoft.AspNet.MVC 5.1.0-rc1 설치 된 경우 다음 명령을 다운 그레이드 하 고 5.0.0에:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>매개 변수

|  매개 변수 | 설명 |
| --- | --- |
| ID | 업데이트 패키지의 식별자입니다. 생략 하면 모든 패키지를 업데이트 합니다. -Id 자체 스위치는 선택 사항입니다. |
| IgnoreDependencies | 패키지의 종속성을 업데이트 하는 생략 합니다. |
| ProjectName | 업데이트할 패키지가 포함 된, 모든 프로젝트에 기본적으로 프로젝트의 이름입니다. |
| 버전 | 버전 업그레이드를 최신 버전을 기본값으로 사용입니다. Nuget 3.0 이상에서 버전 값 중 하나 여야 *Lowest, 최고 HighestMinor*, 또는 *HighestPatch* (안전한 간와 같음). |
| 안전 하 게 보호 | 현재 설치 된 패키지와 동일한 주 버전과 부 버전을 사용 하 여 전용 버전에 대 한 업그레이드를 제한합니다. |
| Source | 검색할 패키지 원본에 대 한 URL 또는 폴더 경로입니다. 로컬 폴더 경로 현재 폴더에 상대적 이거나 절대 경로일 수 있습니다. 생략 하면 `Update-Package` 현재 선택된 된 패키지 소스를 검색 합니다. |
| IncludePrerelease | 업데이트에 대 한 시험판 패키지를 포함합니다. |
| 다시 설치 | 현재 설치 된 버전을 사용 하 여 Resintalls 패키지 있습니다. [패키지 다시 설치 및 업데이트](../consume-packages/reinstalling-and-updating-packages.md)를 참조하세요. |
| FileConflictAction | 덮어쓰거나 프로젝트에서 참조 하는 기존 파일을 무시 하 라는 메시지가 표시 되는 경우 수행할 동작입니다. 가능한 값은 *덮어쓰기, Ignore, None, OverwriteAll*, 및 *IgnoreAll* (3.0 이상). |
| DependencyVersion | 다음 중 하나일 수 있습니다를 사용 하려면 종속성 패키지의 버전:<br/><ul><li>*가장 낮은* (기본값): 가장 낮은 버전</li><li>*HighestPatch*: 가장 낮은 주요, 가장 낮은 부 최고 패치 버전</li><li>*HighestMinor*: 가장 낮은 주 버전, 가장 높은 보조, 최고의 패치</li><li>*가장 높은* (매개 변수 없이 사용 하 여 업데이트 패키지에 대 한 기본값): 가장 높은 버전</li></ul>사용 하 여 기본 값을 설정할 수 있습니다 합니다 [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) 에서 설정 된 `Nuget.Config` 파일. |
| ToHighestPatch | -안전에 해당 합니다. |
| ToHighestMinor | 현재 설치 된 패키지와 동일한 주 버전을 사용 하 여 버전에 업그레이드를 제한합니다. |
| Whatif | 실제로 업데이트를 수행 하지 않고 명령을 실행할 때 발생할 상황을 보여 줍니다. |

이러한 매개 변수 중 파이프라인 입력 하거나 와일드 카드 문자 허용 합니다.

### <a name="common-parameters"></a>일반 매개 변수

`Update-Package` 다음을 지원 합니다 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable.

### <a name="examples"></a>예제

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
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```
