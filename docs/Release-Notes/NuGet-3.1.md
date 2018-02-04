---
title: "NuGet 3.1 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여 NuGet 3.1에 대 한 릴리스 정보입니다."
keywords: "NuGet 3.1 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a7aa43b8701b3bbef8f6ebce9a5d636ee1bc6abe
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-31-release-notes"></a>NuGet 3.1 릴리스 정보

[NuGet 3.0 릴리스 정보](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1 릴리스 정보](../release-notes/nuget-3.1.1.md)

NuGet 3.1는 Visual Studio 2015 용 유니버설 Windows 플랫폼 SDK에 대 한 번들로 묶은 확장으로 2015 년 7 월 27 일에 출시 되었습니다. Windows 개발 환경을 이전에 시작 된 NuGet 플랫폼 간 작업을 이용할 수 있도록 Windows 플랫폼 SDK와 함께이 릴리스를 제공 합니다. 이 NuGet 확장 버전은 Visual Studio 2015에 사용할 수만 있습니다.

Visual Studio 갤러리 업데이트를 사용할 수 있는, 버그 픽스와 새로운 기능을 사용 하 여 업데이트 게시 항상 최신 버전에 액세스할 수 있는 개발자가 사용 하는 것이 좋습니다.

## <a name="nuget-visual-studio-extension"></a>NuGet Visual Studio 확장

문제 및이 릴리스의 기능에에서 포함 된 GitHub의 태그가 지정 됩니다는 ["3.1 RTM UWP 전이적 지원" 마일스 톤](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) 전체적으로 67 3.1 릴리스의 문제 종료 했습니다.

### <a name="new-features"></a>새 기능

* `project.json`ASP.NET 5 및 Windows UWP 지원에 대 한 지원
* 전이적 패키지 설치

설명 및 이러한 기능의 정의 설명서의 다른 곳에서 찾을 수 있습니다.

### <a name="deprecated"></a>사용 되지 않음

Visual Studio 2015에 대 한 다음과 같은 기능을 더 이상:

* 솔루션 수준 패키지 더 이상 설치할 수 없습니다.

Visual Studio 2015 및 사용 하는 프로젝트에 대 한 다음과 같은 기능을 더 이상는 `project.json` 사양

* `install.ps1`및 `uninstall.ps1` -이러한 스크립트 패키지 설치 중에 무시 됩니다, 복원, 업데이트 및 제거
* 구성 변환은 무시 합니다.
* 콘텐츠 배달, 되지만 프로젝트에 복사 되지 않습니다.
    * 다시이 기능을 구현 하 여 토론에 따라에서 진행 되는 팀이 작업: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>알려진 문제

이 릴리스와 함께 제공 되는 알려진된 문제 수가 있었습니다.

* Windows 10 SDK를 사용 하 여 3.1 릴리스 설치 이전에 설치 된 NuGet 확장의 모든 버전을 다운 그레이드할 수 있습니다.

## <a name="nuget-command-line"></a>NuGet 명령줄

NuGet 명령줄 실행 파일은 업데이트 되어 사용할 수 있도록 기록 버전의 nuget.exe 계속할 수 있도록 새로운 배포 가능한 위치로 이동 합니다.  Windows 용 nuget.exe의 3.1 베타 버전을 다운로드할 수 있습니다: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

새 배포 가능한 위치 뒤에 오는이 서식 파일 폴더 구조와 dist.nuget.org 호스트에 상주 합니다.

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>새 기능

* nuget.exe 복원 하 고 사용 하는 프로젝트에 패키지를 설치할 수는 `project.json` 파일입니다.
* nuget.exe에 연결할 수 있고에서 NuGet v3 프로토콜을 사용: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>알려진 문제 ##

1.    팩에 대해 실행할 수 없습니다 한 `project.json` 파일- [928](https://github.com/NuGet/Home/issues/928)
2.    모노-지원 되지 않습니다 [1059](https://github.com/NuGet/Home/issues/1059)
3.    지역화 되지 않은- [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    기존 http://nuget.org/nuget.exe-와 동일 하 게 서명 되지 않은 [1073](https://github.com/NuGet/Home/issues/1073)
