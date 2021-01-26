---
title: NuGet 3.1 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 3.1에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776539"
---
# <a name="nuget-31-release-notes"></a>NuGet 3.1 릴리스 정보

[NuGet 3.0 릴리스 정보](../release-notes/nuget-3.0.0.md)  |  [NuGet 3.1.1 릴리스 정보](../release-notes/nuget-3.1.1.md)

NuGet 3.1는 Visual Studio 2015 용 유니버설 Windows 플랫폼 SDK에 대 한 번들로 제공 되는 확장으로, 2015 7 월 27 일에 출시 되었습니다. Windows 개발 환경에서 이전에 시작 된 NuGet 플랫폼 간 작업을 활용할 수 있도록 Windows Platform SDK를 사용 하 여이 릴리스를 제공 했습니다. 이 NuGet 확장 버전은 Visual Studio 2015 에서만 사용할 수 있습니다.

항상 버그 수정과 새로운 기능을 사용 하 여 업데이트를 게시 하므로 사용 가능한 최신 버전에 대 한 Visual Studio 갤러리 업데이트에 액세스할 수 있는 개발자를 사용 하는 것이 좋습니다.

## <a name="nuget-visual-studio-extension"></a>NuGet Visual Studio 확장

이 릴리스의 문제 및 기능에는 ["3.1 RTM UWP 전이적 지원" 마일스 톤](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  이 포함 된 GitHub에 태그가 지정 되어 있습니다. 3.1 릴리스에서 67 문제가 종결 되었습니다.

### <a name="new-features"></a>새로운 기능

* `project.json` Windows UWP 및 ASP.NET 5 지원 지원
* 전이적 패키지 설치

이러한 기능의 설명 및 정의는 설명서의 다른 위치에서 찾을 수 있습니다.

### <a name="deprecated"></a>사용되지 않음

Visual Studio 2015에는 다음 기능을 더 이상 사용할 수 없습니다.

* 솔루션 수준 패키지는 더 이상 설치할 수 없습니다.

다음 기능은 Visual Studio 2015 및 해당 사양을 사용 하는 프로젝트에서 더 이상 사용할 수 없습니다. `project.json`

* `install.ps1` 및 `uninstall.ps1` -이러한 스크립트는 패키지 설치, 복원, 업데이트 및 제거 중에 무시 됩니다.
* 구성 변환이 무시 됩니다.
* 콘텐츠는 전달 되지만 프로젝트에는 복사 되지 않습니다.
    * 팀에서이 기능을 다시 구현 하기 위해 작업 하 고 있습니다. 다음의 설명 및 진행률을 따르세요. [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>알려진 문제

이 릴리스와 함께 제공 되는 알려진 문제에는 여러 가지가 있습니다.

* Windows 10 SDK를 사용 하 여 3.1 릴리스를 설치 하면 이전에 설치 된 NuGet 확장 버전이 다운 그레이드 됩니다.

## <a name="nuget-command-line"></a>NuGet 명령줄

NuGet 명령줄 실행 파일을 업데이트 하 고 새 배포 가능한 위치로 이동 했으므로 nuget.exe의 기록 버전을 계속 사용할 수 있습니다.  Windows 용 nuget.exe의 3.1 베타 버전은 다음 위치에서 다운로드할 수 있습니다. [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

새 배포 가능한 위치는이 템플릿 뒤에 오는 폴더 구조를 사용 하 여 dist.nuget.org 호스트에 있습니다.

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a>새로운 기능

* nuget.exe 파일을 사용 하는 프로젝트에 패키지를 복원 하 고 설치할 수 있습니다 `project.json` .
* nuget.exe에서 NuGet v3 프로토콜에 연결 하 고 사용할 수 있습니다. [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>알려진 문제 ##

1.    파일에 대해 pack을 실행할 수 없습니다. `project.json` - [928](https://github.com/NuGet/Home/issues/928)
2.    Mono- [1059](https://github.com/NuGet/Home/issues/1059) 에서는 지원 되지 않습니다.
3.    지역화 되지 않음- [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)
4.    은 (는) 기존 1073와 마찬가지로 서명 되지 않습니다. http://nuget.org/nuget.exe  -  [](https://github.com/NuGet/Home/issues/1073)
