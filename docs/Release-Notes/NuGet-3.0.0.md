---
title: "NuGet 3.0 릴리스 정보 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 3.0.0 포함에 대 한 릴리스 정보는 문제, 버그 수정, 추가 된 기능 및 Dcr 알려져 있습니다."
keywords: "NuGet 3.0.0 릴리스 정보, 버그 수정, 알려진 문제, 추가 기능을 Dcr"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ef8557c37105eb7915919c7b15d41d024921761f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-30-release-notes"></a>NuGet 3.0 릴리스 정보

[NuGet 3.0 RC2 릴리스 정보](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 릴리스 정보](../release-notes/nuget-3.1.md)

NuGet 3.0 2015 년 7 월 20 일에 Visual Studio 2015에 대 한 번들 확장으로 릴리스 되었습니다. Visual Studio와 함께이 릴리스를 전체 업데이트 된 NuGet 3.0 환경을 새 Visual Studio 사용자에 대해 사용할 수 있도록 제공 푸시되. 이 NuGet 확장 버전은 Visual Studio 2015에 사용할 수만 있습니다.

Windows 10 개발에 대 한 지원을 포함 하는 Visual Studio 2015 릴리스 직후 게시 업데이트 하는 것 처럼 사용할 수 있는 최신 버전에 대 한 Visual Studio 갤러리 업데이트에 액세스할 수 있는 개발자가 사용 하는 것이 좋습니다.

전체적으로 우리 3.0 버전에서 240 문제 닫히고 검토할 수 있습니다는 [문제 GitHub에서의 전체 목록은](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed)합니다.

## <a name="known-issues"></a>알려진 문제

여러 가지 알려진된 문제가이 릴리스에서 제공 했으며 이러한 항목을 모두 해결 우리의 예약 된 3.1 릴리스의 Windows 10 29th 년 7 월에 일치 하 게 합니다.  이러한 알려진된 문제를 해결 하려면 해당 날짜 또는 그 이후에 갤러리에서 Visual Studio 확장 프로그램을 업데이트할 수 있습니다.

*  미리 보기 창에 "이를 다시 표시 안" 레이블 및 패키지 설명 창에 "작성자" 레이블에 대 한 번역을 제공 되지 않았습니다.
*  TFS를 사용 하 여 프로젝트에서 작업 하면 소스 제어, NuGet 없습니다 제시 패키지 관리자 사용자 인터페이스 Nuget.Config 파일은 읽기 전용으로 표시 된 경우.
   * **해결 방법** TFS에서 파일을 체크 아웃 합니다.
*  Visual Studio 어두운 테마를 사용 하는 경우에 노란색 "다시 시작 막대" NuGet Powershell 창에서 텍스트 표시 되지 않습니다.
   * **해결 방법** Visual Studio 밝은 테마를 사용 합니다.


## <a name="summary-of-top-issues-resolved"></a>주요 문제 해결의 요약

* [패키지 관리자 창을 새로 고칠 때 자주 네트워크 업데이트 호출](https://github.com/NuGet/Home/issues/515)
* [패키지 관리자에 보기를 설치를 변경 하면 스크롤 지연](https://github.com/NuGet/Home/issues/519)
* [백그라운드 스레드에서 네트워크 호출을 실행 해야](https://github.com/NuGet/Home/issues/516)
* ['미리 보기 창 표시 안 함' 확인란을 추가합니다.](https://github.com/NuGet/Home/issues/566)
* [추가 된 프로세스 프로세서 사용량을 줄이기 위해 조절](https://github.com/NuGet/Home/issues/356)
* 쉽게 이식 가능한 클래스 라이브러리 참조 처리
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [자동 완성 서비스에서 대/소문자 구분](https://github.com/NuGet/Home/issues/198)
* [기본 인증 자격 증명을 다시 삽입 하는 업데이트](https://github.com/NuGet/Home/issues/456)
* [향상 된 오류 로깅](https://github.com/NuGet/Home/issues/407)
* [업데이트 패키지를 호출할 때 향상 된 powershell 오류 메시지](https://github.com/NuGet/Home/issues/5)
* [Windows 10에서 충돌을 방지 하기 위해 '옵션에 대 한 자세한 정보' 링크를 고정 합니다.](https://github.com/NuGet/Home/issues/822)
* [시험판 확인란 설정을 기억 합니다.](https://github.com/NuGet/Home/issues/732)
* [솔루션의 프로젝트에서 결과 캐시 하 여 향상 된 수집 성능](https://github.com/NuGet/Home/issues/721)
* [동시에 여러 패키지를 수집할 수 있습니다.](https://github.com/NuGet/Home/issues/713)
* [설치 패키지를 제거-강제로 명령](https://github.com/NuGet/Home/issues/697)

에 유의 하십시오 [블로그에서](http://blog.nuget.org) 자세한 진행률 및 공지에 대 한 대로 Windows 10 개발에 대 한 지원을 제공 하도록 합니다.