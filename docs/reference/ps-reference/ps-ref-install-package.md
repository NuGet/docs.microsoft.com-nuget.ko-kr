---
title: NuGet 설치 패키지 PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 설치 패키지 PowerShell 명령에 대 한 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: a65ba63ed070f40e82c43d12e5fad12d86f28112
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384443"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Visual Studio의 패키지 관리자 콘솔)

*이 항목에서는 Windows의 Visual Studio에서 [패키지 관리자 콘솔](../../consume-packages/install-use-packages-powershell.md) 내의 명령을 설명 합니다. 일반 PowerShell 설치 패키지 명령의 경우 [Powershell PackageManagement 참조](/powershell/module/packagemanagement/?view=powershell-6)를 참조 하세요.*

패키지와 해당 종속성을 프로젝트에 설치 합니다.

## <a name="syntax"></a>구문

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

NuGet 2.8 +에서는 프로젝트의 기존 패키지를 다운 그레이드할 수 `Install-Package`. 예를 들어 5.1.0이 설치 되어 있는 경우 다음 명령을 5.0.0로 다운 그레이드 합니다.

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --- | --- |
| ID | 하다 설치할 패키지의 식별자입니다. (*3.0 이상*) 식별자는 `packages.config` 파일 또는 `.nupkg` 파일의 경로 또는 URL이 될 수 있습니다. -Id 스위치 자체는 선택 사항입니다. |
| IgnoreDependencies | 해당 종속성이 아닌이 패키지만 설치 합니다. |
| ProjectName | 패키지를 설치할 프로젝트 이며 기본 프로젝트를 기본값으로 합니다. |
| 소스 | 검색할 패키지 원본에 대 한 URL 또는 폴더 경로입니다. 로컬 폴더 경로는 절대 경로 이거나 현재 폴더에 대 한 상대 경로일 수 있습니다. 생략 하는 경우 `Install-Package`는 현재 선택 된 패키지 소스를 검색 합니다. |
| Version | 설치할 패키지의 버전입니다. 기본값은 최신 버전입니다. |
| IncludePrerelease | 설치를 위한 시험판 패키지를 고려 합니다. 이 매개 변수가 생략되면 정식 버전의 패키지만 적용됩니다. |
| FileConflictAction | 프로젝트에서 참조 하는 기존 파일을 덮어쓰거나 무시 하도록 요청 된 경우 수행할 작업입니다. 가능한 값은 *Overwrite, Ignore, None, OverwriteAll*및 *(3.0 +)* *ignoreall*입니다. |
| DependencyVersion | 사용할 종속성 패키지의 버전은 다음 중 하나일 수 있습니다.<br/><ul><li>*가장 낮음* (기본값): 가장 낮은 버전</li><li>*HighestPatch*: 최하위 주, 최저 부, 최고 패치가 있는 버전</li><li>*HighestMinor*: 최하위 주, 가장 높은 부, 최고 패치가 있는 버전</li><li>*최상* (매개 변수가 없는 업데이트-패키지의 기본값): 가장 높은 버전</li></ul>`Nuget.Config` 파일의 [`dependencyVersion`](../nuget-config-file.md#config-section) 설정을 사용 하 여 기본값을 설정할 수 있습니다. |
| Whatif | 실제로 설치를 수행 하지 않고 명령을 실행할 때 발생 하는 상황을 보여 줍니다. |

이러한 매개 변수는 파이프라인 입력 또는 와일드 카드 문자를 허용 하지 않습니다.

## <a name="common-parameters"></a>일반 매개 변수

`Install-Package`는 디버그, 오류 동작, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction 및 WarningVariable와 같은 [일반적인 PowerShell 매개 변수](https://go.microsoft.com/fwlink/?LinkID=113216)를 지원 합니다.

## <a name="examples"></a>예

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
