---
title: NuGet 3.0 릴리스 정보
description: NuGet 3.0.0 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551865"
---
# <a name="nuget-30-release-notes"></a>NuGet 3.0 릴리스 정보

[NuGet 3.0 RC2 릴리스 정보](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 릴리스 정보](../release-notes/nuget-3.1.md)

NuGet 3.0은 Visual Studio 2015에 대 한 번들 확장으로 2015 년 7 월 20 년에 출시 되었습니다. Visual Studio를 사용 하 여이 릴리스는 완벽 한 업데이트 된 NuGet 3.0 환경을 새 Visual Studio 사용자에 대해 사용할 수 있도록 전달할 푸시 했습니다. 이 NuGet 확장 버전에만 Visual Studio 2015 용 제공 됩니다.

Windows 10 개발에 대 한 지원을 포함 하는 Visual Studio 2015의 릴리스 직후 게시를 업데이트 하는 것 처럼 사용할 수 있는 최신 버전으로 Visual Studio 갤러리 업데이트에 액세스할 수 있는 개발자를 위해를 사용 하는 것이 좋습니다.

3.0 릴리스에서 240 문제 전체적으로 종료 하 고 검토할 수 있습니다 합니다 [목록은 GitHub에서 문제](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)합니다.

## <a name="known-issues"></a>알려진 문제

이 릴리스에 포함 된 알려진 문제가 많았습니다 및 이러한 항목을 모두는 29 년 7 월에 Windows 10의 출시와 일치 하는 예약 된 3.1 릴리스에서 해결 되었습니다.  이러한 알려진된 문제를 해결 하려면 해당 날짜 또는 그 이후에 갤러리에서 Visual Studio 확장 프로그램을 업데이트할 수 있습니다.

*  변환 미리 보기 창에서 "다시 표시 안 이" 레이블 및 패키지 설명 창에 "작성자" 레이블을 제공 되지 않습니다.
*  TFS를 사용 하 여 프로젝트에서 작업 하면 소스 제어, NuGet 없습니다 제시 패키지 관리자 사용자 인터페이스 Nuget.Config 파일이 읽기 전용으로 표시 된 경우.
   * **해결 방법** TFS에서 파일을 체크 아웃 합니다.
*  Visual Studio 어두운 테마를 사용 하는 경우에 텍스트 "다시 시작 표시줄" NuGet Powershell 창에서 노란색으로 표시 되지 않습니다.
   * **해결 방법** Visual Studio 밝은 테마를 사용 합니다.


## <a name="summary-of-top-issues-resolved"></a>가장 중요 한 문제 해결의 요약

* [패키지 관리자 창을 새로 고칠 때 자주 네트워크 업데이트 호출](https://github.com/NuGet/Home/issues/515)
* [패키지 관리자에서 보기를 설치 하려면 변경 하는 경우 스크롤 지연](https://github.com/NuGet/Home/issues/519)
* [네트워크 호출을 백그라운드 스레드에서 실행할지](https://github.com/NuGet/Home/issues/516)
* ['미리 보기 창 표시 안 함' 확인란을 추가합니다.](https://github.com/NuGet/Home/issues/566)
* [프로세서 사용량을 줄이기 위해 제한 하는 추가 프로세스](https://github.com/NuGet/Home/issues/356)
* 개선 된 이식 가능한 클래스 라이브러리 참조 처리
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [자동 완성 service가 대/소문자 구분](https://github.com/NuGet/Home/issues/198)
* [기본 인증 자격 증명을 다시 삽입 하는 업데이트](https://github.com/NuGet/Home/issues/456)
* [향상 된 오류 로깅](https://github.com/NuGet/Home/issues/407)
* [업데이트 패키지를 호출할 때 개선 된 powershell 오류 메시지](https://github.com/NuGet/Home/issues/5)
* [Windows 10에서 충돌을 방지 하기 위해 '옵션에 대 한 자세한' 링크를 고정 합니다.](https://github.com/NuGet/Home/issues/822)
* [시험판 확인란 설정](https://github.com/NuGet/Home/issues/732)
* [솔루션의 프로젝트에서 결과 캐시 하 여 향상 된 수집 성능](https://github.com/NuGet/Home/issues/721)
* [병렬로 여러 패키지를 수집할 수 있습니다.](https://github.com/NuGet/Home/issues/713)
* [설치 패키지를 제거-강제로 명령](https://github.com/NuGet/Home/issues/697)

에 유의 하세요 [블로그에서](http://blog.nuget.org) 진행률와 공지 사항이 많아졌습니다에 대 한 Windows 10 개발에 대 한 지원을 제공할 준비가 될 때입니다.