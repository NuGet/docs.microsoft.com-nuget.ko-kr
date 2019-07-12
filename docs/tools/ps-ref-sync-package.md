---
title: NuGet 패키지 동기화 PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 동기화 패키지 PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: de0b612e1335cafdcd6a0b802d54f2182d27ad22
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842257"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (Visual Studio의 패키지 관리자 콘솔)

*버전 3.0 이상; 내 에서만 사용 가능 합니다 [패키지 관리자 콘솔](package-manager-console.md) Windows의 Visual Studio에서 합니다.*

프로젝트 하 고 버전 솔루션에서 프로젝트의 나머지 부분을 동기화 하는 지정 된 (또는 기본)에서 설치 된 패키지의 버전을 가져옵니다.

## <a name="syntax"></a>구문

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| ID | (필수) 동기화 하는 패키지의 식별자입니다. -Id 자체 스위치는 선택 사항입니다. |
| IgnoreDependencies | 이 패키지에만 및 해당 종속성 없습니다를 설치 합니다. |
| ProjectName | 프로젝트에서 패키지를 기본 프로젝트 기본값으로 동기화입니다. |
| 버전 | 동기화 하는 패키지의 버전 현재 설치 된 버전을 기본값으로 설정 합니다. |
| Source | 검색할 패키지 원본에 대 한 URL 또는 폴더 경로입니다. 로컬 폴더 경로 현재 폴더에 상대적 이거나 절대 경로일 수 있습니다. 생략 하면 `Sync-Package` 현재 선택된 된 패키지 소스를 검색 합니다. |
| IncludePrerelease | 동기화에 시험판 패키지를 포함합니다. |
| FileConflictAction | 덮어쓰거나 프로젝트에서 참조 하는 기존 파일을 무시 하 라는 메시지가 표시 되는 경우 수행할 동작입니다. 가능한 값은 *덮어쓰기, Ignore, None, OverwriteAll*, 및 *(3.0 이상)* *IgnoreAll*합니다. |
| DependencyVersion | 다음 중 하나일 수 있습니다를 사용 하려면 종속성 패키지의 버전:<br/><ul><li>*가장 낮은* (기본값): 가장 낮은 버전</li><li>*HighestPatch*: 가장 낮은 주요, 가장 낮은 부 최고 패치 버전</li><li>*HighestMinor*: 가장 낮은 주 버전, 가장 높은 보조, 최고의 패치</li><li>*가장 높은* (매개 변수 없이 사용 하 여 업데이트 패키지에 대 한 기본값): 가장 높은 버전</li></ul>사용 하 여 기본 값을 설정할 수 있습니다 합니다 [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section) 에서 설정 된 `Nuget.Config` 파일. |
| Whatif | 실제로 동기화를 수행 하지 않고 명령을 실행할 때 발생할 상황을 보여 줍니다. |

이러한 매개 변수 중 파이프라인 입력 하거나 와일드 카드 문자 허용 합니다.

## <a name="common-parameters"></a>일반 매개 변수

`Sync-Package` 다음을 지원 합니다 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable.

## <a name="examples"></a>예

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
