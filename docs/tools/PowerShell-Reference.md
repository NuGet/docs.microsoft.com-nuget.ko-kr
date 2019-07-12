---
title: NuGet PowerShell 참조
description: Visual Studio에서 NuGet 패키지 관리자 콘솔에서 사용할 수 있는 PowerShell 명령에 대 한 전체 참조 합니다.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 425ba736eba4609ebd6b5185ae3f1f976ab07a67
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842559"
---
# <a name="powershell-reference"></a>PowerShell 참조

패키지 관리자 콘솔에는 아래에 나열 된 특정 명령을 통해 NuGet을 사용 하 여 상호 작용 하는 Windows에서 Visual Studio 내에서 PowerShell 인터페이스를 제공 합니다. (콘솔은 현재 mac 용 Visual Studio에서 사용할 수 있습니다.) 콘솔을 사용 하 여 지침을 참조 하세요 [설치 패키지 관리자 콘솔을 사용 하 여 패키지를 관리 하 고](../tools/package-manager-console.md) 항목입니다.

> [!Tip]
> 모든 PowerShell 명령 패키지 소비만 관련이 있습니다. PowerShell 명령을 패키지 만들기 및 게시 제외 하는 패키지는 다른 패키지의 소비자를 수도 있습니다와 관련이 있습니다.

> [!Important]
> 여기에 나열 된 명령을 Visual Studio에서 패키지 관리자 콘솔에 관련이 있으며 다 합니다 [패키지 관리 모듈 명령을](/powershell/module/packagemanagement/?view=powershell-6) 일반 PowerShell 환경에서 사용할 수 있는 합니다. 특히 각 환경에 다른 사용할 수 없는 명령 및 동일한 이름 사용 하 여 명령을 해당 특정 인수에도 달라질 수 있습니다. Visual Studio에서 패키지 관리 콘솔을 사용 하는 경우 명령과이 있는 항목에 설명 된 인수를 적용 합니다.

| 일반적인 명령 | Description | NuGet 버전 |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | 프로젝트에 패키지 및 해당 종속성을 설치합니다. | 모두 |
| [Update-Package](ps-ref-update-package.md) | 프로젝트의 모든 패키지 및 해당 종속성 또는 패키지를 업데이트합니다. | 모두 |
| [Find-Package](ps-ref-find-package.md) | 패키지 ID 또는 키워드를 사용 하 여 패키지 소스를 검색 합니다. | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | 로컬 저장소에 설치 된 패키지 목록을 검색 하거나 패키지 원본에서 사용할 수 있는 패키지를 나열 합니다. | 모두 |

| 보조 명령 | 설명 | NuGet 버전 |
| --- | --- | --- |
| [Add-BindingRedirect](ps-ref-add-bindingredirect.md) | 프로젝트의 출력 경로 내의 모든 어셈블리를 검사 하 고에 바인딩 리디렉션을 추가 합니다 `app.config` 또는 `web.config` 필요한 경우. | 모두 |
| [Get-Project](ps-ref-get-project.md) | 기본 또는 지정 된 프로젝트에 대 한 정보를 표시합니다. | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | 프로젝트, 라이선스 또는 지정된 된 패키지에 대 한 URL 신고를 사용 하 여 기본 브라우저를 시작합니다. | 3\.0 이상에서 사용 되지 않음 |
| [Register-TabExpansion](ps-ref-register-tabexpansion.md) | 일반적으로 사용 되는 매개 변수 값에 대 한 사용자 지정된 확장을 만들 수 있도록 명령의 매개 변수에 대해 탭 확장을 등록 합니다. | 모두 |
| [Sync-Package](ps-ref-sync-package.md) | 패키지를 설치 하는 버전은 가져오기 프로젝트를 지정 하 고 솔루션에서 프로젝트의 나머지 부분에는 버전 동기화. | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | 필요에 따라 해당 종속성을 제거 하는 프로젝트에서 패키지를 제거 합니다. | 모두 |

콘솔 내에서 이러한 명령 중 하나에서 완전 하 고 자세한 도움이 필요 하면 해당 명령 이름을 사용 하 여 다음 실행:

```ps
Get-Help <command> -full
```

모든 패키지 관리자 콘솔 명령은 다음을 지원 [일반적인 PowerShell 매개 변수](http://go.microsoft.com/fwlink/?LinkID=113216):

- 디버그
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- 자세히
- WarningAction
- WarningVariable

자세한 내용은를 참조 [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) PowerShell 설명서에 있습니다.
