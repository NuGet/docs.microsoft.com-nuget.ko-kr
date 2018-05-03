---
title: NuGet 레지스터 TabExpansion PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 레지스터 TabExpansion PowerShell 명령에 대 한 참조입니다.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 02f6d4ecd246b7ce5425cf56ade10789cf03113c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>등록 키를 누른 채 TabExpansion (Visual Studio에서 패키지 관리자 콘솔)

*내 에서만 사용할 수는 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows에서 Visual Studio에서 합니다.*

확장 된 값이 해당 매개 변수에 대해 사용할 수 있는 옵션으로 표시 탭 명령을 입력할 때 사용 되 면 되도록 지정 된 매개 변수에 대해 탭 확장을 등록 합니다. 명령에 대 한 모든 이전 확장을 덮어씁니다.

## <a name="syntax"></a>구문

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| 이름 | (필수) 확장을 등록할 수 있는 명령입니다. -Name 자체 스위치는 선택 사항입니다. |
| 정의 | (필수) 구문에 대 한 인수를 설명 하는 개체 `@{'<parameter>' = {'<value1>', '<value2>', ...}}` 여기서 `<parameter>` 매개 변수를 수정 하 고 각각의 이름인 `<value>` 특정 확장을 제공 합니다. 작은따옴표와 큰따옴표가 허용 됩니다. |

매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.

## <a name="common-parameters"></a>일반 매개 변수

`Register-TabExpansion` 다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.

## <a name="examples"></a>예제

프로젝트 이름 EventManager, 유틸리티 및 SpecialParser 3 개를 포함 하는 솔루션을 고려 합니다. 개발자는 주로 사용은 `Update-Package` 각각의 해당 프로젝트와 다른 시간에 명령 합니다. 가 편리 하 게 찾습니다 그녀는 `Update-Package` 명령에 대 한 자동 완성 기능 확장을 제공는 `-ProjectName` 인수 하므로 매번 프로젝트 이름을 입력 필요 하지 않습니다. 

다음 명령에 대 한 확장으로 이러한 세 개의 프로젝트 이름을 만든 다음,으로 등록 된 `-ProjectName` 매개 변수:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

개발자 입력할 수 `Update-Package -ProjectName `, tab 키를 및 자동 완성 옵션으로 제공 하는 확장을 참조 하십시오.

![레지스터 TabExpansion 사용의 예](media/Register-TabExpansion-Example.png)
