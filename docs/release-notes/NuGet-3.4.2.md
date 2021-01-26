---
title: NuGet 3.4.2 릴리스 정보
description: 알려진 문제, 버그 수정, 추가 된 기능 및 3.4.2를 포함 하는 NuGet에 대 한 릴리스 정보입니다.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780253"
---
# <a name="nuget-342-release-notes"></a>NuGet 3.4.2 릴리스 정보

[NuGet 3.4.1 릴리스 정보](../release-notes/nuget-3.4.1.md)  |  [NuGet 3.4.3 릴리스 정보](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2는 3.4 및 3.4.1 릴리스에서 식별 된 몇 가지 문제를 해결 하기 위해 2016 년 4 월 8 일에 릴리스 되었습니다.

## <a name="nugetexe-342-rc-is-now-available"></a>이제 nuget.exe 3.4.2 RC를 사용할 수 있습니다.

nuget.exe 3.4.2의 릴리스 후보는 [여기](https://dist.nuget.org/index.html)에서 다운로드할 수 있습니다.

## <a name="updates-and-improvements"></a>업데이트 및 개선 사항

* 심층 종속성 그래프가 포함 된 패키지에 대 한 업데이트는 매우 긴 시간이 소요 되 고 Visual Studio가 중단 되는 특정 시나리오의 업데이트 성능이 크게 향상 되었습니다.
* 네트워크 트래픽이 없는 nuget 복원은 Visual Studio 내에서 2.5 x – 3 배 빠릅니다.
* 이와 같이 변경 하는 것 외에도 VS UI에서 업데이트 횟수를 가져올 때 네트워크를 두 번 적중 하는 문제를 해결 했습니다. 이는 3.4/3.4.1에서 발생 하는 몇 가지 제한 시간 문제를 부분적으로 담당 했습니다.
* No_proxy 설정에 대 한 지원 추가

## <a name="fixes"></a>수정 프로그램

* 3.4.1로 업데이트 한 후 NuGet 설정 또는 구성에 nuget.org 원본이 없는 문제를 해결 했습니다.
* 3.4.1의 FindPackagesById에 대 한 대/소문자 변경이 Artifactory를 중단 하는 문제를 해결 했습니다.
* nuget.exe를 사용 하 여 NuGet 복원에 실패 한 FIPS 문제를 수정 했습니다.
* 잘못 된 아이콘 URL을 사용 하 여 소스를 검색할 때 충돌이 해결 되었습니다.
* ' 모든 원본 '의 병합 버전 및 항목과 관련 된 문제를 해결 했습니다.

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>3.4.2 Windows x86 Commandline (RC)의 알려진 문제

이러한 문제는 RTM에 도달 하기 전에 다음 주 이전에 수정 될 예정입니다.

*  솔루션 파일이 프로젝트 파일 보다 하위 폴더 계층 구조에 배치 되 면 솔루션에 대해 nuget 복원 실행이 실패 합니다.
*  V2 피드를 사용 하 여 패키지에서 nuget delete 명령을 실행 하는 것은 실패 합니다. 대신 V3 피드를 사용 하십시오.


이 릴리스의 수정 사항 및 개선 사항에 대 한 전체 목록은 [여기](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)에서 문제 목록을 확인 하세요.