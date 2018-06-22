---
title: NuGet 3.0 RC 릴리스 정보
description: NuGet 3.0 RC 알려진된 문제, 버그 수정, 추가 된 기능 및 Dcr를 포함 하 여에 대 한 릴리스 정보입니다.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 28ac49d9e9071d16d20b24808abb0acaab214ffd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819600"
---
# <a name="nuget-30-rc-release-notes"></a>NuGet 3.0 RC 릴리스 정보

[NuGet 3.0 베타 릴리스 정보](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 릴리스 정보](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC와 Visual Studio 2015 RC 릴리스 2015 년 4 월 29 일에 출시 되었습니다. 이 릴리스에 다양 한 중요 한 버그 수정, 성능 향상 및 새 프레임 워크를 지 원하는 업데이트에 있습니다.  Visual Studio 2015 용만 가능 합니다.

### <a name="continued-focus-on-performance"></a>성능에 계속된 포커스가

NuGet 쿼리의 안정성과 성능을 계속에 집중 하는 활성 항목 수 있습니다.  이 릴리스에서 NuGet UI와 웹 사이트에서 매우 빠른 검색 작업을 보려면 시작 해야 합니다.  서비스와 이러한 작업을 튜닝에 도움이 될 수 있도록 서비스 사용을 모니터링 하는 것입니다.

## <a name="significant-issues-resolved"></a>중요 한 문제 해결

NuGet 클라이언트가 안정화 하기 위해이 릴리스의 일부로 서 다양 한 문제 해결.  간략 한 목록만 더 중요 한 문제를 해결 중 일부는 다음과 같습니다.

* ASP.NET 5에 대 한 K 프레임 워크의 이름 바꾸기의 일환으로, 프레임 워크 모니커 하도록 업데이트 되었습니다 dnx 및 dnxcore 처리 [링크](https://github.com/NuGet/Home/issues/215)
* Visual Studio UI에서 링크에서 도움말 문서 추가 [링크](https://github.com/NuGet/Home/issues/232)
* 복잡 한 참조를 더 잘 처리 `.nuspec` 쉼표로 구분 된 프레임 워크 참조와 [링크](https://github.com/NuGet/Home/issues/276)
* 일본어 culture에 대 한 지원 고정 [링크](https://github.com/NuGet/Home/issues/253)
* ASP.NET 5 프로젝트에서 새 v3 끝점을 사용 하려면 업데이트 된 클라이언트 [링크](https://github.com/NuGet/Home/issues/219)
* 소스 제어와 핸들을 보다 잘 업데이트 된 패키지 폴더 [링크](https://github.com/NuGet/Home/issues/56)
* 위성 패키지에 대 한 지원 고정 [링크](https://github.com/NuGet/Home/issues/17)
* 프레임 워크 관련 콘텐츠 파일에 대 한 지원을 수정 [링크](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>GitHub 존재 정비

일부 변경 내용을 만들었고 우리의 [GitHub에서 코드 저장소를 원본](http://github.com/nuget/home)합니다.  Visual Studio 클라이언트, Powershell 명령 또는 명령줄 문제가 있는 경우 실행 문제 별로 로그 있고에서 진행 상황을 모니터링 우리의 [홈 GitHub 리포지토리 문제 목록](http://github.com/nuget/home/issues)합니다.  갤러리에 대 한 문제를 추적 하는 것이 [GitHub NuGetGallery 리포지토리](http://github.com/nuget/NuGetGallery/issues)합니다.


## <a name="stay-tuned"></a>기대

에 유의 하십시오 [블로그에서](http://blog.nuget.org) 자세한 진행률 및 NuGet 3.0에 대 한 공지 사항!