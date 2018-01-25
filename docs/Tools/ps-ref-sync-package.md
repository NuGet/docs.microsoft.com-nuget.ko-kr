---
title: "NuGet 동기화 패키지 PowerShell 참조 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio에서 NuGet 패키지 관리자 콘솔에서 동기화 패키지 PowerShell 명령에 대 한 참조입니다."
keywords: "NuGet 패키지 관리자 콘솔, NuGet Powershell 명령, Sync 패키지 NuGet Powershell 참조"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 02233cd0532fab2338e65e0d58b9afc3e2dab6af
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync 패키지 (Visual Studio에서 패키지 관리자 콘솔)

*버전 3.0 +; 내 에서만 사용할 수는 [NuGet 패키지 관리자 콘솔](Package-Manager-Console.md) Windows에서 Visual Studio에서 합니다.*

프로젝트 하 고 버전을 솔루션의 프로젝트의 나머지를 동기화 하는 지정 된 (또는 기본값)에서 설치 된 패키지의 버전을 가져옵니다.

## <a name="syntax"></a>구문

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| ID | (필수) 동기화 할 패키지의 식별자입니다. -Id 스위치 자체는 선택 사항입니다. |
| IgnoreDependencies | 이 패키지만 및 해당 종속성을 설치 합니다. |
| ProjectName | 기본 프로젝트에 기본 설정에서 패키지를 동기화 하는 프로젝트입니다. |
| 버전 | 동기화 되는 데 패키지의 버전은 현재 설치 된 버전을 기본값으로 설정 합니다. |
| 소스 | 검색 하기 위해 패키지 원본에 대 한 URL 또는 폴더 경로입니다. 로컬 폴더 경로는 현재 폴더에 상대적 이거나 절대 경로일 수 있습니다. 생략 하면 `Sync-Package` 현재 선택된 된 패키지 소스를 검색 합니다. |
| IncludePrerelease | Sync에 시험판 패키지를 포함합니다. |
| FileConflictAction | 덮어쓰거나 프로젝트에서 참조 하는 기존 파일을 무시 하도록 요청 시 수행할 동작입니다. 가능한 값은 *덮어쓰기, 건너뛰기, None, OverwriteAll*, 및 *(3.0 이상)* *IgnoreAll*합니다. |
| DependencyVersion | 를 사용 하려면 다음 중 하나일 수 있는 종속성 패키지의 버전:<br/><ul><li>*가장 낮은* (기본값): 최하 버전</li><li>*HighestPatch*: 주요 가장 낮은 가장 낮은 부, 최고의 패치가 포함 된 버전</li><li>*HighestMinor*: 가장 낮은 주 버전과, 가장 높은 보조, 최고의 패치</li><li>*가장 높은* (매개 변수 없이 업데이트 패키지에 대 한 기본값): 가장 높은 버전</li></ul>사용 하 여 기본 값을 설정할 수 있습니다는 [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section) 에서 설정 된 `Nuget.Config` 파일입니다. |
| WhatIf | 실제로 동기화를 수행 하지 않고 명령을 실행할 때 어떻게 되는지를 보여 줍니다. |

매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.

## <a name="common-parameters"></a>일반 매개 변수

`Sync-Package`다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.

## <a name="examples"></a>예제

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
