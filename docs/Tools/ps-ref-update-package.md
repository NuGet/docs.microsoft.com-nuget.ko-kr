---
title: "NuGet 업데이트 패키지 PowerShell 참조 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b4aa92a9-ce47-4d23-ae51-d5683e08a9d5
description: "Visual Studio에서 NuGet 패키지 관리자 콘솔에 업데이트 패키지 PowerShell 명령에 대 한 참조입니다."
keywords: "NuGet 패키지 관리자 콘솔, NuGet Powershell 명령, NuGet Powershell 참조에 업데이트 패키지"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 71f5cd7061e0f765d8808db8a3798657a941ba14
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2017
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>업데이트 패키지 (Visual Studio에서 패키지 관리자 콘솔)

*내 에서만 사용할 수는 [NuGet 패키지 관리자 콘솔](Package-Manager-Console.md) Windows에서 Visual Studio에서 합니다.*

패키지 및 해당 종속 항목 또는 프로젝트에서 모든 패키지를 최신 버전으로 업데이트합니다.

## <a name="syntax"></a>구문

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

NuGet 2.8 +에서 `Update-Package` 는 프로젝트에서 기존 패키지를 다운 그레이드 하는 데 사용할 수 있습니다. 예를 들어 Microsoft.AspNet.MVC 5.1.0-rc1 설치 되어 있는 경우 다음 명령을에 다운 그레이드 5.0.0에:

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

2.7 및 이전 버전의 NuGet을 최신 버전이 이미 설치 되어 있는지 라는 오류가 제공 합니다.

## <a name="parameters"></a>매개 변수

|  매개 변수 | 설명 |
| --- | --- |
| ID | 업데이트할 패키지의 식별자입니다. 생략 하면 모든 패키지를 업데이트 합니다. -Id 스위치 자체는 선택 사항입니다. |
| IgnoreDependencies | 업데이트 패키지의 종속성을 건너뜁니다. |
| ProjectName | 업데이트할 패키지가 포함 된, 모든 프로젝트를 프로젝트의 이름입니다. |
| 버전 | 를 업그레이드 하는 최신 버전으로 기본 설정에 사용할 버전입니다. NuGet 3.0 +에서 버전 값 중 하나 여야 합니다 *Lowest, 최고, HighestMinor*, 또는 *HighestPatch* (에서-Safe와 동일). |
| 안전 | 유일한 버전 현재 설치 된 패키지와 같은 주 / 부 버전으로 업그레이드를 제한합니다. |
| 소스 | 검색 하기 위해 패키지 원본에 대 한 URL 또는 폴더 경로입니다. 로컬 폴더 경로는 현재 폴더에 상대적 이거나 절대 경로일 수 있습니다. 생략 하면 `Uninstall-Package` 현재 선택된 된 패키지 소스를 검색 합니다. |
| IncludePrerelease | 업데이트에 대 한 시험판 패키지를 포함합니다. |
| 다시 설치 | 현재 설치 된 버전을 사용 하 여 Resintalls 패키지 합니다. 참조 [다시 설치 후 패키지를 업데이트 하 고](../consume-packages/reinstalling-and-updating-packages.md)합니다. |
| FileConflictAction | 덮어쓰거나 프로젝트에서 참조 하는 기존 파일을 무시 하도록 요청 시 수행할 동작입니다. 가능한 값은 *덮어쓰기, 건너뛰기, None, OverwriteAll*, 및 *IgnoreAll* (3.0 이상)입니다. |
| DependencyVersion | 를 사용 하려면 다음 중 하나일 수 있는 종속성 패키지의 버전:<br/><ul><li>*가장 낮은* (기본값): 최하 버전</li><li>*HighestPatch*: 주요 가장 낮은 가장 낮은 부, 최고의 패치가 포함 된 버전</li><li>*HighestMinor*: 가장 낮은 주 버전과, 가장 높은 보조, 최고의 패치</li><li>*가장 높은* (매개 변수 없이 업데이트 패키지에 대 한 기본값): 가장 높은 버전</li></ul>사용 하 여 기본 값을 설정할 수 있습니다는 [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) 에서 설정 된 `Nuget.Config` 파일입니다. |
| ToHighestPatch | 현재 설치 된 패키지와 동일한 부 버전으로 버전에 업그레이드를 제한 합니다. |
| ToHighestMinor | 만 버전 현재 설치 된 패키지와 같은 주 버전으로 업그레이드를 제한합니다. |
| WhatIf | 실제로 업데이트를 수행 하지 않고 명령을 실행할 때 어떻게 되는지를 보여 줍니다. |

매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.

### <a name="common-parameters"></a>일반 매개 변수

`Update-Package`다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.

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