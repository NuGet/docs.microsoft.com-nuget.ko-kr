---
title: NuGet 오픈 PackagePage PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 오픈 PackagePage PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e64a83c01a7baac330c99fe40ba52f328a2133b8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817722"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Visual Studio의 패키지 관리자 콘솔)

*3.0 +;에서 사용 되지 않습니다. 내 에서만 사용할 수는 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows에서 Visual Studio에서 합니다.*

프로젝트, 라이선스 또는 지정된 된 패키지에 대 한 보고서 남용 URL을 사용 하 여 기본 브라우저를 시작합니다.

## <a name="syntax"></a>구문

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| ID | 원하는 패키지의 패키지 ID입니다. -Id 스위치 자체는 선택 사항입니다. |
| 버전 | 최신 버전을 기본값으로 패키지의 버전입니다. |
| 소스 | 원본 드롭다운 목록에서에서 선택 된 소스를 패키지 원본입니다. |
| 라이선스 | 패키지의 라이선스 URL로 브라우저를 엽니다. -라이선스 아니고-ReportAbuse를 지정 하는 경우 패키지의 프로젝트 URL 브라우저에 열립니다. |
| ReportAbuse | 패키지의 보고서 남용 URL로 브라우저를 엽니다. -라이선스 아니고-ReportAbuse를 지정 하는 경우 패키지의 프로젝트 URL 브라우저에 열립니다. |
| PassThru | 표시 됩니다. 브라우저를 열지 않으려면-whatif를 지원함을 사용 합니다. |

매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.

## <a name="common-parameters"></a>일반 매개 변수

`Open-PackagePage` 다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.

## <a name="examples"></a>예제

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```