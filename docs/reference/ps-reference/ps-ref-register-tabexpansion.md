---
title: NuGet 레지스터-TabExpansion PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 Register-TabExpansion PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 37aed96760e642b03c02bf31fe47a54f0e3cb74a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384456"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>레지스터-TabExpansion (Visual Studio의 패키지 관리자 콘솔)

*Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내 에서만 사용할 수 있습니다.*

지정 된 명령의 매개 변수에 대 한 탭 확장을 등록 합니다. 예를 들어 명령을 입력할 때 Tab 키를 사용 하는 경우 확장 된 값이 해당 매개 변수에 사용할 수 있는 옵션으로 표시 됩니다. 명령에 대 한 모든 이전 확장을 덮어씁니다.

## <a name="syntax"></a>구문

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| 이름 | 하다 확장을 등록할 명령입니다. -Name 스위치 자체는 선택 사항입니다. |
| 정의 | 하다 구문에서 인수를 설명 하는 개체 `@{'<parameter>' = {'<value1>', '<value2>', ...}}` `<parameter>`는 수정할 매개 변수의 이름이 고 각 `<value>`는 특정 확장을 제공 합니다. 작은따옴표와 큰따옴표가 모두 허용 됩니다. |

이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.

## <a name="common-parameters"></a>일반 매개 변수

`Register-TabExpansion`는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](https://go.microsoft.com/fwlink/?LinkID=113216)를 지원 합니다.

## <a name="examples"></a>예

EventManager, 유틸리티 및 SpecialParser의 세 가지 프로젝트 이름을 포함 하는 솔루션을 고려 합니다. 개발자는 이러한 각 프로젝트와 함께 다양 한 시간에 `Update-Package` 명령을 사용 하는 경우가 많습니다. `Update-Package` 명령이 `-ProjectName` 인수에 대 한 자동 완성 확장 기능을 제공 하 여 매번 프로젝트 이름을 입력할 필요가 없도록 하는 것이 편리 하다는 것을 알게 되었습니다. 

다음 명령에서는 이러한 세 개의 프로젝트 이름을 `-ProjectName` 매개 변수에 대 한 확장으로 등록 합니다.

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

그러면 개발자는 `Update-Package -ProjectName `를 입력 하 고 Tab 키를 눌러 자동 완성 옵션으로 제공 된 확장을 볼 수 있습니다.

![레지스터 탭 확장 사용 예](media/Register-TabExpansion-Example.png)
