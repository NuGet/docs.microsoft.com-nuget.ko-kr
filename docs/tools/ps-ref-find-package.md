---
title: NuGet 패키지 찾기 PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 Find-package PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: fee0ad0496f27d0796eddf177edc235bcb10da70
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842531"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Visual Studio의 패키지 관리자 콘솔)

*버전 3.0 이상; 내에서 명령에 설명 합니다 [패키지 관리자 콘솔](package-manager-console.md) Windows의 Visual Studio에서 합니다. 일반 PowerShell Find-package 명령에 대 한 참조를 [PowerShell PackageManagement 참조](/powershell/module/packagemanagement/?view=powershell-6)합니다.*

패키지 소스에서 지정 된 ID 또는 키워드를 사용 하 여 원격 패키지 집합을 가져옵니다.

## <a name="syntax"></a>구문

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| Id &lt;키워드&gt; | (필수) 패키지 원본을 검색할 때 사용할 키워드입니다. -ExactMatch를 사용 하 여 패키지 ID를 가진 키워드와 일치 하는 패키지에만 반환 합니다. 키워드 지정 된 경우 `Find-Package` 번호나 다운로드 하 여 상위 20 개 패키지의 목록을 먼저-지정 된 반환 합니다. -Id는 선택 사항 및 작동 하지 않습니다. |
| Source | 검색할 패키지 원본에 대 한 URL 또는 폴더 경로입니다. 로컬 폴더 경로 현재 폴더에 상대적 이거나 절대 경로일 수 있습니다. 생략 하면 `Find-Package` 현재 선택된 된 패키지 소스를 검색 합니다. |
| AllVersions | 최신 버전만 대신 각 패키지의 사용 가능한 모든 버전을 표시합니다. |
| 첫째 | 패키지 목록 시작 부분에서 반환할 수 기본값은 20입니다. |
| Skip | 첫 번째 생략 &lt;int&gt; 표시 된 목록에서 패키지 있습니다.  |
| IncludePrerelease | 결과에 시험판 패키지를 포함합니다. |
| ExactMatch | 사용 하 여 지정한 &lt;키워드&gt; 대/소문자 구분 패키지 ID로 |
| StartWith | 반환 된 패키지 ID가 시작 패키지 &lt;키워드&gt;합니다. |

이러한 매개 변수 중 파이프라인 입력 하거나 와일드 카드 문자 허용 합니다.

## <a name="common-parameters"></a>일반 매개 변수

`Find-Package` 다음을 지원 합니다 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable.

## <a name="examples"></a>예

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```
