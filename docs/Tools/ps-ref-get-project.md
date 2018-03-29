---
title: NuGet Get 프로젝트 PowerShell 참조 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 GetProject PowerShell 명령에 대 한 참조입니다.
keywords: NuGet 패키지 관리자 콘솔, NuGet Powershell 명령 가져오기 프로젝트 NuGet Powershell 참조
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 9fcdcf7c550408cd7dfd73787ee14821c46a1df9
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-프로젝트 (Visual Studio에서 패키지 관리자 콘솔)

*내 에서만 사용할 수는 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows에서 Visual Studio에서 합니다.*

기본 또는 지정 된 프로젝트에 대 한 정보를 표시합니다. `Get-Project` 특히 프로젝트에 대 한 Visual Studio DTE (개발 도구 환경) 개체에 참조를 반환합니다.

## <a name="syntax"></a>구문

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| 이름 | 패키지 관리자 콘솔에서 선택 된 기본 프로젝트 기본값으로 표시 하려면 프로젝트를 지정 합니다. -Name 스위치는 선택 사항 자체입니다. |
| 모두 | 솔루션;의 모든 프로젝트에 대 한 정보를 표시합니다. 프로젝트의 순서는 결정적입니다. |

매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.

## <a name="common-parameters"></a>일반 매개 변수

`Get-Project` 다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.

## <a name="examples"></a>예제

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```