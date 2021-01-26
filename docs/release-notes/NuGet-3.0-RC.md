---
title: NuGet 3.0 RC 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 포함 하는 NuGet 3.0 RC에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776577"
---
# <a name="nuget-30-rc-release-notes"></a>NuGet 3.0 RC 릴리스 정보

[NuGet 3.0 베타 릴리스 정보](../release-notes/nuget-3.0-beta.md)  |  [NuGet 3.0 RC2 릴리스 정보](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC는 Visual Studio 2015 RC 릴리스를 사용 하 여 2015 년 4 월 29 일에 출시 되었습니다. 이 릴리스에는 새로운 프레임 워크를 지 원하는 많은 중요 한 버그 수정, 성능 향상 및 업데이트가 포함 되어 있습니다.  Visual Studio 2015 에서만 사용할 수 있습니다.

### <a name="continued-focus-on-performance"></a>성능에 계속 집중

NuGet 쿼리의 안정성 및 성능은 계속 집중 하는 핫 토픽입니다.  이 릴리스에서는 NuGet UI 및 웹 사이트에서 매우 빠른 검색 작업이 표시 되기 시작 합니다.  이러한 작업을 계속 튜닝할 수 있도록 서비스를 모니터링 하 고 서비스를 사용 하는 방법을 모니터링 하 고 있습니다.

## <a name="significant-issues-resolved"></a>해결 된 중요 한 문제

NuGet 클라이언트를 안정화 하기 위해이 릴리스의 일부로 많은 문제를 해결 했습니다.  다음은 해결 된 중요 한 문제 중 일부에 대 한 간단한 목록입니다.

* ASP.NET 5 용 K framework 이름 바꾸기의 일부로, 프레임 워크 모니커가 dnx 및 dnxcore [링크](https://github.com/NuGet/Home/issues/215) 를 처리 하도록 업데이트 되었습니다.
* Visual Studio UI [링크](https://github.com/NuGet/Home/issues/232) 의 링크에서 도움말 설명서를 추가 했습니다.
* `.nuspec`쉼표로 구분 된 프레임 워크 참조 [링크](https://github.com/NuGet/Home/issues/276) 를 사용 하 여에서 복잡 한 참조 처리 향상
* 일본어 문화권 [링크](https://github.com/NuGet/Home/issues/253) 에 대 한 지원 수정
* ASP.NET 5 프로젝트에서 새 v3 끝점 [링크](https://github.com/NuGet/Home/issues/219) 를 사용할 수 있도록 업데이트 된 클라이언트
* 소스 제어 [링크](https://github.com/NuGet/Home/issues/56) 를 사용 하 여 패키지 폴더를 더 잘 처리 하도록 업데이트 됨
* 위성 패키지에 대 한 지원 수정 [링크](https://github.com/NuGet/Home/issues/17)
* 프레임 워크 관련 콘텐츠 파일 [링크](https://github.com/NuGet/Home/issues/18) 에 대 한 수정 된 지원

## <a name="github-presence-overhaul"></a>GitHub 상태 재정비

[GitHub에서 소스 코드 리포지토리](http://github.com/nuget/home)를 변경 했습니다.  NuGet Visual Studio 클라이언트, Powershell 명령 또는 명령줄 실행 파일에 문제가 있는 경우 해당 문제를 기록 하 고 [GitHub 홈 리포지토리 문제 목록](http://github.com/nuget/home/issues)에서 진행 상황을 모니터링할 수 있습니다.  [GitHub NuGetGallery 리포지토리에서](http://github.com/nuget/NuGetGallery/issues)갤러리에 대 한 문제를 추적 하 고 있습니다.


## <a name="stay-tuned"></a>계속 조정

NuGet 3.0에 대 한 자세한 진행률과 공지 사항은 [블로그](http://blog.nuget.org) 를 확인 하세요.