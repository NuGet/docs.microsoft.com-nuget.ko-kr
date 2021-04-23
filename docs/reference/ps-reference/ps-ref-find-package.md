---
title: NuGet Find-Package PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 Find-Package PowerShell 명령에 대 한 참조입니다.
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 263835da64340a13737b32ab54ab057cb640a080
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901761"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Visual Studio의 패키지 관리자 콘솔)

*버전 3.0 이상; 이 항목에서는 Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내의 명령을 설명 합니다. 일반 PowerShell Find-Package 명령의 경우 [Powershell PackageManagement 참조](/powershell/module/packagemanagement)를 참조 하세요.*

패키지 원본에서 지정 된 ID 또는 키워드를 사용 하 여 원격 패키지 집합을 가져옵니다.

## <a name="syntax"></a>구문

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| Id &lt; 키워드&gt; | 하다 패키지 소스를 검색할 때 사용할 키워드입니다. 패키지 ID가 키워드와 일치 하는 패키지만 반환 하려면-ExactMatch을 사용 합니다. 키워드를 지정 하지 않으면에서 `Find-Package` 다운로드 하 여 상위 20 개 패키지의 목록을 반환 하거나,-First로 지정 된 숫자를 반환 합니다. -Id는 선택 사항이 며 작동 하지 않습니다. |
| 원본 | 검색할 패키지 원본에 대 한 URL 또는 폴더 경로입니다. 로컬 폴더 경로는 절대 경로 이거나 현재 폴더에 대 한 상대 경로일 수 있습니다. 생략 하면 `Find-Package` 현재 선택 된 패키지 소스를 검색 합니다. |
| AllVersions | 최신 버전 뿐 아니라 각 패키지의 사용 가능한 모든 버전을 표시 합니다. |
| 첫째 | 목록의 처음부터 반환할 패키지 수입니다. 기본값은 20입니다. |
| 건너뛰기 | &lt; &gt; 표시 된 목록에서 첫 번째 int 패키지를 생략 합니다.  |
| IncludePrerelease | 결과에 시험판 패키지를 포함 합니다. |
| ExactMatch | &lt; &gt; 대/소문자를 구분 하는 패키지 ID로 키워드를 사용 하도록 지정 합니다. |
| StartWith | 패키지 ID가 키워드로 시작 하는 패키지를 반환 &lt; &gt; 합니다. |

이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.

## <a name="common-parameters"></a>일반 매개 변수

`Find-Package` 에서는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](/powershell/module/microsoft.powershell.core/about/about_commonparameters)를 지원 합니다.

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