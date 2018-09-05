---
title: NuGet 패키지 가져오기 PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 패키지 가져오기 PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a28b29614dfe5abdeb24438b3451d96634a120db
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551444"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Visual Studio의 패키지 관리자 콘솔)

*내에서 명령에 설명 합니다 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows의 Visual Studio에서 합니다. 일반 PowerShell 패키지 가져오기 명령에 대 한 참조를 [PowerShell PackageManagement 참조](/powershell/module/packagemanagement/?view=powershell-6)합니다.*

로컬 저장소에 설치 된 패키지 목록을 검색 하 고,-ListAvailable 스위치와 함께 사용할 때 패키지 원본에서 사용할 수 있는 패키지를 나열 또는-업데이트 스위치를 사용 하는 경우 사용 가능한 업데이트를 나열 합니다.

## <a name="syntax"></a>구문

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

매개 변수 없이 `Get-Package` 기본 프로젝트에 설치 된 패키지의 목록을 표시 합니다.

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| 소스 | 패키지에 대 한 URL 또는 폴더 경로입니다. 로컬 폴더 경로 현재 폴더에 상대적 이거나 절대 경로일 수 있습니다. 생략 하면 `Get-Package` 현재 선택된 된 패키지 소스를 검색 합니다. -ListAvailable를 함께 사용 하면 nuget.org에 기본값은입니다. |
| ListAvailable | 기본적으로 nuget.org 패키지 원본에서 사용할 수 있는 패키지를 나열 합니다. -PageSize 및/또는-첫 번째는 지정 하지 않으면 기본값은 50 패키지를 보여 줍니다. |
| Updates | 패키지 소스에서 사용 가능한 업데이트가 있는 패키지를 나열 합니다. |
| ProjectName | 설치 된 패키지를 가져올 프로젝트입니다. 생략 하면 반환 전체 솔루션에 대 한 프로젝트를 설치 합니다. |
| 필터 | 패키지 목록 패키지 ID, 설명 및 태그를 적용 하 여 범위를 좁힐 하는 데 사용 하는 필터 문자열입니다. |
| First | 패키지 목록의 시작 부분에서 반환할 수입니다. 지정 하지 않으면 기본값은 50입니다. |
| Skip | 첫 번째 생략 &lt;int&gt; 표시 된 목록에서 패키지 있습니다.  |
| AllVersions | 최신 버전만 대신 각 패키지의 사용 가능한 모든 버전을 표시합니다. |
| IncludePrerelease | 결과에 시험판 패키지를 포함합니다. |
| PageSize | *(3.0 이상)*  사용한-ListAvailable (필수), 패키지 수가 계속할 것인지 묻는 제공 하기 전에 나열 합니다. |

이러한 매개 변수 중 파이프라인 입력 하거나 와일드 카드 문자 허용 합니다.

## <a name="common-parameters"></a>일반 매개 변수

`Get-Package` 다음을 지원 합니다 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, 자세한 정보 표시, WarningAction, WarningVariable.

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
