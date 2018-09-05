---
title: NuGet 3.1 릴리스 정보
description: NuGet 3.1의 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545349"
---
# <a name="nuget-31-release-notes"></a>NuGet 3.1 릴리스 정보

[NuGet 3.0 릴리스 정보](../release-notes/nuget-3.0.0.md) | [3.1.1 NuGet 릴리스 정보](../release-notes/nuget-3.1.1.md)

NuGet 3.1는 Visual Studio 2015 용 유니버설 Windows 플랫폼 SDK에 포함 된 확장으로 2015 년 7 월 27 일에 출시 되었습니다. Windows 개발 환경을 이전에 시작 되는 NuGet 플랫폼 간 작업을 활용할 수 있도록 Windows Platform SDK를 사용 하 여이 릴리스를 전달 했습니다. 이 NuGet 확장 버전에만 Visual Studio 2015 용 제공 됩니다.

Visual Studio 갤러리 업데이트를 사용할 수 있는, 버그 수정 및 새로운 기능을 사용 하 여 업데이트 게시 항상 최신 버전에 액세스할 수 있는 개발자를 위해를 사용 하는 것이 좋습니다.

## <a name="nuget-visual-studio-extension"></a>NuGet Visual Studio 확장

문제 및 기능을 사용 하 여 GitHub에서 태그가 지정 되어는 [""3.1 RTM UWP 전이적 지원 마일스 톤](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) 67 3.1 릴리스의 문제 전체적으로 종료 합니다.

### <a name="new-features"></a>새 기능

* `project.json` Windows UWP 및 ASP.NET 5 지원
* 전이적 패키지 설치

설명 및 이러한 기능의 정의 설명서의 다른 곳에서 찾을 수 있습니다.

### <a name="deprecated"></a>사용 되지 않음

다음 기능은 Visual Studio 2015에 사용할 수 있는 더 이상:

* 솔루션 수준 패키지를 더 이상 설치할 수 없습니다.

다음 기능은 더 이상 Visual Studio 2015 및 사용 하는 프로젝트에 사용할 수는 `project.json` 사양

* `install.ps1` 및 `uninstall.ps1` -이러한 스크립트는 패키지 설치 동안 무시 됩니다, 복원, 업데이트 및 제거
* 구성 변환 무시 됩니다.
* 콘텐츠를 전달 되지만 프로젝트로 복사 되지 않습니다.
    * 팀은 다시이 기능을 구현 하 고 토론 팔 로우에 진행률: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>알려진 문제

이 릴리스에 포함 된 알려진된 문제가 많이 있었습니다.

* Windows 10 SDK를 사용 하 여 3.1 릴리스의 설치 이전에 설치 된 NuGet 확장의 버전을 다운 그레이드할 수 있습니다.

## <a name="nuget-command-line"></a>NuGet 명령줄

NuGet 명령줄 실행 파일에 업데이트 되어 사용할 수 있도록 nuget.exe의 기록 버전이 계속할 수 있도록 새로운 배포 가능한 위치로 이동 합니다.  Windows에 대 한 nuget.exe의 3.1 베타 버전을 다운로드할 수 있습니다. [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

새 배포 가능한 위치는이 템플릿에 폴더 구조를 사용 하 여 dist.nuget.org 호스트에 상주 합니다.

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>새 기능

* nuget.exe를 복원 하 고 패키지를 사용 하는 프로젝트에 설치할 수는 `project.json` 파일입니다.
* nuget.exe에 연결 하 고에서 NuGet v3 프로토콜을 사용할 수 있습니다. [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>알려진 문제 ##

1.    팩에 대해 실행할 수 없습니다는 `project.json` 파일- [928](https://github.com/NuGet/Home/issues/928)
2.    Mono-지원 되지 않습니다 [1059](https://github.com/NuGet/Home/issues/1059)
3.    -지역화 되지 않은 [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    기존 마찬가지로 서명 되지 않은 http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)
