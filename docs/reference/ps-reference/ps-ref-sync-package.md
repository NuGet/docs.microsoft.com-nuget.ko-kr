---
title: NuGet 동기화-패키지 PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 동기화 패키지 PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 12a3d5f32056539a75da9e17b15d67e72a8a42c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384905"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (Visual Studio의 패키지 관리자 콘솔)

*버전 3.0 이상; Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내 에서만 사용할 수 있습니다.*

지정 된 (또는 기본) 프로젝트에서 설치 된 패키지의 버전을 가져오고 솔루션의 나머지 프로젝트와 버전을 동기화 합니다.

## <a name="syntax"></a>구문

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| ID | 하다 동기화 할 패키지의 식별자입니다. -Id 스위치 자체는 선택 사항입니다. |
| IgnoreDependencies | 해당 종속성이 아닌이 패키지만 설치 합니다. |
| ProjectName | 패키지를 동기화 할 프로젝트입니다. 기본값은 기본 프로젝트입니다. |
| Version | 동기화 할 패키지의 버전으로, 현재 설치 된 버전을 기본값으로 합니다. |
| 소스 | 검색할 패키지 원본에 대 한 URL 또는 폴더 경로입니다. 로컬 폴더 경로는 절대 경로 이거나 현재 폴더에 대 한 상대 경로일 수 있습니다. 생략 하는 경우 `Sync-Package`는 현재 선택 된 패키지 소스를 검색 합니다. |
| IncludePrerelease | 동기화에 시험판 패키지를 포함 합니다. |
| FileConflictAction | 프로젝트에서 참조 하는 기존 파일을 덮어쓰거나 무시 하도록 요청 된 경우 수행할 작업입니다. 가능한 값은 *Overwrite, Ignore, None, OverwriteAll*및 *(3.0 +)* *ignoreall*입니다. |
| DependencyVersion | 사용할 종속성 패키지의 버전은 다음 중 하나일 수 있습니다.<br/><ul><li>*가장 낮음* (기본값): 가장 낮은 버전</li><li>*HighestPatch*: 최하위 주, 최저 부, 최고 패치가 있는 버전</li><li>*HighestMinor*: 최하위 주, 가장 높은 부, 최고 패치가 있는 버전</li><li>*최상* (매개 변수가 없는 업데이트-패키지의 기본값): 가장 높은 버전</li></ul>`Nuget.Config` 파일의 [`dependencyVersion`](../nuget-config-file.md#config-section) 설정을 사용 하 여 기본값을 설정할 수 있습니다. |
| Whatif | 실제로 동기화를 수행 하지 않고 명령을 실행할 때 발생 하는 상황을 보여 줍니다. |

이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.

## <a name="common-parameters"></a>일반 매개 변수

`Sync-Package`는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](https://go.microsoft.com/fwlink/?LinkID=113216)를 지원 합니다.

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
