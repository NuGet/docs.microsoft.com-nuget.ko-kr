---
title: NuGet 3.0 RC 릴리스 정보
description: NuGet 3.0 RC 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr 포함에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551721"
---
# <a name="nuget-30-rc-release-notes"></a>NuGet 3.0 RC 릴리스 정보

[NuGet 3.0 베타 릴리스 정보](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 릴리스 정보](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC는 Visual Studio 2015 RC 릴리스를 사용 하 여 2015 년 4 월 29 일에 출시 되었습니다. 이 릴리스에 다양 한 중요 한 버그 수정, 성능 향상 및 새로운 프레임 워크를 지원 하도록 업데이트 합니다.  만 Visual Studio 2015 용 제공 됩니다.

### <a name="continued-focus-on-performance"></a>성능에 계속된 집중

NuGet 쿼리의 성능과 안정성에 집중 하는 활성 항목 수를 계속 합니다.  이 릴리스에서 NuGet UI 및 웹 사이트에서 매우 빠른 검색 작업을 보려면 보아야 합니다.  서비스 및 이러한 작업을 튜닝할 계속 수 있도록 서비스를 사용 하는 방법을 모니터링 합니다.

## <a name="significant-issues-resolved"></a>중요 한 문제 해결

NuGet 클라이언트를 안정화를 하기 위해이 릴리스의 일환으로 다양 한 문제를 해결 했습니다.  방금 간략 한 목록을 확인 하는 더 중요 한 문제 중 일부는 다음과 같습니다.

* ASP.NET 5 K 프레임 워크의 이름 바꾸기의 일환으로, 프레임 워크 모니커 하도록 업데이트 되었습니다 dnx 및 dnxcore 처리 [링크](https://github.com/NuGet/Home/issues/215)
* Visual Studio UI의 링크 도움말 설명서가 추가 [링크](https://github.com/NuGet/Home/issues/232)
* 더 복잡 한 참조 처리 `.nuspec` 쉼표로 구분 된 프레임 워크 참조를 사용 하 여 [링크](https://github.com/NuGet/Home/issues/276)
* 일본어 culture에 대 한 지원을 고정 [링크](https://github.com/NuGet/Home/issues/253)
* ASP.NET 5 프로젝트에서 새 v3 끝점을 사용 하려면 업데이트 된 클라이언트 [링크](https://github.com/NuGet/Home/issues/219)
* 소스 제어를 사용 하 여 핸들을 업데이트 된 패키지 폴더 [링크](https://github.com/NuGet/Home/issues/56)
* 위성 패키지에 대 한 지원을 고정 [링크](https://github.com/NuGet/Home/issues/17)
* 프레임 워크별 콘텐츠 파일에 대 한 지원 수정 [링크](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>GitHub 있는지 점검

일부 변경 내용을 만들었습니다 우리의 [GitHub에서 코드 리포지토리를 원본](http://github.com/nuget/home)합니다.  NuGet Visual Studio 클라이언트에서 Powershell 명령 또는 명령줄을 사용 하 여 문제가 발생 하는 경우 실행 이러한 문제를 로그 하에서 진행률을 모니터링할 우리의 [홈 GitHub 리포지토리 문제 목록](http://github.com/nuget/home/issues)합니다.  갤러리에 대 한 문제를 추적 하는 것이 [GitHub NuGetGallery 리포지토리](http://github.com/nuget/NuGetGallery/issues)합니다.


## <a name="stay-tuned"></a>계속 주목해 주세요

에 유의 하세요 [블로그에서](http://blog.nuget.org) 자세한 진행률 및 NuGet 3.0에 대 한 알림!