---
title: NuGet 등록 TabExpansion PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 등록 TabExpansion PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 98171c598bd4a3468bd23e2d6060e267c38021b4
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546607"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>등록 키를 누른 채 TabExpansion (Visual Studio에서 패키지 관리자 콘솔)

*내 에서만 사용 가능 합니다 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows의 Visual Studio에서 합니다.*

명령을 입력 하는 경우 탭을 사용 하면 해당 매개 변수에 대해 사용 가능한 옵션으로 확장된 값이 표시 되도록 지정 된 명령의 매개 변수에 대해 탭 확장을 등록 합니다. 명령에 대 한 모든 이전 확장을 덮어씁니다.

## <a name="syntax"></a>구문

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| 이름 | (필수) 확장을 등록 하는 명령입니다. -Name 자체 스위치는 선택 사항입니다. |
| 정의 | (필수) 구문에서 인수를 설명 하는 개체 `@{'<parameter>' = {'<value1>', '<value2>', ...}}` 여기서 `<parameter>` 매개 변수를 수정 하 고 각각의 이름은 `<value>` 특정 확장을 제공 합니다. 모두 작은따옴표와 큰따옴표 허용 됩니다. |

이러한 매개 변수 중 파이프라인 입력 하거나 와일드 카드 문자 허용 합니다.

## <a name="common-parameters"></a>일반 매개 변수

`Register-TabExpansion` 다음을 지원 합니다 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, 자세한 정보 표시, WarningAction, WarningVariable.

## <a name="examples"></a>예제

프로젝트 이름 EventManager, 유틸리티 및 SpecialParser 3 개를 포함 하는 솔루션을 고려 합니다. 개발자가 자주 사용 하는 `Update-Package` 각 해당 프로젝트를 사용 하 여 서로 다른 시간에 명령 합니다. 있으면 편리 찾습니다 그녀는 `Update-Package` 명령에 대 한 자동 완성 확장을 제공 합니다 `-ProjectName` 인수 그녀 때마다 프로젝트 이름을 입력할 필요가 없도록 합니다. 

다음 명령을 그런 다음 이러한 세 가지 프로젝트 이름에 대 한 확장으로 등록 된 `-ProjectName` 매개 변수:

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

개발자 수 입력 `Update-Package -ProjectName `, tab 키를 누르고, 및 자동 완성 옵션으로 제공 되는 확장을 참조 하세요.

![등록 TabExpansion를 사용 하는 예제](media/Register-TabExpansion-Example.png)
