---
title: NuGet Open-PackagePage PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 Open-PackagePage PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ba90e09c017ec66d73c35a60025474bc77cf65a7
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238064"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Visual Studio의 패키지 관리자 콘솔)

*3.0 이상에서 사용 되지 않음 Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내 에서만 사용할 수 있습니다.*

지정 된 패키지에 대 한 프로젝트, 라이선스 또는 신고 URL을 사용 하 여 기본 브라우저를 시작 합니다.

## <a name="syntax"></a>구문

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --- | --- |
| Id | 원하는 패키지의 패키지 ID입니다. -Id 스위치 자체는 선택 사항입니다. |
| 버전 | 패키지의 버전은 기본적으로 최신 버전을 기본값으로 합니다. |
| 원본 | 원본 드롭다운에서 선택 된 소스를 기본값으로 하는 패키지 원본입니다. |
| 라이선스 | 패키지의 라이선스 URL에 대 한 브라우저를 엽니다. 라이선스와-ReportAbuse 모두 지정 하지 않으면 브라우저에서 패키지의 프로젝트 URL을 엽니다. |
| ReportAbuse | 패키지의 신고 URL에 대 한 브라우저를 엽니다. 라이선스와-ReportAbuse 모두 지정 하지 않으면 브라우저에서 패키지의 프로젝트 URL을 엽니다. |
| PassThru | URL을 표시 합니다. 브라우저를 열지 않으려면-WhatIf를 사용 합니다. |

이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.

## <a name="common-parameters"></a>일반 매개 변수

`Open-PackagePage` 에서는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](/powershell/module/microsoft.powershell.core/about/about_commonparameters)를 지원 합니다.

## <a name="examples"></a>예

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