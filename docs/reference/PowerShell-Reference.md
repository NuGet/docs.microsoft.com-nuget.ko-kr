---
title: NuGet PowerShell 참조
description: Visual Studio의 NuGet 패키지 관리자 콘솔에서 사용할 수 있는 PowerShell 명령에 대 한 전체 참조입니다.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 4f8b42847cbc155393fe6d2afbe2e0857b619da3
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236882"
---
# <a name="powershell-reference"></a>PowerShell 참조

패키지 관리자 콘솔은 Windows의 Visual Studio 내 PowerShell 인터페이스를 제공 하 여 아래 나열 된 특정 명령을 통해 NuGet과 상호 작용 합니다. 콘솔은 현재 Mac용 Visual Studio에서 사용할 수 없습니다. 콘솔 사용에 대 한 가이드는 [패키지 관리자 콘솔을 사용 하 여 패키지 설치 및 관리](../consume-packages/install-use-packages-powershell.md) 항목을 참조 하세요.

> [!Tip]
> 모든 PowerShell 명령은 패키지 사용량과만 관련 됩니다. 패키지를 만들고 게시 하는 것과 관련 된 PowerShell 명령은 없습니다. 단, 패키지가 다른 패키지의 소비자 일 수도 있습니다.

> [!Important]
> 여기에 나열 된 명령은 Visual Studio의 패키지 관리자 콘솔과 다르며 일반 PowerShell 환경에서 사용할 수 있는 [패키지 관리 모듈 명령과](/powershell/module/packagemanagement/?view=powershell-6) 다릅니다. 특히, 각 환경에는 사용할 수 없는 명령이 있으며 동일한 이름의 명령은 특정 인수에서 다를 수 있습니다. Visual Studio에서 패키지 관리 콘솔을 사용 하는 경우이 현재 항목에 설명 된 명령 및 인수를 적용 합니다.

| 일반 명령 | Description | NuGet 버전 |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | 패키지와 해당 종속성을 프로젝트에 설치합니다. | 모두 |
| [Update-Package](ps-reference/ps-ref-update-package.md) | 패키지와 해당 종속성 또는 프로젝트의 모든 패키지를 업데이트 합니다. | 모두 |
| [Find-Package](ps-reference/ps-ref-find-package.md) | 패키지 ID 또는 키워드를 사용 하 여 패키지 소스를 검색 합니다. | 3.0+ |
| [Get-Package](ps-reference/ps-ref-get-package.md) | 로컬 리포지토리에 설치 된 패키지 목록을 검색 하거나 패키지 원본에서 사용할 수 있는 패키지를 나열 합니다. | 모두 |

| 보조 명령 | Description | NuGet 버전 |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | 프로젝트의 출력 경로에 있는 모든 어셈블리를 검사 하 고 필요에 따라 또는에 바인딩 리디렉션을 추가 합니다 `app.config` `web.config` . | 모두 |
| [Get-Project](ps-reference/ps-ref-get-project.md) | 기본 또는 지정 된 프로젝트에 대 한 정보를 표시 합니다. | 3.0+ |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | 지정 된 패키지에 대 한 프로젝트, 라이선스 또는 신고 URL을 사용 하 여 기본 브라우저를 시작 합니다. | 3.0 이상에서 사용 되지 않음 |
| [레지스터-TabExpansion](ps-reference/ps-ref-register-tabexpansion.md) | 명령 매개 변수에 대 한 탭 확장을 등록 하 여 일반적으로 사용 되는 매개 변수 값에 대 한 사용자 지정 확장을 만들 수 있도록 합니다. | 모두 |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | 지정 된 프로젝트에서 설치 된 패키지 버전을 가져오고 솔루션의 나머지 프로젝트에 버전을 동기화 합니다. | 3.0+ |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | 프로젝트에서 패키지를 제거 하 고 필요에 따라 해당 종속성을 제거 합니다. | 모두 |

콘솔 내에서 이러한 명령에 대 한 자세한 도움말을 보려면 명령 이름으로 다음을 실행 하면 됩니다.

```ps
Get-Help <command> -full
```

모든 패키지 관리자 콘솔 명령은 다음과 같은 [일반적인 PowerShell 매개 변수](/powershell/module/microsoft.powershell.core/about/about_commonparameters)를 지원 합니다.

- 디버그
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- 자세히
- WarningAction
- WarningVariable

자세한 내용은 PowerShell 설명서의 [about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters) 을 참조 하세요.