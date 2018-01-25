---
title: "NuGet 패키지 가져오기 PowerShell 참조 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio에서 NuGet 패키지 관리자 콘솔에서 패키지 가져오기 PowerShell 명령에 대 한 참조입니다."
keywords: "NuGet 패키지 관리자 콘솔, NuGet Powershell 명령, NuGet Powershell 참조, 패키지 가져오기"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c38e0da2e98d2e5bf5b4fc165462e9abcfdd73c0
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>패키지 가져오기 (Visual Studio에서 패키지 관리자 콘솔)

*이 항목에서는 내에서 명령을 설명에서 [NuGet 패키지 관리자 콘솔](Package-Manager-Console.md) Windows에서 Visual Studio에서 합니다. 일반 PowerShell 패키지 가져오기 명령에 대 한 참조는 [PowerShell PackageManagement 참조](/powershell/module/packagemanagement/?view=powershell-6)합니다.*

로컬 저장소에 설치 된 패키지 목록을 검색 하 고,-ListAvailable 스위치와 함께 사용 하면 패키지 소스에서 사용할 수 있는 패키지를 나열 또는-업데이트 스위치와 함께 사용할 경우 사용 가능한 업데이트를 나열 합니다.

## <a name="syntax"></a>구문

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

매개 변수 없이 `Get-Package` 기본 프로젝트에 설치 된 패키지의 목록이 표시 됩니다.

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| 소스 | 패키지에 대 한 URL 또는 폴더 경로입니다. 로컬 폴더 경로는 현재 폴더에 상대적 이거나 절대 경로일 수 있습니다. 생략 하면 `Get-Package` 현재 선택된 된 패키지 소스를 검색 합니다. -ListAvailable를 함께 사용할 때 nuget.org의 기본값입니다. |
| ListAvailable | Nuget.org를 패키지 소스에서 사용할 수 있는 패키지를 나열 합니다. -PageSize 및/또는-첫 번째는 지정 하지 않으면 기본값은 50 패키지를 보여 줍니다. |
| Updates | 패키지 소스에서 사용 가능한 업데이트가 있는 패키지를 나열 합니다. |
| ProjectName | 설치 된 패키지를 얻을 수 있는 프로젝트입니다. 생략 하면 전체 솔루션에 프로젝트를 설치 된를 반환 합니다. |
| 필터 | 패키지 ID, 설명 및 태그에 적용 하 여 패키지 목록을 줄이는 데 사용 된 필터 문자열입니다. |
| First | 목록 시작 부분부터 반환할 패키지 수입니다. 지정 하지 않으면 기본값은 50입니다. |
| Skip | 첫 번째 생략 &lt;int&gt; 표시 된 목록에서 패키지 합니다.  |
| AllVersions | 최신 버전만 대신 각 패키지의 사용 가능한 모든 버전을 표시합니다. |
| IncludePrerelease | 결과에 시험판 패키지를 포함합니다. |
| PageSize | *(3.0 +)*  계속할 것인지 묻는 제공 하기 전에 나열 하는 패키지 수가-ListAvailable (필수), 함께 사용 하면 됩니다. |

매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.

## <a name="common-parameters"></a>일반 매개 변수

`Get-Package`다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.

## <a name="examples"></a>예제

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```
