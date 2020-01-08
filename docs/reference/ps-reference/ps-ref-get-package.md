---
title: NuGet Get 패키지 PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에 있는 Get Package PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 1c39fea2131b8f4b8a91314347a19366d5a582c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385195"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Visual Studio의 패키지 관리자 콘솔)

*이 항목에서는 Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내의 명령을 설명 합니다. 일반 PowerShell 가져오기 패키지 명령의 경우 [Powershell PackageManagement 참조](/powershell/module/packagemanagement/?view=powershell-6)를 참조 하세요.*

로컬 리포지토리에 설치 된 패키지 목록을 검색 하 고-ListAvailable 스위치와 함께 사용 하는 경우 패키지 원본에서 사용할 수 있는 패키지를 나열 하거나-Update 스위치와 함께 사용 하는 경우 사용 가능한 업데이트를 나열 합니다.

## <a name="syntax"></a>구문

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

매개 변수 없이 `Get-Package` 기본 프로젝트에 설치 된 패키지 목록을 표시 합니다.

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| 소스 | 패키지에 대 한 URL 또는 폴더 경로입니다. 로컬 폴더 경로는 절대 경로 이거나 현재 폴더에 대 한 상대 경로일 수 있습니다. 생략 하는 경우 `Get-Package`는 현재 선택 된 패키지 소스를 검색 합니다. -ListAvailable와 함께 사용 하는 경우 기본값은 nuget.org입니다. |
| ListAvailable | 패키지 원본에서 사용할 수 있는 패키지를 나열 하 고 기본적으로 nuget.org를 사용 합니다. -PageSize 및/또는-First가 지정 되지 않은 경우 50 패키지의 기본값을 표시 합니다. |
| Updates | 패키지 원본에서 업데이트를 사용할 수 있는 패키지를 나열 합니다. |
| ProjectName | 설치 된 패키지를 가져올 프로젝트입니다. 생략 하는 경우 전체 솔루션에 대해 설치 된 프로젝트를 반환 합니다. |
| 필터 | 패키지 ID, 설명 및 태그에 필터를 적용 하 여 패키지 목록의 범위를 좁히는 데 사용 되는 필터 문자열입니다. |
| First | 목록의 처음부터 반환할 패키지 수입니다. 지정 하지 않으면 기본값은 50입니다. |
| 건너뛰기 | 표시 된 목록에서 첫 번째 &lt;int&gt; 패키지를 생략 합니다.  |
| AllVersions | 최신 버전 뿐 아니라 각 패키지의 사용 가능한 모든 버전을 표시 합니다. |
| IncludePrerelease | 결과에 시험판 패키지를 포함 합니다. |
| PageSize | *(3.0 이상)* -ListAvailable (필수)와 함께 사용 하는 경우 계속 하 라는 프롬프트를 제공 하기 전에 나열할 패키지의 수입니다. |

이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.

## <a name="common-parameters"></a>일반 매개 변수

`Get-Package`는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](https://go.microsoft.com/fwlink/?LinkID=113216)를 지원 합니다.

## <a name="examples"></a>예

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
