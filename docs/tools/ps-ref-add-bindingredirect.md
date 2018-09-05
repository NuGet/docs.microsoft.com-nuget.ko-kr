---
title: NuGet 추가 BindingRedirect PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 추가 BindingRedirect PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: dec7db04c5cf239863b9c00e9f5bc0dde42c7e47
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551659"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (Visual Studio의 패키지 관리자 콘솔)

*내 에서만 사용 가능 합니다 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows의 Visual Studio에서 합니다.*

프로젝트의 출력 경로 내의 모든 어셈블리를 검사 하 고 필요한 경우 응용 프로그램 또는 웹 구성 파일에 바인딩 리디렉션을 추가 합니다. 이 명령은 패키지를 설치할 때 자동으로 실행 됩니다.

바인딩 리디렉션 및 사용 되는 이유에 대 한 내용은 참조 하세요 [어셈블리 버전 리디렉션](/dotnet/framework/configure-apps/redirect-assembly-versions) .NET 설명서에서.

## <a name="syntax"></a>구문

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| ProjectName | (필수) 프로젝트를 바인딩 리디렉션을 추가할 위치입니다. -ProjectName 스위치 자체가 선택 사항입니다. |

이러한 매개 변수 중 파이프라인 입력 하거나 와일드 카드 문자 허용 합니다.

## <a name="common-parameters"></a>일반 매개 변수

`Add-BindingRedirect` 다음을 지원 합니다 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, 자세한 정보 표시, WarningAction, WarningVariable.

## <a name="examples"></a>예제

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```