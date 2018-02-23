---
title: "NuGet 추가 BindingRedirect PowerShell 참조 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio에서 NuGet 패키지 관리자 콘솔에서 추가 BindingRedirect PowerShell 명령에 대 한 참조입니다."
keywords: "NuGet 패키지 관리자 콘솔에서 NuGet Powershell 명령 추가 BindingRedirect NuGet Powershell 참조"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 41f27d7a1b6b363a562f26590b220d9e11e944f1
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/20/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>추가 BindingRedirect (Visual Studio에서 패키지 관리자 콘솔)

*내 에서만 사용할 수는 [NuGet 패키지 관리자 콘솔](package-manager-console.md) Windows에서 Visual Studio에서 합니다.*

프로젝트에 대 한 출력 경로 내의 모든 어셈블리를 검사 하 고 요소가 필요한 경우 응용 프로그램 또는 웹 구성 파일에 바인딩 리디렉션을 추가 합니다. 이 명령은 패키지를 설치할 때 자동으로 실행 됩니다.

바인딩 리디렉션 및 사용 하는 이유에 대 한 세부 정보를 참조 하십시오. [어셈블리 버전 리디렉션](/dotnet/framework/configure-apps/redirect-assembly-versions) .NET 설명서에 있습니다.

## <a name="syntax"></a>구문

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| ProjectName | (필수) 바인딩 리디렉션을 추가할 프로젝트입니다. 자체-p r o j 스위치는 선택 사항입니다. |

매개 변수가 파이프라인 입력 또는 와일드 카드 문자를 입력할 수 있습니다.

## <a name="common-parameters"></a>일반 매개 변수

`Add-BindingRedirect` 다음과 같은 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216): 디버그, 오류 시 수행할 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, 및 WarningVariable 합니다.

## <a name="examples"></a>예제

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```