---
title: NuGet Add-BindingRedirect PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 Add-BindingRedirect PowerShell 명령에 대 한 참조입니다.
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 62edf1bf8995a4e1ffb83acc7a7621a786cc53e4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777618"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a>Add-BindingRedirect (Visual Studio의 패키지 관리자 콘솔)

*Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내 에서만 사용할 수 있습니다.*

프로젝트의 출력 경로에 있는 모든 어셈블리를 검사 하 고 필요한 경우 응용 프로그램이 나 웹 구성 파일에 바인딩 리디렉션을 추가 합니다. 이 명령은 패키지를 설치할 때 자동으로 실행 됩니다.

> [!NOTE]
> 이는 packages.config 파일을 사용 하는 시나리오에만 적용 됩니다. 자세한 내용은 [NuGet packages.config 파일 참조](~/reference/packages-config.md)를 참조 하세요.

바인딩 리디렉션 및 사용 이유에 대 한 자세한 내용은 .NET 설명서의 [어셈블리 버전 리디렉션](/dotnet/framework/configure-apps/redirect-assembly-versions) 을 참조 하세요.

## <a name="syntax"></a>구문

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --- | --- |
| ProjectName | 하다 바인딩 리디렉션을 추가할 프로젝트입니다. -ProjectName 스위치 자체는 선택 사항입니다. |

이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.

## <a name="common-parameters"></a>일반 매개 변수

`Add-BindingRedirect` 에서는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](/powershell/module/microsoft.powershell.core/about/about_commonparameters)를 지원 합니다.

## <a name="examples"></a>예

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```