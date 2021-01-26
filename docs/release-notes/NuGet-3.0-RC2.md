---
title: NuGet 3.0 RC2 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 Ecrs를 비롯 한 NuGet 3.0 r c 2에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 355c200481f4acba9931dc3bcd85e99c5ffbf224
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780275"
---
# <a name="nuget-30-rc2-release-notes"></a>NuGet 3.0 RC2 릴리스 정보

[NuGet 3.0 RC 릴리스 정보](../release-notes/nuget-3.0-RC.md)  |  [NuGet 3.0 릴리스 정보](../release-notes/nuget-3.0.0.md)

NuGet 3.0 r c 2는 Visual Studio 2015 확장 갤러리 및 [Codeplex](https://nuget.codeplex.com/releases/view/615507)에서 사용할 수 있는 중간 릴리스로 2015 년 6 월 3 일에 릴리스 되었습니다. 이 릴리스에는 전체 Visual Studio 2015 릴리스 전에 릴리스 하는 것이 중요 한 여러 가지 중요 한 버그 수정 및 성능 향상이 있습니다. 이 NuGet 확장 버전은 Visual Studio 2015 에서만 사용할 수 있습니다.

이 릴리스에서는 총 158 개의 문제를 해결 하 고 [GitHub에서 전체 문제 목록을](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A3.0.0-RTM+sort%3Aupdated-asc+updated%3A%3C%3D2015-06-01)검토할 수 있습니다.

## <a name="summary-of-top-issues-resolved"></a>해결 된 주요 문제 요약

* [패키지 관리자 창이 새로 고쳐질 때 네트워크 업데이트 호출이 자주 발생 합니다.](https://github.com/NuGet/Home/issues/515)
* [패키지 관리자에서 설치 된 뷰로 변경할 때 지연 된 스크롤](https://github.com/NuGet/Home/issues/519)
* [네트워크 호출은 백그라운드 스레드에서 실행 되어야 합니다.](https://github.com/NuGet/Home/issues/516)
* [' 미리 보기 창 표시 안 함 ' 확인란 추가 됨](https://github.com/NuGet/Home/issues/566)
* [프로세서 사용량을 줄이기 위해 프로세스 제한을 추가 했습니다.](https://github.com/NuGet/Home/issues/356)
* 이식 가능한 클래스 라이브러리 참조 처리 향상
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [자동 완성 서비스의 대/소문자 구분](https://github.com/NuGet/Home/issues/198)
* [기본 인증 자격 증명을 새로 소개할 업데이트](https://github.com/NuGet/Home/issues/456)
* [오류 로깅이 개선되었습니다.](https://github.com/NuGet/Home/issues/407)
* [업데이트 패키지를 호출할 때 향상 된 powershell 오류 메시지](https://github.com/NuGet/Home/issues/5)

Codeplex의 [nuget 확장에이 업데이트를](https://nuget.codeplex.com/releases/view/615507) 다운로드 하 고 nuget 3.0에 대 한 자세한 진행 및 공지 사항은 [블로그](http://blog.nuget.org) 를 주시 하세요.